# letsean.dev — 지원 사이트

앱 고객지원 페이지를 한 곳에 모은다. GitHub Pages 가 Jekyll 을 서버에서 빌드하므로
**푸시하면 그대로 배포된다**. 로컬에 Node·Ruby 를 깔 필요가 없다.

| 주소 | 내용 |
|---|---|
| `letsean.dev/` | 제품 목록 |
| `letsean.dev/kanaji/ja` · `/kanaji/ko` | 카나지 (일본어 키보드) |
| `letsean.dev/hankey/ko` · `/hankey/en` | 한글키 (한글 키보드) |
| `letsean.dev/fiveleaf/ko` · `/en` · `/ja` | 「다섯 글자」 (FiveLeaf) — **홈 목록에는 없다**, 아래 |
| `letsean.dev/fiveleaf/privacy/<언어>` | 그 앱의 개인정보 처리방침 |
| `letsean.dev/<제품>/` | 브라우저 언어에 맞는 쪽으로 보낸다 |

## ⚠️ 출시 전인 앱은 홈에 세우지 않는다

**「다섯 글자」(FiveLeaf)가 지금 그렇다.** 루트 `index.html` 의 `products` 에서
주석 처리해 뒀다 — App Store 에 없는 앱을 목록에서 고르게 하면 막다른 길이다.

**페이지 자체는 살아 있다.** `/fiveleaf/ko/` 도 `/fiveleaf/privacy/ko/` 도 그대로
열린다. App Store Connect 는 지원 URL 과 개인정보 처리방침 URL 을 **필수**로
요구하고 심사는 그 주소로 직접 오므로, 홈에서 감춰도 제출에는 지장이 없다.
오히려 아직 살 수 없는 앱을 목록에 세우는 쪽이 방문자에게 불친절하다.

**출시하면 그 두 줄의 주석을 걷는다.** FiveLeaf 저장소의 `CLAUDE.md` M10 항목에도
같은 말이 적혀 있다 — 두 곳 중 한 곳만 보고도 되살릴 수 있게 해 둔 것이다.

## 구조

문구와 마크업을 나눠 둔다. **문구를 고칠 때 여는 파일은 `_data/` 하나뿐이다.**

```
_data/products.yml          제품 공통값 (앱스토어 ID·개인정보 방침·언어 목록·카페 링크)
_data/<제품>_<언어>.yml      그 언어의 모든 문구
_layouts/support.html       지원 페이지 마크업 (제품·언어 공용, 한 장뿐)
_layouts/hub.html           제품 목록
_layouts/redirect.html      /<제품>/ 의 언어 분기
assets/css/site.css         공통 스타일 (라이트·다크)
<제품>/<언어>/index.html     front matter 만 있는 stub
```

## 언어를 늘릴 때

1. `_data/<제품>_<언어>.yml` 을 기존 파일을 복사해 만든다
2. `_data/products.yml` 의 그 제품 `languages` 에 코드를 넣는다
3. `_data/languages.yml` 에 그 언어로 쓴 이름을 넣는다
4. `<제품>/<언어>/index.html` stub 을 만든다

## 제품을 늘릴 때

위 네 가지에 더해 `_data/products.yml` 에 항목을, 루트 `index.html` 의 `products` 에 한 줄을 넣고,
앱 아이콘을 `assets/img/<제품>-mark.png` 로 넣는다(512px 정도).

## `apps.json` — 앱 안의 「추천 앱」 목록

`letsean.dev/apps.json` 은 **손으로 쓰는 파일**이다. 집에갈래(WannaGoHome)가 통계 탭
광고 자리에 우리 앱을 띄울 때 하루 한 번 읽는다. `_data/products.yml` 과 따로 둔다.

- `live: false` 인 앱은 앱 안에 나오지 않는다. **「다섯 글자」가 심사를 통과하면
  `fiveleaf` 의 `live` 를 `true` 로 바꾼다** — 앱 업데이트 없이 다음 날부터 나온다
- `languages` 에 있는 언어의 `name`·`tagline` 이 모두 있어야 그 언어에서 나온다
- 형식을 바꾸면 `version` 을 올린다. 앱은 모르는 `version` 을 무시하고 가진 사본을 쓴다
- 집에갈래 저장소 `App/Resources/apps.json` 에 같은 파일이 번들돼 있다(첫 실행·오프라인용)

## 상단 바 — 언어 이름표가 접히면 원이 된다

`.langs a` 의 `white-space: nowrap` 을 **지우지 말 것.** 없으면 좁은 폭에서
「한국어」가 「한국 / 어」로 접히고, `border-radius: 999px` 가 그 두 줄짜리 상자를
**큰 원**으로 만든다(실기기에서 그렇게 나왔다). 글자 크기의 문제가 아니라
줄바꿈의 문제다.

560px 아래에서는 **브랜드가 양보한다** — 아이콘이 작아지고 부제가 접힌다.
언어 이름표 셋은 한 줄에 서야 고를 수 있고, 브랜드는 이미 고른 것을 말할 뿐이다.

## 색

앱 아이콘에서 그대로 가져왔다 — 종이 `#f6f5f0`, 먹 `#2e2c36`, 키 `#c7c6c0`.
제품마다 색을 바꾸지 않는다. 구분은 아이콘과 이름이 한다.

## 로컬에서 보기 (선택)

```bash
gem install jekyll
jekyll serve
```
