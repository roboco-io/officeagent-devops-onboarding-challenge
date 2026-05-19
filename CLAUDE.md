# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 프로젝트 개요

OfficeAgent DevOps/AIOps 채용 과제 — **AWS → NHN 클라우드 → (장기) 오픈스택 마이그레이션 설계**. OfficeAgent 운영 인프라(별첨 가상 스펙)를 NHN과 오픈스택 둘 다 대응 가능한 마이그레이션 아키텍처로 설계하고 발표하는 과제 리포지토리.

## 핵심 요구사항

1. **마이그레이션 설계서 (`MIGRATION_PLAN.md`)** — 5개 도메인(네트워크·데이터·컴퓨트·관측·비용) 중 **2개를 깊이 분석**, 나머지는 매핑 수준
2. **추상화 설계 (`ARCHITECTURE.md`)** — NHN/오픈스택 둘 다 대응 가능한 분리 설계 (다이어그램·모듈)
3. **검증 산출물 (`VALIDATION.md` 또는 MIGRATION_PLAN §6)** — 깊이 다룬 도메인 2개에 각 1개 이상의 시나리오. 형태 자유(IaC skeleton·리허설·SQL·runbook·비용 표 등). 입력·명령·기대 출력·실패 판단 기준 필수.
4. **발표 자료 (`deck/`)** — 30분 발표 + 30분 Q&A. 핵심 의사결정 3~5개 트레이드오프 표
5. **회고 (`retros/`)** — Retrobot 자동 생성 또는 수동 학습 일지

## 기술 조건

- **IaC 도구**: 자유 (Terraform / OpenTofu / Pulumi / Crossplane / Ansible 등). NHN+오픈스택 둘 다 대응 가능한 구조 입증 필요
- **클라우드 계정**: 불필요 (실 apply 없음, 설계 + 선택적 plan/dry-run으로 충분)
- **LLM SDK (선택 PoC용)**: `claude-code-sdk` (pip) 또는 `@openai/codex` (npm) 중 택 1 — 구독 기반
- **AI 도구 부재 시**: 수동 `retros/*.md` 학습 일지로 대체 가능 (평가 불이익 없음)

## 필수 산출물

- `MIGRATION_PLAN.md` — 마이그레이션 설계서 (`MIGRATION_PLAN.template.md` 기반)
- `ARCHITECTURE.md` — 추상화 설계 (`ARCHITECTURE.template.md` 기반)
- `VALIDATION.md` (또는 MIGRATION_PLAN §6 검증 계획) — 검증 산출물 (`VALIDATION.template.md` 기반)
- `deck/` 안의 발표 자료 (PDF/Keynote/Markdown deck 자유)
- `retros/` 안의 회고 또는 학습 일지

## 선택 산출물 (가산점)

- `infra/` — IaC PoC
- `runbooks/`, `scripts/` — 운영 자동화·AIOps PoC (알람 진단, 드리프트 비교, 비용 이상치 감지 등)

## 별첨 AWS 스펙

`docs/PRD.md` §부록의 **가상 AWS 스펙 골격**을 출발점으로 합니다. VPC + ALB + ECS Fargate + RDS PostgreSQL + S3 + ElastiCache Redis + CloudWatch + IAM + GitHub Actions 수준. 가상 트래픽·CSAP 컴플라이언스·4시간 다운타임 제약이 명시되어 있습니다.

## AGENTS.md

`AGENTS.md`는 `CLAUDE.md`의 심볼릭 링크. Codex 등 다른 AI 에이전트도 동일한 지침을 읽을 수 있도록 제공.

## Retrobot (자동 회고)

- `retrobot/SKILL.md` — AI 에이전트가 읽고 실행하는 KPT 회고 생성 지침
- `.githooks/post-commit` — 커밋 후 `claude` 또는 `codex` CLI 호출
- 커밋 메시지에 "Retrobot"이 포함되면 훅 스킵 (무한 루프 방지)
- 회고는 `retros/` 디렉토리에 저장되고 자동 커밋

### 설정

```bash
git config core.hooksPath .githooks
```

### 수동 실행 (AI 도구 가용 시)

```bash
claude -p "$(cat retrobot/SKILL.md)"   # Claude Code
codex "$(cat retrobot/SKILL.md)"       # Codex
```

## 평가 비중 — 3축 매핑

| 평가 능력 | 영역 | 비중 |
|----------|------|-----:|
| **아키텍처 설계능력** | 마이그레이션 설계 · 의사결정 | 30% |
| **아키텍처 설계능력** | 멀티 환경 추상화 | 20% |
| **구현 및 검증능력** | 구현 · 검증 가능성 (§1.3 검증 산출물의 재현성·구체성) | 20% |
| **잘 모르는 분야 학습능력** | 조사 · 학습 깊이 (1차 자료, 미지 영역 분해, 학습 후 설계 변경) | 20% |
| (보조 — 위 3축 검증 수단) | 발표 · 소통 (30분 Q&A 응답 깊이, 미해결 위험 솔직성) | 10% |

**Track C (학습 궤적, 20점)**은 별도 보조 지표 — 60~75점 경계 후보의 우선순위 카드.

**완성도보다 의사결정·조사 흔적이 우선.** 단, **핵심 결정**(본인이 깊이 다루기로 한 도메인)에는 잠정 결론과 검증 계획이 필요합니다 — 단순 "후속 조사 필요"는 감점.
