# 글·키보드·소리 없이 전시를 이용하기

공개 전시는 글·목록 입구에서 시작합니다. 3D, 걷기, 음성, 오프닝과 마이크는 각각 직접 선택합니다. WebGL/XR가 없어도 현재 허용된 작품 제목·설명·credit·대본을 읽을 수 있습니다. 철회/권리 만료를 접근성 경로로 우회하지 않습니다.

- Tab으로 버튼을 찾고 Enter/Space로 실행합니다. 상세를 닫거나 Esc를 누르면 실행한 버튼으로 focus가 돌아와야 합니다.
- 목록 순서 안내의 이전/다음으로 읽습니다. 이것은 현재 작품 목록 순서이며 별도 큐레이터 공간 경로를 만들어 낸 것이 아닙니다.
- 움직임 줄이기와 고대비를 선택합니다. OS preference를 초기값으로 쓰고 수동 선택은 현재 페이지에 적용됩니다.
- 음성 없이 대본을 읽습니다. 마이크 참여는 별도 동의이며 나간 뒤 자동 재개하지 않습니다.
- 3D에서 불편하면 **글·목록 관람으로 돌아가기**를 선택합니다. 걷기/캡처/XR 종료 후 기본 보기에 돌아와야 합니다. AR/VR 또는 Quick Look의 실측/실기기 동작은 별도 미검증 항목입니다.

## 작성자 점검 순서

공개 전시를 별도 창에서 열고 마우스 없이 입구→작품 상세→닫기→다음→대본→credit→퇴장을 실행합니다. 제목/버튼 이름과 focus 위치를 기록합니다. 3D를 켜지 않은 동안 canvas/media 요청 없이 읽는지 확인하고 WebGL 거부 상태에서도 반복합니다. OS reduced-motion을 켜고 page 설정을 확인합니다. 작은 viewport에서 글 잘림·가로 overflow·읽기 순서를 점검합니다.

그 다음 실제 사용하는 screen reader/키보드/스피커/기기에서 같은 내용을 관찰하고 OS·브라우저·revision·막힌 단계를 기록합니다. DOM/ARIA 합성 검사나 viewport 에뮬레이션은 VoiceOver 및 물리 모바일 검증을 대신하지 않습니다. 전체 WCAG 적합성 인증을 주장하지 않습니다. [기존 Viewer 안내](../viewer/visit.md), [공개 접근성 프로토콜](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/accessibility-protocol.md)과 [접근성 계약](https://github.com/ExhibitOS/platform/blob/6663912e4cdaf205cbc648551f4a0bb55b6f0293/docs/viewer-accessibility.md)을 함께 확인합니다. 보고에는 학생·관람객 개인정보 대신 합성 재현 자료를 사용합니다.
