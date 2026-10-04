# 설계 결정 기록 (ADR)

결정마다 한 장씩, "왜 이렇게 했는가"를 남긴다. 형식: 결정 / 배경 / 대안 / 결과.

| 번호 | 결정 |
|---|---|
| [0001](0001-rule-based-first.md) | AI보다 규칙 기반을 우선한다 |
| [0002](0002-collect-all-validation.md) | 사용자 입력 검증은 Collect-All |
| [0003](0003-all-or-nothing-application.md) | 신청 오류는 전체 반려 |
| [0004](0004-failed-application-is-terminal.md) | 실패한 신청은 종료 상태, 재신청은 새 신청 |
| [0005](0005-line-identity-and-chain.md) | 번호는 PK가 아니고, 번호 변경은 새 Line + 이전 Line 링크 |
| [0006](0006-rule-logic-vs-rule-data.md) | 규칙은 로직(코드)과 데이터(DB)를 분리 |
| [0007](0007-distrust-external-system.md) | 외부 시스템 결과는 사후 검증한다 |
| [0008](0008-validate-and-submit-separated.md) | 검증과 제출 API를 분리 |
| [0009](0009-approval-webhook.md) | 결재 결과는 웹훅으로 수신 |
