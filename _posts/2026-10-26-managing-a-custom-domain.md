---
title: 사용자 지정 도메인 관리하기
description: GitHub Pages 사이트의 사용자 지정 도메인을 설정하거나 수정할 수 있습니다.
date: 2026-10-26 00:00:00 +0900
categories: [GitHub Pages, 사용자 지정 도메인]
tags: [github-pages, custom-domain, dns]
---

> 저장소 관리자(admin) 권한이 있는 사람이 GitHub Pages 사이트의 사용자 지정 도메인을 설정할 수 있습니다.
{: .prompt-info }

## 사용자 지정 도메인 설정 알아보기

> 보안을 높이고 도메인 탈취 공격을 막기 위해, 저장소에 사용자 지정 도메인을 추가하기 전에 도메인을 먼저 인증하는 것을 권장합니다. 자세한 내용은 [GitHub Pages의 사용자 지정 도메인 확인하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)를 참고하세요.
{: .prompt-tip }

DNS 제공업체에서 사용자 지정 도메인을 설정하기 **전에** 먼저 GitHub Pages 사이트에 사용자 지정 도메인을 추가하세요. GitHub에 사용자 지정 도메인을 추가하지 않은 채 DNS 제공업체에서 먼저 설정하면, 다른 사람이 내 서브도메인 중 하나에 사이트를 호스팅할 수 있게 될 수 있습니다.

> **Windows**: DNS 레코드가 올바르게 설정되었는지 확인할 때 쓰는 `dig` 명령은 Windows에 기본으로 들어 있지 않습니다. DNS 레코드가 올바르게 설정되었는지 확인하려면 PowerShell의 `Resolve-DnsName` 명령을 사용하거나 [BIND](https://www.isc.org/bind/)를 설치하세요.
{: .prompt-tip }

> DNS 변경 사항이 전파되기까지 최대 24시간이 걸릴 수 있습니다.
{: .prompt-info }

## 에이펙스 도메인 설정하기

`example.com` 같은 에이펙스 도메인을 설정하려면, 저장소 설정에서 사용자 지정 도메인을 지정하고 DNS 제공업체에서 `ALIAS`, `ANAME`, `A` 레코드를 하나 이상 만들어야 합니다.

1. GitHub에서 사이트 저장소로 이동합니다.
2. 저장소 이름 아래에서 **Settings**를 클릭합니다. "Settings" 탭이 보이지 않으면 <kbd>···</kbd> 드롭다운 메뉴를 선택한 다음 **Settings**를 클릭합니다.

   ![저장소 상단 탭. "Settings" 탭이 강조되어 있음](/assets/img/posts/repo-actions-settings.png){: .shadow w='1098' h='108' }

3. 사이드바의 "Code, planning, and automation" 섹션에서 **Pages**를 클릭합니다.
4. "Custom domain" 아래에 사용자 지정 도메인을 입력하고 **Save**를 클릭합니다. 브랜치에서 사이트를 게시한다면, 원본 브랜치 루트에 `CNAME` 파일을 추가하는 커밋이 만들어집니다. 사용자 지정 GitHub Actions 워크플로로 게시한다면 `CNAME` 파일은 만들어지지 않으며, 기존 `CNAME` 파일이 있어도 무시되고 필요하지 않습니다. 게시 원본에 대한 자세한 내용은 [GitHub Pages 사이트의 게시 원본 구성하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)를 참고하세요.
5. DNS 제공업체로 가서 `ALIAS`, `ANAME`, `A` 레코드 중 하나를 만듭니다. IPv6를 지원하려면 `AAAA` 레코드도 만들 수 있습니다. IPv6를 지원하더라도 전 세계적으로 IPv6 보급이 느리므로 `AAAA` 레코드와 함께 `A` 레코드도 쓰는 것을 강력히 권장합니다. 올바른 레코드를 만드는 방법은 DNS 제공업체의 문서를 참고하세요.
   - `ALIAS` 또는 `ANAME` 레코드를 만들려면, 에이펙스 도메인이 사이트의 기본 도메인을 가리키도록 합니다. 사이트의 기본 도메인에 대한 자세한 내용은 [GitHub Pages 사이트의 종류](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages#types-of-github-pages-sites)를 참고하세요.
   - `A` 레코드를 만들려면, 에이펙스 도메인이 GitHub Pages의 IP 주소를 가리키도록 합니다.

     ```shell
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```

   - `AAAA` 레코드를 만들려면, 에이펙스 도메인이 GitHub Pages의 IP 주소를 가리키도록 합니다.

     ```shell
     2606:50c0:8000::153
     2606:50c0:8001::153
     2606:50c0:8002::153
     2606:50c0:8003::153
     ```

   > DNS 제공업체가 기본 레코드를 자동으로 만들어 두었다면, 계속하기 전에 삭제하세요.
   {: .prompt-info }

   > `*.example.com` 같은 와일드카드 DNS 레코드는 사용하지 않기를 강력히 권장합니다. 도메인을 인증하더라도 이런 레코드는 곧바로 도메인 탈취 위험을 만듭니다. 예를 들어 `example.com`을 인증하면 다른 사람이 `a.example.com`을 쓰지는 못하지만, 와일드카드 DNS 레코드가 적용되는 `b.a.example.com`은 여전히 탈취할 수 있습니다.
   {: .prompt-warning }

6. 터미널을 엽니다. macOS와 Linux는 터미널, Windows는 Git Bash를 사용합니다.
7. DNS 레코드가 올바르게 설정되었는지 확인하려면 `dig` 명령을 사용합니다. _EXAMPLE.COM_ 은 에이펙스 도메인으로 바꿉니다. 결과가 위의 GitHub Pages IP 주소와 일치하는지 확인하세요.
   - `A` 레코드:

     ```shell
     $ dig EXAMPLE.COM +noall +answer -t A
     > EXAMPLE.COM    3600    IN A     185.199.108.153
     > EXAMPLE.COM    3600    IN A     185.199.109.153
     > EXAMPLE.COM    3600    IN A     185.199.110.153
     > EXAMPLE.COM    3600    IN A     185.199.111.153
     ```

   - `AAAA` 레코드:

     ```shell
     $ dig EXAMPLE.COM +noall +answer -t AAAA
     > EXAMPLE.COM     3600    IN AAAA     2606:50c0:8000::153
     > EXAMPLE.COM     3600    IN AAAA     2606:50c0:8001::153
     > EXAMPLE.COM     3600    IN AAAA     2606:50c0:8002::153
     > EXAMPLE.COM     3600    IN AAAA     2606:50c0:8003::153
     ```

8. 정적 사이트 생성기로 사이트를 로컬에서 빌드해 생성된 파일을 GitHub에 push한다면, CNAME 파일을 추가한 커밋을 로컬 저장소로 pull 하세요. 자세한 내용은 [사용자 지정 도메인 문제 해결: CNAME 오류](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/troubleshooting-custom-domains-and-github-pages#cname-errors)를 참고하세요.
9. 필요하다면 사이트에 HTTPS 암호화를 강제 적용하기 위해 **Enforce HTTPS**를 선택합니다. 이 옵션을 쓸 수 있게 되기까지 최대 24시간이 걸릴 수 있습니다. 자세한 내용은 [HTTPS로 GitHub Pages 사이트 보호하기](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)를 참고하세요.

### 에이펙스 도메인과 `www` 서브도메인 함께 설정하기

> HTTPS로 보호되는 웹사이트라면 에이펙스 도메인과 함께 `www` 서브도메인도 설정하는 것을 권장합니다.
{: .prompt-info }

에이펙스 도메인을 사용자 지정 도메인으로 쓴다면 `www` 서브도메인도 함께 설정하는 것을 권장합니다. DNS 제공업체에서 각 도메인 종류에 맞는 레코드를 올바르게 설정하면, GitHub Pages가 도메인 사이의 리디렉션을 자동으로 만들어 줍니다. 예를 들어 사이트의 사용자 지정 도메인을 `www.example.com`으로 설정하고 에이펙스 도메인과 `www` 도메인 모두에 GitHub Pages DNS 레코드를 설정했다면, `example.com`은 `www.example.com`으로 리디렉션됩니다. 반대로 `example.com`을 사용자 지정 도메인으로 설정했다면 `www.example.com`이 `example.com`으로 리디렉션됩니다. 자동 리디렉션은 다른 서브도메인에도 적용되어, `www.blog.example.com`은 `blog.example.com`으로(또는 그 반대로) 리디렉션됩니다. `www.www.`로 시작하는 도메인은 설정할 수 없습니다. 자세한 내용은 아래 "서브도메인 설정하기"를 참고하세요.

DNS 제공업체로 가서, `www` 서브도메인이 GitHub Pages 기본 도메인을 가리키는 `CNAME` 레코드를 만듭니다. 예를 들어 사이트가 `<user>.github.io`에 있다면 `www.example.com`이 `<user>.github.io`를 가리키는 `CNAME` 레코드를 만들어야 합니다. 마찬가지로 `<organization>.github.io`에 있는 조직 사이트라면 `www.example.com`이 `<organization>.github.io`를 가리키는 `CNAME` 레코드를 만들어야 합니다. `CNAME` 레코드는 저장소 이름 없이 `<user>.github.io` 또는 `<organization>.github.io`를 바로 가리켜야 합니다.

이 `CNAME` 레코드 값은 공개로 게시된 GitHub Pages 사이트와 비공개로 게시된 사이트 모두 같습니다. 비공개 게시는 GitHub Enterprise Cloud에서 사용할 수 있습니다.

올바른 레코드를 만드는 방법은 DNS 제공업체의 문서를 참고하세요. 사이트의 기본 도메인에 대한 자세한 내용은 [GitHub Pages 사이트의 종류](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages#types-of-github-pages-sites)를 참고하세요.

## 서브도메인 설정하기

`www.example.com`이나 `blog.example.com` 같은 `www` 또는 사용자 지정 서브도메인을 설정하려면, 저장소 설정에서 도메인을 추가한 뒤 DNS 제공업체에서 CNAME 레코드를 설정해야 합니다.

1. GitHub에서 사이트 저장소로 이동합니다.
2. 저장소 이름 아래에서 **Settings**를 클릭합니다. "Settings" 탭이 보이지 않으면 <kbd>···</kbd> 드롭다운 메뉴를 선택한 다음 **Settings**를 클릭합니다.
3. 사이드바의 "Code, planning, and automation" 섹션에서 **Pages**를 클릭합니다.
4. "Custom domain" 아래에 사용자 지정 도메인을 입력하고 **Save**를 클릭합니다. 브랜치에서 사이트를 게시한다면, 원본 브랜치 루트에 `CNAME` 파일을 추가하는 커밋이 만들어집니다. 사용자 지정 GitHub Actions 워크플로로 게시한다면 `CNAME` 파일은 만들어지지 않으며, 기존 `CNAME` 파일이 있어도 무시되고 필요하지 않습니다.

   > 사용자 지정 도메인이 국제화 도메인 이름(한글 도메인 등)이라면 Punycode로 인코딩한 버전을 입력해야 합니다. Punycode에 대한 자세한 내용은 [국제화 도메인 이름](https://en.wikipedia.org/wiki/Internationalized_domain_name)을 참고하세요.
   {: .prompt-info }

5. DNS 제공업체로 가서, 서브도메인이 사이트의 기본 도메인을 가리키는 `CNAME` 레코드를 만듭니다. 예를 들어 사용자 사이트에 `www.example.com` 서브도메인을 쓰려면 `www.example.com`이 `<user>.github.io`를 가리키는 `CNAME` 레코드를 만듭니다. 조직 사이트에 `another.example.com` 서브도메인을 쓰려면 `another.example.com`이 `<organization>.github.io`를 가리키는 `CNAME` 레코드를 만듭니다. `CNAME` 레코드는 저장소 이름을 뺀 `<user>.github.io` 또는 `<organization>.github.io`를 가리켜야 합니다. 올바른 레코드를 만드는 방법은 DNS 제공업체의 문서를 참고하세요.

   이 `CNAME` 레코드 값은 공개로 게시된 사이트와 비공개로 게시된 사이트 모두 같습니다. 저장소의 GitHub Pages 설정에 표시되는 고유한 `*.pages.github.io` 서브도메인을 `CNAME` 레코드가 가리키게 하지 마세요. 비공개 게시는 GitHub Enterprise Cloud에서 사용할 수 있습니다.

   > `*.example.com` 같은 와일드카드 DNS 레코드는 사용하지 않기를 강력히 권장합니다. 도메인을 인증하더라도 이런 레코드는 곧바로 도메인 탈취 위험을 만듭니다.
   {: .prompt-warning }

6. 터미널을 엽니다. macOS와 Linux는 터미널, Windows는 Git Bash를 사용합니다.
7. DNS 레코드가 올바르게 설정되었는지 확인하려면 `dig` 명령을 사용합니다. _WWW.EXAMPLE.COM_ 은 서브도메인으로 바꿉니다.

   ```shell
   $ dig WWW.EXAMPLE.COM +nostats +nocomments +nocmd
   > ;WWW.EXAMPLE.COM.                    IN      A
   > WWW.EXAMPLE.COM.             3592    IN      CNAME   YOUR-USERNAME.github.io.
   > YOUR-USERNAME.github.io.      43192   IN      CNAME   GITHUB-PAGES-SERVER .
   > GITHUB-PAGES-SERVER .         22      IN      A       192.0.2.1
   ```

8. 정적 사이트 생성기로 사이트를 로컬에서 빌드해 생성된 파일을 GitHub에 push한다면, CNAME 파일을 추가한 커밋을 로컬 저장소로 pull 하세요.
9. 필요하다면 사이트에 HTTPS 암호화를 강제 적용하기 위해 **Enforce HTTPS**를 선택합니다. 이 옵션을 쓸 수 있게 되기까지 최대 24시간이 걸릴 수 있습니다.

   > 사용자 지정 서브도메인이 에이펙스 도메인을 가리키게 하면, 웹사이트에 HTTPS를 강제 적용할 때 문제가 생기고 서브도메인이 GitHub Pages 사이트에 아예 연결되지 않을 수도 있습니다.
   {: .prompt-info }

## 사용자 지정 도메인용 DNS 레코드

GitHub Pages 사이트의 도메인 설정 과정에 익숙하다면, 아래 표에서 내 상황과 DNS 제공업체가 지원하는 레코드 종류에 맞는 DNS 값을 찾을 수 있습니다. GitHub에서 GitHub Pages 사이트를 설정하는 방법과 `dig` 명령으로 설정을 확인하는 방법은 위의 내용을 참고하세요.

에이펙스 도메인을 설정하려면 아래 표의 `A`와 `AAAA` 레코드를 모두 추가하거나, 대신 `ALIAS`/`ANAME` 레코드만 추가합니다. 에이펙스 도메인과 `www` 서브도메인(예: `example.com`과 `www.example.com`)을 함께 설정하려면 에이펙스 도메인을 먼저 설정한 다음 서브도메인을 설정합니다. 자세한 내용은 위의 "에이펙스 도메인과 `www` 서브도메인 함께 설정하기"를 참고하세요.

> `*.example.com` 같은 와일드카드 DNS 레코드는 사용하지 않기를 강력히 권장합니다. 도메인을 인증하더라도 이런 레코드는 곧바로 도메인 탈취 위험을 만듭니다.
{: .prompt-warning }

| 상황 | DNS 레코드 종류 | DNS 레코드 이름 | DNS 레코드 값 |
| --- | --- | --- | --- |
| 에이펙스 도메인<br />(`example.com`) | `A` | `@` | `185.199.108.153`<br />`185.199.109.153`<br />`185.199.110.153`<br />`185.199.111.153` |
| 에이펙스 도메인<br />(`example.com`) | `AAAA` | `@` | `2606:50c0:8000::153`<br />`2606:50c0:8001::153`<br />`2606:50c0:8002::153`<br />`2606:50c0:8003::153` |
| 에이펙스 도메인<br />(`example.com`) | `ALIAS` 또는 `ANAME` | `@` | `USERNAME.github.io` 또는<br />`ORGANIZATION.github.io` |
| 서브도메인<br />(`www.example.com`,<br />`blog.example.com`) | `CNAME` | `SUBDOMAIN.example.com.` | `USERNAME.github.io` 또는<br />`ORGANIZATION.github.io` |

## 사용자 지정 도메인 제거하기

사용자 지정 도메인이 이미 사용 중이라는 오류가 나면, 다른 저장소에서 사용자 지정 도메인을 제거해야 할 수 있습니다.

1. GitHub에서 사이트 저장소로 이동합니다.
2. 저장소 이름 아래에서 **Settings**를 클릭합니다. "Settings" 탭이 보이지 않으면 <kbd>···</kbd> 드롭다운 메뉴를 선택한 다음 **Settings**를 클릭합니다.
3. 사이드바의 "Code, planning, and automation" 섹션에서 **Pages**를 클릭합니다.
4. "Custom domain" 아래에서 **Remove**를 클릭합니다.

   ![사용자 지정 도메인 설정. "example.com" 입력란과 "Save" 버튼 오른쪽에 빨간 글씨의 "Remove" 버튼이 있음](/assets/img/posts/remove-custom-domain.png){: .shadow w='800' h='102' }

## 사용자 지정 도메인 보호하기

GitHub Pages 사이트가 비활성화되었는데 사용자 지정 도메인이 설정되어 있다면 도메인 탈취 위험이 있습니다. 사이트가 비활성화된 상태에서 DNS 제공업체에 사용자 지정 도메인이 설정되어 있으면, 다른 사람이 내 서브도메인 중 하나에 사이트를 호스팅할 수 있습니다.

사용자 지정 도메인을 인증하면 다른 GitHub 사용자가 자기 저장소에서 내 도메인을 사용하지 못하게 막을 수 있습니다. 도메인이 인증되지 않았는데 GitHub Pages 사이트가 비활성화되었다면, 즉시 DNS 제공업체에서 DNS 레코드를 수정하거나 삭제해야 합니다. 자세한 내용은 [GitHub Pages의 사용자 지정 도메인 확인하기](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)를 참고하세요.

## 더 읽어보기

- [사용자 지정 도메인과 GitHub Pages 문제 해결](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/troubleshooting-custom-domains-and-github-pages)

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
