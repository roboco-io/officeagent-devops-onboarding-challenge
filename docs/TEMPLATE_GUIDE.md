# 템플릿 사용 가이드

이 문서는 본 템플릿을 처음 받은 후 어떻게 시작하면 좋은지 안내합니다. PRD([`PRD.md`](./PRD.md))를 먼저 읽은 다음 본 가이드를 참고하세요.

## 1. 첫 30분 — 환경 셋업

```bash
# 1. Use this template으로 본인 계정에 Private 리포 생성
# 2. 클론 후 Retrobot 활성화
git clone <your-private-repo-url>
cd <repo-name>
git config core.hooksPath .githooks

# 3. (선택) Claude Code / Codex CLI 가용성 확인
claude --version 2>/dev/null || echo "Claude Code 미설치"
codex --version 2>/dev/null || echo "Codex CLI 미설치"
```

AI 도구가 둘 다 없어도 진행 가능합니다. `retros/` 디렉토리에 수동으로 KPT 일지(`YYYY-MM-DD.md`)를 작성하시면 동등하게 평가합니다.

## 2. 첫 2일 — 조사 + 도메인 2개 결정

PRD §1.1의 5개 도메인 중 **본인이 깊이 분석할 2개**를 먼저 결정하세요:

| 도메인 | 깊이 분석 시 기대 |
|--------|------------------|
| A. 네트워크 / 보안 | VPC↔NHN VPC, NAT 등가, IAM↔NHN 권한, CSAP 망분리 |
| B. 데이터 / 스토리지 | RDS↔NHN DB, S3↔Object Storage, 이전 단계·일관성 검증 |
| C. 컴퓨트 / 배포 | ECS Fargate↔NHN K8s/VM, 배포 파이프라인, 롤백 |
| D. 운영·관측 / AIOps | CloudWatch↔NHN 모니터링, AIOps 자동화 |
| E. 비용 / 규제 | 비용 정량 비교, CSAP·데이터 주권·계열사 정책 |

**선택 기준 힌트** — 본인이 이미 익숙한 영역 1개 + 도전적인 영역 1개를 섞으면 학습 궤적이 잘 드러납니다.

이 시점부터 1차 자료를 적극적으로 인용하세요:
- NHN Cloud docs: <https://docs.nhncloud.com/>
- CSAP 인증 가이드: KISA 또는 정보보호평가센터 자료
- 오픈스택 docs: <https://docs.openstack.org/>

## 3. 3~10일 — 설계서·아키텍처 작성

- `MIGRATION_PLAN.template.md` → `MIGRATION_PLAN.md`로 복사 후 채우기
- `ARCHITECTURE.template.md` → `ARCHITECTURE.md`로 복사 후 채우기
- 다이어그램: mermaid (리포에 직접) / draw.io (이미지 export) / Excalidraw / 손그림 스캔 자유
- "모른다"고 적을 영역은 **리스크 + 검증 계획**을 함께 적기 (단순 미답은 감점)

(선택) `infra/` 디렉토리에 IaC PoC 작성. NHN+오픈스택 둘 다 적용 가능한 모듈 일부면 충분.

## 4. 11~13일 — 발표 자료 작성

- `deck/` 디렉토리에 PDF/Keynote/Markdown deck (자유 형식)
- 핵심 의사결정 3~5개를 트레이드오프 표로 정리
- 가장 큰 미해결 위험 1~2개를 솔직히 명시 (감점 아닌 가산)
- 30분 발표 + 30분 Q&A 분량 가정

## 5. 14일차 — 제출

- 리포 모든 산출물 커밋 + push
- [`serithemage`](https://github.com/serithemage)를 Collaborator로 초대
- 마감: 공고일로부터 14일 후 KST 23:59

## 6. 제출 후 — 발표 세션

- 제출 마감 후 7일 이내 화상회의
- 30분 발표 + 30분 Q&A
- 평가자 2인 (엔지니어링 리드 + 시니어 멘토) 동석
- 표준 시작 질문: *"본인이 깊이 다룬 2개 도메인 중 가장 큰 미해결 위험 1개와 그 근거"*

## 자주 묻는 질문

**Q. 5개 도메인 다 다뤄야 하나요?**
아니오. 2개를 깊이, 나머지는 매핑·미해결 가정 수준이면 OK. 좁고 깊게가 더 높이 평가됩니다.

**Q. IaC 코드는 꼭 작성해야 하나요?**
아니오. 선택. 다이어그램·문서 분리 설계로 추상화 사고를 입증해도 됩니다.

**Q. NHN 계정이 필요한가요?**
불필요. 실 apply 없음. 설계 + (선택) `terraform plan` / `tofu plan` 정도면 충분.

**Q. AI 도구가 없으면 불리한가요?**
아니오. 수동 학습 일지로 대체 가능. 평가 불이익 없음.
