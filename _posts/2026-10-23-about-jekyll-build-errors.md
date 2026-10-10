---
title: Jekyll 빌드 오류 알아보기
description: >-
  Jekyll이 로컬이나 GitHub에서 GitHub Pages 사이트를 빌드하다가 오류를 만나면,
  자세한 정보가 담긴 오류 메시지를 받게 됩니다.
date: 2026-10-23 00:00:00 +0900
categories: [GitHub Pages, Jekyll]
tags: [github-pages, jekyll, troubleshooting]
---

> `github-pages` gem은 일부 워크플로에서 여전히 지원되지만, 이제는 GitHub Actions로 GitHub Pages 사이트를 배포하고 자동화하는 방식이 권장됩니다.
{: .prompt-info }

## Jekyll 빌드 오류란

브랜치에서 게시하는 경우, 사이트의 게시 원본에 변경 사항을 push해도 GitHub Pages가 사이트 빌드를 시도하지 않을 때가 있습니다.

- 변경 사항을 push한 사람이 이메일 주소를 인증하지 않은 경우. 자세한 내용은 [이메일 주소 인증하기](https://docs.github.com/en/account-and-profile/how-tos/email-preferences/verifying-your-email-address)를 참고하세요.
- 배포 키(deploy key)로 push하는 경우. 사이트 저장소로의 push를 자동화하고 싶다면 대신 머신 사용자(machine user)를 설정할 수 있습니다. 자세한 내용은 [배포 키 관리하기: 머신 사용자](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys#machine-users)를 참고하세요.
- 게시 원본을 빌드하도록 설정되지 않은 CI 서비스를 사용하는 경우. 예를 들어 Travis CI는 `gh-pages` 브랜치를 허용 목록에 추가하지 않으면 그 브랜치를 빌드하지 않습니다. 자세한 내용은 Travis CI의 [Customizing the build](https://docs.travis-ci.com/user/customizing-the-build/#safelisting-or-blocklisting-branches)나 사용하는 CI 서비스의 문서를 참고하세요.

> 변경 사항을 GitHub에 push한 뒤 사이트에 반영되기까지 최대 10분이 걸릴 수 있습니다.
{: .prompt-info }

Jekyll이 사이트 빌드를 시도하다가 오류를 만나면 빌드 오류 메시지를 받게 됩니다.

빌드 오류를 해결하는 방법은 [GitHub Pages 사이트의 Jekyll 빌드 오류 문제 해결](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/troubleshooting-jekyll-build-errors-for-github-pages-sites)을 참고하세요.

## GitHub Actions에서 Jekyll 빌드 오류 메시지 보기

다른 CI 도구를 쓰도록 설정하지 않았다면, GitHub Pages 사이트는 기본적으로 GitHub Actions 워크플로 실행으로 빌드되고 배포됩니다. 빌드 오류를 찾으려면 저장소의 워크플로 실행 기록에서 GitHub Pages 사이트의 워크플로 실행을 확인하면 됩니다. 자세한 내용은 [워크플로 실행 기록 보기](https://docs.github.com/en/actions/how-tos/monitor-workflows/view-workflow-run-history)를 참고하세요. 오류가 났을 때 워크플로를 다시 실행하는 방법은 [워크플로와 잡 다시 실행하기](https://docs.github.com/en/actions/how-tos/manage-workflow-runs/re-run-workflows-and-jobs)를 참고하세요.

## 로컬에서 Jekyll 빌드 오류 메시지 보기

사이트를 로컬에서 테스트하는 것을 권장합니다. 그러면 명령줄에서 빌드 오류 메시지를 확인하고, GitHub에 변경 사항을 push하기 전에 빌드 실패를 해결할 수 있습니다. 자세한 내용은 [Jekyll로 로컬에서 GitHub Pages 사이트 테스트하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)를 참고하세요.

## 풀 리퀘스트에서 Jekyll 빌드 오류 메시지 보기

브랜치에서 게시하는 경우, GitHub에서 게시 원본을 업데이트하는 풀 리퀘스트를 만들면 풀 리퀘스트의 **Checks** 탭에서 빌드 오류 메시지를 볼 수 있습니다. 자세한 내용은 [상태 확인(Status checks)](https://docs.github.com/en/pull-requests/reference/status-checks)을 참고하세요.

사용자 지정 GitHub Actions 워크플로로 게시하는 경우, 풀 리퀘스트에서 빌드 오류 메시지를 보려면 워크플로가 `pull_request` 트리거로 실행되도록 설정해야 합니다. 이때 `pull_request` 이벤트로 시작된 워크플로에서는 배포 단계를 건너뛰는 것을 권장합니다. 그러면 풀 리퀘스트의 변경 사항을 사이트에 배포하지 않고도 빌드 오류를 확인할 수 있습니다. 자세한 내용은 [워크플로를 실행하는 이벤트: pull_request](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#pull_request)와 [표현식](https://docs.github.com/en/actions/reference/workflows-and-actions/expressions)을 참고하세요.

## 이메일로 Jekyll 빌드 오류 받기

브랜치에서 게시하는 경우, GitHub의 게시 원본에 변경 사항을 push하면 GitHub Pages가 사이트 빌드를 시도합니다. 빌드에 실패하면 기본 이메일 주소로 메일을 받게 됩니다.

사용자 지정 GitHub Actions 워크플로로 게시하는 경우, 풀 리퀘스트의 빌드 오류를 이메일로 받으려면 워크플로가 `pull_request` 트리거로 실행되도록 설정해야 합니다. 이때 `pull_request` 이벤트로 시작된 워크플로에서는 배포 단계를 건너뛰는 것을 권장합니다. 그러면 풀 리퀘스트의 변경 사항을 사이트에 배포하지 않고도 빌드 오류를 확인할 수 있습니다.

## 외부 CI 서비스로 풀 리퀘스트에서 Jekyll 빌드 오류 메시지 보기

[Travis CI](https://travis-ci.com/) 같은 외부 서비스가 커밋할 때마다 오류 메시지를 보여 주도록 설정할 수 있습니다.

1. 아직 없다면 게시 원본의 루트에 다음 내용으로 _Gemfile_ 파일을 추가합니다.

   ```ruby
   source `https://rubygems.org`
   gem `github-pages`
   ```

2. 원하는 테스트 서비스에 맞게 사이트 저장소를 설정합니다. 예를 들어 [Travis CI](https://travis-ci.com/)를 사용하려면 게시 원본의 루트에 다음 내용으로 _.travis.yml_ 파일을 추가합니다.

   ```yaml
   language: ruby
   rvm:
     - 2.3
   script: "bundle exec jekyll build"
   ```

3. 외부 테스트 서비스에서 저장소를 활성화해야 할 수도 있습니다. 자세한 내용은 사용하는 테스트 서비스의 문서를 참고하세요.

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-jekyll-build-errors-for-github-pages-sites)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
