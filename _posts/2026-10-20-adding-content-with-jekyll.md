---
title: Jekyll로 사이트에 콘텐츠 추가하기
description: GitHub Pages의 Jekyll 사이트에 새 페이지나 글을 추가할 수 있습니다.
date: 2026-10-20 00:00:00 +0900
categories: [GitHub Pages, Jekyll]
tags: [github-pages, jekyll]
---

> `github-pages` gem은 일부 워크플로에서 여전히 지원되지만, 이제는 GitHub Actions로 GitHub Pages 사이트를 배포하고 자동화하는 방식이 권장됩니다.
{: .prompt-info }

> 저장소 쓰기 권한이 있는 사람이 Jekyll을 사용해 GitHub Pages 사이트에 콘텐츠를 추가할 수 있습니다.
{: .prompt-info }

## Jekyll 사이트의 콘텐츠

GitHub Pages의 Jekyll 사이트에 콘텐츠를 추가하려면 먼저 Jekyll 사이트를 만들어야 합니다. 자세한 내용은 [Jekyll로 GitHub Pages 사이트 만들기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)를 참고하세요.

Jekyll 사이트의 주요 콘텐츠는 페이지와 글입니다. 페이지는 "About" 페이지처럼 특정 날짜와 관련 없는 독립적인 콘텐츠입니다. 기본 Jekyll 사이트에는 `about.md`라는 파일이 있으며, 사이트에서 `YOUR-SITE-URL/about` 주소의 페이지로 표시됩니다. 이 파일 내용을 수정해 "About" 페이지를 꾸밀 수 있고, "About" 페이지를 템플릿 삼아 새 페이지를 만들 수도 있습니다. 자세한 내용은 Jekyll 문서의 [Pages](https://jekyllrb.com/docs/pages/)를 참고하세요.

글은 블로그 게시물입니다. 기본 Jekyll 사이트에는 `_posts`라는 디렉터리가 있고, 그 안에 기본 글 파일이 들어 있습니다. 이 글의 내용을 수정할 수 있고, 기본 글을 템플릿 삼아 새 글을 만들 수도 있습니다. 자세한 내용은 Jekyll 문서의 [Posts](https://jekyllrb.com/docs/posts/)를 참고하세요.

테마에는 사이트의 새 페이지와 글에 자동으로 적용되는 기본 레이아웃과 스타일시트가 들어 있지만, 이 기본값은 무엇이든 덮어쓸 수 있습니다. 자세한 내용은 [GitHub Pages와 Jekyll: 테마](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll#themes)를 참고하세요.

사이트의 페이지나 글에 제목, 레이아웃 같은 변수와 메타데이터를 지정하려면 Markdown 또는 HTML 파일 맨 위에 YAML front matter를 추가합니다. 자세한 내용은 Jekyll 문서의 [Front Matter](https://jekyllrb.com/docs/front-matter/)를 참고하세요.

브랜치에서 게시한다면, 변경 사항이 사이트의 게시 원본에 병합될 때 자동으로 게시됩니다. 사용자 지정 GitHub Actions 워크플로로 게시한다면, 워크플로가 실행될 때마다(보통 기본 브랜치에 push할 때) 변경 사항이 게시됩니다. 변경 사항을 먼저 미리 보고 싶다면 GitHub가 아니라 로컬에서 변경한 뒤 사이트를 로컬에서 테스트하세요. 자세한 내용은 [Jekyll로 로컬에서 GitHub Pages 사이트 테스트하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)를 참고하세요.

## 사이트에 새 페이지 추가하기

1. GitHub에서 사이트 저장소로 이동합니다.
2. 사이트의 게시 원본으로 이동합니다. 자세한 내용은 [GitHub Pages 사이트의 게시 원본 구성하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)를 참고하세요.
3. 게시 원본의 루트에 페이지용 새 파일 `PAGE-NAME.md`를 만듭니다. PAGE-NAME은 페이지를 잘 나타내는 파일 이름으로 바꿉니다.
4. 파일 맨 위에 다음 YAML front matter를 추가합니다. PAGE-TITLE은 페이지 제목으로, URL-PATH는 페이지 URL에 쓸 경로로 바꿉니다. 예를 들어 사이트의 기본 URL이 `https://octocat.github.io`이고 URL-PATH가 `/about/contact/`라면, 페이지 주소는 `https://octocat.github.io/about/contact`가 됩니다.

   ```shell
   layout: page
   title: "PAGE-TITLE"
   permalink: /URL-PATH
   ```

5. front matter 아래에 페이지 내용을 추가합니다.
6. **Commit changes...**를 클릭합니다.
7. "Commit message" 칸에 파일에 어떤 변경을 했는지 설명하는 짧고 의미 있는 커밋 메시지를 입력합니다. 커밋 메시지에서 여러 작성자를 커밋에 표시할 수도 있습니다. 자세한 내용은 [여러 작성자가 있는 커밋 만들기](https://docs.github.com/en/pull-requests/how-tos/commit-changes/creating-a-commit-with-multiple-authors)를 참고하세요.
8. GitHub 계정에 이메일 주소가 여러 개 연결되어 있다면, 이메일 주소 드롭다운 메뉴를 클릭해 Git 작성자 이메일로 쓸 주소를 선택합니다. 이 메뉴에는 인증된 이메일 주소만 나타납니다. 이메일 주소 비공개 설정을 켰다면 no-reply 주소가 기본 커밋 작성자 이메일이 됩니다. no-reply 이메일 주소의 정확한 형식은 [커밋 이메일 주소 설정하기](https://docs.github.com/en/account-and-profile/how-tos/email-preferences/setting-your-commit-email-address)를 참고하세요.

   ![커밋 작성자 이메일을 고르는 드롭다운 메뉴. octocat@github.com이 선택되어 있음](/assets/img/posts/choose-commit-email-address.png){: .shadow w='643' h='234' }

9. 커밋 메시지 입력란 아래에서 커밋을 현재 브랜치에 추가할지, 새 브랜치에 추가할지 정합니다. 현재 브랜치가 기본 브랜치라면 커밋용 새 브랜치를 만든 뒤 풀 리퀘스트를 만드는 것이 좋습니다. 자세한 내용은 [풀 리퀘스트 만들기](https://docs.github.com/en/pull-requests/how-tos/create-pull-requests/creating-a-pull-request)를 참고하세요.

   ![main 브랜치에 바로 커밋할지 새 브랜치를 만들지 고르는 라디오 버튼. 새 브랜치가 선택되어 있음](/assets/img/posts/choose-commit-branch.png){: .shadow w='669' h='166' }

10. **Commit changes** 또는 **Propose changes**를 클릭합니다.
11. 제안한 변경 사항으로 풀 리퀘스트를 만듭니다.
12. "Pull Requests" 목록에서 병합하려는 풀 리퀘스트를 클릭합니다.
13. **Merge pull request**를 클릭합니다. 자세한 내용은 [풀 리퀘스트 병합하기](https://docs.github.com/en/pull-requests/how-tos/merge-and-close-pull-requests/merging-a-pull-request)를 참고하세요.
14. 요청이 나오면 커밋 메시지를 입력하거나 기본 메시지를 그대로 사용합니다.
15. **Confirm merge**를 클릭합니다.
16. 필요하다면 브랜치를 삭제합니다. 자세한 내용은 [저장소 안에서 브랜치 관리하기](https://docs.github.com/en/pull-requests/how-tos/commit-changes/managing-branches-within-your-repository)를 참고하세요.

## 사이트에 새 글 추가하기

1. GitHub에서 사이트 저장소로 이동합니다.
2. 사이트의 게시 원본으로 이동합니다. 자세한 내용은 [GitHub Pages 사이트의 게시 원본 구성하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)를 참고하세요.
3. `_posts` 디렉터리로 이동합니다.
4. `YYYY-MM-DD-NAME-OF-POST.md`라는 새 파일을 만듭니다. YYYY-MM-DD는 글의 날짜로, NAME-OF-POST는 글 이름으로 바꿉니다.
5. 파일 맨 위에 다음 YAML front matter를 추가합니다. 따옴표로 감싼 글 제목, YYYY-MM-DD hh:mm:ss -0000 형식의 날짜와 시간, 그리고 원하는 만큼의 카테고리를 넣습니다.

   ```shell
   layout: post
   title: "POST-TITLE"
   date: YYYY-MM-DD hh:mm:ss -0000
   categories: CATEGORY-1 CATEGORY-2
   ```

6. front matter 아래에 글 내용을 추가합니다.
7. **Commit changes...**를 클릭합니다.
8. "Commit message" 칸에 파일에 어떤 변경을 했는지 설명하는 짧고 의미 있는 커밋 메시지를 입력합니다. 커밋 메시지에서 여러 작성자를 커밋에 표시할 수도 있습니다.
9. GitHub 계정에 이메일 주소가 여러 개 연결되어 있다면, 이메일 주소 드롭다운 메뉴를 클릭해 Git 작성자 이메일로 쓸 주소를 선택합니다.
10. 커밋 메시지 입력란 아래에서 커밋을 현재 브랜치에 추가할지, 새 브랜치에 추가할지 정합니다. 현재 브랜치가 기본 브랜치라면 커밋용 새 브랜치를 만든 뒤 풀 리퀘스트를 만드는 것이 좋습니다.
11. **Commit changes** 또는 **Propose changes**를 클릭합니다.
12. 제안한 변경 사항으로 풀 리퀘스트를 만듭니다.
13. "Pull Requests" 목록에서 병합하려는 풀 리퀘스트를 클릭합니다.
14. **Merge pull request**를 클릭합니다.
15. 요청이 나오면 커밋 메시지를 입력하거나 기본 메시지를 그대로 사용합니다.
16. **Confirm merge**를 클릭합니다.
17. 필요하다면 브랜치를 삭제합니다.

이제 사이트에 글이 올라갔을 것입니다. 사이트의 기본 URL이 `https://octocat.github.io`라면 새 글은 `https://octocat.github.io/YYYY/MM/DD/TITLE.html`에서 볼 수 있습니다.

## 다음 단계

GitHub Pages 사이트에 Jekyll 테마를 추가해 사이트의 모양과 분위기를 바꿀 수 있습니다. 자세한 내용은 [Jekyll로 GitHub Pages 사이트에 테마 추가하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll)를 참고하세요.

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-content-to-your-github-pages-site-using-jekyll)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
