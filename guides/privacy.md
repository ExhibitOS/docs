# 개인정보, 동의와 보관

CMS의 **개인정보와 동의**에서 본인의 현재 tenant를 확인합니다. 기관 token이 이 계정 화면의 권한을 대신하지 않습니다. [현재 서버 정책](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/privacy.md)과 [글 제안](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/assistance.md)은 구현 범위를 설명합니다.

## 분석 동의

분석은 기본 꺼져 있습니다. 관리자가 기관 분석을 켜더라도 방문자가 직접 동의해야 합니다. 로그인 방문자는 본인 계정 동의도 켜져 있어야 합니다. Viewer의 동의는 현재 보기 세션에만 적용되며 철회하면 대기 중 전송/미전송 체류 시간이 폐기됩니다. 로컬 offline 관람은 분석을 전송하지 않습니다.

저장하는 것은 일별 방문·세션·체류·방 방문·완주 집계입니다. 고유 인간 수나 개인 동선을 뜻하지 않습니다. IP·계정/세션 식별자·원문·trajectory를 집계에 넣지 않습니다. 개인과 연결하지 않은 과거 집계에서 계정 하나의 기여를 골라 삭제할 수 없습니다. 관리자는 분석 허용/보관 일수와 raw/temporary 보관 정책을 명시적으로 저장합니다.

## 본인 정보 내보내기와 계정 처리

1. 삭제 전에 **본인 정보 내보내기**를 실행하고 private 위치에 보관합니다. 현재 tenant의 본인 subject·작가/작품 metadata·권리/hash inventory·등록 객체·동의입니다. 계정 전체 media archive, 다른 tenant 자료나 credential/session 사본이 아닙니다.
2. 삭제 요청은 전역 로그인에 영향을 줍니다. 독립 backup은 남으며 처리 이후 로그인할 수 없어 본인 상태 조회가 불가능할 수 있습니다. 필요한 receipt 확인은 운영자에게 요청해야 할 수 있습니다.
3. 독립 backup 보관 안내에 동의한 뒤 요청합니다. 요청 접수는 실제 삭제 완료가 아닙니다. 현재 hold·마지막 admin·등록된 보관 자료 조건으로 blocked될 수 있으며 운영자 worker가 별도로 처리합니다.
4. `ACCOUNT_IDENTITY_ERASED_DATA_RETAINED`는 로그인 identity·credentials가 제거됐지만 불변 작품/권리/승인/검토 이력과 등록 자료·독립 backup이 남는 결과입니다. 모든 개인 데이터가 사라졌다는 뜻이 아닙니다. 콘텐츠는 각각의 권리·보관 정책을 따릅니다.

Master/web bytes는 자동 만료하지 않습니다. raw/temporary 등록에는 기한 안내 확인이 필요하며 참조·법적·backup hold나 불확실한 inventory가 있으면 byte 삭제를 거부합니다. UI 요청만으로 worker가 즉시 삭제하지 않습니다. 운영자는 외부 backup hold와 삭제 receipt를 보존하고 복원 서비스를 열기 전에 backup 이후의 삭제/권리 철회를 대조해야 합니다. 외부/offline 사본을 자동 발견하거나 삭제하는 기능은 없습니다.

## 외부 AI와 보고

원문/제안 분리와 명시적 human 검토를 사용합니다. 외부 AI 준비에는 named provider와 동의가 필요하지만 현재 제품은 실제 provider를 호출하지 않습니다. 동의 기록을 실제 전송/번역 실행으로 해석하지 않습니다. 비공개 작품·원문·token·DB dump를 일반 Issue에 보내지 마세요. 보안 보고는 [기여 안내](../developer/contributing.md)의 비공개 경로를 따릅니다.
