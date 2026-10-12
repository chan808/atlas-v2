# Project Atlas v2

기준일: 2026-10-13 (Asia/Seoul)
초기 개인 사용 설계안 v0.1. 이번 작업은 요구 발견·공식 자료 조사·설계·문서화이며 제품 코드는 아직 없다.

## 목적

배우고 싶은 것을 말하면 현재 수준과 목표에 맞는 설명·자료·시각 표현으로 시작하고, 언제든 방향을 바꾸며, 공부한 내용을 요약·예습·암기·듣기·기록으로 이어가는 개인 학습 공간.

서비스를 개발하면서 소유자의 개발 실력을 늘리는 것은 목표에서 제거한다.

## 확인한 초기 범위

- AI·개발과 외국어 우선. 독립 수학은 보류 가능.
- AI의 추천과 선택지로 시작하고 언제든 방향·자료·깊이를 바꿈.
- 인기 주제의 선택적 템플릿과 독립 새 생성.
- 개인 PC+Android, 같은 기록. 준비한 이동용 요약·암기·음성 offline 사용, 새 생성 online.
- 주제·공개 링크·텍스트부터. 파일 업로드·타인·공유·실시간은 이후.
- 비용은 주요 제약이 아님. AWS/개인 노트북·OpenAI 자원·필요시 local 모델을 고려.
- 미전송 offline 기록은 원 owner 재로그인까지 보관. 다른 계정에 노출/전송하지 않음.

## 먼저 읽기

1. [구현 세션 인계](docs/HANDOFF.md)
2. [결정·제안·검증 대기](docs/DECISION_REGISTER.md)
3. [제품 요구](PRD.md)
4. [첫 구현 행동](docs/IMPLEMENTATION_BRIEF_S1.md)

## 문서 지도

| 묶음 | 문서 |
|---|---|
| 원문·의도 | [사용자 원문](docs/discovery/ORIGINAL_REQUESTS.md), [Q1–Q9와 의도](docs/discovery/USER_INTENT.md) |
| 조사 종합 | [조사 계획](docs/research/RESEARCH_PLAN.md), [결과와 차별화 가설](docs/research/RESEARCH_SYNTHESIS.md) |
| 실제 서비스 | [시각·AI·개발](docs/research/INTERACTIVE_AND_TECH_LEARNING.md), [정리·복습·음성](docs/research/STUDY_TOOLS_AND_AUDIO.md), [외국어와 학습 연구](docs/research/LANGUAGE_AND_LEARNING_SCIENCE.md) |
| 기술 근거 | [Android/PWA/offline](docs/research/PWA_AND_OFFLINE.md), [OpenAI·AWS·노트북](docs/research/PROVIDER_AND_DEPLOYMENT.md) |
| 경험·콘텐츠 | [사용자 흐름](docs/UX_AND_PERSONALIZATION.md), [화면 설계 예시](docs/SCREEN_BLUEPRINTS.md), [콘텐츠·AI·출처 계약](docs/CONTENT_AND_AI_CONTRACT.md) |
| 데이터·구조 | [데이터·API](docs/DATA_AND_API_DESIGN.md), [아키텍처](docs/ARCHITECTURE.md), [기술 추천 ADR](docs/adr/0001-portable-monolith-and-android-pwa.md) |
| 운영 | [보안·비용·운영](docs/SECURITY_AND_OPERATIONS.md) |
| 구현·검증 | [단계별 계획](docs/IMPLEMENTATION_PLAN.md), [수용·내용 평가](docs/ACCEPTANCE_AND_EVALS.md), [요구 추적](docs/REQUIREMENT_TRACEABILITY.md) |
| 검토·인계 | [설계 범위](docs/DESIGN_PLAN.md), [독립 검토](docs/review/DESIGN_REVIEW.md), [인계](docs/HANDOFF.md), [작업 규칙](AGENTS.md) |

## 설계의 상태

사용자가 확인한 요구와 에이전트의 추천은 분리돼 있다. 기술 추천은 React·TypeScript Android PWA + Spring Boot 단일 앱 + PostgreSQL이며 ADR은 제안 상태다. 환경·도구chain·인증·모델/음성 profile의 실제 설정은 첫 구현 계약에서 확인한다.

공식 자료 13개 서비스/도구군을 비교했지만 유료 계정 내부의 직접 생성·수강 실험은 하지 않았다. 지원 기능·업체 효과 주장·조사자의 설계 추론을 구분했다. Android offline·음성도 문서상 근거와 실제 기기 검증이 다르다.

문서 검사는 제품이 실행됐다는 증거가 아니다. 구현 후 실제 사례로 시작·이해·조정·재개·이동 사용의 품질을 검증한다.

## 다음 구현 세션

이 폴더를 작업 공간으로 열고 AGENTS.md와 HANDOFF부터 읽는다. S0와 S1을 구체화한 뒤 사용자 행동 하나씩 구현한다. 이번 대화에서 이미 확인한 요구를 다시 추측하거나 v1의 장애 실습 로드맵을 가져오지 않는다. 인계 문서에 시작 메시지 예시가 있다.
