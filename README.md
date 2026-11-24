<div align="center">
  <h1>claude-plugin-marketplace</h1>
  <p>
    개인용 Claude Code 플러그인 마켓플레이스. 플러그인 목록만 관리하고 각 플러그인은 자기 저장소에서 관리한다.
    <br />
    <br />
    <br />
    주요 문서
    <br />
    <a href="CHANGELOG.md"><strong>CHANGELOG</strong></a> ·
    <a href="CONTRIBUTING.md"><strong>CONTRIBUTING</strong></a>
  </p>
</div>

## 목차
1. [프로젝트 개요](#1-프로젝트-개요)
2. [기술 스택](#2-기술-스택)
3. [디렉토리 구조](#3-디렉토리-구조)
4. [로컬 환경 세팅 및 실행 방법](#4-로컬-환경-세팅-및-실행-방법)
5. [업데이트 및 릴리스](#5-업데이트-및-릴리스)
6. [등록된 플러그인](#6-등록된-플러그인)
7. [이슈 및 문의](#7-이슈-및-문의)

## 1. 프로젝트 개요
* 배경: 플러그인을 하나씩 따로 설치 경로로 안내하지 않고, 이 저장소를 한 번 등록하면 그 안의 플러그인을 골라 설치할 수 있게 하려고 만들었다.
* 핵심 역할:
  - 설치 가능한 플러그인의 목록(`marketplace.json`)을 제공한다.
  - 각 항목은 플러그인 저장소를 가리킨다. 플러그인의 코드와 버전은 이 저장소에 없다.

## 2. 기술 스택
- Language : JSON (마켓플레이스 매니페스트)
- Framework : Claude Code 플러그인 마켓플레이스
- Database : 없음
- Build Tool : 없음
- CI/CD: 없음 (`claude plugin validate`로 검증)

## 3. 디렉토리 구조

```
.
├── .claude-plugin/
│   └── marketplace.json     ------ 마켓플레이스 이름(kimeloo)과 플러그인 목록
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
└── NOTICE
```

저장소 구성 방식: 목록 저장소 하나와 플러그인별 저장소로 나눈다. 이 저장소는 목록만 가지고, 플러그인은 `<플러그인 이름>-plugin` 저장소에서 각각 관리한다. 개발 PC에서는 `claude-plugins/` 같은 상위 폴더 아래에 두 종류의 저장소를 나란히 둔다.

```
claude-plugins/
├── claude-plugin-marketplace/     ------ 이 저장소(목록)
├── visual-decisions-plugin/       ------ 플러그인 저장소
└── <다른 플러그인>-plugin/
```

## 4. 로컬 환경 세팅 및 실행 방법

1. 필수 설치 항목
   - Claude Code
2. 마켓플레이스 등록과 플러그인 설치
   ```bash
   claude plugin marketplace add kimeloo/claude-plugin-marketplace
   claude plugin install <플러그인>@kimeloo
   ```
   - 포크해서 비공개로 쓰는 경우 설치하는 PC에서 git 인증이 비대화형으로 동작해야 한다. SSH 키를 ssh-agent에 등록하거나 `gh auth login` 후 `gh auth setup-git`을 실행한다.
3. 목록 수정 후 검증: `claude plugin validate .`

## 5. 업데이트 및 릴리스

- 목록 갱신과 플러그인 업데이트
  ```bash
  claude plugin marketplace update kimeloo
  claude plugin update <플러그인>@kimeloo
  ```
- 플러그인의 버전은 각 플러그인 저장소의 `plugin.json`에서 관리한다. 플러그인을 고쳤다고 이 저장소를 수정할 필요는 없다.
- 이 저장소는 플러그인을 추가하거나 제거할 때만 수정한다.
- 플러그인을 추가하는 절차는 [CONTRIBUTING.md](CONTRIBUTING.md)를 따른다.

## 6. 등록된 플러그인

| 이름 | 저장소 | 설명 |
|---|---|---|
| `visual-decisions` | [kimeloo/visual-decisions-plugin](https://github.com/kimeloo/visual-decisions-plugin) | 여러 결정을 로컬 HTML 페이지로 한 번에 묻고 선택지 목업을 나란히 비교한다. |

## 7. 이슈 및 문의
문의, 버그 제보, 개선 제안은 [GitHub Issues](https://github.com/kimeloo/claude-plugin-marketplace/issues)에 남긴다. 플러그인 자체의 문제는 해당 플러그인 저장소의 Issues에 남긴다.
