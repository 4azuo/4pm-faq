# Billing, plans & add-ons

**How is 4PM billed?**
Per **organization**. You pick a plan (Free / Pro / Max / Enterprise), pay by **Stripe** or
**PayPal** or a prepaid **credit wallet**, and the plan sets your quota and caps. See
[docs/10](../docs/10-billing-and-plans.md).

**What plan do I start on?**
Every org starts on **Free** (2M quota tokens a month). Only an **ADMIN** can change the plan.

**What do the plans include?**
Free / Pro ($20/mo) / Max ($100/mo) / Enterprise (custom); annual = 10 months. They differ in quota
tokens (2M / 20M / 100M a month), users, projects, parallel AI runs (2 / 10 / 30), AI Help per day,
storage, retention, autonomous rows, automation rules, and features such as teams, chat, 4rum, worker
pools, integrations, marketplace publishing and usage alerts. Prices exclude tax. See the plan table
in [docs/10](../docs/10-billing-and-plans.md#plans) or the pricing page.

**A feature says "not available on your plan".**
It needs a higher plan (see the table). After a downgrade your existing data stays readable, and a
notice shows what's paused.

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
seats. Each add-on bills **monthly on its own cycle**; you pick a quantity, one period is charged up
front and decreases apply at period end. You get reminders before an add-on renews. Free orgs can rent
machines too, paid from the credit balance.

**What happens if a payment fails?**
Your subscription goes **past due** but quota is **preserved for a grace period** (about a week by
default) while 4PM retries and notifies you. If the grace period lapses, the org downgrades to
**Free**.

**Where do I see charges?**
The **statement** shows the current period (plan + add-ons as line items); the **payment history**
lists past periods across both payment methods.

**What do Upgrade / Downgrade / Switch mean?**
In Billing › Change plan (which links to the full plan comparison), each plan button says whether it raises,
lowers or just switches your plan. On the Pricing page, a signed-in ADMIN sees **Current plan**, **Upgrade**
or **Downgrade** and goes straight to the change in Billing; members don't see plan buttons.

**How do I sign up for Enterprise? What are the requirements and pricing?**
Enterprise is a **custom, non-self-serve** plan — it isn't picked in **/billing** like Free/Pro/Max.
Procedure, requirements and pricing are **arranged directly with the 4PM team**, not published in
docs. Open a **support request** (Support in the user menu or footer) describing your Enterprise
needs, or use the in-app **Help** chat and choose "email a human". Only an **ADMIN** can change an
org's plan.
