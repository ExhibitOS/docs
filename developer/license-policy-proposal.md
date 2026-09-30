# 초기 라이선스와 공개 범위 제안

상태: **검토용 제안, 아직 적용하지 않음**. 조사일: 2026-10-01.
이 문서는 저장소에 LICENSE를 추가하거나 공개 범위를 변경하지 않는다. 공식 원문의 조건을 구현·배포 작업에 연결하는 정책 초안이며 특정 결합의 법적 적합성이나 권리 소유를 보장하지 않는다.

## 저장소와 파일 범위

| 저장소/산출물 | 제안 | 적용 범위와 제외 |
| --- | --- | --- |
| platform core | AGPL-3.0-or-later | CMS, Studio, API, Realtime, Runtime과 아직 분리하지 않은 Viewer의 프로젝트 소유 코드·설정·빌드 스크립트 |
| 추후 독립 viewer SDK | MIT 검토 | 새로 작성하거나 모든 권리자가 허용한 독립 SDK만. 현재 platform 코드의 자동 예외가 아님 |
| spec validator·generator·test runner·build code | Apache-2.0 | 프로젝트가 소유하는 실행 코드와 코드 테스트 |
| spec schema·순수 synthetic fixture | CC0-1.0 | 명시된 데이터 파일만. test runner와 schema 생성기까지 CC0로 바꾸지 않음 |
| manager, deployment | Apache-2.0 | 프로젝트 소유 코드·설정·스크립트. 함께 배포하는 AGPL platform image는 원래 조건 유지 |
| 공개 docs의 설명문·도표 | CC-BY-4.0 | 프로젝트 소유 문서. 실행 예제 코드는 별도 Apache-2.0 표기 권고 |
| private Capture, operations | 공개 라이선스 부여 없음 | 프로젝트 소유 자료의 권리 보유. 포함된 third-party 라이선스 의무는 그대로 유지 |

이 표는 설계 선택이다. 공개 표준과 설치 도구의 재사용을 허용하면서 core 서비스 수정의 소스 제공을 유지하려는 목적이다. 작품·사진·음원·폰트·로고·외부 기여·vendored dependency는 blanket LICENSE로 재허가하지 않는다. GitHub owner 이름이 법적 권리자라는 뜻도 아니므로 copyright 주체는 기록을 확인한 뒤 표기한다.

## 공식 원문에서 가져온 조건

### AGPL-3.0-or-later

AGPL v3 §§4–6은 복사·수정·비소스 배포의 고지 및 Corresponding Source 조건을 정한다. §13은 수정한 프로그램과 원격 네트워크로 상호작용하는 이용자에게 그 버전의 Corresponding Source를 무료로 받을 기회를 눈에 띄게 제공하도록 한다. §14 및 적용 예시는 version 3 또는 이후 버전 선택을 지원한다. 릴리스 commit, 빌드·설치 스크립트와 배포 source 경로를 함께 유지하고 서비스 UI에 소스 접근 링크를 준비한다. [GNU 공식 AGPL 원문](https://www.gnu.org/licenses/agpl-3.0.txt)

독립 SDK를 MIT로 만들려면 코드 출처와 기여자 권한을 확인해야 한다. 파일을 다른 repo로 옮기는 것만으로 AGPL 조건이 없어지지 않는다. §5의 independent aggregate와 covered combined work 구분은 실제 결합에 달려 있다. public artifact/API 통신은 제품 설계 경계이며 라이선스 면제 보장은 아니다. [AGPL §§1,5,13](https://www.gnu.org/licenses/agpl-3.0.txt)

### Apache-2.0

§§2–3은 저작권·특허 허락을 정하고 특정 특허 소송에는 특허 허락 종료 조건을 둔다. §4의 재배포에는 원문 license 제공, 수정 파일의 변경 고지, 관련 저작권·특허·상표·출처 고지 보존 및 기존 NOTICE의 필요한 고지 전달이 포함된다. §6은 일반적인 상표 사용 허락을 부여하지 않는다. §5의 기여 조건과 별도 기여 계약도 확인한다. 재배포물마다 third-party 원문·NOTICE를 유지한다. [Apache 공식 원문](https://www.apache.org/licenses/LICENSE-2.0)

Apache component를 AGPL core와 결합할 때도 Apache 고지는 삭제하지 않는다. 별도 manager/deployment 라이선스가 bundled platform의 조건을 덮어쓰지 않는다. 결합물 배포 검토에서 각 파일의 원래 license와 core의 요구를 함께 확인한다.

### CC0-1.0

§§2–3은 허용되는 범위에서 저작권 및 관련 권리를 영구적으로 포기하고, 포기가 무효인 부분에는 fallback 허락을 정한다. §4는 특허·상표를 포기하거나 허락하지 않으며 다른 사람의 권리 정리를 보장하지 않는다. 따라서 스스로 권리를 부여할 수 있는 schema와 synthetic 데이터만 지정한다. 실제 작품·raw Capture·외부 sample의 재허가 수단으로 사용하지 않는다. [CC0 공식 원문](https://creativecommons.org/publicdomain/zero/1.0/legalcode.en)

### CC-BY-4.0

§3은 공유 시 제공된 저자·저작권·license·면책·원본 링크 정보를 유지하고 변경 여부 및 이전 변경 고지를 표시하도록 한다. §2는 하위 이용자의 허용된 권리를 제한하는 추가 조건·기술적 조치를 금지하고 특허·상표 허락을 부여하지 않는다. 문서 export에도 저자/프로젝트, 원본 URL, license URL, 변경 정보를 포함한다. third-party 이미지의 별도 조건은 각각 표시한다. [CC BY 공식 원문](https://creativecommons.org/licenses/by/4.0/legalcode.en)

### 독립 SDK의 MIT 후보

MIT 원문은 복사·수정·배포·판매 등을 허락하며 복사물 또는 중요한 부분에 copyright 및 permission notice를 유지하도록 한다. SDK 후보에 원문과 권리자 고지를 함께 제공한다. SDK 분리나 license 변경의 권한 확인을 대신하지 않는다. [MIT 원문](https://opensource.org/license/mit)

## 적용 PR의 파일 규칙

1. 승인된 정책은 repo별 LICENSE, 여러 license가 있으면 LICENSES 원문과 경로별 매핑에 구현한다. 이 제안 PR에는 license 원문을 추가하지 않는다.
2. 패키지 전체가 같은 조건일 때만 manifest의 license 필드로 표현한다. spec처럼 섞인 경우 파일/디렉터리별 범위를 문서화하고 SPDX header 또는 machine-readable 매핑을 둔다. JSON schema에는 invalid JSON 주석을 삽입하지 않는다.
3. docs의 prose/도표는 CC BY, fenced executable 예제와 실제 source 파일은 명시된 code license로 구분한다. 코드 예제의 upstream 출처가 있으면 원래 조건을 우선한다.
4. synthetic fixture마다 생성 방식·권리자·license·hash를 기록한다. 인간 작품의 단순 변형이나 인터넷에서 받은 sample을 synthetic로 분류하지 않는다.
5. lockfile, vendored code, fonts/media와 배포 image의 transitive dependency를 조사해 license·copyright·NOTICE·변경 고지를 보존한다. root LICENSE로 third-party 의무를 덮지 않는다.
6. 외부 기여에는 기여자가 허락할 수 있는 자료임을 확인하는 기여 안내를 둔다. 기존 기여를 사후 MIT/CC0로 바꿀 때 필요한 권한이 있는지 확인한다.
7. 소프트웨어 라이선스는 사용자가 import한 작품의 display/export 권리를 변경하지 않는다. artifact rights metadata와 프로젝트 코드 license를 분리한다.

## 공개 전 점검과 CI 비용

공개 전환 전 tracked tree뿐 아니라 전체 Git history, branches/tags, PR·Issue·release 첨부와 workflow 로그를 검토한다. credential, private Capture 원본·코드, 내부 운영 자료, 개인정보 및 권리 미확인 asset을 찾는다. 출처·license와 private package/submodule·operations 필수 의존이 없는지 확인한다. credential 발견 시 제거만으로 충분하지 않으므로 폐기/회전하고 기록을 남긴다. 검토 결과와 공개 대상 commit을 고정한 뒤 별도 공개 전환 작업을 수행한다. 공개 후 다시 private로 바꿔도 이미 공유된 복사물이나 부여한 권리가 회수된다고 가정하지 않는다.

GitHub 공식 billing 문서는 **public repo의 standard GitHub-hosted runner 사용이 무료**라고 명시한다. 따라서 공개가 적합하다는 점검을 끝낸 platform에서 표준 `ubuntu-latest` job을 실행하면 private 계정의 포함 분량 미확인 문제를 compute 측면에서 피할 수 있다. 이는 공식 규칙에 따른 운영 판단이며 공개 전 실행·larger runner·외부 유료 API·artifact/cache/package 저장까지 모두 무료라는 보장이 아니다. larger runner는 public에서도 유료다. [GitHub Actions billing](https://docs.github.com/en/billing/concepts/product-billing/github-actions)

초기 job은 짧은 timeout과 concurrency cancellation, 최소 token permission을 사용한다. paid Marketplace action, external service, larger/custom runner, upload-artifact, cache와 package publish는 초기 단계에서 제외한다. 로그·job summary는 artifact allowance에 포함되지 않는다는 공식 설명을 활용해 검사 결과를 남긴다. 이미 발생한 storage 비용은 artifact 삭제나 공개 전환으로 지워진다고 가정하지 않는다. 실제 owner billing plan/잔여 사용량은 별도 확인할 항목이다. 전체 월 예산 상한과 초기 신규 유료비용 0원 정책을 유지한다. [GitHub storage와 과금 규칙](https://docs.github.com/en/billing/concepts/product-billing/github-actions)

## 이 제안의 검증과 다음 작업

- 공식 GNU AGPL txt, ASF Apache 원문, CC legal code, MIT 원문과 GitHub billing 문서를 조사했다. GNU 웹 검색 도구 fetch timeout은 공식 txt의 직접 읽기로 보완했다.
- 이 문서의 조건 요약은 원문을 대체하지 않으며 특정 dependency 조합의 호환성 판정은 아직 수행하지 않았다.
- 문서 변경 검사는 `git diff --check`, README 상대 링크 존재, repo 변경 범위 확인이다. 제품 build/test나 실제 공개 workflow 실행은 이 PR의 검증 대상이 아니다.
- 총괄 검토 후 repo별 적용 PR, dependency/rights/secret audit 및 공개 전환 증거를 별도로 작성한다.
