# KEDA Research Project

KEDA(Kubernetes Event-Driven Autoscaling) 리서치 및 Minikube 테스트, 발표 자료 제작 프로젝트.

## Project Structure

- `keda-presentation-plan.md` — 발표 계획서 (48개 소스 포함)
- `required-skills.md` — 필수/권장 Skills & MCP 서버 분석

## Available Skills

이 프로젝트에서 활용할 Skills:

| Skill | 용도 |
|-------|------|
| `kubernetes-specialist` | K8s 배포, Helm 차트, KEDA 설치/설정, RBAC, 트러블슈팅 |
| `mermaid-diagrams` | 아키텍처/시퀀스/플로우 다이어그램 생성 |
| `nlm-skill` | NotebookLM 기반 리서치 질의 및 콘텐츠 생성 |
| `find-skills` | 추가 스킬 탐색 및 설치 |

## Available MCP Servers

| Server | 용도 | 도구 |
|--------|------|------|
| Context7 | 최신 공식 문서 실시간 조회 (KEDA, K8s, Helm) | `resolve-library-id`, `query-docs` |
| NotebookLM | 기존 KEDA 리서치 노트북 질의 | `ask_question`, `select_notebook` |
| Scholar Gateway | 학술 논문 검색 (claude.ai connector) | `semanticSearch` |
| Playwright | 웹 UI 자동화 및 스크린샷 | `browser_navigate`, `browser_take_screenshot` |
| Chrome DevTools | 브라우저 디버깅 및 성능 분석 | `take_screenshot`, `navigate_page` |
| Pinecone | 벡터 검색 (선택적) | `search-records`, `upsert-records` |

## NotebookLM Reference

- 기존 KEDA 리서치 노트북: `70fc7310-02e6-422d-9cea-cc8afbc2bdcb`
- 소스 48개 포함 (KEDA 공식 문서, 블로그, 사례 연구 등)

## CLI Prerequisites

minikube 테스트 전 필요한 도구:
```bash
minikube version && kubectl version --client && helm version && docker version
```
