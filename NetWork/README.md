# 면접을 위한 CS 전공 지식 노트 - 2.네트워크

태그: BOOK
생성 일시: 2023년 11월 25일 오후 3:29

# 2. 네트워크

## 2.1 네트워크 기초

### 네트워크

- 장치들이 통신 기술을 이용하는 구축하는 연결망의 의미함
- node와 Link가 서로 연결되어 있거나 연결되어 있으며 리소스를 공유하는 집합을 의미함
    - node : server, router, switch 등 네트워크 장비를 의미함
        
        ![Untitled](img/Untitled.png)
        

### 2.1.1 처리량과 지연 시간

- 좋은 네트워크 : 많은 처리량을 처리할 수 있으며 지연 시간이 짧고 장애 빈도가 적고 안전한 보안성을 가진 네트워크

**처리량(throughput)**

- 링크 내에서 성공적으로 전달된 데이터의 양의 말함  = 얼만큼의 트랙픽 처리
- 처리량이 충분하다 = 많은 트랙픽을 감당할 수 있다.
- 단위로는 bps(bit per second)를 사용함 :  초당 수신되는 비트의 수
- 트래픽 : 링크 내 흐르는 데이터의 양 _ 서버에 저장된 파일을 클라이언트에서 다운로드할 때 발생되는 데이터의 누적량

대역폭 : 주어진 시간 동안 네트워크 연결을 통해 흐를 수 있는 최대 비트 수를 의미함 

**지연시간(latency)**

- 요청이 처리되는 시간을 말함 → 메세지가 두 장치 사이를 왕복하는데 걸리는 시간을 의미
- 지연 시간은 매체 타입, 패킷 크기, 라우터의 패킷 처리 시간에 영향을 받음

![Untitled](img/Untitled%201.png)

### 2.1.2 네트워크 병목 현상 : 토폴로지

**네트워크 토폴로지**

- 노드와 링크가 어떻게 배치되어 있는지에 대한 방식이자 연결 형태를 의미함

트리 토폴로지 

- 계층형 토폴로지라고 하며 트리 형태로 배치한 네트워크 구성을 의미
- 노드 추가 삭제가 쉬우며 트래픽이 집중될 때 하위 노드에 영향을 끼칠 수 있음

![Untitled](img/Untitled%202.png)

버스 토폴로지 

- 중앙 통신 회선 하나에 여러 개의 노드가 연결되어 공유하는 네트워크 구성을 의미함 LAN에서 많이 사용된다
- 설치 비용이 적고 신뢰성이 우수함 _ 스푸핑에 대한 위험이 존재한다
    - 스푸핑 : LAN 상에서 송신부의 패킷을 송신과 상관없는 다른 호스트에게 가지 않도록 스위칭하는 기능을 마비시키거나 속여서 특정 노드에 해당 패킷이 오도록 처리하는 것을 의미함

![Untitled](img/Untitled%203.png)

![Untitled](img/Untitled%204.png)

스타 토폴로지 

- 중앙에 있는 노드에 모두가 연결되어있는 구성을 의미함
- 노드 추가 및 에러 탐지 용이, 노드끼리의 간섭이 없음 다만 중앙에 오류가 발생하면 전부 마비되고 설치비용이 비싸다는 단점이 존재함

![Untitled](img/Untitled%205.png)

링형 토폴로지 

- 각각의 노드가 양 옆의 두 노드와 연결하여 전체적으로 고리처럼 하나의 연속된 길을 통해 통신하는 구조를 의미함
- 네트워크 구성 변경이 어렵다는 단점이 존재하며 회선에 장애라도 발생하면 네트워크 전체에 큰 영향이 있음

![Untitled](img/Untitled%206.png)

메시 토폴로지 

- 망형 토폴리지
- 한 단말에 장애가 발생하더라고 여러 개의 경로가 존재함으로 네트워크 지속적으로 사용할 수 있고, 트래픽 분산 처리도 가능하다. 노드 구축이 어려움 운용비용이 고가임

![Untitled](img/Untitled%207.png)

**병목 현상**

- 토폴로지가 중요한 이유는 병목 현상을 찾을 때의 기준이 되기 때문임
- 병목이 발생하면 어떤 구조의 토폴로지로 구성되어있는지 확인 후 회선을 추가하여 병목 현상을 해결 할 수 있음

 

### 2.1.3 네트워크 분류

- 규모에 따른 분류  WAN, MAN, LAN

LAN : 근거리 통신에서 사용됨 = 속도 빠름 

MAN : 대도시 지연 네트워크 도시와 같은 넓은 지역 운영에 사용된다. = 속도 중간 

WAN : 국가 혹은 대륙 같은 더 넓은 지역 운영에 사용된다  = 속도 느림 

### 2.1.4 네트워크 성능 분석 명령어

- 주된 병목 원인
    - 네트워크 대역폭
    - 네트워크 토폴로지
    - 서버, CPU, 메모리 사용량
    - 비효율적 네트워크 구성 등
- Ping
    - TCP/IP의  프로토콜인 ICMP 프로토콜을 활용해 동작함
- netstat
    - 접속되어 있는 서비스들의 네트워크 상태를 표시하는데 사용되며 접속, 라우팅 테이블, 네트워크 프로토콜 등 리스트를 보여줌 = 주로 서비스 포트가 열려있는지 확인할 때 사용함
    - 현재 접속하고 있는 사이트 등에 대한 상태 리스트 확인 가능
- nslookup
    - DNS 에 관련된 내용을 확인하기 위해 쓰는 명령어 _ 특정 도메인에 매핑된 IP를 확인하기 위해 사용한다.
    - nslookup
        - [google.com](http://google.com)
        - naver.com
        - 등 사용 가능
- tracert
    - 윈도우 tracert , 리눅스 traceroute
    - 목적지 노드까지의 네트워크 경로를 확인할 때 사용할 때 사용하는 명령어
    - 어떤 구간에서 명목이 걸리는지 확인할 수 있음

### 2.1.5 네트워크 프로토콜 표준화

- 다른 장치까지 데이터를 주고 받기 위해 설정된 공통된 인터페이스를 말함

## 2.2 TCP/IP 4 계층 모델

### 2.2.1 계층 구조

- OSI 7 계층  TCP/IP 4계층
    - 네트워크 통신 프로토콜의 집합

![Untitled](img/Untitled%208.png)

![Untitled](img/Untitled%209.png)

- 어플리케이션 계층
    - appliction : FTP, HTTP, SSH, SMTP, DNS 등 응용 프로그램이 존재함
    - 웹 서비스, 이메일 등 사용자에게 제공하는 계층을 의미함
    - SMTP : 전자 메일을 위한 프로토콜
- 전송 계층
    - 송신자와 수신자를 연결하는 통신 서비스를 제공하는 계층
    - 연결 지향 데이터 스트림, 신뢰성 , 흐름 제어 등을 제공함
    - TCP. UDP가 여기에 해당함
    
    **TCP**
    
    패킷 사이의 순서를 보장하고 연결 지향 프로토콜을 사용해서 연결하여 신뢰성 구축 수신 여부 확인 “가상회선 패킷 교환 방식”을 이용함
    
    - 각 패킷에 가상회선 식별자가 포함되어 모든 패킷을 전공하면 가상회선이 해체되고 순서대로 도착을 보장함
    
    ![Untitled](img/Untitled%2010.png)
    
    연결 성립 과정 (3way-handshake)
    
    - SYN : isn  임의의 시퀀스 추가해서 보냄
    - SYN + ACK : 서버의 isn과 클라이언트의 isn에 + 1해서보냄
    - ACK :클라이언트는 서버의 ISN +1 한값을 보냄
    
    ![Untitled](img/Untitled%2011.png)
    
    연결 해제 과정 
    
    - Time_Wait가 존재하는 이유는 : 지연 패킷이 발생했을 경우 대비를 하기 위해
    - 무결성 보장을 위해 존재한다.
    
    ![Untitled](img/Untitled%2012.png)
    
    **UDP**
    
    순서를 보장하지 않고 수신 여부를 확인하지 않으며 단순히 데이터만 주고 받는 “데이터그램 패킷 교환 방식”을 이용함 
    
    - 패킷이 독립적으로 이동하며 최적의 경로를 선택해 나감, 서로 다른 경로로 도착할 수 있으며 순서가 다를 수 있는 방식을 의미함
    
    ![Untitled](img/Untitled%2013.png)
    
- 인터넷 계층
    - 패킷을 ip 주소로 지정된 목적지로 전송하기 위해 사용되는 계층
    - ip,arp,icmp등이 있으며 수신해야할 상대의 주소를 지정하여 데이터 전달
    - 상대방에 제대로 받았는지 보장하지 않는 비연결형적인 특징을 가지고 있음
- 링크 계층
    - 전선, 광섬유, 무선 등으로 실질적으로 데이터를 전달하면 장치 간 신호를 주고받는 규칙을 정하는 계층

유선 LAN(IEEE802.3)

- 전이중화 통신을 사용

전이중화 (Full duplex) 통신

- 양쪽 장치가 동시에 송수신 할 수 있는 방식을 의미
- 고속 이더넷은 대부분 이 방식을 기반으로 통신함

**계층 간 데이터 송수신 과정** 

- 요청을 보내면 애플리케이션 → 전송 → 인터넷 계층 → 링크 계층 → 링크 계층 → 인터넷 계층 → 전송 → 애플리케이션 계층 으로 **캡슐화를** 거쳐 전달되고 링크 계층을 통해 해당 서버와 통신하고 해당 서버의 링크 계층으로부터 애플리케이션까지 **비캡슐화** 과정을 거쳐 데이터가 전송된다.

캡슐화 과정 

- 상위 계층의 헤더와 데이터를 하위 계층의 데이터 부분에 포함시키고 해당 계층의 헤더를 삽입하는 과정을 의미함
- 비캡슐화 과정 : 프레임 → 패킷 → 세그먼트, 데이터 그램 → 메세지

## 2.3 네트워크 기기

### 2.3.1 네트워크 기기의 처리 범위

상위 계층을 처리하는 기기는 하위 계층을 처리할 수 있지만 그 반대는 불가함 

- 애플리케이션 계층 : L7 스위치
- 인터넷 계층 : 라우터, L3 스위치
- 데이터 링크 계층 : L2 스위치, 브리지
- 물리 계층 : NIC, 리피터, AP

 

### 2.3.2 애플리케이션 계층을 처리하는 기기

**L7 스위치** 

- 여러 장비를 연결하고 데이터 통신을 중재하며 목적지가 연결된 포트로만 전기 신호를 보내 데이터를 전송하는 통신 네트워크 장비
- **로드밸런서**라고도 불림 → 서버의 부하를 분산하는 기기, 클라이언트로부터 오는 요청들을 뒤쪽의 여러 서버로 나누는 역할을 함 ⇒ 시스템이 처리할 수 있는 트래픽 증가를 목표로함
- URL.서버 , 캐시, 쿠키들을 기반으로 트래픽을 분산, 바이러스. 불필요한 외부 데이터 필터링 기능, 응용 프로그램 수준의 트래픽 모니터링 지원
    
    ![image (10).png](img/image_(10).png)
    

**L7 스위치  VS L4 스위치** 

- L4 스위치는 전송 계층을 처리하는 기기로 스트리밍 관련 서비스에서는 사용할 수 없음 , 메세지를 기반으로 인식하지 못함, **IP와 Port 기반으로 트래픽을 분산함**
- L7은 IP, Port, URL, HTTP Header, 쿠키 등을 기반으로 트래픽을 분산함

**헬스체크** 

- 헬스 체크를 통해 정상적인 서버 또는 비정상적인 서버를 판별, 헬스 체크는전송 주기와 재전송 횟수 등을 설정한 이후 반복적으로 서버에 요청을 보내는 것을 말함

ex) TCP 요청을 보냈는데 3_way handshake가 정상적으로 오지 않으면 정상이 아닌거임 

**로드밸런서를 이용한 이중화** 

- 로드밸런서의 대표적 기능 : 서버 이중화 → 서비스를 안정적으로 운용하기 위해 2개 이상의 서버는 필수적임 → 1개의 서버의 이상이 발생하더라도 서비스는 안정적으로 운영하기 위해
- 0.0.0.12010이 존재하면 → 0.0.0.120111 or 0.0.0.112012로 서빙해줌

### 2.3.3 인터넷 계층을 처리하는 기기

**라우터, L3 스위치** 

- 라우터 (소프트웨어 기반 라우팅 )
    - 여러 개의 네트워크를 연결, 분할, 구분 시켜주는 역할
    - 다른 네트워크상에 존재하는 장치끼리 서로 데이터를 주고 받을 때 패킷 소모를 최소화하여 최소 경로로 패킷을 포워딩 하는 장비
- L3 스위치
    - L2 스위치 + 라우팅 기능을 갖춘 장비  = L3 스위치를 라우터라고 해도 무방함 (하드웨어 기반 라우팅 )

### 2.3.4 데이터 링크 계층을 처리하는 기기

**L2 스위치, 브리지**

L2 스위치 

- MAC 주소를 MAC 주소 테이블을 통해 관리하며, 연결된 장치로부터 패킷이 왔을 때 패킷 전송을 담당함
- IP 이해 못 해 IP 주소를 기반으로 라우팅은 불가하며 단순히 패킷의 MAC 주소를 읽어 스위칭 하는 역할을 함

브리지

- 두 개의 근거리 LAN을 상호 접속 할 수 있도록 하는 통신망 연결 장치로 , 포트와 포트 사이의 중간 다리 역할을 함 = 통신망의 범위를 확장하고 서로 다른 LAN 등으로 이루어진 하나의 통신망을 구축할 때 사용한다.

### 2.3.5 물리계층을 처리하는 기기

**NIC, 리피터, AP**

NIC 

- LAN 카드라고 불리는 녀석, 2대 이상의 컴퓨터 네트워크를 구성하는데 사용함
- 각각을 구분하기 위해 식별번호 MAC 주소가 존재함

리피터 

- 약해진 신호를 증폭해서 다른 쪽으로 보내주는 장치
- 현재는 잘 사용하지 않음 → 광테이블의 보급 때문

AP

- Access Point  패킷을 복사하는 기기

## 2.4 IP 주소

- 인터넷 계층에서 사용하는 주소 IP

### 2.4.1 ARP

- 컴퓨터와 컴퓨터 간의 통신 = IP주소에서 ARP를 통해 MAC을 찾아 MAC주소를 기반으로 통신함
- ARP(address Resolution Protocaol) : IP주소로 부터 MAC 주소를 구하는 프로토콜
- 가상 주소인 IP를 통해 실제 주소인 MAC 주소를 찾는 것 → ARP
- 실제 주소인 MAC 에서 가상 주소인 IP를 찾는 것→ RARP

![Untitled](img/Untitled%2014.png)

![Untitled](img/Untitled%2015.png)

- A ⇒ 브로드 캐스트를 이용해서 전체에게 MAC 주소를 찾으라고 알림
- 해당 하는 B가 유니캐스트 ARP Reply를 통해  MAC 전송해줌

> 브로드캐스트 : 송신 호스트가 전송한 데이터가 네트워크에 연결된 모든 호스트에게 전송
> 

> 유니케스트  : 고유 주소로 식별된 하나의 네트워크에 1 : 1 로 데이터를 전송하는 방식
> 

### 2.4.2 홉바이홉 통신

- 통신망에서 각 패킷이 여러 개의 라우터를 건너가는 모습
- 서브 네트워크 안에 있는 라우팅의 라우팅 테이블 IP를 기반으로 패킷을 전달하고 또 전달해 나가며 라우팅을 수행해 최종 목적지까지 패킷을 전달하는 행위를 의미함

![Untitled](img/Untitled%2016.png)

**라우팅 테이블** 

- 송신자에게 수신자까지 도달하기 위해 라우터에 들어가 있는 목적지 정보들과 가기 위한 방법을 명시해둔 리스트를 의미함
- 게이트워에와 모든 목적지에 대해 해당 목적지에 도달하기 위해 거쳐야할 라우터 정보를 가지고 있음

**게이트 웨이**

- 서로 다른 통신망, 프로토콜을 사용하는 네트워크 간 통신을 가능하게 해주는 컴퓨터나 소프트웨어를 일컫는 용어
- 서로 다른 네트워크상의 통신 프로토콜을 변환해주는 역할
- 게이트 웨이를 확인하기 위해 netstat -r 작성하면 볼 수 있음

![Untitled](img/Untitled%2017.png)

### 2.4.3 IP 주소 체계

IPv4 : 32비트 8비트로 나누어 표현 ⇒ 123.456.7.9

IPv6 : 64비트 16비트로 나어 표현 ⇒ 2001:db8::ff00:42:8329 

**클래스 기반 할당** 

- A,B,C,D,E 다섯 개의 클래스로 구분하는 클래스 기반 할당
- A,B,C 는 일대일 통신으로 사용, D는 멀티캐스트 통신, E는 앞으로 사용할 예비용

![Untitled](img/Untitled%2018.png)

- 클래스 범위

![Untitled](img/Untitled%2019.png)

IP의 낭비를 줄이기 위해 아래 두가지 방식이 등장 

**DHCP**

- IP주소 및 통신 매개변수 직접 할당할 필요없이 인터넷 접속시 자동 할당

**NAT**

- 패킷이 라우팅 장치를 통해 전송되는 동안 패킷의 IP 주소 정보를 수정하여 IP 주소를 다른 주소로 매핑하는 방법
- IPv4 주소 체계만으로 부족한 아이피를 감당하기 위해 공인 IP와 사설 IP로 나누어 처리

![Untitled](img/Untitled%2020.png)

- 192.168.0.1,2,3,4 ⇒ 사설 IP
- NAT 장비를 통해 하나의 공인 IP 121.165.151.200으로 외부 인터넷 요청 가능
- 홍철 및 가영은 하나의 IP인 121.165.151.200을 기반으로 각각의 다른 IP 를 가지는 것 처럼 사용할 수 있음
- NAT 장비를 통해 사설을 공인으로 공인을 사설로 바꾸는 역할을 수행 할 수 있음

**공유기와 NAT**

- NAT를 사용하는 이유는 여러 대의 호스트가 하나의 공인 IP 주소를 사용하여 인터넷에 접속하기 위함
- 인터넷 하나의 회선을 열고 공유기를 달아서 여러 PC를 연결하는 사용하는 것 → 공유기에 NAT 기능이 탑재 되어있기 때문에 가능함

**NAT 보안**

- NAT 이용하면 내부 네트워크 IP주소와 외부에 들어나는 IP가 다르게 유지 할 수 있기 때문에 내부 네트워크에 대한 어느 정도의 보안이 가능

**NAT 단점** 

- 여러 명이 동시에 사용하기 때문에 느려질 수 있음

## 2.5 HTTP

- 애플리케이션 웹 서비스 통신에 사용 현재는 3버전까지 나와있음

### 2.5.1 HTTP/ 1.0

- 한 연결당 하나의 요청을 처리하게 설계되어 있음 , RTT 증가를 통해 불러오게 되어있음
- 파일을 가져올 때 마다 3-way handShake를 계속해서 열어야해서 RTT가 증가

> RTT :패킷이 목적지에 도달하고 다시 출발지로 돌아오기까지의 시간
> 

![Untitled](img/Untitled%2021.png)

- RTT 증가를 해결하기 위해 스플리팅, 코드 압축, 이미지 base64 인코딩을 사용하곤 했음

이미지 스플리팅 

- 이미지가 합쳐져 있는 하나의 이미지를 다운받고, 이를 기반으로 포지션을 설정해서 화면에 표시

코드 압축 

- 개행 문자, 빈칸을 없애서 코드의 크기를 최소화

이미지 Base64 압축 

- 64진법으로 이루어진 문자열로 인코딩하는 방법
- 서버와의 연결을 열고 이미지에 대해 서버에 HTTP 요청을 할 필요가 없다는 장점이 있음
- 다만 이미지가 약 37%정도 증가한다는 단점이 존재함

### 2.5.1 HTTP/ 1.1

- 매번 TCP 연결을 하는 것이 아닌 한 번의 TCP 초기화 후 Keep-alive 옵션으로 여러 개의 파일을 송수신할 수 있게 함
- 핸드 쉐이크를 한 번 발생 시키고 그 이후에는 발생하지 않음
- 다수의 리소스등을 처리하려면 요청할 리소스 개수에 비해 대기 시간이 길어진다는 단점 존재
- 헤더안에 쿠키 등 다양한 메타데이터가 존재하여 압축이 되지 않아 무거웠음

![Untitled](img/Untitled%2022.png)

- HOL Blocking → 네트워크 큐에 있는 패킷이 첫 번째 패킷에 의해 지연될 때 발생하는 성능 저하

![Untitled](img/Untitled%2023.png)

### 2.5.3 HTTP/ 2

- 지연 시간 줄이고 응답 시간을 더 빠르게
- 멀티 플랙싱, 헤더 압축, 서버 푸시, 요청의 우선순위 처리지원

**멀티  플랙싱**

- 여러 개의 스트림을 사용하여 송수신, 특정 스트림 패킷이 손실되었다고 하더라도 해당 스트림에만 영향을 미치고 나머지 스트림은 이상 없이 작동 가능

> 스트림(Steam)
> 
- 시간이 지남에 따라 사용할 수 있게 되는 일련의 데이터 요소를 가리키는 데이터 흐름

 

![Untitled](img/Untitled%2024.png)

- 단일 연결을 사용해서 병렬로 여러 요청을 받을 수 있고 응답을 줄일 수 있음
- 이를 통해 HOL Blocking 을 해결 할 수 있음

![Untitled](img/Untitled%2025.png)

**헤더 압축**

- 기존 HTTP/1.X에는 큰 헤더가 문제가 되었음
- HTTP/2 에서 헤더 압축을 사용해서 해결함 ⇒ 압축 알고리즘 = 허프만 코딩 압축 알고리즘 ⇒ HPACK  압축 형식을 가짐

허프만 코딩 : 문잦열을 문자 단위로 쪼개 빈도수를 세어 빈도가 높은 정보는 적은 비트 수를 사용하여 표현하고 빈도가 낮은 정보는 비트 수를 많이 사용하여 표현  = 전체 데이터에 필요한 피트양을 줄이는 원리 

**서버 푸시** 

- HTTP/2 클라이언트 요청 없이 서버가 바로 리소스 푸시 가능

![Untitled](img/Untitled%2026.png)

### 2.5.4 HTTPS

- 통신을 암호화하는 SSL/TSL를 사용함
- HTTP/2 는 HTTPS 위에서 작동함

**SSL/TLS**

- SSL(Secure Socket Layer)는 SSL 1.0 ~> 3.0 → TLS(Transprot Layer Security Protocol)로 명칭을 바꾸고 1.3 버전까지 올라옴
- 공격자가 서버인 척 하면서 사용자 정보를 가로채는 “인터셉터”를 방지함
- 보안 세션을 기반으로 데이터를 암호화하며 보안 세션이 만들어질 때 인증 메커니즘, 키 교환 암호화 알고리즘, 해싱 알고리즘이 활용된다.

보안세션

- 보안이 시작되고 끝나는 동안 유지되는 세션 → SSL/TLS는 핸드 쉐이크를 통한 보안 세션을 생성하고 이를 기반으로 상태 정보 공유

인증 매커니즘 

- CA(Certificate Authorties)에서 발급한 인증서를 기반으로 이루어짐
- 공개키를 클라이언트에게 제공하고 사용자가 접속한 서버가 신뢰 할 수 있는 서버임을 보장

CA 발급

- 자신의 사이트 정보와 공개키를 CA에 제출 → CA는 공개키를 해시한 값인 지문을 사용하는 CA의 비밀키 등을 기반으로 인증서를 발급해줌

암호화 알고리즘 

디피- 헬만 알고리즘을 주로 사용함 

![Untitled](img/Untitled%2027.png)

- 초반  공개키를 공유하고 각자의 비밀 값과 혼합 후 혼합 값을 공유함 → 각자 자신의 비밀 값과 다시 혼합→ 그 후 공통 암호키인 PSK가 생성된다.
- 이렇게 클라이언트 서버 모두 개인키 및 공개키를 생성하고 서로의 공개키와 개인키를 결합하여 PSK가 생성된다면, 악의적인 공격자가 개인키 또는 공개키를 가지고도 PSK가 없어 아무것도 못 함

해싱 알고리즘 

- 데이터 추정하기 힘든더 작고, 섞여 있는 조각으로 만드는 알고리즘
- SSL/TLS는 SHA-256, 384 알고리즘을 주로 사용함

**SHA-256 알고리즘** 

- 해시 함수의 결과값이 256비트인 알고리즘이며 비트 코인을 비롯한 많은 블록 체인 시스템에서 사용함
- 해싱을 해야 할 메세지에 1을 추가하는 등 전체리를 하고 전처리된 메세지를 기반으로 해시를 반환함

### 2.5.5 HTTP / 3

- QUIC이라는 계층위에서 돌아가며 TCP가 아닌 UDP 기반으로 돌아감.
- 초기 연결 설정 시 지연 시간을 감소 시킨다. → TCP 기반이 아니기 때문에 핸드 쉐이크 과정이 없음

# 예상 질문

### OSI 7계층과 TCP/IP 4계층의 차이점은 무엇인가?

- OSI 7 계층의 경우 애플리케이션 계층을  3개의 계층을 쪼개 설명한다. 또한 인터넷 계층을 네트워크 계층으로 부른 다른 점이 차이가 있다

### HTTP/2 를 설명하고 장점을 설명해봐라

- HTTP/1.X 대비 지연 시간이 줄어들었으며 응답 시간이 빠르다.
- 멀티 플랙싱, 헤더 압축 , 서버 푸시, 요청의 우선순위를 지원하는 프로토콜임
- 장점으로는 멀티 플랙싱을 지원하여 여러개의 스트림을 사용하여 송수신할 수 있고 특정 스트림의 패킷이 손실되더라도 해당 스트림에만 영향일 미치고 나머지 스트림은 정상적으로 동작할 수 있게 해준다. 또한, 서버 푸시가 장점이라고 생각한다. 기존 클라이언트가 서버에 요청을 해야 파일을 다운받을 수 있었다면 2버전 부터는 클라이언트의 요청 없이 바로 리소스를 푸시할 수 있다는 것이 장점입니다.