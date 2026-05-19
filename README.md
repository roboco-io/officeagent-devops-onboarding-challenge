# OfficeAgent DevOps/AIOps 채용 과제 — AWS → NHN → 오픈스택 마이그레이션 설계

## 시작하기

이 리포지토리를 **Use this template**으로 복사한 후, 아래 PRD에 따라 과제를 진행하세요.

[![Use this template](https://img.shields.io/badge/Use_this_template-238636?style=for-the-badge&logo=github&logoColor=white)](https://github.com/roboco-io/officeagent-devops-onboarding-challenge/generate)

GitHub 로그인 상태에서 위 버튼을 누르면 "Create a new repository from officeagent-devops-onboarding-challenge" 페이지로 바로 이동합니다.

## 과제 내용

**[PRD 바로가기 →](./docs/PRD.md)**

OfficeAgent 인프라를 AWS에서 NHN 클라우드로, 장기적으로 오픈스택 기반 온프레미스로 단계적 이전하는 **마이그레이션 설계서 + 발표 세션**을 작성합니다. 코드 구현은 선택이며 PoC 수준으로 충분합니다.

### 평가 역량 — 3축 매핑

| 평가 능력 | 채점 영역 | 비중 |
|----------|----------|-----:|
| **아키텍처 설계능력** | 마이그레이션 설계 + 멀티 환경 추상화 | 30% + 20% = **50%** |
| **구현 및 검증능력** | 구현 · 검증 가능성 (`VALIDATION.md` 또는 MIGRATION_PLAN §검증) | **20%** |
| **잘 모르는 분야 학습능력** | 조사 · 학습 깊이 (+ Track C 20점 보조) | **20%** |
| (보조) 발표 · 소통 | 30분 Q&A에서 위 3축 검증 수단 | **10%** |

### 기술 스택

- **IaC 도구:** 자유 (Terraform / OpenTofu / Pulumi / Crossplane / Ansible 등). NHN+오픈스택 둘 다 대응 가능한 구조 입증이 필요.
- **클라우드 계정:** 불필요 (실 apply 없음, 설계 + 선택적 plan/dry-run으로 충분)
- **LLM (선택 PoC용):** Claude Code SDK 또는 Codex CLI

### 5개 도메인 중 2개를 깊이

PRD §1.1의 5개 도메인 (네트워크·데이터·컴퓨트·관측·비용) 중 **2개를 정해 깊이 분석**하고 나머지는 매핑·미해결 가정 수준으로 다룹니다. **넓고 얕게보다 좁고 깊게**가 더 높이 평가됩니다.

## Retrobot — 자동 회고

이 프로젝트에는 [Retrobot](./retrobot/README.md)이 포함되어 있습니다. `git commit`할 때마다 Claude Code / Codex 작업 로그를 분석하여 KPT 회고를 자동 생성합니다.

**초기 설정 (리포지토리 생성 후 1회):**

```bash
git config core.hooksPath .githooks
```

> 유료 AI 구독(Claude Pro/Max 또는 ChatGPT Pro)이 없는 경우 수동으로 `retros/YYYY-MM-DD.md` 학습 일지를 작성하셔도 평가 불이익 없습니다. PRD §기술 조건 참조.

## 디렉토리 구조

```
.
├── docs/
│   ├── PRD.md                     # 과제 PRD (요구사항·5영역 채점표·2026-05-31 23:59 KST 마감)
│   └── TEMPLATE_GUIDE.md          # 본 템플릿 사용 가이드 (선택형 깊이 + 검증 산출물 안내)
├── MIGRATION_PLAN.template.md     # 마이그레이션 설계서 + §6 검증 계획 → MIGRATION_PLAN.md
├── ARCHITECTURE.template.md       # 추상화 설계 → ARCHITECTURE.md
├── VALIDATION.template.md         # 검증 산출물 (PRD §1.3, 필수) → VALIDATION.md
│                                  #   ※ MIGRATION_PLAN §6에 통합해도 동등
├── deck/                          # 발표 자료 (PDF/Keynote/Markdown deck 자유)
├── retros/                        # Retrobot 또는 수동 학습 일지
├── infra/                         # (선택) IaC PoC 확장
├── runbooks/                      # (선택) 운영 자동화·AIOps PoC
├── scripts/                       # (선택) 검증 스크립트
├── observability/                 # (선택) 메트릭/로그 대시보드 정의
├── .githooks/                     # Retrobot post-commit 훅
└── retrobot/                      # Retrobot 스킬 정의
```

## 제출 방법

1. 아래 버튼 클릭, 또는 우측 상단 **"Use this template"** → **"Create a new repository"**:

   [![Use this template](https://img.shields.io/badge/Use_this_template-238636?style=for-the-badge&logo=github&logoColor=white)](https://github.com/roboco-io/officeagent-devops-onboarding-challenge/generate)
2. Owner를 본인 계정으로, **Private** 리포지토리로 생성
3. `git config core.hooksPath .githooks` 실행 (Retrobot 활성화)
4. PRD에 따라 과제 진행
5. [`serithemage`](https://github.com/serithemage)를 Collaborator로 초대

**기한:** 2026-05-31 (일) 23:59 KST
**발표 세션:** 제출 마감 후 7일 이내, 30분 발표 + 30분 Q&A

자세한 내용은 [PRD](./docs/PRD.md) · [본 템플릿 가이드](./docs/TEMPLATE_GUIDE.md)를 참고하세요.
