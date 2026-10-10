---
title: 새 글 작성하기
date: 2026-09-04 11:00:00 +0900
categories: [블로그, 튜토리얼]
tags: [writing]
render_with_liquid: false
---

이 튜토리얼에서는 _Chirpy_ 템플릿에서 글을 작성하는 방법을 안내합니다. 많은 기능이 특정 변수를 설정해야 동작하므로, Jekyll을 사용해 본 적이 있더라도 한 번 읽어 볼 만합니다.

## 파일 이름과 경로

`YYYY-MM-DD-TITLE.EXTENSION`{: .filepath} 형식의 새 파일을 만들어 루트 디렉터리의 `_posts`{: .filepath}에 넣습니다. 이때 `EXTENSION`{: .filepath}은 반드시 `md`{: .filepath} 또는 `markdown`{: .filepath} 중 하나여야 합니다. 파일을 만드는 시간을 줄이고 싶다면 [`Jekyll-Compose`](https://github.com/jekyll/jekyll-compose) 플러그인을 사용해 보세요.

## Front Matter

기본적으로 글 맨 위에 아래와 같이 [Front Matter](https://jekyllrb.com/docs/front-matter/)를 작성해야 합니다.

```yaml
---
title: TITLE
date: YYYY-MM-DD HH:MM:SS +/-TTTT
categories: [TOP_CATEGORY, SUB_CATEGORY]
tags: [TAG]     # 태그 이름은 항상 소문자로 작성
---
```

> 글의 _layout_ 은 기본적으로 `post`로 설정되어 있으므로, Front Matter에 _layout_ 변수를 추가할 필요가 없습니다.
{: .prompt-tip }

### 날짜의 시간대

글의 게시 날짜를 정확하게 기록하려면 `_config.yml`{: .filepath}의 `timezone`을 설정할 뿐만 아니라, 글의 Front Matter에 있는 `date` 변수에도 시간대를 적어야 합니다. 형식은 `+/-TTTT`이며, 예를 들면 `+0900`입니다.

### 카테고리와 태그

각 글의 `categories`는 최대 두 개의 항목을 갖도록 설계되어 있으며, `tags`는 0개부터 무제한까지 넣을 수 있습니다. 예를 들면 다음과 같습니다.

```yaml
---
categories: [Animal, Insect]
tags: [bee]
---
```

### 작성자 정보

글의 작성자 정보는 보통 _Front Matter_ 에 적지 않아도 됩니다. 기본적으로 설정 파일의 `social.name` 변수와 `social.links`의 첫 번째 항목에서 가져옵니다. 하지만 아래와 같이 덮어쓸 수도 있습니다.

`_data/authors.yml`에 작성자 정보를 추가합니다. (사이트에 이 파일이 없다면 새로 만들면 됩니다.)

```yaml
<author_id>:
  name: <full name>
  twitter: <twitter_of_author>
  url: <homepage_of_author>
```
{: file="_data/authors.yml" }

그런 다음 `author`로 한 명을, `authors`로 여러 명을 지정합니다.

```yaml
---
author: <author_id>                     # 한 명일 때
# 또는
authors: [<author1_id>, <author2_id>]   # 여러 명일 때
---
```

참고로 `author` 키로도 여러 명을 지정할 수 있습니다.

> `_data/authors.yml`{: .filepath } 파일에서 작성자 정보를 읽어 오면 페이지에 `twitter:creator` 메타 태그가 추가되어 [Twitter 카드](https://developer.twitter.com/en/docs/twitter-for-websites/cards/guides/getting-started#card-and-content-attribution)가 풍부해지고 SEO에도 도움이 됩니다.
{: .prompt-info }

### 글 설명

기본적으로 글의 앞부분 몇 단어가 홈 화면의 글 목록, _더 읽어보기(Further Reading)_ 영역, RSS 피드 XML에 표시됩니다. 자동으로 생성된 설명을 쓰고 싶지 않다면 _Front Matter_ 의 `description` 필드로 직접 지정할 수 있습니다.

```yaml
---
description: 글의 짧은 요약.
---
```

또한 `description` 내용은 글 페이지의 제목 아래에도 표시됩니다.

## 목차

기본적으로 목차(**T**able **o**f **C**ontents, TOC)는 글 오른쪽 패널에 표시됩니다. 전체적으로 끄려면 `_config.yml`{: .filepath}에서 `toc` 변수 값을 `false`로 설정하세요. 특정 글에서만 끄려면 해당 글의 [Front Matter](https://jekyllrb.com/docs/front-matter/)에 다음을 추가합니다.

```yaml
---
toc: false
---
```

## 댓글

댓글의 전체 설정은 `_config.yml`{: .filepath} 파일의 `comments.provider` 옵션으로 정합니다. 이 변수에 댓글 시스템을 지정하면 모든 글에 댓글이 활성화됩니다.

특정 글에서 댓글을 닫으려면 해당 글의 **Front Matter**에 다음을 추가합니다.

```yaml
---
comments: false
---
```

## 미디어

_Chirpy_ 에서는 이미지, 오디오, 동영상을 미디어 리소스라고 부릅니다.

### URL 접두사

한 글 안에서 여러 리소스에 같은 URL 접두사를 반복해서 적어야 할 때가 있습니다. 번거로운 작업이지만 두 가지 파라미터를 설정하면 피할 수 있습니다.

- CDN으로 미디어 파일을 호스팅한다면 `_config.yml`{: .filepath }에 `cdn`을 지정할 수 있습니다. 그러면 사이트 아바타와 글의 미디어 리소스 URL 앞에 CDN 도메인이 붙습니다.

  ```yaml
  cdn: https://cdn.com
  ```
  {: file='_config.yml' .nolineno }

- 현재 글/페이지 범위의 리소스 경로 접두사를 지정하려면 글의 _front matter_ 에 `media_subpath`를 설정합니다.

  ```yaml
  ---
  media_subpath: /path/to/media/
  ---
  ```
  {: .nolineno }

`site.cdn`과 `page.media_subpath` 옵션은 따로 또는 함께 사용할 수 있으며, 최종 리소스 URL을 유연하게 구성할 수 있습니다: `[site.cdn/][page.media_subpath/]file.ext`

### 이미지

#### 캡션

이미지 다음 줄에 기울임꼴 텍스트를 추가하면, 그 텍스트가 캡션이 되어 이미지 아래에 표시됩니다.

```markdown
![img-description](/path/to/image)
_Image Caption_
```
{: .nolineno}

#### 크기

이미지가 로드될 때 페이지 레이아웃이 밀리지 않도록, 각 이미지에 너비와 높이를 지정하는 것이 좋습니다.

```markdown
![Desktop View](/assets/img/sample/mockup.png){: width="700" height="400" }
```
{: .nolineno}

> SVG는 최소한 _width_ 를 지정해야 하며, 그렇지 않으면 표시되지 않습니다.
{: .prompt-info }

_Chirpy v5.0.0_ 부터 `height`와 `width`는 약어(`height` → `h`, `width` → `w`)를 지원합니다. 아래 예시는 위와 같은 효과를 냅니다.

```markdown
![Desktop View](/assets/img/sample/mockup.png){: w="700" h="400" }
```
{: .nolineno}

#### 위치

기본적으로 이미지는 가운데 정렬되지만, `normal`, `left`, `right` 클래스 중 하나를 사용해 위치를 지정할 수 있습니다.

> 위치를 지정한 경우에는 이미지 캡션을 추가하면 안 됩니다.
{: .prompt-warning }

- **기본 위치**

  아래 예시에서는 이미지가 왼쪽 정렬됩니다.

  ```markdown
  ![Desktop View](/assets/img/sample/mockup.png){: .normal }
  ```
  {: .nolineno}

- **왼쪽으로 띄우기**

  ```markdown
  ![Desktop View](/assets/img/sample/mockup.png){: .left }
  ```
  {: .nolineno}

- **오른쪽으로 띄우기**

  ```markdown
  ![Desktop View](/assets/img/sample/mockup.png){: .right }
  ```
  {: .nolineno}

#### 다크/라이트 모드

이미지가 테마의 다크/라이트 모드 설정을 따르게 할 수 있습니다. 다크 모드용과 라이트 모드용 이미지 두 개를 준비한 뒤, 각각 특정 클래스(`dark` 또는 `light`)를 지정하면 됩니다.

```markdown
![Light mode only](/path/to/light-mode.png){: .light }
![Dark mode only](/path/to/dark-mode.png){: .dark }
```

#### 그림자

프로그램 창 스크린샷에는 그림자 효과를 넣는 것을 고려해 볼 수 있습니다.

```markdown
![Desktop View](/assets/img/sample/mockup.png){: .shadow }
```
{: .nolineno}

#### 미리보기 이미지

글 맨 위에 이미지를 넣고 싶다면 `1200 x 630` 해상도의 이미지를 준비하세요. 이미지 비율이 `1.91 : 1`이 아니면 이미지가 확대·축소되고 잘립니다.

이 조건을 알았다면 이미지 속성을 설정할 수 있습니다.

```yaml
---
image:
  path: /path/to/image
  alt: image alternative text
---
```

[`media_subpath`](#url-접두사)는 미리보기 이미지에도 적용됩니다. 즉, `media_subpath`가 설정되어 있다면 `path` 속성에는 이미지 파일명만 적으면 됩니다.

간단하게 `image`만으로 경로를 지정할 수도 있습니다.

```yml
---
image: /path/to/image
---
```

#### LQIP

미리보기 이미지의 경우:

```yaml
---
image:
  lqip: /path/to/lqip-file # 또는 base64 URI
---
```

> LQIP는 "[텍스트와 타이포그래피](../text-and-typography/)" 글의 미리보기 이미지에서 확인할 수 있습니다.

일반 이미지의 경우:

```markdown
![Image description](/path/to/image){: lqip="/path/to/lqip-file" }
```
{: .nolineno }

### 소셜 미디어 플랫폼

아래 문법으로 소셜 미디어 플랫폼의 동영상/오디오를 삽입할 수 있습니다.

```liquid
{% include embed/{Platform}.html id='{ID}' %}
```

`Platform`은 플랫폼 이름의 소문자이고, `ID`는 동영상 ID입니다.

아래 표는 동영상/오디오 URL에서 필요한 두 파라미터를 찾는 방법과, 현재 지원하는 플랫폼을 보여 줍니다.

| 동영상 URL                                                                                                                  | 플랫폼     | ID                       |
| -------------------------------------------------------------------------------------------------------------------------- | ---------- | :----------------------- |
| [https://www.**youtube**.com/watch?v=**H-B46URT4mg**](https://www.youtube.com/watch?v=H-B46URT4mg)                         | `youtube`  | `H-B46URT4mg`            |
| [https://www.**twitch**.tv/videos/**1634779211**](https://www.twitch.tv/videos/1634779211)                                 | `twitch`   | `1634779211`             |
| [https://www.**bilibili**.com/video/**BV1Q44y1B7Wf**](https://www.bilibili.com/video/BV1Q44y1B7Wf)                         | `bilibili` | `BV1Q44y1B7Wf`           |
| [https://www.open.**spotify**.com/track/**3OuMIIFP5TxM8tLXMWYPGV**](https://open.spotify.com/track/3OuMIIFP5TxM8tLXMWYPGV) | `spotify`  | `3OuMIIFP5TxM8tLXMWYPGV` |

Spotify는 몇 가지 추가 파라미터를 지원합니다.

- `compact` - 작은 플레이어로 표시 (예: `{% include embed/spotify.html id='3OuMIIFP5TxM8tLXMWYPGV' compact=1 %}`)
- `dark` - 다크 테마 강제 적용 (예: `{% include embed/spotify.html id='3OuMIIFP5TxM8tLXMWYPGV' dark=1 %}`)

### 동영상 파일

동영상 파일을 직접 삽입하려면 아래 문법을 사용합니다.

```liquid
{% include embed/video.html src='{URL}' %}
```

`URL`은 동영상 파일의 주소입니다. 예: `/path/to/sample/video.mp4`

삽입한 동영상 파일에 추가 속성을 지정할 수도 있습니다. 사용할 수 있는 속성은 다음과 같습니다.

- `poster='/path/to/poster.png'` — 동영상을 내려받는 동안 표시할 포스터 이미지
- `title='Text'` — 동영상 아래에 표시되는 제목 (이미지 캡션과 같은 모양)
- `autoplay=true` — 가능한 시점에 바로 자동 재생
- `loop=true` — 끝까지 재생되면 처음으로 돌아가 반복 재생
- `muted=true` — 처음에 소리를 끈 상태로 재생
- `types` — 추가 동영상 형식의 확장자를 `|`로 구분해 지정. 해당 파일들은 기본 동영상 파일과 같은 디렉터리에 있어야 합니다.

위 속성을 모두 사용한 예시는 다음과 같습니다.

```liquid
{%
  include embed/video.html
  src='/path/to/video.mp4'
  types='ogg|mov'
  poster='poster.png'
  title='Demo video'
  autoplay=true
  loop=true
  muted=true
%}
```

### 오디오 파일

오디오 파일을 직접 삽입하려면 아래 문법을 사용합니다.

```liquid
{% include embed/audio.html src='{URL}' %}
```

`URL`은 오디오 파일의 주소입니다. 예: `/path/to/audio.mp3`

삽입한 오디오 파일에 추가 속성을 지정할 수도 있습니다. 사용할 수 있는 속성은 다음과 같습니다.

- `title='Text'` — 오디오 아래에 표시되는 제목 (이미지 캡션과 같은 모양)
- `types` — 추가 오디오 형식의 확장자를 `|`로 구분해 지정. 해당 파일들은 기본 오디오 파일과 같은 디렉터리에 있어야 합니다.

위 속성을 모두 사용한 예시는 다음과 같습니다.

```liquid
{%
  include embed/audio.html
  src='/path/to/audio.mp3'
  types='ogg|wav|aac'
  title='Demo audio'
%}
```

## 고정 글

하나 이상의 글을 홈 화면 맨 위에 고정할 수 있으며, 고정된 글은 게시 날짜의 역순으로 정렬됩니다. 다음과 같이 설정합니다.

```yaml
---
pin: true
---
```

## 프롬프트

프롬프트에는 `tip`, `info`, `warning`, `danger` 등 여러 유형이 있습니다. 인용문에 `prompt-{type}` 클래스를 추가하면 만들 수 있습니다. 예를 들어 `info` 유형의 프롬프트는 다음과 같이 정의합니다.

```md
> Example line for prompt.
{: .prompt-info }
```
{: .nolineno }

## 문법

### 인라인 코드

```md
`inline code part`
```
{: .nolineno }

### 파일 경로 강조

```md
`/path/to/a/file.extend`{: .filepath}
```
{: .nolineno }

### 코드 블록

마크다운 기호 ```` ``` ````로 아래와 같이 쉽게 코드 블록을 만들 수 있습니다.

````md
```
This is a plaintext code snippet.
```
````

#### 언어 지정

```` ```{language} ````를 사용하면 구문 강조가 적용된 코드 블록이 만들어집니다.

````markdown
```yaml
key: value
```
````

> Jekyll 태그 `{% highlight %}`는 이 테마와 호환되지 않습니다.
{: .prompt-danger }

#### 줄 번호

기본적으로 `plaintext`, `console`, `terminal`을 제외한 모든 언어에 줄 번호가 표시됩니다. 코드 블록의 줄 번호를 숨기려면 `nolineno` 클래스를 추가합니다.

````markdown
```shell
echo 'No more line numbers!'
```
{: .nolineno }
````

#### 파일명 지정

코드 블록 위쪽에 코드 언어가 표시되는 것을 보셨을 겁니다. 이를 파일명으로 바꾸고 싶다면 `file` 속성을 추가하면 됩니다.

````markdown
```shell
# content
```
{: file="path/to/file" }
````

#### Liquid 코드

**Liquid** 코드 조각을 그대로 보여 주려면 Liquid 코드를 `{% raw %}`와 `{% endraw %}`로 감쌉니다.

````markdown
{% raw %}
```liquid
{% if product.title contains 'Pack' %}
  This product's title contains the word Pack.
{% endif %}
```
{% endraw %}
````

또는 글의 YAML 블록에 `render_with_liquid: false`를 추가해도 됩니다. (Jekyll 4.0 이상 필요)

## 수식

수식은 [**MathJax**][mathjax]로 생성합니다. 웹사이트 성능을 위해 수식 기능은 기본적으로 불러오지 않지만, 다음과 같이 활성화할 수 있습니다.

[mathjax]: https://www.mathjax.org/

```yaml
---
math: true
---
```

수식 기능을 활성화한 뒤에는 아래 문법으로 수식을 추가할 수 있습니다.

- **블록 수식**은 `$$ math $$`로 추가하며, `$$` 앞뒤에 빈 줄이 **반드시** 있어야 합니다.
  - **수식 번호 붙이기**는 `$$\begin{equation} math \end{equation}$$`로 추가합니다.
  - **수식 번호 참조하기**는 수식 블록 안에 `\label{eq:label_name}`을, 본문에 `\eqref{eq:label_name}`을 사용합니다. (아래 예시 참고)
- **인라인 수식**(문장 안)은 `$$ math $$`로 추가하며, `$$` 앞뒤에 빈 줄이 없어야 합니다.
- **인라인 수식**(목록 안)은 `\$$ math $$`로 추가합니다.

```markdown
<!-- 블록 수식, 빈 줄을 모두 유지 -->

$$
LaTeX_math_expression
$$

<!-- 수식 번호, 빈 줄을 모두 유지 -->

$$
\begin{equation}
  LaTeX_math_expression
  \label{eq:label_name}
\end{equation}
$$

Can be referenced as \eqref{eq:label_name}.

<!-- 문장 안 인라인 수식, 빈 줄 없음 -->

"Lorem ipsum dolor sit amet, $$ LaTeX_math_expression $$ consectetur adipiscing elit."

<!-- 목록 안 인라인 수식, 첫 번째 `$`를 이스케이프 -->

1. \$$ LaTeX_math_expression $$
2. \$$ LaTeX_math_expression $$
3. \$$ LaTeX_math_expression $$
```

> `v7.0.0`부터 **MathJax** 설정 옵션은 `assets/js/data/mathjax.js`{: .filepath } 파일로 옮겨졌으며, [확장 기능][mathjax-exts] 추가 등 필요에 따라 옵션을 변경할 수 있습니다.  
> `chirpy-starter`로 사이트를 만들었다면, gem 설치 디렉터리(`bundle info --path jekyll-theme-chirpy` 명령으로 확인)에서 이 파일을 내 저장소의 같은 디렉터리로 복사하세요.
{: .prompt-tip }

[mathjax-exts]: https://docs.mathjax.org/en/latest/input/tex/extensions/index.html

## Mermaid

[**Mermaid**](https://github.com/mermaid-js/mermaid)는 훌륭한 다이어그램 생성 도구입니다. 글에서 사용하려면 YAML 블록에 다음을 추가합니다.

```yaml
---
mermaid: true
---
```

그런 다음 다른 마크다운 언어처럼 사용하면 됩니다. 그래프 코드를 ```` ```mermaid ````와 ```` ``` ````로 감싸면 됩니다.

## 더 알아보기

Jekyll 글에 대해 더 알고 싶다면 [Jekyll 문서: Posts](https://jekyllrb.com/docs/posts/)를 참고하세요.
