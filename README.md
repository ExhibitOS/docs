# ExhibitOS docs

User and developer documentation. 작가, 큐레이터, 기관, 개발자와 self-host 운영자의 공개 가능한 사용법 및 기여 안내를 담당한다.

## 현재 상태

2026-10-01 기준 공개 Platform의 인증된 단일 GLB/PNG import API가 구현·검증되었다. [작가용 import 안내](artist/import.md)는 서버 권한, quarantine, 실패·재시도와 원본 제한을 설명한다. [Artist CMS](artist/cms.md)는 인증된 작가·작품 등록과 치수·권리·revision 검토, 제한된 GLB/PNG display 미리보기를 제공한다. [Studio 로컬 초안과 공간 편집](artist/studio.md)은 계정 없는 방·평면 표면·사각 개구부·문 연결·재질 편집과 제한된 3D 미리보기, JSON 편집·오프라인 준비·이력·파일 복원과 선택적 ETag 서버 동기화의 개발 안내다. 승인된 CMS 작품의 실제 치수 배치·벽 정렬·조명·관람 설정도 구현·검증되었으며 같은 Studio 안내에 사용 절차와 제한을 기록한다. 저장된 서버 revision의 READY 검사·명시적 immutable 공개·철회와 제한된 anonymous preview는 독립 검증 중인 T03-04 후보이며 같은 안내에 후보 절차를 기록한다. 전체 Viewer·Runtime·OES/OEX 패키지 import는 후속 구현이다. 이 저장소는 문서 저장소로 별도의 제품 runtime이나 자동 테스트 suite가 없다.

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
