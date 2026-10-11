# 공개 소스 개발과 계약 확인

사용하는 exact revision의 README와 LICENSE를 기준으로 합니다. 이 문서 저장소는 runtime, npm package, 제품 suite 또는 설치 파일을 포함하지 않습니다. 비공개 Capture/operations 코드를 복사하거나 설치/CI 필수 의존성으로 추가하지 않습니다.

[Platform](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/README.md)은 Node24.21.0/npm11.19.0에서 `npm ci`, `npm run build`를 실행한 뒤 개발 API/웹을 시작합니다. [Spec](https://github.com/ExhibitOS/spec) 공개 package/schema/fixture가 OES/OEX/OED 형식 기준입니다. [Manager](https://github.com/ExhibitOS/manager)와 [Deployment](https://github.com/ExhibitOS/deployment)는 각각 설치 lifecycle과 배포 adapter를 담당합니다. 원본 byte 보존, 미터 단위, current rights/approval과 idempotent 실패 복구를 바꾸지 않습니다.

Platform 변경은 현재 README의 typecheck/lint/unit/build와 영향 범위의 실제 API/DB/브라우저 검사로 확인합니다. 서로 다른 환경 결과를 섞거나 mock을 실제 device/cloud/API 통과로 쓰지 않습니다. 원본 hash·source revision·명령·exit/result·미실행 한계를 기록합니다. build 성공은 physical ARscale나 작품 색 품질 검증이 아닙니다.

API 입력의 role/tenant를 신뢰하지 말고 서버 session·현재 membership·resource scope·Origin/Host/CSRF를 사용합니다. approval·display·download·export·AI 전송 동의는 독립입니다. source metadata와 human/AI 제안은 분리하고 review 없이 publish하지 않습니다. 서버 backup과 operator 삭제는 HTTP 권한을 가진 사용자의 임의 실행 기능이 아닙니다.

[PR51](https://github.com/ExhibitOS/platform/pull/51)은 기관/XR/federation, [PR52](https://github.com/ExhibitOS/platform/pull/52)는 privacy·reviewed assistance·preservation의 소스 참조입니다. 이는 해당 컴포넌트 통합 기록이며 전체 출시·외부 AI 실행·실기기 qualification 선언이 아닙니다. [현재 지원 범위](../status.md)와 [기여 절차](contributing.md)를 확인하세요.
