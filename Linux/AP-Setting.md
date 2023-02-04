# 접속 가능 AP 리스트 확인
```sh
iwlist {interface-name} scan
```
- interface-name: 네트워크 인터페이스

# 보안 없는 AP 연결
- ssid: 무선인터넷 이름
```bash
iwconfig {interface-name} essid {ssid}
```

# WPA AP 연결

## WPA PSK 파일 생성
```bash
wpa_passphrase {ssid} {password} > /etc/wpa_supplicant/wpa_supplicant.conf 
```

## 수동 연결
```bash
wpa_supplicant -B -i {interface-name} -c /etc/wpa_supplicant/wpa_supplicant.conf
```

## 서비스 등록을 통한 자동연결
- /etc/init.d 하위에 스크립트 생성
```bash
ex) ap-conecction

    #! /bin/sh

    ### BEGIN INIT INFO
    # Provides: ap-connection
    # Required-Start:
    # Required-Stop:
    # Default-Start: 2 3 4 5
    # Default-Stop:
    # Short-Description: auto connection AP
    ### END INIT INFO

    case $1 in
        start)
            echo "Down eth0 Interface"
            sudo ifconfig eth0 down

            echo "Up wlan0 Interface"
            sudo ifconfig wlan0 up

            echo "Connection AP"
            sudo wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant/wpa_supplicant.conf
            ;;
        stop)
            echo "Up eth0 Interface"
            sudo ifconfig eth0 up

            echo "Down wlan0 Interface"
            sudo ifconfig wlan0 down
            ;;
        restart)
            echo "Connection AP"
            sudo wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant/wpa_supplicant.conf
            ;;
    esac

    exit 0
```
- 생성된 스크립트 권한 설정 및 서비스 등록
```bash
chmod +x ap-connection
update-rc.d ap-connection defaults
```
- 서비스 등록 여부 확인
```bash
ls /etc/rc*/*ap-connection
```
- 재시작 후 ap connection 여부 확인
```bash
iwconfig
```

# 자동 IP 할당
```bash
dhclient {interface-name}
```

# 고정 IP 할당
- netplan 설정 파일 추가 - /etc/netplan
```bash
ex) 10-wifi-static-init.yaml
network:
    wifis:
        wlan0:
            optional: true
            addresses:
                - {ip}/24
            routes:
                - to: default
                    via: {gateway}
            access-points:
                {ssid}:
                    password: {password}
    version: 2
```
- netplan 적용 및 확인
```bash
netplan generate
netplan apply
```