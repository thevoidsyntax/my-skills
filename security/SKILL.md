---
name: security
description: "Enterprise security standards including authentication, authorization, secrets management, and encryption best practices."
version: "1.0"
---

# SECURITY MODULE

Kamu adalah Security Specialist. Gunakan rules ini untuk setiap aspek keamanan dalam proyek.

---

## 1. AUTHENTICATION & AUTHORIZATION
- **Strong Authentication:** Implementasikan multi-factor authentication (MFA) untuk semua user accounts. Gunakan TOTP, WebAuthn/FIDO2, atau SMS fallback (dengan understanding limitations).
- **Password Policy:** Minimum 12 karakter, mix uppercase/lowercase, angka, special character. Jangan pernah store plain password — gunakan bcrypt/argon2 dengan salt.
- **Authorization Model:** Implementasikan RBAC (Role-Based Access Control) atau ABAC (Attribute-Based Access Control) sesuai kompleksitas aplikasi.
- **Principle of Least Privilege:** Setiap service/user harus punya akses minimal yang dibutuhkan untuk menjalankan fungsinya.
- **Session Management:** Generate session ID yang cryptographically secure (min 128 bits entropy). Implementasikan sliding expiration dengan reasonable timeout (15-30 menit idle).

## 2. SECRETS MANAGEMENT
- **Never Hardcode:** Jangan pernah hardcode credentials, API keys, atau secrets di source code. Gunakan environment variables atau secret manager.
- **Secret Rotation:** Implementasikan automated secret rotation untuk service accounts dan API keys (max 90 hari rotation).
- **Secret Storage:** Gunakan dedicated secret management service:
  - HashiCorp Vault (self-hosted)
  - AWS Secrets Manager / GCP Secret Manager / Azure Key Vault (cloud-managed)
  - Doppler /.envchain (developer-friendly)
- **Secret Scanning:** Implementasikan pre-commit dan CI/CD scanning untuk detect secrets yang ter-commit tidak sengaja (gunakan tools seperti GitGuardian, TruffleHog).

## 3. ENCRYPTION STANDARDS
- **In-Transit Encryption:** Wajib gunakan TLS 1.2+ untuk semua komunikasi. Redirect HTTP ke HTTPS. Implementasikan HSTS (HTTP Strict Transport Security).
- **At-Rest Encryption:** Encrypt semua data sensitif di database menggunakan AES-256. Enable disk encryption untuk storage (LUKS, dm-crypt).
- **Key Management:** Gunakan dedicated KMS (Key Management Service). Jangan pernah store encryption keys di codebase atau config files.
- **Key Rotation:** Implementasikan automated key rotation dengan re-encryption dari data yang sudah ada.
- **Credential Transmission:** Jangan pernah kirim credentials via URL parameters — gunakan POST body atau headers.

## 4. INPUT VALIDATION & SANITIZATION
- **Defense in Depth:** Validasi input di setiap layer (API gateway, application layer, database layer).
- **SQL Injection Prevention:** Gunakan parameterized queries / prepared statements. Jangan pernah concatenate user input ke SQL query.
- **XSS Prevention:** Escape semua output sesuai context (HTML, JavaScript, URL, CSS). Gunakan Content Security Policy (CSP) headers.
- **Command Injection:** Jangan pernah pass user input ke system shell tanpa sanitization yang ketat. Gunakan allowlist untuk command arguments.
- **Serialization Attacks:** Jangan deserialize untrusted data tanpa validation. Pertimbangkan untuk menggunakan JSON-only APIs.

## 5. SECURITY HEADERS
- **Content-Security-Policy:** Definisikan CSP yang restrictive untuk prevent XSS dan injection attacks.
- **X-Frame-Options:** Set ke `DENY` atau `SAMEORIGIN` untuk prevent clickjacking.
- **X-Content-Type-Options:** Set ke `nosniff` untuk prevent MIME sniffing.
- **Referrer-Policy:** Set ke `strict-origin-when-cross-origin` atau `no-referrer`.
- **Permissions-Policy:** Disable fitur browser yang tidak diperlukan (camera, microphone, geolocation).

## 6. ZERO TRUST ARCHITECTURE
- **Never Trust, Always Verify:** Jangan ada implicit trust antar services. Setiap request harus di-authenticate dan di-authorize.
- **Service-to-Service Auth:** Implementasikan mTLS atau JWT-based service authentication untuk inter-service communication.
- **Network Segmentation:** Pisahkan network berdasarkan trust level (DMZ, internal services, database tier).
- **Micro-segmentation:** Implementasikan granular network policies — setiap service hanya bisa communicate dengan service yang dibutuhkan.

## 7. THREAT MODELING
- **STRIDE Model:** Evaluasi setiap komponen terhadap:
  - **S**poofing (authentication threats)
  - **T**ampering (integrity threats)
  - **R**epudiation (non-repudiation threats)
  - **I**nformation Disclosure (confidentiality threats)
  - **D**enial of Service (availability threats)
  - **E**levation of Privilege (authorization threats)
- **Attack Surface Analysis:** Identifikasi dan minimize attack surface untuk setiap service.
- **Threat Tree:** Document potential attack vectors dan mitigations.

## 8. DEPENDENCY VULNERABILITY MANAGEMENT
- **Dependency Scanning:** Scan semua dependencies (direct dan transitive) untuk known vulnerabilities. Gunakan tools seperti:
  - Snyk, Dependabot, Renovate (for package managers)
  - Trivy, Grype (for container images)
- **SBOM (Software Bill of Materials):** Generate dan maintain SBOM untuk setiap release.
- **Patch Management:** Tentukan SLA untuk patching critical/high vulnerabilities:
  - Critical: 24 jam
  - High: 7 hari
  - Medium: 30 hari
- **License Compliance:** Scan untuk problematic licenses (GPL, AGPL, copyleft) yang bisa mempengaruhi legal status aplikasi.

## 9. GDPR & PII HANDLING
- **Data Minimization:** Collect hanya data yang benar-benar dibutuhkan.
- **Purpose Limitation:** Data hanya boleh diproses untuk tujuan yang sudah didefinisikan.
- **Consent Management:** Implementasikan clear consent mechanism dengan granular opt-in/opt-out.
- **Right to Erasure:** Pastikan semua PII bisa dihapus sepenuhnya (termasuk dari backups).
- **Data Portability:** Sediakan mekanisme untuk export data dalam machine-readable format.
- **Privacy by Design:** Privacy harus di-consider sejak design phase, bukan ditambahkan kemudian.

## 10. SECURITY AUDIT & COMPLIANCE
- **Security Audit Trail:** Log semua security-relevant events (login attempts, privilege changes, data access).
- **Immutable Logs:** Logs harus immutable dan tamper-evident. Gunakan append-only storage atau signed logs.
- **Penetration Testing:** Lakukan penetration testing secara berkala (minimal annually atau setelah major changes).
- **Compliance Framework:** Identifikasi dan implementasikan relevant compliance requirements:
  - SOC 2 Type II untuk service providers
  - ISO 27001 untuk information security
  - PCI-DSS jika memproses payment cards
  - HIPAA jika memproses PHI

## 11. INCIDENT RESPONSE
- **Incident Classification:** Definisikan severity levels dan response time targets.
- **Communication Plan:** Siapkan template untuk breach notification sesuai regulasi (GDPR: 72 jam).
- **Forensic Readiness:** Implementasikan logging dan monitoring yang cukup untuk forensic analysis.
- **Post-Incident Review:** Lakukan root cause analysis dan implementasikan preventive measures.

## 12. SECURE DEVELOPMENT LIFECYCLE
- **Secure Coding Standards:** Dokumentasikan dan enforce secure coding guidelines.
- **Code Review Security Checklist:** Tambahkan security checkpoints di code review process.
- **Security Training:** Pastikan semua developers mendapat security awareness training.
- **Threat Modeling in Design:** Lakukan threat modeling untuk setiap new feature sebelum implementation.

---

**Invok:** `/security` | **Priority:** HIGH | **Version:** 1.0
