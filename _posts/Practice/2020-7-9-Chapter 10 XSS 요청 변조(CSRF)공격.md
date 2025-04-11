---
layout: post
category : Practice

---

--------------------------------------------------

<center style="color:red;">
!warning!<br>

본 게시글은 본인의 학습기록을 위해 작성된 알려진 학습 기법<br>

함부로 악의적으로 이용은 엄연히 불법 임으로<br>

절대 시도하지 말 것이며<br>

사고 발생 시 본인은 절대로 책임지지 않습니다!<br>
</center>

--------------------------------------------------
<div align="center" >
<img src="/Art of Web Hacking/Chapter10/Chapter10.png" width="400" height="300"> <br>
</div><br>

<center><font size="5em" color="#0091ff">Chapter 10. XSS 요청 변조(CSRF) 공격</font> </center>
<font size="3em" color="#0091ff">
<br>

<center><font size="4em" color="#0091ff">CSRF 공격 개요</font> </center><br>
- CSRF의 취약점의 공격 방법은 공격자가 피싱을 이용하여 공격 대상이
<br>
링크에 정상적인 접속하도록 하여 웹사이트의 어떤 기능을 실행하게 하는 것입니다. 
<br>
<center><font size="4em" color="#0091ff">CSRF 공격 실습</font> </center><br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter10/001.png" width="520" height="400"> <br>
</div>스샷. 1<br><br>
- DVWA → Vulnerability: CSRF에 패스워드 값으로 test 입력했을 때 버프스위트에 잡히는 내역
<br>
- 사용자가 로그인 되어 있을 때에는 웹 페이지를 요청할 때마다 쿠키가 웹 브라우저에 의해<br>
자동으로 전달됨 → 로그인된 웹 사이트의 링크를 누르게 만들면 쿠키를 전달시킬 수 있습니다.
<br><br>
- 어떤 정보를 변경하는 요청 메시지에 쿠키 이외에는 랜덤 한 값이 없으면 CSRF에 취약할 수 있습니다.

<div >
<img src="/Art of Web Hacking/Chapter10/002.png" width="520" height="400"> <br>
</div><br>
<div >
<img src="/Art of Web Hacking/Chapter10/003.png" width="360" height="180"> <br>
</div>스샷. 1-2<br><br>

-1번 부분에서는 요청 url과 파라미터가 똑같이 구성되어 있고, 2번 <br>부분에서는 withCredentials 속성을 true로 설정하여,<br>
요청이 전송될 떄 웹 브라우저가 쿠키를 자동으로 같이 전송하도록 합니다.
<br>

<div >
<img src="/Art of Web Hacking/Chapter10/004.png" width="520" height="90"> <br>
</div>스샷. 3<br><br>

-실습·복습에 앞서 15번째 줄 host를 DVWA 즉 타깃의 IP 주소로 변경하고<br>
/var/www/html 디렉터리로 옮깁니다.

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">http://localhosy/csrf.html</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>
<br>

<div >
<img src="/Art of Web Hacking/Chapter10/005.png" width="520" height="160"> <br>
</div>스샷. 4<br><br>
- 주소창에 해당 명령어를 입력했으면 이렇게 과거 추억의 유희왕 짜가 카드팩<br>
마냥 금융기관 같은 가짜 사이트 가 출력됩니다. ōxō<br>
<span style="color: #FFFFFF">~~주소창에 해당 명령어를 입력했으면 이렇게 과거 추억의 유희왕 짜가 카드팩~~</span><br>
<span style="color: #FFFFFF">~~마냥 금융기관 같은 가짜 사이트 가 출력됩니다. ōxō~~</span><br>

<span style="color: #FFFFFF">유희왕2 OO하는 미친해골~~(…)</span><br>


<br><div>
<img src="/Art of Web Hacking/Chapter10/006.png" width="520" height="460"> <br>
</div>스샷. 5<br><br>
- click 링크를 눌렀을 때 http history를 통해 기록을 확인하면 password가 Lucia로<br>
변경된것을 확인할 수 있습니다.
<br>

-또한 응답코드가 200으로 변경되어 있으면 패스워드가 정상적으로 변경된 것입니다.


<center><font size="4em" color="#0091ff">CSRF 공격 대응</font> </center><br>

1 . 요청 메시지의 레퍼러 헤더<br>

(해당 요청을 링크하고 있던 이전 웹 페이지의 주소를 아려주는 헤더)<br>

를 검사하여, 웹 메일이나 타 사이트에서<br>

피싱을 당해 전송되는 요청을 실행하지 않게 하는 것입니다.<br>
<br>

2 . CSRF 토큰(CSRF 공격 대응을 위해 포함시키느 랜덤 한 값) 사용을 합니다.<br>


-웹 애플리케이션이 CSRF 토큰을 매 응답마다 랜덤하게 생성하여

히든 폼 필드를 통해 클라이언트에게 전송<br>


-클라이언트는 이전 응답 메시지에 포함된 토큰 값을 다음 요청 시 포함시켜 전송<br>


-웹 애플리케이션이 CARF 토큰 값을 검사하면 정상적인 과정을 토해 전달된 요청인지

확인할 수 있습니다.<br>


<center>

==================================<br>

휴 … 이제서야 두 자리 숫자 챕터까지 왔습니다ōxō;<br>

휴 … 이제서야 두 자리 숫자 챕터까지 왔습니다ōxō;<br>


마지막 챕터까지 다 작성 할 수 있을지 는 모르겠지만<br>

여튼 계속 복습완주차 포스팅 해볼렵니다 .<br>


그럼 그렇고 아직까지 일용직<br>

출근 확정 문자 오지않아 못하고 있군요<br>

ㅋㅋㅋㅋㅋㅋㅋㅋ<br>


이 미친놈들 ㅋㅋㅋㅋㅋ<br>

이럴꺼면 뭣하러 안드로이드& IOS<br>

출근 스케쥴 어플 만들었냐?<br>

ㅋㅋㅋㅋㅋㅋㅋㅋㅋ<br>


진심 효율성 제롭니다 제로<br>

햐… 정말 어메이징 합니다.<br>

중국코로나 터지니까 그제서야<br>

조치를 취하는거 보니 정말 어이가없습니다<br>

ㅋㅋㅋㅋㅋ<br>


결국 이러지도 저러지도 못하고<br>

또 다른 자리 알아봅니다<br>


아 이야기가 옆으로 셌군요 아무튼 시간 과 상황이<br>

허락하는 대로 복습차 글 작성 해봅니다.<br>


여러모로 흉흉합니다. 여러분들도 항상 건강하시고<br>

좋은 일만 있으시길 바랍니다<br>

중국코로나 도 항상 조심하시길…。<br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter10/007.png" width="320" height="320"> <br>
</div>

</center>
