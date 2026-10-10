---
title: GitHub Pages 사이트 게시 취소하기
description: >-
  GitHub Pages 사이트의 게시를 취소하면 현재 배포가 제거되어 사이트를 더 이상 볼 수 없게 됩니다.
  사이트를 삭제하는 것과는 다릅니다.
date: 2026-10-12 00:00:00 +0900
categories: [GitHub Pages, 시작하기]
tags: [github-pages, github]
---

사이트 게시를 취소하면 현재 배포가 제거되고 사이트에 더 이상 접속할 수 없게 됩니다. 기존 저장소 설정이나 콘텐츠에는 아무 영향이 없습니다.

게시를 취소해도 사이트가 영구적으로 삭제되지는 않습니다. 사이트를 삭제하는 방법은 [GitHub Pages 사이트 삭제하기](https://docs.github.com/en/pages/getting-started-with-github-pages/deleting-a-github-pages-site)를 참고하세요.

1. GitHub에서 저장소의 메인 페이지로 이동합니다.
2. **GitHub Pages** 아래의 **Your site is live at** 메시지 옆에서 <kbd>···</kbd>를 클릭합니다.
3. 나타나는 메뉴에서 **Unpublish site**를 선택합니다.

   ![GitHub Pages 설정 화면. 사이트 주소 오른쪽 메뉴에서 "Unpublish site" 항목이 강조되어 있음](/assets/img/posts/unpublish-site.png){: .shadow w='800' h='178' }

## 게시를 취소한 사이트 다시 켜기

GitHub Pages 사이트의 게시를 취소하면 현재 배포가 제거됩니다. 사이트를 다시 볼 수 있게 하려면 새 배포를 만들면 됩니다.

### GitHub Actions로 다시 켜기

사이트 저장소에서 워크플로가 한 번 성공적으로 실행되면 새 배포가 만들어집니다. 워크플로를 실행해 사이트를 다시 배포하세요.

### 브랜치에서 게시하는 경우 다시 켜기

1. 원하는 브랜치에서 게시하도록 게시 원본을 구성합니다. 자세한 내용은 [브랜치에서 게시하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-from-a-branch)를 참고하세요.
2. 게시 원본에 커밋하면 새 배포가 만들어집니다.

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/getting-started-with-github-pages/unpublishing-a-github-pages-site)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
