# 무엇을 백업해야 하나요?

복원할 대상에 따라 필요한 사본이 다릅니다. 백업 파일이 있다는 사실과 실제 복원 검증은 구분합니다.

| 대상 | 보관해야 할 것 | 포함되지 않는 것 |
| --- | --- | --- |
| Studio 로컬 초안 | [Studio 안내](../artist/studio.md)의 JSON 파일 백업 | 서버 계정·승인·전체 작품 bytes |
| 개발 소스 | 원격 Git과 별도 Git bundle | 미커밋 파일·LFS bytes·DB·blob·credentials·브라우저 초안 |
| OEX·고정 전시 | 해당 export와 runtime/권리·서명에 필요한 자료 | 전체 서비스 계정·작업 상태·관리 설정 |
| 서비스 전체 | 일관된 DB와 전체 blob inventory/bytes, 명시적으로 포함한 runtime·설정, 별도 암호화 key | 지정하지 않은 OS/keychain·IAM·DNS·global DB role·브라우저 상태 |

## 서비스 운영자의 복구 순서

1. 사용하는 정확한 revision의 [서비스 백업 안내](../status.md)를 읽고 관리 권한과 호환 PostgreSQL 도구를 확인합니다.
2. 모든 writer와 진행 중인 worker를 멈추고 정지 여부를 확인합니다. 쓰기가 계속되면 일관된 백업으로 간주하지 않습니다.
3. 새 private 경로에 DB와 모든 blob을 함께 암호화해 보관합니다. 필요한 runtime·설정을 명시적으로 포함하고 key는 별도 안전한 경로에 보관합니다.
4. 별도의 빈 DB/blob 환경에서 실제 복원합니다. 크기·hash·schema·권한·현재 유효한 공개 접근과 거부 경로를 검사합니다.
5. 검사한 경로·revision·시각·결과를 private 운영 기록에 남긴 후 복원 지점으로 사용합니다. 기존 백업과 이전 key는 유지합니다.

key가 없으면 암호화 백업을 복원할 수 없습니다. key·DB URL·원본 작품을 Git이나 Issue에 넣지 않습니다. 복원으로 만료된 권리가 다시 유효해지거나 현재 접근 제어를 우회하지 않습니다.

공개 도구는 격리된 합성 PostgreSQL/객체 저장소에서 검사됐습니다. 이는 실제 운영 dataset, 모든 provider 또는 production SLA 검증이 아닙니다. 실제 데이터 삭제·파괴적 유지보수는 검증된 복원 지점이 있을 때만 진행합니다.
