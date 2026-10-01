# Artist CMS: 작품 정보·권리·파일 검토

2026-10-01. [Platform PR9](https://github.com/ExhibitOS/platform/pull/9)의 병합된 CMS를 설명한다. 별도 checkout의 실제 PostgreSQL·Chromium 검사로 핵심 흐름을 확인했다. ExhibitOS contributors. 문서 CC-BY-4.0, 실행 예제 Apache-2.0.

## 로그인과 작가 identity

운영자가 [Platform 인증 설정](https://github.com/ExhibitOS/platform/blob/main/docs/auth.md)에 따라 계정을 발급하고 서버를 구성한다. 웹의 `/cms`를 열고 기관 UUID, 계정과 비밀번호로 로그인한다. 현재 self-signup·비밀번호 복구·외부 OIDC는 지원하지 않는다. CMS는 로그인 비밀번호를 browser localStorage에 저장하지 않는다.

작가 탭에서 이름·소개를 등록한다. 작가 identity ID는 로그인 사용자 ID와 별개이며 한 계정에 여러 작가 identity를 연결할 수 있다. Admin은 같은 기관의 다른 사용자에게 새 작가를 연결할 수 있다. 다른 기관의 사용자 연결은 서버에서 거부한다. 기존 작가의 로그인 소유자 변경 UI는 제공하지 않는다.

Artist는 자신에게 연결된 작가·작품을 관리하고 admin은 같은 기관의 관리 권한을 가진다. Curator의 전시 배정은 해당 작품의 display 접근에만 사용되며 다른 작가의 CMS 편집 권한을 만들지 않는다. 서버가 tenant·membership·소유자·세션·권리를 다시 검사한다.

## 작품 등록과 치수·출처

작품 탭에서 새 작품을 만들고 작가, 제목·설명, 미터 단위 너비·높이·깊이를 입력한다. 각 치수는 양수여야 한다. PNG 평면 작품에도 두께를 기록한다. 원본 단위(m/cm/mm), 이미 단위 변환을 적용했는지, 출처·변환 메모와 사람 제작/AI 보조/AI 생성 표시를 기록한다. 이 정보는 사실에 맞게 직접 검토한다. CMS는 실제 치수를 촬영·측정하거나 원본 파일을 자동 단위 변환하지 않는다.

원래 generic metadata로 등록된 작품은 strict CMS metadata로 변환하기 전 승인할 수 없다. 잘못된 치수·rights·provenance는 서버가 거부한다. 수정은 현재 revision과 함께 제출하고 새로운 immutable snapshot을 남긴다. 다른 편집으로 revision이 바뀌면 충돌 오류와 미저장 입력을 유지한다. 이전 revision과 비교한 뒤 명시적으로 서버 내용을 새로 읽거나 다시 적용한다. 새로 읽으면 현재 미저장 입력이 대체되므로 먼저 확인한다.

## 권리와 원본 정책

권리자, 소유/허가 근거, license ID 또는 license 전문, credit line을 기록한다. display/download/export/commercial은 독립 선택이다. validity를 지정하면 UTC timestamp와 유효한 기간을 사용한다. Artwork metadata 권리 수정은 현재 연결 asset 권리에도 반영된다. 기존 승인 revision은 수정 후 다시 검토해야 한다.

전시만 허용하면 download와 export를 끈다. 원본 접근 확인 버튼은 실제 서버의 원본 download 정책을 검사하며 허용되는 경우 파일을 전달한다. export 확인은 자격만 검사하며 OEX를 생성하지 않는다. 승인된 display 사본을 볼 수 있어도 원본 download/export를 허용받은 것은 아니다.

프로젝트 코드 AGPL은 작품에 자동 적용되지 않는다. 권리 고지는 선언이며 법적 권한을 대신 만들어주지 않는다. Browser에 받은 bytes는 복제될 수 있고 watermarked derivative의 geometry도 추출할 수 있으므로 DRM이나 암호학적 복제 방지를 약속하지 않는다.

## 파일 검사와 작품 revision 승인

[파일 import 안내](import.md)의 크기·MIME·hash·quarantine 제한을 따른다. 최대32MiB의 GLB/PNG를 선택하고 scaleMeters를 기록한다. 같은 업로드를 재시도할 때 기존 job을 이어받는다. payload가 바뀐 새 등록은 기존 job을 취소/종료한 뒤 명시적으로 시작한다. 이 재시도 정보는 현재 화면의 memory에 있으며 browser 종료 후에는 API의 기존 job 상태를 확인해야 한다.

Worker가 동작해야 queued가 처리된다. failed는 error와 retryAt을 확인하고 재시도한다. 취소와 실패는 실제 파일을 자동 삭제하지 않는다. 파일 `approved` 상태와 작품의 검토 승인 revision은 별개이다.

파일 목록을 새로 읽고 승인된 asset을 선택한 뒤 치수·권리·출처를 검토해 현재 revision을 승인한다. Revision+metadata+asset hash+rights revision이 immutable 승인 기록에 묶인다. 현재 치수나 권리 등을 수정하면 전시 승인을 다시 받아야 한다. 승인은 anonymous publication이나 URL 공유를 수행하지 않는다.

## 전시용 미리보기

PNG 사본에는 diagonal stripes watermark와 최대512px 너비 제한이 적용된다. GLB에는 붉은 geometry stripes가 추가된다. GLB의 첫 display profile은 단일 default scene, 모든 node/mesh가 그 scene에 연결된 정적 모델이며 node transform은 identity여야 한다. Animation·skin·morph/weights·외부 URI·texture·extension은 지원하지 않는다. Scene에서 mesh 재사용을 포함해 POSITION vertices 500,000개, index entries 1,500,000개, primitive draw calls 256개까지 제한한다. Import가 파일 형식 검사를 통과했어도 CMS display profile에 맞지 않으면 작품 승인이 거부될 수 있다. 원본을 보존하고 호환 사본을 준비한다.

미리보기는 서버가 현재 display 권리·기간·승인 revision·asset integrity를 다시 검사해 내보낸 display 사본만 사용한다. 오류 시 원본으로 대체하지 않는다. GLB는 회전 버튼을 제공하고 WebGL 지원이 없으면 제목·설명·치수를 읽는 경로를 유지한다. 이는 전체 Viewer·Studio·전시 공개 구현이 아니다.

## 검색·보관·복원

작품 제목 검색과 더 보기 pagination을 사용한다. 작가·작품의 이전 revision을 비교할 수 있다. 보관은 soft archive이며 파일과 snapshot을 삭제하지 않는다. 보관된 항목을 선택하면 복원할 수 있다. 활성 작품이 연결된 작가를 먼저 보관할 수 없으므로 작품의 보관 상태부터 검토한다. 보관과 복원도 revision을 변경하고 작품의 전시 재검토가 필요하다.

브라우저 편집은 backup이 아니다. 운영자는 [DB/object 복구 절차](https://github.com/ExhibitOS/platform/blob/main/docs/storage.md)에 따라 metadata·rights·job·derivative inventory를 같은 시점에 보존해야 한다. Git 백업에 실제 작품 bytes나 credentials가 들어간다고 가정하지 않는다.

구체적인 API 필드·오류·role 범위는 [CMS OpenAPI](https://github.com/ExhibitOS/platform/blob/main/contracts/cms-openapi.json)와 [CMS 개발 안내](https://github.com/ExhibitOS/platform/blob/main/docs/cms.md)를 따른다.
