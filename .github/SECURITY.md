# Security Policy

## Supported versions

Only the latest released version of Stealtify receives security fixes. Please
update to the newest build before reporting an issue.

| Version | Supported |
|---------|-----------|
| 1.0.x   | ✅        |
| < 1.0   | ❌        |

## Reporting a vulnerability

**Please do not open a public issue for security vulnerabilities.**

Report privately through one of:

- GitHub → **Security** tab → **Report a vulnerability** (private advisory), or
- email **security@stealtify.app** (fallback: **support@stealtify.app**).

Include where possible:

- affected version (`versionName` / `versionCode`) and device/Android version,
- a description of the issue and its impact,
- steps to reproduce or a proof of concept,
- any relevant logs (with IPs/hostnames redacted).

### What to expect

- Acknowledgement within **72 hours**.
- An initial assessment within **7 days**.
- Coordinated disclosure: we will agree on a timeline before any public
  disclosure and credit you in the release notes unless you prefer to stay
  anonymous.

## Scope

In scope: the Stealtify Android app (`com.stealtify.app`), the packet engine,
the Go engine (`gostengine`), the update/subscription handling, and secret
storage.

Out of scope: vulnerabilities in third-party proxy servers you configure, in
bundled upstream libraries that already have an upstream fix (report those
upstream), and issues requiring a rooted/compromised device or physical access
with an unlocked bootloader.

## Handling of secrets

Stealtify stores proxy credentials and keys in the Android Keystore
(`SecretStore`); they are never written to the exported schema or logs in
plaintext. If you find a path that leaks a secret (logs, backups, IPC), treat it
as a security report and use the private channel above.
