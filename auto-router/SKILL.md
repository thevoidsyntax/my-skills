---
name: auto-router
description: |
  Auto-invoke relevant skills based on conversation context and project type.
  Automatically activates appropriate skills when related topics are mentioned.
---

# Auto-Skill Router v2.0

This skill helps with auto-invocation of relevant skills based on detected context.

---

## 🔄 INVOCATION WORKFLOW

### When using /project-init:

```
1. User invokes /project-init
2. Answer Q&A about project requirements
3. System AUTO-INVOKES core skills:
   /git, /docker, /ci-cd, /code-quality, /deployment, /logging, /config
4. System shows OPTIONAL skills list with numbered options
5. User selects which optional skills to activate
6. System INVOKES selected optional skills
```

### When using /analyze-project:

```
1. User invokes /analyze-project
2. System scans project files
3. System AUTO-INVOKES core skills (always)
4. System AUTO-INVOKES context-specific skills (based on detected tech stack)
5. System shows remaining OPTIONAL skills for user selection
6. User selects which optional skills to activate
7. System INVOKES selected optional skills
```

---

## 📋 CORE SKILLS (Always Auto-Invoke)

These skills are invoked automatically in EVERY project:

```
CORE SKILLS (7):
/git              → Version control workflows
/docker           → Containerization
/ci-cd           → Pipeline automation
/code quality     → Code review & standards
/deployment       → Deployment strategies
/logging          → Structured logging
/config           → Configuration management
```

---

## 🔍 CONTEXT → SKILLS MAPPING

### Backend Frameworks

| Detected | Auto-Invoke | Optional |
|----------|-------------|----------|
| Express.js | /api-design, /security | /api-client, /messaging |
| NestJS | /api-design, /security, /messaging | /code-quality |
| Fastify | /api-design, /security | /api-client |
| Django | /api-design, /security | /data-engineering, /compliance |
| FastAPI | /api-design, /security | /data-engineering |
| Spring Boot | /api-design, /security | /scalability |
| Rails | /api-design, /security | /data-engineering |
| Go | /api-design, /performance | /code-quality |

### Databases

| Detected | Auto-Invoke | Optional |
|----------|-------------|----------|
| PostgreSQL | /database | /data-engineering, /scalability |
| MySQL | /database | /data-engineering |
| MongoDB | /data-engineering | /scalability |
| Redis | /scalability | /messaging |
| Elasticsearch | /search | /data-engineering |

### Frontend

| Detected | Auto-Invoke | Optional |
|----------|-------------|----------|
| React | /frontend, /performance | /testing |
| Vue.js | /frontend | /performance, /testing |
| Next.js | /frontend, /performance | /api-design, /testing |
| Angular | /frontend | /performance, /testing |
| Svelte | /frontend | /performance |

### Infrastructure

| Detected | Auto-Invoke | Optional |
|----------|-------------|----------|
| Docker | /docker (already core) | /kubernetes |
| Kubernetes | /kubernetes, /reliability | /observability |
| Terraform | /terraform | /ansible |
| GitHub Actions | /ci-cd (already core) | - |
| Serverless | /serverless | /scalability |

---

## 🎯 OPTIONAL SKILLS BY CATEGORY

### API & Backend
```
[ ] /api-client        HTTP client patterns
[ ] /graphql           GraphQL schema & resolvers
[ ] /message-queue     Kafka, RabbitMQ, SQS
```

### Data & Database
```
[ ] /database         SQL optimization
[ ] /data-engineering ETL, Data warehouse
[ ] /search           Elasticsearch, search
```

### Frontend & Mobile
```
[ ] /mobile            React Native, Flutter
[ ] /performance       Core Web Vitals
[ ] /testing          E2E, mutation testing
```

### Security & Compliance
```
[ ] /security          Auth, encryption
[ ] /identity          OAuth, SSO, MFA
[ ] /compliance        GDPR, HIPAA, SOC2
[ ] /reliability       SLO/SLA
```

### Infrastructure
```
[ ] /kubernetes        K8s orchestration
[ ] /terraform         Infrastructure as Code
[ ] /ansible           Configuration mgmt
[ ] /serverless        Lambda, Cloud Functions
[ ] /scalability       Auto-scaling
```

### Observability
```
[ ] /observability     Metrics, logs, traces
[ ] /sre-operations    DORA metrics
```

### ML & AI
```
[ ] /ml-engineering    ML lifecycle
[ ] /ai-integration    LLM integration
```

### Team & Process
```
[ ] /team-processes    Code ownership
[ ] /documentation     README, RFC
[ ] /developer-experience IDP, SDK design
```

### Domain-Specific
```
[ ] /gaming           Game server patterns
[ ] /iot-edge         IoT patterns
```

---

## 🔧 USER SELECTION FORMAT

When prompting for optional skills:

```
┌─────────────────────────────────────────────────────┐
│  🎯 SELECT OPTIONAL SKILLS                            │
│                                                     │
│  Ketik nomor yang ingin diaktifkan:                 │
│  Contoh: 1, 3, 5, 8                               │
│                                                     │
│  Atau gunakan shortcut:                              │
│  • "all"     → Aktifkan semua                     │
│  • "none"    → Skip optional skills                │
│  • "minimal" → Hanya yang critical                │
│  • "recommend" → Auto-recommend based on stack   │
└─────────────────────────────────────────────────────┘
```

---

## 📝 EXAMPLE FLOWS

### Flow 1: New Project (project-init)

```
User: /project-init

System: "Apa tipe system?"
User: [2] Full-Stack Web

System: "Scale?"
User: [2] Small-Medium

System: "Auto-invoking core skills..."
Invoke: /git, /docker, /ci-cd, /code-quality, /deployment, /logging, /config

System: "Pilihan opsional (berdasarkan Full-Stack Web):"
[ ] /frontend
[ ] /api-design
[ ] /security
[ ] /performance
[ ] /testing

User: 1, 3, 5

System: "Invoke selected..."
Invoke: /frontend, /security, /testing

System: "Setup complete!"
```

### Flow 2: Existing Project (analyze-project)

```
User: /analyze-project

System: "Scanning project files..."
Detected: Next.js, PostgreSQL, Redis, Docker, GitHub Actions

System: "Auto-invoking core skills..."
Invoke: /git, /docker, /ci-cd, /code-quality, /deployment, /logging, /config

System: "Detected context skills..."
Invoke: /frontend (Next.js)
Invoke: /api-design (likely backend)
Invoke: /database (PostgreSQL)
Invoke: /scalability (Redis)

System: "Pilihan opsional:"
[ ] /security
[ ] /performance
[ ] /observability
[ ] /graphql

User: 2, 3

System: "Invoke selected..."
Invoke: /performance, /observability

System: "Analysis complete!"
```

---

## 💡 KEY PRINCIPLES

1. **Core = Always** - 7 core skills always invoked
2. **Context = Auto** - Based on detected tech stack
3. **Optional = User Choice** - User picks what they need
4. **Transparency** - Always show what's being invoked and why

---

**This skill is referenced by /project-init and /analyze-project**
