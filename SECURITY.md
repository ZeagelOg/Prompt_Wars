# 🔒 Security Policy

## 🛡️ Secrets Management
- **Never Hardcode Keys:** API keys for Google Maps and Firebase are strictly managed through environment variables.
- **Secrets Manager:** In production, keys are injected via Google Cloud Secrets Manager.
- **Local Dev:** Use `.env` (ignored by git). See `.env.example`.

## 📜 Firebase Security Rules
We follow the **8 Pillars of Hardened Rules** to ensure zero-trust access:
1. **Master Gate:** Relational sync for sub-collections.
2. **Validation Blueprints:** Strict schema enforcement on every write.
3. **Path Hardening:** ID poisoning guards on document IDs.
4. **Tiered Identity:** Partitioned permissions for Staff vs. Attendees.
5. **Array Guarding:** Size limits on all list fields.
6. **PII Isolation:** Strict read restrictions on user data.
7. **Atomicity Guarantee:** `existsAfter` checks for relational integrity.
8. **Secure List Queries:** Rule-side enforcement on all queries.

## 🧪 Input Sanitization
All client-side data is validated via **Zod** before being sent to Firestore.
