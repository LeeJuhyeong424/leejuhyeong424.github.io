---
title: GitHub Pages에서 하위 모듈 사용하기
description: GitHub Pages에서 Git 하위 모듈(submodule)을 사용해 다른 프로젝트를 사이트 코드에 포함할 수 있습니다.
date: 2026-10-15 00:00:00 +0900
categories: [GitHub Pages, 시작하기]
tags: [github-pages, git]
---

GitHub Pages 사이트 저장소에 하위 모듈이 있으면, 사이트를 빌드할 때 하위 모듈의 내용도 자동으로 함께 가져옵니다.

GitHub Pages 서버는 비공개 저장소에 접근할 수 없으므로, 공개 저장소를 가리키는 하위 모듈만 사용할 수 있습니다.

중첩된 하위 모듈을 포함한 모든 하위 모듈에는 `https://` 읽기 전용 URL을 사용하세요. 이 설정은 `.gitmodules` 파일에서 바꿀 수 있습니다.

## 더 읽어보기

- _Pro Git_ 책의 [Git 도구 - 서브모듈](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
- [GitHub Pages 사이트의 Jekyll 빌드 오류 문제 해결](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/troubleshooting-jekyll-build-errors-for-github-pages-sites)

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/getting-started-with-github-pages/using-submodules-with-github-pages)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
