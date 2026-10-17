# Reference 설치·export·복원 검증 기록

이 절차는 공개 제품의 실제 명령/화면을 따라 새 사용자 문서 검사를 할 수 있도록 구성했습니다. 2026-10-11에 공개 문서 절차를 따라 새 합성 환경에서 install→실제 CMS/Studio 화면→OEX→별도 DB/blob 복원을 실행했습니다. 실제 브라우저 조작을 자동화했으며 기존 제품 test driver·mock API·기존 node_modules 사본으로 대체하지 않았습니다. 실패한 문서/host 경로와 검사 driver 오류는 아래에서 성공 단계와 구분합니다. 실사용자·실제 작품·기기/원격 hosted 검증 결과는 아닙니다. 문서 저장소에는 제품 build/test suite가 없습니다.

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
| 신규 reference 문서 절차 설치/로그인 | PASS: 새 공개 Platform `ce0f4ab6ac9495753669f828690b12b0908fff4b` snapshot의 실제 npm ci/build, storage:init, 14 migration, private bootstrap, 실제 CMS 로그인 |
| 합성 작품 승인·전시 공개/OEX export→새 draft import | PASS: 실제 작가/작품 form·PNG upload·import:work·현재 revision 승인·Studio 서버 저장/READY/공개·비로그인 관람. OEX 다운로드4,383B와 기존 job refresh/import로 별도 draft/artwork ID, PNG bytes·치수·권리·credit·방·배치 보존 |
| 일관된 service backup→별도 새 DB/blob 복원 | PASS: writer 정지→암호화 create→독립 recovery-key 사본 verify→같은 소유 PG cluster의 별도 새 빈 DB와 새 blob root restore. 14 migrations/71 tables/5 objects 검증 및 restored.json complete. 새 로그인·공개 화면·원본/공개 derivative 각각의 hash 확인, 복원 후보의 명시적 display 철회 후 익명 publication/media 각각404 |
| 실제 접근성/키보드·기여/번역 양식 사용 | 실제 익명 화면 Tab focus smoke PASS. 전체 접근성/보조기기 audit와 외부 기여자·번역가의 실제 제출은 미실행; 양식/원문·license 추적 안내와 링크 검토를 별도로 기록 |
| 문서 상대 링크·고정 소스 참조·diff 검토 | 2026-10-11 최종 수정: 상대 링크81개·고정 Platform source 참조40회(고유31개)의 Git object 경로 확인, 오류0; `git diff --check` exit0. HTTP live 링크 상태는 미검사; 실제 reference 실행은 위 단계별 결과 참조 |

통과는 실제 실행 결과·명령/화면·exact source와 증거가 있을 때만 갱신합니다. 개인정보가 없는 compact 결과는 공유할 수 있으나 원본·credentials·복호화 후보/DB/backup은 private 보관합니다. 이 양식은 새 product gate/지원 환경을 만들지 않고 원래 documentation acceptance의 실행 결과를 구분합니다.


## 2026-10-11 reference 실제 실행의 범위

최종 기록 시각은 **2026-10-11 18:12 Europe/Berlin (CEST)**입니다. Platform source는 위 `ce0f4ab`이며 docs baseline은 `50a7bfd47adeabfca18dc948b92805172b456327`와 이 작업의 self-host 환경/worker/host-network 안내 수정입니다. 환경은 macOS27.0.1 arm64, Node24.21.0/npm11.19.0, 공식 PostgreSQL18.6 index `74935e72241653ca55e0414067e6d8763aceb8a810eb51b452253ec3dcfc4336`, 기존 Playwright1.63.0 Chromium 캐시(bundle153.0.8010.12)입니다. 새 private 경로와 고유 Compose project만 사용했고 기존 사용자 container/network/volume을 지우지 않았습니다.

- 설치 첫 offline cache 시도는 missing tarball로 실패했습니다. 문서의 정상 `npm ci`를 새 snapshot에서 실제 실행하여 통과했으며 dependency 사본을 붙이지 않았습니다. 첫 build는 저장공간 감시의 global growth 한도에 걸려 정지했습니다. 실패 로그를 유지하고 한도를 다시 확인한 뒤 **실패한 build만** 실행해 exit0(6.36초)를 확인했습니다.
- 기존 공개 source의 PostgreSQL digest는 registry manifest가 아닌 잘못된 pin이었습니다. 공개 Platform PR54의 공식 digest 수정이 병합된 뒤 새 `ce0f4ab` snapshot을 설치했습니다. 로컬 config-ID나 다른 image를 숨겨 대체하지 않았습니다.
- 기본 Compose network 생성은 실제 host의 Docker address-pool 소진으로 실패했습니다. [self-host](guides/self-host.md)의 명시적 operator-checked IPAM overlay 경로로 같은 검사 project를 재개했습니다. 기본 네트워크 경로를 통과한 것으로 기록하지 않습니다. filesystem blob 경로이므로 PostgreSQL만 시작했습니다.
- 임시 브라우저 검사 driver의 잘못된 health URL, 비동기 목록/refresh 대기 누락, 중복 제목의 다른 artwork 선택, master와 공개 derivative 해시 혼동으로 생긴 실패를 보존했습니다. 완료한 설치·저작·백업을 반복하거나 실패를 제품 통과로 바꾸지 않고 해당 실패 단계만 고쳤습니다. 제품 API/화면 응답은 실제 실행 결과이며 mock이 아닙니다.

원본 합성 PNG는 **163B**, SHA-256 `e0dd220fecc7ccf7c66d72e840a948b97aba0e523fbbf97b110a588f544d0495`입니다. OEX와 복원 CMS의 실제 원본 다운로드가 이 bytes를 보존했습니다. 공개 승인 PNG derivative는 **220B**, SHA-256 `9b20e3ffe9046ca46c8eb65c9aeee344a2c87b51e5da8a91bf3e3cd6e28fd8d2`이며 자신의 snapshot hash와 비교했습니다. 두 artifact를 같은 원본이라고 부르지 않습니다. OEX SHA-256은 `6e6f324b2e4a8b5fae9e775aaafdfe95647693ca520c1a0e55b94d726d4533ca`입니다. 합성 메타데이터의 1×1m는 워크플로용 명시적 선언이며 실제 작품을 실측한 결과가 아닙니다.

독립 암호화 복원 manifest SHA-256은 `a84f3e9914cc1f058d0766fd5517a7b3a0ffc15a6d8094583cc9c60f81c09f15`입니다. private 단계별 source/명령/실패·성공/log hash를 묶은 compact aggregate receipt SHA-256은 `a8c9765a3c1645c57bb9d9a202d02081a373d25a0a182b56777bf7fb223fed25`입니다. credentials·key·복호화 DB·작품 파일은 문서 저장소에 포함하지 않습니다. 원본 서비스와 백업은 검사 중 보존했고 복원 후보에서만 display consent를 철회했습니다. 실제 권리 철회 검사는 이미 전달된 파일의 원격 삭제나 independent backup의 삭제를 보장하지 않습니다.


## 2026-10-18 시작·사용 안내 갱신의 제한된 검사

처음 시작하기, 선택적 촬영·Mac 처리, 작품 가져오기·배치, 관람, 로컬 운영과 공개 방향을 기존 문서 안에서 정리했습니다. 일반 사용자 흐름과 개발·과거 운영 참고를 구분합니다. 공개 저장소의 실제 visibility와 새 연결 문서 경로를 읽기 조회했고, 변경 Markdown9개에서 상대 파일 링크61개의 존재와 whitespace를 확인했습니다. 이는 제품 설치·원격 배포·복원·공식 스토어 또는 실기기 지원의 재검증이 아닙니다.

별도 정적 웹사이트의 로컬 Chromium 검사에서는 기존21개 페이지/폭 조합과 이후 카드 밑줄만 다듬은 영향6개 화면을 확인했습니다. 이 결과를 위 과거 reference 설치·export·복원 증거에 합치거나 새 제품 검증으로 확대하지 않습니다. Safari·실제 iOS·VoiceOver와 초보자 직접 관찰은 이번에 수행하지 않았습니다. 정식 다운로드·App Store·정적 체험 URL은 실제 제공 전 준비 중으로 유지합니다.
