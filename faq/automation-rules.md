# Automation rules

**What can rules do?**
When something happens (a task fails, a PR is merged, a checklist falls below its minimum, a worker goes
offline, on a schedule…), notify people, call a webhook, generate a document, run a checklist with AI,
run a read-only AI instruction, pause autonomous mode, or write to the activity log. See
[docs/27](../docs/27-automation-rules.md).

**Where do I create them?**
Organization rules in Home › **Rules** (ADMIN); project rules in the project's **Rules** tab (ADMIN and the
project's PM).

**I don't see Rules / can't create a rule.**
Rules need the **Pro** plan or higher, and you must be an ADMIN (org rules) or the project's PM (project
rules). Pro allows 50 rules, Max 100; the count includes rules that are switched off.

**Can a project turn off an org rule?**
Yes, from its Rules tab — unless the org rule is **Enforced**.

**How do I test a rule safely?**
Use **Dry run**: it shows what the rule would do for an event, without doing it.

**My rule didn't run.**
Check the **Runs** log: the run may be *skipped* (outside the time window, throttled, over the daily limit)
or the event didn't match the filters. Some triggers (autonomous, PRs) need an up-to-date worker CLI, and
PR merged/closed need the GitHub App or a GitLab credential.

**My rule was disabled by itself.**
Its owner lost a permission the actions need, or left the organization. Its managers were notified;
update the rule (a new owner) and enable it again.

**How do I verify the webhook came from 4PM?**
Check the `X-4PM-Signature` HMAC with the secret shown once when you saved the rule (you can rotate it).

**Can a rule merge a PR or approve a task?**
No. Merging PRs, approving book rows and deleting branches always stay with people.
