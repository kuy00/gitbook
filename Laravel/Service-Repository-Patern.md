# 서론
- 라라벨로 프로젝트 개발을 진행하면서 컨트롤러에 모든 비즈니스 로직을 작성하고 있음.
- 이로 인해 비즈니스 로직을 다른 컨트롤에서 재사용이 불가능하여 중복 코드를 작성하고 있음.
- 중복 코드가 계속 작성되면서 유지보수, 디버깅 시 어려움이 있어 이러한 구조를 버림.
- Service, Repository를 추가하여 컨트롤러에서 비즈니스 로직 분리, 비즈니스 로직에서 데이터 레이어를 분리하였음.

# 구조 설계
- Controller는 Service를 의존함
- Service는 Reposistory를 의존함
- 각 계층에 적절한 책임을 전가

## Controller
- 요청에 대한 유효성 검사 
- 응답 값 핸들링
```php
class ProductController extends Controller
{
    private $productService;

    public function __construct(ProductService $productService)
    {
        $this->productService = $productService;
    }

    public function store(ProductRequest $request)
    {
        $response = [
            'result' => true,
           'message' => '상품 등록 성공',
           'data' => [],
        ];

        try {
            $validated = $request->validated();
            $response['data'] = $this->productService->create($validated);
        } catch (\Throwable $th) {
            $response['result'] = false;
            $response['message'] = $th->getMessage();
        }

        return $response;
  }
}
```

## Service
- 비즈니스 로직을 작성
- 트랜잭션 관리
- Exception 처리
```php
class ProductService extends CRUDBaseService
{
    private $variantService;

    public function __construct(ProductRepository $productRepository, VariantService $variantService)
    {
        $this->repository = $productRepository;
        $this->variantService = $variantService;
    }

    public function create($data = null)
    {
        $product = [];

        try {
            DB::beginTransaction();

            $product = parent::create($data);
            foreach ($data['variants'] as $key => $value) {
                $value['product_id'] = $product->id;
                $this->variantService->create($value);
            }
            $product->variants;

            DB::commit();
        } catch (\Throwable $th) {
            DB::rollback();
            throw new \Exception('상품 등록 실패');
        }

        return $product;
    }
}
```

## Repository
- 데이터 로직을 작성
- 라라벨 모델과 직접 통신
```php
class BaseRepository implements RepositoryInterface
{
    private $model;

    public function create($data = [])
    {
        return $this->model->create($data);
    }
}
```

# 구현
- https://github.com/kuy00/service-repository-pattern-by-laravel