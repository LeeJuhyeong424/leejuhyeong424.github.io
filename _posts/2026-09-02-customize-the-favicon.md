---
title: 파비콘 커스터마이징하기
date: 2026-09-02 01:20:00 +0900
categories: [블로그, 튜토리얼]
tags: [favicon]
---

[**Chirpy**](https://github.com/cotes2020/jekyll-theme-chirpy/)의 [파비콘](https://www.favicon-generator.org/about/)은 `assets/img/favicons/`{: .filepath} 디렉터리에 들어 있습니다. 이 파비콘을 내 것으로 바꾸고 싶다면, 아래 안내에 따라 파비콘을 만들고 기본 파비콘을 교체하면 됩니다.

## 파비콘 만들기

512x512 이상 크기의 정사각형 이미지(PNG, JPG 또는 SVG)를 준비한 뒤, 온라인 도구 [**Real Favicon Generator**](https://realfavicongenerator.net/)에 접속해 <kbd>Pick your favicon image</kbd> 버튼을 클릭하고 이미지 파일을 업로드합니다.

다음 단계에서는 파비콘이 쓰이는 모든 사용 환경이 표시됩니다. 기본 옵션을 그대로 두고 페이지 맨 아래로 스크롤한 뒤 <kbd>Next →</kbd> 버튼을 클릭하면 파비콘이 생성됩니다.

## 다운로드 및 교체

생성된 패키지를 다운로드해 압축을 풀고, 압축을 푼 파일 중 아래 파일을 삭제합니다.

- `site.webmanifest`{: .filepath}

그런 다음 나머지 이미지 파일(`.PNG`{: .filepath}, `.ICO`{: .filepath}, `.SVG`{: .filepath})을 Jekyll 사이트의 `assets/img/favicons/`{: .filepath} 디렉터리에 복사해 기존 파일을 덮어씁니다. 아직 이 디렉터리가 없다면 새로 만들면 됩니다.

아래 표는 파비콘 파일이 어떻게 바뀌는지 정리한 것입니다.

| 파일 | 온라인 도구에서 받은 파일 | Chirpy 기본 파일 |
| ---- | :----------------------: | :--------------: |
| `*.PNG` |            ✓            |        ✗         |
| `*.ICO` |            ✓            |        ✗         |
| `*.SVG` |            ✓            |        ✗         |


<!-- markdownlint-disable-next-line -->
>  ✓는 유지, ✗는 삭제를 의미합니다.
{: .prompt-info }

다음에 사이트를 빌드하면 파비콘이 내가 만든 것으로 교체됩니다.

---
