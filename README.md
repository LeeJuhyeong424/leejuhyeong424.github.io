# 쭈꾸미블로그

각종 개발 관련 메모와 기록을 남기는 아카이빙 블로그입니다.

🔗 **https://leejuhyeong.pe.kr**

---

## 사용 기술

- [Jekyll](https://jekyllrb.com/) 정적 사이트 생성기
- [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy/) 테마 ([chirpy-starter](https://github.com/cotes2020/chirpy-starter) 기반)
- GitHub Pages + GitHub Actions 자동 배포

## 폴더 구조

```
.
├── _config.yml        # 사이트 설정
├── _posts/            # 게시글 (YYYY-MM-DD-제목.md)
├── _tabs/             # 사이드바 탭 (About, Archives, Categories, Tags)
├── _data/             # 연락처 아이콘 등 데이터
├── _plugins/          # 커스텀 플러그인
├── assets/            # 이미지 등 정적 파일
├── index.html         # 홈 화면
└── .github/workflows/ # 빌드·배포 워크플로
```

## 글 작성 방법

`_posts` 폴더에 `YYYY-MM-DD-제목.md` 파일을 만들고 맨 위에 아래 내용을 넣습니다.

```markdown
---
title: 글 제목
date: 2026-10-10 12:00:00 +0900
categories: [상위카테고리, 하위카테고리]
tags: [태그1, 태그2]
---

본문을 마크다운으로 작성합니다.
```

`main` 브랜치에 push하면 GitHub Actions가 자동으로 빌드하고 배포합니다.

## 로컬에서 실행

```bash
bundle install
bundle exec jekyll serve
```

브라우저에서 `http://127.0.0.1:4000`으로 확인할 수 있습니다.

## 라이선스

이 저장소는 [MIT License](LICENSE)를 따르며, 테마 원저작권은 [Cotes Chung](https://github.com/cotes2020)에게 있습니다.
