# Rented machine-users

**What is a rented machine-user?**
A worker from 4PM's pool that you rent instead of running your own. 4PM operates the machine; you
attach it to a project and use it like any machine-user. See
[docs/11](../docs/11-rented-machines.md).

**How do I rent one?**
In **/billing**, open the **rentable machines** list, optionally filter by **region**, pick a
machine, and confirm. This buys 1 unit of the **machine-user add-on** bound to that machine.

**How is it billed?**
As a recurring **machine-user add-on** seat on your subscription (see
[docs/10](../docs/10-billing-and-plans.md)). AI usage on it meters to **your org** and counts
against your quota.

**Whose account does it run on?**
A **4PM-operated AI account**, not yours — you acknowledge a security notice when renting.

**The machine I picked was just taken.**
4PM tops you up from any available machine so you're never charged for nothing. If the pool is
genuinely empty, renting fails with a "no slot available" message and you aren't charged.

**Where does it show up?**
In your **org users list** badged **Rented**, and under **Your rented machines** in /billing. Its
detail view is read-only (Info · Usage · Console · Logs · History).

**Is my data safe from other renters?**
Yes. 4PM isolates rented machine-users between renters. When a rental ends the workspace is
**scrubbed**, so the next renter sees none of your code, usage, console, logs or history.

**How do I stop renting?**
Reduce or cancel the add-on (a payment lapse also releases it). Release happens at **period end**:
the machine detaches, its workspace is scrubbed, and it returns to the pool. Your **rental
history** keeps a read-only record of what you rented and when.
