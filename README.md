# MTA-STS policy for mhs.mn

This repository only hosts the MTA-STS policy for the **mhs.mn** mail domain
(Microsoft 365 / Exchange Online). It is published with GitHub Pages at:

https://mta-sts.mhs.mn/.well-known/mta-sts.txt

MTA-STS tells other mail servers to deliver email to mhs.mn only over a
verified, encrypted (TLS) connection to Microsoft's mail servers.

## Related DNS records (Datacom panel)

| Host | Type | Value |
|---|---|---|
| `mta-sts` | CNAME | `tugutg.github.io` |
| `_mta-sts` | TXT | `v=STSv1; id=<policy id>` |
| `_smtp._tls` | TXT | `v=TLSRPTv1; rua=mailto:tuguldur@mhs.mn` |

## Changing the policy

1. Edit `.well-known/mta-sts.txt` (LF or CRLF line endings are both fine, RFC 8461).
2. Change the `id=` value in the `_mta-sts` TXT record (any new value, e.g. a date like `2026110201`),
   otherwise senders keep using their cached copy.

Modes: `testing` (report only, never blocks mail) → `enforce` (block delivery over
insecure connections). Switch to `enforce` only after TLS-RPT reports show no failures.

If the MX record ever changes away from `*.mail.protection.outlook.com`
(for example to Microsoft's newer `*.mx.microsoft` hosts), update the `mx:` line
**before** changing the MX record.
