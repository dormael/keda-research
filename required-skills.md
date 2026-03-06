# KEDA 리서치 & Minikube 테스트를 위한 필수 Skills / MCP Servers

> 작성일: 2026-03-07
> 목적: `keda-presentation-plan.md` 기반 리서치 및 로컬 Kubernetes(minikube) 클러스터 테스트에 필요한 도구 정리

---

## 1. Skills (슬래시 커맨드로 호출 가능)

### 1.1 `kubernetes-specialist` — Kubernetes 배포 및 운영 전문가

| 항목 | 내용 |
|------|------|
| **경로** | `~/.claude/skills/kubernetes-specialist/SKILL.md` |
| **호출** | 자동 트리거 (Kubernetes, kubectl, Helm 등 키워드) |
| **용도** | KEDA 리서치에서 **가장 핵심적인 스킬** |

**활용 시나리오:**
- Minikube 클러스터 설정 및 관리
- KEDA Helm 차트 설치 (`helm install keda kedacore/keda`)
- ScaledObject / ScaledJob CRD 매니페스트 작성
- RabbitMQ, Kafka 등 메시지 브로커 Deployment 작성
- TriggerAuthentication 설정
- RBAC, NetworkPolicy 구성
- kubectl 트러블슈팅

**발표 계획 연관 섹션:** 3(아키텍처), 7(고급기능), 8(Kafka 스케일러), 10(RabbitMQ/SQS), 13(데모/실습)

---

### 1.2 `mermaid-diagrams` — 소프트웨어 다이어그램 생성

| 항목 | 내용 |
|------|------|
| **경로** | `~/.agents/skills/mermaid-diagrams/SKILL.md` |
| **호출** | 자동 트리거 (diagram, visualize, 아키텍처 등 키워드) |
| **용도** | 발표 자료용 시각화 |

**활용 시나리오:**
- KEDA 3-컴포넌트 아키텍처 다이어그램 (C4 Container Diagram)
- 스케일링 동작 흐름 시퀀스 다이어그램
- KEDA vs HPA 비교 플로우차트
- Kafka 컨슈머 랙 기반 스케일링 시퀀스 다이어그램
- CNCF 여정 타임라인 (Gantt Chart)
- ScaledObject 수명주기 상태 다이어그램

**발표 계획 연관 섹션:** 3(아키텍처), 4(KEDA vs HPA), 5(직접 통신), 8(Kafka), 슬라이드 구성 전반

---

### 1.3 `nlm-skill` — NotebookLM CLI & MCP 연동

| 항목 | 내용 |
|------|------|
| **경로** | `~/.claude/skills/nlm-skill/SKILL.md` |
| **호출** | 자동 트리거 (nlm, notebooklm, podcast 등 키워드) |
| **용도** | 기존 KEDA 리서치 노트북 활용 |

**활용 시나리오:**
- 기존 NotebookLM 노트북(`70fc7310-...`)에 질의하여 추가 리서치
- 발표 자료 초안 생성 (보고서, 퀴즈, 마인드맵 등)
- 48개 소스 기반 심화 질의 (예: "Alibaba Cloud가 KEDA를 선택한 기술적 이유 상세 설명")
- 팟캐스트/오디오 개요 생성

**발표 계획 연관 섹션:** 전체 (리서치 기반 자료)

---

### 1.4 `find-skills` — 추가 스킬 탐색

| 항목 | 내용 |
|------|------|
| **경로** | `~/.agents/skills/find-skills/SKILL.md` |
| **호출** | `/find-skills` 또는 "find a skill for..." |
| **용도** | 필요시 추가 전문 스킬 검색 및 설치 |

**활용 시나리오:**
- Helm 전문 스킬 탐색
- Kafka/RabbitMQ 전용 스킬 존재 여부 확인
- 프레젠테이션 생성 관련 스킬 탐색

---

## 2. MCP Servers (외부 도구 연동)

### 2.1 `Context7` — 라이브러리 문서 실시간 조회 ⭐ 핵심

| 항목 | 내용 |
|------|------|
| **서버** | `@upstash/context7-mcp` (plugin + claude.ai 양쪽 제공) |
| **주요 도구** | `resolve-library-id`, `query-docs` |
| **용도** | KEDA, Kubernetes, Helm 등 **최신 공식 문서를 실시간으로 조회** |

**활용 시나리오:**
- KEDA 공식 문서에서 ScaledObject spec 최신 버전 조회
- Helm 차트 설치 명령어 및 values.yaml 옵션 확인
- minikube 최신 설치 가이드 조회
- Strimzi Kafka Operator 설정 방법 검색
- RabbitMQ Kubernetes Operator 문서 확인

**사용 흐름:**
```
1. resolve-library-id("keda", "KEDA Kubernetes autoscaling") → library ID 획득
2. query-docs(libraryId, "ScaledObject configuration for Kafka") → 최신 문서 조회
```

---

### 2.2 `NotebookLM` — Google NotebookLM 직접 연동

| 항목 | 내용 |
|------|------|
| **서버** | NotebookLM MCP Server |
| **주요 도구** | `ask_question`, `add_notebook`, `list_notebooks`, `select_notebook` 등 |
| **용도** | 기존 KEDA 리서치 노트북(48개 소스)에 **직접 질의** |

**활용 시나리오:**
- 노트북에 추가 소스(URL) 등록하여 리서치 확장
- 특정 주제에 대한 심화 질의 (Gemini 2.5 기반 RAG)
- 세션 기반 대화형 리서치
- 노트북 관리 (목록 조회, 선택, 업데이트)

**기존 노트북 URL:** `https://notebooklm.google.com/notebook/70fc7310-02e6-422d-9cea-cc8afbc2bdcb`

---

### 2.3 `Playwright` — 브라우저 자동화

| 항목 | 내용 |
|------|------|
| **서버** | `@playwright/mcp@latest` |
| **주요 도구** | `browser_navigate`, `browser_snapshot`, `browser_take_screenshot`, `browser_click` 등 20+ |
| **용도** | 웹 기반 리서치 및 대시보드 테스트 |

**활용 시나리오:**
- KEDA 공식 사이트에서 최신 스케일러 목록 스크래핑
- Kubernetes Dashboard 접근 및 스크린샷
- KEDA 데모 환경의 웹 UI 상호작용 테스트
- Grafana/Prometheus 대시보드 스크린샷 캡처 (발표 자료용)

---

### 2.4 `Chrome DevTools` — 브라우저 개발자 도구

| 항목 | 내용 |
|------|------|
| **서버** | Chrome DevTools MCP Server |
| **주요 도구** | `take_snapshot`, `take_screenshot`, `navigate_page`, `evaluate_script`, `lighthouse_audit`, `performance_*` 등 |
| **용도** | 심층 웹 분석 및 성능 측정 |

**활용 시나리오:**
- KEDA 관련 웹 리소스 탐색
- Kubernetes Dashboard 성능 분석
- 네트워크 요청 모니터링

---

### 2.5 `Scholar Gateway` — 학술 논문 검색

| 항목 | 내용 |
|------|------|
| **서버** | Scholar Gateway (Semantic Search) |
| **주요 도구** | `semanticSearch` |
| **용도** | KEDA 관련 **학술 논문 및 연구 자료** 검색 |

**활용 시나리오:**
- "Kubernetes event-driven autoscaling performance evaluation" 학술 논문 검색
- KEDA 아키텍처 분석 관련 피어리뷰 논문 조회
- 클라우드 오토스케일링 벤치마크 연구 자료 수집
- 발표자료 `참고문헌` 섹션에 학술적 근거 보강

**사용 예시:**
```
semanticSearch(
  query: "What is the performance impact of event-driven autoscaling with KEDA in Kubernetes?",
  topN: 10,
  start_year: 2020
)
```

---

### 2.6 `Pinecone` — 벡터 데이터베이스 (선택)

| 항목 | 내용 |
|------|------|
| **서버** | `@pinecone-database/mcp` |
| **주요 도구** | `search-docs`, `search-records`, `upsert-records`, `create-index-for-model` 등 |
| **용도** | 리서치 자료의 시맨틱 검색 인덱스 구축 (선택적) |

**활용 시나리오 (선택):**
- 48개 소스 문서를 벡터화하여 시맨틱 검색 구축
- 발표 준비 중 특정 키워드/주제에 대한 빠른 관련 자료 검색
- KEDA 문서 RAG 파이프라인 구성

---

## 3. 내장 도구 (Built-in Tools)

### 3.1 `WebSearch` — 웹 검색

| 용도 | 최신 KEDA 릴리스, 블로그 포스트, 튜토리얼 검색 |
|------|------|
| **활용** | KEDA 2.19 최신 변경사항, 새로운 스케일러 추가 여부, 커뮤니티 블로그 탐색 |

### 3.2 `WebFetch` — 웹 페이지 콘텐츠 수집

| 용도 | 특정 URL의 콘텐츠를 가져와 분석 |
|------|------|
| **활용** | `keda-presentation-plan.md`에 나열된 48개 소스 URL에서 상세 내용 추출 |

### 3.3 `Bash` — 터미널 명령 실행

| 용도 | minikube, kubectl, helm 등 CLI 도구 직접 실행 |
|------|------|
| **활용** | KEDA 설치, ScaledObject 배포, 로그 확인, 클러스터 상태 모니터링 |

---

## 4. 작업 단계별 도구 매핑

### Phase 1: 리서치 심화
| 작업 | 도구 |
|------|------|
| KEDA 최신 문서 조회 | Context7 (`query-docs`) |
| 기존 노트북 기반 심화 질의 | NotebookLM (`ask_question`) |
| 학술 논문 검색 | Scholar Gateway (`semanticSearch`) |
| 최신 블로그/릴리스 검색 | WebSearch |
| 특정 소스 URL 상세 조회 | WebFetch |

### Phase 2: Minikube 환경 구축 및 KEDA 테스트
| 작업 | 도구 |
|------|------|
| Minikube 클러스터 시작 | Bash (`minikube start`) |
| KEDA Helm 설치 | Bash + kubernetes-specialist |
| 메시지 브로커 배포 (RabbitMQ/Kafka) | kubernetes-specialist |
| ScaledObject 매니페스트 작성 | kubernetes-specialist |
| 스케일링 동작 검증 | Bash (`kubectl get pods -w`) |
| 최신 설정 옵션 확인 | Context7 |

### Phase 3: 발표 자료 제작
| 작업 | 도구 |
|------|------|
| 아키텍처 다이어그램 | mermaid-diagrams |
| 시퀀스/플로우 다이어그램 | mermaid-diagrams |
| 대시보드 스크린샷 | Playwright / Chrome DevTools |
| 데모 시나리오 정리 | kubernetes-specialist |

---

## 5. 사전 설치 확인 필요 항목

minikube에서 KEDA 테스트 전에 로컬 환경에서 확인해야 할 CLI 도구:

```bash
# 필수 CLI 도구 확인
minikube version          # Minikube 설치 여부
kubectl version --client  # kubectl 설치 여부
helm version              # Helm 설치 여부
docker version            # Docker (minikube 드라이버)

# KEDA Helm 리포지토리 추가
helm repo add kedacore https://kedacore.github.io/charts
helm repo update

# KEDA 설치
helm install keda kedacore/keda --namespace keda --create-namespace

# 테스트용 메시지 브로커 (예: RabbitMQ)
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install rabbitmq bitnami/rabbitmq --namespace demo --create-namespace
```

---

## 6. 요약: 우선순위별 도구 분류

### 필수 (Must-have)
| 도구 | 유형 | 목적 |
|------|------|------|
| **kubernetes-specialist** | Skill | K8s 배포, Helm, KEDA 설치/설정 |
| **Context7** | MCP Server | 최신 공식 문서 실시간 조회 |
| **Bash** | Built-in | CLI 명령 실행 (minikube, kubectl, helm) |
| **WebSearch** | Built-in | 최신 정보 검색 |

### 권장 (Should-have)
| 도구 | 유형 | 목적 |
|------|------|------|
| **mermaid-diagrams** | Skill | 아키텍처/플로우 다이어그램 생성 |
| **NotebookLM** | MCP Server | 기존 리서치 노트북 활용 |
| **Scholar Gateway** | MCP Server | 학술 논문 검색 |
| **WebFetch** | Built-in | 특정 URL 콘텐츠 수집 |

### 선택 (Nice-to-have)
| 도구 | 유형 | 목적 |
|------|------|------|
| **Playwright** | MCP Server | 웹 UI 자동화/스크린샷 |
| **Chrome DevTools** | MCP Server | 브라우저 디버깅/성능 |
| **Pinecone** | MCP Server | 벡터 검색 인덱스 구축 |
| **find-skills** | Skill | 추가 스킬 탐색 |
