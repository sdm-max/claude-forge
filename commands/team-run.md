---
name: team-run
description: 기획→UI→개발→보안→테스트→Docker배포 전체 팀 파이프라인. /team-run [기능 설명]
---
<Skill>team-orchestrator</Skill>

## STEP 1 — planner
<task>
agent: planner
PRD, 사용자 스토리, UI 목록, API 목록, DB 스키마, 완료 기준 작성.
기능: $ARGUMENTS
</task>task>

## STEP 2 — architect
<task>
agent: architect
컴포넌트 구조, API 스펙, DB 스키마, 파일 소유권 분리 계획 작성.
</task>task>

## STEP 3 — 병렬 구현 (동시 실행)
<task>
agent: e2e-runner
UI 디자인 + 프론트엔드. 담당: src/components/ src/pages/ src/styles/ src/hooks/
Tailwind CSS, 모바일 반응형 필수. ⚠️ src/types/ src/api/ 수정 금지
</task>task>
<task>
  agent: build-error-resolver
  백엔드 + DB. 담당: src/api/ src/db/ src/types/ src/middleware/
  ⚠️ src/components/ src/pages/ 수정 금지
</task>task>

## STEP 4 — security-reviewer
<task>
  agent: security-reviewer
  OWASP Top10, STRIDE, 시크릿 탐지, npm audit. Critical/High/Medium/Low 분류 + 수정 코드 제시.
</task>task>

## STEP 5 — tdd-guide
<task>
  agent: tdd-guide
  Jest 유닛·통합 + Playwright E2E. RED→GREEN→IMPROVE. 커버리지 80% 이상.
</task>task>

## STEP 6 — 병렬 마무리 (동시 실행)
<task>
  agent: verify-agent
  빌드·타입·린트·테스트 검증 + Dockerfile + docker-compose.yml + nginx.conf + deploy/deploy.sh
  CLAUDE.md의 DEPLOY_HOST, SSH_KEY, DOMAIN 참조하여 SSH 배포 스크립트 작성.
  배포 후 헬스체크 (curl https://$DOMAIN/health).
</task>task>
<task>
  agent: doc-updater
  README.md + CHANGELOG.md + 릴리즈 노트 업데이트.
</task>task>

## STEP 7 — 완료 보고
════════════════════════════════════
✅ /team-run $ARGUMENTS 완료
UI+Frontend / Backend+DB / QA+Docker
빌드: PASS/FAIL | 테스트: PASS/FAIL | Docker: [상태]
다음: /handoff-verify → /commit-push-pr
════════════════════════════════════
</task>
</task>
