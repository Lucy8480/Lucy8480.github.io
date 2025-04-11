---
layout: post
category : Practice

---


<div align="center" >
<img src="/Art of Web Hacking/Chapter1/Chapter1.png" width="400" height="300"> <br>
</div>

# Chapter 01. 웹과 HTTP 기초

이 카테고리는 본인이 완주한
"화이트 해커를 위한 웹 해킹의 기술"이라는
책으로 공부한 내용을 복습 겸 게시할 계획입니다.

웹 해킹 사이트에서 직접 실습을 할 수 있고.
무료로 강의를 제고해서무리(?) 없이 학습을 해갔었다.

## 웹 아키텍처
1. 클라이언트 영역
    <br>1.1 프레젠테이션 티어

2. 서버 영역
    <br>2.2 로직 티어 : HTTP 요청 처리 및 응답 (ex: 웹 서버와 웹 프레임워크)    
    <br>2.3 데이터 티어: 데이터 처리 및 결과 응답(ex: DBMS, DB)

## HTTP 요청 메시지
1. 요청 메세지의 구성
<br>   1.1 <바디>를 통해 데이터가 전송됨
<br>   1.2 데이터를 전송할 필요가 없는 경우에는<바디> 부분 없이 구성

//헤더와 바디가 구분도리 때 빈 줄에 줄 바꿈을 위해 CRLFCRLF 사용되는데, CRLF를 강제로 전송하여 의도치
않은 결과를 초래하도록 만든것-> CRLF 인젝션, HTTP 응답 스플리팅

2. 메소드
  - 서버에게 어떤 명령을 실행할지 알려주는 역할
<br> 2.1 GET:  지정된 리소스를 요청
<br> 2.2 POST: 클라이언트 쪽에서 데이터를 서버 쪽으로 전달
<br> 2.3 PUT: 지정된 리소스에 데이터를 저장
<br> 2.4 DELETE: 지정된 리소스를 삭제

3. 요청 URI
- 요청이 파라미터를 전달하는 경우에는 ?가 사용됨
  (ex: /sqli/?id=1&Submit)

4. 요청 헤더

<div align="center" >
<img src="/Art of Web Hacking/Chapter1/002.png" width="400" height="300"> <br>
</div>
<이미지출저: https://mer-bleu.tistory.com/13> <br>
-헤더는 리스트의 형태로 여러 개 전송 가능<br>


>헤더이름: 헤더 값


5. 헤더 예제

    5.1 HOST<br>
    -서버의 도메인 이름과 포트를 명시,생략될 경우에는웹 서비스 포트(80) 이해
    
    5.2 User-Agent
    - 클라이언트를 식별할 수 있는 헤더
    - User-Agent 헤더에 따라 서버 동작이 달라지는 경우, <br>특정 앱들은 호환성을 위해 다른 User-Agent 정보를 사용하기도 함<br>
     //악성 봇들이나 자동화 프로그램도 가짜 User-agent 헤더를 사용하는 경우가 많음
->User-agent Spoofing
    
    5.3 HOST<br>
    - 5.3.1 Accept 헤더는 클라이언트가 어떤 컨텐트 타입을 처리 할 수 있는지 서버에게 알려줌
    - 5.3.2 Accept-Language 헤더는 클라이언트가어떤 언어를 처리할 수 있는지 서버에게 알려줌
    - 5.3.3 Accpet-Encoding 헤더는 클라이언트가처리할 수 있는 인코딩 방식이나 압축 알고리즘 정보 알려줌

    5.4 Referer<br>
    - 리피러 헤더는 이전 웹 페이지의 주소를 알려줌, 요청이 웹사이트 내부인지 외부인지 판단 가능 -> SRF 대응

    5.5 Content-Type, Content-Length
      - 바디가 존재하는 경우 바디의 종류와 같이 알려줌
   
   5.6 Cookie
   - 5.6.1 쿠키를 전달하는 헤더, 변수와 값의 쌍으로 구성
   - 5.6.2 여러 요청에 걸쳐 클라이언트에서 동일한 데이터를 전달할 필요가 있을 때 사용


## HTTP 응답 메시지
   > <버전><응답 코드><응답코드텍스트><br><헤더><br><바디>


1. 응답 코드/응답 코드 텍스트
    - 헤더와 바디 부분 형식 동일

    1.1 응답코드
    - 1.1.1 100번대 : 정보 전달 목적 
    - 1.1.2 200번대 : 요청 처리 성공
    - 1.1.3 300번대 : 다른 웹페이지로 리다이렉트 필요
    - 1.1.4 400번대 : 클라이언트가 원인이 되어 에러 발생
    - 1.1.5 500번대 : 서버 에러

2. 응답 헤더
   - 2.1 Server
        <br>- 웹 서버와 웹 프레임워크의 버전 정보 알려줌 

   - 2.2 Set-cookie
        <br>- 서버에서 클라이언트로 쿠키를 전달할 때 사용, 쿠키 이름과 값 설정은 필수
        >Set-Cookie: <쿠키 이름>=<쿠키 값>; Expires=<날짜>; Path=<경로>; Secure; HttpOnly

    - 2.2.1 Expires
         <br>- 쿠키의 유효기간설정,<br>설정되어 있지 않으면 세션이 종료 될<br> 때까지의 유효기간을 가짐
    - 2.2.2 Path
        <br>- 쿠키를 전송할 리소스의 결로 짖어,<br>서브 디렉토리까지 같이 매칭 
     
    - 2.2.3 Secure
        <br>- 해당 옵션을 지정한 쿠키는 HTTP 요청 시<br>에만 전달 ->네트워크 스니핑 대응

    - 2.2.死 HttpOnly
        <br>- 해당 키워드를 통해 쿠키 값이 자바스크립트에<br>의해 접근되는 것을 방지 -> XSS 방지

    - 2.2.5 X-Frame-Options
        <br>- < frame > or < iframe >를 사용한 웹 페이지 출력 제어->클릭재킹 공격 방지 알려줌  
        <br>- ex: X-Frame-Options: Deny, X-Frame-Options: SAMEORIGIN

    - 2.2.6 X-XSS-Protection
        <br>- XSS 공격이 탐지되었을 떄, 웹 페이지가 로딩되는 것을 막아줌
        <br>- ex: X-XSS-Protection: 1; mode=block

    - 2.2.7 X-Content-Type-Options
        <br>- MIME 스니핑을 차단하기 위해 사용하는 헤더,Content-Type에 설정된 형식으로만 처리
        <br>- ex: X-Content-Type-Options: nonsniff
