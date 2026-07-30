# Billing, plans & add-ons

**How is 4PM billed?**
Per **organization**. You pick a plan (Free / Pro / Max / Enterprise), pay by **Stripe** or
**PayPal** or a prepaid **credit wallet**, and the plan sets your quota and caps. See
[docs/10](../docs/10-billing-and-plans.md).

**What plan do I start on?**
Every org starts on **Free**. Only an **ADMIN** can change the plan.

**How do I upgrade?**
In **/billing**, pick the plan and provider and complete checkout. You can also pick a plan at
registration — checkout opens automatically after you verify and log in. On payment, your quota
regenerates automatically.

**What's the credit wallet?**
A prepaid balance. **Top up**, then **pay by credit** at checkout (activates immediately, no
redirect). Renewals are **wallet-first, card-fallback** — the wallet is used first, then your card
if needed.

**How does changing plans work?**
Paid→paid changes are **immediate**. You see a **quote** first (new full-period price, where it's
paid from, and the refund of your old plan's unused remainder). On confirm, 4PM charges (wallet
then card); if neither covers it, nothing changes. After the charge, the old plan's remainder is
refunded to your **credit wallet**.

**How do I downgrade to Free?**
Use **Cancel** (going to Free isn't a plan "change"). Enterprise and your current plan aren't
valid change targets.

**I ran out of AI quota.**
Upgrade your plan or buy a **scale-pack** add-on. Quota regenerates when the change activates.

**What add-ons are there?**
Extra **storage**, **scale packs** (add users/projects/storage), and **rented machine-user**
seats. You pick a quantity; one full period is charged up front and decreases apply at period end.

**What happens if a payment fails?**
Your subscription goes **past due** but quota is **preserved for a grace period** (about a week by
default) while 4PM retries and notifies you. If the grace period lapses, the org downgrades to
**Free**.

**Where do I see charges?**
The **statement** shows the current period (plan + add-ons as line items); the **payment history**
lists past periods across both payment methods.
