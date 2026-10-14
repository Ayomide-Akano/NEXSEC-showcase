# NEXSEC: Nexera Security

**A defensive security framework that understands a network before it acts on it.**
Built in Bash and SQLite for authorized lab networks. It discovers assets, classifies them from evidence, watches for change, and keeps *discovery*, *authorization* and *enforcement* strictly separate.

> **Understand before acting. Authorize before controlling. Validate before enforcing.**

![status](https://img.shields.io/badge/version-0.3-blue) ![stack](https://img.shields.io/badge/stack-Bash%20%2B%20SQLite-lightgrey) ![scope](https://img.shields.io/badge/scope-authorized%20lab%20networks-green) ![source](https://img.shields.io/badge/source-private-red)

This is the public overview. **The source code is private.** See [Contact](#contact) if you would like to try it.

---

## Why NEXSEC exists

Modern networks are dynamic and poorly understood. Devices come and go, services change, and several systems (routers, firewalls, identity and cloud controls) may all claim authority over the same network. Most security tools work alone, and automation that acts without understanding its environment can make wrong calls at machine speed.

NEXSEC is built on one idea: **never confuse the ability to act with the authority to act.** Seeing a gateway does not mean controlling it. NEXSEC records it as a *candidate*, and any use of it requires explicit authorization from IT first.

## One lifecycle, not a pile of tools

```
Discover → Find authorities → Classify → IT authorizes → Integrate
        → Validate capability → Enforce (controlled) → Baseline → Watch
```

| Stage | What happens |
|---|---|
| **Discover** | An observation-only first scan inventories hosts and services. Nothing is blocked. |
| **Find authorities** | Gateways and firewall-capable devices are recorded as candidates, with evidence. |
| **Classify** | Assets are classified from evidence (gateway, sensor, endpoint) with a confidence level, not guesswork. |
| **Authorize** | IT chooses which device may enforce. Authorization is a human decision, recorded and auditable. |
| **Validate** | The chosen enforcer is tested to prove what it can actually do *before* it is relied on. |
| **Enforce** | Quarantine runs through one central gate. It stays deferred until a validated enforcer exists. |
| **Baseline and Watch** | A known-good baseline is saved, then continuously compared against reality. |

---

## What's new in v0.3: "Watch detects more"

Continuous Watch now runs a registry of **21 tunable detectors** on top of the asset-change monitoring from earlier versions.

| Area | What it looks for |
|---|---|
| **Network integrity** | ARP spoofing, MAC address changes, one device claiming several addresses |
| **Device identity** | A device whose vendor or OS no longer matches its baseline, and newly opened risky services (Telnet, SMB, RDP, VNC and similar) |
| **Presence** | Devices that leave, return, or stay away for a long time |
| **Access** | Brute-force attempts, successful logins after failures, new login sources, odd-hour logins, new remote sessions |
| **Integrity** | Changes to accounts, privileges, SSH keys, scheduled jobs, startup items and NEXSEC's own files |
| **Traffic** | Port scans and new remote-access connections seen through the gateway |

Every detector has its own **severity, confidence, cooldown and response**, and can be switched off.

### An alert centre built for people

- **Severity-coloured pop-ups:** critical is red, high orange, medium amber, low blue, info green
- **Alert lifecycle:** new → acknowledged → resolved, with automatic **escalation** if nobody responds
- **Delivery:** desktop, syslog, webhook (including Slack), Telegram and email
- **Privacy on the way out:** alerts sent outside the machine are redacted by default

### Safety rules that are built in

- **Every detector is alert-only by default.** A person decides before anything is blocked.
- Automatic responses require a **minimum confidence**, and **never** touch the gateway, protected devices or devices IT has accepted.
- Repeat alerts inside a cooldown are suppressed and counted rather than flooding the screen.

---

## Reports

Every assessment produces an **HTML or XML report in two versions**:

- **Admin:** the full picture
- **Standard user:** sensitive details redacted (hostnames are pseudonymised)

Access to each is gated by its own key.

## Status

| Status | Capability |
|---|---|
| ✅ Tested in a real lab | Security setup with separate **ADMIN** and **USER** access |
| ✅ Tested in a real lab | Observation-only discovery, device classification, gateway detected as an authority candidate |
| ✅ Tested in a real lab | Guided onboarding: choose and validate an enforcer, then quarantine and authorize devices |
| ✅ Tested in a real lab | Real quarantine through a Linux gateway (a quarantined device could no longer be reached) |
| ✅ Tested in a real lab | Vulnerability assessment with risk scoring, and HTML/XML reports in two audiences |
| ✅ Tested in a real lab | Continuous Watch: new devices and new services detected and alerted |
| 🔧 Built, mock-tested, lab validation in progress | **v0.3 detectors and alert centre** (21 detectors, escalation, multi-channel delivery) |
| 🧭 Planned | Scanner plugin layer, local vulnerability intelligence, confidence and decision model |
| 🧭 Planned | Lightweight host agents, a Linux agent first |
| 🧭 Planned | AI layer, starting in shadow mode and then advisory only |

*"Tested in a real lab" means exercised on a virtual lab I own, using Kali Linux as the gateway and several Linux and Windows machines. v0.3 passes 46 automated checks on a simulated lab, and is now being validated on real hardware.*

## Roadmap

1. **Watch detects more** ✅ *v0.3*
2. **Scanner plugin layer:** bring in established scanners (for example Nuclei and testssl.sh) as plugins, with results normalised into the same findings and risk model
3. **Local vulnerability intelligence:** map findings to known CVEs without sending data off the network
4. **Confidence model and decision table:** every decision explained by its evidence
5. **Host agents:** lightweight agents on IT-approved devices
6. **AI layer:** first in *shadow mode* (it suggests and is scored against what people actually decided), then *advisory*. **The AI layer never has authority to act on its own.**
7. **Dashboard:** a web view for alerts and reports

## Design principles

- **Understand before acting.** A system should not defend what it does not understand.
- **Authorize before controlling.** Discovering an authority does not grant control of it.
- **Validate before enforcing.** Confirm what an integration can do before relying on it.
- **Observation before enforcement.** The first pass inventories and classifies without blocking anything.
- **Represent reality, not fabricated capability.** If no safe adapter exists, NEXSEC says so.
- **Explain important decisions.** Every decision traces back to evidence, authorization and integration state.
- **Controlled autonomy.** More autonomy requires more visibility, policy, validation and auditing.
- **Protect the protector.** NEXSEC itself is treated as a high-value asset.
- **Conservative classification.** Evidence and confidence over false certainty.
- **Humans stay in charge.** Trustworthy automation, not maximum automation.

## How it is built and tested

```
TEST → OBSERVE → DOCUMENT → FIX → RETEST
```

Each version is tested twice: on a simulated lab (automated, repeatable), then on a real virtual lab with a written test guide. Real hardware keeps finding things simulations miss, and each finding becomes a fix with its own test. For example:

- a gateway with two network interfaces confused address selection, so the enforcer was never offered
- DHCP lease timers caused false "network changed" alarms
- a vulnerability scan that failed silently now reports why, and retries with a lighter scan
- scans were slowing small machines, so they now run at lower priority with per-script limits

NEXSEC is only used on networks and devices I own or am authorized to test. **No production systems, real credentials or real network data appear in this repository.**

## Documentation

- Architecture
- Design principles
- Security model (high level)
- Testing method
- Roadmap
- Sanitized sample output

## Related work

- **[Nmap Network Scanning Lab](https://github.com/Ayomide-Akano/01-Nmap-Network-Scanning-Lab):** the documented assessment project that started all of this.

## Contact

**Ayomide Temitayo Akano**, cybersecurity, Lagos, Nigeria.

I am looking for **small businesses and schools** willing to try NEXSEC on a network they own, free of charge, in exchange for honest feedback. I am also open to junior SOC and security analyst roles, security engineering opportunities, contract work, internships and collaboration.

- Email: akanoayomi1276@gmail.com
- LinkedIn: https://www.linkedin.com/in/akano-ayomide-6a20a4193
- GitHub: https://github.com/Ayomide-Akano

## License

Copyright (c) 2026 Ayomide Temitayo Akano. All rights reserved. See [LICENSE](LICENSE).
