---
name: architecture-patterns
description: "Enterprise architecture patterns including Hexagonal Architecture, Micro-frontend, and Modular Monolith. Use for system design decisions."
version: "1.0"
---

# ARCHITECTURE PATTERNS MODULE

Kamu adalah Software Architect. Gunakan rules ini untuk setiap aspek architecture patterns.

---

## 1. HEXAGONAL ARCHITECTURE
- **Ports & Adapters:**
  - Core business logic isolated
  - Driving ports (input)
  - Driven ports (output)
- **Layers:**
  - Domain (pure business logic)
  - Application (use cases)
  - Infrastructure (adapters)
- **Benefits:**
  - Testability
  - Flexibility
  - Framework independence
- **Implementation:**
  - Interfaces for ports
  - Dependency injection
  - No framework in domain

## 2. LAYERED ARCHITECTURE
- **Classic Layers:**
  - Presentation
  - Application
  - Domain
  - Infrastructure
- **Dependencies:**
  - Direction inward only
  - Domain is center
  - No infrastructure in domain
- **Use Cases:**
  - Enterprise applications
  - Complex business logic
  - Team-based development
- **Best Practices:**
  - Clear boundaries
  - Dependency rules
  - Module organization

## 3. MICROSERVICES ARCHITECTURE
- **Service Design:**
  - Single responsibility
  - Independent deployment
  - Own database
  - API contracts
- **Communication:**
  - Synchronous (REST, gRPC)
  - Asynchronous (events)
  - Saga patterns
- **Data Management:**
  - Database per service
  - Event sourcing
  - CQRS
- **Operational:**
  - Service mesh
  - Observability
  - CI/CD per service

## 4. MICRO-FRONTEND ARCHITECTURE
- **Approaches:**
  - Build-time: Module federation
  - Run-time: Iframes, Web Components
  - Shell: Container app
- **Benefits:**
  - Independent deployment
  - Team autonomy
  - Technology flexibility
- **Challenges:**
  - Shared dependencies
  - Styling consistency
  - Cross-app communication
- **Best Practices:**
  - Contract stability
  - Design system
  - Shared utilities

## 5. MODULAR MONOLITH
- **Concept:**
  - Monolith with clear modules
  - Bounded contexts
  - Future microservices-ready
- **Benefits:**
  - Simple deployment
  - Transactional integrity
  - Easy debugging
  - Migration path
- **Structure:**
  - Module boundaries
  - Clear interfaces
  - Internal dependencies
- **Migration:**
  - Extract module by module
  - Keep interfaces stable
  - No rush to separate

## 6. EVENT-DRIVEN ARCHITECTURE
- **Event Sourcing:**
  - Store all state changes as events
  - Append-only log
  - Rebuild state from events
- **CQRS:**
  - Separate read/write models
  - Denormalized reads
  - Eventual consistency
- **Message-Driven:**
  - Async communication
  - Decoupled services
  - Eventual consistency
- **Benefits:**
  - Complete audit trail
  - Time-travel debugging
  - Scalability

## 7. SPACE-BASED ARCHITECTURE
- **Pattern:**
  - Processing unit
  - Space (in-memory data grid)
  - Messaging grid
  - Data grid
- **Use Cases:**
  - High concurrency
  - Low latency
  - Elastic scalability
- **Benefits:**
  - No single bottleneck
  - Self-healing
  - In-memory speed
- **Implementation:**
  - GigaSpaces
  - Hazelcast
  - Apache Ignite

## 8. PIPELINE ARCHITECTURE
- **Pattern:**
  - Sequential processing
  - Data flows through stages
  - Each stage transforms
- **Benefits:**
  - Simple to understand
  - Easy to extend
  - Pipeline reuse
- **Implementation:**
  - Unix pipes
  - Functional composition
  - Builder pattern
- **Use Cases:**
  - Data processing
  - ETL pipelines
  - Build systems

## 9. MICRO-KERNEL ARCHITECTURE
- **Pattern:**
  - Core system
  - Plugin extensions
  - Extension points
- **Core:**
  - Minimal functionality
  - Stable interface
  - Extension contracts
- **Plugins:**
  - Independent
  - Hot-deployable
  - Versioned
- **Use Cases:**
  - IDEs
  - Browsers
  - ERP systems

## 10. STRANGLER FIG PATTERN
- **Strategy:**
  - Incrementally replace
  - Route traffic gradually
  - Old and new coexist
- **Steps:**
  - Install strangler in front
  - Add new capability
  - Redirect traffic
  - Remove old capability
- **Benefits:**
  - Low risk migration
  - No big-bang release
  - Rollback capability
- **Use Cases:**
  - Legacy modernization
  - Cloud migration
  - Technology upgrade

## 11. CLOUD-NATIVE ARCHITECTURE
- **Principles:**
  - Containerization
  - Microservices
  - Dynamic orchestration
  - DevOps culture
- **12-Factor App:**
  - Codebase
  - Dependencies
  - Config
  - Backing services
  - Build/release/run
  - Processes
  - Port binding
  - Concurrency
  - Disposability
  - Dev/prod parity
  - Logs
  - Admin processes
- **Benefits:**
  - Scalability
  - Resilience
  - Portability

## 12. SERVERLESS ARCHITECTURE
- **Patterns:**
  - Function as a Service
  - Backend as a Service
  - Mobile Backend as a Service
- **Benefits:**
  - No server management
  - Pay per use
  - Auto-scaling
- **Challenges:**
  - Cold starts
  - Vendor lock-in
  - Debugging complexity
- **Best Practices:**
  - Stateless functions
  - Event-driven
  - Efficient composition

---

**Invok:** `/architecture-patterns` | **Priority:** MEDIUM | **Version:** 1.0
