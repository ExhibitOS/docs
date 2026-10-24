# ExhibitOS docs

저장소별 책임·빌드 경계는 [아키텍처 정본](https://github.com/ExhibitOS/platform/blob/main/docs/architecture.md#repository-roles-build-boundaries)을 참조합니다. 이 저장소는 사용자·개발자 안내이며 아래 소스 개발 절차를 설치 사용자의 필수 준비물로 확대하지 않습니다.

## Product names

The capture app is **ExhibitOS Capture** (previously CaptureSpike); the macOS processing app is **ExhibitOS Processing** (previously Mac Processing). These are user-facing display names. Existing repository/source paths, command names, bundle identifiers, saved files and historical evidence retain their existing identifiers. Documentation naming does not establish that a newly named app package has shipped.


## GLB 중심 제작과 독립 실행 — 2026-10-21

ExhibitOS Capture와 ExhibitOS Processing은 선택적 제작 도구입니다. 지원되는 GLB가 있으면 두 앱의 설치·계정·서명·촬영 이력이나 OES/별도 메타데이터 파일 없이 Studio에서 작품을 만들 수 있습니다. 제목·작가·실측 치수·권한·출처는 Studio에서 입력하며, 사용자 제공 출처를 인증된 촬영 기록으로 간주하지 않습니다. Studio/Platform이 전시 구성과 새 OEX 내보내기를 담당하며 기존 OEX 가져오기는 유지합니다. 공개 컴포넌트는 비공개 앱/operations 저장소 없이 자체 빌드·운영하는 경계를 유지합니다. 설정한 자체 서버·DB·계정을 사용하며 중앙 ExhibitOS 계정을 요구하지 않습니다. 실제 설치·지원 제한과 남은 검증은 각 버전의 안내를 따르세요. [GLB 가져오기](artist/import.md)로 시작할 수 있습니다. 역할 결정은 새 UI·공식 배포 완료를 뜻하지 않습니다.

> 최신 1차 범위: [iPhone 촬영 → Mac 최종 처리](artist/mac-processing-first-release.md). 과거 지원 후보나 iPhone 최종 처리 안내보다 이 사용자 결정이 우선합니다. 실제 통과 범위는 각 검사 기록을 확인하세요.

User and developer documentation. 작가, 큐레이터, 기관, 개발자와 self-host 운영자의 공개 가능한 사용법 및 기여 안내를 담당한다.

## 여기서 시작하세요

[처음 시작하기](start-here.md)에서 목적에 맞는 준비·실행·확인·문제 해결을 찾으세요. Manager의 브라우저 Studio 연결과 호환 파일 경로를 설명하며 정식 다운로드·스토어·설치 검증이 완료된 것으로 안내하지 않습니다.

| 목적 | 안내 |
| --- | --- |
| 작품 등록·검토 | [Import](artist/import.md) · [CMS](artist/cms.md) |
| 전시 공간 편집·공개 | [Studio](artist/studio.md) |
| 목록·3D·소리·함께 관람 | [관람 안내](viewer/visit.md) |
| 초안·소스·서비스 복원 | [백업 선택](operator/backup.md) |
| 역할별 가이드 | [작가](guides/artist.md) · [큐레이터](guides/curator.md) · [기관](guides/institution.md) |
| 동의·읽기·운영 | [개인정보](guides/privacy.md) · [접근성](guides/accessibility.md) · [self-host/hosted](guides/self-host.md) |
| 개발·커뮤니티 | [개발](developer/development.md) · [기여](developer/contributing.md) · [번역](developer/translation.md) · [template 권리](developer/template-rights.md) |
| 문서만으로 실행할 reference 검사 | [설치·export·복원 절차/실행 결과](docs-validation.md) |
| 개발판 기능과 검증 제한 | [지원 범위·공개 소스 색인](status.md) |

이 저장소는 사용법 문서이며 제품 runtime이나 자동 테스트 suite를 포함하지 않습니다. 개발판에 구현된 기능, 기본 브랜치에 반영된 기능과 실제 출시·기기 검증은 구분합니다. 실행 환경과 검사 명령은 사용하는 제품 revision의 README를 따릅니다.

## 책임과 계약

spec/platform/manager/deployment의 공개 계약과 검증된 사용법을 설명한다.

이 저장소는 GitHub에서 공개되어 있다. operations 및 Capture 저장소는 빌드·설치·CI 의존성이 될 수 없다. private submodule, private package와 secret을 필수 조건으로 추가하지 않는다. 라이선스 범위는 아래 고지와 license-map.json을 따른다.

## 구현 순서

제품별 실제 사용법과 공통 문서·기여 양식을 기존 지원 범위에서 유지한다.

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
