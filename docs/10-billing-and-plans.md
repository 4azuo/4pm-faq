# Plans, billing & add-ons

4PM bills per **organization**. You pick a **plan**, pay with **Stripe** or **PayPal** (or a
prepaid **credit wallet**), and your plan sets the quota and caps your org gets. Add-ons let you
top up specific limits without changing plan.

## Plans

| | Free | Pro | Max | Enterprise |
| --- | --- | --- | --- | --- |
| Price / month (annual = 10 months) | 0 | $20 | $100 | contact sales |
| AI quota tokens / month | 2M | 20M | 100M | custom |
| Users · projects | 5 · 1 | 20 · 3 | 100 · 10 | unlimited |
| Parallel AI runs (org) | 2 | 10 | 30 | unlimited |
| AI Help questions / user / day | 10 | 30 | 100 | unlimited |
| Hosted storage | 1 GB | 10 GB | 100 GB | unlimited |
| Data retention | 15 days | 90 days | 365 days | unlimited |
| Memo items | 200 | 2 000 | 10 000 | unlimited |
| New autonomous rows / book / month | 100 | 500 | 3 000 | unlimited |
| Automation rules · rule runs / day | — | 50 · 500 | 100 · 5 000 | unlimited |
| Teams, chat, worker pools, integrations, marketplace publishing, usage alerts, announcements | — | ✓ | ✓ | ✓ |
| Community (4rum) | — | — | ✓ | ✓ |
| SAML SSO, organization audit log | — | — | — | ✓ |
| Rent 4PM machines · install from the Marketplace | ✓ | ✓ | ✓ | ✓ |

Prices exclude tax. **Quota tokens** are weighted by token type, so usage
charts show both every token used and the quota tokens counted. Only an **ADMIN** can change the plan;
the **Usage** tab shows how much of each limit you use.

After a downgrade, existing data stays readable and a notice shows which features are paused.

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

You choose a **quantity** per add-on. Each add-on bills **monthly on its own cycle**: one period is
charged up front; decreases or cancellations take effect at the end of the period, and you get reminders
30, 10, 3 and 1 days before a renewal. Add-ons stack on top of your plan's caps. Buying one shows the
terms that apply, which you confirm first.

- **Free** orgs can rent machines too, paid from the credit balance.
- **Cancelling** a paid plan keeps your rented machines running; extra storage and scale packs end with
  the plan.

## Payment failure (dunning)

- If a renewal payment fails, your subscription goes **past due** but your quota is **preserved
  for a grace period** (about a week by default) while 4PM retries and notifies you.
- If the grace period passes (or you cancel at period end), the org is downgraded to **Free** and
  quota is regenerated for the Free plan.

## Statements & history

- The **statement** shows the current period's charges (plan + add-ons as line items), with a
  **timeline** chart of past and upcoming payments.
- The **payment history** lists every past period across both payment methods.

## Common questions

- **"How do I upgrade?"** — /billing → pick the plan → confirm the quote (immediate).
- **"I ran out of AI quota."** — upgrade your plan or buy a scale-pack add-on; quota regenerates
  when the change activates.
- **"Will I lose access if a payment fails?"** — not immediately; there's a grace period before
  any downgrade.

See also: [Billing FAQ](../faq/billing.md).
