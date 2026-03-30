IAA is a simple way to think about how users and their actions are verified on applications.

It means, if a previous item isn't being performed, you cannot perform the later items which are:

1. Identity - the unique account (e.g user ID/email) that represents a person or service
2. Authentication - proving that identity (Passwords, OTP, passkeys)
3. Authorization - what that identity is allowed to do.
4. Accountability - recording and alerting on who did what, when and from where.

### Broken Access Control

It happens when the server doesn't properly enforce who can access what on every request.

A common occurence of this is IDOR(Insecure Direct Object Reference). if changing an ID (like ?id=7 -> ?id=6) lets you see or edit someone else's data, access control is broken.

In practice, this shows up as horizontal privilege escalation (same role, other user's stuff) or vertical privilage escalation (jumping to admin-only actions) because the application trusts the client too much.

### Authentication Failures

They happen when an application can't reliably verify or bind a user's identity. Common issues include:

- username enumeration
- weak/guessable passwords (no lockout/rate limits)
- logic flaws in the login/registration flow
- insecure session or cookie handling.

If any of these are present, an attacker can often log in as someone else or bind a session to the wrong account.

i.e. registering on a site as aDmiN instead of admin to gain access.

- **A01 Broken Access Control:** Enforce server-side checks on **every** request
- **A07 Authentication Failures:** Enforce unique indexes on the canonical form, rate-limit/lock out brute force, and rotate sessions on password/privilege changes.
- **A09 Logging & Alerting Failures:** Log the full auth lifecycle (fail/success, password/2FA/role changes, admin actions), centralise logs off-host with retention, and alert on anomalies (e.g., brute-force bursts, privilege elevation).