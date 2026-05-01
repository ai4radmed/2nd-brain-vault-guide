# 2nd-brain-guide — second-brain 운영 지침 (참고용)

이 저장소는 [2nd-brain-docker](https://github.com/ai4radmed/2nd-brain-docker) 컨테이너 환경 안에서 PARA 기반 second-brain 을 운영할 때 참고할 **방법론·장기기억·템플릿** 모음입니다.

> 이 파일은 Claude Code 가 자동으로 읽도록 의도된 *프로젝트 권위 문서* 가 아닙니다 — 가이드 저장소 자체에 대한 안내입니다. 실제 vault 운영 시 자기 데이터 저장소에 별도의 `CLAUDE.md` 를 두세요.

## 들어 있는 것

| 위치 | 내용 |
|---|---|
| `knowledge/02_areas/brain-system/README.md` | second-brain 시스템 정의, PARA 4분류, 브레인화, 동반 노트 패턴 |
| `knowledge/02_areas/brain-system/claude-instruction-layers.md` | Claude Code 지침 7계층과 토큰 예산 가이드 |
| `claude-config/shared/memory/feedback-*.md` | Claude 협업 시 빠지기 쉬운 함정과 그 대응 (지식 컷오프·과거 판단 존중) |
| `knowledge/02_areas/인맥/_template.md` | 인물 노트 frontmatter·본문 템플릿 |

## 아직 들어 있지 않은 것 (의도적, 다음 라운드 예정)

다음 문서들은 한 사용자의 실제 운영 환경(특정 도구 스택·조직·연락처)에 대한 의존도가 높아, 방법론만 추출해 일반화하는 별도 작업이 필요합니다:

- 도구·자동화 architecture — CLI vs MCP, AI 매개 vs 결정형 트랙 분리
- Gmail · Contacts 브레인화 워크플로우 (5단계 안전장치 패턴)
- 02_areas 폴더 격상·강등 운영 지침
- 인맥 관리 시스템 운영 규칙
- 다중 기기 동기 운영 규칙 (현재 사용자 시스템도 이행 중)

## 환경 셋업

이 저장소는 운영 *지침* 의 출발점만 제공합니다. 컨테이너 실행환경 셋업은 짝 저장소 [2nd-brain-docker](https://github.com/ai4radmed/2nd-brain-docker) 가 담당합니다.

## 라이선스·기여

`README.md` 참조.
