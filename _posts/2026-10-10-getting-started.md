---
title: 시작하기
description: >-
  Chirpy의 기본 사항을 한눈에 살펴봅니다.
  Chirpy 기반 웹사이트를 설치, 설정, 사용하는 방법과 웹 서버에 배포하는 방법을 알아봅니다.
date: 2026-10-10 02:00:00 +0900
categories: [블로그, 튜토리얼]
tags: [getting started]
---

## 사이트 저장소 만들기

사이트 저장소를 만들 때는 필요에 따라 두 가지 방법 중 하나를 선택할 수 있습니다.

### 방법 1. 스타터 사용하기 (권장)

업그레이드가 간편하고 불필요한 파일이 분리되어 있어, 최소한의 설정으로 글쓰기에 집중하고 싶은 사용자에게 적합한 방법입니다.

1. GitHub에 로그인한 뒤 [**스타터**][starter] 저장소로 이동합니다.
2. <kbd>Use this template</kbd> 버튼을 클릭한 다음 <kbd>Create a new repository</kbd>를 선택합니다.
3. 새 저장소 이름을 `<username>.github.io`로 지정합니다. 이때 `username`은 소문자로 된 본인의 GitHub 사용자명으로 바꿉니다.

### 방법 2. 테마 포크하기

기능이나 UI 디자인을 수정하기에는 편리하지만, 업그레이드할 때 어려움이 따릅니다. 따라서 Jekyll에 익숙하고 테마를 대폭 수정할 계획이 아니라면 이 방법은 권하지 않습니다.

1. GitHub에 로그인합니다.
2. [테마 저장소를 포크합니다](https://github.com/cotes2020/jekyll-theme-chirpy/fork).
3. 새 저장소 이름을 `<username>.github.io`로 지정합니다. 이때 `username`은 소문자로 된 본인의 GitHub 사용자명으로 바꿉니다.

## 개발 환경 설정하기

저장소를 만들었다면 이제 개발 환경을 설정할 차례입니다. 크게 두 가지 방법이 있습니다.

### Dev Containers 사용하기 (Windows 권장)

Dev Containers는 Docker를 이용해 격리된 환경을 제공하므로 시스템과의 충돌을 막고, 모든 의존성을 컨테이너 안에서 관리할 수 있습니다.

**단계**:

1. Docker를 설치합니다.
   - Windows/macOS: [Docker Desktop][docker-desktop]을 설치합니다.
   - Linux: [Docker Engine][docker-engine]을 설치합니다.
2. [VS Code][vscode]와 [Dev Containers 확장][dev-containers]을 설치합니다.
3. 저장소를 클론합니다.
   - Docker Desktop: VS Code를 실행하고 [컨테이너 볼륨에 저장소를 클론][dc-clone-in-vol]합니다.
   - Docker Engine: 저장소를 로컬에 클론한 뒤, VS Code에서 [컨테이너로 엽니다][dc-open-in-container].
4. Dev Containers 설정이 완료될 때까지 기다립니다.

### 네이티브로 설정하기 (유닉스 계열 OS 권장)

유닉스 계열 시스템에서는 최적의 성능을 위해 네이티브로 환경을 설정할 수 있습니다. 물론 Dev Containers를 대안으로 사용해도 됩니다.

**단계**:

1. [Jekyll 설치 가이드](https://jekyllrb.com/docs/installation/)를 따라 Jekyll을 설치하고, [Git](https://git-scm.com/)이 설치되어 있는지 확인합니다.
2. 저장소를 로컬 컴퓨터에 클론합니다.
3. 테마를 포크했다면 [Node.js][nodejs]를 설치하고, 루트 디렉터리에서 `bash tools/init.sh`를 실행해 저장소를 초기화합니다.
4. 저장소 루트에서 `bundle install` 명령을 실행해 의존성을 설치합니다.

## 사용법

### Jekyll 서버 실행하기

사이트를 로컬에서 실행하려면 다음 명령을 사용합니다.

```terminal
$ bundle exec jekyll serve
```

> Dev Containers를 사용하는 경우, 반드시 **VS Code** 터미널에서 이 명령을 실행해야 합니다.
{: .prompt-info }

몇 초 뒤 <http://127.0.0.1:4000>에서 로컬 서버에 접속할 수 있습니다.

### 설정

필요에 따라 `_config.yml`{: .filepath}의 변수를 수정합니다. 대표적인 옵션은 다음과 같습니다.

- `url`
- `avatar`
- `timezone`
- `lang`

### 소셜 연락처 옵션

소셜 연락처는 사이드바 하단에 표시됩니다. `_data/contact.yml`{: .filepath} 파일에서 원하는 연락처를 켜거나 끌 수 있습니다.

### 스타일시트 커스터마이징

스타일시트를 커스터마이징하려면 테마의 `assets/css/jekyll-theme-chirpy.scss`{: .filepath} 파일을 내 Jekyll 사이트의 같은 경로에 복사한 뒤, 파일 끝에 원하는 스타일을 추가합니다.

### 정적 에셋 커스터마이징

정적 에셋 설정은 `5.1.0` 버전에서 도입되었습니다. 정적 에셋의 CDN은 `_data/origin/cors.yml`{: .filepath }에 정의되어 있으며, 웹사이트를 공개하는 지역의 네트워크 상황에 맞게 일부를 교체할 수 있습니다.

정적 에셋을 직접 호스팅하고 싶다면 [_chirpy-static-assets_](https://github.com/cotes2020/chirpy-static-assets#readme) 저장소를 참고하세요.

## 배포

배포하기 전에 `_config.yml`{: .filepath} 파일을 확인하고 `url`이 올바르게 설정되어 있는지 확인하세요. 커스텀 도메인 없이 [**프로젝트 사이트**](https://help.github.com/en/github/working-with-github-pages/about-github-pages#types-of-github-pages-sites)를 사용하거나, **GitHub Pages**가 아닌 다른 웹 서버에서 기본 URL(base URL)을 붙여 접속하려는 경우에는 `baseurl`을 슬래시로 시작하는 프로젝트 이름(예: `/project-name`)으로 설정해야 합니다.

이제 아래 방법 중 _하나_를 선택해 Jekyll 사이트를 배포할 수 있습니다.

### GitHub Actions로 배포하기

다음 사항을 준비합니다.

- GitHub Free 플랜을 사용 중이라면 사이트 저장소를 공개(public)로 유지하세요.
- `Gemfile.lock`{: .filepath}을 저장소에 커밋했고 로컬 컴퓨터가 Linux가 아니라면, lock 파일의 플랫폼 목록을 업데이트하세요.

  ```console
  $ bundle lock --add-platform x86_64-linux
  ```

다음으로 _Pages_ 서비스를 설정합니다.

1. GitHub에서 저장소로 이동합니다. _Settings_ 탭을 선택한 뒤 왼쪽 메뉴에서 _Pages_를 클릭합니다. **Source** 항목(_Build and deployment_ 아래)의 드롭다운 메뉴에서 [**GitHub Actions**][pages-workflow-src]를 선택합니다.  
   ![Build source](/assets/img/posts/pages-source-light.png){: .light .border .normal w='375' h='140' }
   ![Build source](/assets/img/posts/pages-source-dark.png){: .dark .normal w='375' h='140' }

2. 아무 커밋이나 GitHub에 push하면 _Actions_ 워크플로가 실행됩니다. 저장소의 _Actions_ 탭에서 _Build and Deploy_ 워크플로가 실행되는 것을 확인할 수 있으며, 빌드가 성공적으로 완료되면 사이트가 자동으로 배포됩니다.

이제 GitHub에서 제공하는 URL로 사이트에 접속할 수 있습니다.

### 수동 빌드 및 배포

직접 운영하는 서버에 배포하려면 로컬 컴퓨터에서 사이트를 빌드한 뒤 사이트 파일을 서버에 업로드해야 합니다.

소스 프로젝트의 루트로 이동한 뒤, 다음 명령으로 사이트를 빌드합니다.

```console
$ JEKYLL_ENV=production bundle exec jekyll b
```

출력 경로를 따로 지정하지 않았다면 생성된 사이트 파일은 프로젝트 루트의 `_site`{: .filepath} 폴더에 저장됩니다. 이 파일들을 대상 서버에 업로드하면 됩니다.

---

[nodejs]: https://nodejs.org/
[starter]: https://github.com/cotes2020/chirpy-starter
[pages-workflow-src]: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow
[docker-desktop]: https://www.docker.com/products/docker-desktop/
[docker-engine]: https://docs.docker.com/engine/install/
[vscode]: https://code.visualstudio.com/
[dev-containers]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers
[dc-clone-in-vol]: https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-a-git-repository-or-github-pr-in-an-isolated-container-volume
[dc-open-in-container]: https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-an-existing-folder-in-a-container
