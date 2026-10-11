# Reference 설치·export·복원 검증 기록

이 절차는 공개 제품의 실제 명령/화면을 따라 새 사용자 문서 검사를 할 수 있도록 구성했습니다. 작성 시점(2026-10-11)에 이 문서만 읽은 새 사용자의 전체 install→export→restore 실행은 **미실행**입니다. 이전 제품의 API/브라우저·합성 DB 복원 결과를 그 사용자의 통과 결과로 대체하지 않습니다. 문서 저장소에는 제품 build/test suite가 없습니다.

## 검사 준비와 설치

기록에 제품 exact commit, OS/Node/npm/PostgreSQL/browser 버전, 사용한 공개 문서, 시작/종료 시각과 결과를 적습니다. 모두 새 합성 작품/전시와 private 후보 경로를 사용하고 기존 사용자 volume·서비스·백업은 건드리지 않습니다. 실제 전시를 지우거나 복원 대상으로 사용하지 않습니다. 비용·필요 여유 공간을 먼저 확인하고 기존 로컬 도구만 사용합니다.

[로컬 self-host 설치](guides/self-host.md)의 명령을 순서대로 실행합니다. 권한 없는 사용자는 관리자 bootstrap/DB 접속을 대신할 수 없습니다. admin이 private 환경과 계정을 준비한 다음 CMS에서 로그인합니다. 새 합성 작가/작품과 지원 GLB 또는 PNG를 등록하고 현재 revision·asset·실측 치수·권리를 검토 승인합니다. 서버 readiness·로그인·파일 approval·작품 approval 결과는 각각 기록합니다. 기본 password를 문서에 새로 넣지 않습니다.

## 전시 내보내기와 다시 가져오기

[큐레이터 절차](guides/curator.md)대로 새 전시를 저장하고 READY/공개를 명시적으로 실행합니다. 새 비로그인 창의 글·목록/허용된 media를 확인하고 current rights 거부도 관찰합니다. export 허용 합성 작품으로 OEX를 생성하고 파일 SHA/bytes를 기록합니다. 별도 새 draft로 import하여 job 완료·별도 ID·원래 bytes hash·치수·credit·권리/공간 보존을 비교합니다. import만으로 publication이 생기지 않아야 합니다. JSON backup/OEX와 full service backup의 범위가 다름을 설명할 수 있어야 합니다.

## 전체 서비스의 별도 복원

아래는 Unix 운영자용 **공개 Platform checkout 안의** 명령입니다. [고정 source 전체 안내](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/storage-service-backup.md)의 DB/role/파일 권한·설정 포함 범위를 먼저 준비합니다. `DATABASE_URL`, `BLOB_ROOT`, 기타 설정은 운영자가 관리하는 private 환경으로만 공급합니다. `source`로 읽는 환경 파일은 실행 코드이므로 자신이 관리하는 파일만 사용합니다. password/연결 URL/key bytes를 인수·로그·Git에 넣지 않습니다.

모든 API/worker와 외부 writer를 실제로 정지합니다. PostgreSQL18.6 호환 `pg_dump`/`pg_restore` 또는 승인된 기존 PG container를 준비합니다. 새 private key 부모를 만든 뒤 기존 파일을 덮어쓰지 않는 key-init를 실행합니다.

```sh
BACKUP_KEY_DIRECTORY="<존재하지 않는 새 private key 부모의 실제 절대 경로>"
mkdir -m 700 "$BACKUP_KEY_DIRECTORY"
BACKUP_KEY_FILE="$BACKUP_KEY_DIRECTORY/service-backup.key"
node scripts/service-backup.mjs key-init --key-file "$BACKUP_KEY_FILE"
BACKUP_DESTINATION="<존재하지 않는 backup 대상의 실제 절대 경로>"
node scripts/service-backup.mjs create \
  --key-file "$BACKUP_KEY_FILE" --destination "$BACKUP_DESTINATION" --quiesced
VERIFY_DESTINATION="<존재하지 않는 별도 verify 대상의 실제 절대 경로>"
node scripts/service-backup.mjs verify \
  --key-file "$BACKUP_KEY_FILE" --source "$BACKUP_DESTINATION" \
  --destination "$VERIFY_DESTINATION"
```

각 대상 부모는 소유자 전용의 실제 canonical 경로여야 합니다. key는 backup 밖에 별도 보관하고 key 복구 사본으로도 verify합니다. `--quiesced`는 정지 증거가 아니라 확인 선언입니다. verify의 plaintext는 민감 자료이며 공개 파일로 배포하지 않습니다. backup receipt만으로 실제 복원 통과로 기록하지 않습니다.

새 빈 PostgreSQL DB와 새 빈 blob root/bucket, dump의 owner/ACL에 필요한 role을 준비합니다. 기존 schema·object·writer가 있는 대상은 사용하지 않습니다. **대상** 연결 설정을 private 환경으로 바꾸고 원본 DB URL/blob root가 남아 있지 않은지 확인합니다. 아래 destination은 blob root가 아닌 새 검증 workspace입니다.

```sh
RESTORE_WORKSPACE="<존재하지 않는 새 복원 검증 경로의 실제 절대 경로>"
node scripts/service-backup.mjs restore \
  --key-file "$BACKUP_KEY_FILE" --source "$BACKUP_DESTINATION" \
  --destination "$RESTORE_WORKSPACE" --quiesced --fresh-destination
```

`restored.json`과 전체 schema/migration/table/object 크기·hash 대조 성공을 확인합니다. runtime/configuration이 포함됐다면 검증된 내용만 새 private 경로에 설치하고 자동 활성화됐다고 가정하지 않습니다. backup 이후의 권리 철회·계정/byte 삭제 receipt·hold·restored sessions를 운영자가 대조한 뒤 후보 서비스만 실행합니다. 실제 로그인, 승인 작품/음성, 공개/거부, OEX job과 현재 rights를 확인하고 oldsource·key·backup을 그대로 보존합니다. 실패 후보를 비워 재사용하지 않고 별도 새 후보로 다시 시도합니다.

Manager를 사용하는 운영자는 [그 제품 복원 절차](https://github.com/ExhibitOS/manager/blob/main/docs/backup-restoration.md)의 새 관리 공간·외부 key·유지보수 image·unused port·writer 동의를 따릅니다. 현재 각 OS/GUI/cold engine qualification과 이 docs-only 검사를 분리합니다. Generic SSH의 actual remote recovery는 미검증이며 대신 통과했다고 적지 않습니다.

## 완료 기록

| 확인 | source/실제 결과를 기입 |
| --- | --- |
| 신규 사용자 문서-only 설치/로그인 | 미실행 |
| 합성 작품 승인·전시 공개/OEX export→새 draft import | 미실행 |
| 일관된 service backup→별도 새 DB/blob 복원 | 미실행 |
| 실제 접근성/키보드·기여/번역 양식 사용 | 미실행 |
| 문서 상대 링크·고정 소스 참조·diff 검토 | 2026-10-11: 상대 링크79/고정 Platform Git object 경로26 존재 확인, 오류0; `git diff --check` exit0. HTTP live 상태·실제 예제 실행은 미검사 |

통과는 실제 실행 결과·명령/화면·exact source와 증거가 있을 때만 갱신합니다. 개인정보가 없는 compact 결과는 공유할 수 있으나 원본·credentials·복호화 후보/DB/backup은 private 보관합니다. 이 양식은 새 product gate/지원 환경을 만들지 않고 원래 documentation acceptance의 실행 결과를 구분합니다.
