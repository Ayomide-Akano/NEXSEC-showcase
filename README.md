# NEXSEC — Nexera Security

A Bash and SQLite defensive security framework for authorized lab networks. It discovers assets, classifies them from evidence, and keeps **discovery, authorization, and enforcement strictly separate**.

> Understand before acting. Authorize before controlling. Validate before enforcing.

*This is the public overview. The source code is kept private. See [Contact](#contact).*

## The problem

Modern environments are dynamic and poorly understood. Devices appear and disappear, services change, and several authorities (routers, firewalls, cloud controls, identity systems) may control the same network. Security tools often work in isolation, while security automation that acts without understanding its environment can make inaccurate assessments or take inappropriate actions.

## The approach

NEXSEC is built around one **lifecycle** instead of a pile of separate tools:

**Discovery → Authority Discovery → Classification → IT Authorization → Access Provisioning → Integration → Capability Validation → Controlled Enforcement → Baseline → Continuous Watch**

The core rule is simple: **never confuse the ability to act with the authority to act.** Seeing a gateway does not mean controlling it. NEXSEC records it as a candidate, and any use of it requires explicit authorization first.

## Status

| Status | Capability |
|---|---|
| Working | Security setup with separate ADMIN and USER secrets |
| Working | Observation-only first discovery scan (nothing is blocked automatically) |
| Working | Discovery of directly connected networks and hosts |
| Working | Gateway detected as an authority candidate, with recorded evidence |
| Working | NEXSEC-side authorization (does not grant device-side access) |
| Working | Evidence-based asset classification (gateway, NEXSEC sensor, endpoint) |
| In progress | Command Center: asset and service inventory and details (implementation complete; full interactive verification pending) |
| Working | Database reset for repeatable lab testing |
| In progress | Continuous Watch (start, suspend, resume, stop, status) |
| In progress | Firewall enforcement, segmentation, risk, incidents, audit, zero trust |
| Planned | Linux/nftables gateway integration, baselines, anomaly detection, policy engine |

Status reflects capabilities that have been implemented and/or exercised in the controlled lab; items awaiting full end-to-end verification are deliberately not presented as complete.

## Design principles

- **Understand before acting.** A system should not defend what it does not understand.
- **Authorize before controlling.** Discovering an authority does not grant control of it.
- **Validate before enforcing.** Confirm what an integration can actually do before relying on it.
- **Observation before enforcement.** The first discovery pass inventories and classifies without automatically blocking newly observed assets.
- **Represent reality, not fabricate capability.** If no safe adapter exists, NEXSEC reports that the integration is awaiting an adapter.
- **Explain important decisions.** Decisions should be traceable to evidence, authorization, and integration state.
- **Controlled autonomy.** Greater autonomy requires stronger visibility, policy controls, validation, and auditing.
- **Protect the protector.** NEXSEC itself must be treated as a high-value security asset.
- **Conservative classification.** Evidence and confidence are preferred over false certainty.
- **Trustworthy automation, not maximum automation.**

## Lab environment

Development and validation use an isolated, authorized lab with Kali Linux as the NEXSEC host and a Metasploitable test target.

The development method is:

**TEST → OBSERVE → DOCUMENT → FIX → RETEST**

No real production systems or credentials are represented in this public showcase.

## Documentation

- [Architecture](docs/architecture.md)
- [Design principles](docs/design-principles.md)
- [Security model — high level](docs/security-model.md)
- [Testing method](docs/testing-method.md)
- [Roadmap](docs/roadmap.md)
- [Sanitized sample output](demo/sample-output.md)

## Related work

- [Nmap Network Scanning Lab](https://github.com/Ayomide-Akano/01-Nmap-Network-Scanning): a documented security assessment portfolio project.

## Contact

**Ayomide Temitayo Akano**, cybersecurity — Nigeria.

Open to cybersecurity roles, security engineering opportunities, contract work, internships, and collaboration.

GitHub: https://github.com/Ayomide-Akano

## License

Copyright (c) 2026 Ayomide Temitayo Akano. All rights reserved. See [LICENSE](LICENSE).
