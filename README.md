# Career-Ops

**[:kr: 한국어](#career-ops란)** | **[:gb: English](#what-is-this)** | **[:es: Español](#es-versión-en-español)**

> AI 에이전트 기반 취업 파이프라인. Claude Code로 채용공고 평가, 맞춤형 이력서 생성, 포털 스캔, 지원 현황 추적을 자동화합니다.

![Claude Code](https://img.shields.io/badge/Claude_Code-000?style=flat&logo=anthropic&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)
![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat&logo=playwright&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)

---

<p align="center">
  <img src="docs/demo.gif" alt="Career-Ops Demo" width="800">
</p>

## Career-Ops란

Career-Ops는 Claude Code를 취업 검색 통합 관제 시스템으로 만들어줍니다. 스프레드시트에 수동으로 지원 현황을 관리하는 대신, AI 기반 파이프라인이 모든 것을 처리합니다:

- **채용공고 평가** -- A-F 구조화된 스코어링 시스템 (10개 가중치 기반)
- **맞춤형 PDF 생성** -- 공고별 ATS 최적화 이력서 자동 생성
- **포털 자동 스캔** -- Greenhouse, Ashby, Lever, 회사 채용 페이지 자동 탐색
- **배치 처리** -- 서브 에이전트를 활용해 10개 이상 공고를 병렬 평가
- **통합 추적** -- 단일 소스 오브 트루스 + 무결성 검사

> **중요: 이것은 무차별 지원 도구가 아닙니다.** Career-ops는 필터입니다 -- 수백 개 공고 중 지원할 가치가 있는 것만 골라줍니다. 4.0/5 이하 공고에는 지원하지 않는 것을 강력히 권장합니다. 당신의 시간도, 리크루터의 시간도 소중합니다. 제출 전 반드시 검토하세요.

Career-ops는 에이전틱합니다: Claude Code가 Playwright로 채용 페이지를 탐색하고, 키워드 매칭이 아닌 이력서 vs 채용공고 추론으로 적합도를 평가하며, 공고별로 이력서를 맞춤 조정합니다.

> **참고: 처음 몇 번의 평가는 정확하지 않을 수 있습니다.** 시스템이 아직 당신을 모르기 때문입니다. 이력서, 커리어 스토리, 핵심 성과, 선호도, 강점, 피하고 싶은 것 등 맥락을 제공해주세요. 더 많이 알려줄수록 더 좋은 필터가 됩니다. 새로운 리크루터 온보딩이라고 생각하세요 -- 첫 주에는 당신을 알아가는 시간이 필요하고, 그 이후로는 없어서는 안 될 존재가 됩니다.

740개 이상의 채용공고를 평가하고, 100개 이상의 맞춤형 이력서를 생성하고, Head of Applied AI 포지션을 획득한 경험을 바탕으로 만들어졌습니다. [전체 케이스 스터디 보기](https://santifer.io/career-ops-system).

## 주요 기능

| 기능 | 설명 |
|------|------|
| **자동 파이프라인** | URL 붙여넣기 한 번으로 평가 + PDF + 트래커 엔트리 완성 |
| **6블록 평가** | 역할 요약, 이력서 매칭, 레벨 전략, 보상 리서치, 개인화, 면접 준비 (STAR+R) |
| **면접 스토리 뱅크** | 평가할 때마다 STAR+Reflection 스토리를 축적 -- 5~10개 마스터 스토리로 모든 행동 면접 질문에 대응 |
| **협상 스크립트** | 연봉 협상 프레임워크, 지역 할인 반박, 경쟁 오퍼 레버리지 |
| **ATS PDF 생성** | Space Grotesk + DM Sans 디자인의 키워드 주입 이력서 |
| **포털 스캐너** | 45개 이상 기업 사전 설정 (Anthropic, OpenAI, ElevenLabs, Retool, n8n...) + Ashby, Greenhouse, Lever, Wellfound 커스텀 쿼리 |
| **배치 처리** | `claude -p` 워커로 병렬 평가 |
| **대시보드 TUI** | 터미널 UI로 파이프라인 탐색, 필터링, 정렬 |
| **휴먼-인-더-루프** | AI가 평가하고 추천하면, 당신이 결정하고 행동. 시스템이 지원서를 제출하지 않습니다 -- 최종 결정은 항상 당신 |
| **파이프라인 무결성** | 자동 병합, 중복 제거, 상태 정규화, 헬스 체크 |

## 빠른 시작

```bash
# 1. 클론 및 설치
git clone https://github.com/santifer/career-ops.git
cd career-ops && npm install
npx playwright install chromium   # PDF 생성에 필요

# 2. 설정 확인
npm run doctor                     # 모든 전제조건 검증

# 3. 설정
cp config/profile.example.yml config/profile.yml  # 본인 정보로 수정
cp templates/portals.example.yml portals.yml       # 기업 목록 커스터마이즈

# 4. 이력서 추가
# 프로젝트 루트에 cv.md를 만들고 마크다운으로 이력서 작성

# 5. Claude와 함께 개인화
claude   # 이 디렉토리에서 Claude Code 실행

# Claude에게 시스템을 맞춤 설정하도록 요청:
# "아키타입을 백엔드 엔지니어링 역할로 변경해줘"
# "모드를 한국어로 설정해줘"
# "portals.yml에 이 기업들 추가해줘"
# "이 이력서로 프로필 업데이트해줘"

# 6. 사용 시작
# 채용공고 URL을 붙여넣거나 /career-ops 실행
```

> **이 시스템은 Claude가 직접 커스터마이즈하도록 설계되었습니다.** 모드, 아키타입, 스코어링 가중치, 협상 스크립트 -- 그냥 Claude에게 바꿔달라고 하세요. Claude가 사용하는 파일을 직접 읽기 때문에 정확히 무엇을 수정해야 하는지 알고 있습니다.

전체 설정 가이드는 [docs/SETUP.md](docs/SETUP.md)를 참고하세요.

## 사용법

Career-ops는 하나의 슬래시 커맨드에 여러 모드로 작동합니다:

```
/career-ops                → 사용 가능한 모든 명령어 표시
/career-ops {JD 붙여넣기}   → 전체 자동 파이프라인 (평가 + PDF + 트래커)
/career-ops scan           → 포털 스캔
/career-ops pdf            → ATS 최적화 이력서 생성
/career-ops batch          → 배치 평가
/career-ops tracker        → 지원 현황 조회
/career-ops apply          → AI로 지원서 작성
/career-ops pipeline       → 대기 URL 처리
/career-ops contacto       → LinkedIn 아웃리치 메시지
/career-ops deep           → 기업 심층 리서치
/career-ops training       → 교육/자격증 평가
/career-ops project        → 포트폴리오 프로젝트 평가
```

채용공고 URL이나 설명을 직접 붙여넣어도 됩니다 -- career-ops가 자동으로 감지하고 전체 파이프라인을 실행합니다.

## 작동 방식

```
채용공고 URL 또는 설명을 붙여넣기
        │
        ▼
┌──────────────────┐
│  아키타입         │  분류: LLMOps / Agentic / PM / SA / FDE / Transformation
│  감지             │
└────────┬─────────┘
         │
┌────────▼─────────┐
│  A-F 평가         │  매칭, 갭 분석, 보상 리서치, STAR 스토리
│  (cv.md 참조)     │
└────────┬─────────┘
         │
    ┌────┼────┐
    ▼    ▼    ▼
 리포트  PDF  트래커
  .md   .pdf   .tsv
```

## 사전 설정 포털

스캐너에는 **45개 이상의 기업**이 사전 설정되어 있고, 주요 채용 포털에서 **19개 검색 쿼리**가 준비되어 있습니다. `templates/portals.example.yml`을 `portals.yml`로 복사하고 원하는 기업을 추가하세요:

**AI Labs:** Anthropic, OpenAI, Mistral, Cohere, LangChain, Pinecone
**Voice AI:** ElevenLabs, PolyAI, Parloa, Hume AI, Deepgram, Vapi, Bland AI
**AI 플랫폼:** Retool, Airtable, Vercel, Temporal, Glean, Arize AI
**컨택 센터:** Ada, LivePerson, Sierra, Decagon, Talkdesk, Genesys
**엔터프라이즈:** Salesforce, Twilio, Gong, Dialpad
**LLMOps:** Langfuse, Weights & Biases, Lindy, Cognigy, Speechmatics
**자동화:** n8n, Zapier, Make.com
**유럽:** Factorial, Attio, Tinybird, Clarity AI, Travelperk

**채용 포털:** Ashby, Greenhouse, Lever, Wellfound, Workable, RemoteFront

## 대시보드 TUI

내장 터미널 대시보드로 파이프라인을 시각적으로 탐색할 수 있습니다:

```bash
cd dashboard
go build -o career-dashboard .
./career-dashboard
```

기능: 6개 필터 탭, 4가지 정렬 모드, 그룹/플랫 뷰, 지연 로딩 미리보기, 인라인 상태 변경.

## 프로젝트 구조

```
career-ops/
├── CLAUDE.md                    # 에이전트 지침
├── cv.md                        # 이력서 (직접 생성)
├── article-digest.md            # 핵심 성과/증거 (선택)
├── config/
│   └── profile.example.yml      # 프로필 템플릿
├── modes/                       # 14개 스킬 모드
│   ├── _shared.md               # 공유 컨텍스트 (커스터마이즈 대상)
│   ├── oferta.md                # 단일 평가
│   ├── pdf.md                   # PDF 생성
│   ├── scan.md                  # 포털 스캐너
│   ├── batch.md                 # 배치 처리
│   └── ...
├── templates/
│   ├── cv-template.html         # ATS 최적화 이력서 템플릿
│   ├── portals.example.yml      # 스캐너 설정 템플릿
│   └── states.yml               # 정규 상태값
├── batch/
│   ├── batch-prompt.md          # 독립 실행 워커 프롬프트
│   └── batch-runner.sh          # 오케스트레이터 스크립트
├── dashboard/                   # Go TUI 파이프라인 뷰어
├── data/                        # 추적 데이터 (gitignored)
├── reports/                     # 평가 리포트 (gitignored)
├── output/                      # 생성된 PDF (gitignored)
├── fonts/                       # Space Grotesk + DM Sans
├── docs/                        # 설정, 커스터마이즈, 아키텍처 문서
└── examples/                    # 샘플 이력서, 리포트, 증거 자료
```

## 기술 스택

![Claude Code](https://img.shields.io/badge/Claude_Code-000?style=flat&logo=anthropic&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)
![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat&logo=playwright&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)
![Bubble Tea](https://img.shields.io/badge/Bubble_Tea-FF75B5?style=flat&logo=go&logoColor=white)

- **에이전트**: Claude Code + 커스텀 스킬 및 모드
- **PDF**: Playwright/Puppeteer + HTML 템플릿
- **스캐너**: Playwright + Greenhouse API + WebSearch
- **대시보드**: Go + Bubble Tea + Lipgloss (Catppuccin Mocha 테마)
- **데이터**: Markdown 테이블 + YAML 설정 + TSV 배치 파일

## 함께 오픈소스

- **[cv-santiago](https://github.com/santifer/cv-santiago)** -- AI 챗봇, LLMOps 대시보드, 케이스 스터디가 포함된 포트폴리오 웹사이트(santifer.io). 취업과 함께 포트폴리오가 필요하다면 포크해서 자유롭게 활용하세요.

## 저자 소개

Santiago입니다 -- Head of Applied AI, 전 창업자 (직접 만들고 매각한 사업이 지금도 운영 중). 본인의 취업 과정을 관리하기 위해 career-ops를 만들었고, 실제로 이것을 사용해 현재 포지션을 획득했습니다.

포트폴리오 및 기타 오픈소스 프로젝트 → [santifer.io](https://santifer.io)

☕ career-ops가 취업에 도움이 되셨다면 [커피 한 잔 사주세요](https://buymeacoffee.com/santifer).

## 면책 조항

**career-ops는 로컬 오픈소스 도구이며 호스팅 서비스가 아닙니다.** 이 소프트웨어를 사용함으로써 다음에 동의하는 것입니다:

1. **데이터는 사용자가 관리합니다.** 이력서, 연락처, 개인 정보는 사용자의 머신에 저장되며, 사용자가 선택한 AI 제공자(Anthropic, OpenAI 등)에게만 직접 전송됩니다. 저희는 어떤 데이터도 수집, 저장, 접근하지 않습니다.
2. **AI는 사용자가 제어합니다.** 기본 프롬프트는 AI가 지원서를 자동 제출하지 않도록 지시하지만, AI 모델은 예측할 수 없게 동작할 수 있습니다. 프롬프트를 수정하거나 다른 모델을 사용하는 경우 그 책임은 사용자에게 있습니다. **제출 전 AI가 생성한 콘텐츠를 반드시 검토하세요.**
3. **서드파티 이용 약관을 준수합니다.** 채용 포털(Greenhouse, Lever, Workday, LinkedIn 등)의 이용 약관에 따라 이 도구를 사용해야 합니다. 이 도구를 기업 스팸이나 ATS 시스템 과부하에 사용하지 마세요.
4. **보증은 없습니다.** 평가는 추천이지 진실이 아닙니다. AI 모델은 기술이나 경험을 환각할 수 있습니다. 저자는 고용 결과, 거부된 지원서, 계정 제한 또는 기타 결과에 대해 책임지지 않습니다.

자세한 내용은 [LEGAL_DISCLAIMER.md](LEGAL_DISCLAIMER.md)를 참고하세요. 이 소프트웨어는 [MIT 라이선스](LICENSE)에 따라 어떠한 보증 없이 "있는 그대로" 제공됩니다.

## 문서

- [SETUP.md](docs/SETUP.md) -- 설치 가이드
- [CUSTOMIZATION.md](docs/CUSTOMIZATION.md) -- 커스터마이즈 방법
- [ARCHITECTURE.md](docs/ARCHITECTURE.md) -- 시스템 아키텍처

## 라이선스

MIT

---

# :gb: English

## What Is This

Career-Ops turns Claude Code into a full job search command center. Instead of manually tracking applications in a spreadsheet, you get an AI-powered pipeline that:

- **Evaluates offers** with a structured A-F scoring system (10 weighted dimensions)
- **Generates tailored PDFs** -- ATS-optimized CVs customized per job description
- **Scans portals** automatically (Greenhouse, Ashby, Lever, company pages)
- **Processes in batch** -- evaluate 10+ offers in parallel with sub-agents
- **Tracks everything** in a single source of truth with integrity checks

> **Important: This is NOT a spray-and-pray tool.** Career-ops is a filter -- it helps you find the few offers worth your time out of hundreds. The system strongly recommends against applying to anything scoring below 4.0/5. Your time is valuable, and so is the recruiter's. Always review before submitting.

Career-ops is agentic: Claude Code navigates career pages with Playwright, evaluates fit by reasoning about your CV vs the job description (not keyword matching), and adapts your resume per listing.

> **Heads up: the first evaluations won't be great.** The system doesn't know you yet. Feed it context -- your CV, your career story, your proof points, your preferences, what you're good at, what you want to avoid. The more you nurture it, the better it gets. Think of it as onboarding a new recruiter: the first week they need to learn about you, then they become invaluable.

Built by someone who used it to evaluate 740+ job offers, generate 100+ tailored CVs, and land a Head of Applied AI role. [Read the full case study](https://santifer.io/career-ops-system).

## Features

| Feature | Description |
|---------|-------------|
| **Auto-Pipeline** | Paste a URL, get a full evaluation + PDF + tracker entry |
| **6-Block Evaluation** | Role summary, CV match, level strategy, comp research, personalization, interview prep (STAR+R) |
| **Interview Story Bank** | Accumulates STAR+Reflection stories across evaluations -- 5-10 master stories that answer any behavioral question |
| **Negotiation Scripts** | Salary negotiation frameworks, geographic discount pushback, competing offer leverage |
| **ATS PDF Generation** | Keyword-injected CVs with Space Grotesk + DM Sans design |
| **Portal Scanner** | 45+ companies pre-configured (Anthropic, OpenAI, ElevenLabs, Retool, n8n...) + custom queries across Ashby, Greenhouse, Lever, Wellfound |
| **Batch Processing** | Parallel evaluation with `claude -p` workers |
| **Dashboard TUI** | Terminal UI to browse, filter, and sort your pipeline |
| **Human-in-the-Loop** | AI evaluates and recommends, you decide and act. The system never submits an application -- you always have the final call |
| **Pipeline Integrity** | Automated merge, dedup, status normalization, health checks |

## Quick Start

```bash
# 1. Clone and install
git clone https://github.com/santifer/career-ops.git
cd career-ops && npm install
npx playwright install chromium   # Required for PDF generation

# 2. Check setup
npm run doctor                     # Validates all prerequisites

# 3. Configure
cp config/profile.example.yml config/profile.yml  # Edit with your details
cp templates/portals.example.yml portals.yml       # Customize companies

# 4. Add your CV
# Create cv.md in the project root with your CV in markdown

# 5. Personalize with Claude
claude   # Open Claude Code in this directory

# Then ask Claude to adapt the system to you:
# "Change the archetypes to backend engineering roles"
# "Translate the modes to English"
# "Add these 5 companies to portals.yml"
# "Update my profile with this CV I'm pasting"

# 6. Start using
# Paste a job URL or run /career-ops
```

> **The system is designed to be customized by Claude itself.** Modes, archetypes, scoring weights, negotiation scripts -- just ask Claude to change them. It reads the same files it uses, so it knows exactly what to edit.

See [docs/SETUP.md](docs/SETUP.md) for the full setup guide.

## Usage

Career-ops is a single slash command with multiple modes:

```
/career-ops                → Show all available commands
/career-ops {paste a JD}   → Full auto-pipeline (evaluate + PDF + tracker)
/career-ops scan           → Scan portals for new offers
/career-ops pdf            → Generate ATS-optimized CV
/career-ops batch          → Batch evaluate multiple offers
/career-ops tracker        → View application status
/career-ops apply          → Fill application forms with AI
/career-ops pipeline       → Process pending URLs
/career-ops contacto       → LinkedIn outreach message
/career-ops deep           → Deep company research
/career-ops training       → Evaluate a course/cert
/career-ops project        → Evaluate a portfolio project
```

Or just paste a job URL or description directly -- career-ops auto-detects it and runs the full pipeline.

## How It Works

```
You paste a job URL or description
        │
        ▼
┌──────────────────┐
│  Archetype       │  Classifies: LLMOps / Agentic / PM / SA / FDE / Transformation
│  Detection       │
└────────┬─────────┘
         │
┌────────▼─────────┐
│  A-F Evaluation   │  Match, gaps, comp research, STAR stories
│  (reads cv.md)    │
└────────┬─────────┘
         │
    ┌────┼────┐
    ▼    ▼    ▼
 Report  PDF  Tracker
  .md   .pdf   .tsv
```

## Pre-configured Portals

The scanner comes with **45+ companies** ready to scan and **19 search queries** across major job boards. Copy `templates/portals.example.yml` to `portals.yml` and add your own:

**AI Labs:** Anthropic, OpenAI, Mistral, Cohere, LangChain, Pinecone
**Voice AI:** ElevenLabs, PolyAI, Parloa, Hume AI, Deepgram, Vapi, Bland AI
**AI Platforms:** Retool, Airtable, Vercel, Temporal, Glean, Arize AI
**Contact Center:** Ada, LivePerson, Sierra, Decagon, Talkdesk, Genesys
**Enterprise:** Salesforce, Twilio, Gong, Dialpad
**LLMOps:** Langfuse, Weights & Biases, Lindy, Cognigy, Speechmatics
**Automation:** n8n, Zapier, Make.com
**European:** Factorial, Attio, Tinybird, Clarity AI, Travelperk

**Job boards searched:** Ashby, Greenhouse, Lever, Wellfound, Workable, RemoteFront

## Dashboard TUI

The built-in terminal dashboard lets you browse your pipeline visually:

```bash
cd dashboard
go build -o career-dashboard .
./career-dashboard
```

Features: 6 filter tabs, 4 sort modes, grouped/flat view, lazy-loaded previews, inline status changes.

## Project Structure

```
career-ops/
├── CLAUDE.md                    # Agent instructions
├── cv.md                        # Your CV (create this)
├── article-digest.md            # Your proof points (optional)
├── config/
│   └── profile.example.yml      # Template for your profile
├── modes/                       # 14 skill modes
│   ├── _shared.md               # Shared context (customize this)
│   ├── oferta.md                # Single evaluation
│   ├── pdf.md                   # PDF generation
│   ├── scan.md                  # Portal scanner
│   ├── batch.md                 # Batch processing
│   └── ...
├── templates/
│   ├── cv-template.html         # ATS-optimized CV template
│   ├── portals.example.yml      # Scanner config template
│   └── states.yml               # Canonical statuses
├── batch/
│   ├── batch-prompt.md          # Self-contained worker prompt
│   └── batch-runner.sh          # Orchestrator script
├── dashboard/                   # Go TUI pipeline viewer
├── data/                        # Your tracking data (gitignored)
├── reports/                     # Evaluation reports (gitignored)
├── output/                      # Generated PDFs (gitignored)
├── fonts/                       # Space Grotesk + DM Sans
├── docs/                        # Setup, customization, architecture
└── examples/                    # Sample CV, report, proof points
```

## Tech Stack

![Claude Code](https://img.shields.io/badge/Claude_Code-000?style=flat&logo=anthropic&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)
![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat&logo=playwright&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)
![Bubble Tea](https://img.shields.io/badge/Bubble_Tea-FF75B5?style=flat&logo=go&logoColor=white)

- **Agent**: Claude Code with custom skills and modes
- **PDF**: Playwright/Puppeteer + HTML template
- **Scanner**: Playwright + Greenhouse API + WebSearch
- **Dashboard**: Go + Bubble Tea + Lipgloss (Catppuccin Mocha theme)
- **Data**: Markdown tables + YAML config + TSV batch files

## Also Open Source

- **[cv-santiago](https://github.com/santifer/cv-santiago)** -- The portfolio website (santifer.io) with AI chatbot, LLMOps dashboard, and case studies. If you need a portfolio to showcase alongside your job search, fork it and make it yours.

## About the Author

I'm Santiago -- Head of Applied AI, former founder (built and sold a business that still runs with my name on it). I built career-ops to manage my own job search. It worked: I used it to land my current role.

My portfolio and other open source projects → [santifer.io](https://santifer.io)

☕ [Buy me a coffee](https://buymeacoffee.com/santifer) if career-ops helped your job search.

## Disclaimer

**career-ops is a local, open-source tool — NOT a hosted service.** By using this software, you acknowledge:

1. **You control your data.** Your CV, contact info, and personal data stay on your machine and are sent directly to the AI provider you choose (Anthropic, OpenAI, etc.). We do not collect, store, or have access to any of your data.
2. **You control the AI.** The default prompts instruct the AI not to auto-submit applications, but AI models can behave unpredictably. If you modify the prompts or use different models, you do so at your own risk. **Always review AI-generated content for accuracy before submitting.**
3. **You comply with third-party ToS.** You must use this tool in accordance with the Terms of Service of the career portals you interact with (Greenhouse, Lever, Workday, LinkedIn, etc.). Do not use this tool to spam employers or overwhelm ATS systems.
4. **No guarantees.** Evaluations are recommendations, not truth. AI models may hallucinate skills or experience. The authors are not liable for employment outcomes, rejected applications, account restrictions, or any other consequences.

See [LEGAL_DISCLAIMER.md](LEGAL_DISCLAIMER.md) for full details. This software is provided under the [MIT License](LICENSE) "as is", without warranty of any kind.

## License

MIT

---

# :es: Version en Español

## Que es esto

Career-Ops convierte Claude Code en un centro de mando de busqueda de empleo. En vez de trackear aplicaciones en un spreadsheet, tienes un pipeline AI que:

- **Evalua ofertas** con scoring estructurado A-F (10 dimensiones ponderadas)
- **Genera PDFs personalizados** -- CVs ATS-optimizados por oferta
- **Escanea portales** automaticamente (Greenhouse, Ashby, Lever, webs de empresas)
- **Procesa en batch** -- evalua 10+ ofertas en paralelo con sub-agentes
- **Trackea todo** en una fuente de verdad unica con checks de integridad

> **Importante: Esto NO es para spamear empresas.** Career-ops es un filtro -- te ayuda a encontrar las pocas ofertas que merecen tu tiempo entre cientos. El sistema recomienda encarecidamente no aplicar a nada por debajo de 4.0/5. Tu tiempo es valioso, y el del recruiter tambien. Siempre revisa antes de enviar.

> **Aviso: las primeras evaluaciones no seran buenas.** El sistema no te conoce todavia. Dale contexto -- tu CV, tu historia profesional, tus proof points, tus preferencias, en que eres bueno, que quieres evitar. Cuanto mas lo nutras, mejor filtra. Piensa en ello como hacer onboarding a un recruiter nuevo: la primera semana necesita conocerte, luego se vuelve invaluable.

Construido por alguien que lo uso para evaluar 740+ ofertas, generar 100+ CVs personalizados, y conseguir un rol de Head of Applied AI. [Lee el case study completo](https://santifer.io/career-ops).

## Inicio rapido

```bash
# 1. Clonar
git clone https://github.com/santifer/career-ops.git
cd career-ops && npm install

# 2. Verificar setup
npm run doctor                     # Valida todos los prerequisitos

# 3. Configurar
cp config/profile.example.yml config/profile.yml  # Editar con tus datos
cp templates/portals.example.yml portals.yml       # Personalizar empresas

# 4. Añadir tu CV
# Crear cv.md en la raiz del proyecto con tu CV en markdown

# 5. Personalizar con Claude
claude   # Abrir Claude Code en este directorio

# Pidele a Claude que adapte el sistema a ti:
# "Cambia los arquetipos a roles de backend"
# "Traduce los modes a ingles"
# "Añade estas empresas a portals.yml"
# "Actualiza mi perfil con este CV que te pego"

# 6. Usar
# Pega una URL de oferta o ejecuta /career-ops
```

> **El sistema esta diseñado para que Claude lo personalice.** Modes, arquetipos, scoring, scripts de negociacion -- solo pidelo. Claude lee los mismos archivos que usa, asi que sabe exactamente que editar.

Guia completa en [docs/SETUP.md](docs/SETUP.md).

## Portales incluidos

El scanner viene con **45+ empresas** pre-configuradas y **19 queries** en los principales portales de empleo. Copia `templates/portals.example.yml` a `portals.yml` y añade las tuyas:

**AI Labs:** Anthropic, OpenAI, Mistral, Cohere, LangChain, Pinecone
**Voice AI:** ElevenLabs, PolyAI, Parloa, Hume AI, Deepgram, Vapi, Bland AI
**Plataformas AI:** Retool, Airtable, Vercel, Temporal, Glean, Arize AI
**Contact Center:** Ada, LivePerson, Sierra, Decagon, Talkdesk, Genesys
**Enterprise:** Salesforce, Twilio, Gong, Dialpad
**LLMOps:** Langfuse, Weights & Biases, Lindy, Cognigy, Speechmatics
**Automatizacion:** n8n, Zapier, Make.com
**Europa:** Factorial, Attio, Tinybird, Clarity AI, Travelperk

**Portales de empleo:** Ashby, Greenhouse, Lever, Wellfound, Workable, RemoteFront

## Uso

Career-ops es un unico slash command con multiples modos:

```
/career-ops                → Mostrar todos los comandos
/career-ops {pega un JD}   → Pipeline completo (evaluar + PDF + tracker)
/career-ops scan           → Escanear portales
/career-ops pdf            → Generar CV ATS-optimizado
/career-ops batch          → Evaluar ofertas en batch
/career-ops tracker        → Ver estado de aplicaciones
/career-ops apply          → Rellenar formularios con IA
/career-ops pipeline       → Procesar URLs pendientes
/career-ops contacto       → Mensaje LinkedIn outreach
/career-ops deep           → Research profundo de empresa
```

O simplemente pega una URL o descripcion de oferta -- career-ops la detecta y ejecuta el pipeline completo.

## Tambien Open Source

- **[cv-santiago](https://github.com/santifer/cv-santiago)** -- El portfolio (santifer.io) con chatbot IA, dashboard LLMOps y case studies. Si necesitas un portfolio para acompañar tu busqueda de empleo, echale un vistazo.

## Documentacion

- [SETUP.md](docs/SETUP.md) -- Guia de instalacion
- [CUSTOMIZATION.md](docs/CUSTOMIZATION.md) -- Como personalizar
- [ARCHITECTURE.md](docs/ARCHITECTURE.md) -- Como funciona el sistema

☕ [Invitame a un cafe](https://buymeacoffee.com/santifer) si career-ops te ayudo en tu busqueda.

## Aviso legal

**career-ops es una herramienta local y open source — NO un servicio alojado.** Al usar este software, aceptas que:

1. **Tu controlas tus datos.** Tu CV, datos de contacto e informacion personal se quedan en tu maquina y se envian directamente al proveedor de IA que elijas (Anthropic, OpenAI, etc.). No recopilamos, almacenamos ni tenemos acceso a tus datos.
2. **Tu controlas la IA.** Los prompts por defecto instruyen a la IA a no enviar aplicaciones automaticamente, pero los modelos pueden comportarse de forma impredecible. Si modificas los prompts o usas otros modelos, lo haces bajo tu responsabilidad. **Revisa siempre el contenido generado antes de enviarlo.**
3. **Tu cumples con los terminos de terceros.** Debes usar esta herramienta de acuerdo con los Terminos de Servicio de los portales de empleo (Greenhouse, Lever, Workday, LinkedIn, etc.). No uses esta herramienta para spamear empresas.
4. **Sin garantias.** Las evaluaciones son recomendaciones, no verdad absoluta. Los modelos pueden inventar habilidades o experiencia. Los autores no son responsables de resultados laborales, candidaturas rechazadas, restricciones de cuenta ni ninguna otra consecuencia.

Ver [LEGAL_DISCLAIMER.md](LEGAL_DISCLAIMER.md) para mas detalles. Este software se proporciona bajo la [Licencia MIT](LICENSE) "tal cual", sin garantia de ningun tipo.

## Let's Connect

[![Website](https://img.shields.io/badge/santifer.io-000?style=for-the-badge&logo=safari&logoColor=white)](https://santifer.io)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/santifer)
[![Email](https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:hola@santifer.io)
[![Buy Me a Coffee](https://img.shields.io/badge/Buy_Me_a_Coffee-FFDD00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black)](https://buymeacoffee.com/santifer)
