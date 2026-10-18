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

**Can one rule start another?**
Yes. Pick **Another rule finished** as the trigger, choose the rule it follows and which results start it
(succeeded, partial, failed). The follow-up rule can use that rule's AI output and the original event —
e.g. *AI summarises a failed task* → *post the summary to a webhook*. A run shows which rule's run started
it.

**Are there limits on chains?**
Saving a link that would make a loop, or a chain longer than **5** rules, is refused. A
rule that other rules follow can't be deleted until you change or remove the followers.

**What is the Rules Board?**
Rules › **Board**: all rules as connected lanes — each chain from its trigger, then the standalone rules —
coloured by their last run (or *never run* / *off*). Search, show enabled or all, click a rule to see it,
or **+** to add a rule that follows it. **Dry run** also lists the rules that would follow (*Then: …*).

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
