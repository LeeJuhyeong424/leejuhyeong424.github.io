---
title: GitHub Pages 사이트 만들기
description: 새 저장소나 기존 저장소에서 GitHub Pages 사이트를 만들 수 있습니다.
date: 2026-10-10 14:20:00 +0900
categories: [GitHub Pages, 시작하기]
tags: [github-pages, github]
---

## 사이트용 저장소 만들기

저장소를 새로 만들어도 되고, 기존 저장소를 골라 사이트로 써도 됩니다.

저장소 안의 모든 파일이 사이트와 관련된 것은 아닌 저장소에 GitHub Pages 사이트를 만들고 싶다면, 사이트의 게시 원본을 따로 구성할 수 있습니다. 예를 들어 사이트 소스 파일만 담는 전용 브랜치와 폴더를 두거나, 사용자 지정 GitHub Actions 워크플로로 사이트 소스 파일을 빌드하고 배포할 수 있습니다.

저장소를 소유한 계정이 GitHub Free(개인) 또는 GitHub Free(조직)를 사용한다면, 저장소는 공개(public)여야 합니다.

기존 저장소에 사이트를 만들려면 아래 [사이트 만들기](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site#creating-your-site) 단계로 넘어가세요.

1. 아무 페이지에서나 오른쪽 위의 <kbd>+</kbd>를 선택한 다음 **New repository**를 클릭합니다.

   ![새 항목 만들기 메뉴. "New repository" 항목이 강조되어 있음](/assets/img/posts/github-pages/repo-create-global-nav-update.png){: .shadow w='366' h='258' }

2. **Owner** 드롭다운 메뉴에서 저장소를 소유할 계정을 선택합니다.

   ![새 저장소의 소유자 메뉴. octocat과 github 두 가지 선택지가 보임](/assets/img/posts/github-pages/create-repository-owner.png){: .shadow w='764' h='152' }

3. 저장소 이름과 설명(선택)을 입력합니다. 사용자 또는 조직 사이트를 만든다면 저장소 이름은 반드시 `<user>.github.io` 또는 `<organization>.github.io`여야 합니다. 사용자명이나 조직명에 대문자가 있다면 소문자로 바꿔서 입력해야 합니다. 자세한 내용은 [GitHub Pages 사이트의 종류](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages#types-of-github-pages-sites)를 참고하세요.

   ![저장소 이름 입력란에 "octocat.github.io"가 입력된 화면](/assets/img/posts/github-pages/create-repository-name-pages.png){: .shadow w='1106' h='277' }

4. 저장소 공개 범위를 선택합니다. 자세한 내용은 [저장소 정보](https://docs.github.com/en/repositories/creating-and-managing-repositories/about-repositories#about-repository-visibility)를 참고하세요.
5. **Add README**를 **On**으로 켭니다.
6. **Create repository**를 클릭합니다.

## 사이트 만들기

사이트를 만들려면 먼저 GitHub에 사이트용 저장소가 있어야 합니다. 기존 저장소에 사이트를 만드는 게 아니라면 위의 "사이트용 저장소 만들기"를 먼저 진행하세요.

> 저장소가 비공개(private)이더라도 GitHub Pages 사이트는 인터넷에 공개됩니다(요금제나 조직 설정이 허용하는 경우). 사이트 저장소에 민감한 데이터가 있다면 게시 전에 제거하는 것이 좋습니다. 자세한 내용은 [저장소 공개 범위](https://docs.github.com/en/repositories/creating-and-managing-repositories/about-repositories#about-repository-visibility)를 참고하세요.
{: .prompt-warning }

1. GitHub에서 사이트 저장소로 이동합니다.
2. 사용할 게시 원본을 정합니다. [GitHub Pages 사이트의 게시 원본 구성하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)를 참고하세요.
3. 사이트의 진입 파일을 만듭니다. GitHub Pages는 사이트의 진입 파일로 `index.html`, `index.md`, `README.md` 중 하나를 찾습니다.

   게시 원본이 브랜치와 폴더라면, 진입 파일은 원본 브랜치에 있는 원본 폴더의 최상위에 있어야 합니다. 예를 들어 게시 원본이 `main` 브랜치의 `/docs` 폴더라면, 진입 파일은 `main` 브랜치의 `/docs` 폴더 안에 있어야 합니다.

   게시 원본이 GitHub Actions 워크플로라면, 배포하는 아티팩트의 최상위에 진입 파일이 있어야 합니다. 진입 파일을 저장소에 직접 추가하는 대신, 워크플로가 실행될 때 진입 파일을 생성하도록 할 수도 있습니다.

4. 게시 원본을 구성합니다. [GitHub Pages 사이트의 게시 원본 구성하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)를 참고하세요.
5. GitHub Pages 사이트는 GitHub Actions 워크플로로 빌드되고 배포됩니다. 자세한 내용은 [워크플로 실행 기록 보기](https://docs.github.com/en/actions/how-tos/monitor-workflows/view-workflow-run-history)를 참고하세요.

   > GitHub Actions는 공개 저장소에서 무료입니다. 비공개·내부 저장소는 매월 제공되는 무료 사용 시간을 넘기면 요금이 부과됩니다. 자세한 내용은 [GitHub Actions 요금과 사용량](https://docs.github.com/en/actions/concepts/billing-and-usage)을 참고하세요.
   {: .prompt-info }

## 게시된 사이트 확인하기

1. 저장소 이름 아래에서 **Settings**를 클릭합니다. "Settings" 탭이 보이지 않으면 <kbd>···</kbd> 드롭다운 메뉴를 선택한 다음 **Settings**를 클릭합니다.

   ![저장소 상단 탭. "Settings" 탭이 강조되어 있음](/assets/img/posts/github-pages/repo-actions-settings.png){: .shadow w='1098' h='108' }

2. 사이드바의 "Code, planning, and automation" 섹션에서 **Pages**를 클릭합니다.
3. 게시된 사이트를 보려면 "GitHub Pages" 아래의 **Visit site**를 클릭합니다.

> 변경 사항을 GitHub에 push한 뒤 사이트에 반영되기까지 최대 10분이 걸릴 수 있습니다. 1시간이 지나도 브라우저에 변경 사항이 보이지 않는다면 [GitHub Pages 사이트의 Jekyll 빌드 오류 알아보기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-jekyll-build-errors-for-github-pages-sites)를 참고하세요.
{: .prompt-info }

> - 브랜치에서 게시하는데 사이트가 자동으로 게시되지 않았다면, 관리자 권한과 인증된 이메일 주소를 가진 사람이 게시 원본에 push했는지 확인하세요.
> - `GITHUB_TOKEN`을 사용하는 GitHub Actions 워크플로가 push한 커밋은 GitHub Pages 빌드를 실행하지 않습니다.
{: .prompt-info }

## 정적 사이트 생성기

GitHub Pages는 저장소에 push한 정적 파일이라면 무엇이든 게시합니다. 정적 파일을 직접 만들어도 되고, 정적 사이트 생성기로 사이트를 빌드해도 됩니다. 로컬이나 다른 서버에서 빌드 과정을 직접 구성할 수도 있습니다.

직접 구성한 빌드 과정이나 Jekyll이 아닌 정적 사이트 생성기를 사용한다면, GitHub Actions 워크플로를 작성해 사이트를 빌드하고 게시할 수 있습니다. GitHub는 여러 정적 사이트 생성기용 워크플로 템플릿을 제공합니다. 자세한 내용은 [GitHub Pages 사이트의 게시 원본 구성하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)를 참고하세요.

원본 브랜치에서 사이트를 게시하면 GitHub Pages는 기본적으로 Jekyll로 사이트를 빌드합니다. Jekyll이 아닌 정적 사이트 생성기를 쓰고 싶다면, 그 대신 GitHub Actions 워크플로를 작성해 사이트를 빌드하고 게시하는 것을 권장합니다. 그렇지 않다면 게시 원본의 루트에 `.nojekyll`이라는 빈 파일을 만들어 Jekyll 빌드 과정을 끄고, 사용하는 정적 사이트 생성기의 안내에 따라 로컬에서 사이트를 빌드하세요.

> GitHub Pages는 PHP, Ruby, Python 같은 서버 측 언어를 지원하지 않습니다.
{: .prompt-info }

## GitHub Pages의 MIME 타입

MIME 타입은 서버가 브라우저에 보내는 헤더로, 브라우저가 요청한 파일의 성격과 형식을 알려 줍니다. GitHub Pages는 수천 개의 파일 확장자에 걸쳐 750개가 넘는 MIME 타입을 지원합니다. 지원하는 MIME 타입 목록은 [mime-db 프로젝트](https://github.com/jshttp/mime-db)에서 만들어집니다.

파일이나 저장소 단위로 사용자 지정 MIME 타입을 지정할 수는 없지만, GitHub Pages에서 쓰일 MIME 타입을 추가하거나 수정할 수는 있습니다. 자세한 내용은 [mime-db 기여 가이드](https://github.com/jshttp/mime-db#adding-custom-media-types)를 참고하세요.

## 다음 단계

새 파일을 더 만들어 사이트에 페이지를 추가할 수 있습니다. 각 파일은 게시 원본과 같은 디렉터리 구조로 사이트에 게시됩니다. 예를 들어 프로젝트 사이트의 게시 원본이 `gh-pages` 브랜치이고, `gh-pages` 브랜치에 `/about/contact-us.md`라는 새 파일을 만들었다면, 그 파일은 `https://<user>.github.io/<repository>/about/contact-us.html`에서 볼 수 있습니다.

테마를 추가해 사이트의 모양과 분위기를 바꿀 수도 있습니다. 자세한 내용은 [Jekyll로 GitHub Pages 사이트에 테마 추가하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll)를 참고하세요.

## 더 읽어보기

- [GitHub Pages와 Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll)
- [GitHub Pages 사이트의 Jekyll 빌드 오류 문제 해결](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/troubleshooting-jekyll-build-errors-for-github-pages-sites)
- [저장소 안에서 브랜치 관리하기](https://docs.github.com/en/pull-requests/how-tos/commit-changes/managing-branches-within-your-repository)
- [새 파일 만들기](https://docs.github.com/en/repositories/working-with-files/managing-files/creating-new-files)
- [GitHub Pages 사이트의 404 오류 문제 해결](https://docs.github.com/en/pages/getting-started-with-github-pages/troubleshooting-404-errors-for-github-pages-sites)

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
