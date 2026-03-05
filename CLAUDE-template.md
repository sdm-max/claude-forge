# CLAUDE.md — 팀 에이전트 설정 (sdm-max)
# 이 파일을 프로젝트 루트에 CLAUDE.md 로 복사해서 사용하세요

## 팀 구성 (Lead 1 + Teammate 3 = 최대 4명)
| 역할 | 에이전트 | 파일 소유권 |
|------|---------|------------|
| Lead | pm-orchestrator | 조율만 (구현 금지) |
| UI+Frontend | e2e-runner | src/components/ src/pages/ src/styles/ src/hooks/ public/ |
| Backend+DB | build-error-resolver | src/api/ src/db/ src/types/ src/middleware/ src/lib/ |
| QA+Docker | verify-agent | tests/ e2e/ Dockerfile docker-compose.yml deploy/ .github/ |

## 파일 소유권 규칙 (CRITICAL)
- 같은 파일을 2명이 편집하면 덮어쓰기 발생 → 반드시 분리
- - src/types/ 는 Backend+DB 독점 (공유 타입 충돌 방지)
  - - 팀원 프롬프트에 수정 금지 파일 명시 필수
   
    - ## 커맨드
    - /team-run [기능]   전체 파이프라인 (기획→UI→개발→보안→테스트→Docker배포)
    - /orchestrate       팀 자동 구성
    - /auto [기능]       plan→code→verify→PR 전체 자동
    - /plan [기능]       기획만 (planner Opus)
    - /tdd [기능]        TDD 방식 개발
    - /security-review   OWASP 보안 감사
    - /handoff-verify    빌드/타입/테스트 검증
    - /commit-push-pr    커밋+푸시+PR 생성
    - /sync              세션 동기화 (세션 시작/끝마다 실행)
   
    - ## 기술 스택
    - <!-- 실제 프로젝트에 맞게 수정하세요 -->
    - - Frontend: Next.js 14 (App Router), TypeScript, Tailwind CSS
      - - Backend: Node.js, Fastify, PostgreSQL
        - - ORM: Drizzle
          - - Auth: JWT + OAuth2
            - - Test: Jest, Playwright
              - - Deploy: Docker, GitHub Actions
               
                - ## 서버 배포 정보
                - <!-- 실제 값으로 교체하세요 -->
                - DEPLOY_HOST=your-server-ip
                - DEPLOY_USER=ubuntu
                - SSH_KEY=~/.ssh/deploy_key
                - DOMAIN=yourdomain.com
                - APP_PORT=3000
                - DOCKER_REGISTRY=ghcr.io/sdm-max
               
                - ## 코딩 규칙
                - - 함수 단일 책임 원칙
                  - - 모든 함수 JSDoc 작성
                    - - 에러 반드시 핸들링
                      - - 시크릿은 환경변수로만 관리
                        - - SQL은 파라미터화 쿼리만 사용
