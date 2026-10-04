# 07. 도메인 모델

## 개념
| 개념 | 역할 | 상태 보유 | MVP |
|---|---|---|---|
| Application (신청) | 신청 헤더: 유형, 신청자, 승인 상태, 처리 상태 | O | O |
| ApplicationItem (신청 항목) | 회선별 단말, 요금제, 종료일, 번호 유지/변경 (한 신청에 5~100개) | O | O |
| Line (회선) | 배정된 번호를 가진 자원. 번호가 바뀌면 새 Line + 이전 Line 링크 | O | O |
| Device (단말) | 사전 등록된 단말 마스터, 예약 상태를 가짐 | O | O |
| Plan (요금제) | 요금제 마스터 | 사용 가능 여부 | O |
| DeviceType + 호환 규칙 | 단말 유형 × 요금제 × 번호 풀 호환성 | X (데이터) | O |
| NumberPool (번호 풀) | 번호 자원 구분 (일반 / 전용) — 가상 | X | O |
| Attachment (첨부) | 통보서 등 | X | O |
| ProvisioningAttempt | 개통/변경 단계별 실행 기록 | O | v0.3 |
| ErrorCode | 오류 코드 정의 | X | O |

## 두 개의 상태 축
| 축 | 관리 주체 | 의미 |
|---|---|---|
| 승인 상태 (approvalStatus) | ApprovalHub (외부), 우리는 결과를 복사 | 결재 진행 |
| 처리 상태 (processingStatus) | LineFlow | 검증, 비교, 개통 진행 정도 |

## 처리 상태 머신 v1
```
DRAFT ──제출(사전검증 통과)──▶ SUBMITTED
SUBMITTED ──(결재 승인 완료 수신)──▶ APPROVED
APPROVED ──자동 비교──▶ COMPARE_PASSED / COMPARE_FAILED(종료)
COMPARE_PASSED ──개통 요청──▶ PROVISIONING
PROVISIONING ──▶ COMPLETED(종료) / PROVISION_FAILED
PROVISION_FAILED ──롤백──▶ ROLLED_BACK(종료)
(결재 반려) ──▶ REJECTED(종료)
```
- 사전 검증 실패는 별도 상태가 아니라 DRAFT에 머물며 오류 목록만 반환한다.
- 종료 상태에서 되돌아가지 않는다. 재신청은 **새 Application**이다. (ADR-0004)

## 설계 원칙
1. 번호는 식별자가 아니다. 바뀌거나 재사용될 수 있는 값은 PK로 쓰지 않는다.
2. 상태를 거꾸로 돌리지 않는다. 실패는 종료 상태로 남기고 재신청은 새 건으로.
3. 규칙은 로직(코드)과 데이터(DB)를 분리한다.
4. 코드의 검증은 친절한 메시지를 위한 것, DB 제약은 최후의 방어선. 둘 다 둔다.
