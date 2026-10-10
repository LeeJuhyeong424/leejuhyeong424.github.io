---
title: GitHub Pages와 Jekyll
description: Jekyll은 GitHub Pages를 기본으로 지원하는 정적 사이트 생성기입니다.
date: 2026-10-17 00:00:00 +0900
categories: [GitHub Pages, Jekyll]
tags: [github-pages, jekyll]
---

> `github-pages` gem은 일부 워크플로에서 여전히 지원되지만, 이제는 GitHub Actions로 GitHub Pages 사이트를 배포하고 자동화하는 방식이 권장됩니다.
{: .prompt-info }

## Jekyll 소개

Jekyll은 GitHub Pages를 기본으로 지원하고 빌드 과정이 단순한 정적 사이트 생성기입니다. Jekyll은 Markdown과 HTML 파일을 가져와 내가 고른 레이아웃에 맞춰 완성된 정적 웹사이트를 만들어 줍니다. Jekyll은 Markdown과, 사이트에 동적 콘텐츠를 불러오는 템플릿 언어인 Liquid를 지원합니다. 자세한 내용은 [Jekyll](https://jekyllrb.com/)을 참고하세요.

Jekyll은 Windows를 공식적으로 지원하지 않습니다. 자세한 내용은 Jekyll 문서의 [Windows에서 Jekyll 사용하기](https://jekyllrb.com/docs/windows/#installation)를 참고하세요.

GitHub Pages에서는 Jekyll 사용을 권장합니다. 원한다면 다른 정적 사이트 생성기를 사용하거나, 로컬 또는 다른 서버에서 빌드 과정을 직접 구성할 수도 있습니다. 자세한 내용은 [GitHub Pages 사이트 만들기: 정적 사이트 생성기](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site#static-site-generators)를 참고하세요.

## GitHub Pages 사이트에서 Jekyll 설정하기

사이트 테마나 플러그인 같은 Jekyll 설정 대부분은 `_config.yml`{: .filepath} 파일을 수정해 바꿀 수 있습니다. 자세한 내용은 Jekyll 문서의 [Configuration](https://jekyllrb.com/docs/configuration/)을 참고하세요.

일부 설정은 GitHub Pages 사이트에서 바꿀 수 없습니다.

```yaml
lsi: false
safe: true
source: [your repo's top level directory]
incremental: false
highlighter: rouge
gist:
  noscript: false
kramdown:
  math_engine: mathjax
  syntax_highlighter: rouge
```

기본적으로 Jekyll은 다음과 같은 파일이나 폴더는 빌드하지 않습니다.

- `/node_modules` 또는 `/vendor` 폴더 안에 있는 것
- `_`, `.`, `#`로 시작하는 것
- `~`로 끝나는 것
- 설정 파일의 `exclude` 설정으로 제외된 것

이런 파일도 Jekyll이 처리하게 하려면 설정 파일의 `include` 설정을 사용하면 됩니다.

## Front matter

사이트의 페이지나 글에 제목, 레이아웃 같은 변수와 메타데이터를 지정하려면 Markdown 또는 HTML 파일 맨 위에 YAML front matter를 추가합니다. 자세한 내용은 Jekyll 문서의 [Front Matter](https://jekyllrb.com/docs/front-matter/)를 참고하세요.

글이나 페이지에 `site.github`를 추가하면 저장소 관련 메타데이터를 사이트에 넣을 수 있습니다. 자세한 내용은 Jekyll Metadata 문서의 [`site.github` 사용하기](https://jekyll.github.io/github-metadata/site.github/)를 참고하세요.

## 테마

GitHub Pages 사이트에 Jekyll 테마를 추가해 사이트의 모양과 분위기를 바꿀 수 있습니다. 자세한 내용은 Jekyll 문서의 [Themes](https://jekyllrb.com/docs/themes/)를 참고하세요.

GitHub에서 지원하는 테마를 사이트에 추가할 수 있습니다. 자세한 내용은 [지원되는 테마](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll#supported-themes)와 [Jekyll로 GitHub Pages 사이트에 테마 추가하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll)를 참고하세요.

GitHub에 공개된 다른 오픈 소스 Jekyll 테마를 쓰려면 테마를 직접 추가하면 됩니다. 자세한 내용은 [GitHub에 공개된 테마](https://github.com/topics/jekyll-theme)와 [Jekyll로 GitHub Pages 사이트에 테마 추가하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll)를 참고하세요.

테마 파일을 수정하면 테마의 기본값을 무엇이든 덮어쓸 수 있습니다. 자세한 내용은 사용하는 테마의 문서와 Jekyll 문서의 [테마 기본값 덮어쓰기](https://jekyllrb.com/docs/themes/#overriding-theme-defaults)를 참고하세요.

## 플러그인

Jekyll 플러그인을 내려받거나 직접 만들어 사이트에서 Jekyll의 기능을 넓힐 수 있습니다. 예를 들어 [jemoji](https://github.com/jekyll/jemoji) 플러그인을 쓰면 GitHub에서처럼 사이트의 어느 페이지에서나 GitHub 스타일 이모지를 사용할 수 있습니다. 자세한 내용은 Jekyll 문서의 [Plugins](https://jekyllrb.com/docs/plugins/)를 참고하세요.

GitHub Pages는 기본으로 켜져 있고 끌 수 없는 다음 플러그인을 사용합니다.

- [`jekyll-coffeescript`](https://github.com/jekyll/jekyll-coffeescript)
- [`jekyll-default-layout`](https://github.com/benbalter/jekyll-default-layout)
- [`jekyll-gist`](https://github.com/jekyll/jekyll-gist)
- [`jekyll-github-metadata`](https://github.com/jekyll/github-metadata)
- [`jekyll-optional-front-matter`](https://github.com/benbalter/jekyll-optional-front-matter)
- [`jekyll-paginate`](https://github.com/jekyll/jekyll-paginate)
- [`jekyll-readme-index`](https://github.com/benbalter/jekyll-readme-index)
- [`jekyll-titles-from-headings`](https://github.com/benbalter/jekyll-titles-from-headings)
- [`jekyll-relative-links`](https://github.com/benbalter/jekyll-relative-links)

`_config.yml`{: .filepath} 파일의 `plugins` 설정에 플러그인 gem을 추가하면 플러그인을 더 켤 수 있습니다. 자세한 내용은 Jekyll 문서의 [Configuration](https://jekyllrb.com/docs/configuration/)을 참고하세요.

지원되는 플러그인 목록은 GitHub Pages 사이트의 [Dependency versions](https://pages.github.com/versions.json)에서 확인할 수 있습니다. 특정 플러그인의 사용법은 해당 플러그인의 문서를 참고하세요.

> GitHub Pages gem을 최신 상태로 유지하면 모든 플러그인의 최신 버전을 사용할 수 있습니다. 자세한 내용은 [GitHub Pages gem 업데이트하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll#updating-the-github-pages-gem)와 GitHub Pages 사이트의 [Dependency versions](https://pages.github.com/versions.json)를 참고하세요.
{: .prompt-tip }

GitHub Pages는 지원되지 않는 플러그인을 사용하는 사이트를 빌드할 수 없습니다. 지원되지 않는 플러그인을 쓰고 싶다면, 로컬에서 사이트를 생성한 뒤 사이트의 정적 파일을 GitHub에 push하세요.

## 구문 강조

사이트를 읽기 쉽게 하기 위해, GitHub Pages 사이트의 코드 조각은 GitHub에서와 같은 방식으로 구문 강조됩니다. 구문 강조에 대한 자세한 내용은 [코드 블록 만들기와 강조하기](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks)를 참고하세요.

기본적으로 사이트의 코드 블록은 Jekyll이 강조합니다. Jekyll은 [Pygments](https://pygments.org/)와 호환되는 [Rouge](https://github.com/rouge-ruby/rouge) 강조 도구를 사용합니다. `_config.yml`{: .filepath} 파일에 Pygments를 지정하면 대신 Rouge가 사용됩니다. Jekyll은 다른 구문 강조 도구를 사용할 수 없으며, `_config.yml`{: .filepath} 파일에 다른 도구를 지정하면 페이지 빌드 경고가 나타납니다. 자세한 내용은 [GitHub Pages 사이트의 Jekyll 빌드 오류 알아보기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-jekyll-build-errors-for-github-pages-sites)를 참고하세요.

> Rouge는 펜스 코드 블록의 언어 식별자를 소문자로만 인식합니다. 지원되는 언어 목록은 [Languages](https://rouge-ruby.github.io/docs/file.Languages.html)를 참고하세요.
{: .prompt-info }

[highlight.js](https://github.com/highlightjs/highlight.js) 같은 다른 강조 도구를 쓰고 싶다면, 프로젝트의 `_config.yml`{: .filepath} 파일을 수정해 Jekyll의 구문 강조를 꺼야 합니다.

```yaml
kramdown:
  syntax_highlighter_opts:
    disable : true
```

테마에 구문 강조용 CSS가 없다면, GitHub의 구문 강조 CSS를 생성해 프로젝트의 `style.css` 파일에 추가할 수 있습니다.

```shell
rougify style github > style.css
```

## 로컬에서 사이트 빌드하기

브랜치에서 게시한다면, 변경 사항이 사이트의 게시 원본에 병합될 때 자동으로 게시됩니다. 사용자 지정 GitHub Actions 워크플로로 게시한다면, 워크플로가 실행될 때마다(보통 기본 브랜치에 push할 때) 변경 사항이 게시됩니다. 변경 사항을 먼저 미리 보고 싶다면 GitHub가 아니라 로컬에서 변경한 뒤 사이트를 로컬에서 테스트하세요. 자세한 내용은 [Jekyll로 로컬에서 GitHub Pages 사이트 테스트하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)를 참고하세요.

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
