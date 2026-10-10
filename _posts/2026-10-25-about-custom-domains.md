---
title: 사용자 지정 도메인 알아보기
description: >-
  GitHub Pages는 사용자 지정 도메인을 지원합니다. octocat.github.io 같은 기본 주소 대신
  내가 소유한 도메인을 사이트 주소로 쓸 수 있습니다.
date: 2026-10-25 00:00:00 +0900
categories: [GitHub Pages, 사용자 지정 도메인]
tags: [github-pages, custom-domain]
---

## 지원되는 사용자 지정 도메인

> 보안을 높이고 도메인 탈취 공격을 막기 위해, 저장소에 사용자 지정 도메인을 추가하기 전에 도메인을 먼저 인증하는 것을 권장합니다. 자세한 내용은 [GitHub Pages의 사용자 지정 도메인 확인하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)를 참고하세요.
{: .prompt-tip }

GitHub Pages는 서브도메인과 에이펙스 도메인, 두 종류의 도메인을 지원합니다. 지원되지 않는 사용자 지정 도메인 목록은 [사용자 지정 도메인 문제 해결: 지원되지 않는 도메인](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/troubleshooting-custom-domains-and-github-pages#custom-domain-names-that-are-unsupported)을 참고하세요.

| 지원되는 사용자 지정 도메인 종류 | 예시 |
| --- | --- |
| `www` 서브도메인 | `www.example.com` |
| 사용자 지정 서브도메인 | `blog.example.com` |
| 에이펙스 도메인 | `example.com` |

사이트에 에이펙스 도메인과 `www` 서브도메인 중 하나만 설정해도 되고, 둘 다 설정해도 됩니다. 에이펙스 도메인에 대한 자세한 내용은 아래 "GitHub Pages 사이트에 에이펙스 도메인 사용하기"를 참고하세요.

에이펙스 도메인을 함께 쓰더라도 항상 `www` 서브도메인을 사용하는 것을 권장합니다. 에이펙스 도메인으로 새 사이트를 만들면, GitHub가 사이트 콘텐츠를 제공할 때 쓸 `www` 서브도메인을 자동으로 확보하려고 시도합니다. 하지만 `www` 서브도메인을 사용하려면 DNS 설정은 직접 바꿔야 합니다. `www` 서브도메인을 설정하면 GitHub가 연결된 에이펙스 도메인을 자동으로 확보하려고 시도합니다. 자세한 내용은 [GitHub Pages 사이트의 사용자 지정 도메인 관리하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)를 참고하세요.

## 여러 저장소에서 사용자 지정 도메인 사용하기

기본적으로 **사용자 사이트**나 **조직 사이트**에 사용자 지정 도메인을 설정하면, 같은 계정이 소유한 모든 프로젝트 사이트에도 같은 사용자 지정 도메인이 적용됩니다. 사이트 종류에 대한 자세한 내용은 [GitHub Pages 사이트의 종류](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages#types-of-github-pages-sites)를 참고하세요.

예를 들어 사용자 사이트의 사용자 지정 도메인이 `www.octocat.com`이고, 사용자 지정 도메인을 따로 설정하지 않은 `octo-project` 저장소에서 프로젝트 사이트를 게시한다면, 그 저장소의 GitHub Pages 사이트는 `www.octocat.com/octo-project`에서 볼 수 있습니다.

개별 저장소에 사용자 지정 도메인을 추가하면 이 기본 사용자 지정 도메인을 덮어쓸 수 있습니다.

> 비공개로 게시된 프로젝트 사이트의 URL은 사용자 사이트나 조직 사이트의 사용자 지정 도메인의 영향을 받지 않습니다. 비공개로 게시된 사이트에 대한 자세한 내용은 GitHub Enterprise Cloud 문서의 [GitHub Pages 사이트 공개 범위 바꾸기](https://docs.github.com/en/enterprise-cloud@latest/pages/getting-started-with-github-pages/changing-the-visibility-of-your-github-pages-site)를 참고하세요.
{: .prompt-info }

기본 사용자 지정 도메인을 없애려면 사용자 사이트나 조직 사이트에서 사용자 지정 도메인을 제거해야 합니다.

## GitHub Pages 사이트에 서브도메인 사용하기

서브도메인은 URL에서 루트 도메인 앞에 오는 부분입니다. 서브도메인은 `www`로 설정할 수도 있고, `blog.example.com`처럼 사이트의 별도 영역으로 설정할 수도 있습니다.

서브도메인은 DNS 제공업체에서 `CNAME` 레코드로 설정합니다. 자세한 내용은 [사용자 지정 도메인 관리하기: 서브도메인 설정하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-a-subdomain)를 참고하세요.

### `www` 서브도메인

`www` 서브도메인은 가장 흔하게 쓰이는 서브도메인입니다. 예를 들어 `www.example.com`에는 `www` 서브도메인이 들어 있습니다.

`www` 서브도메인은 GitHub 서버의 IP 주소가 바뀌어도 영향을 받지 않기 때문에 가장 안정적인 사용자 지정 도메인입니다.

### 사용자 지정 서브도메인

사용자 지정 서브도메인은 표준 `www`가 아닌 서브도메인입니다. 주로 사이트를 서로 다른 두 영역으로 나누고 싶을 때 사용합니다. 예를 들어 `blog.example.com`이라는 사이트를 만들어 `www.example.com`과 따로 꾸밀 수 있습니다.

## GitHub Pages 사이트에 에이펙스 도메인 사용하기

에이펙스 도메인은 `example.com`처럼 서브도메인이 없는 사용자 지정 도메인입니다. 베이스, 베어, 네이키드, 루트 에이펙스, 존 에이펙스 도메인이라고도 부릅니다.

에이펙스 도메인은 DNS 제공업체에서 `A`, `ALIAS`, `ANAME` 레코드로 설정합니다. 자세한 내용은 [사용자 지정 도메인 관리하기: 에이펙스 도메인 설정하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain)를 참고하세요.

에이펙스 도메인을 사용자 지정 도메인으로 쓴다면 `www` 서브도메인도 함께 설정하는 것을 권장합니다. DNS 제공업체에서 각 도메인 종류에 맞는 레코드를 올바르게 설정하면, GitHub Pages가 도메인 사이의 리디렉션을 자동으로 만들어 줍니다. 예를 들어 사이트의 사용자 지정 도메인을 `www.example.com`으로 설정하고 에이펙스 도메인과 `www` 도메인 모두에 GitHub Pages DNS 레코드를 설정했다면, `example.com`은 `www.example.com`으로 리디렉션됩니다. 반대로 `example.com`을 사용자 지정 도메인으로 설정했다면 `www.example.com`이 `example.com`으로 리디렉션됩니다. 자동 리디렉션은 다른 서브도메인에도 적용되어, `www.blog.example.com`은 `blog.example.com`으로(또는 그 반대로) 리디렉션됩니다. `www.www.`로 시작하는 도메인은 설정할 수 없습니다. 자세한 내용은 [사용자 지정 도메인 관리하기: 서브도메인 설정하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-a-subdomain)를 참고하세요.

## GitHub Pages 사이트의 사용자 지정 도메인 보호하기

GitHub Pages 사이트가 비활성화되었는데 사용자 지정 도메인이 설정되어 있다면 도메인 탈취 위험이 있습니다. 사이트가 비활성화된 상태에서 DNS 제공업체에 사용자 지정 도메인이 설정되어 있으면, 다른 사람이 내 서브도메인 중 하나에 사이트를 호스팅할 수 있습니다.

사용자 지정 도메인을 인증하면 다른 GitHub 사용자가 자기 저장소에서 내 도메인을 사용하지 못하게 막을 수 있습니다. 도메인이 인증되지 않았는데 GitHub Pages 사이트가 비활성화되었다면, 즉시 DNS 제공업체에서 DNS 레코드를 수정하거나 삭제해야 합니다. 자세한 내용은 [GitHub Pages의 사용자 지정 도메인 확인하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)와 [GitHub Pages 사이트의 사용자 지정 도메인 관리하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)를 참고하세요.

사이트가 자동으로 비활성화되는 경우는 다음과 같습니다.

- GitHub Pro에서 GitHub Free로 요금제를 낮추면, 계정의 비공개 저장소에서 게시 중이던 GitHub Pages 사이트는 모두 게시가 취소됩니다. 자세한 내용은 [요금제 낮추기](https://docs.github.com/en/billing/how-tos/manage-plan-and-licenses/downgrade-plan)를 참고하세요.
- 비공개 저장소를 GitHub Free를 사용하는 개인 계정으로 옮기면, 그 저장소는 GitHub Pages 기능을 쓸 수 없게 되고 게시 중이던 GitHub Pages 사이트는 게시가 취소됩니다. 자세한 내용은 [저장소 옮기기](https://docs.github.com/en/repositories/creating-and-managing-repositories/transferring-a-repository)를 참고하세요.

## 더 읽어보기

- [사용자 지정 도메인과 GitHub Pages 문제 해결](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/troubleshooting-custom-domains-and-github-pages)

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
