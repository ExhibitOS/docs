# ExhibitOS docs

User and developer documentation. 작가, 큐레이터, 기관, 개발자와 self-host 운영자의 공개 가능한 사용법 및 기여 안내를 담당한다.

## 여기서 시작하세요

[역할별 시작 안내](start-here.md)에서 목적에 맞는 절차를 찾으세요.

| 목적 | 안내 |
| --- | --- |
| 작품 등록·검토 | [Import](artist/import.md) · [CMS](artist/cms.md) |
| 전시 공간 편집·공개 | [Studio](artist/studio.md) |
| 목록·3D·소리·함께 관람 | [관람 안내](viewer/visit.md) |
| 초안·소스·서비스 복원 | [백업 선택](operator/backup.md) |
| 개발판 기능과 검증 제한 | [지원 범위·공개 소스 색인](status.md) |

이 저장소는 사용법 문서이며 제품 runtime이나 자동 테스트 suite를 포함하지 않습니다. 개발판에 구현된 기능, 기본 브랜치에 반영된 기능과 실제 출시·기기 검증은 구분합니다. 실행 환경과 검사 명령은 사용하는 제품 revision의 README를 따릅니다.

## 책임과 계약

spec/platform/manager/deployment의 공개 계약과 검증된 사용법을 설명한다.

이 저장소는 GitHub에서 공개되어 있다. operations 및 Capture 저장소는 빌드·설치·CI 의존성이 될 수 없다. private submodule, private package와 secret을 필수 조건으로 추가하지 않는다. 라이선스 범위는 아래 고지와 license-map.json을 따른다.

## 구현 순서

제품 task별 사용법을 보완하고 T11-04에서 공통 문서·community template을 검증한다.

제품 저장소의 README가 toolchain과 실제 검사 명령의 기준이다. 각 task의 검증된 기능과 오류 경로를 공개 사용법에 반영한다. 링크·예제 명령, 새 환경 quickstart, 접근성 보기, 기여 안내와 비공개 자료 노출 여부를 검사한다.

이 문서 저장소에는 제품 build/test 명령이 없다. Platform의 실행과 검사는 [공개 README](https://github.com/ExhibitOS/platform/blob/main/README.md)를 따른다. 이 문서 변경은 `git diff --check`와 tracked tree/의존 경계 검토로 확인한다.

## 기여와 보안 보고

작업 전 [AGENTS.md](AGENTS.md)를 읽고 `codex/<작업명>` 브랜치와 PR로 변경한다. 일반 문제는 이 저장소의 Issue/PR에서 다룬다. 취약점·토큰·비공개 작품을 일반 Issue에 게시하지 않는다. GitHub private vulnerability reporting이 활성화돼 있으면 사용하고, 없으면 조직 관리자에게 비공개 보고한다. 아직 전용 보안 연락처나 security reporting 기능이 설정됐다고 가정하지 않는다.

기획·상태 조정 자료는 접근 권한이 있는 에이전트가 operations에서 확인한다. 제품의 빌드와 배포는 이 운영 문서 없이 실행할 수 있어야 한다.

## 검토 중인 프로젝트 정책

[초기 라이선스·공개·CI 비용 정책 제안](developer/license-policy-proposal.md)은 정책 선택의 연구 기록이다. 현재 이 저장소의 적용 범위는 아래 LICENSE를 따른다.

## 라이선스

프로젝트 소유 설명문·도표는 **CC-BY-4.0**, 실행 가능한 fenced 예제와 코드·설정·스크립트는 **Apache-2.0**입니다.
[적용 범위](LICENSE), [기계가 읽는 범위 매핑](license-map.json),
[CC BY 원문](LICENSES/CC-BY-4.0.txt), [Apache 원문](LICENSES/Apache-2.0.txt)을 확인하세요.
문서를 공유할 때 제공된 저자/저작권/면책 정보, 원본 URL과 license 링크를 유지하고 변경을 표시합니다.
외부 인용·코드·media는 원래 조건을 유지하며 프로젝트 license가 사용자 작품이나 상표를 허가하지 않습니다.
