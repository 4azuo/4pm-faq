# Rent a 4PM machine-user

Don't want to run your own worker? You can **rent a machine-user from 4PM's pool**. 4PM operates
the worker for you; your org rents one, attaches it to a project, and uses it like any other
machine-user. 4PM isolates each renter's data.

## Why rent

- **No worker to run.** 4PM provides and operates the machine and its CLI.
- **On-demand.** Rent when you need capacity; release it when you don't.
- **Billed as an add-on.** A rented machine-user is a `machine_user` add-on seat on your
  subscription (see [Plans, billing & add-ons](./10-billing-and-plans.md)).

The rented worker runs on a **4PM-operated AI account**. You acknowledge a security notice when
renting, since the work runs on 4PM's account rather than your own.

## How to rent

1. In **/billing**, open the **rentable machines** list. It shows available pooled machines as
   `{ label, region }`.
2. **Filter by region** if you care where it runs, and **pick a machine**.
3. Confirm — this buys **1 unit of the machine-user add-on** bound to that machine. Once it
   activates, the machine-user is **bound to your org**.

If the exact machine you picked was just taken, 4PM tops you up from any available one so you're
never charged for nothing. If the pool is genuinely empty, renting fails with a "no slot
available" message and you aren't charged.

## Using a rented machine-user

- It appears in your **org's users list**, badged **Rented**, and under **Your rented machines**
  in /billing.
- Attach it to a project and use it exactly like your own machine-user — dispatch AI, Git, etc.
- **AI usage meters to your org** and counts against your quota, same as any machine-user.
- Its user detail view is read-only and rental-scoped: **Info · Usage · Console · Logs · History**.

## Isolation & privacy

4PM isolates rented machine-users between renters. The rented user isn't owned by any customer
org, and its per-renter data is never cross-exposed. When a rental ends, the worker workspace is
**scrubbed** — the next renter sees **none** of your code, usage, console, logs or history.

## Releasing a rental

- Reducing or cancelling the add-on (or a payment lapse) releases the seat **at the end of the
  period**.
- On release, the machine-user is detached from your project and its workspace is scrubbed; the
  machine returns to the pool as available.
- Your **rental history** in /billing keeps a read-only record of which machine you rented and for
  how long (never the scrubbed worker data). Usage and invoices for the rented period are retained
  under your org.

See also: [Rented machines FAQ](../faq/rented-machines.md).
