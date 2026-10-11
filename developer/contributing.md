# Issue와 PR 기여

먼저 해당 저장소의 AGENTS/README와 현재 공개 계약을 읽습니다. 공개 코드/문서만으로 재현 가능한 작은 변경을 별도 브랜치/PR로 제안합니다. 원래 요구·권리·검증 기준을 축소해 통과시키지 않습니다. 다른 사람의 변경, 원본, 실패 자료를 보존하고 강제 reset/clean/push를 복구 기본값으로 쓰지 않습니다.

1. [Issue 양식](../templates/issue.md)에 제품 revision·OS/브라우저·합성 재현·기대/실제 결과를 기록합니다. secret·token·private 작품·DB dump·개인정보를 첨부하지 않습니다.
2. 기존 Issue/작업과 중복 여부를 확인하고 변경 파일·효과·검증 계획을 설명합니다. 문서/번역·접근성 대체 텍스트·작은 공개 fixture 개선은 첫 기여 후보입니다.
3. 변경 후 diff·링크/예제·영향 있는 실제 검사를 수행합니다. 실패/미실행/외부 조건을 그대로 기록합니다. PR에는 source와 명령/결과, 사용자 영향과 남은 조건을 적습니다.
4. 권리·비밀·의존 경계를 검토받은 후 병합합니다. repository 공개, hosted CI 비용 또는 새 서비스 활성화는 유지관리자/소유자 결정과 별도입니다.

관리자가 Issue를 분류할 때 `documentation`, `translation`, `accessibility`, `bug`, `good-first-issue`, `needs-reproduction`을 사용할 수 있습니다. 이는 권장 분류이며 GitHub에 해당 label/자동화가 이미 설정됐다는 주장이 아닙니다. good-first-issue는 기존 계약이 명확하고 synthetic 자료로 검사 가능한 범위를 골라 승인합니다.

취약점은 활성화된 GitHub private vulnerability reporting으로 보고합니다. 활성화 여부가 확인되지 않으면 조직 관리자에게 비공개 채널을 먼저 요청합니다. 아직 전용 보안 주소가 있다고 가정하지 않습니다. 취약한 token/작품/로그를 일반 Issue로 보내지 마세요.

설명문·도표는 [CC-BY-4.0](../LICENSE), 실행 가능한 예제·코드/설정은 Apache-2.0이며 third-party 고지를 유지합니다. 번역은 [원문 추적](translation.md), 전시 template은 [독립 권리 검토](template-rights.md)를 따릅니다. 후원은 선택적 소유자 운영 결정이며 기여·self-host 이용을 유료 가입에 묶지 않습니다.
