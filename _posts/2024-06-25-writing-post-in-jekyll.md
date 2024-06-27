---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "jekyll 블로그 포스팅 syntax"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-06-25
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [git, gitpage]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [github, blog, jekyll]
# 공개여부 설정. true면 공개하고 false면 공개하지 않는다.
published: true
# 사용자 정의 변수. 본문에서 {{ page. food }} 형태로 사용 가능하다.
food: Pizza
# 작성자. authors.yml 파일의 아이디를 사용한다.
author: jihwan
# 만약 우측 Table Of Contents를 사용하고 싶지 않다면 false로 전환
toc: true
# 댓글 사용 여부, _config.yml의 comments.active를 사용한다.
comments: true
# image:
#  path: /path/to/image
#  alt: image alternative text
# pin: true
---

## 개발 환경

Github 블로그 Chirpy 테마를 사용했을 때의 포스팅 문법입니다. 다른 테마에서는 다를 수 있습니다.

## Headings
H2 Heading 부터 Table Of Contents에 적용됩니다. 
```markdown
# H1 Heading
## H2 Heading
### H3 Heading
#### H4 Heading
##### H5 Heading
```
## Paragraph
line break<br>
*italic text*<br>
**bold text**<br>
***bold and italic text***
```markdown
<br>
*italic text*
**bold text**
***bold and italic text***
```
### 인용구
> 인용구

```markdown
> 인용구
> 다음 줄
```

### Prompts

> An example showing the `tip` type prompt.
{: .prompt-tip }

> An example showing the `info` type prompt.
{: .prompt-info }

> An example showing the `warning` type prompt.
{: .prompt-warning }

> An example showing the `danger` type prompt.
{: .prompt-danger }


```markdown

> An example showing the `tip` type prompt.
{: .prompt-tip }

> An example showing the `info` type prompt.
{: .prompt-info }

> An example showing the `warning` type prompt.
{: .prompt-warning }

> An example showing the `danger` type prompt.
{: .prompt-danger }

```

## Lists
### Ordered Lists
1. First item
2. Second item
3. Third item
4. Fourth item

```markdown
1. First item
2. Second item
3. Third item
4. Fourth item
```

### Unordered Lists
- First item
- Second item
- Third item
  - Fourth item

```markdown
- First item
- Second item
- Third item
  - Fourth item
```

### ToDo list
- [ ] Mercury
- [x] Venus
- [x] Earth (Orbit/Moon)
- [x] Mars
- [ ] Jupiter
```markdown
- [ ] Mercury
- [x] Venus
- [x] Earth (Orbit/Moon)
- [x] Mars
- [ ] Jupiter
```


## Links
[나의 링크](https://intoreal.github.io)
```markdown
[나의 링크](https://intoreal.github.io)
```

## Image
```markdown
![Desktop View](/assets/img/sample/mockup.png){: width="700" height="400" }
![Desktop View](/assets/img/sample/mockup.png){: .normal }
![Desktop View](/assets/img/sample/mockup.png){: .left }
![Desktop View](/assets/img/sample/mockup.png){: .right }
![Desktop View](/assets/img/sample/mockup.png){: .shadow }

```