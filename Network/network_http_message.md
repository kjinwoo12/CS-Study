# HTTP 메시지

## 메시지의 흐름
* 인바운드, 아웃바운드, 업스트림, 다운스트림

### 인바운드 & 아웃바운드
> "메시지는 원 서버 방향을 인바운드로 하여 송신된다"

![alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FePdLDE%2FbtsJFJ1jJWI%2F1LeMVKXT328zWwkh6hHzS1%2Fimg.png)


* HTTP는 인바운드와 아웃바운드라는 용어를 트랜잭션 방향으로 표현하기 위해 사용한다.
* 인바운드로 이동한다 == 메시지가 원서버 방향으로 향한다.
* 아웃바운드로 이동한다 == (모든 처리가 끝난 뒤) 메시지가 사용자 에이전트로 돌아오는 것

### 다운스트림 & 업스트림
> " 다운스트림으로 흐르는 메시지 "

![alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FY48KI%2FbtsJGwmMEF0%2FOv9774EUm9nAk9b8A6RLZ1%2Fimg.png)

* 다운스트림과 업스트림이란 용어는 발송자와 수신자에 대한것이다.
* HTTP는 강물과 같이 흐른다. 모든 메시지는 요청 또는 응답 메시지냐에 관계없이 다운스트림으로 흐른다.
* 메시지의 발송자는 수신자의 업스트림이다.
(요청에서는 프락시 1이 프락시 3의 업스트림이지만, 응답에서는 프락시 3이 프락시 1의 업스트림이 될 수도 있다.)

## 메시지의 각 부분
> HTTP 메시지는 단순한, 데이터의 구조화된 블록

각 메시지는 클라이언트로부터 요청이나 서버로부터의 응답 중 하나를 포함한다.

### 메시지의 구성
* 메시지는 시작줄, 헤더블록, 본문 3가지 파트로 구성된다.
* 시작줄: 이것이 어떤 메시지인지 서술
* 헤더블록: 메시지의 속성을 담고 있음

```
Content-type: text/plain # 본문이 무엇인지 말해줌
Content-length: 19 # 본문의 크기: 19byte
```

* 본문: 선택적인 데이터 덩어리 (optional 한 부분)

시작줄 & 헤더블록 → 줄 단위로 분리된 아스키 문자열
(각 줄은 캐리지리턴(ACSII 13) & 개행문자(ACSII 10)로 구성된 두 글자의 줄바꿈 문자열(CRLF)로 끝난다)

본문 → 시작줄, 헤더블록과 달리 본문은 텍스트와 이진데이터(ex) 이미지나 동영상)를 포함할 수 있고, 그냥 비어있을 수도 있음

### 메시지 문법
모든 HTTP 메시지

* 요청: 웹 서버에 어떤 동작을 요구
* 응답: 요청의 수행 결과를 클라이언트에게 돌려줌 (상태정보와 결과 데이터 등)
    
    ⇒ 둘다 기본적 구조가 같음!

### 요청/응답 메시지 형식
* 요청
```
<메서드> <요청 Url> <버전>
<헤더>

<엔터티 본문>
```
* 응답
```
<버전> <상태 코드> <사유 구절>
<헤더>

<엔터티 본문>
```

- 메서드: 클라이언트 측에서 서버가 리소스에 대해 수행해주길 바라는 동작
- 요청 URL: 요청 대상이 되는 리소스를 지칭하는 완전한 URL 혹은 URL의 경로 구성요소다
- 버전: 메시지에서 사용 중인 HTTP의 버전이다. 
- 형식 - HTTP/<메이저>, <마이너>
- 상태 코드: 요청 중에 무엇이 일어났는지 설명하는 3자리 숫자
- 사유 구절: 숫자로 된 상태 코드의 의미를 사람이 이해할 수 있게 설명해주는 짧은 문구
- 상태 코드 이후부터 줄바꿈 문자열까지가 사유 구절이다. 이는 오로지 사람에게 읽히기 위한 목적으로 존재한다.
- 헤더: 이름, 콜론(:), 선택적인 공백, 값, CRLF가 순서대로 나타나는 0개 이상의 헤더들
- 엔터티 본문: 임의의 데이터 블록을 포함한다

### 시작줄

모든 HTTP 메시지는 시작 줄로 시작한다. 
메서드, 상태 코드, 사유 구절, 버전 번호 등이 포함된다.

### 헤더
HTTP 헤더 필드는 요청과 응답 메시지에 추가 정보를 더한다. 기본적으로 이름/값 쌍의 목록이다.

### 엔티티 본문
엔티티 본문은 이미지, 비디오, HTML 문서, 소프트웨어 애플리케이션, 신용카드 트랜잭션, 전자우편 등 여러 종류의 디지털 데이터를 실어 나를 수 있다.

 
## 메서드
1. GET
    * GET은 주로 서버에게 리소스를 달라고 요청하기 위해 쓰인다. 

2. HEAD
    * HEAD 메서드는 정확히 GET 처럼 동작하지만, 서버는 응답으로 헤더만을 반환하며 엔티티 본문은 반환되지 않는다.
    * HEAD를 사용하는 이유
        - 리소스를 가져오지 않고도 그에 대해 무엇인가를 알아낼 수 있다.
        - 응답의 상태코드를 통해 개체의 존재 여부를 확인할 수 있다.
        - 헤더를 확인하여 리소스가 변경되었는지 검사할 수 있다.
3. PUT
    * PUT 메서드는 서버가 요청의 본문을 가지고 요청 URL의 이름대로 새 문서를 만들거나 이미 URL이 존재한다면 본문을 사용해서 교체한다.

    * PUT은 콘텐츠 변경을 하도록 해주므로, 웹 서버가 PUT을 수행하기 전에 사용자 인증을 해야한다.

 

4. POST
    * POST 메서드는 서버에 입력 데이터를 전송하기 위해 설계되었다.

 

5. TRACE
    * 클라이언트가 어떤 요청을 할 때, 그 요청은 방화벽, 프락시, 게이트웨이 등의 애플리케이션을 통과할 수 있다. 이들한테는 원래의 HTTP 요청을 수정할 수 있는 기회가 있으며, TRACE 메서드는 클라이언트에게 자신의 요청이 서버한테 도달했을 때 어떻게 보이는지 알려준다.
    
    * TRACE 메서드는 주로 진단을 위해 사용된다. 요청이 의도한 요청/응답 연쇄를 거쳐가는지 검사할 수 있으며, 프락시나 다른 애플리케이션들이 요청에 어떤 영향을 미치는지 확인해보고자 할 때도 좋은 도구다.


6. OPTIONS
    * OPTIONS 메서드는 웹 서버에게 여러가지 종류의 지원범위에 대해 물어본다. 
    
    * 서버에게 특정 리소스에 대해 어떤 메서드가 지원되는지 물어볼 수 있다.

 

7. DELETE
    *  DELETE 메서드는 서버에게 요청 URL로 지정한 리소스를 삭제할 것을 요청한다. 

 
