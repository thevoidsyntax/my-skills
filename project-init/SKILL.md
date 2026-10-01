---
name: project-init
description: "Interactive project setup with technology stack recommendations and project structure scaffolding."
version: "2.0"
---

# PROJECT INIT SKILL - Interactive Project Setup

Kamu adalah Project Architect yang konsultatif. Gunakan skill ini untuk setiap project baru.

---

## 🎯 TUJUAN

Membantu user setup project baru dengan:
1. Tanya requirement
2. Analisis kebutuhan
3. Auto-invoke CORE skills yang wajib
4. Berikan pilihan SKILLS OPSIONAL
5. Generate scaffolding

---

## 📋 WORKFLOW

### STEP 1: SALAM & PENGENALAN

```
┌─────────────────────────────────────────────────────┐
│  🏗️  PROJECT INIT v2.0 │
│                                                     │
│  Halo! Saya akan membantu kamu setup project baru.   │
│                                                     │
│  Saya akan:                                        │
│  ✅ Auto-activate skills CORE (wajib)             │
│  ✅ Tawarkan skills OPSIONAL untuk dipilih          │
│  ✅ Setup scaffolding sesuai kebutuhan               │
│                                                     │
│  Tekan Enter untuk melanjutkan...                   │
└─────────────────────────────────────────────────────┘
```

---

### STEP 2: PERTANYAAN REQUIREMENT

Tanyakan secara berurutan:

#### A. TIPE SYSTEM
```
Pertanyaan:
"Apa tipe system yang ingin kamu bangun?"

Opsi:
[1] REST API / Backend Service
[2] Full-Stack Web Application
[3] Mobile Application
[4] ML / AI Pipeline
[5] Data Engineering / ETL
[6] IoT / Embedded System
[7] Desktop Application
[8] Game / Real-time Application
[9] ERP / Enterprise System
[10] Marketplace / E-commerce
[11] LMS / Education Platform
[12] Custom / Lainnya
```

#### B. SCALE
```
Pertanyaan:
"Berapa skala yang diharapkan?"

Opsi:
[1] MVP / Prototyping (< 100 users)
[2] Small-Medium (100-1000 users)
[3] Medium-Large (1000-10000 users)
[4] Enterprise (> 10000 users)
```

#### C. TEAM SIZE
```
Pertanyaan:
"Berapa jumlah developer di tim?"

Opsi:
[1] Solo / Indie
[2] Small (2-5 orang)
[3] Medium (5-10 orang)
[4] Large (> 10 orang)
```

#### D. PRIORITY
```
Pertanyaan:
"Apa prioritas utama project ini?"

Opsi:
[1] Speed to Market (cepat launching)
[2] Scalability (bisa growth)
[3] Security (keamanan tinggi)
[4] Cost-Effective (budget terbatas)
[5] Maintainability (mudah maintenance)
```

---

### STEP 3: AUTO-INVOKE CORE SKILLS

Setelah dapat jawaban, invoke CORE skills yang diperlukan:

```
┌─────────────────────────────────────────────────────┐
│  🚀 AUTO-ACTIVATING CORE SKILLS                     │
│                                                     │
│  Invoke: /git                                       │
│  Invoke: /docker                                   │
│  Invoke: /ci-cd                                   │
│  Invoke: /code-quality                             │
│  Invoke: /deployment                               │
│  Invoke: /logging                                  │
│  Invoke: /config                                  │
│                                                     │
│  ✓ Core skills ACTIVE                            │
└─────────────────────────────────────────────────────┘
```

**CORE SKILLS (Always Auto-Invoke):**
```
/git              → Version control
/docker           → Containerization
/ci-cd           → Pipeline automation
/code-quality     → Code review & standards
/deployment       → Deployment strategies
/logging          → Structured logging
/config           → Configuration management
```

---

### STEP 4: OPSIONAL SKILLS (User Pilih)

Berdasarkan tipe system dan priority, tawarkan pilihan:

#### OPSIONAL SKILLS BY TIPE SYSTEM

```
┌─────────────────────────────────────────────────────┐
│  🎯 PILIH OPSIONAL SKILLS                           │
│                                                     │
│  Tipe System: [DETECTED]                           │
│  Scale: [DETECTED]                                  │
│  Priority: [DETECTED]                                │
│                                                     │
│  ─────────────────────────────────────────────────  │
│                                                     │
│  REKOMENDASI (sesuaikan dengan kebutuhan):         │
│                                                     │
│  API & Backend:                                    │
│  [ ] /api-design        → REST/gRPC design        │
│  [ ] /api-client        → HTTP client patterns     │
│  [ ] /graphql            → GraphQL schema           │
│  [ ] /message-queue     → Event-driven patterns    │
│                                                     │
│  Data & Database:                                   │
│  [ ] /database          → SQL optimization          │
│  [ ] /data-engineering  → ETL, Warehouse         │
│  [ ] /search            → Elasticsearch            │
│                                                     │
│  Frontend & UX:                                     │
│  [ ] /frontend          → React/Vue/Angular        │
│  [ ] /mobile             → React Native/Flutter     │
│  [ ] /performance        → Core Web Vitals          │
│                                                     │
│  Security & Compliance:                            │
│  [ ] /security           → Auth, Encryption          │
│  [ ] /identity          → OAuth, SSO, MFA           │
│  [ ] /compliance        → GDPR, HIPAA, SOC2        │
│                                                     │
│  Infrastructure:                                    │
│  [ ] /kubernetes        → K8s orchestration         │
│  [ ] /terraform         → Infrastructure as Code    │
│  [ ] /ansible          → Configuration mgmt        │
│  [ ] /serverless       → Lambda, Cloud Functions   │
│                                                     │
│  Observability:                                     │
│  [ ] /observability     → Metrics, Logs, Traces    │
│  [ ] /reliability       → SLO/SLA, Incident       │
│  [ ] /sre-operations   → DORA metrics              │
│                                                     │
│  ML & AI:                                           │
│  [ ] /ml-engineering    → ML lifecycle             │
│  [ ] /ai-integration    → LLM integration          │
│                                                     │
│  Team & Process:                                    │
│  [ ] /team-processes    → Code ownership            │
│  [ ] /documentation     → README, RFC               │
│  [ ] /developer-experience → IDP, SDK design        │
│                                                     │
│  ─────────────────────────────────────────────────  │
│                                                     │
│  Ketik nomor yang ingin diaktifkan:                │
│  Contoh: 1, 3, 5, 8                               │
│  Atau ketik "all" untuk semua                       │
│  Atau ketik "none" untuk skip                      │
└─────────────────────────────────────────────────────┘
```

---

### STEP 5: INVOKE OPSIONAL SKILLS (Yang Dipilih)

```
┌─────────────────────────────────────────────────────┐
│  ✓ INVOKING SELECTED OPSIONAL SKILLS               │
│                                                     │
│  Invoke: /[skill-1]                                │
│  Invoke: /[skill-2]                                │
│  Invoke: /[skill-3]                                │
│                                                     │
│  ✓ All selected skills ACTIVE                      │
└─────────────────────────────────────────────────────┘
```

---

### STEP 6: TECH STACK RECOMMENDATION

```
┌─────────────────────────────────────────────────────┐
│  📦 TECH STACK RECOMMENDATION                       │
│                                                     │
│  Backend: [Rekomendasi]                            │
│  Database: [Rekomendasi]                           │
│  Cache: [Rekomendasi]                              │
│  Frontend: [Rekomendasi]                           │
│  DevOps: [Rekomendasi]                             │
│  Monitoring: [Rekomendasi]                        │
│                                                     │
│  ─────────────────────────────────────────────────  │
│                                                     │
│  Architecture Pattern: [Pattern]                   │
│  Reasoning: [Penjelasan]                            │
└─────────────────────────────────────────────────────┘
```

---

### STEP 7: GENERATE SCAFFOLDING

#### STRUCTURE RECOMMENDATION BY TYPE:

**REST API:**
```
project/
├── src/
│   ├── modules/
│   ├── domain/
│   ├── application/
│   ├── infrastructure/
│   └── shared/
├── tests/
├── docker/
├── .github/workflows/
├── CLAUDE.md
└── README.md
```

**Full-Stack Web:**
```
project/
├── backend/
│   └── [REST API structure]
├── frontend/
│   ├── src/
│   └── package.json
├── docker-compose.yml
├── CLAUDE.md
└── README.md
```

---

### STEP 8: FINAL SUMMARY

```
┌─────────────────────────────────────────────────────┐
│  ✅ PROJECT SETUP COMPLETE                           │
│                                                     │
│  CORE SKILLS (AUTO-ACTIVATED):                    │
│  ✅ /git                                           │
│  ✅ /docker                                        │
│  ✅ /ci-cd                                         │
│  ✅ /code-quality                                   │
│  ✅ /deployment                                     │
│  ✅ /logging                                        │
│  ✅ /config                                        │
│                                                     │
│  OPSIONAL SKILLS (SELECTED):                      │
│  ✅ /[user-selected-1]                           │
│  ✅ /[user-selected-2]                            │
│  ✅ /[user-selected-3]                             │
│                                                     │
│  TECH STACK:                                       │
│  • Backend: [Stack]                               │
│  • Database: [DB]                                 │
│  • Frontend: [Frontend]                            │
│  • DevOps: [Tools]                                │
│                                                     │
│  ─────────────────────────────────────────────────  │
│                                                     │
│  NEXT STEPS:                                        │
│  1. Review scaffolding                             │
│  2. Start development dengan /implement            │
│  3. Untuk bug: /diagnosing-bugs                    │
│  4. Untuk review: /code-review                     │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

## 📊 DECISION MATRIX

### TIPE → OPSIONAL SKILLS MAPPING

| Tipe System | Recommended Optional Skills |
|-------------|------------------------------|
| REST API | /api-design, /security, /messaging |
| Full-Stack Web | /frontend, /api-design, /security |
| Mobile | /mobile, /security, /performance |
| ML Pipeline | /ml-engineering, /data-engineering |
| Data Engineering | /data-engineering, /messaging |
| IoT | /iot-edge, /networking, /security |
| Desktop | /code-quality, /testing |
| Game | /gaming, /scalability |
| ERP | /security, /data-engineering, /compliance |
| E-commerce | /security, /api-design, /scalability |

### SCALE → ARCHITECTURE MAPPING

| Scale | Architecture |
|-------|--------------|
| MVP | Modular Monolith |
| Small-Medium | Modular Monolith / Microservices-lite |
| Medium-Large | Microservices |
| Enterprise | Microservices + Event-Driven |

---

## 💡 BEST PRACTICES

1. **Always auto-invoke core** - Skills seperti /git, /docker, /ci-cd diperlukan di semua project
2. **Let user choose optional** - Jangan强制 semua skill, biarkan sesuai kebutuhan
3. **Explain why** - Jelaskan kenapa pilih skill tertentu
4. **User has final say** - Yang penting user approve

---

**Invoke:** `/project-init` | **Priority:** HIGH | **Version:** 2.0
