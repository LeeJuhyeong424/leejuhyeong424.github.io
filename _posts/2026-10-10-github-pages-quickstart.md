---
title: GitHub Pages 빠른 시작
description: >-
  GitHub Pages로 오픈 소스 프로젝트를 소개하거나, 블로그를 호스팅하거나, 이력서를 공유할 수 있습니다.
  이 가이드는 첫 웹사이트를 만드는 과정을 안내합니다.
date: 2026-10-10 14:00:00 +0900
categories: [GitHub Pages, 빠른 시작]
tags: [github-pages, github]
---

## 소개

이 가이드에서는 `<username>.github.io` 주소의 사용자 사이트를 만듭니다.

## 웹사이트 만들기

1. 아무 페이지에서나 오른쪽 위의 <kbd>+</kbd>를 선택한 다음 **New repository**를 클릭합니다.

   ![새 항목 만들기 메뉴. "New repository" 항목이 강조되어 있음](/assets/img/posts/repo-create-global-nav-update.png){: .shadow w='366' h='258' }

2. 저장소 이름으로 `username.github.io`를 입력합니다. `username`은 본인의 GitHub 사용자명으로 바꿉니다. 예를 들어 사용자명이 `octocat`이라면 저장소 이름은 `octocat.github.io`가 됩니다.

   ![저장소 이름 입력란에 "octocat.github.io"가 입력된 화면](/assets/img/posts/create-repository-name-pages.png){: .shadow w='1106' h='277' }

3. 저장소 공개 범위를 선택합니다. 자세한 내용은 [저장소 정보](https://docs.github.com/en/repositories/creating-and-managing-repositories/about-repositories#about-repository-visibility)를 참고하세요.
4. **Add README**를 **On**으로 켭니다.
5. **Create repository**를 클릭합니다.
6. 저장소 이름 아래에서 **Settings**를 클릭합니다. "Settings" 탭이 보이지 않으면 <kbd>···</kbd> 드롭다운 메뉴를 선택한 다음 **Settings**를 클릭합니다.

   ![저장소 상단 탭. "Settings" 탭이 강조되어 있음](/assets/img/posts/repo-actions-settings.png){: .shadow w='1098' h='108' }

7. 사이드바의 "Code, planning, and automation" 섹션에서 **Pages**를 클릭합니다.
8. "Build and deployment"의 "Source"에서 **Deploy from a branch**를 선택합니다.
9. "Build and deployment"의 "Branch"에서 브랜치 드롭다운 메뉴를 사용해 게시 원본을 선택합니다.

   ![Pages 설정 화면. 게시 원본 브랜치를 고르는 "None" 메뉴가 강조되어 있음](/assets/img/posts/publishing-source-drop-down.png){: .shadow w='807' h='148' }

10. 원한다면 저장소의 `README.md` 파일을 엽니다. 사이트의 내용은 이 `README.md` 파일에 작성합니다. 지금 수정해도 되고, 기본 내용을 그대로 두어도 됩니다.
11. `username.github.io`에 접속해 새 웹사이트를 확인합니다. 변경 사항을 GitHub에 push한 뒤 사이트에 반영되기까지 최대 10분이 걸릴 수 있습니다.

## 제목과 설명 바꾸기

기본적으로 사이트 제목은 `username.github.io`입니다. 저장소의 `_config.yml`{: .filepath} 파일을 수정해 제목을 바꿀 수 있고, 사이트 설명도 추가할 수 있습니다.

1. 저장소의 **Code** 탭을 클릭합니다.
2. 파일 목록에 `_config.yml`{: .filepath}이 있는지 확인합니다. 없다면 `_config.yml`이라는 이름으로 새 파일을 만듭니다.
3. 파일 목록에서 `_config.yml`{: .filepath}을 클릭해 엽니다.
4. 연필 아이콘을 클릭해 파일을 수정합니다.
5. `_config.yml`{: .filepath}에는 이미 사이트 테마를 지정하는 줄이 있습니다. `title:` 뒤에 원하는 제목을 적은 줄과, `description:` 뒤에 원하는 설명을 적은 줄을 새로 추가합니다. 예를 들면 다음과 같습니다.

   ```yaml
   theme: jekyll-theme-minimal
   title: Octocat's homepage
   description: Bookmark this to keep an eye on my project updates!
   ```

6. 수정이 끝나면 **Commit changes**를 클릭합니다.

## 다음 단계

첫 GitHub Pages 웹사이트를 만들고, 꾸미고, 게시하는 데 성공했습니다. 하지만 살펴볼 것이 훨씬 더 많습니다. 다음 단계로 나아가는 데 도움이 되는 자료는 아래와 같습니다.

- [Jekyll로 GitHub Pages 사이트에 콘텐츠 추가하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-content-to-your-github-pages-site-using-jekyll#about-content-in-jekyll-sites): 사이트에 페이지를 더 추가하는 방법을 설명합니다.
- [GitHub Pages 사이트에 사용자 지정 도메인 구성하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site): 사이트를 GitHub의 `github.io` 도메인이나 내 도메인에서 호스팅할 수 있습니다.

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/quickstart)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
