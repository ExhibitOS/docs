# 작가용 작품 import 안내

## 현재 Mac 네이티브 파일 등록

지원 GLB·PNG를 Manager의 네이티브 편집에서 선택하고 제목·작가·실측 치수·권리·출처를 입력합니다. PNG 회화의 물리적 두께를 모르면 비워 둡니다. 저장 후 다시 열어 정보·배치를 확인하고 [전시 제작](studio.md)으로 이어갑니다. Capture·Processing·별도 OES 파일이나 스토어 영수증은 기본 수용 조건이 아닙니다. 파일의 무결성·형식 검사는 품질·실측·공개 권리의 인증이 아닙니다.

## 기존 브라우저에서 파일 선택으로 시작하기

**목표:** 지원되는 GLB로 비공개 작품을 만들고 Studio에서 정보·권한·출처를 관리합니다. ExhibitOS Capture와 ExhibitOS Processing은 선택적 제작 도구입니다. 지원되는 GLB가 있으면 두 앱의 설치·계정·서명·촬영 이력이나 OES/별도 메타데이터 파일 없이 Studio에서 작품을 만들 수 있습니다. 제목·작가·실측 치수·권한·출처는 Studio에서 입력하며, 사용자 제공 출처를 인증된 촬영 기록으로 간주하지 않습니다.

1. 작품 관리에서 작가·작품을 만들거나 선택하고 제목·설명·치수·권리·출처를 확인합니다.
2. Processing 또는 다른 촬영·모델링 프로그램에서 만든 지원 `.glb`를 선택해 전송합니다. 원본은 보존합니다. OES 폴더를 만들거나 `.oex`로 포장할 필요가 없습니다.
3. 전송·형식 검사·등록 상태를 구분해 확인합니다. 대기 상태가 지속되면 현재 설치의 처리 도구 상태를 확인합니다.
4. 실제 파일과 작품 정보를 검토합니다. 파일 검사 통과는 작품·공개 승인이 아닙니다.

**확인:** 해당 작품의 파일과 검사 결과가 보이고 현재 정보·권리·파일을 검토할 수 있어야 합니다. 오류가 있으면 이유와 현재 지원 규격을 확인하고 실패한 단계만 재시도하세요.

현재 입력 계약·지원 텍스처·패키지·크기 한도는 [사용하는 버전의 파일 가져오기 안내](https://github.com/ExhibitOS/platform/blob/main/docs/imports.md)를 따릅니다. 아래 2026-10-01 API 기록은 초기 profile의 역사적 참고이며 최신 지원 한도를 대신하지 않습니다.

새 OEX는 전시 편집 후 Studio에서 내보냅니다. 기존 OEX 가져오기는 별도의 전시 교환 경로로 유지됩니다. 현재 UI는 작품을 먼저 만들고 GLB를 올리는 순서이며, 파일 선택으로 시작하는 새 화면이 이미 배포됐다고 가정하지 마세요. GLB의 파일 검사 통과와 작품 검토·공개 승인은 구분합니다.

## 초기 API 참고 기록


2026-10-01. ExhibitOS contributors. 문서 CC-BY-4.0, 실행 예제 Apache-2.0. 이 안내는 [Platform PR8](https://github.com/ExhibitOS/platform/pull/8)의 구현된 API를 설명한다. 작가·작품 생성과 파일 검토 UI는 [Artist CMS 안내](cms.md)를 따른다. 전체 OES/OEX package 또는 Capture 원본을 import하는 기능은 아직 제공하지 않는다.

## 시작 조건

관리자가 [Platform README](https://github.com/ExhibitOS/platform/blob/main/README.md)와 [인증 안내](https://github.com/ExhibitOS/platform/blob/main/docs/auth.md)에 따라 로컬 서버와 PostgreSQL/object storage를 구성해야 한다. 로그인은 tenant를 선택하며 작가의 작품 소유 관계는 로그인 사용자와 별도로 관리한다. 이 import API는 기존 artwork에 단일 primary asset을 추가한다. 새 작가·작품은 CMS에서 먼저 등록한다. 공개 signup·비밀번호 복구는 현재 지원하지 않는다.

작품 소유 작가 또는 해당 tenant admin만 import를 생성하고 읽고 취소·재시도할 수 있다. 큐레이터와 관람자 역할은 이 권한을 얻지 않는다. 다른 tenant의 admin 권한은 사용할 수 없다. 로그인 세션과 모든 변경의 Origin/Host/CSRF 검사는 서버에서 수행한다.

## 지원 파일과 물리 크기

단일 GLB2 또는 PNG를 최대32MiB까지 받는다. GLB는 외부 URI·image·texture·extension 없이 self-contained여야 한다. PNG는 non-interlaced8-bitRGB/RGBA, 최대4,194,304pixels, 각 변8192이하이며 ancillary metadata를 받지 않는다. JPEG/WebP, remote URL과 archive는 지원하지 않는다. 폭넓은 일반 glTF 지원을 뜻하지 않으므로 오류 시 원본을 보존하고 호환되는 사본을 준비한다.

등록 값 `scaleMeters`는 양수(최대1,000,000)여야 한다. 이는 전체 작품의 width/height/depth나 provenance 편집을 대체하지 않는다. CMS에서 치수와 단위 변환 기록을 별도로 검토한다.

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

`approved`는 제한된 파일 검사를 통과했다는 뜻이다. 공개 전시를 허가하거나 anonymous URL을 발급하지 않는다. display와 download/export 권한은 독립이다. 원본 URL 제한과 향후 watermarked derivative는 브라우저에서 이미 받은 데이터를 복제할 수 없도록 보장하는 DRM이 아니다. CMS는 watermarked display derivative를 제공한다. 실제 전시 공개 흐름은 후속 작업이다.

## 보존과 복구

취소·실패·복구 과정에서 job staging/approved bytes를 자동 삭제하지 않는다. 보존 정책은 별도 운영 검토 대상이다. Git 백업만으로 database rows·object bytes·local credential/config를 복원할 수 없다. 관리자는 [일관된 DB/object 복구 절차](https://github.com/ExhibitOS/platform/blob/main/docs/storage.md)를 사용하고 실제 작품 도입 전에 새 환경에서 복원을 검증해야 한다. 이 안내의 합성 데이터 검사 결과는 실제 작품의 production 백업을 뜻하지 않는다.
