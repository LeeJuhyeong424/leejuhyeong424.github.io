---
title: Jekyll 빌드 오류 문제 해결
description: Jekyll 빌드 오류 메시지를 보고 GitHub Pages 사이트의 문제를 해결하는 방법을 알아봅니다.
date: 2026-10-24 00:00:00 +0900
categories: [GitHub Pages, Jekyll]
tags: [github-pages, jekyll, troubleshooting]
render_with_liquid: false
---

## 빌드 오류 해결하기

Jekyll이 로컬이나 GitHub에서 GitHub Pages 사이트를 빌드하다가 오류를 만나면, 오류 메시지를 보고 문제를 해결할 수 있습니다. 오류 메시지와 확인 방법은 [Jekyll 빌드 오류 알아보기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-jekyll-build-errors-for-github-pages-sites)를 참고하세요.

일반적인 오류 메시지를 받았다면 흔한 원인부터 확인하세요.

- 지원되지 않는 플러그인을 사용하고 있습니다. 자세한 내용은 [GitHub Pages와 Jekyll: 플러그인](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll#plugins)을 참고하세요.
- 저장소가 저장소 크기 한도를 넘었습니다. 자세한 내용은 [GitHub의 대용량 파일 정보](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github)를 참고하세요.
- `_config.yml`{: .filepath} 파일의 `source` 설정을 바꿨습니다. 브랜치에서 사이트를 게시한다면 GitHub Pages가 빌드 과정에서 이 설정을 덮어씁니다.
- 게시하는 파일 이름에 지원되지 않는 콜론(`:`)이 들어 있습니다.

특정 오류 메시지를 받았다면 아래에서 해당 오류의 해결 방법을 확인하세요.

오류를 고친 뒤에는 사이트의 원본 브랜치에 변경 사항을 push하거나(브랜치에서 게시하는 경우), 사용자 지정 GitHub Actions 워크플로를 실행해(GitHub Actions로 게시하는 경우) 다시 빌드하세요.

## Config file error

`_config.yml`{: .filepath} 파일에 문법 오류가 있어 사이트 빌드에 실패했다는 뜻입니다.

`_config.yml`{: .filepath} 파일이 다음 규칙을 지키는지 확인하세요.

- 탭 대신 스페이스를 사용합니다.
- 각 키-값 쌍에서 `:` 뒤에 공백을 넣습니다. 예: `timezone: Africa/Nairobi`
- UTF-8 문자만 사용합니다.
- `:` 같은 특수 문자는 따옴표로 감쌉니다. 예: `title: "my awesome site: an adventure in parse errors"`
- 여러 줄 값은 줄바꿈을 유지하려면 `|`, 줄바꿈을 무시하려면 `>`를 사용합니다.

오류를 찾으려면 YAML 파일 내용을 [YAML Validator](https://codebeautify.org/yaml-validator) 같은 YAML 검사기에 붙여 넣어 보세요.

> 저장소에 심볼릭 링크가 있다면 GitHub Actions 워크플로로 사이트를 게시해야 합니다. GitHub Actions에 대한 자세한 내용은 [GitHub Actions 문서](https://docs.github.com/en/actions)를 참고하세요.
{: .prompt-info }

## Date is not a valid datetime

사이트의 어느 페이지에 올바르지 않은 날짜·시간 값이 들어 있다는 뜻입니다.

오류 메시지에 나온 파일과 그 파일의 레이아웃에서 날짜 관련 Liquid 필터를 호출하는 곳을 찾아보세요. 날짜 관련 Liquid 필터에 넘기는 변수가 모든 경우에 값을 갖고 있는지, `nil`이나 `""`를 넘기지 않는지 확인하세요. 자세한 내용은 Liquid 문서의 [Filters](https://shopify.dev/docs/api/liquid/filters)를 참고하세요.

## File does not exist in includes directory

코드가 `_includes` 디렉터리에 없는 파일을 참조한다는 뜻입니다.

오류 메시지에 나온 파일에서 `include`를 검색해 `{% include example_header.html %}`처럼 다른 파일을 참조하는 곳을 찾아보세요. 참조한 파일 중 `_includes` 디렉터리에 없는 것이 있다면 그 파일을 `_includes` 디렉터리로 복사하거나 옮기세요.

## File is not properly UTF-8 encoded

`日本語` 같은 비라틴 문자를 사용하면서 컴퓨터에 이런 문자가 나온다는 것을 알려 주지 않았다는 뜻입니다.

`_config.yml`{: .filepath} 파일에 다음 줄을 추가해 UTF-8 인코딩을 강제하세요.

```yaml
encoding: UTF-8
```

## Invalid highlighter language

설정 파일에 [Rouge](https://github.com/jneen/rouge)나 [Pygments](https://pygments.org/)가 아닌 구문 강조 도구를 지정했다는 뜻입니다.

`_config.yml`{: .filepath} 파일에서 [Rouge](https://github.com/jneen/rouge)나 [Pygments](https://pygments.org/)를 지정하도록 수정하세요. 자세한 내용은 [GitHub Pages와 Jekyll: 구문 강조](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll#syntax-highlighting)를 참고하세요.

## Invalid post date

사이트의 글 파일 이름이나 YAML front matter에 올바르지 않은 날짜가 들어 있다는 뜻입니다.

모든 날짜가 UTC 기준 YYYY-MM-DD HH:MM:SS 형식이고 실제로 존재하는 날짜인지 확인하세요. UTC와의 시차로 시간대를 지정하려면 `2014-04-18 11:30:00 +0800`처럼 YYYY-MM-DD HH:MM:SS +/-TTTT 형식을 사용합니다.

`_config.yml`{: .filepath} 파일에 날짜 형식을 지정했다면 형식이 올바른지 확인하세요.

## Invalid Sass or SCSS

저장소에 내용이 올바르지 않은 Sass 또는 SCSS 파일이 있다는 뜻입니다.

오류 메시지에 나온 줄 번호에서 잘못된 Sass나 SCSS를 확인하세요. 앞으로의 오류를 막으려면 자주 쓰는 텍스트 편집기에 Sass나 SCSS 검사기(linter)를 설치하세요.

## Invalid submodule

저장소에 제대로 초기화되지 않은 하위 모듈이 있다는 뜻입니다.

먼저 하위 모듈(Git 프로젝트 안의 Git 프로젝트)을 정말 사용하려는 것인지 판단하세요. 하위 모듈은 실수로 만들어지기도 합니다.

하위 모듈을 쓰지 않으려면 하위 모듈을 제거합니다. PATH-TO-SUBMODULE은 하위 모듈의 경로로 바꿉니다.

```shell
git submodule deinit PATH-TO-SUBMODULE
git rm PATH-TO-SUBMODULE
git commit -m "Remove submodule"
rm -rf .git/modules/PATH-TO-SUBMODULE
```

하위 모듈을 쓰려면, 하위 모듈을 참조할 때 `http://`가 아니라 `https://`를 사용하고, 하위 모듈이 공개 저장소에 있는지 확인하세요.

## Invalid YAML in data file

`_data` 폴더의 파일 중 하나 이상에 올바르지 않은 YAML이 들어 있다는 뜻입니다.

`_data` 폴더의 YAML 파일이 다음 규칙을 지키는지 확인하세요.

- 탭 대신 스페이스를 사용합니다.
- 각 키-값 쌍에서 `:` 뒤에 공백을 넣습니다. 예: `timezone: Africa/Nairobi`
- UTF-8 문자만 사용합니다.
- `:` 같은 특수 문자는 따옴표로 감쌉니다. 예: `title: "my awesome site: an adventure in parse errors"`
- 여러 줄 값은 줄바꿈을 유지하려면 `|`, 줄바꿈을 무시하려면 `>`를 사용합니다.

오류를 찾으려면 YAML 파일 내용을 [YAML Validator](https://codebeautify.org/yaml-validator) 같은 YAML 검사기에 붙여 넣어 보세요.

Jekyll 데이터 파일에 대한 자세한 내용은 Jekyll 문서의 [Data Files](https://jekyllrb.com/docs/datafiles/)를 참고하세요.

## Markdown errors

저장소에 Markdown 오류가 있다는 뜻입니다.

먼저 지원되는 Markdown 프로세서를 사용하고 있는지 확인하세요. 자세한 내용은 [Markdown 프로세서 설정하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/setting-a-markdown-processor-for-your-github-pages-site-using-jekyll)를 참고하세요.

그다음 오류 메시지에 나온 파일이 올바른 Markdown 문법을 사용하는지 확인하세요. 자세한 내용은 Daring Fireball의 [Markdown: Syntax](https://daringfireball.net/projects/markdown/syntax)를 참고하세요.

## Missing docs folder

어떤 브랜치의 `docs` 폴더를 게시 원본으로 골랐지만, 그 브랜치의 저장소 루트에 `docs` 폴더가 없다는 뜻입니다.

`docs` 폴더를 실수로 옮겼다면, 게시 원본으로 고른 브랜치의 저장소 루트로 `docs` 폴더를 다시 옮겨 보세요. `docs` 폴더를 실수로 삭제했다면 다음 중 하나를 하면 됩니다.

- Git으로 삭제를 되돌립니다. 자세한 내용은 Git 문서의 [git-revert](https://git-scm.com/docs/git-revert.html)를 참고하세요.
- 게시 원본으로 고른 브랜치의 저장소 루트에 `docs` 폴더를 새로 만들고, 사이트 소스 파일을 그 폴더에 추가합니다. 자세한 내용은 [새 파일 만들기](https://docs.github.com/en/repositories/working-with-files/managing-files/creating-new-files)를 참고하세요.
- 게시 원본을 바꿉니다. 자세한 내용은 [GitHub Pages 사이트의 게시 원본 구성하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)를 참고하세요.

## Missing submodule

저장소에 존재하지 않거나 제대로 초기화되지 않은 하위 모듈이 있다는 뜻입니다.

먼저 하위 모듈(Git 프로젝트 안의 Git 프로젝트)을 정말 사용하려는 것인지 판단하세요. 하위 모듈은 실수로 만들어지기도 합니다.

하위 모듈을 쓰지 않으려면 하위 모듈을 제거합니다. PATH-TO-SUBMODULE은 하위 모듈의 경로로 바꿉니다.

```shell
git submodule deinit PATH-TO-SUBMODULE
git rm PATH-TO-SUBMODULE
git commit -m "Remove submodule"
rm -rf .git/modules/PATH-TO-SUBMODULE
```

하위 모듈을 쓰려면 하위 모듈을 초기화하세요. 자세한 내용은 _Pro Git_ 책의 [Git 도구 - 서브모듈](https://git-scm.com/book/en/v2/Git-Tools-Submodules)을 참고하세요.

## Relative permalinks configured

`_config.yml`{: .filepath} 파일에 GitHub Pages가 지원하지 않는 상대 퍼머링크가 설정되어 있다는 뜻입니다.

퍼머링크는 사이트의 특정 페이지를 가리키는 영구 URL입니다. 절대 퍼머링크는 사이트 루트에서 시작하고, 상대 퍼머링크는 해당 페이지가 들어 있는 폴더에서 시작합니다. GitHub Pages와 Jekyll은 더 이상 상대 퍼머링크를 지원하지 않습니다. 퍼머링크에 대한 자세한 내용은 Jekyll 문서의 [Permalinks](https://jekyllrb.com/docs/permalinks/)를 참고하세요.

`_config.yml`{: .filepath} 파일에서 `relative_permalinks` 줄을 지우고, 사이트의 상대 퍼머링크를 모두 절대 퍼머링크로 바꾸세요. 자세한 내용은 [파일 수정하기](https://docs.github.com/en/repositories/working-with-files/managing-files/editing-files)를 참고하세요.

## Syntax error in 'for' loop

Liquid `for` 반복문 선언에 잘못된 문법이 있다는 뜻입니다.

오류 메시지에 나온 파일의 모든 `for` 반복문 문법이 올바른지 확인하세요. `for` 반복문의 올바른 문법은 Liquid 문서의 [Tags](https://shopify.dev/docs/api/liquid/tags/for)를 참고하세요.

## Tag not properly closed

제대로 닫히지 않은 로직 태그가 있다는 뜻입니다. 예를 들어 `{% capture example_variable %}`는 반드시 `{% endcapture %}`로 닫아야 합니다.

오류 메시지에 나온 파일의 모든 로직 태그가 제대로 닫혀 있는지 확인하세요. 자세한 내용은 Liquid 문서의 [Tags](https://shopify.dev/docs/api/liquid/tags)를 참고하세요.

## Tag not properly terminated

제대로 끝나지 않은 출력 태그가 있다는 뜻입니다. 예를 들어 `{{ page.title }}` 대신 `{{ page.title }`라고 쓴 경우입니다.

오류 메시지에 나온 파일의 모든 출력 태그가 `}}`로 끝나는지 확인하세요. 자세한 내용은 Liquid 문서의 [Objects](https://shopify.dev/docs/api/liquid/objects)를 참고하세요.

## Unknown tag error

코드에 인식할 수 없는 Liquid 태그가 있다는 뜻입니다.

오류 메시지에 나온 파일의 모든 Liquid 태그가 Jekyll의 기본 변수와 일치하는지, 태그 이름에 오타가 없는지 확인하세요. 기본 변수 목록은 Jekyll 문서의 [Variables](https://jekyllrb.com/docs/variables/)를 참고하세요.

지원되지 않는 플러그인은 인식할 수 없는 태그의 흔한 원인입니다. 사이트를 로컬에서 생성해 정적 파일을 GitHub에 push하는 방식으로 지원되지 않는 플러그인을 쓴다면, 그 플러그인이 Jekyll 기본 변수에 없는 태그를 만들어 내지 않는지 확인하세요. 지원되는 플러그인 목록은 [GitHub Pages와 Jekyll: 플러그인](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll#plugins)을 참고하세요.

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/troubleshooting-jekyll-build-errors-for-github-pages-sites)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
