# claude-plugin-marketplace

개인용 Claude Code 플러그인 마켓플레이스이다. 이 저장소에는 목록(`.claude-plugin/marketplace.json`)만 있고, 각 플러그인은 자기 저장소에서 관리한다.

## 사용

```bash
claude plugin marketplace add kimeloo/claude-plugin-marketplace
claude plugin install <플러그인>@kimeloo
```

## 플러그인

| 이름 | 저장소 | 설명 |
|---|---|---|
| `visual-decisions` | [kimeloo/visual-decisions-plugin](https://github.com/kimeloo/visual-decisions-plugin) | 여러 결정을 로컬 HTML 페이지로 한 번에 묻고 선택지 목업을 나란히 비교한다. |

## 업데이트

```bash
claude plugin marketplace update kimeloo
claude plugin update <플러그인>@kimeloo
```

버전은 각 플러그인 저장소의 `plugin.json`에서 관리한다. 목록 파일은 플러그인을 추가하거나 제거할 때만 수정한다.

## 플러그인 추가

`.claude-plugin/marketplace.json`의 `plugins`에 항목을 추가한다.

```json
{ "name": "<플러그인>", "source": { "source": "github", "repo": "kimeloo/<저장소>" }, "description": "..." }
```

저장소 이름 규칙: 플러그인 저장소는 `<플러그인 이름>-plugin`으로 짓는다. 검증은 `claude plugin validate .`로 한다.

## 라이선스

Apache License 2.0. [LICENSE](LICENSE)와 [NOTICE](NOTICE)를 참조한다.
