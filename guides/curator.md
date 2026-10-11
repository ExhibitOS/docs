# 큐레이터: 검토된 전시를 저장하고 공개하기

[Studio 상세 조작](../artist/studio.md)을 따라 `/studio`에서 로컬 초안을 만듭니다. 실제 단위는 미터입니다. 방·벽의 수치와 작품 transform을 검토하고 승인된 CMS 작품만 선택합니다. 치수 맞춤이나 보기 편의를 이유로 원본 형상·색을 조용히 바꾸지 않습니다.

1. 로컬 초안을 JSON으로 백업합니다. 이 파일은 metadata이며 작품 bytes나 서비스 계정을 포함하지 않습니다.
2. 공간·배치·조명·viewpoint와 접근성 설명, credit, 대본을 편집합니다. 큐레이션 순서는 명시적으로 검토합니다. 존재하지 않는 음성·번역·작품 정보는 채워 넣지 않습니다.
3. 로그인한 실제 계정과 서버를 확인하고 초안을 서버에 저장합니다. ETag 충돌 시 로컬 사본을 보존하고 서버 변경을 비교합니다. 다시 연결됐다는 이유로 자동 덮어쓰지 않습니다.
4. 저장한 정확한 revision의 READY 검사를 실행하고 오류의 위치·수정 안내를 해결합니다. 작품 승인·현재 display 권리·참조와 접근성 metadata가 필요합니다.
5. 명시적으로 **공개**를 선택한 뒤 새 `/p/…` URL에서 글·목록과 작품 접근을 확인합니다. 로그인 없는 별도 창에서도 확인하세요. 저장·CMS 승인·READY 결과만으로 공개되지 않습니다.
6. 수정하려면 새 초안/revision을 만듭니다. 공개 snapshot은 직접 바뀌지 않습니다. 철회는 이후 접근을 막지만 이미 전달된 bytes를 원격 삭제하지 않습니다.

## OEX로 전달하고 다시 가져오기

현재 로컬 입력과 서버 revision을 저장한 뒤 **OEX 내보내기**를 선택합니다. 포함된 작품·음성 모두의 현재 export 권한이 필요합니다. OEX는 공개 전시 형식의 사본이며 계정·DB·환경 설정 전체 backup이 아닙니다.

새 계정/환경의 Studio에서 `.oex`를 선택하고 **파일 전달·가져오기 시작** → **가져오기 상태 새로고침** → 완료 후 **가져온 전시 열기**를 실행합니다. 별도 draft와 새 ID가 생기며 기존 전시를 덮어쓰거나 자동 공개하지 않습니다. 원본 archive hash와 asset bytes의 크기/hash를 비교하고 치수·배치·credit·현재 권리를 다시 검토합니다. 서버 응답이 끊겼으면 동일 파일과 기존 요청을 재사용하고, 변경한 파일을 같은 요청으로 제출하지 않습니다. 실패한 job은 원인을 확인한 후 재시도하거나 명시적으로 취소합니다.

현재 Platform archive/upload/decoded total은 64MiB입니다. 일반 ZIP 또는 모든 media/extension 호환을 보장하지 않습니다. [정확한 OEX 지원 형식과 복구](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/oex.md), [공개·철회 계약](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/studio-publication.md)을 확인하세요. [접근성 점검](accessibility.md)은 공개 전에 함께 실행합니다.
