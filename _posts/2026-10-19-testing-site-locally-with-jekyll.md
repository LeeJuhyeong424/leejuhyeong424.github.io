---
title: Jekyll로 로컬에서 사이트 테스트하기
description: GitHub Pages 사이트를 로컬에서 빌드해 사이트의 변경 사항을 미리 보고 테스트할 수 있습니다.
date: 2026-10-19 00:00:00 +0900
categories: [GitHub Pages, Jekyll]
tags: [github-pages, jekyll]
---

> 저장소 읽기 권한이 있는 사람이라면 누구나 GitHub Pages 사이트를 로컬에서 테스트할 수 있습니다.
{: .prompt-info }

## 사전 준비

Jekyll로 사이트를 테스트하려면 먼저 다음이 필요합니다.

- [Jekyll](https://jekyllrb.com/docs/installation/) 설치
- Jekyll 사이트 만들기. 자세한 내용은 [Jekyll로 GitHub Pages 사이트 만들기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)를 참고하세요.

Jekyll을 설치하고 실행할 때는 [Bundler](https://bundler.io/) 사용을 권장합니다. Bundler는 Ruby gem 의존성을 관리하고, Jekyll 빌드 오류를 줄이며, 환경 차이로 생기는 버그를 막아 줍니다. Bundler 설치 방법은 다음과 같습니다.

1. Ruby를 설치합니다. 자세한 내용은 Ruby 문서의 [Ruby 설치하기](https://www.ruby-lang.org/en/documentation/installation/)를 참고하세요.
2. Bundler를 설치합니다. 자세한 내용은 [Bundler](https://bundler.io/)를 참고하세요.

> **macOS**: Bundler로 Jekyll을 설치하다가 Ruby 오류가 나면 [RVM](https://rvm.io/)이나 [Homebrew](https://brew.sh/) 같은 패키지 관리자로 Ruby 설치를 관리해야 할 수 있습니다. 자세한 내용은 Jekyll 문서의 [Troubleshooting](https://jekyllrb.com/docs/troubleshooting/#jekyll--macos)을 참고하세요.
{: .prompt-tip }

## 로컬에서 사이트 빌드하기

1. 터미널을 엽니다. macOS와 Linux는 터미널, Windows는 Git Bash를 사용합니다.
2. 사이트의 게시 원본으로 이동합니다. 자세한 내용은 [GitHub Pages 사이트의 게시 원본 구성하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)를 참고하세요.
3. `bundle install`을 실행합니다.
4. Jekyll 사이트를 로컬에서 실행합니다.

   ```shell
   $ bundle exec jekyll serve
   > Configuration file: /Users/octocat/my-site/_config.yml
   >            Source: /Users/octocat/my-site
   >       Destination: /Users/octocat/my-site/_site
   > Incremental build: disabled. Enable with --incremental
   >      Generating...
   >                    done in 0.309 seconds.
   > Auto-regeneration: enabled for '/Users/octocat/my-site'
   > Configuration file: /Users/octocat/my-site/_config.yml
   >    Server address: http://127.0.0.1:4000/
   >  Server running... press ctrl-c to stop.
   ```

   > - Ruby 3.0 이상을 설치했다면(Homebrew로 기본 버전을 설치했다면 그럴 수 있습니다) 이 단계에서 오류가 날 수 있습니다. 이 버전의 Ruby에는 `webrick`이 더 이상 기본으로 들어 있지 않기 때문입니다. 오류를 고치려면 `bundle add webrick`을 실행한 뒤 `bundle exec jekyll serve`를 다시 실행해 보세요. Ruby 3.2 이상을 설치했다면 `github-pages` gem과의 호환성 문제로 gem이나 메서드가 없다는 다른 오류가 날 수 있습니다. 이때는 Ruby 3.1.x 이하를 설치해야 합니다.
   > - `_config.yml` 파일의 `baseurl` 항목에 GitHub 저장소 링크가 들어 있다면, 로컬에서 빌드할 때 다음 명령으로 그 값을 무시하고 `localhost:4000/`에서 사이트를 띄울 수 있습니다. `bundle exec jekyll serve --baseurl=""`
   {: .prompt-info }

5. 웹 브라우저에서 `http://localhost:4000`으로 이동해 사이트를 미리 봅니다.

## GitHub Pages gem 업데이트하기

> `github-pages` gem은 일부 워크플로에서 여전히 지원되지만, 이제는 GitHub Actions로 GitHub Pages 사이트를 배포하고 자동화하는 방식이 권장됩니다.
{: .prompt-info }

Jekyll은 자주 업데이트되는 활발한 오픈 소스 프로젝트입니다. 내 컴퓨터의 `github-pages` gem이 GitHub Pages 서버의 `github-pages` gem보다 오래되었다면, 로컬에서 빌드한 사이트와 GitHub에 게시된 사이트의 모습이 다를 수 있습니다. 이를 막으려면 컴퓨터의 `github-pages` gem을 주기적으로 업데이트하세요.

1. 터미널을 엽니다. macOS와 Linux는 터미널, Windows는 Git Bash를 사용합니다.
2. `github-pages` gem을 업데이트합니다.
   - Bundler를 설치했다면 `bundle update github-pages`를 실행합니다.
   - Bundler가 없다면 `gem update github-pages`를 실행합니다.

## 더 읽어보기

- Jekyll 문서의 [GitHub Pages](https://jekyllrb.com/docs/github-pages/)

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
