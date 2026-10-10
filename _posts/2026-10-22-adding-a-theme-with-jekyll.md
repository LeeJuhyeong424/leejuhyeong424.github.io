---
title: Jekyll로 사이트에 테마 추가하기
description: 테마를 추가하고 꾸며서 Jekyll 사이트를 내 스타일로 바꿀 수 있습니다.
date: 2026-10-22 00:00:00 +0900
categories: [GitHub Pages, Jekyll]
tags: [github-pages, jekyll, theme]
render_with_liquid: false
---

> `github-pages` gem은 일부 워크플로에서 여전히 지원되지만, 이제는 GitHub Actions로 GitHub Pages 사이트를 배포하고 자동화하는 방식이 권장됩니다.
{: .prompt-info }

> 저장소 쓰기 권한이 있는 사람이 Jekyll을 사용해 GitHub Pages 사이트에 테마를 추가할 수 있습니다.
{: .prompt-info }

브랜치에서 게시한다면, 변경 사항이 사이트의 게시 원본에 병합될 때 자동으로 게시됩니다. 사용자 지정 GitHub Actions 워크플로로 게시한다면, 워크플로가 실행될 때마다(보통 기본 브랜치에 push할 때) 변경 사항이 게시됩니다. 변경 사항을 먼저 미리 보고 싶다면 GitHub가 아니라 로컬에서 변경한 뒤 사이트를 로컬에서 테스트하세요. 자세한 내용은 [Jekyll로 로컬에서 GitHub Pages 사이트 테스트하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)를 참고하세요.

## 지원되는 테마

기본으로 지원되는 테마는 다음과 같습니다.

- [Architect](https://github.com/pages-themes/architect)
- [Cayman](https://github.com/pages-themes/cayman)
- [Dinky](https://github.com/pages-themes/dinky)
- [Hacker](https://github.com/pages-themes/hacker)
- [Leap day](https://github.com/pages-themes/leap-day)
- [Merlot](https://github.com/pages-themes/merlot)
- [Midnight](https://github.com/pages-themes/midnight)
- [Minima](https://github.com/jekyll/minima)
- [Minimal](https://github.com/pages-themes/minimal)
- [Modernist](https://github.com/pages-themes/modernist)
- [Slate](https://github.com/pages-themes/slate)
- [Tactile](https://github.com/pages-themes/tactile)
- [Time machine](https://github.com/pages-themes/time-machine)

[`jekyll-remote-theme`](https://github.com/benbalter/jekyll-remote-theme) Jekyll 플러그인도 사용할 수 있으며, 이 플러그인으로 다른 테마를 불러올 수 있습니다.

## 테마 추가하기

1. GitHub에서 사이트 저장소로 이동합니다.
2. 사이트의 게시 원본으로 이동합니다. 자세한 내용은 [GitHub Pages 사이트의 게시 원본 구성하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)를 참고하세요.
3. `_config.yml`{: .filepath}로 이동합니다.
4. 파일 화면 오른쪽 위의 연필 아이콘을 클릭해 파일 편집기를 엽니다.

   ![파일 화면 상단. 연필 아이콘 버튼이 강조되어 있음](/assets/img/posts/edit-file-edit-button.png){: .shadow w='703' h='224' }

   > 기본 파일 편집기 대신, 아래쪽 화살표 드롭다운 메뉴에서 **github.dev**를 클릭해 [github.dev 코드 편집기](https://docs.github.com/en/codespaces/the-githubdev-web-based-editor)를 사용할 수도 있습니다. **GitHub Desktop**을 클릭해 저장소를 클론하고 GitHub Desktop에서 로컬로 파일을 수정할 수도 있습니다.
   {: .prompt-info }

   ![파일 화면 상단. 아래쪽 화살표 아이콘이 강조되어 있음](/assets/img/posts/edit-file-edit-dropdown.png){: .shadow w='703' h='117' }

5. 파일에 테마 이름을 적을 새 줄을 추가합니다.
   - 지원되는 테마를 쓰려면 `theme: THEME-NAME`을 입력합니다. THEME-NAME은 테마 저장소의 `_config.yml`{: .filepath}에 나와 있는 테마 이름으로 바꿉니다(대부분의 테마는 `jekyll-theme-NAME` 형식을 따릅니다). 지원되는 테마 목록은 위의 "지원되는 테마"를 참고하세요. 예를 들어 Minimal 테마를 고르려면 `theme: jekyll-theme-minimal`을 입력합니다.
   - GitHub에 공개된 다른 Jekyll 테마를 쓰려면 `remote_theme: THEME-NAME`을 입력합니다. THEME-NAME은 테마 저장소의 README에 나와 있는 테마 이름으로 바꿉니다.
6. **Commit changes...**를 클릭합니다.
7. "Commit message" 칸에 파일에 어떤 변경을 했는지 설명하는 짧고 의미 있는 커밋 메시지를 입력합니다. 커밋 메시지에서 여러 작성자를 커밋에 표시할 수도 있습니다.
8. GitHub 계정에 이메일 주소가 여러 개 연결되어 있다면, 이메일 주소 드롭다운 메뉴를 클릭해 Git 작성자 이메일로 쓸 주소를 선택합니다.

   ![커밋 작성자 이메일을 고르는 드롭다운 메뉴. octocat@github.com이 선택되어 있음](/assets/img/posts/choose-commit-email-address.png){: .shadow w='643' h='234' }

9. 커밋 메시지 입력란 아래에서 커밋을 현재 브랜치에 추가할지, 새 브랜치에 추가할지 정합니다. 현재 브랜치가 기본 브랜치라면 커밋용 새 브랜치를 만든 뒤 풀 리퀘스트를 만드는 것이 좋습니다.

   ![main 브랜치에 바로 커밋할지 새 브랜치를 만들지 고르는 라디오 버튼. 새 브랜치가 선택되어 있음](/assets/img/posts/choose-commit-branch.png){: .shadow w='669' h='166' }

10. **Commit changes** 또는 **Propose changes**를 클릭합니다.

## 테마의 CSS 꾸미기

이 방법은 GitHub Pages가 공식 지원하는 테마에서 가장 잘 동작합니다. 지원되는 테마 전체 목록은 위의 "지원되는 테마"를 참고하세요.

테마의 소스 저장소에서 테마를 꾸미는 방법을 안내하기도 합니다. 예를 들어 [Minimal의 README](https://github.com/pages-themes/minimal#customizing)를 참고하세요.

1. GitHub에서 사이트 저장소로 이동합니다.
2. 사이트의 게시 원본으로 이동합니다. 자세한 내용은 [GitHub Pages 사이트의 게시 원본 구성하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)를 참고하세요.
3. `/assets/css/style.scss`라는 새 파일을 만듭니다.
4. 파일 맨 위에 다음 내용을 추가합니다.

   ```scss
   ---
   ---

   @import "{{ site.theme }}";
   ```

5. `@import` 줄 바로 아래에 원하는 CSS나 Sass(import 포함)를 추가합니다.

## 테마의 HTML 레이아웃 꾸미기

이 방법은 GitHub Pages가 공식 지원하는 테마에서 가장 잘 동작합니다. 지원되는 테마 전체 목록은 위의 "지원되는 테마"를 참고하세요.

테마의 소스 저장소에서 테마를 꾸미는 방법을 안내하기도 합니다. 예를 들어 [Minimal의 README](https://github.com/pages-themes/minimal#customizing)를 참고하세요.

1. GitHub에서 테마의 소스 저장소로 이동합니다. 예를 들어 Minimal의 소스 저장소는 `https://github.com/pages-themes/minimal`입니다.
2. `_layouts` 폴더에서 테마의 `_default.html` 파일로 이동합니다.
3. 파일 내용을 복사합니다.
4. GitHub에서 사이트 저장소로 이동합니다.
5. 사이트의 게시 원본으로 이동합니다.
6. `_layouts/default.html`이라는 파일을 만듭니다.
7. 앞에서 복사한 기본 레이아웃 내용을 붙여 넣습니다.
8. 원하는 대로 레이아웃을 꾸밉니다.

## 더 읽어보기

- [새 파일 만들기](https://docs.github.com/en/repositories/working-with-files/managing-files/creating-new-files)

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
