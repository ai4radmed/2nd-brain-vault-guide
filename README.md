# 2nd-brain-vault-guide — PARA 기반 second-brain 운영 지침

Claude Code · Obsidian · Docker 환경에서 [Tiago Forte의 BASB](https://www.buildingasecondbrain.com/) 와 [PARA 방법론](https://fortelabs.com/blog/para/) 으로 개인 지식관리(PKM) 시스템을 운영하기 위한 **공개 지침·템플릿·골격 모음**.

> 이 저장소는 *방법론과 골격* 만 공개합니다. 개인 노트·원본 자료는 포함되지 않습니다.
> 이 가이드는 [2nd-brain-docker](https://github.com/ai4radmed/2nd-brain-docker) 가 제공하는 컨테이너 환경 (Claude CLI, Gemini CLI, OpenClaw, MCP 서버들) 을 가정합니다.

---

## 자매 저장소

| 저장소 | 역할 | 공개 여부 |
|---|---|---|
| **[2nd-brain-docker](https://github.com/ai4radmed/2nd-brain-docker)** | 격리 실행환경 (Docker 이미지·compose·Makefile) | 공개 |
| **2nd-brain-vault-guide** *(이 저장소)* | PARA 운영 지침·워크플로우·빈 vault 골격 | 공개 |
| **2nd-brain-vault** *(개인)* | 실제 knowledge·sources 데이터 + 얇은 개인 CLAUDE.md | 비공개 (각자 운영, Syncthing 동기) |

세 저장소는 다음 비유로 이해할 수 있습니다.

- **docker** = 건물(실행환경)을 짓는 도면
- **vault-guide** = 건물 안에서의 생활 규칙·가구 배치도 *(이 저장소)*
- **vault** = 그 건물에서 실제로 살아가는 한 사람의 살림살이

`2nd-brain-docker` 로 환경을 띄우고, 본 저장소를 별도 위치에 clone 합니다. 자기 vault 는 별도의 **비공개 저장소** (Syncthing 으로 PC 간 동기, 로컬 git 으로 버전관리) 로 운영하며, vault 의 `CLAUDE.md` 는 본 가이드 문서들을 `@`-import 하는 *얇은 layer* 로 둡니다.

---

## 저장소 구조

```
2nd-brain-vault-guide/
├── CLAUDE.md                   권위 문서 — Claude Code 가 자동으로 읽는 운영 매뉴얼
├── claude-config/              Claude Desktop / Claude Code 설정 동기화 3계층
│   ├── platform/               OS별 차이 (Windows / WSL2)
│   ├── scripts/                동기화 셋업 스크립트
│   └── shared/                 기기·OS 무관 공통 자산
│       ├── memory/             장기 기억 (user / feedback / project / reference)
│       ├── skills/             공용 skill 정의
│       └── commands/           커스텀 슬래시 커맨드
├── knowledge/                  Obsidian vault 골격 (마크다운만)
│   ├── 00_inbox/
│   ├── 01_projects/
│   ├── 02_areas/
│   │   └── brain-system/       이 vault 자체에 관한 메타 문서
│   │       ├── workflows/      브레인화 워크플로우 (Gmail / Contacts 등)
│   │       └── tools/          외부 도구 메타 (Claude Code / OpenClaw 등)
│   ├── 03_resources/
│   │   └── setup/              환경 셋업 가이드
│   └── 04_archive/
├── sources/                    원본 파일(PDF·docx·xlsx 등) 보관 골격
│   └── (knowledge/와 동일한 PARA 4분류)
└── templates/                  노트 템플릿 (인맥 카드 등)
```

### `knowledge/` 와 `sources/` 의 짝 구조

PARA 4분류(00_inbox · 01_projects · 02_areas · 03_resources · 04_archive)를 **두 폴더에 미러링**합니다.

| `knowledge/` | `sources/` |
|---|---|
| 생각·요약·연결 | 원본 파일 저장 |
| `.md` 마크다운만 | PDF·docx·xlsx·이미지 등 바이너리 |
| Obsidian 볼트로 열기 | 파일 탐색기로 탐색 |
| 가변 — 갱신·재작성 | 불변 — 추가만, 수정 안 함 |

같은 주제의 동반 노트는 두 폴더에서 **동일한 상대 경로**에 둡니다. 예를 들어 `knowledge/02_areas/조직/회의록.md` 옆에 `sources/02_areas/조직/회의록.pdf` 가 있는 식입니다. 마크다운 노트에서 원본을 `file://` 로 참조합니다.

### `claude-config/` 의 3계층

| 계층 | 무엇이 들어가나 | 공유 범위 |
|---|---|---|
| `shared/` | 보편 규약·공용 skill·장기 기억 | 모든 기기·OS 동일 |
| `platform/` | OS별 경로 변환·환경 차이 | OS별 |
| `device/` | 기기별 설정 (호스트명·드라이브 문자 등) | 기기별 (이 저장소엔 미포함, 비공개) |

본 저장소는 `shared/` 와 `platform/` 만 포함합니다. `device/` 는 개인 환경에 종속되므로 비공개 vault 측에서 관리합니다.

---

## 사용 패턴

### A. 새로 시작하는 사람 — vault 템플릿으로 사용

```bash
# 1. 이 저장소를 clone
git clone https://github.com/ai4radmed/2nd-brain-vault-guide.git my-second-brain
cd my-second-brain

# 2. git 이력 분리 (자기 비공개 저장소로 다시 시작)
rm -rf .git
git init
git remote add origin <자신의-비공개-저장소-URL>

# 3. 도커 환경에서 실행
git clone https://github.com/ai4radmed/2nd-brain-docker.git ../2nd-brain-docker
cd ../2nd-brain-docker
make build && make rw
```

### B. 운영 지침만 참고

`CLAUDE.md`, `knowledge/02_areas/brain-system/`, `claude-config/shared/memory/feedback-*.md` 만 보고 자기 시스템에 응용하세요.

### C. 짝 저장소로 운영 (저자 권장)

`2nd-brain-vault-guide` 를 별도 위치에 clone 하고, 자기 vault 의 `CLAUDE.md` 가 가이드 문서들을 `@`-import 하는 *얇은 layer* 패턴으로 운영합니다. 가이드는 git 으로 갱신, vault 는 Syncthing 으로 PC 간 동기 + 로컬 git 으로 버전관리 — 두 흐름이 분리되어 가이드는 항상 최신을 유지하고 vault 는 개인 영역으로 남습니다.

---

## 진행 상태

### 1차 publish (방법론·메모리·템플릿)

- [x] 디렉토리 골격
- [x] `CLAUDE.md` (가이드 안내, thin stub)
- [x] `knowledge/02_areas/brain-system/README.md` (PARA·브레인화·동반 노트 패턴)
- [x] `knowledge/02_areas/brain-system/claude-instruction-layers.md` (지침 7계층·토큰 예산)
- [x] `claude-config/shared/memory/{MEMORY, feedback-knowledge-cutoff-humility, feedback-respect-past-diagnosis}.md`
- [x] `knowledge/02_areas/인맥/_template.md`

### 2차 publish 후보 (방법론 추출·일반화 필요)

- [ ] `knowledge/02_areas/brain-system/folder-organization.md` — 02_areas 격상·강등 방법론만 추출 (실제 조직 예시 제거)
- [ ] `knowledge/02_areas/brain-system/cli-mcp-architecture.md` — AI 매개 vs 결정형 트랙 분리 원칙만 추출 (특정 도구 스택 의존 제거)
- [ ] `knowledge/02_areas/brain-system/workflows/gmail-capture.md` — 4분류·5단계 안전장치·일·주·월 루틴 (도구 명령어 일반화)
- [ ] `knowledge/02_areas/brain-system/workflows/contacts-capture.md` — Layer 분리·파일명 정책 (실명 제거)
- [ ] `knowledge/02_areas/인맥/README.md` — 운영 워크플로우 (조직·역할 일반화)

### 추후 (사용자 시스템 새 동기 아키텍처 안정 후)

- [ ] `claude-config/platform/{paths-table, windows, wsl2}.md` — 새 아키텍처 기준 재작성
- [ ] `claude-config/scripts/setup-*.sh` — 새 아키텍처 기준 재작성
- [ ] `knowledge/03_resources/setup/` — 셋업 가이드 (현재 모두 도구 스택 의존)

### 기타

- [ ] LICENSE 결정 (MIT 후보)
- [ ] `git init` + GitHub 레포 생성 + 첫 푸시
- [ ] 외부인 시점 검증 (깨끗한 환경에서 README 단계대로 따라해보기)

---

## 라이선스

미정. MIT 또는 CC BY-SA 검토 중. 결정 전까지는 fork·참고는 자유, 재배포는 저자 문의 바랍니다.

## 문의

issue 또는 [@BenKorea](https://github.com/BenKorea) 로 연락 바랍니다.
