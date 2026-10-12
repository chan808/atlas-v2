# PC·안드로이드와 offline 이동 학습의 기술 근거

확인일: 2026-10-13. 공식 브라우저 문서 조사. 목표 휴대폰 실험은 하지 않았다.

## 설치와 offline 시작

Android 설치형 웹은 manifest·HTTPS 등 설치 조건이 필요하다. Service Worker로 준비한 화면·자료를 제공할 수 있지만 설치만으로 학습 자료가 다운로드되는 것은 아니다. [MDN 설치](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Guides/Making_PWAs_installable), [Caching](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Guides/Caching)

추천: 반응형 웹과 작은 offline 이동 묶음으로 시작한다. 첫 방문부터 offline이 되는 것처럼 약속하지 않는다.

## 저장소

IndexedDB는 구조화한 개인 자료·이벤트·파일에 적합하고 Cache API는 응답을 저장한다. 두 영역 모두 quota와 삭제 정책의 영향을 받는다. [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API), [Cache](https://developer.mozilla.org/en-US/docs/Web/API/Cache)

기본 저장은 best-effort이며 공간 압박·사용자 삭제·비공개 모드 종료 등으로 사라질 수 있다. estimate는 추정치이고 persist 요청도 거절될 수 있다. [Quota와 eviction](https://developer.mozilla.org/en-US/docs/Web/API/Storage_API/Storage_quotas_and_eviction_criteria), [persist](https://developer.mozilla.org/en-US/docs/Web/API/StorageManager/persist)

추천: manifest·digest·완료 상태와 재다운로드를 제공한다. 서버에 원본·확인된 기록을 보관한다. 아직 sync하지 않은 offline 이벤트는 브라우저 자료 삭제 시 잃을 수 있으므로 영구 저장을 보증하지 않는다.

## 음성

Media Session은 재생 정보와 제어를 연결한다. 운영체제가 항상 재생을 유지한다는 보장은 아니다. 재생 시작에 사용자 조작이 필요할 수 있다. [Media Session](https://developer.mozilla.org/en-US/docs/Web/API/Media_Session_API), [Chrome 설명](https://web.dev/articles/media-session), [Autoplay](https://developer.mozilla.org/en-US/docs/Web/Media/Guides/Autoplay)

스트리밍으로 일부를 재생한 것과 음성 전체를 받은 것은 다르다. 공식 Workbox 안내는 전체 파일 준비와 Range 요청 처리를 고려한다. [Cached audio/video](https://developer.chrome.com/docs/workbox/serving-cached-audio-and-video)

추천: 서버에서 만든 유한한 음성 파일을 미리 저장하고 실제 비행기 모드에서 재생·seek·잠금화면·다른 앱 전환·통화 중단·복귀를 검사한다. 브라우저 TTS나 Service Worker를 계속 살아있는 음성 생성 엔진으로 의존하지 않는다.

## 동기화

Background Sync는 지원과 실행 제한이 있다. [Background Sync](https://developer.mozilla.org/en-US/docs/Web/API/Background_Synchronization_API), [Offline/background operation](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Guides/Offline_and_background_operation)

추천: 앱을 열거나 연결이 돌아오면 outbox를 재전송한다. 인증된 사용자+eventId로 서버가 중복을 제거하고 확인한 것만 장치에서 제거한다. 다른 두 기기의 별도 회상을 중복으로 제거하지 않는다. 이 로직은 브라우저가 자동 제공하는 것이 아니라 앱의 책임이다.

## 계정 경계

Cache API는 HTTP cache header에 맞춰 항목을 자동 만료시키지 않는다. Clear-Site-Data도 사용할 수 있지만 앱 직접 정리 경로가 필요하다. [Cache 동작](https://developer.mozilla.org/en-US/docs/Web/API/Cache), [Clear-Site-Data](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Clear-Site-Data)

추천: 로그인·계정 API를 무차별 cache하지 않는다. 계정별 자료·outbox·현재 재생 정보를 구분한다. offline 로그아웃의 로컬 차단과 online 서버 세션 폐기를 구분한다.

## 초기 검증 기준

준비 완료→종료→비행기 모드→재시작→요약/카드/음성→재연결→PC에 기록 반영, 부분 다운로드, quota, 저장소 제거, 업데이트 호환, 계정 변경을 검사한다.

앱 내 잠금화면 재생이 목표폰에서 실패하면 먼저 시스템 플레이어용 파일 제공을 검토한다. 앱 안에서 반드시 성립해야 하는 요구라면 음성 재생 계층만 native로 보완하는 대안을 제안한다. offline 필수 요구를 조용히 삭제하지 않는다.

iOS는 초기 검증 대상이 아니며 추후 별도 검사한다.

## 미전송 기록의 로그아웃 보관 — 추가 설계 근거

사용자가 원 owner 재로그인까지 보존을 선택했다. owner별 암호화 payload와 재인증 후 복원 key 제공, 로그아웃 시 장치 key 제거를 구현 후보로 둔다. Web Crypto는 표준 primitive를 제공하지만 key 관리와 전체 보안이 자동 해결되는 것은 아니다. 구현과 key lifecycle은 별도 독립 검토가 필요하다. [Web Crypto](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API), [encrypt](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/encrypt)
