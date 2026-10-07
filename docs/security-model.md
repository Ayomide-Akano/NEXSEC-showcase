# Security model (high level)

This page describes the security *approach*. Implementation details are intentionally not published.

- **Role separation:** separate ADMIN and USER secrets, so sensitive information is not freely exposed through the interface.
- **Authority separation:** discovering an authority, authorizing it, and gaining access to it are three different recorded steps.
- **Safe defaults:** early discovery is observation-oriented and enforcement is not assumed to be available merely because a candidate is detected.
- **Authorized scope only:** NEXSEC must only be used on networks and systems the operator owns or is explicitly authorized to assess.
- **Auditability:** security-sensitive actions are designed to be reconstructable after the fact.
- **Operator interface:** an authenticated Command Center is intended to be the normal way to inspect inventory rather than having operators query internal storage directly.
- **Least capability:** an unavailable adapter or unvalidated capability is represented as unavailable rather than guessed.
- **Planned hardening:** secure credential storage, encryption of sensitive state, key rotation, privilege separation, tamper detection, protected audit logs, secure updates, and integrity verification.
