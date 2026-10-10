---
title: Jekyll로 GitHub Pages 사이트 만들기
description: Jekyll을 사용해 새 저장소나 기존 저장소에 GitHub Pages 사이트를 만들 수 있습니다.
date: 2026-10-18 00:00:00 +0900
categories: [GitHub Pages, Jekyll]
tags: [github-pages, jekyll]
---

> `github-pages` gem은 일부 워크플로에서 여전히 지원되지만, 이제는 GitHub Actions로 GitHub Pages 사이트를 배포하고 자동화하는 방식이 권장됩니다.
{: .prompt-info }

## 사전 준비

Jekyll로 GitHub Pages 사이트를 만들려면 먼저 Jekyll과 Git을 설치해야 합니다. 자세한 내용은 Jekyll 문서의 [Installation](https://jekyllrb.com/docs/installation/)과 [Git 설정하기](https://docs.github.com/en/get-started/git-basics/set-up-git)를 참고하세요.

Jekyll을 설치하고 실행할 때는 [Bundler](https://bundler.io/) 사용을 권장합니다. Bundler는 Ruby gem 의존성을 관리하고, Jekyll 빌드 오류를 줄이며, 환경 차이로 생기는 버그를 막아 줍니다. Bundler 설치 방법은 다음과 같습니다.

1. Ruby를 설치합니다. 자세한 내용은 Ruby 문서의 [Ruby 설치하기](https://www.ruby-lang.org/en/documentation/installation/)를 참고하세요.
2. Bundler를 설치합니다. 자세한 내용은 [Bundler](https://bundler.io/)를 참고하세요.

> **macOS**: Bundler로 Jekyll을 설치하다가 Ruby 오류가 나면 [RVM](https://rvm.io/)이나 [Homebrew](https://brew.sh/) 같은 패키지 관리자로 Ruby 설치를 관리해야 할 수 있습니다. 자세한 내용은 Jekyll 문서의 [Troubleshooting](https://jekyllrb.com/docs/troubleshooting/#jekyll--macos)을 참고하세요.
{: .prompt-tip }

## 사이트용 저장소 만들기

저장소를 새로 만들어도 되고, 기존 저장소를 골라 사이트로 써도 됩니다.

저장소 안의 모든 파일이 사이트와 관련된 것은 아닌 저장소에 GitHub Pages 사이트를 만들고 싶다면, 사이트의 게시 원본을 따로 구성할 수 있습니다. 예를 들어 사이트 소스 파일만 담는 전용 브랜치와 폴더를 두거나, 사용자 지정 GitHub Actions 워크플로로 사이트 소스 파일을 빌드하고 배포할 수 있습니다.

저장소를 소유한 계정이 GitHub Free(개인) 또는 GitHub Free(조직)를 사용한다면, 저장소는 공개(public)여야 합니다.

기존 저장소에 사이트를 만들려면 아래 "사이트 만들기" 단계로 넘어가세요.

1. 아무 페이지에서나 오른쪽 위의 <kbd>+</kbd>를 선택한 다음 **New repository**를 클릭합니다.

   ![새 항목 만들기 메뉴. "New repository" 항목이 강조되어 있음](/assets/img/posts/repo-create-global-nav-update.png){: .shadow w='366' h='258' }

2. **Owner** 드롭다운 메뉴에서 저장소를 소유할 계정을 선택합니다.

   ![새 저장소의 소유자 메뉴. octocat과 github 두 가지 선택지가 보임](/assets/img/posts/create-repository-owner.png){: .shadow w='764' h='152' }

3. 저장소 이름과 설명(선택)을 입력합니다. 사용자 또는 조직 사이트를 만든다면 저장소 이름은 반드시 `<user>.github.io` 또는 `<organization>.github.io`여야 합니다. 사용자명이나 조직명에 대문자가 있다면 소문자로 바꿔서 입력해야 합니다. 자세한 내용은 [GitHub Pages 사이트의 종류](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages#types-of-github-pages-sites)를 참고하세요.

   ![저장소 이름 입력란에 "octocat.github.io"가 입력된 화면](/assets/img/posts/create-repository-name-pages.png){: .shadow w='1106' h='277' }

4. 저장소 공개 범위를 선택합니다. 자세한 내용은 [저장소 공개 범위](https://docs.github.com/en/repositories/creating-and-managing-repositories/about-repositories#about-repository-visibility)를 참고하세요.

## 사이트 만들기

사이트를 만들려면 먼저 GitHub에 사이트용 저장소가 있어야 합니다. 기존 저장소에 사이트를 만드는 게 아니라면 위의 "사이트용 저장소 만들기"를 먼저 진행하세요.

> 저장소가 비공개(private)이더라도 GitHub Pages 사이트는 인터넷에 공개됩니다(요금제나 조직 설정이 허용하는 경우). 사이트 저장소에 민감한 데이터가 있다면 게시 전에 제거하는 것이 좋습니다. 자세한 내용은 [저장소 공개 범위](https://docs.github.com/en/repositories/creating-and-managing-repositories/about-repositories#about-repository-visibility)를 참고하세요.
{: .prompt-warning }

1. 터미널을 엽니다. macOS와 Linux는 터미널, Windows는 Git Bash를 사용합니다.
2. 저장소의 로컬 복사본이 아직 없다면, 사이트 소스 파일을 보관할 위치로 이동합니다. PARENT-FOLDER는 저장소 폴더를 담을 폴더로 바꿉니다.

   ```shell
   cd PARENT-FOLDER
   ```

3. 아직 하지 않았다면 로컬 Git 저장소를 초기화합니다. REPOSITORY-NAME은 저장소 이름으로 바꿉니다.

   ```shell
   git init REPOSITORY-NAME
   > Initialized empty Git repository in /REPOSITORY-NAME/.git/
   # 컴퓨터에 새 폴더를 만들고 Git 저장소로 초기화
   ```

4. 저장소 폴더로 이동합니다.

   ```shell
   cd REPOSITORY-NAME
   # 작업 디렉터리 변경
   ```

5. 사용할 게시 원본을 정합니다. 자세한 내용은 [GitHub Pages 사이트의 게시 원본 구성하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)를 참고하세요.
6. 사이트의 게시 원본으로 이동합니다. 예를 들어 기본 브랜치의 `docs` 폴더에서 사이트를 게시하기로 했다면 `docs` 폴더를 만들고 그 안으로 이동합니다.

   ```shell
   mkdir docs
   # docs라는 새 폴더 만들기
   cd docs
   ```

   `gh-pages` 브랜치에서 사이트를 게시하기로 했다면 `gh-pages` 브랜치를 만들고 체크아웃합니다.

   ```shell
   git checkout --orphan gh-pages
   # 기록과 내용이 없는 gh-pages 브랜치를 새로 만들고 그 브랜치로 전환
   git rm -rf .
   # 작업 디렉터리에서 기본 브랜치의 내용 제거
   ```

7. 새 Jekyll 사이트를 만들려면 저장소 루트 디렉터리에서 `jekyll new` 명령을 사용합니다.

   ```shell
   jekyll new --skip-bundle .
   # 현재 디렉터리에 Jekyll 사이트 만들기
   ```

8. Jekyll이 만든 Gemfile을 엽니다.
9. `gem "jekyll"`로 시작하는 줄 맨 앞에 "#"을 붙여 이 줄을 주석 처리합니다.
10. `# gem "github-pages"`로 시작하는 줄을 수정해 `github-pages` gem을 추가합니다. 이 줄을 다음과 같이 바꿉니다.

    ```ruby
    gem "github-pages", "~> GITHUB-PAGES-VERSION", group: :jekyll_plugins
    ```

    GITHUB-PAGES-VERSION은 지원되는 `github-pages` gem의 최신 버전으로 바꿉니다. 버전은 [Dependency versions](https://pages.github.com/versions.json)에서 확인할 수 있습니다.

    올바른 버전의 Jekyll은 `github-pages` gem의 의존성으로 함께 설치됩니다.

11. Gemfile을 저장하고 닫습니다.
12. 명령줄에서 `bundle install`을 실행합니다.
13. Jekyll이 만든 `.gitignore` 파일을 열고, 다음 줄을 추가해 gem 잠금 파일을 무시하도록 합니다.

    ```shell
    Gemfile.lock
    ```

14. 필요하다면 `_config.yml`{: .filepath} 파일을 수정합니다. 저장소가 하위 디렉터리에서 호스팅될 때 상대 경로를 쓰려면 이 설정이 필요합니다. 자세한 내용은 [하위 폴더를 새 저장소로 분리하기](https://docs.github.com/en/get-started/using-git/splitting-a-subfolder-out-into-a-new-repository)를 참고하세요.

    ```yaml
    domain: my-site.github.io       # HTTPS를 강제하려면 앞의 http 없이 도메인만 적기 (예: example.com)
    url: https://my-site.github.io  # 사이트의 기본 호스트명과 프로토콜 (예: http://example.com)
    baseurl: /REPOSITORY-NAME/      # 사이트가 하위 폴더에서 제공된다면 폴더 이름 적기
    ```

15. 필요하다면 사이트를 로컬에서 테스트합니다. 자세한 내용은 [Jekyll로 로컬에서 GitHub Pages 사이트 테스트하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)를 참고하세요.
16. 작업한 내용을 추가하고 커밋합니다.

    ```shell
    git add .
    git commit -m 'Initial GitHub pages site with Jekyll'
    ```

17. GitHub의 저장소를 원격 저장소로 추가합니다. USER는 저장소를 소유한 계정으로, REPOSITORY는 저장소 이름으로 바꿉니다.

    ```shell
    git remote add origin https://github.com/USER/REPOSITORY.git
    ```

18. 저장소를 GitHub에 push합니다. BRANCH는 작업 중인 브랜치 이름으로 바꿉니다.

    ```shell
    git push -u origin BRANCH
    ```

19. 게시 원본을 구성합니다. 자세한 내용은 [GitHub Pages 사이트의 게시 원본 구성하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)를 참고하세요.
20. GitHub에서 사이트 저장소로 이동합니다.
21. 저장소 이름 아래에서 **Settings**를 클릭합니다. "Settings" 탭이 보이지 않으면 <kbd>···</kbd> 드롭다운 메뉴를 선택한 다음 **Settings**를 클릭합니다.

    ![저장소 상단 탭. "Settings" 탭이 강조되어 있음](/assets/img/posts/repo-actions-settings.png){: .shadow w='1098' h='108' }

22. 사이드바의 "Code, planning, and automation" 섹션에서 **Pages**를 클릭합니다.
23. 게시된 사이트를 보려면 "GitHub Pages" 아래의 **Visit site**를 클릭합니다.

    ![GitHub Pages 확인 메시지와 사이트 주소. 회색 "Visit site" 버튼이 강조되어 있음](/assets/img/posts/click-pages-url-to-preview.png){: .shadow w='800' h='191' }

    > 변경 사항을 GitHub에 push한 뒤 사이트에 반영되기까지 최대 10분이 걸릴 수 있습니다. 1시간이 지나도 브라우저에 변경 사항이 보이지 않는다면 [GitHub Pages 사이트의 Jekyll 빌드 오류 알아보기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-jekyll-build-errors-for-github-pages-sites)를 참고하세요.
    {: .prompt-info }

24. GitHub Pages 사이트는 GitHub Actions 워크플로로 빌드되고 배포됩니다. 자세한 내용은 [워크플로 실행 기록 보기](https://docs.github.com/en/actions/how-tos/monitor-workflows/view-workflow-run-history)를 참고하세요.

    > GitHub Actions는 공개 저장소에서 무료입니다. 비공개·내부 저장소는 매월 제공되는 무료 사용 시간을 넘기면 요금이 부과됩니다. 자세한 내용은 [GitHub Actions 요금과 사용량](https://docs.github.com/en/actions/concepts/billing-and-usage)을 참고하세요.
    {: .prompt-info }

> - 브랜치에서 게시하는데 사이트가 자동으로 게시되지 않았다면, 관리자 권한과 인증된 이메일 주소를 가진 사람이 게시 원본에 push했는지 확인하세요.
> - `GITHUB_TOKEN`을 사용하는 GitHub Actions 워크플로가 push한 커밋은 GitHub Pages 빌드를 실행하지 않습니다.
{: .prompt-info }

## 다음 단계

사이트에 새 페이지나 글을 추가하는 방법은 [Jekyll로 GitHub Pages 사이트에 콘텐츠 추가하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-content-to-your-github-pages-site-using-jekyll)를 참고하세요.

GitHub Pages 사이트에 Jekyll 테마를 추가해 사이트의 모양과 분위기를 바꿀 수 있습니다. 자세한 내용은 [Jekyll로 GitHub Pages 사이트에 테마 추가하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll)를 참고하세요.

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
