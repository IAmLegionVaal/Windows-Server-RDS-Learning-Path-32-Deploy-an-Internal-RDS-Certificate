# Windows Server RDS Learning Path 32 — Deploy an Internal RDS Certificate

**Level:** Intermediate · **Module:** 32/70

## Goal
Request or issue trusted certificates for the RDS role names used by the lab.

## Setup
1. Define final FQDNs for Broker publishing, Broker SSO, Web Access and Gateway.
2. Request a certificate with matching subject/SAN values and Server Authentication EKU.
3. Enroll it on the correct server.
4. Verify chain, name, private key, expiry and revocation reachability.
5. Export a PFX only when role assignment requires it.
6. Protect the PFX and password outside Git.

```powershell
Get-ChildItem Cert:\LocalMachine\My | Select-Object `
 Subject,DnsNameList,Thumbprint,NotAfter,HasPrivateKey,EnhancedKeyUsageList
certutil.exe -store My
```

## Evidence
Store request/template settings, public certificate properties, chain validation, approved names, expiry/renewal plan and private-key handling record under `evidence/`. Never commit PFX files or passwords.

## Troubleshooting
Name mismatch requires a corrected certificate, not ignoring warnings. Chain errors require root/intermediate trust and reachable revocation information.

## Security
Private keys and PFX passwords are secrets. Limit export permission and use trusted certificate authorities.

## Rollback
Remove only the test certificate after role bindings are moved to a valid replacement.

## Next
`Windows-Server-RDS-Learning-Path-33-Assign-Certificates-to-RDS-Roles`
