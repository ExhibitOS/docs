# 지원 범위와 공개 소스 색인

> 최신 1차 범위: [iPhone 촬영 → Mac 최종 처리](artist/mac-processing-first-release.md). 과거 지원 후보나 iPhone 최종 처리 안내보다 이 사용자 결정이 우선합니다. 실제 통과 범위는 각 검사 기록을 확인하세요.

## 현재 1차 방향과 실제 배포 상태 · 2026-10-17

일반 시작 경로는 [처음 시작하기](start-here.md)에서 확인합니다. Manager의 환경 준비→설치→시작→브라우저 Studio, 작품 가져오기→배치→저장→관객 미리보기→공개 준비와 Viewer의 관람 시작 흐름으로 안내를 갱신했습니다. 문서 갱신을 실제 새 컴퓨터 설치·정식 앱 배포·실기기·전체 품질 검증으로 계산하지 않습니다.

- **Manager:** Mac용 Developer ID 서명·Apple 공증 후 웹사이트 배포 방향. 정식 배포판·신규 컴퓨터 설치 자격 검증은 미완료입니다. 인증서 없는 로컬 소스 빌드는 별도 개발 경로입니다.
- **Capture / Mac Processing:** 선택 도구입니다. iPhone 원본 전달→Mac 최종 재구성·검토·내보내기를 사용하며 공식 Mac Processing 스토어 배포와 Capture 일반 설치는 준비 중입니다. Platform은 호환 파일로 독립 사용할 수 있습니다.
- **인터넷 전시:** Cloudflare Pages 정적 단독과 선택적 Render 동적 서버·Render PostgreSQL. 로컬 제작에 계정·토큰은 필요하지 않습니다. 실제 원격 배포와 복원 증거는 사용하는 버전의 기록을 확인해야 합니다.
- **관람:** Safari·Chrome 대상, 공식 검증 환경은 macOS·iOS. Windows·Linux Chrome은 호환 후보이고 해당 OS의 실제 검사 전 지원 완료로 표시하지 않습니다.
- **보류:** Windows/Linux 네이티브·Android·iPhone 최종 처리·Node 재구성·범용 원격 배포·XR/Federation/기관 고급 연동은 1차 필수 대상이 아닙니다. 기존 구현·결과는 보존합니다.

정적 Viewer·Studio 체험은 별도 API·DB·로그인·토큰 없이 제공하는 방향이며 이 문서에는 확인되지 않은 데모 URL을 넣지 않습니다. 현재 홈페이지와 사용 안내는 제품 정식 배포판 자체가 아닙니다.

## 과거 개발 snapshot과 근거

아래 2026-10-11 표·고정 링크는 당시 구현·검사의 역사적 참조입니다. 최신 지원/출시 선언이나 보류 환경을 현재 필수로 되돌리는 근거로 쓰지 않습니다.

확인 기준: 2026-10-11. 아래 링크는 공개 Platform 개발 snapshot `6663912e4cdaf205cbc648551f4a0bb55b6f0293`에 고정합니다. 개발 브랜치의 기능이 기본 브랜치·배포판에 이미 포함됐다는 뜻은 아닙니다. 최신 실행에는 선택한 revision의 README와 변경 이력을 함께 확인하세요.

## 기능과 남은 조건

| 범위 | 개발 구현 | 남은 조건 |
| --- | --- | --- |
| CMS·Studio | 권리 승인·로컬 초안·공간/작품 배치·서버 revision·명시적 공개/철회 | 실제 운영 배포와 사용 환경별 qualification |
| Viewer | 목록·3D 로딩·보행·음성·대본·접근성 대체 보기 | 물리 모바일/GPU·전체 성능·전체 적합성 인증 |
| 고급 관람 | 큐레이션·공간 스크립트·presence·명시적 오프닝 동의 | 새 조작의 실물 VoiceOver·장거리 음성 연결·출시 통합 |
| 패키징·보존 | OEX·freeze/offline·일관된 서비스 백업 | 실제 운영 dataset와 provider별 복원 검증 |
| 기관/XR/federation | 제한된 기관 catalog/token·교육 경로, 명시적 WebXR/Quick Look, 등록된 federation source | 실제 AR/VR 물리 scale·원격/기관 운영 검증 |
| 개인정보/제안/보존 | 기본 opt-out 분석·본인 metadata export·명시 계정 처리·human/AI proposal review·기술 보존 inventory | actual external AI 호출 없음; 운영 backup/삭제와 전체 보존 corpus 검증 별도 |
| Capture·Manager | 별도 제품: iPhone 기본 영상/tracking/depth와 Windows lifecycle 실제 사용자 관찰 일부 있음 | 원본 촬영 품질·완전한 export pipeline/복원·OS 설치/서명 인수 검증 별도 |

문서·합성 테스트·빌드 성공을 실기기 검사나 production 출시로 대체하지 않습니다. 웹사이트/도메인의 상태는 제품 API hosted 운영·backup 또는 출시 qualification의 증거가 아닙니다. 이 문서 갱신에서는 live 사이트/Cloudflare 배포를 재검사하지 않았습니다.

## 유지할 공개 참조

| 내용 | 고정된 소스 |
| --- | --- |
| 실행·toolchain·검사 | [README.md](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/README.md) |
| 보행 조작·충돌 한도 | [docs/viewer-navigation.md](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/viewer-navigation.md) |
| 목록·키보드·접근성 | [docs/viewer-accessibility.md](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/viewer-accessibility.md) |
| 오프닝·마이크·가이드 동의 | [docs/opening.md](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/opening.md) |
| 큐레이션·대본·안전 viewpoint | [docs/studio-curation.md](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/studio-curation.md) |
| 서비스 백업·새 환경 복원 | [docs/storage-service-backup.md](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/storage-service-backup.md) |
| 오디오·상세 설계 결정 | [docs/adr/0011-viewer-audio-detail.md](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/adr/0011-viewer-audio-detail.md) |

공개 규격은 [Spec](https://github.com/ExhibitOS/spec), 설치 수명주기는 [Manager](https://github.com/ExhibitOS/manager), 배포 계약은 [Deployment](https://github.com/ExhibitOS/deployment)의 README에서 시작합니다. 이 문서는 비공개 Capture/운영 저장소를 설치나 빌드 조건으로 사용하지 않습니다.

문서 갱신자는 실제 소스를 확인한 뒤 snapshot 링크와 기능·제한을 함께 갱신합니다. 검증하지 않은 절차나 배포 URL은 완료된 사용법으로 추가하지 않습니다. 문서 기여·권리 고지는 [README](README.md)를 따릅니다.

## 2026-10-11 역할별 보완

[Platform PR51](https://github.com/ExhibitOS/platform/pull/51), [PR52](https://github.com/ExhibitOS/platform/pull/52)의 현재 구현을 [역할별 가이드](start-here.md)에 연결합니다. [기관](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/institution.md), [privacy](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/privacy.md), [assistance](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/assistance.md), [preservation](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/preservation.md), [XR](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/xr.md)가 해당 범위의 기준입니다. 초기 artist import/Studio 문서는 역사적 단계의 설명도 포함하므로 최신 codec/extension/권한 한도는 선택한 제품 revision의 계약을 확인합니다.

이 docs repository의 역할별 안내·community 양식 구현과 [문서-only 새 사용자 reference 검사](docs-validation.md)는 구분합니다. 후자는 2026-10-11 공개 Platform `ce0f4ab` 새 합성 환경에서 실제 명령과 CMS/Studio 브라우저 조작으로 설치·OEX·별도 DB/blob 복원·현재 권리 거부를 확인했습니다. 실패한 기본 Docker network 경로와 수정한 검사 driver 오류도 보존했습니다. 실사용자·물리 작품·기기/원격 hosted 결과나 전체 접근성 audit로 확대하지 않습니다. 운영 비용/후원·상표 사용·공식 hosted 서비스 조건은 소유자 결정이고 새 license/상표 허락으로 확정하지 않습니다.
