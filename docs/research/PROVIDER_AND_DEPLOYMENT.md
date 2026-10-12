# OpenAI·로컬 모델·AWS/개인 노트북 설계 근거

확인일: 2026-10-13. 공식 문서 조사이며 사용자 계정·잔액·인프라에 접속하지 않았다.

## 사용자의 운영 의도

AWS 무료 적용 자원 또는 개인 노트북을 고려한다. 개인 OpenAI API 비용/크레딧 수백 달러가 있고, 필요하면 로컬 LLM을 고려한다. 비용은 현재 핵심 제품 제약이 아니다. 월 3만 원의 고정 상한은 선택되지 않았다.

## OpenAI: 형태와 내용의 구분

Structured Outputs는 JSON Schema에 맞는 출력을 제공하지만 refusal·미완료를 처리해야 하고 내용 오류가 남을 수 있다. 앱의 구조·참조·범위 검사와 내용 평가는 계속 필요하다. [공식 Structured Outputs](https://developers.openai.com/api/docs/guides/structured-outputs)

추천: 경로·설명 단위·시각 데이터마다 작은 스키마를 사용하고 provider 객체를 제품 모델로 유출하지 않는다. 정답성과 출처 충실도는 스키마 적합성과 별도로 기록한다.

## OpenAI: 출처 검색

Responses API web search는 인용 정보와 출처 목록, domain filtering을 설명한다. 사용자에게 검색 근거를 보여줄 때 인용은 눈에 보이고 클릭 가능해야 한다. [공식 Web Search](https://developers.openai.com/api/docs/guides/tools-web-search)

추천: AI·개발 최신 사실은 공식 출처를 우선하는 작은 검색 단계로 구성한다. 비용·시간·출처 범위가 제한된 작업이며 임의 shell·DB·코드 실행 권한과 합치지 않는다. 목록에 링크가 많다고 주장 검증이 끝난 것은 아니다.

## OpenAI: 음성

음성 API는 파일 형식과 여러 언어를 지원하지만 목소리는 영어에 최적화됐다고 설명한다. AI 음성임을 사용자에게 분명하게 알려야 한다. [공식 TTS](https://developers.openai.com/api/docs/guides/text-to-speech)

추천: 첫 언어·한국어 설명·전문 용어·외국어 표현의 실제 음성을 평가한 뒤 profile을 정한다. model·voice를 서버 설정으로 바꿀 수 있게 하되 변경 뒤 품질을 다시 확인한다. 본문·대본·음성 버전과 offline 파일을 함께 저장한다.

## SDK와 공급자 경계

공식 Java SDK는 서버 클라이언트와 Responses API 사용을 설명한다. [Java SDK](https://developers.openai.com/api/reference/java)

추천: Java를 선택한다면 제품이 정의한 설명·출처·음성 port 뒤의 어댑터에 SDK를 둔다. 정확한 SDK 버전·지원 모델·timeout·retry는 구현 시작 때 문서와 호환성 검사로 고정한다.

로컬 LLM은 같은 제품 계약을 통과하는 선택적 공급자다. OpenAI-compatible endpoint라고 출력·검색·음성 기능이 동일한 것은 아니다. 브라우저가 임의 base URL과 서버 자격증명을 설정하게 하지 않는다. 품질·속도·하드웨어가 확인되기 전 자동 대체를 보증하지 않는다.

## AWS 무료 적용

공식 자료에서 무료 혜택은 계정 plan·가입 조건·크레딧·기간·서비스에 따라 다르다. 현재 신규 Free plan 설명에는 기간과 크레딧 소진 조건이 있다. 사용자의 기존 계정이 어느 조건인지 조사하지 않았다. [AWS Free Tier](https://aws.amazon.com/free/), [AWS Billing](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/free-tier.html)

추천: 무료로 영구 운영 가능하다는 전제로 특정 서비스를 선택하지 않는다. 실제 배포 때 계정 조건·RAM·DB/파일 보관·네트워크를 확인한다. 무료 자원의 성능이 부족하면 같은 앱·DB·파일을 개인 노트북으로 옮길 수 있게 한다.

## 개인 노트북의 운영 조건

노트북이 꺼져 있으면 새 생성·server sync는 사용할 수 없고 이미 받은 이동 묶음만 사용한다. 외부 휴대폰에서 연결하는 경로와 HTTPS가 필요하다. 이 경로는 배포 단계에서 정하고, DB·관리 화면을 그대로 인터넷에 공개하지 않는다.

이 문서에서 외부 접속·계정·키·실제 모델 호출·유료 자원 생성은 수행하지 않았다.
