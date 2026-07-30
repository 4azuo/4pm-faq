# Plans, billing & add-ons

4PM bills per **organization**. You pick a **plan**, pay with **Stripe** or **PayPal** (or a
prepaid **credit wallet**), and your plan sets the quota and caps your org gets. Add-ons let you
top up specific limits without changing plan.

## Plans

4PM offers tiered plans, for example:

| Plan | For |
| --- | --- |
| **Free** | Getting started; the plan every org begins on. |
| **Pro** | Growing teams that need more quota and higher caps. |
| **Max** | Heavier usage and larger teams. |
| **Enterprise** | Custom terms (arranged with 4PM, not self-serve). |

A plan determines your **quota** (AI usage) and your **caps** (users, projects, teams, storage,
retention, etc.). Only an **ADMIN** can change the plan.

## Subscribe / checkout

You can subscribe from **/billing**, or during registration (the plan you pick at sign-up opens
checkout automatically after you verify your email and log in).

1. Pick the plan (e.g. **Pro**) and a **provider** (Stripe or PayPal).
2. 4PM sends you to the provider's hosted checkout page.
3. Pay there. When the payment confirms, your org is switched to the plan and its **quota is
   regenerated** automatically from the plan's limits.

Payment status drives entitlement automatically — there's nothing to toggle manually after paying.

## Credit wallet

Instead of (or before) paying by card, an org can keep a **prepaid credit balance**:

- **Top up** the wallet with a one-time charge.
- **Pay by credit** at checkout — the first period is deducted from the wallet and activates
  immediately (no redirect). If the balance is too low, you're pointed to top up.
- **Renewals** are **wallet-first, card-fallback**: each period 4PM deducts the wallet and only
  charges your card if the wallet can't cover it.

## Change plan

Every paid→paid change takes effect **immediately**:

1. You see a **quote** first — the new plan's full-period price, where it's paid from, and the
   **refund** of your old plan's unused remainder.
2. On confirm, 4PM charges the amount (wallet first, then card). If neither can cover it, the
   change is refused with a payment error and nothing changes.
3. After the charge succeeds, the unused remainder of your old plan is **refunded to your credit
   wallet**, and your new plan starts a fresh period.

To go to **Free**, use **Cancel** (it's not a plan "change"). Enterprise and your current plan
aren't valid change targets.

## Add-ons

Beyond your base plan you can buy recurring **add-ons** on the same subscription period, for
example:

- **Extra storage** (GB packs).
- **Scale packs** that add users / projects / storage (mirroring a plan tier).
- **Rented machine-user seats** — a pooled worker you don't have to run yourself (see
  [Rent a 4PM machine-user](./11-rented-machines.md)).

You choose a **quantity** per add-on. One full period is charged up front; decreases or
cancellations take effect at the end of the period. Add-ons stack on top of your plan's caps.

## Payment failure (dunning)

- If a renewal payment fails, your subscription goes **past due** but your quota is **preserved
  for a grace period** (about a week by default) while 4PM retries and notifies you.
- If the grace period passes (or you cancel at period end), the org is downgraded to **Free** and
  quota is regenerated for the Free plan.

## Statements & history

- The **statement** shows the current period's charges (plan + add-ons as line items).
- The **payment history** lists every past period across both payment methods.

## Common questions

- **"How do I upgrade?"** — /billing → pick the plan → confirm the quote (immediate).
- **"I ran out of AI quota."** — upgrade your plan or buy a scale-pack add-on; quota regenerates
  when the change activates.
- **"Will I lose access if a payment fails?"** — not immediately; there's a grace period before
  any downgrade.

See also: [Billing FAQ](../faq/billing.md).
