---
title: HTTPS로 사이트 보호하기
description: >-
  HTTPS는 다른 사람이 사이트로 오가는 트래픽을 엿보거나 조작하지 못하게 막는 암호화 계층을 추가합니다.
  GitHub Pages 사이트에 HTTPS를 강제로 적용해 모든 HTTP 요청을 HTTPS로 넘길 수 있습니다.
date: 2026-10-14 00:00:00 +0900
categories: [GitHub Pages, 시작하기]
tags: [github-pages, https]
---

> 저장소 관리자(admin) 권한이 있는 사람이 GitHub Pages 사이트에 HTTPS를 강제로 적용할 수 있습니다.
{: .prompt-info }

## HTTPS와 GitHub Pages

사용자 지정 도메인이 올바르게 구성된 사이트를 포함해, 모든 GitHub Pages 사이트는 HTTPS와 HTTPS 강제 적용을 지원합니다. 사용자 지정 도메인에 대한 자세한 내용은 [사용자 지정 도메인과 GitHub Pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages)와 [사용자 지정 도메인 문제 해결: HTTPS 오류](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/troubleshooting-custom-domains-and-github-pages#https-errors)를 참고하세요.

2016년 6월 15일 이후에 만들어졌고 `github.io` 도메인을 사용하는 GitHub Pages 사이트는 자동으로 HTTPS로 제공됩니다.

GitHub Pages 사이트를 비밀번호나 신용카드 번호 전송 같은 민감한 거래에 사용해서는 안 됩니다.

> 저장소가 비공개(private)이더라도 GitHub Pages 사이트는 인터넷에 공개됩니다(요금제나 조직 설정이 허용하는 경우). 사이트 저장소에 민감한 데이터가 있다면 게시 전에 제거하는 것이 좋습니다. 자세한 내용은 [저장소 공개 범위](https://docs.github.com/en/repositories/creating-and-managing-repositories/about-repositories#about-repository-visibility)를 참고하세요.
{: .prompt-warning }

> RFC3280에 따르면 common name의 최대 길이는 64자입니다. 따라서 인증서가 정상적으로 만들어지려면 GitHub Pages 사이트의 전체 도메인 이름이 64자보다 짧아야 합니다.
{: .prompt-info }

## GitHub Pages 사이트에 HTTPS 강제 적용하기

1. GitHub에서 사이트 저장소로 이동합니다.
2. 저장소 이름 아래에서 **Settings**를 클릭합니다. "Settings" 탭이 보이지 않으면 <kbd>···</kbd> 드롭다운 메뉴를 선택한 다음 **Settings**를 클릭합니다.

   ![저장소 상단 탭. "Settings" 탭이 강조되어 있음](/assets/img/posts/repo-actions-settings.png){: .shadow w='1098' h='108' }

3. 사이드바의 "Code, planning, and automation" 섹션에서 **Pages**를 클릭합니다.
4. "GitHub Pages" 아래에서 **Enforce HTTPS**를 선택합니다.

## 인증서 발급 문제 해결 ("Certificate not yet created" 오류)

Pages 설정에서 사용자 지정 도메인을 설정하거나 바꾸면 자동 DNS 검사가 시작됩니다. 이 검사는 GitHub가 인증서를 자동으로 받을 수 있도록 DNS가 설정되어 있는지 확인합니다. 검사에 성공하면 GitHub는 [Let's Encrypt](https://letsencrypt.org/)에 TLS 인증서를 요청하는 작업을 대기열에 넣습니다. 유효한 인증서를 받으면 GitHub가 Pages의 TLS 종료를 처리하는 서버에 인증서를 자동으로 올립니다. 이 과정이 성공적으로 끝나면 사용자 지정 도메인 이름 옆에 체크 표시가 나타납니다.

이 과정은 시간이 좀 걸릴 수 있습니다. **Save**를 누르고 몇 분이 지나도 끝나지 않는다면, 사용자 지정 도메인 이름 옆의 **Remove**를 클릭해 보세요. 그런 다음 도메인 이름을 다시 입력하고 **Save**를 다시 클릭합니다. 이렇게 하면 발급 과정이 취소되었다가 다시 시작됩니다.

## 혼합 콘텐츠 문제 해결하기

GitHub Pages 사이트에 HTTPS를 켰는데 사이트 HTML이 여전히 HTTP로 이미지, CSS, JavaScript를 불러온다면, 사이트가 _혼합 콘텐츠(mixed content)_ 를 제공하고 있는 것입니다. 혼합 콘텐츠를 제공하면 사이트의 보안이 약해지고 리소스를 불러오는 데 문제가 생길 수 있습니다.

사이트의 혼합 콘텐츠를 없애려면 사이트 HTML에서 `http://`를 `https://`로 바꿔 모든 리소스가 HTTPS로 제공되게 하세요.

리소스는 보통 다음 위치에 있습니다.

- 사이트가 Jekyll을 사용한다면 HTML 파일은 대개 `_layouts` 폴더에 있습니다.
- CSS는 보통 HTML 파일의 `<head>` 영역에 있습니다.
- JavaScript는 보통 `<head>` 영역이나 닫는 `</body>` 태그 바로 앞에 있습니다.
- 이미지는 주로 `<body>` 영역에 있습니다.

> 사이트 소스 파일에서 리소스를 찾지 못했다면, 텍스트 편집기나 GitHub에서 사이트 소스 파일을 대상으로 `http://`를 검색해 보세요.
{: .prompt-tip }

### HTML 파일에서 리소스를 참조하는 예

| 리소스 종류 | HTTP | HTTPS |
| :---: | :--- | :--- |
| CSS | `<link rel="stylesheet" href="http://example.com/css/main.css">` | `<link rel="stylesheet" href="https://example.com/css/main.css">` |
| JavaScript | `<script type="text/javascript" src="http://example.com/js/main.js"></script>` | `<script type="text/javascript" src="https://example.com/js/main.js"></script>` |
| 이미지 | `<a href="http://www.somesite.com"><img src="http://www.example.com/logo.jpg" alt="Logo"></a>` | `<a href="https://www.somesite.com"><img src="https://www.example.com/logo.jpg" alt="Logo"></a>` |

## DNS 설정 확인하기

사용자 지정 도메인의 DNS 설정 때문에 HTTPS 인증서를 만들지 못하는 경우가 있습니다. 불필요한 DNS 레코드가 더 있거나, 레코드가 GitHub Pages의 IP 주소를 가리키지 않을 때 생길 수 있습니다.

HTTPS 인증서가 정상적으로 만들어지도록 아래 구성을 권장합니다. 호스트가 `@`인 `A`, `AAAA`, `ALIAS`, `ANAME` 레코드가 추가로 있거나, GitHub Pages에서 쓰려는 `www` 서브도메인이나 다른 서브도메인을 가리키는 `CNAME` 레코드가 추가로 있으면 HTTPS 인증서가 만들어지지 않을 수 있습니다.

| 상황 | DNS 레코드 종류 | DNS 레코드 이름 | DNS 레코드 값 |
| --- | --- | --- | --- |
| 에이펙스 도메인<br />(`example.com`) | `A` | `@` | `185.199.108.153`<br />`185.199.109.153`<br />`185.199.110.153`<br />`185.199.111.153` |
| 에이펙스 도메인<br />(`example.com`) | `AAAA` | `@` | `2606:50c0:8000::153`<br />`2606:50c0:8001::153`<br />`2606:50c0:8002::153`<br />`2606:50c0:8003::153` |
| 에이펙스 도메인<br />(`example.com`) | `ALIAS` 또는 `ANAME` | `@` | `USERNAME.github.io` 또는<br />`ORGANIZATION.github.io` |
| 서브도메인<br />(`www.example.com`,<br />`blog.example.com`) | `CNAME` | `SUBDOMAIN.example.com.` | `USERNAME.github.io` 또는<br />`ORGANIZATION.github.io` |

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
