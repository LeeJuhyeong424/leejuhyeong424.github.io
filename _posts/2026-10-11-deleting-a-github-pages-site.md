---
title: GitHub Pages 사이트 삭제하기
description: GitHub Pages 사이트를 삭제하는 방법을 알아봅니다.
date: 2026-10-11 00:00:00 +0900
categories: [GitHub Pages, 시작하기]
tags: [github-pages, github]
---

## 사이트 삭제하기

사이트를 삭제하는 방법은 두 가지입니다.

- 저장소를 삭제합니다. 자세한 내용은 [저장소 삭제하기](https://docs.github.com/en/repositories/creating-and-managing-repositories/deleting-a-repository)를 참고하세요.
- 게시 원본을 `None` 브랜치로 바꿉니다. 자세한 내용은 아래 "게시 원본을 바꿔서 사이트 삭제하기"를 참고하세요.

사이트를 삭제하지는 않고 현재 배포만 내리고 싶다면 사이트 게시를 취소할 수 있습니다. 자세한 내용은 [GitHub Pages 사이트 게시 취소하기](https://docs.github.com/en/pages/getting-started-with-github-pages/unpublishing-a-github-pages-site)를 참고하세요.

## 게시 원본을 바꿔서 사이트 삭제하기

1. GitHub에서 사이트 저장소로 이동합니다.
2. 저장소 이름 아래에서 **Settings**를 클릭합니다. "Settings" 탭이 보이지 않으면 <kbd>···</kbd> 드롭다운 메뉴를 선택한 다음 **Settings**를 클릭합니다.

   ![저장소 상단 탭. "Settings" 탭이 강조되어 있음](/assets/img/posts/repo-actions-settings.png){: .shadow w='1098' h='108' }

3. 사이드바의 "Code, planning, and automation" 섹션에서 **Pages**를 클릭합니다.
4. "Build and deployment"의 "Source"에서 **Deploy from a branch**를 선택합니다. 사이트가 지금 GitHub Actions를 사용하고 있더라도 이 항목을 선택합니다.
5. "Build and deployment"에서 브랜치 드롭다운 메뉴를 사용해 게시 원본으로 `None`을 선택합니다.

   ![Pages 설정 화면. 게시 원본 브랜치를 고르는 "None" 메뉴가 강조되어 있음](/assets/img/posts/publishing-source-drop-down.png){: .shadow w='807' h='148' }

6. **Save**를 클릭합니다.

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/getting-started-with-github-pages/deleting-a-github-pages-site)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
