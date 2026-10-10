---
title: 404 오류 문제 해결
description: GitHub Pages 사이트에서 404 오류가 나타나는 흔한 원인과 해결 방법을 알아봅니다.
date: 2026-10-16 00:00:00 +0900
categories: [GitHub Pages, 시작하기]
tags: [github-pages, troubleshooting]
---

## 404 오류 문제 해결

이 가이드에서는 GitHub Pages 사이트를 빌드하는 동안 404 오류가 나타날 수 있는 흔한 원인을 다룹니다. 확인할 항목은 GitHub 상태 페이지, DNS 설정, 브라우저 캐시, `index.html` 파일, 디렉터리 내용, 사용자 지정 도메인, 저장소입니다.

### GitHub 상태 페이지

GitHub Pages 사이트를 빌드하다가 404 오류가 나타나면, 먼저 GitHub의 [상태 페이지](https://githubstatus.com)에서 진행 중인 장애가 있는지 확인하세요.

### DNS 설정

DNS 제공업체에서 GitHub의 DNS 레코드가 올바르게 설정되어 있는지 확인하세요. 자세한 내용은 [GitHub Pages 사이트의 사용자 지정 도메인 관리하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)를 참고하세요.

### 브라우저 캐시

GitHub Pages 사이트가 비공개인데 404 오류가 나타난다면 브라우저 캐시를 지워야 할 수 있습니다. 캐시를 지우는 방법은 사용하는 브라우저의 문서를 참고하세요.

### `index.html` 파일

GitHub Pages는 사이트의 진입 파일로 `index.html` 파일을 찾습니다.

- GitHub의 사이트 저장소에 `index.html` 파일이 있는지 확인하세요. 자세한 내용은 [GitHub Pages 사이트 만들기](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site#creating-your-site)를 참고하세요.
- 진입 파일은 선택한 게시 원본의 최상위에 있어야 합니다. 예를 들어 게시 원본이 `main` 브랜치의 `/docs` 디렉터리라면, 진입 파일은 `main` 브랜치의 `/docs` 디렉터리 안에 있어야 합니다.

  게시 원본이 브랜치와 디렉터리라면, 진입 파일은 원본 브랜치에 있는 원본 디렉터리의 최상위에 있어야 합니다.

  게시 원본이 GitHub Actions 워크플로라면, 배포하는 아티팩트의 최상위에 진입 파일이 있어야 합니다. 진입 파일을 저장소에 직접 추가하는 대신, 워크플로가 실행될 때 진입 파일을 생성하도록 할 수도 있습니다.

- `index.html` 파일 이름은 대소문자를 구분합니다. 예를 들어 `Index.html`은 동작하지 않습니다.
- 파일 이름은 `index.HTML` 같은 변형이 아닌 정확히 `index.html`이어야 합니다.

### 디렉터리 내용

디렉터리 내용이 루트 디렉터리에 있는지 확인하세요.

### 사용자 지정 도메인

사용자 지정 도메인을 사용한다면 올바르게 설정되어 있는지 확인하세요. 자세한 내용은 [사용자 지정 도메인과 GitHub Pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages)를 참고하세요.

- `CNAME` 레코드는 저장소 이름을 뺀 `<USER>.github.io` 또는 `<ORGANIZATION>.github.io`를 가리켜야 합니다. 올바른 레코드를 만드는 방법은 DNS 제공업체의 문서를 참고하세요.
- 첫 페이지에는 접속되는데 곳곳의 링크가 깨진다면, 이전에 사용자 지정 도메인이 없었거나 사용자 지정 도메인을 쓰다가 되돌린 경우일 가능성이 큽니다. 이때는 라우팅 경로가 바뀌어도 페이지가 다시 빌드되지 않습니다. 사용자 지정 도메인을 추가하거나 제거할 때 사이트가 자동으로 다시 빌드되도록 하는 것이 권장 해결책입니다. 커밋 작성자를 설정하고 사용자 지정 도메인 설정을 수정해야 할 수도 있습니다.

### 저장소

저장소가 다음 조건을 갖추었는지 확인하세요.

- 사이트를 게시하는 브랜치는 `main` 또는 기본 브랜치여야 합니다.
- 저장소 소유자처럼 저장소 관리자 권한이 있는 사람이 커밋을 push한 적이 있어야 합니다.
- 저장소 공개 범위를 공개에서 비공개로, 또는 그 반대로 바꾸면 GitHub Pages 사이트의 URL이 바뀌므로 사이트가 다시 빌드될 때까지 링크가 깨집니다.
- GitHub Pages 사이트에 비공개 저장소를 사용한다면 GitHub Pro, GitHub Team, GitHub Enterprise Cloud 구독이 아직 유효한지 확인하세요. 요금제를 갱신하면 GitHub Pages 사이트가 자동으로 다시 배포됩니다. 그렇지 않다면 저장소를 공개로 바꿔 GitHub Pages를 무료로 계속 사용할 수 있습니다.

그래도 404 오류가 계속된다면 Pages 카테고리에서 [GitHub Community 토론](https://github.com/orgs/community/discussions/categories/pages)을 시작하세요.

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/getting-started-with-github-pages/troubleshooting-404-errors-for-github-pages-sites)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
