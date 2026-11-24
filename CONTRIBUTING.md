# Contributing

이 저장소(`claude-plugin-marketplace`)에 기여하는 방법을 정리한다.

## 저장소 구성 방식

- 목록 저장소 하나와 플러그인별 저장소로 나눠 관리한다. 이 저장소는 목록(`.claude-plugin/marketplace.json`)만 가진다.
- 각 플러그인은 `<플러그인 이름>-plugin` 이름의 별도 저장소에서 코드와 버전을 관리한다. 목록의 각 항목은 그 저장소를 가리킨다.
- 플러그인을 고쳐도 이 저장소를 수정할 필요는 없다. 플러그인을 추가하거나 제거할 때만 목록을 고친다.
- 마켓플레이스 이름은 `kimeloo`이다. 플러그인과 마켓플레이스 이름은 `claude-`나 `anthropic-`로 시작할 수 없다.
- 개발 PC에서는 `claude-plugins/` 같은 상위 폴더 아래에 목록 저장소와 플러그인 저장소를 나란히 둔다.

```
claude-plugins/
├── claude-plugin-marketplace/     ------ 이 저장소(목록)
├── visual-decisions-plugin/       ------ 플러그인 저장소
└── <다른 플러그인>-plugin/
```

## 플러그인 추가 절차

1. 플러그인 저장소를 `kimeloo/<플러그인 이름>-plugin`으로 만들고 push한다. 저장소 루트에 `.claude-plugin/plugin.json`과 `skills/` 등이 있어야 하며, 저장소는 공개 상태여야 한다.
2. 플러그인 저장소에서 `claude plugin validate .`가 통과하는지 확인한다.
3. 이 저장소의 `.claude-plugin/marketplace.json`에 항목을 추가한다.
   ```json
   {
     "name": "<플러그인 이름>",
     "source": { "source": "github", "repo": "kimeloo/<플러그인 이름>-plugin" },
     "description": "..."
   }
   ```
4. README의 "등록된 플러그인" 표와 CHANGELOG를 갱신한다.
5. `claude plugin validate .`로 목록을 검증한 뒤 Pull Request를 연다.

플러그인을 제거할 때는 항목을 지우고 CHANGELOG에 기록한다.

## 개발 환경

- Claude Code (`claude plugin validate`에 사용)

## 작업 흐름

1. 이슈를 먼저 남기거나 기존 이슈에서 논의한다.
2. 브랜치를 만들어 작업한다. 브랜치 이름은 `feature/<주제>` 또는 `hotfix/<주제>`를 사용한다.
3. 변경을 커밋하고 `claude plugin validate .`를 통과시킨 뒤 Pull Request를 연다.

## 커밋 메시지

- 제목 형식: `<type>: <summary>` (type과 summary는 영어, summary는 소문자로 시작하고 50자 이내의 명령형)
- type: `feat`, `fix`, `refactor`, `docs`, `chore`
- 본문은 필요할 때만 작성하며, 어느 시점에서 읽어도 이해할 수 있게 적는다.

## 버전과 릴리스

- 플러그인의 버전은 각 플러그인 저장소의 `plugin.json`에서 관리한다. 이 저장소의 목록 항목에는 `version`을 적지 않는다.
- 이 저장소의 CHANGELOG에는 플러그인의 추가, 제거와 목록 구조 변경만 기록한다.

## 이슈와 Pull Request

- 버그 제보, 개선 제안, 문의는 GitHub Issues에 남긴다. 플러그인 자체의 문제는 해당 플러그인 저장소의 Issues에 남긴다.
- Pull Request에는 무엇이 왜 바뀌는지와 확인한 방법을 적는다.

## 라이선스

기여한 내용은 이 저장소와 같은 [Apache License 2.0](LICENSE)으로 배포되는 것에 동의한 것으로 본다.
