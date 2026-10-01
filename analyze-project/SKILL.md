---
name: analyze-project
description: "Tech stack detection for existing projects. Analyzes project files to identify technology stack and auto-invoke required skills. Use when user wants to understand or start working on an existing project."
version: "2.0"
---

# ANALYZE PROJECT SKILL v2.0
# Tech Stack Detection for Existing Projects

Kamu adalah Project Analyzer yang teliti. Gunakan skill ini untuk menganalisis project yang sudah ada.

---

## 🎯 TUJUAN

Mendeteksi tech stack project berdasarkan file-file yang ada:
1. Baca configuration files
2. Identifikasi dependencies
3. Auto-invoke CORE skills yang wajib
4. Berikan pilihan OPSIONAL skills
5. Generate project-specific CLAUDE.md

---

## 📋 ANALYZER WORKFLOW

### STEP 1: SCAN PROJECT FILES

Scan file-file berikut secara berurutan:

```
Priority 1 (Wajib):
├── package.json           → Node.js/npm ecosystem
├── requirements.txt      → Python ecosystem
├── pyproject.toml        → Python modern
├── go.mod                → Go ecosystem
├── pom.xml / build.gradle → Java ecosystem
├── Cargo.toml            → Rust ecosystem
├── composer.json         → PHP ecosystem
└── *.csproj / *.sln      → C#/.NET ecosystem

Priority 2 (Configuration):
├── docker-compose.yml    → Container services
├── Dockerfile            → Containerization
├── terraform/            → IaC
├── kubernetes/ / k8s/   → K8s deployment
├── .github/workflows/   → GitHub Actions
├── .gitlab-ci.yml        → GitLab CI
└── prisma/schema.prisma  → Prisma ORM

Priority 3 (Frontend):
├── package.json          → Check react, vue, angular, svelte, next, nuxt
├── vite.config.ts        → Vite
├── webpack.config.js     → Webpack
└── tsconfig.json         → TypeScript

Priority 4 (Database):
├── prisma/schema.prisma  → PostgreSQL (via Prisma)
├── *.sql                 → Raw SQL migrations
├── config/database.yml   → Rails DB config
└── settings.py           → Django DB config
```

---

### STEP 2: EXTRACT DEPENDENCIES

Parsing dan ekstrak dependencies:

**Node.js (package.json):**
```json
{
  "dependencies": {
    "express": "4.18.0",      → Express.js
    "fastify": "4.0.0",       → Fastify
    "@nestjs/core": "10.0.0", → NestJS
    "next": "14.0.0",         → Next.js
    "react": "18.2.0",         → React
    "vue": "3.3.0",           → Vue.js
    "@prisma/client": "5.0.0" → PostgreSQL (Prisma)
    "mongoose": "8.0.0",      → MongoDB
    "ioredis": "5.0.0",       → Redis
    "typeorm": "0.3.0"        → TypeORM
  }
}
```

---

### STEP 3: GENERATE DETECTION REPORT

```
┌─────────────────────────────────────────────────────┐
│  📊 PROJECT ANALYSIS REPORT v2.0                    │
│                                                     │
│  DETECTED TECH STACK:                              │
│  • Backend: [Framework] ([Language])              │
│  • Database: [DB Engine]                           │
│  • Cache: [Cache Engine] (if detected)            │
│  • Frontend: [Framework] (if detected)           │
│  • DevOps: [Tools detected]                       │
│  • ML/AI: [Tools detected] (if any)              │
│                                                     │
│  PROJECT SCALE (estimated):                        │
│  • [Based on complexity, dependencies, etc]         │
│                                                     │
│  ─────────────────────────────────────────────────  │
│                                                     │
│  ⏱️ Processing skills recommendations...           │
└─────────────────────────────────────────────────────┘
```

---

### STEP 4: AUTO-INVOKE CORE SKILLS

Berdasarkan detection, invoke CORE skills yang diperlukan:

```
┌─────────────────────────────────────────────────────┐
│  🚀 AUTO-ACTIVATING CORE SKILLS                     │
│                                                     │
│  Invoke: /git                                       │
│  Invoke: /docker                                   │
│  Invoke: /ci-cd                                   │
│  Invoke: /code-quality                             │
│  Invoke: /deployment                               │
│  Invoke: /logging                                 │
│  Invoke: /config                                  │
│                                                     │
│  ✓ Core skills ACTIVE                            │
└─────────────────────────────────────────────────────┘
```

**CORE SKILLS (Always Auto-Invoke):**
```
/git              → Version control (ALWAYS)
/docker           → Containerization (if Dockerfile/docker-compose detected)
/ci-cd           → Pipeline automation (if .github/workflows detected)
/code-quality     → Code review & standards (ALWAYS)
/deployment       → Deployment strategies (ALWAYS)
/logging          → Structured logging (ALWAYS)
/config           → Configuration management (ALWAYS)
```

---

### STEP 5: INVOKE DETECTED SKILLS (Otomatis)

Berdasarkan tech stack yang terdeteksi:

```
┌─────────────────────────────────────────────────────┐
│  🔍 DETECTED → AUTO-INVOKING                      │
│                                                     │
│  Tech Stack Detected          → Skills Invoked    │
│  ────────────────────────────────────────────────  │
│  Node.js + Express           → /api-design, /security │
│  Node.js + NestJS            → /api-design, /security, /messaging │
│  Node.js + Next.js           → /frontend, /api-design, /performance │
│  Python + FastAPI            → /api-design, /security │
│  Python + Django             → /api-design, /security, /data-engineering │
│  Python + ML Stack           → /ml-engineering, /data-engineering │
│  Java + Spring Boot          → /api-design, /security, /scalability │
│  Go                          → /api-design, /performance │
│                                                     │
│  PostgreSQL detected         → /data-engineering, /database │
│  MongoDB detected            → /data-engineering │
│  Redis detected              → /scalability, /messaging │
│  Docker detected             → /docker (already invoked) │
│  Kubernetes detected          → /kubernetes, /reliability │
│                                                     │
│  ✓ Context skills ACTIVE                          │
└─────────────────────────────────────────────────────┘
```

---

### STEP 6: OPSIONAL SKILLS (User Pilih)

```
┌─────────────────────────────────────────────────────┐
│  🎯 OPSIONAL SKILLS (PILIH YANG DIBUTUHKAN)       │
│                                                     │
│  Tech Stack: [DETECTED]                           │
│  Scale: [ESTIMATED]                               │
│                                                     │
│  ─────────────────────────────────────────────────  │
│                                                     │
│  SKILLS BERDASARKAN TECH STACK:                   │
│                                                     │
│  API & Backend:                                    │
│  [ ] /api-client        → HTTP client patterns     │
│  [ ] /graphql            → GraphQL schema           │
│  [ ] /message-queue     → Event-driven patterns    │
│                                                     │
│  Data & Database:                                   │
│  [ ] /database          → SQL optimization          │
│  [ ] /data-engineering  → ETL, Warehouse          │
│  [ ] /search            → Elasticsearch            │
│                                                     │
│  Frontend & UX:                                     │
│  [ ] /frontend          → React/Vue/Angular        │
│  [ ] /mobile           → React Native/Flutter     │
│  [ ] /performance       → Core Web Vitals          │
│                                                     │
│  Security & Compliance:                              │
│  [ ] /security         → Auth, Encryption         │
│  [ ] /identity         → OAuth, SSO, MFA          │
│  [ ] /compliance       → GDPR, HIPAA, SOC2       │
│  [ ] /reliability      → SLO/SLA, Incident        │
│                                                     │
│  Infrastructure:                                    │
│  [ ] /kubernetes       → K8s orchestration        │
│  [ ] /terraform        → Infrastructure as Code   │
│  [ ] /ansible          → Configuration mgmt        │
│  [ ] /serverless       → Lambda, Cloud Functions  │
│                                                     │
│  Observability:                                     │
│  [ ] /observability    → Metrics, Logs, Traces   │
│  [ ] /sre-operations  → DORA metrics             │
│                                                     │
│  ML & AI:                                          │
│  [ ] /ml-engineering   → ML lifecycle            │
│  [ ] /ai-integration  → LLM integration         │
│                                                     │
│  Team & Process:                                   │
│  [ ] /team-processes  → Code ownership          │
│  [ ] /documentation   → README, RFC              │
│  [ ] /developer-experience → IDP, SDK design       │
│                                                     │
│  Domain-Specific:                                   │
│  [ ] /gaming          → Game server patterns      │
│  [ ] /iot-edge        → IoT patterns              │
│  [ ] /scalability     → Auto-scaling, CDN        │
│                                                     │
│  ─────────────────────────────────────────────────  │
│                                                     │
│  INPUT:                                            │
│  Ketik nomor yang ingin diaktifkan:                │
│  Contoh: 1, 3, 5, 8                               │
│  Atau ketik "all" untuk semua                      │
│  Atau ketik "none" untuk skip                     │
│  Atau ketik "recommend" untuk auto-recommend     │
└─────────────────────────────────────────────────────┘
```

---

### STEP 7: INVOKE OPSIONAL SKILLS (Yang Dipilih)

```
┌─────────────────────────────────────────────────────┐
│  ✓ INVOKING SELECTED OPSIONAL SKILLS               │
│                                                     │
│  Invoke: /[skill-1]                               │
│  Invoke: /[skill-2]                               │
│  Invoke: /[skill-3]                               │
│                                                     │
│  ✓ All selected skills ACTIVE                     │
└─────────────────────────────────────────────────────┘
```

---

### STEP 8: GENERATE PROJECT CLAUDE.MD

```
┌─────────────────────────────────────────────────────┐
│  📝 GENERATING PROJECT-SPECIFIC CLAUDE.MD           │
│                                                     │
│  Analyzing project structure...                     │
│  Generating CLAUDE.md dengan:                       │
│  • Tech stack detected                             │
│  • Skills yang aktif                              │
│  • Project-specific rules                          │
│  • Best practices                                  │
│                                                     │
│  ✓ CLAUDE.md Generated                            │
└─────────────────────────────────────────────────────┘
```

---

## 🔍 FILE DETECTION RULES

### BACKEND

| File | Language/Framework |
|------|-------------------|
| `package.json` | Node.js |
| `requirements.txt`, `pyproject.toml` | Python |
| `go.mod` | Go |
| `pom.xml`, `build.gradle` | Java |
| `*.csproj` | C# / .NET |
| `Cargo.toml` | Rust |
| `composer.json` | PHP |

### FRAMEWORK

| Indicator | Framework |
|----------|-----------|
| `express` in deps | Express.js |
| `fastify` in deps | Fastify |
| `@nestjs/core` in deps | NestJS |
| `next` in deps | Next.js |
| `django` in deps | Django |
| `fastapi` in deps | FastAPI |
| `flask` in deps | Flask |
| `spring-boot` in deps | Spring Boot |

### DATABASE

| Indicator | Database |
|----------|----------|
| `pg`, `postgres` | PostgreSQL |
| `mysql` | MySQL |
| `mongodb` | MongoDB |
| `redis` | Redis |
| `sqlite` | SQLite |
| `dynamodb` | DynamoDB |

### DEVOPS

| File | Tool |
|------|------|
| `Dockerfile` | Docker |
| `docker-compose.yml` | Docker Compose |
| `kubernetes/` | Kubernetes |
| `.github/workflows/` | GitHub Actions |
| `.gitlab-ci.yml` | GitLab CI |
| `terraform/` | Terraform |

---

## 📊 SKILL MAPPING TABLE

| Detection | Core Auto-Invoke | Optional Recommend |
|----------|-----------------|------------------|
| Node.js + Express | /git, /docker, /ci-cd, /code-quality, /deployment | /api-design, /security, /api-client |
| Node.js + NestJS | /git, /docker, /ci-cd, /code-quality, /deployment | /api-design, /security, /messaging |
| Node.js + Next.js | /git, /docker, /ci-cd, /code-quality, /deployment | /frontend, /api-design, /performance |
| Python + FastAPI | /git, /docker, /ci-cd, /code-quality, /deployment | /api-design, /security, /database |
| Python + Django | /git, /docker, /ci-cd, /code-quality, /deployment | /api-design, /security, /data-engineering |
| Python + ML Stack | /git, /docker, /ci-cd, /code-quality, /deployment | /ml-engineering, /data-engineering |
| Java + Spring | /git, /docker, /ci-cd, /code-quality, /deployment | /api-design, /security, /scalability |
| Go | /git, /docker, /ci-cd, /code-quality, /deployment | /api-design, /performance |
| PostgreSQL | (auto-invoked via above) | /database, /data-engineering |
| Redis | (auto-invoked via above) | /scalability, /messaging |
| Kubernetes | /kubernetes (added to core) | /reliability, /observability |
| React/Vue/Angular | (auto-invoked via above) | /frontend, /performance |

---

## 🎯 BEST PRACTICES

1. **Auto-invoke what detected** - Jangan minta user invoke manual untuk yang jelas
2. **Offer optional** - Skills yang belum jelas, tawarkan pilihan
3. **Explain detection** - Tunjukkan ke user apa yang terdeteksi
4. **Let user decide** - User punya hak pilih final

---

## 📝 FINAL OUTPUT EXAMPLE

```
┌─────────────────────────────────────────────────────┐
│  ✅ PROJECT ANALYSIS COMPLETE                        │
│                                                     │
│  DETECTED:                                         │
│  • Backend: Next.js 14 + Express (Node.js)         │
│  • Database: PostgreSQL (Prisma)                    │
│  • Cache: Redis                                    │
│  • DevOps: Docker, GitHub Actions                  │
│                                                     │
│  CORE SKILLS (AUTO-ACTIVATED):                   │
│  ✅ /git                                           │
│  ✅ /docker                                        │
│  ✅ /ci-cd                                         │
│  ✅ /code-quality                                   │
│  ✅ /deployment                                     │
│  ✅ /logging                                        │
│  ✅ /config                                        │
│                                                     │
│  CONTEXT SKILLS (DETECTED → AUTO):               │
│  ✅ /frontend (Next.js detected)                  │
│  ✅ /api-design (Express detected)                 │
│  ✅ /database (PostgreSQL detected)                │
│                                                     │
│  OPSIONAL SKILLS (SELECTED BY USER):              │
│  ✅ /security                                       │
│  ✅ /performance                                   │
│  ✅ /observability                                  │
│                                                     │
│  ─────────────────────────────────────────────────  │
│                                                     │
│  NEXT STEPS:                                       │
│  1. Review generated CLAUDE.md                     │
│  2. Start development dengan /implement            │
│  3. Untuk bug: /diagnosing-bugs                   │
│  4. Untuk review: /code-review                    │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

**Invoke:** `/analyze-project` | **Priority:** HIGH | **Version:** 2.0
