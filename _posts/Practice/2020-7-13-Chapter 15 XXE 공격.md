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
<img src="/Art of Web Hacking/Chapter15/Chapter15.png" width="400" height="300"> <br>
</div><br>

<center><font size="5em" color="#0091ff">XXE 공격 개요</font> </center>
<font size="3em" color="#0091ff">
<br>
<span style="color: #FFFFFF"></span>

-XML 타입의 데이터가 웹 요청을 통해 전송되고,<br>
서버에서 XML 외부 엔티티를 처리할 수 있도록<br>
설정된 경우 발생할 수 있음<br>
<br>
<br>

-사용자가 웹 어플리케이션으로 전달되는 XML 데이터를<br>
직접 업로드하거나 수정할 수 있는 경우, 공격자는 외부<br><br>
엔티티를 참조하는 XML 데이터를 전송하여 파일과 같은 서버<br>
내부의 정보를 탈취하거나 서비스 거부 공격, SSRF 등의 공격을
할 수 있음<br>


<center><font size="5em" color="#0091ff">XXE 공격 실습</font> </center>

<div align="center" >
<img src="/Art of Web Hacking/Chapter15/001.png" width="500" height="400"> <br>
</div>스샷. 1<br>

-bwapp>XML External Entity Attacks (XXE)에서<br>
[Any Bugs?]누르면 전송되는 데이터에서 XML이<br>
전송되는 것을 발견<br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter15/002.png" width="500" height="210"> <br>
</div>스샷. 2<br>

-bee가 응답 데이터도 있군요 → XML 태그의 내용이 응답 페이지에서<br>
발견된다면 XXE 공격을 시도해볼 수 있습니다.<br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter15/003.png" width="500" height="400"> <br>
</div>스샷. 3<br>
-해당 요청을 repeater로 보내고 문자열을 바꿔서 보냈더니 response<br>
쪽에서도 같은 문자열이 있음 → 서버가 xml을 처리하고 있습니다‥ōxō?<br>
서버가 xml을 처리하고 있습니다‥ōxō?<br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter15/004.png" width="500" height="400"> <br>
</div>스샷. 4<br>

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div><div style="line-height:130%">2</div><div style="line-height:130%">3</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#0086b3"></span><span style="color:#ff3399">&lt;</span><span style="color:#0086b3"></span><span style="color:#ff3399">!</span>DOCTYPE&nbsp;XXE&nbsp;[</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#0086b3"></span><span style="color:#ff3399">&lt;</span><span style="color:#0086b3"></span><span style="color:#ff3399">!</span>ENTITY&nbsp;XXE&nbsp;SYSTEM&nbsp;<span style="color:#993333">"file:///etc/passwd"</span><span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">]<span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span></div></div><div style="text-align:right;margin-top:-13px;margin-right:5px;font-size:9px;font-style:italic"><a href="http://colorscripter.com/info#e" target="_blank" style="color:#e5e5e5text-decoration:none">Colored by Color Scripter</a></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>

-body 부분에 < login > 태그에서 외부 엔티티를 참조할 수 있도록 하고<br>
패킷 전송하면 파일 내용을 출력되어 이렇게 해서 XXE 공격에 성공합니다.<br>


<center><font size="5em" color="#0091ff">XXE 공격 대응</font> </center>

-외부 엔티티 참조 기능이 필요하지 않은 경우 DTDs나 외부 엔티티 관련<br>
설정을 비활성화해 둡니다.(웹 방화벽 등 사용)<br>





<center>

=====================================<br>
<br>


장문의 글을 읽어주셔서 감사합니다.<br>
<br>
남은 시간 좋은 하루 되시고,<br>
<br>
하시는 일 잘 되시고,<br>
<br>
중국 코로나 조심하십시오:)<br>













<div align="center" >
<img src="/Art of Web Hacking/Chapter12/005.png" width="320" height="320"> <br>
</div>

</center>