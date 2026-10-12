# 실제 서비스 및 설계 방식 조사 계획

기준일: 2026-10-13 (Asia/Seoul)
상태: 공식 자료의 1차 조사 정리 완료. 실제 계정/기기 사용과 교육 효과 검증은 아직 수행하지 않았다.

## 조사 질문

기능의 수보다 사용자가 얼마나 적은 준비로 학습을 시작하고, 이해·기억·재개·연결·공유로 이어갈 수 있는지를 비교한다.

## 조사군

1. 자료 기반 설명·요약·음성: NotebookLM 및 실제 공식 자료의 최신 상태, StudyFetch 등
2. 암기·복습·지식 기록: Anki, RemNote, Quizlet
3. 시각적·단계적 이해: Brilliant, Khan Academy/Khanmigo, 3Blue1Brown
4. 조작 가능한 수학 표현과 공유: Desmos, GeoGebra
5. 개발·AI 학습: DataCamp 등
6. 외국어 짧은 학습·듣기: Duolingo, Busuu
7. 의도 분석·설계 인계 방식: Dryforge, Matt Pocock의 grill-me/grilling

## 각 근거의 기록 항목

- 공식 페이지 제목·직접 URL·확인일
- 확인한 행동, 입력과 결과, 이용 조건
- 공식 문서로 확인한 사실 / 사업자의 효과 주장 / 조사자의 추론 구분
- 직접 사용 검증 여부
- Atlas에 가져올 원리와 가져오지 않을 복잡성
- 요구 ID 연결과 수용 시나리오
- 문서가 확인하지 못한 부분

공식 설명이 없다는 이유만으로 기능이 없다고 단정하지 않는다. 로그인·유료 계정 내부를 직접 써보지 않은 서비스의 실제 품질을 검증됐다고 쓰지 않는다. 가격·무료 제공 범위·플랜 제한은 중요한 결정을 할 때 최신 공식 페이지로 별도 확인한다.

## 참고할 방식

- [Dryforge ready 원문](https://github.com/prekuter/dryforge/blob/main/src/skills/ready/SKILL.md)
- [Dryforge 결과 문서 형식](https://github.com/prekuter/dryforge/blob/main/src/skills/ready/references/output-format.md)
- [Matt Pocock grill-me 원문](https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md)
- [실제 grilling 인터뷰 원문](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md)

현재 로컬에 해당 플러그인·스킬이 설치돼 있지 않다. 공개 원문을 참고하는 설계 작업이며, 설치된 ready/go를 실행하거나 최종 승인을 받았다고 주장하지 않는다. 사용자 요청에 따라 이번 작업은 조사·설계·문서화까지다.

요구와 구현 방법을 분리하고, 근거를 찾을 수 있는 사실은 조사하며, 사용자의 판단이 필요한 선택은 추천과 이유를 붙여 질문한다. 인터뷰 기록을 보존하고, 독립 검토에서 미확인 가정이 확정 요구로 바뀌었는지 확인한다.
