# 지원 범위와 공개 소스 색인

> 최신 1차 범위: [iPhone 촬영 → Mac 최종 처리](artist/mac-processing-first-release.md). 과거 지원 후보나 iPhone 최종 처리 안내보다 이 사용자 결정이 우선합니다. 실제 통과 범위는 각 검사 기록을 확인하세요.

## 현재 제작 경로와 제공 상태 · 2026-10-25

현재 제작 방향은 Mac Manager 안의 네이티브 편집과 Docker 없는 개인 작업 공간입니다. 기존 브라우저 Studio·서버 절차는 아래 날짜가 있는 호환 안내로 보존합니다. 소스 구현, 개발 앱 생성, 실제 조작 확인, 공식 설치·배포와 사람의 수락은 서로 다릅니다.

| 대상 | 확인된 범위 | 아직 제공·확인되지 않은 범위 |
| --- | --- | --- |
| Manager | 네이티브에서 외부 GLB·PNG 등록, 권리·치수 입력, 배치·저장·다시 열기, OEX·정적 Viewer 출력의 한정된 실제 확인 | 정식 서명·공증 다운로드, 새 컴퓨터 설치 전체 수락, 모든 편집·충돌·접근성 검증 |
| ExhibitOS Processing | 로컬 개발판의 모델 중심 작업실·모드 전환·일부 편집 상태를 한정된 실제 화면에서 확인; 기존 편집·GLB 결과는 해당 버전 범위에서 재사용 | 새 곡면 정리의 화면 갱신·Esc 취소 문제와 적용·저장·GLB 소비 확인, 전체 키보드·접근성 수락, 정식 서명·스토어 설치는 미완료입니다. |
| ExhibitOS Capture | 촬영 원본·EXCP를 Mac 처리 도구로 전달하는 선택 도구 | 일반 사용자 설치 경로와 최종 촬영 품질의 전체 수락 |
| Viewer | 홈페이지에서 제공하는 세 회화의 정적 관람 데모. 기본 입장·안내 건너뛰기 수정의 게시와 짧은 데스크톱 입장·작은 화면의 안내 닫기·초점 이동을 한정 확인; 제작 앱·API·DB·로그인 없이 관람 | 새 입장 연출의 디자인 수락, 물리 모바일·지속 보행 성능·전체 화질 및 사람의 수락 |
| 기존 자료 복구 | 기존 자료를 유지한 같은 후보의 취소·읽기 전용 원본 소유자 확인; 엔진 이용 불가 시 안전하게 거부. 과거 설치에서는 같은 백업의 격리 복원·검증 완료 | 실제 원본 소유자가 확인되는 정상 경로, 실패 후 freeze 복구·이전 자료 cold reopen 전체 수락. 엔진 연결 불가는 ‘정지 확인’이 아닙니다. |

정식 Manager 다운로드·Processing 스토어·Capture 일반 설치 링크는 아직 제공하지 않습니다. 로컬 개발 패키지를 공식 설치 앱으로 대체하지 않습니다. [처음 시작하기](start-here.md), [파일 제작](artist/studio.md), [관람](viewer/visit.md), [백업·복구](operator/backup.md)에서 현재 가능한 경로를 확인하세요. 공개 데모의 기술 확인과 모든 개발 UX·사람의 수락은 구분합니다.

홈페이지의 데모 진입은 Viewer만 제공합니다. 고흐·Rembrandt·Cézanne 세 회화의 출처는 Metropolitan Museum of Art Open Access이며 해당 파일의 CC0·출처 고지를 유지합니다. 기관의 제휴·보증을 뜻하지 않습니다. 홈페이지의 합성 소개 이미지와 실제 전시 작품을 구분합니다. 작품·음원은 각각 제공된 출처·라이선스·변경 표시를 확인하며, 프로젝트 코드 라이선스를 사용자 작품이나 음원에 적용하지 않습니다.

외부 도구의 지원 GLB·PNG는 Capture·Processing 설치나 영수증 없이 가져올 수 있습니다. 개인 로컬 제작과 별도 서버 운영·인터넷 공개의 계정·권한 조건은 구분합니다. Cloudflare Pages 정적 공개와 선택적 Render 서버·PostgreSQL은 배포별 실제 결과를 확인합니다.

Safari·Chrome이 대상이고 macOS·iOS가 공식 검증 대상입니다. 물리 기기 검사 전 지원 완료를 뜻하지 않습니다. Windows/Linux Chrome은 호환 후보입니다. Windows/Linux 네이티브·Android·iPhone 최종 처리·Node 재구성·범용 원격 배포·XR/Federation/기관 고급 연동은 보류입니다. 출입구 마감·명판·벤치의 기본 제작 범위는 이 고급 기능 보류에 포함하지 않습니다.

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
