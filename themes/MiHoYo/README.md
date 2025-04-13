# hexo-theme-MiHoYo

## 초심

헥소는 제가 개발한 것이 아니지만 헥소테마를 많이 보면 개발하고 싶은 충동이 일어납니다. [자신의 헥소테마를 작성](https://easyhexo.com/4-High-order-hexo-gamer/4-2-theme-develop/ #%E7%BC%96%E5%E8%E8%E8%E8%A5%B7%B7%B1%E7%E7%E7%E7%E7%E7%E7%E7%E7%E7%E7%E7%E7%E7%E7%E7%E7%E7%E7%E%E4%B%E9%A2%98)에서 말한 것처럼, "당신이 사용하는 테마를 두 개 이상의 블로그에 게시하는 것을 볼 때 당신은 스스로 작성해야 합니다. "사실 이 물건은 제가 2주 동안 개발했고, 매우 빨리도 썩었습니다. 같은 시기의 다른 작품들과 비교가 안 됩니다. 하지만 사람은 꿈을 이루고 싶고, 할 수 없는 것들을 원합니다. 개발 기간 동안 저는 저의 첨단 기술에 대해 완전히 반성하게 되었습니다. 왜냐하면 기술이 정말 너무 형편없었기 때문입니다. 저는 제 기술이 언제 이렇게 형편없을지 몰랐습니다(사실 좋은 스타일은 그렇게 쉽게 만들 수 없기 때문입니다), 네, 저도 천천히, 천천히 강해지고, 모든 것을 천천히 해야 합니다. ..., 지금 초판은 3가지 페이지 밖에 없습니다, 앞으로 열심히 하겠습니다, 화이팅. 🎉

연락을 원하시면 **issue**로 메시지를 남기시거나 이메일 연락 주시면 됩니다:1907065810@qq. com, 최대한 빨리 답변드리겠습니다.🎈

## 설명

이 hexo 테마는 2차원적인 hexo 테마를 표현하기 위한 것으로, 이후 이 컨셉에 맞게 개선하여 MiHoYo의 공식 페이지를 주요 타겟으로 하여 MiHoYo 게이머들에게 친근한 느낌을 줄 수 있는 2차원적인 컨셉의 콘텐츠를 제작하고 있으며, 현재도 적합한 스타일을 찾아 개발하고 있습니다. 더 좋은 아이디어가 있으면 연락주세요. 우리 모두 능력에 맞는 2차원 스타일의 헥소템을 만들기 위해 노력합시다.！！！😁

## 미리 보기

PC측:

![预览图片](https://i.loli.net/2021/10/24/bNlAoIfzGPQJcnt.png)

手机端：

<p align="center"> <image src="https://github.com/redhat123456/pohots/blob/master/gif/1.gif?raw=true"></image> </p>

Tanger: http://mihoyo.tanger.ltd/

이 테마를 사용하고 blog를 보여주고 싶으시다면 <ahref="https://github.com/redhat123456/hexo-theme-MiHoYo/issues ">issue</a>에 댓글로 남겨주시면 보여드리겠습니다. 🎃

## 설치

수동 설치

이 테마를 설치하려면 다음과 같이 하십시오.

1、下载 hexo-theme-MiHoYo

'루트 디렉터리/ themes' 이 파일을 선택한 후 오른쪽 단추로 'Git Bash Here'나 'PowerShell' 을 선택해도 됩니다. (이하 이 명령줄 창을 명령줄이라고 합니다.)

`git clone git@github. com:redhat123456/hexo-theme-MiHoYo.git`
or
`git clone https://github.com/redhat123456/hexo-theme-MiHoYo.git`

첫 번째 다운로드 테마 확장팩을 완성했습니다

2、설정`_config. yml`(⚠ 주의할 점: 여기의 `_config. yml` 파일은 루트 디렉터리의 `_config. yml`）

편집기로 파일을 연 다음,

`theme: XXXX` 이 줄에서 theme 뒤에 있는 `XXXX`를 `hexo-theme-MiHoYo`로 고칩니다.

3. 배치 hexo 페이지 및 미리보기 hexo 페이지

루트 디렉터리에서 명령줄을 열고 `hexog`와 `hexos`를 차례로 입력하고 브라우저를 열고 `http://localhost:4000`을 입력하여 테마 효과를 미리 봅니다.

## 글짓기

- 참고 [헥소|쓰기](https://hexo.io/zh-cn/docs/writing)

* 也可以参考 GitHub 的 [markdown 教程](https://guides.github.com/features/mastering-markdown/)

* 기사 제목과 분류 추가, 더 많은 특성은 [Hexo|Front-matter](https://hexo.io/zh-cn/docs/front-matter) , 예시:

```markdown
---
title: 'Hello World ! '
date: 2020-10-23 21:54:02
tags: code
category: Example
---
```

## 기본 스타일 수정

우리는 'theme/hexo-theme-MiHoYo' 파일 아래의 '_config. yml`은 주제 양식을 수정하는데, 주로 다음과 같은 양식을 수정할 수 있습니다.

### 위쪽 탐색 모음 설정

테마 페이지에서 '_config. yml`에서 이 코드 라인을 다음과 같이 수정합니다.

```markdown
menuname: Tanger's blog

# 닉네임 | Your Name

author: Your Name

# main menu navigation

menu:
about 👀: /about
홈 사이트 방문 🎃: http://tanger.cloud/
GitHub🧨: https://github.com/KuraiLuna
```

#### author

blog 작성자 이름

#### menuname

왼쪽 링크, 기본적으로 blog 첫 페이지를 가리킵니다

#### menu

오른쪽 상단 탐색 모음

설정:
`:` 번호 앞에 대응하는 것은 제목명 뒤에 링크를 나타내며, 위쪽 탐색 모음은 바로 이 줄의 코드에 따라 사용자 정의 탐색 모음입니다.

### 정보바 설정

대응하는 것은 `_config. yml`의

```markdown
topmenu:
홈:/
정보: /about

## 웹 설명

description:이봐,나는 Tanger야~이것은 내 자역이야, 전시용 Hexo 주제:MiHoYo. 방문을 환영합니다!

## 사이트키워드: 영어 쉼표로 구분

keywords: hexo,theme,MiHoYo

## 블로그 프로필 사진

img_src: https://avatars.githubusercontent.com/u/57751257?v=4

# 사이트 제목 | Title

logo_title: Hexo Theme

#슬로건 | Your Slogan
words: Your Words
```

해당 정보에 따라 수정할 수 있습니다

## 리뷰 시스템

이 테마는 [Valine](https://valine.js.org/) )을 지원합니다.
테마 목록 아래의 '_config. yml` 파일에서`valine:` 의`app_id:` 와`app_key:`.

参考 [Valine 快速开始](https://valine.js.org/quickstart.html)

开启邮件提醒：[zhaojun1998 / Valine-Admin](https://github.com/zhaojun1998/Valine-Admin)

## 개발참가

### 개발자

- [Tanger](https://github.com/redhat123456)
- [Yue_plus](https://github.com/Yue-plus)

> 欢迎提交 [Issues](https://github.com/redhat123456/hexo-theme-MiHoYo/issues/new) 与 [PR](https://github.com/redhat123456/hexo-theme-MiHoYo/issues/pulls)

### 개발 참여에 필요한 문서

- [Hexo 官方文档](https://hexo.io/zh-cn/docs/templates)
- [ejs 템플릿 엔진 중국어 문서](https://ejs.bootcss.com/)

- 또한 몇몇 거물들의 blog를 인용합니다.
> - <https://easyhexo.com/>
> - [헥소가 만든 블로그에 LaTeX 지원 요청](http://cps.ninja/2019/03/16/hexo-with-latex/)
> - [헥소 콘텐츠 개발 - ﹏ 원숭이가 모신 구원병 - 블로그 정원](https://www.cnblogs.com/yyhh/p/11058985.html)
> - [벽][헥소 테마 개발 경험 잡담 | MARKSZ T블로그](https://molunerfinn.com/make-a-hexo-theme/)
> - 【墙】[Hexo 主题开发指南 | Peak Xin's Blog](https://xinyufeng.net/2019/04/15/hexo-theme-guide/)

## 다음에 구현되는 기능

* 적응 이동단
* 배경 그림 추가하기
* 메시지 카드 업데이트 효과

## 주제 개발 지원

이 주제를 좋아한다면:

- 작은 별 하나 주세요`(/▽＼)`
> - 작은 목표 50star 새로운 콘셉트를 만들어주세요~
- QQ 단톡방: 808985048
>단톡방 개발 위주, 뻥튀기, 공유하시고 싶은 코드 있으시면 언제든지 환영합니다~ ===== (￣▽￣*)b`
