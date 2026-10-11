# 기관: 목록, 권리와 교육 자료를 관리하기

기관 metadata는 작품의 원본·저작권·승인과 별도로 보존합니다. 기관 admin이 기존 소유/허용 작품에 컬렉션을 연결하며 타 기관/tenant의 권한을 사용할 수 없습니다. [현재 기관 API와 교육 절차](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/institution.md)가 정확한 입력·한도의 기준입니다.

1. 기관 admin으로 컬렉션을 만듭니다. 먼저 두 개의 허용된 작품으로 작게 시작합니다.
2. 실제 artwork ID와 accession number·분류·취득 연도·보존 상태·출처/전시/보존 이력을 검토해 batch import합니다. 알 수 없는 값은 unknown 또는 미기록으로 남깁니다. 개인 학생 평가나 민감 자료는 기관 공개 metadata에 넣지 않습니다.
3. 현재 한도는 batch 100행/256KiB, 컬렉션 1,000항목입니다. 부분 실패와 각 행 상태를 확인합니다. 같은 request ID는 동일 입력 재시도에만 씁니다.
4. 실수한 batch는 명시적으로 rollback합니다. 이는 그 batch의 연결을 비활성화하며 원래 작품·권리·불변 이력을 지우지 않습니다. 수정 입력에는 새 request ID를 사용합니다.
5. 목록/이력/export의 현재 권리를 확인합니다. 저장된 pagination snapshot은 15분이며 다음 페이지에도 접근을 재검사합니다. metadata export는 작품 원본 배포 허가가 아닙니다.

## 교육용 공유와 외부 연동

승인된 전시의 공개 URL을 준비하고, 기관 catalog 읽기에는 정확한 컬렉션/작품·scope·만료를 지정한 최소 token을 발급합니다. 예를 들어 허용 작품 두 개만 read scope로 1시간 공유하고 수업 후 폐기합니다. token은 한 번만 반환되며 URL·Issue·콘솔·문서에 붙이지 않습니다. issuer가 현재 admin/member여야 하며 wildcard 권한은 없습니다. 만료·폐기·한도 오류를 무시해 우회하지 않습니다.

작품 설명·credit·대본·목록 순서를 비교하는 수업은 3D 없이도 가능합니다. 기관 목록과 공개 전시의 저작권 범위가 다를 수 있음을 설명합니다. 실제 교실/보조기기 사용성은 별도 관찰이며 API 검사만으로 검증됐다고 주장하지 않습니다.

운영자는 [서비스 backup](self-host.md)과 [개인정보·hold](privacy.md)를 함께 관리합니다. 보존 상태 complete는 예술 품질 평가나 복원 가능성 인증이 아닙니다.
