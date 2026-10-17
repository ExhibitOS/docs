# 직접 운영하기와 공식 호스팅의 경계

## 현재 제작·공개 경로

로컬 Studio 사용에는 Cloudflare·Render 계정이나 토큰이 필요하지 않습니다. Manager의 **Studio 준비하고 열기**는 선택한 설치의 환경·실행 패키지·서버 준비를 확인한 뒤 기본 브라우저에서 Studio를 여는 경로입니다. 포함 runtime이 없거나 실제 OS 승인이 필요하면 안내하고 멈춥니다. 새 컴퓨터·공식 배포판 전체 설치가 이미 검증됐다는 뜻은 아닙니다.

Manager는 Developer ID 서명·Apple 공증 후 웹사이트 배포, 공식 Mac Processing은 Mac App Store 배포 방향입니다. 정식 다운로드·스토어 경로는 아직 준비 중입니다. Manager의 일반 로컬 소스 빌드는 유료 Apple 개발자 계정이나 정식 배포 인증서를 필수로 요구하지 않습니다. [현재 Manager 사용법](https://github.com/ExhibitOS/manager/blob/main/docs/desktop.md)을 확인하세요.

### 인터넷 공개가 필요할 때

1. Studio에서 작품 권리·검토·저장·공개 준비를 확인합니다. 로컬 저장·미리보기만으로 공개되지 않습니다.
2. Manager **배포 준비 → 전시를 웹에 공개하기**에서 정적 단독 또는 선택적 동적 구성을 고릅니다.
3. 정적 단독에는 Cloudflare Pages 인증만 사용합니다. 정적+동적에는 별도의 Render 토큰도 필요합니다. 토큰은 Manager의 가림 입력·Keychain 경로를 사용하고 문서·Git·채팅·화면 공유에 넣지 않습니다.
4. 승인된 전시를 선택해 배포하고 실제 공개 URL에서 관람·접근 범위를 확인합니다. 이 문서 작성은 새 원격 배포 완료 증거가 아닙니다.

기본 구성은 Pages의 정적 작품·전시와 선택적 Render Node 서버·Render PostgreSQL입니다. 세 번째 호스팅·저장 서비스를 필수로 추가하지 않습니다. 로컬 서버·동적 기능이 중단돼도 정적 관람은 유지해야 합니다. Ubuntu 직접 배포·Railway·범용 원격 배포는 1차 필수 대상에서 보류합니다.

**비용·데이터 주의:** Render 무료 PostgreSQL은 생성 30일 후 만료되므로 만료 전에 접근 가능한 동안 백업해야 합니다. 무료 서버는 유휴 시 절전되고 임시 파일시스템은 영속 작품 보관소가 아닙니다. 실제 계정의 무료 한도와 만료일을 확인하며 영구 무료·자동 무료 연장·무제한 재생성을 보장하지 않습니다. 자동 유료 전환도 승인하지 않습니다. 정책 확인 2026-10-17: [Render 공식 무료 조건](https://render.com/docs/free), [Cloudflare Pages 한도](https://developers.cloudflare.com/pages/platform/limits/).

## 개발·운영 참고의 기존 경로

아래 소스 실행·기존 원격 adapter 설명은 개발/장기 운영 참고입니다. 현재 일반 사용자 기본 설치나 1차 공개 필수 환경으로 오인하지 마세요.


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
docker compose --env-file .local/storage.env -f compose.storage.yml up -d postgres
npm run build
```

`storage:init`는 새 private `.local/storage.env`에 무작위 PostgreSQL password를 만들며 기존 파일을 덮어쓰지 않습니다. 이 파일만 생성해서는 API의 `DATABASE_URL`이 설정되지 않습니다. 아래는 위 Compose의 새 로컬 DB와 filesystem blob을 사용하는 reference 설정입니다. 자신의 관리자 권한으로 생성한 환경 파일만 읽습니다. shell tracing(`set -x`)을 켜지 말고 환경/비밀값을 콘솔·공유 로그에 출력하지 않습니다.

```sh
set -a
source .local/storage.env
set +a
export DATABASE_URL="postgresql://postgres:${POSTGRES_PASSWORD}@127.0.0.1:5432/exhibitos"
export AUTH_MODE=local
export AUTH_ORIGIN=http://127.0.0.1:5173
export HOST=127.0.0.1
export PORT=3000
mkdir -m 700 .local/blobs
export BLOB_ROOT="$PWD/.local/blobs"
npm run storage:migrate
```

filesystem blob reference는 PostgreSQL만 시작하므로 쓰지 않는 S3 서비스/volume을 만들지 않습니다. S3 backend를 선택했다면 linked storage guide의 별도 설정을 따릅니다.

Docker가 `all predefined address pools have been fully subnetted`로 새 네트워크를 만들지 못하면 기존 전시/정지 container의 네트워크를 prune하지 않습니다. 운영자가 `docker network inspect`의 모든 subnet과 host/VPN route를 확인한 뒤 **겹치지 않는** 작은 private subnet을 선택할 수 있습니다. 다음 `10.241.0.0/28`은 예시이며 다른 컴퓨터에서 그대로 안전하다고 가정하지 않습니다. 확인한 값만 ignored private overlay에 기록합니다. image/권한/DB 설정은 원래 Compose 그대로 유지합니다.

```sh
cat > .local/reference-network.yml <<'YAML'
networks:
  default:
    ipam:
      config:
        - subnet: 10.241.0.0/28
YAML
chmod 600 .local/reference-network.yml
docker compose --env-file .local/storage.env \
  -f compose.storage.yml -f .local/reference-network.yml up -d postgres
```

이 host-specific 해결 경로를 실제로 썼으면 원래 기본 네트워크 생성 실패와 overlay 사용을 결과에 함께 기록합니다. 동일 검사 project에 사용했던 overlay를 정지/정리 명령에도 유지하며 기존 환경의 리소스에는 적용하지 않습니다.

`AUTH_ORIGIN`은 브라우저가 여는 정확한 웹 origin입니다. 기본 Vite 웹은 `/api`를 loopback API3000으로 전달합니다. 기존 경로/포트가 사용 중이면 기존 서비스를 멈추거나 폴더를 비워 재사용하지 말고 운영자에게 별도 설정을 요청합니다. 설정된 환경은 API를 실행할 같은 터미널에서 유지합니다. [storage](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/storage.md)와 [auth](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/auth.md)의 실제 DB/권한/새 대상 조건도 따릅니다.

첫 bootstrap JSON은 정확히 `tenantId`, `subject`, `password`만 포함합니다. 아래는 새 reference 계정의 UUID와 무작위 password를 private 파일로 만드는 예이며 기본/공유 password가 아닙니다.

```sh
node --input-type=module <<'JS'
import { randomUUID, randomBytes } from 'node:crypto';
import { writeFileSync } from 'node:fs';
writeFileSync('.local/bootstrap-admin.json', JSON.stringify({
  tenantId: randomUUID(), subject: 'reference-operator',
  password: randomBytes(32).toString('base64url')
}), { flag: 'wx', mode: 0o600 });
JS
npm run auth:bootstrap < .local/bootstrap-admin.json
```

파일에서 자신의 tenant UUID/subject/password를 개인 컴퓨터에서만 확인해 CMS 로그인에 사용합니다. 내용을 Issue·공유 화면·로그에 넣지 않습니다. bootstrap은 기존 계정이 있는 DB에서 다시 실행하지 않습니다. 같은 private 환경을 유지한 터미널에서 `npm run dev:api`, 별도 터미널에서 `npm run dev:web`를 실행하고 `http://127.0.0.1:5173/cms`를 엽니다. 실제 준비된 계정으로 로그인→[작가 등록](artist.md)→[Studio 공개/OEX](curator.md)를 실행합니다. 작품 파일이 queued로 남으면 API가 파일 import worker를 자동 실행한다고 가정하지 않습니다. 같은 private `DATABASE_URL`/`BLOB_ROOT`를 유지한 별도 터미널에서 `npm run import:work`를 실행한 뒤 CMS의 검사 상태/파일 목록을 다시 읽습니다. 이것은 한 번 실행하는 기존 import worker이며 production scheduler를 설치하지 않습니다. OEX job worker는 configured API의 별도 경로입니다.

이 명령은 공개 네트워크 배포가 아닙니다. 네트워크 서비스에는 외부 TLS terminator·secure cookie·정확한 origin과 별도 운영 검토가 필요합니다. 공개 signup·credential recovery를 가정하지 않습니다. reference 신규 사용자 실제 실행 결과는 [검증 기록](../docs-validation.md)에서 별도로 확인합니다.

## Manager와 복구

Manager에서는 검증된 runtime bundle과 실제 연결 가능한 Docker/Podman을 준비한 뒤 실행 도구 확인→새 관리 공간→전시 설치→시작→전시 열기→API 연결 확인을 실행합니다. bundle이 없으면 성공으로 표시하지 않습니다. 진행 표시와 완료/실패 결과를 구분하며 정지는 volume을 삭제하지 않습니다. 현재 [Manager 사용법](https://github.com/ExhibitOS/manager/blob/main/docs/desktop.md)을 확인하세요. private repository 권한이 없으면 공개 Platform 경로를 사용하며 Manager 접근을 핵심 self-host의 필수 조건으로 추가하지 않습니다.

서비스 backup은 [reference 복원 절차](../docs-validation.md)와 [backup 구분](../operator/backup.md)을 따릅니다. OEX/JSON/Git 사본은 DB·전체 blob·credentials·환경 설정을 대신하지 않습니다. 원격 source adapter는 [Deployment 제한](https://github.com/ExhibitOS/deployment/blob/main/docs/generic-ssh.md)을 읽고 실제 Linux 배포 검증 전 운영 준비 완료로 표시하지 않습니다.
