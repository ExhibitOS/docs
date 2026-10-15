# 1차 출시: iPhone에서 촬영하고 Mac에서 완성하기

2026-10-15 사용자가 확정한 제품 방향입니다. 구현 대상과 실제 검증 완료는 구분합니다.

1. iPhone에서 촬영·품질 안내를 확인하고 원본을 보관합니다. 선택적인 `.reduced`는 빠른 촬영 확인이며 최종 승인이 아닙니다.
2. 사진·깊이·카메라 metadata·세션·치수·권리·출처를 포함한 원본 폴더 전체를 Mac으로 전달합니다. 미리보기 모델을 원본 대신 사용하지 않습니다.
3. Mac Swift·RealityKit Processing에서 원본을 재구성합니다. 지원되는 상세 수준을 선택하고 진행·실패·취소·재시도를 확인합니다. 높은 상세 수준이 잘못 찍힌 부분을 복구한다고 가정하지 않습니다.
4. 실제 내보낼 GLB와 LOD를 회전·확대해 형상·표면·치수를 검토합니다. 생성 성공은 품질/공개 승인이 아닙니다. 원본 master와 파생본은 구분해 보존합니다.
5. GLB·LOD·OES를 내보내 Mac Studio/CMS에서 작품을 등록·검토·승인하고 전시를 공개합니다. Mac Manager가 설치·실행·백업·복원·업데이트·롤백을 담당합니다.

촬영·Mac 처리·파일 내보내기는 서버/클라우드 계정 없이 로컬에서 완료하는 경로입니다. 외부 업로드는 별도 선택과 권한 검사를 거칩니다. 기존 암호화 자료·키·원본·완료 결과는 새 경로 검증 전 삭제하지 않습니다.

Viewer 구현 대상은 Safari·Chrome이고 공식 검증 환경은 macOS/iOS입니다. 각 실제 검사 전 지원 완료로 표시하지 않습니다. Windows/Linux Chrome은 호환 후보이며 Mac Chrome 검사로 입증하지 않습니다. 첫 공개 서버는 선택한 Ubuntu OCI/compose 단일 profile로 검증하고 사용자 앱의 OS 지원과 구분합니다.

Windows/Linux native Manager·Processing, Android Capture, iPhone 최종 Processing, Node 재구성, 다중 cloud/범용 원격 배포, AR/XR/Federation/기관 고급 연동은 후속 보류입니다. Node의 기존 검사·출력·백업 도구는 재사용할 수 있습니다.
