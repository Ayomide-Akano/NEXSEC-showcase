# Testing method

Every NEXSEC capability follows the same controlled loop:

**TEST → OBSERVE → DOCUMENT → FIX → RETEST**

A capability is not considered finished simply because its code exists. It must be exercised in the isolated lab, its behavior must be observed, failures documented, fixes applied, and the capability tested again.

## Test boundaries

Testing is staged from least invasive to most capable:

1. **Safe-mode tests** — syntax, dependency, state, and temporary-data checks.
2. **Local observation** — inspect NEXSEC behavior without changing external security state.
3. **Isolated discovery** — discover only explicitly authorized lab networks and hosts.
4. **Baseline and change detection** — establish known-good state and identify controlled changes.
5. **Correlation and risk scoring** — connect observations into meaningful security context.
6. **Controlled enforcement** — test only explicitly authorized enforcement actions.
7. **Recovery and watchdog testing** — verify safe failure, suspension, restart, and recovery behavior.

## Evidence standard

For each test, record:

- what was tested;
- the expected behavior;
- what actually happened;
- relevant evidence;
- defects or gaps discovered;
- the fix applied;
- the retest result.

This method is intended to prevent "implemented" from being confused with "verified."
