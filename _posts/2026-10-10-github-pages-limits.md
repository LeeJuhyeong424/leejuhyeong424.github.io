---
title: GitHub Pages 제한 사항
description: GitHub Pages의 사용 한도와 제한 사항을 알아봅니다.
date: 2026-10-10 14:30:00 +0900
categories: [GitHub Pages, 시작하기]
tags: [github-pages, github]
---

## 사용 한도

GitHub Pages는 온라인 사업, 전자상거래 사이트, 또는 상업적 거래를 돕거나 상업용 SaaS(서비스형 소프트웨어)를 제공하는 것이 주목적인 웹사이트를 운영하기 위한 무료 웹 호스팅 서비스로 만들어지지 않았으며, 그런 용도로 사용하는 것도 허용되지 않습니다. 또한 GitHub Pages 사이트를 비밀번호나 신용카드 번호 전송 같은 민감한 거래에 사용해서는 안 됩니다.

이와 함께 GitHub Pages 사용은 [GitHub 서비스 약관](https://docs.github.com/en/site-policy/github-terms/github-terms-of-service)을 따라야 하며, 여기에는 일확천금 사기, 음란물, 폭력적이거나 위협적인 콘텐츠나 활동에 대한 제한이 포함됩니다.

GitHub Pages 사이트에는 다음과 같은 사용 한도가 있습니다.

- 사용자 또는 조직 사이트는 GitHub 계정당 하나만 만들 수 있습니다.
- GitHub Pages 소스 저장소의 권장 용량 한도는 1GB입니다. 자세한 내용은 [GitHub의 대용량 파일 정보](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github)를 참고하세요.
- 게시된 GitHub Pages 사이트의 크기는 1GB를 넘을 수 없습니다.
- GitHub Pages 배포가 10분 넘게 걸리면 시간 초과로 실패합니다.
- GitHub Pages 사이트에는 월 100GB의 _소프트_ 대역폭 한도가 있습니다.
- GitHub Pages 사이트에는 시간당 10회 빌드의 _소프트_ 한도가 있습니다. 사용자 지정 GitHub Actions 워크플로로 사이트를 빌드하고 게시하는 경우에는 이 한도가 적용되지 않습니다.
- 모든 GitHub Pages 사이트에 일관된 서비스 품질을 제공하기 위해 요청 수 제한(rate limit)이 적용될 수 있습니다. 이 제한은 GitHub Pages의 정상적인 사용을 방해하려는 것이 아닙니다. 요청이 제한에 걸리면 HTTP 상태 코드 `429`와 함께 안내가 담긴 HTML 본문이 응답으로 옵니다.

사이트가 이 사용 한도를 넘으면 사이트를 제공하지 못할 수 있습니다. 또는 GitHub 지원팀이 서버 부담을 줄이는 방법을 안내하는 정중한 이메일을 보낼 수 있습니다. 예를 들어 사이트 앞에 외부 CDN(콘텐츠 전송 네트워크)을 두거나, 릴리스 같은 다른 GitHub 기능을 활용하거나, 필요에 더 맞는 다른 호스팅 서비스로 옮기는 방법 등입니다.

## 교육용 실습

학습 목적으로 GitHub Pages에 기존 웹사이트의 복제본을 만드는 것은 금지되어 있지 않습니다. 다만 [GitHub 서비스 약관](https://docs.github.com/en/site-policy/github-terms/github-terms-of-service)을 지키는 것에 더해, 코드는 직접 작성해야 하고, 사이트는 어떤 사용자 데이터도 수집해서는 안 되며, 이 프로젝트가 원본과 관련이 없고 교육 목적으로만 만들어졌다는 고지를 사이트에 눈에 띄게 표시해야 합니다.

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
