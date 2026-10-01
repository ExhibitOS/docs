# 작가용 작품 import 안내

2026-10-01. ExhibitOS contributors. 문서 CC-BY-4.0, 실행 예제 Apache-2.0. 이 안내는 [Platform PR8](https://github.com/ExhibitOS/platform/pull/8)의 구현된 API를 설명한다. 현재 CMS UI는 구현 중이다. 전체 OES/OEX package 또는 Capture 원본을 import하는 기능은 아직 제공하지 않는다.

## 시작 조건

관리자가 [Platform README](https://github.com/ExhibitOS/platform/blob/main/README.md)와 [인증 안내](https://github.com/ExhibitOS/platform/blob/main/docs/auth.md)에 따라 로컬 서버와 PostgreSQL/object storage를 구성해야 한다. 로그인은 tenant를 선택하며 작가의 작품 소유 관계는 로그인 사용자와 별도로 관리한다. 현재 API는 기존 artwork에 단일 primary asset을 추가하므로 새 작가·작품 등록 UI가 필요한 경우 후속 CMS 구현을 기다린다. 공개 signup·비밀번호 복구는 현재 지원하지 않는다.

작품 소유 작가 또는 해당 tenant admin만 import를 생성하고 읽고 취소·재시도할 수 있다. 큐레이터와 관람자 역할은 이 권한을 얻지 않는다. 다른 tenant의 admin 권한은 사용할 수 없다. 로그인 세션과 모든 변경의 Origin/Host/CSRF 검사는 서버에서 수행한다.

## 지원 파일과 물리 크기

단일 GLB2 또는 PNG를 최대32MiB까지 받는다. GLB는 외부 URI·image·texture·extension 없이 self-contained여야 한다. PNG는 non-interlaced8-bitRGB/RGBA, 최대4,194,304pixels, 각 변8192이하이며 ancillary metadata를 받지 않는다. JPEG/WebP, remote URL과 archive는 지원하지 않는다. 폭넓은 일반 glTF 지원을 뜻하지 않으므로 오류 시 원본을 보존하고 호환되는 사본을 준비한다.

등록 값 `scaleMeters`는 양수(최대1,000,000)여야 한다. 이는 전체 작품의 width/height/depth나 provenance 편집을 대체하지 않는다. 별도의 CMS에서 치수와 단위 변환을 확인하는 기능이 후속 구현 대상이다.

## 등록 순서

정확한 request/response 필드는 [import OpenAPI](https://github.com/ExhibitOS/platform/blob/main/contracts/import-openapi.json)와 [서버 안내](https://github.com/ExhibitOS/platform/blob/main/docs/imports.md)를 따른다. 자격정보나 작품 원본을 Git에 저장하지 않는다.

1. `POST /api/v1/tenants/:tenantId/imports`에 artwork ID, idempotency key, MIME, lowercase SHA-256, bytes, scaleMeters와 full OES rights를 보낸다. 같은 key와 같은 payload는 같은 job으로 돌아온다. payload를 바꾸어 같은 key를 쓰면 충돌한다.
2. 받은 job의 `PUT .../imports/:id/bytes`에 전체 파일을 application/octet-stream으로 보낸다. 선언된 크기/hash와 일치해야 한다. 중단된 업로드는 완료되지 않는다.
3. `POST .../imports/:id/complete`가 저장된 bytes를 확인하고 queue에 넣는다. 관리자가 검증 worker를 실행해야 한다.
4. `GET .../imports/:id`로 상태와 progress를 확인한다. progress는 단계 표시이며 측정된 전송 백분율이 아니다. `approved`이면 asset ID가 반환된다.
5. failed는 안전한 errorCode와 retryAt을 제공한다. retryAt 이후 `POST .../retry`로 재시도하며 총5회까지만 검증한다. queued/processing 취소는 `POST .../cancel`; approved 이후 취소는 지원하지 않는다.

업로드 상태는 uploading→queued→processing→approved 또는 failed/cancelled이다. 파일은 검증 전 quarantine에 남는다. Worker crash는 lease 만료 후 복구할 수 있고 취소·만료된 worker는 승인할 수 없다. 네트워크 중단 때 동일 key/payload를 유지하면 중복 등록을 피할 수 있다. 실패의 상세 서버 내부 trace를 클라이언트에 제공하지 않는다.

## 권리와 공개 범위

작품 권리는 코드 라이선스와 독립이다. 소유자, license, credit, validity와 nested display/download/export 등 full OES rights를 제공해야 한다. 임의의 flat boolean grant나 잘못된 기간은 거부한다. 별도 원본 download는 현재 유효한 download 권한과 작품 접근 권한을 요구한다. export-check는 export 자격 검사이며 OEX 파일을 만드는 기능이 아니다.

`approved`는 제한된 파일 검사를 통과했다는 뜻이다. 공개 전시를 허가하거나 anonymous URL을 발급하지 않는다. display와 download/export 권한은 독립이다. 원본 URL 제한과 향후 watermarked derivative는 브라우저에서 이미 받은 데이터를 복제할 수 없도록 보장하는 DRM이 아니다. Watermarked derivative와 실제 전시 공개 흐름은 아직 후속 작업이다.

## 보존과 복구

취소·실패·복구 과정에서 job staging/approved bytes를 자동 삭제하지 않는다. 보존 정책은 별도 운영 검토 대상이다. Git 백업만으로 database rows·object bytes·local credential/config를 복원할 수 없다. 관리자는 [일관된 DB/object 복구 절차](https://github.com/ExhibitOS/platform/blob/main/docs/storage.md)를 사용하고 실제 작품 도입 전에 새 환경에서 복원을 검증해야 한다. 이 안내의 합성 데이터 검사 결과는 실제 작품의 production 백업을 뜻하지 않는다.
