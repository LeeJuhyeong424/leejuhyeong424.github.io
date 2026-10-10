---
title: 게시 원본 구성하기
description: >-
  특정 브랜치에 변경 사항이 push될 때 GitHub Pages 사이트가 게시되도록 구성하거나,
  GitHub Actions 워크플로를 작성해 사이트를 게시할 수 있습니다.
date: 2026-10-10 14:50:00 +0900
categories: [GitHub Pages, 시작하기]
tags: [github-pages, github-actions]
---

> 저장소의 관리자(admin) 또는 유지 관리자(maintainer) 권한이 있는 사람이 GitHub Pages 사이트의 게시 원본을 구성할 수 있습니다.
{: .prompt-info }

## 게시 원본이란

특정 브랜치에 변경 사항이 push될 때 사이트를 게시할 수도 있고, GitHub Actions 워크플로를 작성해 사이트를 게시할 수도 있습니다.

사이트의 빌드 과정을 직접 제어할 필요가 없다면, 특정 브랜치에 push될 때 게시하는 방식을 권장합니다. 게시 원본으로 사용할 브랜치와 폴더를 지정할 수 있습니다. 원본 브랜치는 저장소의 어떤 브랜치든 될 수 있고, 원본 폴더는 원본 브랜치의 저장소 루트(`/`) 또는 원본 브랜치의 `/docs` 폴더 중 하나입니다. 원본 브랜치에 변경 사항이 push될 때마다 원본 폴더의 변경 사항이 GitHub Pages 사이트에 게시됩니다.

Jekyll이 아닌 빌드 과정을 사용하고 싶거나, 컴파일된 정적 파일을 담을 전용 브랜치를 두고 싶지 않다면, GitHub Actions 워크플로를 작성해 사이트를 게시하는 방식을 권장합니다. GitHub는 흔한 게시 시나리오에 맞춘 워크플로 템플릿을 제공해 워크플로 작성을 도와줍니다.

> 저장소가 비공개(private)이더라도 GitHub Pages 사이트는 인터넷에 공개됩니다(요금제나 조직 설정이 허용하는 경우). 사이트 저장소에 민감한 데이터가 있다면 게시 전에 제거하는 것이 좋습니다. 자세한 내용은 [저장소 공개 범위](https://docs.github.com/en/repositories/creating-and-managing-repositories/about-repositories#about-repository-visibility)를 참고하세요.
{: .prompt-warning }

## 브랜치에서 게시하기

1. 게시 원본으로 사용할 브랜치가 저장소에 이미 있는지 확인합니다.
2. GitHub에서 사이트 저장소로 이동합니다.
3. 저장소 이름 아래에서 **Settings**를 클릭합니다. "Settings" 탭이 보이지 않으면 <kbd>···</kbd> 드롭다운 메뉴를 선택한 다음 **Settings**를 클릭합니다.

   ![저장소 상단 탭. "Settings" 탭이 강조되어 있음](/assets/img/posts/repo-actions-settings.png){: .shadow w='1098' h='108' }

4. 사이드바의 "Code, planning, and automation" 섹션에서 **Pages**를 클릭합니다.
5. "Build and deployment"의 "Source"에서 **Deploy from a branch**를 선택합니다.
6. "Build and deployment"에서 브랜치 드롭다운 메뉴를 사용해 게시 원본을 선택합니다.

   ![Pages 설정 화면. 게시 원본 브랜치를 고르는 "None" 메뉴가 강조되어 있음](/assets/img/posts/publishing-source-drop-down.png){: .shadow w='807' h='148' }

7. 필요하면 폴더 드롭다운 메뉴를 사용해 게시 원본 폴더를 선택합니다.

   ![Pages 설정 화면. 게시 원본 폴더를 고르는 "/(root)" 메뉴가 강조되어 있음](/assets/img/posts/publishing-source-folder-drop-down.png){: .shadow w='807' h='147' }

8. **Save**를 클릭합니다.

### 브랜치에서 게시할 때 문제 해결

> 저장소에 심볼릭 링크가 있다면 GitHub Actions 워크플로로 사이트를 게시해야 합니다. GitHub Actions에 대한 자세한 내용은 [GitHub Actions 문서](https://docs.github.com/en/actions)를 참고하세요.
{: .prompt-info }

> - 브랜치에서 게시하는데 사이트가 자동으로 게시되지 않았다면, 관리자 권한과 인증된 이메일 주소를 가진 사람이 게시 원본에 push했는지 확인하세요.
> - `GITHUB_TOKEN`을 사용하는 GitHub Actions 워크플로가 push한 커밋은 GitHub Pages 빌드를 실행하지 않습니다.
{: .prompt-info }

어떤 브랜치의 `docs` 폴더를 게시 원본으로 골랐다가 나중에 저장소의 해당 브랜치에서 `/docs` 폴더를 지우면, 사이트가 빌드되지 않고 `/docs` 폴더가 없다는 페이지 빌드 오류 메시지가 나타납니다. 자세한 내용은 [Jekyll 빌드 오류 문제 해결: docs 폴더 누락](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/troubleshooting-jekyll-build-errors-for-github-pages-sites#missing-docs-folder)을 참고하세요.

GitHub Pages 사이트를 다른 CI 도구로 빌드하도록 구성했더라도, 사이트는 항상 GitHub Actions 워크플로 실행으로 배포됩니다. 대부분의 외부 CI 워크플로는 빌드 결과물을 저장소의 `gh-pages` 브랜치에 커밋하는 방식으로 GitHub Pages에 "배포"하며, 보통 `.nojekyll` 파일을 함께 넣습니다. 이 경우 GitHub Actions 워크플로는 해당 브랜치에 빌드 단계가 필요 없다는 것을 감지하고, 사이트를 GitHub Pages 서버에 배포하는 데 필요한 단계만 실행합니다.

빌드나 배포에서 발생할 수 있는 오류를 찾으려면, 저장소의 워크플로 실행 기록에서 GitHub Pages 사이트의 워크플로 실행을 확인하면 됩니다. 자세한 내용은 [워크플로 실행 기록 보기](https://docs.github.com/en/actions/how-tos/monitor-workflows/view-workflow-run-history)를 참고하세요. 오류가 났을 때 워크플로를 다시 실행하는 방법은 [워크플로와 잡 다시 실행하기](https://docs.github.com/en/actions/how-tos/manage-workflow-runs/re-run-workflows-and-jobs)를 참고하세요.

## 사용자 지정 GitHub Actions 워크플로로 게시하기

GitHub Actions로 사이트를 게시하도록 구성하는 방법은 다음과 같습니다.

1. GitHub에서 사이트 저장소로 이동합니다.
2. 저장소 이름 아래에서 **Settings**를 클릭합니다. "Settings" 탭이 보이지 않으면 <kbd>···</kbd> 드롭다운 메뉴를 선택한 다음 **Settings**를 클릭합니다.
3. 사이드바의 "Code, planning, and automation" 섹션에서 **Pages**를 클릭합니다.
4. "Build and deployment"의 "Source"에서 **GitHub Actions**를 선택합니다.
5. GitHub가 여러 워크플로 템플릿을 추천합니다. 사이트를 게시하는 워크플로가 이미 있다면 이 단계는 건너뛰어도 됩니다. 그렇지 않다면 선택지 중 하나를 골라 GitHub Actions 워크플로를 만듭니다. 사용자 지정 워크플로를 만드는 방법은 아래 "사이트를 게시하는 사용자 지정 GitHub Actions 워크플로 만들기"를 참고하세요.

   GitHub Pages는 특정 워크플로를 GitHub Pages 설정에 연결하지 않습니다. 다만 GitHub Pages 설정 화면에는 가장 최근에 사이트를 배포한 워크플로 실행으로 가는 링크가 표시됩니다.

### 사이트를 게시하는 사용자 지정 GitHub Actions 워크플로 만들기

GitHub Actions에 대한 자세한 내용은 [GitHub Actions 문서](https://docs.github.com/en/actions)를 참고하세요.

GitHub Actions로 사이트를 게시하도록 구성하면, GitHub가 흔한 게시 시나리오에 맞는 워크플로 템플릿을 추천합니다. 워크플로의 일반적인 흐름은 다음과 같습니다.

1. 저장소의 기본 브랜치에 push가 있거나, Actions 탭에서 워크플로를 수동으로 실행할 때마다 시작합니다.
2. [`actions/checkout`](https://github.com/actions/checkout) 액션으로 저장소 내용을 체크아웃합니다.
3. 사이트에 필요하다면 정적 사이트 파일을 빌드합니다.
4. [`actions/upload-pages-artifact`](https://github.com/actions/upload-pages-artifact) 액션으로 정적 파일을 아티팩트로 업로드합니다.
5. 기본 브랜치에 대한 push로 워크플로가 시작되었다면 [`actions/deploy-pages`](https://github.com/actions/deploy-pages) 액션으로 아티팩트를 배포합니다. 풀 리퀘스트로 시작된 경우에는 이 단계를 건너뜁니다.

워크플로 템플릿은 `github-pages`라는 배포 환경을 사용합니다. 저장소에 `github-pages` 환경이 아직 없다면 자동으로 만들어집니다. 기본 브랜치만 이 환경에 배포할 수 있도록 배포 보호 규칙을 추가하는 것을 권장합니다. 자세한 내용은 [환경 관리하기](https://docs.github.com/en/actions/how-tos/deploy/configure-and-manage-deployments/manage-environments)를 참고하세요.

> 저장소에 있는 `CNAME` 파일은 사용자 지정 도메인을 자동으로 추가하거나 제거하지 않습니다. 사용자 지정 도메인은 저장소 설정이나 API를 통해 구성해야 합니다. 자세한 내용은 [서브도메인 구성하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-a-subdomain)와 [Pages REST API](https://docs.github.com/en/rest/pages#update-information-about-a-github-pages-site)를 참고하세요.
{: .prompt-info }

### 사용자 지정 GitHub Actions 워크플로로 게시할 때 문제 해결

GitHub Actions 워크플로의 문제를 해결하는 방법은 [워크플로 모니터링](https://docs.github.com/en/actions/how-tos/monitor-workflows)을 참고하세요.

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
