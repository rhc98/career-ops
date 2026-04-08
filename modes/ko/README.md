# career-ops -- 한국어 모드 (`modes/ko/`)

이 폴더는 한국 취업시장을 타겟으로 하는 사용자를 위한 career-ops 모드 한국어 번역을 담고 있습니다. 한국어 채용공고 평가, 자기소개서 작성, 이력서 생성, 포털 스캔 등을 한국 시장에 맞게 최적화합니다.

## 언제 이 모드를 사용하나요?

다음 중 하나라도 해당되면 `modes/ko/`를 사용하세요:

- **한국어 채용공고**에 주로 지원하는 경우 (Wanted, 잡코리아, 사람인, 점핏, 로켓펀치, 회사 채용페이지)
- **이력서가 한국어**이거나 공고에 따라 한국어/영어를 번갈아 사용하는 경우
- 자기소개서, 경력기술서 등 **한국식 지원 서류**가 필요한 경우
- **한국 시장 특유의 조건**을 평가해야 하는 경우: 4대보험, 퇴직금, 연봉 구조, 주 52시간, 수습 기간, 스톡옵션, 복리후생

대부분의 채용공고가 영어라면 기본 모드(`modes/`)를 그대로 사용하세요. 영어 모드도 한국어 공고를 처리할 수는 있지만, 한국 시장의 세부 사항을 같은 수준으로 반영하지는 못합니다.

## 활성화 방법

### 방법 1 -- 세션별 활성화

세션 시작 시 Claude에게 직접 말합니다:

> "한국어 모드를 사용해줘. `modes/ko/`에서 읽어줘."

또는

> "채용공고 평가를 한국어로 해줘 -- `modes/ko/_shared.md`와 `modes/ko/채용공고.md`를 사용해."

Claude가 `modes/` 대신 이 폴더의 파일을 읽습니다.

### 방법 2 -- 영구 설정

`config/profile.yml`에 언어 설정을 추가합니다:

```yaml
language:
  primary: ko
  modes_dir: modes/ko
```

첫 세션에서 Claude에게 이 설정을 참조하라고 알려주세요 ("`profile.yml`에 `language.modes_dir` 설정했어"). 이후 Claude가 자동으로 한국어 모드를 사용합니다.

## 번역된 모드 목록

| 파일 | 원본 | 역할 |
|------|------|------|
| `_shared.md` | `modes/_shared.md` (EN) | 공유 컨텍스트, 아키타입, 글로벌 규칙, 한국 시장 특화 |
| `채용공고.md` | `modes/oferta.md` (ES) | 채용공고 평가 (블록 A-F) |
| `지원.md` | `modes/apply.md` (EN) | 지원 폼 보조 + 자기소개서 생성 |
| `파이프라인.md` | `modes/pipeline.md` (ES) | URL 인박스 / 채용공고 수집 처리 |
| `자동파이프라인.md` | `modes/auto-pipeline.md` (EN) | JD -> 평가 -> PDF -> 트래커 전체 파이프라인 |
| `비교.md` | `modes/ofertas.md` (ES) | 복수 채용공고 비교/랭킹 |
| `연락.md` | `modes/contacto.md` (ES) | LinkedIn 아웃리치 |
| `기업조사.md` | `modes/deep.md` (EN) | 회사 심층 조사 |
| `이력서.md` | `modes/pdf.md` (ES) | PDF 이력서 생성 |
| `스캔.md` | `modes/scan.md` (EN) | 채용 포털 스캐너 |
| `배치.md` | `modes/batch.md` (EN) | 배치 처리 |
| `트래커.md` | `modes/tracker.md` (EN) | 지원 현황 조회 |
| `교육.md` | `modes/training.md` (EN) | 교육/자격증 평가 |
| `프로젝트.md` | `modes/project.md` (EN) | 포트폴리오 프로젝트 평가 |

## 영어로 유지하는 것들

의도적으로 번역하지 않는 표준 기술 용어:

- `cv.md`, `pipeline`, `tracker`, `report`, `score`, `archetype`, `proof point`
- 도구 이름 (`Playwright`, `WebSearch`, `WebFetch`, `Read`, `Write`, `Edit`, `Bash`)
- 트래커 상태값 (`Evaluated`, `Applied`, `Interview`, `Offer`, `Rejected`)
- 코드 스니펫, 파일 경로, 명령어

모드 파일은 한국 테크 업계에서 실제로 사용하는 자연스러운 한국어를 사용합니다: 한국어 본문에 영어 기술 용어가 자연스럽게 섞이는 방식. "Pipeline"을 "배관"으로 억지 번역하거나, `cv.md`를 "이력서 파일"로 바꾸지 않습니다.

## 용어 사전

모드를 수정하거나 확장할 때 이 용어를 기준으로 일관성을 유지하세요:

| English | 한국어 (이 코드베이스에서) |
|---------|--------------------------|
| Job posting | 채용공고 |
| Application | 지원 / 지원서 |
| Cover letter / Self-introduction | 자기소개서 |
| Resume / CV | 이력서 |
| Salary | 연봉 / 급여 |
| Compensation | 보상 패키지 / 연봉 |
| Skills | 기술 스택 / 역량 |
| Interview | 면접 |
| Hiring manager | 채용 담당자 |
| Recruiter | 리크루터 |
| AI | AI / 인공지능 |
| Requirements | 자격요건 |
| Nice-to-have / Preferred | 우대사항 |
| Career history | 경력사항 |
| Notice period | 퇴사 예정일 |
| Probation | 수습 기간 |
| Vacation / PTO | 연차 |
| Severance | 퇴직금 |
| 4 major insurances | 4대보험 |
| Stock options | 스톡옵션 |
| Permanent employment | 정규직 |
| Contract employment | 계약직 |
| Internship | 인턴 |
| Benefits / Perks | 복리후생 |
| Company culture | 기업문화 |
| Work-life balance | 워라밸 |
| Base salary | 기본급 |
| Performance bonus | 성과급 |
| Annual salary | 연봉 |

## 한국 시장 주요 특징

이 모드는 다음 한국 시장 특화 요소를 반영합니다:

- **4대보험**: 국민연금, 건강보험, 고용보험, 산재보험 (정규직 기본)
- **퇴직금**: 1년 이상 근무 시 법정 의무
- **주 52시간**: 법정 근로시간 상한
- **연봉 구조**: 기본급 + 성과급 + 인센티브 (기본급 비중 확인 중요)
- **자기소개서**: 한국 고유의 지원 서류 (성장과정/지원동기/입사후포부)
- **채용 포털**: Wanted, 잡코리아, 사람인, 점핏, 로켓펀치
- **기업 유형**: 대기업/중견기업/스타트업/외국계의 서로 다른 평가 기준

## 기여하기

번역을 개선하거나 모드를 추가하고 싶다면:

1. `CONTRIBUTING.md`에 따라 Issue를 열어주세요
2. 위 용어 사전을 기준으로 일관된 톤을 유지하세요
3. 의역으로 자연스럽게 -- 직역은 금물
4. 구조적 요소(블록 A-F, 테이블, 코드 블록, 도구 지침)는 그대로 유지
5. 실제 한국어 채용공고(Wanted, 잡코리아 등)로 테스트한 뒤 PR을 올려주세요
