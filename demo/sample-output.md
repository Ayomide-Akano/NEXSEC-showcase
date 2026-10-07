# Sample output (sanitized)

The examples below are based on observed NEXSEC lab output. Real network identifiers have been replaced with documentation/demo values. No secrets, real IP addresses, MAC addresses, hostnames, or database details are included.

## Asset classification

```text
Asset classification completed: 3 asset(s) classified.

    asset_key          asset_id      ip          classification    role             confidence
------------------  -----------  ----------  ----------------  ---------------  ----------
ip:10.0.0.1        NEX-DEMO-001 10.0.0.1    network_gateway   gateway          high
ip:10.0.0.155      NEX-DEMO-003 10.0.0.155  nexsec_host       security_sensor  high
ip:10.0.0.205      NEX-DEMO-002 10.0.0.205  endpoint           endpoint         medium
```

## Authority candidate

```text
Candidate ID:            AUTH-DEMO-000001-gateway
Asset ID:                NEX-DEMO-001
Asset key:               ip:10.0.0.1
Candidate type:          gateway
Confidence:             70
Authorization state:    discovered
Integration state:      unknown
Authorized by:          —
ROLES
["gateway_candidate","enforcement_candidate"]

CAPABILITIES
["traffic_boundary_candidate"]
```

## NEXSEC-side authorization

```text
NEXSEC-side authority authorization recorded.
Device-side credentials/privileges have NOT been granted by this action.
```

## Access provisioning boundary

When no safe management adapter has been established, NEXSEC represents the state honestly rather than pretending it has access:

```text
Integration/access state: awaiting_adapter
```

These examples are intentionally sanitized. The public showcase does not publish the private implementation, database schema, exact classification rules, real network identifiers, credentials, or operational configuration.
