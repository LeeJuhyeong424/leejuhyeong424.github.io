---
title: 사용자 지정 도메인 확인하기
description: >-
  사용자 지정 도메인을 인증하면 다른 GitHub 사용자가 내 도메인을 탈취해
  자기 GitHub Pages 사이트를 게시하는 것을 막을 수 있습니다.
date: 2026-10-27 00:00:00 +0900
categories: [GitHub Pages, 사용자 지정 도메인]
tags: [github-pages, custom-domain]
---

## GitHub Pages의 도메인 인증

개인 계정에서 사용자 지정 도메인을 인증하면, 내 개인 계정이 소유한 저장소만 그 인증된 도메인이나 바로 아래 서브도메인에 GitHub Pages 사이트를 게시할 수 있습니다. 마찬가지로 조직에서 사용자 지정 도메인을 인증하면, 그 조직이 소유한 저장소만 인증된 도메인이나 바로 아래 서브도메인에 GitHub Pages 사이트를 게시할 수 있습니다.

도메인을 인증하면 다른 GitHub 사용자가 내 사용자 지정 도메인을 탈취해 자기 GitHub Pages 사이트를 게시하는 것을 막을 수 있습니다. 도메인 탈취는 저장소를 삭제했을 때, 요금제가 낮아졌을 때, 또는 도메인이 GitHub Pages용으로 설정되어 있고 인증되지 않은 상태에서 사용자 지정 도메인 연결이 끊기거나 GitHub Pages가 꺼지는 다른 변경이 생겼을 때 일어날 수 있습니다.

도메인을 인증하면 바로 아래의 서브도메인도 함께 인증됩니다. 예를 들어 `github.com` 사용자 지정 도메인을 인증하면 `docs.github.com`, `support.github.com` 등 바로 아래의 모든 서브도메인도 탈취로부터 보호됩니다.

> `*.example.com` 같은 와일드카드 DNS 레코드는 사용하지 않기를 강력히 권장합니다. 도메인을 인증하더라도 이런 레코드는 곧바로 도메인 탈취 위험을 만듭니다. 예를 들어 `example.com`을 인증하면 다른 사람이 `a.example.com`을 쓰지는 못하지만, 와일드카드 DNS 레코드가 적용되는 `b.a.example.com`은 여전히 탈취할 수 있습니다.
{: .prompt-warning }

조직에서 도메인을 인증할 수도 있으며, 그러면 조직 프로필에 "Verified" 배지가 표시됩니다. 자세한 내용은 [조직의 도메인 인증 또는 승인하기](https://docs.github.com/en/organizations/managing-organization-settings/verifying-or-approving-a-domain-for-your-organization)를 참고하세요.

### 이미 다른 곳에서 쓰는 도메인 인증하기

내가 소유한 도메인을 다른 사용자나 조직이 사용하고 있을 때, 내 GitHub Pages 웹사이트에서 쓰려고 그 도메인을 인증할 수 있습니다. 이 경우 다른 사용자나 조직이 소유한 GitHub Pages 웹사이트에서 그 도메인이 즉시 해제됩니다. 다만 이미 다른 사용자나 조직이 인증한 도메인을 인증하려고 하면 해제 과정이 성공하지 않습니다.

## 사용자 사이트의 도메인 인증하기

> 아래 설명한 옵션이 보이지 않는다면 저장소 설정이 아니라 **프로필 설정**에 있는지 확인하세요. 도메인 인증은 프로필 단위에서 이루어집니다.
{: .prompt-info }

1. GitHub 아무 페이지에서나 오른쪽 위의 프로필 사진을 클릭한 다음 **Settings**를 클릭합니다.
2. 사이드바의 "Code, planning, and automation" 아래에서 **Pages**를 클릭합니다.
3. 오른쪽에서 **Add a domain**을 클릭합니다.
4. "What domain would you like to add?" 아래에 인증하려는 도메인을 입력하고 **Add domain**을 선택합니다.

   ![인증할 도메인을 입력하는 칸. 아래에 초록색 "Add domain" 버튼이 있음](/assets/img/posts/verify-enter-domain.png){: .shadow w='732' h='140' }

5. "Add a DNS TXT record" 아래의 안내에 따라 도메인 호스팅 서비스에서 TXT 레코드를 만듭니다.

   ![example.com의 DNS 설정에 TXT 레코드를 추가하라는 GitHub Pages 안내](/assets/img/posts/verify-dns.png){: .shadow w='800' h='345' }

6. DNS 설정이 바뀔 때까지 기다립니다. 바로 적용될 수도 있고, 최대 24시간이 걸릴 수도 있습니다. 명령줄에서 `dig` 명령을 실행해 DNS 설정이 바뀌었는지 확인할 수 있습니다. 아래 명령에서 `USERNAME`은 내 사용자명으로, `example.com`은 인증하려는 도메인으로 바꿉니다. DNS 설정이 반영되었다면 출력에 새 TXT 레코드가 보입니다.

   ```text
   dig _github-pages-challenge-USERNAME.example.com +nostats +nocomments +nocmd TXT
   ```

7. DNS 설정이 반영된 것을 확인했다면 도메인을 인증할 수 있습니다. 바로 반영되지 않아 이전 페이지를 벗어났다면, 앞의 몇 단계를 다시 따라 Pages 설정으로 돌아간 뒤 도메인 오른쪽의 <kbd>···</kbd>를 클릭하고 **Continue verifying**을 클릭합니다.

   ![인증된 도메인 설정. 오른쪽 메뉴에서 "Continue verifying" 항목이 강조되어 있음](/assets/img/posts/verify-continue.png){: .shadow w='831' h='206' }

8. 도메인을 인증하려면 **Verify**를 클릭합니다.
9. 사용자 지정 도메인의 인증 상태를 유지하려면 도메인 DNS 설정에 TXT 레코드를 그대로 남겨 두세요.

## 조직 사이트의 도메인 인증하기

조직 소유자는 조직의 사용자 지정 도메인을 인증할 수 있습니다.

> 아래 설명한 옵션이 보이지 않는다면 **조직 설정**에 있는지 확인하세요. 도메인 인증은 저장소 설정에서 하지 않습니다.
{: .prompt-info }

1. GitHub 오른쪽 위의 프로필 사진을 클릭한 다음 **Organizations**를 클릭합니다.
2. 조직을 클릭해 선택합니다.
3. 조직 이름 아래에서 **Settings**를 클릭합니다. "Settings" 탭이 보이지 않으면 <kbd>···</kbd> 드롭다운 메뉴를 선택한 다음 **Settings**를 클릭합니다.

   ![조직 프로필의 탭. "Settings" 탭이 강조되어 있음](/assets/img/posts/org-settings-global-nav-update.png){: .shadow w='962' h='71' }

4. 사이드바의 "Code, planning, and automation" 아래에서 **Pages**를 클릭합니다.
5. 오른쪽에서 **Add a domain**을 클릭합니다.
6. "What domain would you like to add?" 아래에 인증하려는 도메인을 입력하고 **Add domain**을 선택합니다.
7. "Add a DNS TXT record" 아래의 안내에 따라 도메인 호스팅 서비스에서 TXT 레코드를 만듭니다.
8. DNS 설정이 바뀔 때까지 기다립니다. 바로 적용될 수도 있고, 최대 24시간이 걸릴 수도 있습니다. 아래 명령에서 `ORGANIZATION`은 조직 이름으로, `example.com`은 인증하려는 도메인으로 바꿉니다. DNS 설정이 반영되었다면 출력에 새 TXT 레코드가 보입니다.

   ```text
   dig _github-pages-challenge-ORGANIZATION.example.com +nostats +nocomments +nocmd TXT
   ```

9. DNS 설정이 반영된 것을 확인했다면 도메인을 인증할 수 있습니다. 이전 페이지를 벗어났다면 Pages 설정으로 돌아가 도메인 오른쪽의 <kbd>···</kbd>를 클릭하고 **Continue verifying**을 클릭합니다.
10. 도메인을 인증하려면 **Verify**를 클릭합니다.
11. 사용자 지정 도메인의 인증 상태를 유지하려면 도메인 DNS 설정에 TXT 레코드를 그대로 남겨 두세요.

---

> 이 글은 GitHub Docs의 [원문](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)을 한국어로 번역하고 일부 표현을 다듬은 것입니다. 원문은 GitHub, Inc.의 문서이며 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스를 따릅니다.
{: .prompt-tip }
