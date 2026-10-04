# LineFlow

기업용 테스트 회선 **신청 · 승인 · 개통 · 연장** 업무 자동화 시스템 (개인 포트폴리오 프로젝트)

> **안내**: 이 프로젝트는 실제 업무에서 발견한 *문제 상황의 아이디어*만 일반화하여 새로 설계한 개인 프로젝트입니다.
> 회사명, 시스템명, 직원 정보, 번호, 단말 정보, 오류 코드, 내부 문서는 모두 **가상**이며 실제 정보를 사용하지 않습니다.
> (가상 시스템: `ApprovalHub` = 전자결재, `LegacyProv` = 기존 개통 시스템)

## 한 문장 정의
회선 신청·연장·해지 업무에서 사람이 눈으로 하던 검증과 반복 입력을 규칙 기반 Validation, 자동 비교, 구조화된 Error Code로 대체하고, 해결할 수 없는 예외만 운영 담당자에게 넘기는 시스템.

## 설계 철학
1. 잘못된 입력은 신청 시점에 막는다 (사전 Validation)
2. 오류는 모호한 메시지가 아니라 정확한 Error Code로 알린다
3. 반복 업무는 규칙 기반으로 자동화한다
4. 두 시스템의 데이터를 자동으로 비교한다
5. 외부 시스템(LegacyProv)의 결과는 믿지 않고 사후 검증한다
6. AI는 필요한 곳(매뉴얼 기반 문의)에만, 가장 마지막에 적용한다
7. 예외는 사람이 처리한다 (80% 자동화)

## 기술 스택 (계획)
Java 21, Spring Boot, Spring Data JPA, PostgreSQL, Docker, GitHub Actions, Swagger/OpenAPI, JUnit, Testcontainers

## 문서
| 문서 | 내용 |
|---|---|
| [01 문제 정의](docs/01-problem-definition.md) | 핵심 문제, 사용자, 프로젝트 가치 |
| [02 As-Is](docs/02-as-is.md) | 현재 업무 프로세스 |
| [03 Pain Point](docs/03-pain-points.md) | 문제 우선순위 |
| [04 To-Be](docs/04-to-be.md) | 개선된 프로세스, 정책 |
| [05 자동화 범위](docs/05-automation-scope.md) | 자동 / 반자동 / 수동 구분 |
| [06 MVP 범위](docs/06-mvp-scope.md) | 포함 / 제외, 버전 계획 |
| [07 도메인 모델](docs/07-domain-model.md) | 개념, 상태 머신 |
| [08 ERD](docs/08-erd.md) | 데이터 모델 (작성 중) |
| [설계 결정 기록](docs/decisions/) | ADR: 왜 이렇게 설계했나 |

## 진행 상황
- [x] STEP 1~7 기획 및 도메인 모델링
- [ ] STEP 8 ERD (작성 중)
- [ ] STEP 9~ API, Validation, Error Code, 구현
