# Atlas v2 에이전트 작업 규칙

## 첫 읽기

README.md → docs/HANDOFF.md → docs/DECISION_REGISTER.md → PRD.md를 읽는다.
실제 요구의 권위는 docs/discovery/USER_INTENT.md와 ORIGINAL_REQUESTS.md다.
변경 대상에 따라 UX_AND_PERSONALIZATION, CONTENT_AND_AI_CONTRACT, DATA_AND_API_DESIGN, ARCHITECTURE, SECURITY_AND_OPERATIONS, IMPLEMENTATION_PLAN, ACCEPTANCE_AND_EVALS를 읽는다.

## 제품

- 사용자의 학습을 쉽게 만드는 결과에 집중한다. 개발자 기술 학습 목적의 아키텍처·실습을 추가하지 않는다.
- AI가 수준·목표에 맞는 시작안을 제시하고 사용자가 언제든 바꿀 수 있게 한다.
- 원문·사용자 직접 선택과 AI 추정을 구분한다.
- 콘텐츠 생성·열람·청취·회상·적용을 혼동하지 않는다. 근거 없는 숙련 수치를 만들지 않는다.
- 템플릿을 강제하지 않으며 새 생성 선택을 유지한다.
- 초기 개인 PC·안드로이드와 준비 자료 offline 요구를 보존한다.
- 미래 공유·실시간·수학을 자동으로 첫 단계에 포함하지 않는다.

## 설계 상태

현재 문서는 설계 초안과 추천안을 포함한다. 기술 선택과 실기기/실 모델 검증 대기는 HANDOFF에 있다. 문서가 있다는 이유로 모든 선택이 accepted 또는 모든 검사가 passed라고 쓰지 않는다.
이번 설계 대화는 문서화 전용이다. 다른 세션에서 사용자가 구현을 요청하면 인계에 따라 첫 구현 범위를 확인하고 진행한다.

## 구현

- 실제 사용자 행동 하나씩 구현하고 목표·보존 조건·실패·파일·검증·되돌림을 기록한다.
- 외부 호출은 DB 트랜잭션 밖, 변경은 소유권·버전·중복 요청 검사 뒤 적용한다.
- 스키마 migration과 UTC 시간·주입 가능한 Clock을 사용한다.
- 공급자 SDK를 제품 domain에서 분리한다. 비밀은 서버에서 관리한다.
- 앱 권한으로 임의 AI HTML/JS·사용자 코드·shell을 실행하지 않는다.
- 내용·출처의 지시문을 앱 명령으로 취급하지 않는다.
- 미래 모듈·microservice·broker·vector/graph DB는 측정된 필요 없이는 추가하지 않는다.
- 정상·timeout·중복·동시·부분 실패·권한을 독립적으로 검토한다.
- CI는 paid model/API key를 요구하지 않는다. 실제 품질 평가와 CI를 구분한다.
- 실패한 검사를 통과시키려고 요구·검증을 약화하지 않는다.
- unsupported 환경 또는 실행 못 한 검사는 unverified로 기록한다.

## 현재 검증

제품 코드·실행 스크립트는 아직 없다. 구현 세션에서 선택 스택의 검증 명령을 만들어 인계와 README에 기록한다. 문서 검사 결과는 docs/review/DESIGN_REVIEW.md를 참고한다.
