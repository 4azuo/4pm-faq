# Accounts & login

**How do I sign up?**
Register with a username, email and password. This creates your **organization** and its first
**root** user, and sends a verification email. Details:
[docs/02](../docs/02-accounts-and-login.md).

**Why can't I log in right after registering?**
You must **verify your email** first via the link 4PM sends. Login isn't possible before
verification.

**I have the right password but login fails — why?**
Check your **login mode**. Leave the *Organization Identifier* empty to log in as the **root**
user; enter your org's **Organization Identifier** (a UUID) to log in as an org user. Using the
wrong mode returns an invalid-credentials error.

**What's the "Organization Identifier"?**
A UUID that identifies your organization at login. Org (non-root) users need it; an ADMIN can
provide it. Root users leave it empty.

**Why am I asked for a 6-digit code?**
**Root** users must complete MFA at login. 4PM emails a 6-digit one-time code (valid ~5 minutes,
limited attempts). Enter it to finish logging in.

**My account is locked.**
Too many failed attempts triggers a lockout. Wait and retry, or ask an ADMIN in your org.

**How do I reset my password?**
Use the reset-password flow; 4PM emails you a reset link. For security, the response is the same
whether or not the address exists.

**How long do sessions last?**
Sessions refresh automatically; by default the refresh window is 7 days, after which you log in
again. There is no "remember password" option.

**Why is an action blocked for me?**
You're probably missing the **permission** for it. Roles (ADMIN, PM, TL, etc.) grant permissions —
ask an ADMIN or PM to grant what you need. See [docs/02](../docs/02-accounts-and-login.md#roles--permissions).
