# letsean.dev — 지원 사이트

앱 고객지원 페이지를 한 곳에 모은다. GitHub Pages 가 Jekyll 을 서버에서 빌드하므로
**푸시하면 그대로 배포된다**. 로컬에 Node·Ruby 를 깔 필요가 없다.

| 주소 | 내용 |
|---|---|
| `letsean.dev/` | 제품 목록 |
| `letsean.dev/kanaji/ja` · `/kanaji/ko` | 카나지 (일본어 키보드) |
| `letsean.dev/hankey/ko` · `/hankey/en` | 한글키 (한글 키보드) |
| `letsean.dev/<제품>/` | 브라우저 언어에 맞는 쪽으로 보낸다 |

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

## 색

앱 아이콘에서 그대로 가져왔다 — 종이 `#f6f5f0`, 먹 `#2e2c36`, 키 `#c7c6c0`.
제품마다 색을 바꾸지 않는다. 구분은 아이콘과 이름이 한다.

## 로컬에서 보기 (선택)

```bash
gem install jekyll
jekyll serve
```
