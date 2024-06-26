
### Protocol

- 서로 다른 시스템에 있는 두 개체 간의 데이터 통신을 원활하게 하기 위한 <br/>
	일종의 통신 규약을 말한다.
- 이러한 통신을 위해서 프로토콜은 데이터 처리 기능, 제어 기능, 관리적 기능을 <br/>
	기본적으로 가지고 있어야 한다.
- 프로토콜을 구성하는 기본 요소로는 '**구문**', '**의미**', '**타이밍**'이 존재한다.

| 기본 요소                | 의미                                           |
| -------------------- | -------------------------------------------- |
| **구문 <br/>Syntax**   | 시스템 간의 정보 전송을 위한 데이터 형식, 코딩, 신호 레벨 등의 규정     |
| **의미 <br/>Semantic** | 시스템 간의 정보 전송을 위한 제어 정보 <br/>조정과 에러 처리를 위한 규정 |
| **타이밍 <br/>Timing**  | 시스템 간의 정보 전송을 위한 속도 조절과 순서 관리 규정             |

---

#### 인터넷 주소 체계

- 인터넷 주소를 나타내는 방식은 IP, Domain 두 가지 방식이 존재한다.

- **IP 방식**
	- 32bit의 주소 체계(IPv4 기준)를 기준으로 <br/>
		인터넷 상에 존재하는 Host나 서버의 위치를 지정해주는 방식
	- `.` (Dot)에 의해 구분되는 10진수 값은 하나 당 1 byte로 <br/>
		총 4 byte로 구성됐다.

- **Domain 방식 (DNS 방식)**
	- Domain Name System, DNS는 Host의 도메인 이름을 <br/>
		Host의 네트워크 주소로 바꾸거나 그 반대의 변환을 수행할 수 있도록 개발된 방식
	- 특정 컴퓨터나 혹은 네트워크로 연결된 임의의 장치의 주소를 찾기 위해 <br/>
		사람이 이해하기 쉬운 도메인 이름을 숫자로 된 식별 번호 (`IP 주소`) 변환
	- `www.example.com`과 같은 도메인 이름을 `192.168.1.0`와 같은 IP 주소로 변환 <br/>
		Routing 정보를 제공한다.

---

