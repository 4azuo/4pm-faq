# Worker pools & AI routing

**What's a worker pool?**
A named group of your machine-users with a duty — e.g. one pool for spec work, another for autonomous
runs. Manage pools in **Machines › Pools** (ADMIN, Pro plan and above). See
[docs/24](../docs/24-worker-pools-and-routing.md).

**How do I make a project use several workers?**
In the project's **Members › AI routing**, attach pools or lone machines, choose which AI jobs each serves
and their priority, then **Save routing**.

**Which worker runs a job?**
Pools before lone machines, then higher priority, then order; the first idle worker wins. Busy, offline
or out-of-budget workers are skipped, so work fails over automatically.

**"All workers busy" — what now?**
Every worker that serves this job is busy, offline or out of AI budget. Wait, add a worker or pool to the
routing, or add AI accounts to the workers.

**My AI run says "Waiting for an AI run slot — N ahead".**
Your organization is at its plan's limit of parallel AI runs (Free 2, Pro 10, Max 30). The run starts
automatically when a slot frees up.

**Can a worker serve only some teams?**
Yes — set **Teams served** on its routing entry. It then takes only those teams' autonomous requests and
tasks.

**A newly attached machine shows "Not provisioned".**
It couldn't clone the repo — usually git authentication. Fix it in **Git › Configuration**, then
**Retry**.

**What's the org AI pool in Settings › AI?**
The pool that runs organization-level AI tasks such as AI checklist authoring and AI Research. It can't
also be attached to a project.

**Can I put a rented machine in my pool?**
Yes, while you rent it. It leaves your pools and routing automatically when the rental ends.
