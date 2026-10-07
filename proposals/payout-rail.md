# Payout Rail — LAB Open Source Builders Fund Proposal

## Project name

**Payout Rail**

## Builder or team

**Victor Omenai** — lead maintainer and architect. Led the extraction of the orchestration layer, built the orchestration core, and delivered the evidence chain, reconciliation layer, v1 public API, and demo. Based in Jos, Nigeria.

**McDaniells Albert** — co-maintainer. Co-developer on the CineX project until the previous grant cycle concluded. Available for adapter work and integration testing.

**Jacob Momoh** — senior advisor. Senior engineer with production experience. Provides architectural review and security review.

## Problem being solved

Stacks applications can settle programmable value on-chain, but developers serving users in emerging markets face a fragmented last-mile problem. There is no reusable orchestration layer that turns settlement into reliable local payouts. Every team that needs to pay a user in local currency rebuilds the same state machine, retries, evidence trail, and reconciliation logic from scratch.

Most users in emerging markets do not want crypto. They want local currency in their bank account. Without a reliable payout layer, Stacks applications cannot serve those users at all. That excludes the majority of the market the Bitcoin and Stacks ecosystems are trying to reach.

## Technical approach

Payout Rail is a provider-agnostic orchestration layer. It sits between a Stacks application and a local payout provider. It holds the payout lifecycle: a 15-state machine, transition guards, deterministic idempotency, a compare-and-swap concurrency guard, provider adapters, webhook verification, a five-mode reconciliation layer, an audit-grade evidence chain, and a versioned v1 public API.

The orchestration core does not contain provider-specific logic. Each provider sits behind an adapter interface. Two adapters exist: **Yellow Card** (NGN bank and mobile money payouts) and **Flutterwave** (stablecoin transfers, pending F4B production approval). A third adapter (**xReserve**) observes on-chain release.

The layer is MIT-licensed, self-hostable, and built in Node.js with no runtime dependencies beyond what is already in the repository. The test suite has **243 tests with 0 failures**.

## Repository link

https://github.com/OmenaiVIC/payout-rail

## Milestones

### Milestone 1 — Provider onboarding and sandbox validation

**Objective:** Complete provider onboarding for Yellow Card and Flutterwave, and validate the Nigeria/NGN payout corridor in sandbox if access is granted.

**Deliverables:**
- Yellow Card onboarding: introductory call, pre-integration form, KYB documentation, AML review, legal agreement
- Flutterwave F4B KYC 
- If sandbox access is granted: end-to-end USDCx-to-NGN payout with webhook verification evidence and a settlement receipt with zero gaps
- If sandbox access is not granted: documented blocker report with the correct integration boundary in place, marked as pending external verification

**Repository progress:** The adapter interfaces, the orchestration core, the evidence chain, and the reconciliation layer are already committed. This milestone adds the real provider integration and the sandbox evidence.

**Documentation status:** `docs/PROVIDER_ADAPTERS.md` documents the adapter interface. `docs/flutterwave-api-reference.md` documents the Flutterwave wire model. The milestone report will document the onboarding outcomes.

**Demo or testing status:** The offline demo (`npm run demo:payout:ngn`) runs end-to-end with mocked adapters. This milestone adds sandbox evidence if access is granted.

**Target:** 6 weeks, with the understanding that provider timelines may extend it.

### Milestone 2 — Public SDK and external integration

**Objective:** Publish the public SDK and integration guide, ship the external integrator example, and conduct external developer testing.

**Deliverables:**
- Public SDK or integration package
- Integration guide
- External integrator example
- External developer testing with written feedback
- Release candidate with security posture, architecture documentation, and maturity statement

**Repository progress:** The v1 public API and the example client are already committed. This milestone packages them as a distributable SDK and adds the integration guide.

**Documentation status:** `docs/INTEGRATION.md` documents the v1 API. The SDK will include its own reference documentation.

**Demo or testing status:** External developer testing will be conducted through Zero Authority bounties and other outlets as facilitated by LAB. Written feedback will be incorporated into the release candidate.

**Target:** 4 weeks.

## Funding requested

**$5,000**

## Ecosystem relevance

Payout Rail serves the Bitcoin and Stacks ecosystems by completing the last mile. Most infrastructure in the ecosystem moves value *into* Bitcoin or Stacks. Payout Rail moves value *out* to where real people receive it — local currency in a bank account.

This matters because it makes Stacks applications complete. A marketplace, a DAO, a creator platform cannot currently pay users in local currency without building their own orchestration. With Payout Rail, they can. That expands what Stacks applications can be built for, who they can serve, and how much real economic activity flows through the network.

It also demonstrates that Bitcoin-settled value can reach real people in real economies — not just crypto-native users. That is the difference between infrastructure that serves a niche and infrastructure that serves a market.

## Status

- [x] Proposal submitted
- [ ] Under review
- [ ] Approved
- [ ] In progress
- [ ] Completed
