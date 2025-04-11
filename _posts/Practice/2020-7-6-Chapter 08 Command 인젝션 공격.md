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
<img src="/Art of Web Hacking/Chapter8/Chapter8.png" width="400" height="300"> <br>
</div><br>


<center><font size="5em" color="#0091ff">Chapter 08. Command 인젝션 공격</font> </center>
<font size="3em" color="#0091ff">
<center>커맨드 인젝션 공격 개요</center>
<br>
-웹 요청 메시지에 임의의 시스템 명령어를 삽입하고 전송하여<br> 웹 서버에서 해당 명령어를 실행하는 것입니다.
<br><br>
<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">ping&nbsp;x.x.x.x;&nbsp;cat&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">/</span>etc<span style="color:#0086b3"></span><span style="color:#a71d5d">/</span>passwd</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>
<br>

-세미클론을 이용한 추가 명령을 실행, etc/passwd파일은 리눅스 사용자 목록이<br>
들어있는 파일을 알아내기 위한 실습 및 복습입니다.
<br>

<center>커맨드 인젝션 공격 실습</center>
<br>

-웹 요청 메시지에 임의의 시스템 명령어를 삽입하고 전송하여<br> 웹 서버에서 해당
<div align="center" >
<img src="/Art of Web Hacking/Chapter8/001.png" width="600" height="500"> <br>
</div>스샷. 1<br><br>
- 2의 경우 시스템 명령어를 내리는 함수입니다, target 변수는 1의 ip이지요<br>
('-c' 옵션은 핑 몇 번 때 릴지 성정하는 것)
<div align="center" >
<img src="/Art of Web Hacking/Chapter8/002.png" width="600" height="200"> <br>
</div>스샷. 2<br><br>
- ping -c 4 127.0.0.1; ls를 실행하면 디렉토리 내용이 출력됩니다.

<div align="center" >
<img src="/Art of Web Hacking/Chapter8/003.png" width="600" height="200"> <br>
</div>스샷. 3<br><br>
- ping 명령어 결과가 표시되는 게 아니라 디렉토리가 출력됨니다.<br><br>
<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">;&nbsp;cat&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">/</span>etc<span style="color:#0086b3"></span><span style="color:#a71d5d">/</span>passwd</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>
<br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter8/004.png" width="600" height="500"> <br>
</div>스샷. 4<br><br>
- 리눅스를 대상으로 파라미터에 ; 등의 특수문자와 함께 시스템 명령어를 입력하여 커맨드<br>

인젝션을 시도하고 윈도의 경우 &&를 사용합니다.
<center>커맨드 인젝션 공격 대응</center>
<br>

-소스 코스에서 exec()나 system()과 같은<br>
직접적으로 명령어를 실행하는 함수 지양하시고<br>
→ 라이브러리를 사용합시다.
<br>

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#0086b3"></span><span style="color:#a71d5d">&lt;</span><span style="color:#0086b3"></span><span style="color:#a71d5d">-</span><span style="color:#0086b3"></span><span style="color:#a71d5d">-</span>&nbsp;system(“mkdir&nbsp;$dir_name”)이&nbsp;아닌&nbsp;mkdir($dir_name)&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">-</span><span style="color:#0086b3"></span><span style="color:#a71d5d">-</span><span style="color:#0086b3"></span><span style="color:#a71d5d">&gt;</span></div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>


<br><br>

<center>==========================================<br>
<br>

이어서 올려봅니다, =^∇^*=<br>

이번 챕터는 비교적 간단한(?)<br>

부분이었습니다(ōx ō)?<br>
<span style="color: #FFFFFF">~~부분이었습니다(ōx ō)?~~</span><br>



다음날에는 챕터 9 이여서 올리겠습니다<br>

이글을 읽어주신 분들께 정말 감사합니다 (✿╹◡╹)<br>


좋은 하루 되시고, 하시는 일 잘되시고<br>

중국산 코로나 조심하시길 바랍니다.<br>


<div align="center" >
<img src="/Art of Web Hacking/Chapter8/005.png" width="320" height="320"> <br>
</div>



</center>