---
title: GitHub Pages란?
description: >-
  GitHub Pages를 사용하면 GitHub 저장소에서 바로 나, 조직, 프로젝트를 소개하는 웹사이트를 호스팅할 수 있습니다.
date: 2026-10-10 14:10:00 +0900
categories: [GitHub Pages, 시작하기]
tags: [github-pages, github]
---

## GitHub Pages 소개

GitHub Pages는 GitHub 저장소에서 HTML, CSS, JavaScript 파일을 바로 가져와, 필요하면 빌드 과정을 거친 뒤 웹사이트로 게시해 주는 정적 사이트 호스팅 서비스입니다. GitHub Pages 사이트의 예시는 [GitHub Pages 예시 모음](https://github.com/collections/github-pages-examples)에서 볼 수 있습니다.

## GitHub Pages 사이트의 종류

GitHub Pages 사이트에는 두 가지 종류가 있습니다. 사용자 또는 조직 계정에 연결된 사이트와, 특정 프로젝트를 위한 사이트입니다.

| 항목 | 사용자·조직 사이트 | 프로젝트 사이트 |
| :--- | :--- | :--- |
| 소스 파일 | `<owner>.github.io`라는 이름의 저장소에 저장해야 함 (`<owner>`는 개인 또는 조직 계정 이름) | 프로젝트 코드가 있는 저장소 안의 폴더에 저장 |
| 제한 | 계정당 최대 1개 | 저장소당 최대 1개 |
| 기본 사이트 주소 | `http(s)://<owner>.github.io` | `http(s)://<owner>.github.io/<repositoryname>` |

### 내 도메인에서 호스팅하기

사이트는 GitHub의 `github.io` 도메인이나 내 도메인에서 호스팅할 수 있습니다. 자세한 내용은 [GitHub Pages 사이트에 사용자 지정 도메인 구성하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)를 참고하세요.

## 데이터 수집

GitHub Pages 사이트를 방문하면, 방문자가 GitHub에 로그인했는지와 관계없이 보안을 위해 방문자의 IP 주소가 기록되고 저장됩니다. GitHub의 보안 관행에 대한 자세한 내용은 [GitHub 개인정보처리방침](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement)을 참고하세요.

## 더 읽어보기

- GitHub Skills의 [GitHub Pages](https://github.com/skills/github-pages) 과정
- [저장소 REST API: Pages](https://docs.github.com/en/rest/repos#pages)
- [GitHub Pages 사이트의 게시 원본 구성하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [여러 저장소에서 사용자 지정 도메인 사용하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages#using-a-custom-domain-across-multiple-repositories)

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
