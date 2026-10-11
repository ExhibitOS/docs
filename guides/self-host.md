# 직접 운영하기와 공식 호스팅의 경계

ExhibitOS 핵심 self-host는 유료 공식 호스팅 구매가 필수 조건이 아닙니다. 공개 Platform/Spec 계약으로 자신의 서버를 구성하고 OEX와 일관된 서비스 backup을 내보낼 수 있습니다. 브라우저 초안은 계정 없이 편집할 수 있으나 protected 작품 import·승인·공개에는 구성된 서버와 계정이 필요합니다.

| 경로 | 제공/책임 | 현재 한계 |
| --- | --- | --- |
| 로컬 개발 self-host | 공개 소스·로컬 PostgreSQL/object backend, 소유자가 환경과 backup 관리 | production 보안·복구·기기별 검증을 대신하지 않음 |
| Manager self-host | 준비된 검증 runtime bundle의 설치/시작/정지와 백업·복원 코어 | 자동 release 다운로드/모든 OS 설치·서명·복원 완료 아님 |
| Generic SSH | 준비된 Linux host/runtime에서 제한된 plan/lifecycle source adapter | 실제 원격 host·DNS/TLS·firewall·rollback qualification 미완료 |
| 공식 hosted | 운영 주체의 서비스/가격/지원/보관 약정이 별도로 필요 | 현재 이 문서는 운영 중인 hosted 서비스·SLA·유료 가입을 제공하지 않음 |

웹사이트가 열리거나 Git 자동 배포가 연결됐다는 사실은 계정/작품 서버의 hosted 운영·복원 검증이 아닙니다. 새 paid provider/resource를 이 가이드가 생성하지 않습니다. 기관이 직접 운영하면 TLS, OS 접근, secret, 용량, backup key·보관/삭제 정책과 복구 훈련 책임을 명시해야 합니다. 브랜드 사용·공식 인증·후원 조건은 소유자 결정이 필요하며 코드 라이선스와 별개입니다.

## 로컬 reference 설치

합성 전시로 먼저 실행합니다. Node24.21.0/npm11.19.0과 로컬 Docker, 공개 Platform의 선택한 revision이 필요합니다. 새 checkout에서 실행하고 이미 있는 환경/volume을 지우지 않습니다.

```sh
npm ci
npm run storage:init
docker compose --env-file .local/storage.env -f compose.storage.yml up -d
npm run build
```

`storage:init`는 새 private `.local/storage.env`를 만들며 기존 값을 덮어쓰지 않습니다. 운영자는 [storage 연결/마이그레이션](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/storage.md)에 따라 `DATABASE_URL`을 private 환경으로 공급하고 `npm run storage:migrate`를 실행합니다. filesystem `BLOB_ROOT`를 private 실제 경로로 준비합니다. [인증 설정](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/auth.md)의 `AUTH_MODE`, 정확한 `AUTH_ORIGIN`, loopback `HOST`/`PORT`와 서버 origin을 함께 구성하고 새 private bootstrap JSON에 실제 tenant UUID/subject/password를 넣습니다. 자격정보를 인수·공유 콘솔·Git에 넣지 않습니다.

```sh
npm run auth:bootstrap < .local/bootstrap-admin.json
```

그 뒤 설정된 API와 웹을 별도 터미널에서 `npm run dev:api`, `npm run dev:web`로 시작하고 `/cms` 로그인→[작가 등록](artist.md)→[Studio 공개/OEX](curator.md)를 실행합니다. 개발 웹 주소와 API origin은 [README](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/README.md)의 현재 proxy 설정에 맞춥니다. 이 개발 명령은 공개 네트워크 배포 명령이 아닙니다. 네트워크 서비스에는 외부 TLS terminator·secure cookie·정확한 origin과 별도 운영 검토가 필요합니다. 기본 password·공개 signup·credential recovery를 가정하지 않습니다.

## Manager와 복구

Manager에서는 검증된 runtime bundle과 실제 연결 가능한 Docker/Podman을 준비한 뒤 실행 도구 확인→새 관리 공간→전시 설치→시작→전시 열기→API 연결 확인을 실행합니다. bundle이 없으면 성공으로 표시하지 않습니다. 진행 표시와 완료/실패 결과를 구분하며 정지는 volume을 삭제하지 않습니다. 현재 [Manager 사용법](https://github.com/ExhibitOS/manager/blob/main/docs/desktop.md)을 확인하세요. private repository 권한이 없으면 공개 Platform 경로를 사용하며 Manager 접근을 핵심 self-host의 필수 조건으로 추가하지 않습니다.

서비스 backup은 [reference 복원 절차](../docs-validation.md)와 [backup 구분](../operator/backup.md)을 따릅니다. OEX/JSON/Git 사본은 DB·전체 blob·credentials·환경 설정을 대신하지 않습니다. 원격 source adapter는 [Deployment 제한](https://github.com/ExhibitOS/deployment/blob/main/docs/generic-ssh.md)을 읽고 실제 Linux 배포 검증 전 운영 준비 완료로 표시하지 않습니다.
