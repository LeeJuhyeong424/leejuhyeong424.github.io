---
title: GitHub Pages에서 사용자 지정 워크플로 사용하기
description: >-
  워크플로 파일을 직접 만들거나 미리 정의된 워크플로를 골라
  GitHub Actions와 GitHub Pages를 함께 활용할 수 있습니다.
date: 2026-10-10 14:40:00 +0900
categories: [GitHub Pages, 시작하기]
tags: [github-pages, github-actions]
render_with_liquid: false
---

## 사용자 지정 워크플로 소개

사용자 지정 워크플로를 사용하면 GitHub Actions로 GitHub Pages 사이트를 빌드할 수 있습니다. 사용할 브랜치는 여전히 워크플로 파일에서 고를 수 있으며, 그 밖에도 훨씬 많은 일을 할 수 있습니다. 사용자 지정 워크플로를 쓰려면 먼저 현재 저장소에서 활성화해야 합니다. 자세한 내용은 [사용자 지정 GitHub Actions 워크플로로 게시하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow)를 참고하세요.

## `configure-pages` 액션 설정하기

GitHub Actions에서는 `configure-pages` 액션으로 GitHub Pages를 사용할 수 있으며, 이 액션으로 웹사이트에 대한 여러 메타데이터도 가져올 수 있습니다. 자세한 내용은 [`configure-pages`](https://github.com/marketplace/actions/configure-github-pages) 액션을 참고하세요.

이 액션을 사용하려면 원하는 워크플로의 `jobs` 아래에 다음 코드를 넣습니다.

```yaml
- name: Configure GitHub Pages
  uses: actions/configure-pages@v5
```

이 액션은 어떤 정적 사이트 생성기에서든 GitHub Pages로 배포할 수 있도록 도와줍니다. 이 과정을 덜 반복적으로 만들기 위해, 널리 쓰이는 정적 사이트 생성기 일부에 대해서는 워크플로 템플릿을 사용할 수 있습니다. 자세한 내용은 [워크플로 템플릿 사용하기](https://docs.github.com/en/actions/how-tos/write-workflows/use-workflow-templates)를 참고하세요.

## `upload-pages-artifact` 액션 설정하기

`upload-pages-artifact` 액션은 아티팩트를 패키징하고 업로드해 줍니다. GitHub Pages 아티팩트는 `tar` 파일 하나를 담은 `gzip` 압축 파일이어야 합니다. `tar` 파일은 10GB 미만이어야 하며, 심볼릭 링크나 하드 링크를 포함해서는 안 됩니다. 자세한 내용은 [`upload-pages-artifact`](https://github.com/marketplace/actions/upload-github-pages-artifact) 액션을 참고하세요.

현재 워크플로에서 이 액션을 사용하려면 `jobs` 아래에 다음 코드를 넣습니다.

```yaml
- name: Upload GitHub Pages artifact
  uses: actions/upload-pages-artifact@v4
```

## GitHub Pages 아티팩트 배포하기

`deploy-pages` 액션은 아티팩트를 배포하는 데 필요한 설정을 처리합니다. 제대로 동작하려면 다음 조건을 갖춰야 합니다.

- 잡(job)에 최소한 `pages: write`와 `id-token: write` 권한이 있어야 합니다.
- `needs` 파라미터를 빌드 단계의 `id`로 설정해야 합니다. 이 파라미터를 설정하지 않으면, 아직 만들어지지 않은 아티팩트를 계속 찾는 독립적인 배포가 실행될 수 있습니다.
- 브랜치·배포 보호 규칙을 적용하려면 `environment`를 지정해야 합니다. 기본 환경은 `github-pages`입니다.
- 페이지의 URL을 출력값으로 지정하려면 `url:` 필드를 사용합니다.

자세한 내용은 [`deploy-pages`](https://github.com/marketplace/actions/deploy-github-pages-site) 액션을 참고하세요.

```yaml
# ...

jobs:
  deploy:
    permissions:
      contents: read
      pages: write
      id-token: write
    runs-on: ubuntu-latest
    needs: jekyll-build
    environment:
      name: github-pages
      url: ${{steps.deployment.outputs.page_url}}
    steps:
      - name: Deploy artifact
        id: deployment
        uses: actions/deploy-pages@v4
# ...
```

## 빌드 잡과 배포 잡 연결하기

`build` 잡과 `deploy` 잡을 하나의 워크플로 파일 안에서 연결할 수 있으므로, 같은 결과를 얻으려고 파일을 두 개 만들 필요가 없습니다. 워크플로 파일을 시작하려면 `jobs` 아래에 `build`와 `deploy` 잡을 정의하면 됩니다.

```yaml
# ...

jobs:
  # 빌드 잡
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v5
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5
      - name: Build with Jekyll
        uses: actions/jekyll-build-pages@v1
        with:
          source: ./
          destination: ./_site
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v4

  # 배포 잡
  deploy:
    environment:
      name: github-pages
      url: ${{steps.deployment.outputs.page_url}}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
# ...
```

빌드 과정이 필요 없는 경우처럼, 모든 것을 하나의 잡으로 합치는 편이 나을 때도 있습니다. 이때는 배포 단계에만 집중하면 됩니다.

```yaml
# ...

jobs:
  # 빌드 없이 배포만 하는 단일 잡
  deploy:
    environment:
      name: github-pages
      url: ${{steps.deployment.outputs.page_url}}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v5
      - name: Setup Pages
        uses: actions/configure-pages@v5
      - name: Upload Artifact
        uses: actions/upload-pages-artifact@v4
        with:
          # 디렉터리 전체 업로드
          path: '.'
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4

# ...
```

잡을 서로 다른 러너에서, 순서대로, 또는 동시에 실행하도록 정의할 수 있습니다. 자세한 내용은 [워크플로가 할 일 정하기](https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do)를 참고하세요.

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
