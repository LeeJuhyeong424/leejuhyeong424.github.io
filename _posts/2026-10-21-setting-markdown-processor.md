---
title: Markdown 프로세서 설정하기
description: GitHub Pages 사이트에서 Markdown을 렌더링할 때 사용할 Markdown 프로세서를 고를 수 있습니다.
date: 2026-10-21 00:00:00 +0900
categories: [GitHub Pages, Jekyll]
tags: [github-pages, jekyll, markdown]
---

> `github-pages` gem은 일부 워크플로에서 여전히 지원되지만, 이제는 GitHub Actions로 GitHub Pages 사이트를 배포하고 자동화하는 방식이 권장됩니다.
{: .prompt-info }

> 저장소 쓰기 권한이 있는 사람이 GitHub Pages 사이트의 Markdown 프로세서를 설정할 수 있습니다.
{: .prompt-info }

GitHub Pages는 두 가지 Markdown 프로세서를 지원합니다. 하나는 [kramdown](https://kramdown.gettalong.org/)이고, 다른 하나는 GitHub 전체에서 [GitHub Flavored Markdown(GFM)](https://github.github.com/gfm/)을 렌더링하는 데 쓰는 GitHub 자체 Markdown 프로세서입니다. 자세한 내용은 [GitHub에서 글 쓰기와 서식 지정하기](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/about-writing-and-formatting-on-github)를 참고하세요.

두 프로세서 모두에서 GitHub Flavored Markdown을 사용할 수 있습니다.

1. GitHub에서 사이트 저장소로 이동합니다.
2. 저장소에서 `_config.yml`{: .filepath} 파일로 이동합니다.
3. 파일 화면 오른쪽 위의 연필 아이콘을 클릭해 파일 편집기를 엽니다.

   ![파일 화면 상단. 연필 아이콘 버튼이 강조되어 있음](/assets/img/posts/edit-file-edit-button.png){: .shadow w='703' h='224' }

   > 기본 파일 편집기 대신, 아래쪽 화살표 드롭다운 메뉴에서 **github.dev**를 클릭해 [github.dev 코드 편집기](https://docs.github.com/en/codespaces/the-githubdev-web-based-editor)를 사용할 수도 있습니다. **GitHub Desktop**을 클릭해 저장소를 클론하고 GitHub Desktop에서 로컬로 파일을 수정할 수도 있습니다.
   {: .prompt-info }

   ![파일 화면 상단. 아래쪽 화살표 아이콘이 강조되어 있음](/assets/img/posts/edit-file-edit-dropdown.png){: .shadow w='703' h='117' }

4. `markdown:`으로 시작하는 줄을 찾아 값을 `kramdown` 또는 `GFM`으로 바꿉니다. 완성된 줄은 `markdown: kramdown` 또는 `markdown: GFM`이어야 합니다.
5. **Commit changes...**를 클릭합니다.
6. "Commit message" 칸에 파일에 어떤 변경을 했는지 설명하는 짧고 의미 있는 커밋 메시지를 입력합니다. 커밋 메시지에서 여러 작성자를 커밋에 표시할 수도 있습니다. 자세한 내용은 [여러 작성자가 있는 커밋 만들기](https://docs.github.com/en/pull-requests/how-tos/commit-changes/creating-a-commit-with-multiple-authors)를 참고하세요.
7. GitHub 계정에 이메일 주소가 여러 개 연결되어 있다면, 이메일 주소 드롭다운 메뉴를 클릭해 Git 작성자 이메일로 쓸 주소를 선택합니다. 이 메뉴에는 인증된 이메일 주소만 나타납니다. 이메일 주소 비공개 설정을 켰다면 no-reply 주소가 기본 커밋 작성자 이메일이 됩니다.

   ![커밋 작성자 이메일을 고르는 드롭다운 메뉴. octocat@github.com이 선택되어 있음](/assets/img/posts/choose-commit-email-address.png){: .shadow w='643' h='234' }

8. 커밋 메시지 입력란 아래에서 커밋을 현재 브랜치에 추가할지, 새 브랜치에 추가할지 정합니다. 현재 브랜치가 기본 브랜치라면 커밋용 새 브랜치를 만든 뒤 풀 리퀘스트를 만드는 것이 좋습니다. 자세한 내용은 [풀 리퀘스트 만들기](https://docs.github.com/en/pull-requests/how-tos/create-pull-requests/creating-a-pull-request)를 참고하세요.

   ![main 브랜치에 바로 커밋할지 새 브랜치를 만들지 고르는 라디오 버튼. 새 브랜치가 선택되어 있음](/assets/img/posts/choose-commit-branch.png){: .shadow w='669' h='166' }

9. **Commit changes** 또는 **Propose changes**를 클릭합니다.

## 더 읽어보기

- [kramdown 문서](https://kramdown.gettalong.org/documentation.html)
- [GitHub Flavored Markdown 명세](https://github.github.com/gfm/)

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/setting-a-markdown-processor-for-your-github-pages-site-using-jekyll)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
