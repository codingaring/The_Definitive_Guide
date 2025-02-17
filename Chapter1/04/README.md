# 4장 커넥션 관리
- HTTP는 어떻게 TCP 커넥션을 사용하는가
- TCP 커넥션의 지연, 병목, 막힘
- 병렬 커넥션, keep-alive 커넥션, 커넥션 파이프라인을 활용한 HTTP의 최적화
- 커넥션 관리를 위해 따라야 할 규칙들

## TCP 커넥션
 URL을 입력받은 브라우저의 수행 단계
 1. 브라우저가 URL라는 호스트 명을 호출한다.
 2. 브라우저가 이 호스트 명에 대한 IP 주소를 찾는다
 3. 브라우저가 포트 번호(80)를 얻는다
 4. 브라우저가 202.43.78.3의 80포트로 TCP 커넥션을 생성한다. (해당 IP 주소)
 5. 브라우저가 서버로 HTTP GET 요청 메시지를 보낸다.
 6. 브라우저가 서버에서 온 HTTP 응답 메시지를 읽는다.
 7. 브라우저가 커넥션을 끊는다.

  ### 4.1.1 신뢰할 수 있는 데이터 전송 통로인 TCP
  HTTP 커넥션은 몇몇 사용 규칙을 제외하고는 TCP 커넥션에 불과하다. 
  - TCP 커넥션은 인터넷을 안정적으로 연결해준다.
  - TCP는 HTTP에게 신뢰할 만한 통신 방식을 제공한다. TCP 커넥션의 한 쪽에 있는 바이트들은 반대쪽으로 순서에 맞게 정확히 전달된다.

  ### 4.1.2 TCP 스트림은 세그먼트로 나뉘어 IP 패킷을 통해 전송된다
  - TCP는 IP패킷(혹은 IP 데이터그램)이라고 불리는 작은 조각을 통해 데이터를 전송한다.
  - HTTP에 보안 기능을 더한 HTTPS는 TLS 혹은 SSL이라 불리기도 하며, HTTP와 TCP 사이에 있는 암호화(cryptographic encryption) 계층이다.
  - HTTP가 메시지를 전송하고자 할 경우, 현재 연결되어 있는 TCP 커넥션을 통해서 메시지 데이터의 내용을 순서대로 보낸다. 
  - TCP는 **세그먼트**라는 단위로 데이터 스트림을 잘게 나누고, 세그먼트를 **IP 패킷**이라고 불리는 봉투에 담아서 인터넷을 통해 데이터를 전달한다.
  -IP 패킷 구성
    - IP패킷 헤더 (보통 20 바이트)
    - TCP 세그먼트 헤더(보통 20 바이트)
    - TCP 데이터 조각 (0 혹은 그 이상의 바이트)

  #### IP헤더
  - 발신지와 목적지
  - IP 주소
  - 크기
  - 기타 플래그
  > TCP 세그먼트 헤더는 TCP 포트 번호, TCP 제어 플래그, 그리고 데이터의 순서와 무결성을 검사하기 위해 사용되는 숫자 값을 포함한다.

   
     


