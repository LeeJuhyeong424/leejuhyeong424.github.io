---
title: 사용자 지정 도메인 문제 해결
description: GitHub Pages 사이트의 사용자 지정 도메인에서 흔히 생기는 오류를 확인하고 해결합니다.
date: 2026-10-28 00:00:00 +0900
categories: [GitHub Pages, 사용자 지정 도메인]
tags: [github-pages, custom-domain, troubleshooting]
---

## CNAME 오류

사용자 지정 GitHub Actions 워크플로로 게시한다면 CNAME 파일은 무시되며 필요하지 않습니다.

브랜치에서 게시한다면 사용자 지정 도메인은 게시 원본 루트의 CNAME 파일에 저장됩니다. 이 파일은 저장소 설정에서 추가하거나 수정할 수도 있고, 직접 만들어도 됩니다. 자세한 내용은 [GitHub Pages 사이트의 사용자 지정 도메인 관리하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)를 참고하세요.

사이트가 올바른 도메인에서 표시되려면 CNAME 파일이 저장소에 그대로 남아 있어야 합니다. 예를 들어 많은 정적 사이트 생성기는 저장소에 강제 push(force push)를 하는데, 이때 사용자 지정 도메인을 설정하면서 저장소에 추가된 CNAME 파일을 덮어쓸 수 있습니다. 사이트를 로컬에서 빌드해 생성된 파일을 GitHub에 push한다면, CNAME 파일을 추가한 커밋을 먼저 로컬 저장소로 pull 해서 그 파일이 빌드에 포함되도록 하세요.

그다음 CNAME 파일의 형식이 올바른지 확인하세요.

- CNAME 파일 이름은 모두 대문자여야 합니다.
- CNAME 파일에는 도메인을 하나만 넣을 수 있습니다. 여러 도메인이 사이트를 가리키게 하려면 DNS 제공업체에서 리디렉션을 설정해야 합니다.
- CNAME 파일에는 도메인 이름만 들어가야 합니다. 예: `www.example.com`, `blog.example.com`, `example.com`
- 도메인 이름은 모든 GitHub Pages 사이트 사이에서 고유해야 합니다. 예를 들어 다른 저장소의 CNAME 파일에 `example.com`이 들어 있다면, 내 저장소의 CNAME 파일에는 `example.com`을 쓸 수 없습니다.

## DNS 설정 오류

사이트의 기본 도메인이 사용자 지정 도메인을 가리키도록 하는 데 문제가 있다면 DNS 제공업체에 문의하세요.

다음 방법으로 사용자 지정 도메인의 DNS 레코드가 올바르게 설정되었는지 테스트할 수도 있습니다.

- `dig` 같은 CLI 도구. 자세한 내용은 [GitHub Pages 사이트의 사용자 지정 도메인 관리하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)를 참고하세요.
- 온라인 DNS 조회 도구

## 지원되지 않는 사용자 지정 도메인

사용자 지정 도메인이 지원되지 않는다면 지원되는 도메인으로 바꿔야 할 수 있습니다. DNS 제공업체에 도메인 포워딩 서비스를 제공하는지 문의해 볼 수도 있습니다.

사이트가 다음에 해당하지 않는지 확인하세요.

- 에이펙스 도메인을 둘 이상 사용합니다. 예: `example.com`과 `anotherexample.com`을 모두 사용
- `www` 서브도메인을 둘 이상 사용합니다. 예: `www.example.com`과 `www.anotherexample.com`을 모두 사용
- 에이펙스 도메인과 사용자 지정 서브도메인을 함께 사용합니다. 예: `example.com`과 `docs.example.com`을 모두 사용

  단, `www` 서브도메인은 예외입니다. 올바르게 설정하면 `www` 서브도메인은 에이펙스 도메인으로 자동 리디렉션됩니다. 자세한 내용은 [사용자 지정 도메인 관리하기: 에이펙스 도메인 설정하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain)를 참고하세요.

> `*.example.com` 같은 와일드카드 DNS 레코드는 사용하지 않기를 강력히 권장합니다. 도메인을 인증하더라도 이런 레코드는 곧바로 도메인 탈취 위험을 만듭니다. 예를 들어 `example.com`을 인증하면 다른 사람이 `a.example.com`을 쓰지는 못하지만, 와일드카드 DNS 레코드가 적용되는 `b.a.example.com`은 여전히 탈취할 수 있습니다.
{: .prompt-warning }

지원되는 사용자 지정 도메인 목록은 [사용자 지정 도메인과 GitHub Pages: 지원되는 도메인](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages#supported-custom-domains)을 참고하세요.

## HTTPS 오류

`CNAME`, `ALIAS`, `ANAME`, `A` DNS 레코드가 올바르게 설정된 사용자 지정 도메인을 쓰는 GitHub Pages 사이트는 HTTPS로 접속할 수 있습니다. 자세한 내용은 [HTTPS로 GitHub Pages 사이트 보호하기](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)를 참고하세요.

사용자 지정 도메인을 설정한 뒤 사이트에 HTTPS로 접속할 수 있게 되기까지 최대 1시간이 걸릴 수 있습니다. 기존 DNS 설정을 바꿨다면, HTTPS 활성화 과정을 다시 시작하기 위해 사이트 저장소에서 사용자 지정 도메인을 제거했다가 다시 추가해야 할 수 있습니다. 자세한 내용은 [GitHub Pages 사이트의 사용자 지정 도메인 관리하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)를 참고하세요.

CAA(Certification Authority Authorization) 레코드를 사용한다면, 사이트에 HTTPS로 접속하려면 값이 `letsencrypt.org`인 CAA 레코드가 하나 이상 있어야 합니다. 자세한 내용은 Let's Encrypt 문서의 [Certificate Authority Authorization (CAA)](https://letsencrypt.org/docs/caa/)를 참고하세요.

## Linux에서의 URL 형식

사이트 URL에 들어가는 사용자명이나 조직명이 대시(`-`)로 시작하거나 끝나거나, 대시가 연속으로 들어 있다면, Linux에서 접속하는 사람은 사이트에 들어갈 때 서버 오류를 보게 됩니다. 이를 고치려면 GitHub 사용자명을 바꿔 영문자와 숫자가 아닌 문자를 없애세요. 자세한 내용은 [사용자명 변경](https://docs.github.com/en/account-and-profile/concepts/username-changes)을 참고하세요.

## 브라우저 캐시

최근에 사용자 지정 도메인을 바꾸거나 제거했는데 브라우저에서 새 URL에 접속되지 않는다면, 새 URL로 들어가기 위해 브라우저 캐시를 지워야 할 수 있습니다. 캐시를 지우는 방법은 사용하는 브라우저의 문서를 참고하세요.

## 이미 사용 중인 도메인

사용자 지정 도메인을 쓰려는데 이미 사용 중인 도메인이라고 나온다면, 먼저 도메인을 인증해서 내가 쓸 수 있게 만들 수 있습니다. 자세한 내용은 [GitHub Pages의 사용자 지정 도메인 확인하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)를 참고하세요.

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/troubleshooting-custom-domains-and-github-pages)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
