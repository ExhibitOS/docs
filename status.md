# 지원 범위와 공개 소스 색인

확인 기준: 2026-10-03. 아래 링크는 공개 Platform 개발 snapshot `2dacde22e7dd3da1e9fa5d580024cec557c3f59b`에 고정합니다. 개발 브랜치의 기능이 기본 브랜치·배포판에 이미 포함됐다는 뜻은 아닙니다. 최신 실행에는 선택한 revision의 README와 변경 이력을 함께 확인하세요.

## 기능과 남은 조건

| 범위 | 개발 구현 | 남은 조건 |
| --- | --- | --- |
| CMS·Studio | 권리 승인·로컬 초안·공간/작품 배치·서버 revision·명시적 공개/철회 | 실제 운영 배포와 사용 환경별 qualification |
| Viewer | 목록·3D 로딩·보행·음성·대본·접근성 대체 보기 | 물리 모바일/GPU·전체 성능·전체 적합성 인증 |
| 고급 관람 | 큐레이션·공간 스크립트·presence·명시적 오프닝 동의 | 새 조작의 실물 VoiceOver·장거리 음성 연결·출시 통합 |
| 패키징·보존 | OEX·freeze/offline·일관된 서비스 백업 | 실제 운영 dataset와 provider별 복원 검증 |
| Capture·Manager | 별도 제품 범위 | 실제 iPhone 연결/서명·센서와 Windows/native GUI 검증 |

문서·합성 테스트·빌드 성공을 실기기 검사나 production 출시로 대체하지 않습니다. 웹사이트 도메인 연결과 Cloudflare 배포도 현재 보류이며 실제 공개 사이트가 동작한다고 가정하지 않습니다.

## 유지할 공개 참조

| 내용 | 고정된 소스 |
| --- | --- |
| 실행·toolchain·검사 | [README.md](https://github.com/ExhibitOS/platform/blob/2dacde22e7dd3da1e9fa5d580024cec557c3f59b/README.md) |
| 보행 조작·충돌 한도 | [docs/viewer-navigation.md](https://github.com/ExhibitOS/platform/blob/2dacde22e7dd3da1e9fa5d580024cec557c3f59b/docs/viewer-navigation.md) |
| 목록·키보드·접근성 | [docs/viewer-accessibility.md](https://github.com/ExhibitOS/platform/blob/2dacde22e7dd3da1e9fa5d580024cec557c3f59b/docs/viewer-accessibility.md) |
| 오프닝·마이크·가이드 동의 | [docs/opening.md](https://github.com/ExhibitOS/platform/blob/2dacde22e7dd3da1e9fa5d580024cec557c3f59b/docs/opening.md) |
| 큐레이션·대본·안전 viewpoint | [docs/studio-curation.md](https://github.com/ExhibitOS/platform/blob/2dacde22e7dd3da1e9fa5d580024cec557c3f59b/docs/studio-curation.md) |
| 서비스 백업·새 환경 복원 | [docs/storage-service-backup.md](https://github.com/ExhibitOS/platform/blob/2dacde22e7dd3da1e9fa5d580024cec557c3f59b/docs/storage-service-backup.md) |
| 오디오·상세 설계 결정 | [docs/adr/0011-viewer-audio-detail.md](https://github.com/ExhibitOS/platform/blob/2dacde22e7dd3da1e9fa5d580024cec557c3f59b/docs/adr/0011-viewer-audio-detail.md) |

공개 규격은 [Spec](https://github.com/ExhibitOS/spec), 설치 수명주기는 [Manager](https://github.com/ExhibitOS/manager), 배포 계약은 [Deployment](https://github.com/ExhibitOS/deployment)의 README에서 시작합니다. 이 문서는 비공개 Capture/운영 저장소를 설치나 빌드 조건으로 사용하지 않습니다.

문서 갱신자는 실제 소스를 확인한 뒤 snapshot 링크와 기능·제한을 함께 갱신합니다. 검증하지 않은 절차나 배포 URL은 완료된 사용법으로 추가하지 않습니다. 문서 기여·권리 고지는 [README](README.md)를 따릅니다.
