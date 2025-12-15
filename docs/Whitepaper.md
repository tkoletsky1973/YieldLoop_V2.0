# YieldLoop V2.0

**Title:** YieldLoop V2.0  
**Version:** v2.0  
**Date:** December 14, 2025  
**Author:** Todd Koletsky  
**Contact:** founder@yieldloop.io


## Table of Contents

1. Abstract  
2. Problem Statement  
3. What YieldLoop Solves  

4. Overview  
5. Design Principles  
6. System Architecture  
7. Non-Custodial Vault Model  

8. Yield & Trading Engines  
9. Engine Configuration, Controls & AI Operation  

10. Cycle-Based Execution Model  
11. Profit Verification & Settlement Logic  
12. LOOP Token Mechanics  

13. Fee Structure & Allocation  
14. Floor Reinforcement & Liquidity Design  

15. User Flow & UX States  
16. Gas Fees & Cost Responsibility  
17. Withdrawals, Compounding & Account Closure  

18. Emergency Controls & Fail-Safe Logic  
19. Security, Auditing & Risk Disclosures  
20. Governance, Admin Controls & Limitations  
21. Regulatory & Classification Posture  

22. Limitations & Known Constraints  
23. Future Extensions (Non-Canonical)  
24. Glossary


## 1. Abstract

YieldLoop is a non-custodial, cycle-based yield settlement protocol designed to execute trading and yield strategies, verify real profit, and convert verified surplus into a fully backed internal settlement token.

Unlike traditional DeFi platforms that rely on projected APYs, emissions, or continuously updating balances, YieldLoop operates in fixed calendar-month cycles. Each cycle produces only one of two outcomes: verified profit or zero profit. Profit is recognized only if the ending value of a user’s vault exceeds its starting value after all execution costs, fees, and slippage are accounted for.

When profit exists, it is settled at the end of the cycle and distributed to users in the form of LOOP, a platform-native settlement token that is minted only after profit is verified and is immediately redeemable for underlying value. When no profit exists, no rewards are issued and no performance fees are taken.

YieldLoop is designed to be transparent, auditable, and resistant to misleading yield representations, while reinforcing long-term protocol value through a permanently rising redemption floor.

---

## 2. Problem Statement

Most yield-generating platforms in decentralized finance do not clearly distinguish between projected returns and realized profit. Users are frequently shown estimated APYs, reward emissions, or gross returns that fail to account for volatility, slippage, drawdowns, execution costs, or adverse market conditions.

As a result:
- Users cannot easily determine whether real surplus was created
- Losses may be obscured by token emissions or accounting conventions
- Performance comparisons across strategies and platforms are unreliable
- Incentives favor activity and volume rather than verified outcomes

Additionally, many platforms rely on pooled custody, continuous withdrawal access, or discretionary control over funds, creating systemic risk, unclear accountability, and exposure to bank-run dynamics.

YieldLoop is built to address these issues directly by enforcing strict accounting boundaries, eliminating mid-cycle exits, and recognizing profit only when it can be objectively verified on-chain.

---

## 3. What YieldLoop Solves

YieldLoop introduces a disciplined alternative to assumption-based yield systems by enforcing the following guarantees:

- Profit is recognized only after a fixed execution period completes
- Profit is measured net of all costs and fees
- Losses are not masked or socialized
- Rewards are not emitted without surplus
- Users retain non-custodial ownership of funds at all times

By using fixed calendar-month cycles, YieldLoop creates deterministic accounting windows that allow strategies to operate without interference while preserving clear settlement rules.

By issuing rewards exclusively through a fully backed settlement token, YieldLoop decouples user rewards from speculative emissions and aligns protocol growth with verified economic surplus.

This approach enables:
- Transparent performance reporting
- A defensible rising floor mechanism
- Reduced incentive for manipulation or short-term gaming
- A yield system that remains coherent across varying market conditions

---

## 4. Overview

YieldLoop operates through a set of non-custodial, account-segmented vaults controlled by user wallets. Each vault is configured with one or more yield or trading engines and participates in a fixed calendar-month execution cycle.

### Protocol Classification: Verified Settlement Protocol (VSP)

YieldLoop operates as a **non-custodial Verified Settlement Protocol (VSP)**.

A Verified Settlement Protocol is a category of financial infrastructure that:
- Executes user-authorized strategies within fixed accounting windows
- Enforces deterministic, cycle-based execution boundaries
- Verifies whether real economic surplus exists only after execution concludes
- Settles outcomes exclusively at defined settlement points
- Refuses to recognize or distribute profit prior to settlement finality

A VSP does not project yield, manage assets, optimize outcomes, or recognize unrealized gains. Its function is not to generate returns, but to **verify and settle outcomes with accounting integrity**.

YieldLoop’s architecture, fee model, and token mechanics are intentionally designed to operate as settlement infrastructure rather than as an investment product, trading platform, or asset management system.

At the start of a cycle, a user:
- Connects a wallet
- Configures strategies manually or selects AI-guided safe settings
- Acknowledges strategy parameters, risk, gas costs, and withdrawal constraints
- Deposits funds into a user-specific vault

Once the cycle begins, funds are locked until cycle completion. Strategies execute according to their configured parameters, and all execution costs are borne by the user.

At the end of the cycle, the protocol verifies whether real profit exists by comparing the vault’s ending value to its starting value. If profit exists, a performance fee is applied and the remaining surplus is settled to the user as LOOP. If no profit exists, the cycle closes with no rewards and no fees.

LOOP may be redeemed immediately upon claim through the platform’s redemption mechanism, which is designed to maintain excess backing at all times. Protocol-owned liquidity and floor reinforcement mechanisms ensure that the redemption floor can only remain stable or rise over time.

YieldLoop does not custody user funds, does not guarantee returns, and does not recognize profit that cannot be verified. Its sole function is to execute strategies, verify outcomes, and settle results with precision.


## 5. Design Principles

YieldLoop is built around a small set of non-negotiable design principles that govern every architectural, economic, and operational decision in the protocol. These principles exist to eliminate ambiguity, reduce systemic risk, and ensure that all reported outcomes correspond to verifiable reality.

### 5.1 Profit Must Be Verifiable

YieldLoop recognizes profit only when it can be objectively measured on-chain at the end of a completed cycle. Projected returns, estimated APYs, unrealized gains, or emissions-based incentives are not considered profit and are not used for settlement.

Each cycle produces only one of two outcomes:
- Verified profit
- Zero profit

There is no partial recognition and no discretionary adjustment.

### 5.2 Fixed Accounting Windows

All strategy execution occurs within fixed calendar-month cycles. Accounting is performed only at cycle boundaries. This prevents continuous revaluation, mid-cycle manipulation, and selective exits that distort performance reporting.

Funds are locked for the duration of the cycle to preserve accounting integrity and ensure fair, deterministic settlement.

### 5.3 Non-Custodial User Ownership

User funds are held in account-segmented smart contract vaults controlled by the user’s wallet. YieldLoop does not custody assets, does not commingle balances, and does not have the ability to seize or redirect user funds.

The protocol orchestrates execution but never takes possession of user capital.

### 5.4 No Emissions Without Surplus

YieldLoop does not mint or distribute rewards unless real surplus exists. The LOOP token is issued only after a profitable cycle closes and only in proportion to verified net profit after fees.

This prevents inflationary dilution and ensures that rewards always correspond to real economic value.

### 5.5 Capital Preservation Over Yield

In all normal and emergency conditions, the system prioritizes capital safety over yield generation. If strategies cannot operate safely or deterministically, execution halts and cycles may close flat.

Yield is optional. Capital integrity is mandatory.

### 5.6 Explicit User Authorization

All strategy parameters, AI control options, gas cost responsibility, withdrawal constraints, and risk assumptions require explicit user acknowledgment prior to deposit. YieldLoop does not operate under implied consent or hidden defaults.

Users always know what has been authorized and under what conditions.

### 5.7 Deterministic Settlement

Settlement logic is rule-based and non-discretionary. Fees, rewards, and token minting follow predefined formulas that cannot be altered mid-cycle. Administrative controls cannot override settlement outcomes.

This ensures that results are reproducible, auditable, and resistant to manipulation.

### 5.8 Floor Integrity

The system is designed so that the redemption floor of LOOP can only remain constant or increase over time. Protocol-owned liquidity, overcollateralized backing, and surplus routing mechanisms prevent floor erosion and eliminate death-spiral dynamics.

YieldLoop does not optimize for short-term upside at the expense of long-term solvency.


## 6. System Architecture

YieldLoop is composed of a modular set of smart contracts that separate fund ownership, strategy execution, cycle accounting, settlement, and safety controls. This separation is intentional and designed to minimize trust assumptions, reduce blast radius, and ensure that no single component can compromise user funds or settlement integrity.

### 6.1 Architectural Overview

At a high level, the system consists of five primary layers:

- User-Owned Vaults  
- Strategy Execution Modules  
- Cycle Controller  
- Settlement & Redemption Layer  
- Administrative & Safety Controls  

Each layer has a narrowly defined responsibility and operates under explicit constraints.

---

### 6.2 User-Owned Vaults

Each user deposit is routed into an account-segmented, non-custodial vault that is controlled by the user’s wallet. These vaults are smart contracts that hold user funds and interface with approved strategy modules.

Properties of user vaults:
- Funds are never pooled across users
- Ownership is enforced at the contract level
- The protocol cannot seize, redirect, or withdraw funds
- Vaults are cycle-aware and strategy-aware

Vaults expose only the minimum functionality required to:
- Accept deposits
- Execute authorized strategies
- Report balances at cycle boundaries
- Release funds at cycle completion or emergency exit

---

### 6.3 Strategy Execution Modules

Strategy execution logic is isolated into modular contracts that vaults may call during a cycle. These modules implement the mechanics of grid trading, yield farming, staking, or other approved strategies.

Key characteristics:
- Strategies do not custody funds
- Strategies execute only through vault authorization
- Parameters are locked at cycle start
- Strategies cannot modify settlement logic

This separation ensures that strategy complexity does not compromise fund ownership or accounting integrity.

---

### 6.4 Cycle Controller

The Cycle Controller enforces the fixed calendar-month execution model.

Responsibilities include:
- Defining cycle start and end timestamps
- Locking vault configurations at cycle start
- Preventing mid-cycle withdrawals or reconfiguration
- Triggering end-of-cycle accounting

At cycle close, the controller signals vaults to report final balances for profit verification. No discretionary adjustments are permitted.

---

### 6.5 Settlement & Redemption Layer

The settlement layer is responsible for:
- Verifying net profit or zero-profit outcomes
- Applying platform fees only when profit exists
- Minting LOOP exclusively after verified profit
- Managing the LOOP redemption mechanism

LOOP is minted against a dedicated settlement vault that holds underlying assets with excess backing. Redemption is available immediately upon claim and does not rely on secondary market liquidity.

---

### 6.6 Administrative & Safety Controls

Administrative controls are intentionally limited and protected by multisignature authorization and optional time delays.

Permitted actions include:
- Pausing strategy execution
- Halting new deposits
- Forcing vaults to unwind to base assets
- Closing cycles as flat in emergency conditions

Administrative controls cannot:
- Seize or redirect user funds
- Mint LOOP manually
- Alter settlement formulas mid-cycle

In all emergency scenarios, the system defaults to capital preservation and user withdrawal access.

---

### 6.7 Separation of Concerns

No single contract or role has unilateral control over:
- User funds
- Strategy logic
- Cycle accounting
- Reward issuance

This separation ensures that YieldLoop remains auditable, resilient to failure, and resistant to both technical and governance abuse.


## 7. Non-Custodial Vault Model

YieldLoop is built on a strictly non-custodial vault architecture. User funds are never held, pooled, or controlled by the protocol or its operators. Instead, each deposit is placed into an account-segmented smart contract vault that enforces ownership, execution rules, and withdrawal constraints at the contract level.

This model is foundational to YieldLoop’s security, legal posture, and accounting integrity.

---

### 7.1 Account-Segmented Vaults

Each user deposit creates or utilizes a dedicated vault instance that is logically and operationally isolated from all other users.

Key properties:
- One vault per user (and per deposit, if configured)
- No shared balances or pooled custody
- On-chain ownership enforced by the user’s wallet
- Vault state is independently auditable

This eliminates cross-user risk and prevents losses, errors, or exploits in one vault from affecting others.

---

### 7.2 Ownership & Control

Vault ownership remains with the user at all times.

- Only the user’s wallet can authorize deposits and final withdrawals
- The protocol cannot transfer assets out of a vault
- Administrative roles cannot assume control or override ownership

The protocol’s role is limited to orchestrating execution through pre-approved interfaces.

---

### 7.3 Vault Lifecycle

Each vault follows a deterministic lifecycle:

1. **Initialization**
   - Vault is deployed or activated
   - Strategy parameters are configured
   - User acknowledges all constraints and costs

2. **Cycle Lock**
   - At cycle start, vault parameters are frozen
   - No withdrawals or reconfiguration permitted
   - Strategies execute under locked settings

3. **Cycle Settlement**
   - Vault reports final balances
   - Profit or zero-profit is verified
   - Settlement instructions are applied

4. **Post-Cycle State**
   - User may withdraw, compound, or close the vault
   - LOOP rewards (if any) become claimable

---

### 7.4 Withdrawal Constraints

To preserve accounting integrity and prevent manipulation:

- Mid-cycle withdrawals are not permitted
- Partial withdrawals are not permitted
- Withdrawals occur only at cycle completion or during emergency system halts

These constraints are enforced by the vault contract and cannot be bypassed by users or administrators.

---

### 7.5 Emergency Behavior

In the event of an emergency halt:
- Strategy execution is paused
- Vaults are instructed to unwind to base assets
- Cycles may close early as flat (no profit, no fees)
- Users regain withdrawal access

Emergency actions cannot result in asset seizure, redistribution, or forced conversion.

---

### 7.6 Gas & Execution Costs

All gas and execution costs incurred by vault operations are the responsibility of the user.

Users explicitly acknowledge that:
- Vault execution requires on-chain transactions
- Gas costs may vary based on network conditions
- Execution costs reduce net cycle results

These costs are included implicitly in profit verification and are not reimbursed or subsidized by the protocol.

---

### 7.7 Security Implications

By enforcing non-custodial ownership, account segmentation, and immutable cycle rules, the vault model:
- Reduces systemic risk
- Prevents bank-run dynamics
- Simplifies auditing and verification
- Aligns incentives between users and the protocol

The vault is the primary security boundary of YieldLoop, and all other system components are designed to operate without breaching this boundary.


## 8. Yield & Trading Engines

YieldLoop executes capital deployment through a defined set of yield and trading engines. Each engine represents a bounded strategy class with explicit rules, constraints, and execution limits. Engines are designed to operate autonomously within a cycle while remaining fully accountable to the protocol’s verification and settlement logic.

Engines do not custody funds, do not issue rewards, and do not determine settlement outcomes. Their sole purpose is to execute authorized strategy logic on behalf of user-owned vaults during an active cycle.

All engines operate under the same non-negotiable constraints:
- Parameters are fixed at cycle start
- Execution occurs only through user vault authorization
- Results are evaluated only at cycle end
- No engine may override cycle, fee, or settlement rules

---

### 8.1 Grid Trading Engines

Grid trading engines deploy capital across predefined price intervals, placing buy and sell orders around a reference price to capture volatility within a bounded range.

Key characteristics:
- Operate on major liquid assets (e.g., BTC, ETH, SOL, XRP, BNB)
- Use predefined grid spacing and position sizing
- Avoid directional leverage
- Generate returns from range-bound price movement rather than trend prediction

Risk controls include:
- Maximum capital allocation limits
- Hard bounds on price ranges
- Automatic order cancellation outside defined conditions

Grid engines are designed to reduce exposure to single-direction market risk while remaining sensitive to execution costs and slippage.

---

### 8.2 Yield Farming Engines

Yield farming engines deploy capital into selected liquidity pools or yield-bearing protocols that meet predefined liquidity, risk, and sustainability criteria.

Characteristics:
- Focus on stable or low-volatility pairs
- Avoid reliance on inflationary reward emissions
- Emphasize fee-based or interest-based yield

Yield farming engines account for:
- Impermanent loss
- Pool utilization changes
- Fee variability

All yield outcomes are measured net of impermanent loss and execution costs at cycle end.

---

### 8.3 Stablecoin Staking Engines

Stablecoin staking engines allocate capital into low-volatility strategies intended to preserve capital while generating modest yield.

These engines serve as:
- Risk anchors during volatile markets
- Capital parking mechanisms
- Baseline yield generators when other engines are constrained

Stablecoin engines prioritize solvency and liquidity over yield maximization.

---

### 8.4 PAXG Trading Engine

The PAXG trading engine provides exposure to tokenized gold as a low-correlation asset within the YieldLoop ecosystem.

Purpose:
- Reduce correlation to crypto-native volatility
- Introduce non-crypto price dynamics
- Act as a defensive allocation option

PAXG strategies operate under conservative execution rules and are subject to the same cycle-based verification and settlement constraints as all other engines.

---

### 8.5 Engine Independence & Risk Isolation

Each engine operates independently within the vault execution framework.

This ensures:
- Losses in one engine do not contaminate others
- Strategy failure does not compromise settlement logic
- Engine upgrades or removals do not affect vault ownership

Engines may be added, deprecated, or modified over time, but only through protocol upgrades and never mid-cycle.

---

### 8.6 Engine Output & Accountability

Engines do not report profit directly. They report only final asset balances back to the vault.

Profit determination occurs exclusively at the protocol level during cycle settlement. Engines cannot influence:
- Whether profit exists
- How much LOOP is minted
- How fees are applied

This separation ensures that strategy execution and profit recognition remain strictly decoupled.


## 9. Engine Configuration, Controls & Guardrail Operation

YieldLoop allows users to configure yield and trading engines either manually or through an optional guardrail configuration system. Regardless of configuration method, all strategy parameters must be explicitly authorized by the user prior to deposit and are enforced immutably for the duration of each cycle.

The configuration layer determines how engines operate, but it does not alter vault ownership, settlement rules, profit verification logic, or withdrawal constraints.

---

### 9.1 Manual Configuration

Users may manually select:
- Which strategy engines are enabled
- Capital allocation across enabled engines
- Engine-specific parameters such as allocation limits, range bounds, or execution constraints

Manual configuration requires explicit acknowledgment of:
- Strategy behavior and risk characteristics
- Gas and execution cost responsibility
- Locked-cycle constraints
- Settlement and fee mechanics

Once a cycle begins, all manual configuration settings are locked and cannot be modified until the cycle completes.

---

### 9.2 Guardrail Configuration (Rules-Based)

YieldLoop offers an optional guardrail configuration mode that assists users in selecting conservative, safety-constrained strategy parameters prior to cycle initiation.

Guardrail configuration:
- Operates only before a cycle begins
- Selects parameters exclusively from predefined, governance-approved rule sets
- Enforces conservative allocation limits and execution boundaries
- Does not predict market behavior
- Does not optimize for profit
- Does not adapt, learn, or reconfigure during an active cycle
- Does not influence settlement outcomes

Guardrail configuration exists solely to reduce configuration complexity and enforce safety boundaries. It does not exercise discretion, managerial judgment, or outcome optimization.

Users explicitly authorize guardrail configuration and retain full responsibility for participation, configuration choice, and outcomes.

---

### 9.3 User Authorization & Acknowledgment

Whether configuration is manual or guardrail-based, users must explicitly authorize:
- Selected engines and parameters
- Gas and execution cost responsibility
- Locked-cycle constraints
- Settlement and reward mechanics

Authorization occurs prior to deposit and is recorded through verifiable on-chain transactions or equivalent cryptographic signatures.

---

### 9.4 Parameter Locking & Immutability

At cycle start:
- All engine parameters are frozen
- No configuration changes are permitted
- No automated or administrative process may alter execution settings

This immutability ensures deterministic accounting, auditability, and non-discretionary settlement.

---

### 9.5 Safety Constraints & Fallback Behavior

All configurations are subject to protocol-enforced safety constraints, including:
- Maximum capital allocation limits
- Engine-specific risk boundaries
- Exposure caps

If a strategy engine cannot operate safely within its authorized parameters, execution halts for that engine and capital remains idle or reverts to base assets within the vault.

---

### 9.6 Accountability

All configuration decisions remain the responsibility of the user.

YieldLoop provides execution and settlement infrastructure only and does not assume fiduciary responsibility, advisory duty, or managerial control over user capital.


## 10. Cycle-Based Execution Model

YieldLoop operates exclusively on fixed calendar-month execution cycles. Each cycle begins at the start of a calendar month and ends at the close of the same month. All strategy execution, accounting, and settlement logic is bounded by these predefined time windows.

This model eliminates continuous revaluation, mid-cycle interference, and ambiguous profit reporting.

---

### 10.1 Cycle Initiation

A cycle begins when:
- A user has deposited funds into a vault
- All strategy configurations and acknowledgments have been completed
- The calendar cycle start timestamp is reached

Once a cycle starts:
- Vault parameters are locked
- Strategies become active
- Withdrawals are disabled

No changes may be made until the cycle concludes.

---

### 10.2 Execution Phase

During the active cycle:
- Authorized engines execute according to fixed parameters
- Execution costs and gas fees are incurred by the user
- Capital may move between assets only as permitted by engine logic

The protocol does not evaluate profit or performance during this phase. Intermediate values are informational only and have no settlement impact.

---

### 10.3 Cycle Completion

At the end of the calendar month:
- Strategy execution halts
- Vaults are instructed to report final balances
- Assets are returned to their base accounting form

No strategy may continue execution beyond the cycle boundary.

---

### 10.4 Profit Determination

Profit is determined by comparing:
- Vault value at cycle start
- Vault value at cycle end

All execution costs, gas fees, slippage, and losses are implicitly reflected in the final balance.

If the ending value exceeds the starting value, the difference is considered verified profit. If not, the cycle is recorded as zero profit.

---

### 10.5 Flat Cycles

Cycles that do not produce verified profit:
- Do not generate rewards
- Do not incur performance fees
- Close without settlement events

Flat cycles are a valid and expected outcome and do not trigger penalties or carry forward losses.

---

### 10.6 Determinism & Auditability

Because cycles are fixed and immutable:
- Results are reproducible
- Accounting is deterministic
- Audits can independently verify outcomes

This structure ensures that YieldLoop reports reality rather than projections.

---

### 10.7 Early Termination (Emergency Only)

Cycles may be terminated early only under emergency conditions defined by protocol safety controls.

In such cases:
- Strategies unwind to base assets
- Cycles close as flat
- Users regain withdrawal access
- No rewards or fees are applied


## 11. Profit Verification & Settlement Logic

YieldLoop determines profit and performs settlement exclusively at the conclusion of each calendar-month cycle. No profit is recognized, recorded, or distributed at any other time. This section defines the exact rules used to verify outcomes and settle results.

---

### 11.1 Starting and Ending Values

For each user vault, the protocol records:
- The vault’s total value at the start of the cycle
- The vault’s total value at the end of the cycle

Values are measured using on-chain balances of the assets held by the vault, converted to a common accounting unit where necessary.

All strategy execution, slippage, gas fees, and losses are implicitly reflected in the ending value.

---

### 11.2 Verified Profit Determination

A cycle produces **verified profit** if and only if:

Ending Value > Starting Value

The difference between the two values constitutes the gross profit for the cycle.

If the ending value is equal to or less than the starting value, the cycle is recorded as **zero profit**.

There is no partial recognition and no carry-forward of losses.

---

### 11.3 Fee Applicability

Performance fees are applied **only** when verified profit exists.

- If gross profit is zero, no fees are charged
- If gross profit is positive, the platform fee is calculated as a fixed percentage of gross profit

Fees are never charged against principal and are never charged during flat cycles.

---

### 11.4 Net Profit Calculation

When verified profit exists, the protocol calculates net profit as:

Net Profit = Gross Profit – Platform Fees

Only net profit is eligible for settlement and reward issuance.

---

### 11.5 Settlement Timing

Settlement occurs immediately after cycle close and profit verification.

At settlement:
- Platform fees are routed to their designated destinations
- Net profit is converted into settlement value
- LOOP is minted corresponding to net profit

No settlement actions occur prior to cycle completion.

---

### 11.6 LOOP Issuance Trigger

LOOP is minted only when all of the following conditions are met:
- The cycle has completed
- Verified profit exists
- Platform fees have been applied

If any condition is not met, no LOOP is minted.

There is no discretionary minting and no manual override.

---

### 11.7 Flat Cycle Handling

In a flat cycle:
- No LOOP is minted
- No fees are charged
- Vault balances remain unchanged except for execution costs already incurred

Flat cycles do not affect future cycles and do not create negative balances or obligations.

---

### 11.8 Determinism & Reproducibility

Profit verification and settlement logic is deterministic and rule-based.

Given the same starting balances, ending balances, and fee parameters, any independent observer can reproduce the same settlement outcome.

This property is critical to YieldLoop’s auditability and transparency.

---

### 11.9 Separation of Execution and Settlement

Strategy execution and settlement are intentionally decoupled.

Engines:
- Execute trades and yield strategies
- Report final balances

The protocol:
- Determines profit
- Applies fees
- Issues LOOP

No engine has influence over settlement outcomes.


## 12. LOOP Token Mechanics

LOOP is the internal settlement token of the YieldLoop protocol. It is designed to represent verified net surplus generated during completed cycles and functions as a redeemable accounting instrument rather than a speculative reward or emissions-based token.

LOOP exists solely to settle verified outcomes and reinforce protocol solvency.

---

### 12.1 Purpose of LOOP

LOOP serves three primary purposes:
- Represent net verified profit generated by user vaults
- Enable immediate, deterministic settlement at cycle end
- Support a permanently rising redemption floor through protocol-owned liquidity

LOOP is not issued in advance, does not accrue yield on its own, and does not confer governance rights.

---

### 12.2 Minting Conditions

LOOP is minted only under the following conditions:
- A cycle has completed
- Verified net profit exists after fees
- Settlement logic has been executed

LOOP minting is proportional to net profit and occurs only once per cycle.

There is no pre-minting, no emissions schedule, and no discretionary issuance.

---

### 12.3 Backing & Overcollateralization

Each unit of LOOP is backed by underlying assets held within the protocol’s settlement and redemption infrastructure.

Key properties:
- Backing value is at least equal to outstanding LOOP supply
- Excess backing is maintained at all times
- Backing assets are derived from realized surplus

This design ensures that LOOP remains fully redeemable under all normal operating conditions.

---

### 12.4 Redemption Mechanics

LOOP may be redeemed immediately upon claim.

Redemption process:
- User submits LOOP for redemption
- LOOP is burned
- Underlying value is released from the redemption vault

Redemption does not rely on secondary market liquidity and does not require waiting periods.

---

### 12.5 Floor Integrity

The LOOP redemption floor reflects the amount of underlying backing held by the protocol at the time of redemption.

The redemption floor is designed to be non-decreasing under normal operating conditions, subject to smart contract risk, systemic failure, or external infrastructure disruption.

YieldLoop does not guarantee redemption outcomes under all circumstances and does not intervene in secondary markets to influence price behavior. Redemption availability is a settlement mechanism based on existing backing and does not constitute a price guarantee, yield promise, or market support activity.

Any increase in the redemption floor results solely from realized surplus that has already been generated, verified, and settled according to protocol rules.

---

### 12.5.1 Floor Interpretation Limitation

The LOOP redemption floor is an accounting representation of available backing at the time of redemption and is not a promise, target, or guarantee of future value.

References to a non-decreasing floor reflect settlement discipline and surplus accounting mechanics only. They do not imply that the protocol engineers appreciation, targets price outcomes, or ensures economic gain.

The redemption floor:
- Is not managed to increase in value
- Does not represent expected profit
- Does not constitute a yield promise or investment return
- May remain static for extended periods
- Is subject to smart contract risk, execution failure, market conditions, and external system disruption

Any perception of value increase results solely from independently realized surplus that has already occurred and been fully settled. No value is projected, implied, or assumed prior to settlement finality.

---
### 12.6 Transferability & Scope

LOOP is minted and redeemed exclusively through the YieldLoop platform.

Transferability, if enabled, does not affect:
- Backing integrity
- Redemption rights
- Settlement rules

LOOP is not required to be freely tradable to fulfill its function.

---

### 12.7 Risk Considerations

LOOP does not guarantee profit and does not represent a claim on future cycles.

It represents only:
- Verified surplus from completed cycles
- Backing that already exists

If no profit is generated, no LOOP is issued.

---

### 12.8 Accounting Role

Within YieldLoop, LOOP functions as:
- A settlement receipt
- A proof of realized surplus
- A mechanism to separate execution from distribution

LOOP does not participate in strategy execution and does not influence trading behavior.

---

### 12.9 Supply Characteristics

LOOP supply:
- Expands only through profitable cycles
- Contracts through redemption
- Is directly linked to realized economic activity

There is no fixed maximum supply and no inflation outside of verified surplus generation.


## 13. Fee Structure & Allocation

YieldLoop applies a performance-based fee model designed to align protocol revenue with verified economic surplus while avoiding fees on losses, idle capital, or unrealized outcomes.

Fees are applied deterministically, disclosed in advance, and enforced exclusively through protocol logic. There are no discretionary charges.

---

### 13.1 Platform Performance Fee

The platform performance fee is set at **20% of verified gross profit**.

The performance fee:
- Applies **only** when verified profit exists
- Is calculated **after** all execution costs, gas fees, slippage, and losses are reflected
- Is **never** charged on principal
- Is **never** charged during flat or losing cycles
- Is applied **only at cycle completion**, never mid-cycle

If a cycle produces zero verified profit, the performance fee is zero.

---

### 13.2 Fee Calculation Method

When a cycle completes with verified profit, the protocol calculates:

- **Gross Profit**  
  Ending Vault Value − Starting Vault Value

- **Platform Fee**  
  20% × Gross Profit

- **Net Profit**  
  Gross Profit − Platform Fee

Only net profit is eligible for settlement and LOOP issuance.

All calculations are deterministic and reproducible from on-chain data.

---

### 13.3 Fee Timing & Settlement

Fees are applied **only after**:
- The cycle has fully completed
- All strategy execution has halted
- Final vault balances have been reported
- Verified profit has been objectively determined

No fees are assessed prior to settlement, and no fees are charged retroactively.

---

### 13.4 Fee Scope & Limitations

YieldLoop does not charge:
- Management fees
- Deposit fees
- Withdrawal fees
- Fees on idle or unallocated capital
- Fees on losses or unrealized gains

The protocol earns revenue solely from performance fees applied to verified profit.

---

### 13.5 Fee Purpose & Disclosure

The performance fee compensates the protocol for:
- Strategy execution infrastructure
- Cycle-based accounting and verification
- Settlement and redemption mechanisms
- Ongoing maintenance of non-custodial protocol systems

The performance fee does **not**:
- Guarantee profit
- Imply expected returns
- Create fiduciary responsibility
- Represent discretionary asset management

All fee parameters are disclosed prior to participation and are acknowledged explicitly by users before deposit.

---

### 13.6 Fee Transparency & Auditability

All fee calculations:
- Are executed through deterministic smart contract logic
- Are observable on-chain
- Can be independently verified by third parties

No hidden fees, adjustments, or discretionary overrides exist.

---

### 13.7 Design Rationale

YieldLoop intentionally employs a performance-only fee model to:
- Align protocol incentives with user outcomes
- Avoid charging users during unfavorable market conditions
- Preserve transparency and trust
- Prevent fee extraction unrelated to verified surplus

This structure prioritizes long-term protocol sustainability without obscuring risk or inflating reported performance.


## 14. Floor Reinforcement & Liquidity Design

YieldLoop includes structural mechanisms intended to reinforce the availability of LOOP redemption backing over time without introducing discretionary control, price targeting, or market intervention.

These mechanisms operate only through deterministic, rule-based processes and apply exclusively to protocol-owned assets. They do not guarantee market price behavior, future value, or redemption outcomes under all conditions.

Floor reinforcement reflects settlement discipline and surplus routing, not price support or financial guarantees.

---

### 14A. Overcollateralization Management

### 14A.0 Settlement Priority and Redeployment Constraint

Under no circumstances may overcollateralization management or system-level redeployment occur unless all user settlement obligations and minimum LOOP redemption backing requirements are fully satisfied.

Specifically:
- User principal and user profit are settled in full prior to any redeployment activity
- Assets required to satisfy all outstanding LOOP redemption rights are preserved at all times
- Redeployment applies exclusively to protocol-owned assets in excess of required settlement and redemption thresholds

Overcollateralization redeployment is a post-settlement, system-level capital efficiency mechanism and does not involve user funds, user rewards, or assets required to satisfy redemption guarantees.

### 14A.0.1 Redeployment Exposure Limits and Controls

Any system-level redeployment of overcollateralization is subject to explicit exposure limits and safety controls.

Redeployment constraints include:
- Redeployment may apply only to protocol-owned assets in excess of all user settlement and LOOP redemption backing requirements
- Redeployment exposure is capped at a fixed maximum percentage of excess backing, as defined by governance parameters
- Redeployment may be fully disabled by governance without affecting user settlement or redemption rights
- No redeployment may occur during an active execution cycle
- No redeployment may increase leverage or introduce cross-collateral dependencies

Redeployment logic is deterministic and subject to audit. Its purpose is limited to operational efficiency and capital preservation, not profit maximization.

Failure or underperformance of redeployed assets does not impair user principal, user settlement outcomes, or minimum redemption backing.

### 14A.1 Purpose

The purpose of overcollateralization management is to:
- Prevent excessive accumulation of idle capital
- Maintain efficient use of verified surplus
- Reinforce long-term protocol sustainability
- Avoid future discretionary interventions

This mechanism is preventive and structural, not reactive.

---

### 14A.2 Excess Backing Definition

Excess backing is defined as backing value held beyond the protocol’s predefined safety thresholds relative to:
- Outstanding LOOP supply
- Active system value
- Redemption demand assumptions

Thresholds are comparative and rule-based rather than fixed numerical values.

---

### 14A.3 Redeployment Mechanism

When excess backing thresholds are exceeded, the protocol may automatically redeploy a portion of excess backing into protocol-owned system deposits.

Key constraints:
- Redeployed assets remain fully protocol-owned
- Assets are not distributed to users
- Assets are not withdrawn from the ecosystem
- Assets are deployed only into conservative, bounded strategies

Redeployment does not reduce redemption guarantees below required safety margins.

---

### 14A.4 Relationship to Floor Integrity

Overcollateralization management does not reduce the redemption floor.

Instead:
- Minimum backing requirements are preserved
- Excess above required backing is made productive
- Future surplus generated by system deposits contributes back to floor reinforcement through fee routing

The redemption floor remains stable or increasing at all times.

---

### 14A.5 Governance & Automation

Overcollateralization management is executed:
- Automatically based on predefined rules, or
- Through governance-approved parameters applied only between cycles

No redeployment may occur mid-cycle, and no discretionary withdrawals are permitted.

---

### 14A.6 Risk Controls

If system deposits cannot be executed safely:
- Excess backing remains idle
- No forced redeployment occurs
- Capital preservation takes priority over yield

This ensures that overcollateralization management never introduces new systemic risk.


## 15. User Flow & UX States

YieldLoop is designed to present a clear, deterministic user experience that mirrors the protocol’s underlying execution and settlement logic. User actions are constrained to defined states to prevent ambiguity, accidental misuse, or misinterpretation of results.

The user interface reflects system state rather than attempting to smooth or abstract it.

---

### 15.1 Wallet Connection

The user begins by connecting a supported wallet to the YieldLoop interface.

At this stage:
- No funds are committed
- No strategies are authorized
- No execution occurs

The interface displays current cycle timing, supported engines, and system status.

---

### 15.2 Strategy Selection & Configuration

The user is presented with available yield and trading engines and may either:
- Configure engines manually, or
- Select AI-guided safe configuration

For each selection, the interface displays:
- Strategy behavior summary
- Risk characteristics
- Execution constraints
- Gas cost responsibility
- Locked-cycle disclosure

No configuration proceeds without explicit acknowledgment.

---

### 15.3 Authorization & Acknowledgments

Before deposit, the user must explicitly authorize:
- Selected engines and parameters
- AI control (if applicable)
- Gas and execution costs
- No mid-cycle withdrawals
- Settlement and fee mechanics

Authorizations are confirmed through wallet signatures or equivalent verifiable actions.

---

### 15.4 Deposit & Vault Activation

Once authorized, the user deposits funds into a user-specific, non-custodial vault.

Upon deposit:
- The vault is activated
- Funds remain idle until the next cycle begins
- Vault state is visible on-chain

---

### 15.5 Active Cycle State

During an active cycle:
- Strategies execute autonomously
- Vault parameters remain locked
- Withdrawals and reconfiguration are disabled

The interface may display informational metrics, but these do not affect settlement.

---

### 15.6 Cycle Completion & Settlement

At cycle end:
- Execution halts
- Profit is verified
- Fees are applied if profit exists
- LOOP is minted for net profit

The user is notified of settlement results.

---

### 15.7 Post-Cycle Options

After settlement, the user may choose to:
- Withdraw all funds
- Compound funds into the next cycle
- Split between withdrawal and compounding
- Redeem LOOP immediately

These options are available only between cycles.

---

### 15.8 Account Closure

A user may request full account closure through the defined support channel.

Account closure:
- Occurs only at cycle end
- Settles all balances
- Applies applicable fees
- Deactivates the vault

No partial closures are permitted.

---

### 15.9 State Transparency

At all times, the interface reflects:
- Current cycle state
- Vault status
- Pending actions
- Available user options

States are explicit and mutually exclusive to prevent confusion or misinterpretation.


## 16. Gas Fees & Cost Responsibility

YieldLoop is a non-custodial protocol that executes strategies through on-chain transactions. As such, all gas and execution costs incurred during vault operation are the responsibility of the user. The protocol does not subsidize, smooth, or obscure these costs.

Gas cost responsibility is explicit, acknowledged, and enforced by design.

---

### 16.1 User-Paid Gas Model

All on-chain actions required to operate a user vault—including deposits, strategy execution, settlement, redemption, and withdrawals—consume network gas.

Under YieldLoop:
- Gas fees are paid by the user
- Fees are charged at prevailing network rates
- Costs vary based on network conditions and strategy activity

Gas fees are not pooled, reimbursed, or offset by the protocol.

---

### 16.2 Acknowledgment Requirement

Before depositing funds, users must explicitly acknowledge that:
- Vault execution requires on-chain transactions
- Gas fees are unpredictable and variable
- Gas costs reduce net cycle outcomes
- Gas costs may exceed expectations during periods of network congestion

This acknowledgment is required regardless of whether strategies are manually configured or AI-guided.

---

### 16.3 Gas During Active Cycles

During an active cycle:
- Strategy modules may execute multiple transactions
- Execution frequency depends on strategy parameters and market conditions
- Gas costs are incurred as execution occurs

Intermediate gas usage is not refunded or deferred and is reflected implicitly in final cycle results.

---

### 16.4 Gas at Settlement and Redemption

Additional gas costs may be incurred at:
- Cycle settlement
- LOOP minting
- LOOP redemption
- Withdrawals or compounding actions

These costs are borne by the user initiating the action.

---

### 16.5 No Gas Optimization Guarantees

While the protocol may attempt to use efficient execution patterns, YieldLoop does not guarantee:
- Minimum gas usage
- Predictable gas costs
- Cost neutrality across strategies

Gas optimization does not override safety, correctness, or verification requirements.

---

### 16.6 Impact on Profit Verification

Gas costs are treated as real economic costs.

As a result:
- High gas usage may reduce or eliminate profit
- Cycles may close as flat due to execution costs alone
- No adjustments are made to compensate for gas expenditure

This ensures that profit verification reflects net reality rather than theoretical returns.

---

### 16.7 Transparency

Users may independently inspect:
- On-chain transactions
- Gas usage
- Execution frequency

YieldLoop does not abstract or conceal gas consumption and does not represent gas-adjusted profit as gross yield.

---

### 16.8 Design Rationale

Requiring users to bear gas costs:
- Preserves non-custodial integrity
- Avoids hidden fees or cross-subsidization
- Ensures honest accounting
- Aligns execution decisions with economic reality

Gas is treated as a first-class constraint, not an afterthought.


## 17. Withdrawals, Compounding & Account Closure

YieldLoop enforces strict withdrawal and compounding rules to preserve accounting integrity, prevent manipulation, and ensure deterministic settlement. User actions related to fund movement are permitted only at defined points in the cycle lifecycle.

There are no discretionary or mid-cycle exit paths.

---

### 17.1 No Mid-Cycle Withdrawals

Once a cycle has begun:
- Funds are locked
- Withdrawals are disabled
- Partial exits are not permitted

This rule applies universally and cannot be overridden by users, AI systems, or administrators.

The absence of mid-cycle withdrawals ensures:
- Fair accounting
- Non-manipulable performance reporting
- Consistent execution conditions for all vaults

---

### 17.2 Post-Cycle Withdrawal Options

After a cycle has completed and settlement has occurred, users may choose from the following options:

- **Withdraw All**  
  Withdraw full principal and redeem or retain any LOOP issued.

- **Compound All**  
  Roll full principal and any compounded value into the next cycle.

- **Split (50/50)**  
  Withdraw a portion of funds while compounding the remainder into the next cycle.

These options are available only during the post-cycle window before the next cycle begins.

---

### 17.3 LOOP Handling During Withdrawal

When a profitable cycle completes:
- Net profit is issued as LOOP
- LOOP may be redeemed immediately or retained

Withdrawal of principal is independent of LOOP redemption. LOOP does not automatically convert unless the user initiates redemption.

---

### 17.4 Account Closure Requests

Users may request full account closure at any time during an active cycle; however, closure is executed only at the end of the current cycle.

Account closure:
- Settles all vault balances
- Applies performance fees to any rewards
- Deactivates the vault permanently

Closure requests must be submitted through the defined support channel and are processed deterministically at cycle end.

---

### 17.5 Emergency Withdrawal Exception

In the event of a system-wide emergency halt:
- Strategies unwind to base assets
- Cycles may close early as flat
- Users regain withdrawal access

Emergency withdrawals do not include rewards and do not trigger performance fees.

---

### 17.6 Compounding Mechanics

Compounding occurs only at cycle boundaries.

When compounding is selected:
- Principal and selected balances are retained in the vault
- Vault configuration persists into the next cycle unless changed
- New cycle execution begins under locked parameters

Compounding does not bypass verification or settlement rules.

---

### 17.7 Timing & User Responsibility

Users are responsible for:
- Selecting withdrawal or compounding options within the available window
- Initiating withdrawals or redemptions
- Understanding that inactivity may default to compounding or rollover behavior as defined by the interface

YieldLoop does not auto-withdraw or auto-close vaults without user instruction except under emergency conditions.

---

### 17.8 Design Rationale

Restricting withdrawals and compounding to cycle boundaries:
- Preserves deterministic accounting
- Eliminates strategic exit timing advantages
- Prevents griefing and gas abuse
- Aligns with proof-based profit recognition

These rules are foundational to YieldLoop’s integrity and cannot be relaxed without undermining the protocol’s core guarantees.

  
## 18. Emergency Controls & Fail-Safe Logic

YieldLoop includes a limited set of emergency controls designed solely to protect user capital and preserve settlement integrity under adverse conditions. These controls are defensive in nature and do not grant discretionary authority over user funds, rewards, or protocol economics.

Emergency controls exist to stop harm, not to manage outcomes.

---

### 18.1 Purpose of Emergency Controls

Emergency controls may be activated only to address situations such as:
- Critical smart contract vulnerabilities
- Severe market dislocations affecting execution safety
- Oracle or infrastructure failures
- External dependencies behaving unpredictably

They are not intended for routine management or optimization.

---

### 18.2 Authorized Emergency Actions

When activated, emergency controls may allow the protocol to:
- Pause strategy execution across affected vaults
- Halt new deposits
- Prevent new cycle initiation
- Instruct vaults to unwind positions to base assets
- Close active cycles early as flat

These actions are limited to preserving capital and system integrity.

---

### 18.3 Prohibited Actions

Under no circumstances may emergency controls be used to:
- Seize or redirect user funds
- Transfer assets out of user vaults
- Mint LOOP manually
- Modify settlement formulas
- Alter fee structures mid-cycle

Emergency authority does not supersede non-custodial ownership.

---

### 18.4 Emergency Cycle Closure

If a cycle is terminated early due to an emergency:
- All strategies are halted
- Positions are unwound to base assets where possible
- The cycle is closed as zero profit
- No rewards are issued
- No performance fees are charged

Users regain withdrawal access immediately following emergency settlement.

---

### 18.5 Administrative Safeguards

Emergency controls are protected by:
- Multisignature authorization
- Optional time delays where feasible
- Scope-limited permissions

No single actor may unilaterally trigger or execute emergency actions.

---

### 18.6 Transparency & Disclosure

All emergency actions:
- Are recorded on-chain
- Are publicly observable
- Include clear system status indicators in the user interface

Users are notified when emergency states are entered or exited.

---

### 18.7 Fail-Safe Defaults

In any ambiguous or failure condition, the system defaults to:
- Halting execution
- Preserving capital
- Allowing user withdrawal

YieldLoop prioritizes solvency and user access over yield generation in all failure scenarios.

---

### 18.8 Recovery & Resumption

Following resolution of an emergency:
- Execution may resume only after verification of safety
- New cycles may be initiated under normal rules
- No retroactive settlement or reward issuance occurs

Recovery procedures are conservative by design and favor stability over speed.

---

### 18.9 Design Rationale

Emergency controls are intentionally minimal to:
- Reduce governance risk
- Prevent abuse
- Preserve user trust
- Maintain auditability

YieldLoop is designed to fail safely, not gracefully.

---

### 18.10 Emergency Authority Scope and Sunset Limits

Emergency controls exist solely to preserve system integrity, prevent cascading failure, and protect user access to settlement and redemption.

Emergency authority is explicitly limited in scope:

- Emergency actions may pause execution, settlement, or deposits
- Emergency actions may not seize user assets
- Emergency actions may not reallocate user funds
- Emergency actions may not mint, burn, or modify LOOP balances
- Emergency actions may not alter user configuration parameters
- Emergency actions may not confer economic advantage to administrators or governance participants

Emergency states are temporary by design.

- Each emergency action is subject to a predefined maximum duration
- Emergency states automatically expire unless explicitly renewed through transparent governance procedures
- All emergency actions are logged and publicly auditable

When an emergency state concludes:
- Execution resumes only through standard protocol rules
- Any affected cycles default to flat closure where applicable
- User access to settlement and redemption is preserved

Emergency authority is a safety mechanism, not a control mechanism, and does not introduce discretionary asset management or custodial behavior.


## 19. Security, Auditing & Risk Disclosures

YieldLoop is designed with security, transparency, and failure containment as primary objectives. While the protocol incorporates multiple safeguards to reduce risk, it does not eliminate risk. Users remain exposed to market conditions, smart contract execution, and blockchain infrastructure.

This section outlines the security model, auditing approach, and required risk disclosures.

---

### 19.1 Security Architecture

YieldLoop’s security model is based on:
- Non-custodial, account-segmented vaults
- Separation of execution, settlement, and administration
- Immutable cycle-based accounting
- Limited, scope-constrained administrative controls

No single component or role has unilateral control over user funds or settlement outcomes.

---

### 19.2 Smart Contract Risk

All protocol functionality is implemented through smart contracts, which may contain unknown vulnerabilities or emergent behaviors.

Risks include:
- Coding errors
- Unexpected interactions between contracts
- Exploits affecting external dependencies
- Blockchain-level failures

Users acknowledge that smart contract risk cannot be fully eliminated.

---

### 19.3 Strategy & Market Risk

YieldLoop executes real trading and yield strategies that are subject to:
- Market volatility
- Liquidity changes
- Slippage
- Impermanent loss
- Adverse price movements

Cycles may close with zero profit due to market conditions alone. YieldLoop does not guarantee positive outcomes.

---

### 19.4 Gas & Infrastructure Risk

Execution depends on blockchain infrastructure, including:
- Network availability
- Transaction finality
- Fee market conditions

High gas costs, congestion, or network instability may impair execution or settlement.

---

### 19.5 Oracle & External Dependency Risk

Where applicable, YieldLoop may rely on:
- Price oracles
- External protocols
- Third-party infrastructure

Failures or inaccuracies in these dependencies may affect execution outcomes.

---

### 19.6 Auditing Practices

YieldLoop intends to:
- Subject core contracts to independent third-party audits
- Publish audit reports where feasible
- Address identified issues prior to production deployment

Audits reduce risk but do not guarantee absence of vulnerabilities.

---

### 19.7 Ongoing Monitoring

The protocol may implement:
- On-chain monitoring
- Execution alerts
- Safety checks

Monitoring is defensive and does not imply active fund management or guarantees.

---

### 19.8 User Responsibility

Users are responsible for:
- Understanding protocol mechanics
- Accepting execution and market risks
- Reviewing documentation and disclosures
- Managing their own private keys and access

YieldLoop does not act as a fiduciary or financial advisor.

---

### 19.9 No Insurance

YieldLoop does not provide insurance or loss coverage.

Losses resulting from market conditions, smart contract failures, or infrastructure issues are borne entirely by users.

---

### 19.10 Disclosure Philosophy

YieldLoop prioritizes clear disclosure over optimistic representations.

Risk is not hidden, smoothed, or abstracted. Users are expected to engage with the protocol with full awareness of potential downsides.


## 20. Governance, Admin Controls & Limitations

YieldLoop is designed to minimize governance risk by limiting discretionary control and constraining administrative authority. Governance and administrative mechanisms exist to maintain protocol safety, support upgrades, and enforce predefined rules — not to manage user outcomes or direct capital.

This section defines what governance and administrators can and cannot do.

---

### 20.1 Governance Scope

Governance authority is intentionally narrow and applies only to:
- Protocol parameter updates between cycles
- Approval of new strategy engines or deprecation of existing ones
- Adjustment of safety thresholds and limits
- Upgrade authorization for core contracts

Governance does not control user vaults, funds, or settlement outcomes.

---

### 20.2 Administrative Roles

Administrative roles are implemented through multisignature-controlled accounts with scope-limited permissions.

Administrators may:
- Trigger emergency controls as defined in Section 18
- Pause or resume protocol components
- Execute approved contract upgrades
- Manage infrastructure-related configurations

Administrators may not act unilaterally and are subject to transparency and on-chain accountability.

---

### 20.3 Explicit Limitations

Governance and administrators **cannot**:
- Seize, redirect, or withdraw user funds
- Override vault ownership
- Modify active cycle parameters
- Alter settlement formulas mid-cycle
- Mint LOOP outside verified settlement logic
- Bypass redemption guarantees

These limitations are enforced at the contract level.

---

### 20.4 Upgrade Process

Protocol upgrades:
- Are proposed and reviewed prior to execution
- Occur only between cycles
- Do not affect active vaults or settlements
- Preserve backward compatibility where possible

Users are informed of pending upgrades through public disclosures.

---

### 20.5 Parameter Changes

Governance may adjust parameters such as:
- Fee allocation destinations
- Safety thresholds
- Engine availability
- Overcollateralization management rules

Parameter changes:
- Do not apply retroactively
- Do not affect completed or active cycles
- Are transparent and auditable

---

### 20.6 No Discretionary Management

YieldLoop governance does not:
- Select trades
- Manage positions
- Adjust strategies mid-cycle
- Intervene to improve outcomes

Execution and settlement remain rule-based and deterministic.

---

### 20.7 Governance Risk Reduction

By limiting governance scope:
- Attack surface is reduced
- Abuse potential is minimized
- Predictability is preserved
- User trust is strengthened

YieldLoop prioritizes protocol rules over human discretion.

---

### 20.8 Accountability & Transparency

All governance actions:
- Are recorded on-chain
- Are publicly observable
- Are constrained by predefined permissions

There are no hidden administrative functions.

---

### 20.9 Design Rationale

YieldLoop treats governance as a maintenance function, not a control layer.

The protocol is designed to operate predictably with minimal intervention, relying on structure and verification rather than discretion.


## 21. Regulatory & Classification Posture

YieldLoop is designed to operate as a non-custodial software protocol that executes user-authorized strategies, verifies outcomes, and settles results according to deterministic rules. It does not custody user funds, does not guarantee returns, and does not issue rewards absent verified surplus.

This section describes the protocol’s intended classification posture and design intent. It does not constitute legal advice.

---

### 21.1 Non-Custodial Protocol Design

YieldLoop does not take possession of user assets.

- Funds remain in user-owned smart contract vaults
- Users authorize all strategy execution
- Administrators cannot seize or redirect assets

This structure is intended to distinguish YieldLoop from custodial platforms and managed investment accounts.

---

### 21.2 No Profit Guarantees

YieldLoop does not promise, advertise, or guarantee profit.

- Cycles may close with zero profit
- Rewards are issued only when surplus exists
- Losses are possible and disclosed

YieldLoop reports outcomes; it does not manufacture them.

---

### 21.3 LOOP Classification Intent

LOOP is designed as a **settlement and accounting token**, not an investment vehicle.

LOOP:
- Is minted only after verified profit
- Represents realized surplus, not future expectation
- Is fully backed and redeemable
- Does not confer governance rights
- Does not promise appreciation

Its purpose is to settle completed cycles, not to raise capital or incentivize speculation.

---

### 21.4 User Control & Authorization

Users retain control over:
- Whether to participate
- Which strategies are used
- Whether AI assistance is enabled
- When to deposit, compound, or withdraw (at cycle boundaries)

YieldLoop does not exercise discretionary control over user decisions.

---

### 21.5 Fee-for-Execution Model

YieldLoop earns revenue only through a predefined performance fee applied to verified profit.

- No fees are charged on losses
- No fees are charged on idle capital
- Fees are disclosed in advance

This model aligns protocol revenue with user success without guaranteeing outcomes.

---

### 21.6 No Investment Advice

YieldLoop does not provide personalized financial advice.

- Strategy descriptions are informational
- AI configuration is rules-based, not advisory
- Users remain responsible for their own decisions

The protocol provides tools, not recommendations.

---

### 21.7 Jurisdictional Variability

Regulatory treatment of digital assets and DeFi protocols varies by jurisdiction and may change over time.

Users are responsible for:
- Understanding applicable laws
- Complying with tax and reporting obligations
- Determining eligibility to use the protocol

YieldLoop does not enforce jurisdictional access controls by default.

As a U.S.-based entity, YieldLoop’s user interface may implement sanctions screening consistent with applicable Office of Foreign Assets Control (OFAC) lists and may restrict access from prohibited jurisdictions or sanctioned persons at the application layer. Such measures do not alter the non-custodial nature of the protocol or the neutrality of the underlying smart contracts.

---

### 21.8 Design Intent

YieldLoop is designed to:
- Maximize transparency
- Minimize trust assumptions
- Avoid custodial risk
- Avoid misleading yield representations

Its architecture reflects an intent to operate as infrastructure rather than as a financial intermediary.

---

### 21.9 Disclosure Philosophy

YieldLoop favors explicit disclosure over optimistic framing.

If profit cannot be verified, it is not reported.  
If risk exists, it is not hidden.

Users are expected to engage with the protocol with informed consent.

### 21.10 Regulatory Pathways and Restricted Interface Modes

YieldLoop is designed to operate as non-custodial settlement infrastructure across multiple regulatory environments.

Where required by applicable law or regulatory guidance, YieldLoop may offer restricted interface modes that limit or modify user access without altering the neutrality or determinism of the underlying protocol.

Such restricted interface modes may include, where applicable:
- Jurisdiction-based access limitations at the application layer
- Sanctions screening consistent with Office of Foreign Assets Control (OFAC) requirements
- Transaction size limits or feature restrictions
- Additional user acknowledgments or disclosures
- Optional identity verification for higher-risk or higher-value participation tiers

Restricted interface modes do not:
- Convert the protocol into a custodian
- Introduce discretionary asset management
- Alter execution, verification, or settlement mechanics
- Change the non-custodial nature of user vaults

The availability of restricted interface modes reflects compliance flexibility and does not imply that unrestricted protocol operation constitutes regulated activity in all jurisdictions.


### 21.11 Terminology Clarification

For clarity, YieldLoop uses the term “yield” descriptively to reference realized outcomes of execution, not as a promise, projection, or expectation of return.

Within this document and associated materials:
- “Yield” does not imply predicted performance, guaranteed returns, or continuous accrual
- “Profit” refers only to surplus verified after execution concludes and settlement finality is reached
- No yield, profit, or value is assumed, estimated, or recognized prior to settlement

All references to yield or profit are conditional, retrospective, and subject to execution costs, losses, and verification outcomes. Any use of yield-related terminology should be understood as descriptive of accounting results, not as marketing claims or financial assurances.


## 22. Limitations & Known Constraints

YieldLoop is intentionally designed with constraints that prioritize verification, safety, and determinism over flexibility or convenience. These limitations are not incidental; they are fundamental to the protocol’s operating model.

Users must understand and accept these constraints before participating.

---

### 22.1 No Continuous Liquidity Access

YieldLoop does not support continuous deposits and withdrawals.

- Funds are locked for the duration of each cycle
- Withdrawals occur only at cycle boundaries or during emergencies

This constraint preserves accounting integrity and prevents manipulation.

---

### 22.2 No Mid-Cycle Strategy Changes

Once a cycle begins:
- Strategy parameters are immutable
- AI systems cannot reconfigure execution
- Administrators cannot intervene

This prevents discretionary outcome management.

---

### 22.3 Flat Cycles Are Expected

Cycles may close with zero profit.

- Flat cycles are not failures
- No rewards or fees are issued during flat cycles
- Losses are not socialized or offset

This reflects real market conditions rather than smoothed performance.

---

### 22.4 Gas Cost Sensitivity

High gas costs may:
- Reduce net profit
- Eliminate profit entirely
- Make some strategies temporarily impractical

YieldLoop does not shield users from gas market dynamics.

---

### 22.5 Strategy Coverage Limits

YieldLoop supports a defined set of strategy engines.

- Not all assets or markets are supported
- Strategy expansion requires protocol upgrades
- Unsupported strategies cannot be accessed through the protocol

This constraint reduces risk and complexity.

---

### 22.6 Smart Contract Risk

Despite best practices and audits, smart contracts may fail.

- Vulnerabilities may exist
- External dependencies may behave unexpectedly
- Losses are possible

YieldLoop does not provide insurance.

---

### 22.7 No Guaranteed Availability

The protocol may:
- Pause execution
- Disable deposits
- Enter emergency states

Availability is not guaranteed under all conditions.

---

### 22.8 No Retroactive Adjustments

Settlement outcomes:
- Are final once executed
- Are not retroactively modified
- Are not compensated after the fact

This ensures deterministic accounting.

---

### 22.9 User Responsibility

Users are responsible for:
- Understanding protocol mechanics
- Evaluating risk tolerance
- Managing wallet security
- Monitoring participation windows

YieldLoop does not assume responsibility for user decision-making.

---

### 22.10 Design Tradeoffs

YieldLoop intentionally trades:
- Convenience for integrity
- Flexibility for determinism
- Hype for verifiable outcomes

These tradeoffs define the protocol’s identity.


### 22.11 Consumer Safeguards and Participation Acknowledgments

YieldLoop is designed to prioritize transparency, determinism, and informed participation.

Prior to deposit, users are explicitly informed that:
- Capital is committed for the full duration of each cycle
- No mid-cycle withdrawals or parameter changes are permitted
- Execution costs and gas fees may exceed returns
- Cycles may close with zero verified profit
- Settlement outcomes are final once verification concludes

For smaller deposits or gas-sensitive participation, the protocol interface may present additional acknowledgments to ensure users understand:
- The impact of fixed execution costs on smaller positions
- The potential for flat or negative outcomes due to market conditions or fees
- That YieldLoop does not optimize outcomes or guarantee profitability

These acknowledgments are designed to reinforce informed consent and do not alter protocol execution, settlement mechanics, or user rights.

YieldLoop does not restrict participation based on deposit size but emphasizes user understanding and responsibility for configuration choices and outcomes.


## 23. Future Extensions (Non-Canonical)

This section describes potential future extensions to YieldLoop that are not part of the canonical protocol definition. These items are illustrative and exploratory only. They do not affect the operation, guarantees, or constraints of the current system and should not be interpreted as commitments or roadmap promises.

All future extensions would require separate design review, governance approval, and implementation outside of active cycles.

---

### 23.1 Additional Strategy Engines

Future versions of YieldLoop may support additional yield or trading engines, such as:
- Expanded asset coverage
- Additional market-neutral strategies
- Cross-market or cross-venue execution
- Conservative index-style allocations

Any new engine would be subject to the same non-custodial, cycle-based, and verification constraints as existing engines.

---

### 23.2 Cross-Chain Support

YieldLoop may be extended to support multiple blockchain networks.

Cross-chain support would require:
- Chain-specific vault deployments
- Independent cycle accounting per chain
- Explicit user acknowledgment of cross-chain risk

Cross-chain execution would not merge accounting across chains without verifiable settlement guarantees.

---

### 23.3 Advanced Analytics & Reporting

Future interfaces may include:
- Enhanced performance analytics
- Cycle history visualization
- Strategy attribution reporting
- Comparative performance summaries

These features would remain informational and would not alter settlement logic.

---

### 23.4 Governance Tooling Enhancements

Governance processes may be augmented with:
- Improved proposal frameworks
- Parameter simulation tools
- Formal verification of changes

Such enhancements would focus on transparency and predictability rather than expanding discretionary control.

---

### 23.5 LOOP Utility Extensions

Potential future uses of LOOP may include:
- Internal accounting optimizations
- Fee settlement mechanisms
- Optional protocol interactions

Any extension would preserve LOOP’s role as a backed settlement instrument and would not introduce emissions or speculative incentives.

---

### 23.6 Infrastructure & Automation Improvements

Operational improvements may include:
- Improved execution efficiency
- Monitoring and alerting systems
- Automation of safety checks

These changes would not affect user ownership or settlement rules.

---

### 23.7 Explicit Non-Commitment

All items in this section are non-canonical and non-binding.

The canonical definition of YieldLoop is limited to the sections preceding this one. Future extensions do not modify or override existing guarantees unless explicitly adopted through governance and documented in an updated canonical specification.


## 24. Glossary

**Active Cycle**  
A calendar-month period during which strategies execute and funds are locked. Cycles begin on the first day of the month and end on the last day of the month.

**AI-Guided Configuration**  
A rules-based configuration option that automatically selects conservative, safety-first strategy parameters prior to cycle start. AI does not adjust parameters mid-cycle and does not influence settlement.

**Backing**  
Underlying assets held by the protocol to support LOOP redemption. Backing must meet or exceed outstanding LOOP supply at all times.

**Cycle Boundary**  
The transition point between cycles at which execution halts, profit is verified, settlement occurs, and user actions such as withdrawal or compounding are permitted.

**Emergency Halt**  
A protocol state in which execution is paused and strategies unwind to base assets due to safety concerns. Emergency halts result in flat cycle closure.

**Execution Costs**  
All costs incurred during strategy execution, including gas fees, slippage, and protocol interaction costs. Execution costs are borne by the user and reflected in final settlement.

**Flat Cycle**  
A completed cycle in which no verified profit exists. Flat cycles result in no rewards and no performance fees.

**Floor (Redemption Floor)**  
The minimum value at which LOOP can always be redeemed through the protocol’s internal redemption mechanism.

**Grid Trading Engine**  
A strategy module that places buy and sell orders across predefined price ranges to capture volatility without directional leverage.

**LOOP**  
The internal settlement token of YieldLoop, minted only after verified profit and redeemable immediately for underlying value.

**Non-Custodial**  
A property of the protocol in which user funds are never held or controlled by the protocol or administrators.

**Overcollateralization**  
The condition in which backing value exceeds outstanding LOOP supply, providing excess redemption capacity and system resilience.

**Protocol-Owned Liquidity**  
Liquidity provisioned and controlled by the protocol to support LOOP redemption and floor integrity. Users do not own or withdraw this liquidity.

**Profit Verification**  
The process of determining whether a cycle produced real surplus by comparing starting and ending vault values.

**Settlement**  
The post-cycle process of applying fees, minting LOOP (if applicable), and finalizing cycle outcomes.

**Strategy Engine**  
A modular contract that executes a specific trading or yield strategy on behalf of user vaults during an active cycle.

**User Vault**  
A non-custodial, account-segmented smart contract that holds user funds and interfaces with strategy engines.

**Withdrawal Window**  
The period between cycles during which users may withdraw funds, compound balances, or close accounts.

**Zero-Profit Cycle**  
A cycle that ends with no verified profit and therefore results in no LOOP issuance and no platform fees.


## 25. Regulatory, Risk, and Adversarial Review Disclosures

This section is provided to address foreseeable regulatory, legal, political, competitive, and consumer-protection concerns. It is intended to clarify the design intent, operating boundaries, and explicit limitations of the YieldLoop protocol. Nothing in this section modifies the canonical rules defined above.

---

### 25.1 No Managerial Reliance or Profit Expectation

YieldLoop does not promise, market, or imply profit.

- The protocol does not manage portfolios
- The protocol does not optimize outcomes
- The protocol does not intervene to improve results
- AI-guided configuration is rules-based and static per cycle

All strategy execution occurs strictly according to parameters authorized by the user prior to cycle start. Users are not relying on the discretionary efforts of YieldLoop operators, developers, or administrators to generate profit.

YieldLoop executes instructions and reports outcomes; it does not manage investments.

---

### 25.2 LOOP Is a Settlement Instrument, Not an Investment Asset

LOOP is an internal settlement and accounting token used solely to represent verified net surplus from completed cycles.

LOOP:
- Is not sold or marketed
- Is not pre-minted
- Is not emitted on a schedule
- Does not confer governance rights
- Does not represent a claim on future profits
- Does not promise appreciation

LOOP exists only after profit has already been realized and only to facilitate deterministic settlement and redemption of that surplus.

---

### 25.3 No Price Support or Market Intervention

YieldLoop does not defend, target, or manage the secondary market price of LOOP.

- The redemption floor is a settlement mechanism, not a price peg
- No intervention occurs to maintain market price above the floor
- The protocol does not engage in price stabilization activities

Market price behavior, if any, is independent of protocol guarantees.

---

### 25.4 Non-Custodial, Non-Banking Design

YieldLoop is not a bank, savings account, payment service, or custodial platform.

- User funds remain in user-owned smart contract vaults
- The protocol cannot seize or redirect assets
- There is no deposit insurance
- There are no guaranteed withdrawals outside defined rules

YieldLoop does not accept deposits in a custodial capacity and does not perform maturity transformation or credit creation.

---

### 25.5 Fee-for-Execution, Not Yield Provision

The protocol earns revenue only through a predefined performance fee applied to verified profit.

- No fees are charged during flat or losing cycles
- No fees are charged on idle capital
- No fees are charged independent of outcomes

YieldLoop is compensated for execution and settlement infrastructure, not for producing returns.

---

### 25.6 Consumer Risk Disclosure (Plain Language)

By using YieldLoop, users acknowledge that:

- Funds are locked for the duration of each cycle
- Cycles may end with zero profit
- Gas and execution costs may exceed returns
- No mid-cycle withdrawals are permitted
- LOOP may be redeemed only against existing backing
- Losses are possible and not reimbursed

Disclosure does not eliminate risk. Users are responsible for understanding and accepting these conditions.

---

### 25.7 Jurisdictional Responsibility

YieldLoop is a globally accessible protocol. Regulatory treatment of digital assets varies by jurisdiction.

Users are responsible for:
- Determining eligibility to use the protocol
- Complying with applicable laws and tax obligations
- Understanding restrictions that may apply in their jurisdiction

YieldLoop does not solicit participation from prohibited jurisdictions and does not provide legal or tax advice.

---

### 25.8 Capital Efficiency and Design Tradeoffs

YieldLoop intentionally prioritizes:
- Verifiable outcomes over projected APY
- Capital safety over yield maximization
- Determinism over flexibility

As a result:
- YieldLoop may underperform speculative strategies in bull markets
- Capital efficiency may be lower than high-risk alternatives
- Flat cycles are expected and acceptable outcomes

These tradeoffs are deliberate and central to the protocol’s design.

---

### 25.9 Overcollateralization and System Sustainability

YieldLoop may manage excess overcollateralization through rule-based redeployment into protocol-owned system deposits.

- Excess backing is never distributed to users
- Excess backing is never withdrawn from the ecosystem
- Redeployment preserves minimum redemption guarantees

This mechanism exists to prevent inefficient accumulation of idle capital while maintaining solvency and floor integrity.

---

### 25.10 What YieldLoop Is Not

YieldLoop is not:
- An investment fund
- A managed portfolio
- A savings product
- A stablecoin issuer
- A guarantee mechanism
- A substitute for financial advice

YieldLoop is execution and settlement infrastructure governed by deterministic rules.

---

### 25.11 Disclosure Philosophy

YieldLoop favors explicit disclosure over optimistic framing.

If profit cannot be verified, it is not reported.  
If risk exists, it is disclosed.  
If uncertainty remains, it is not concealed.

Participation in YieldLoop constitutes informed, voluntary use of non-custodial financial infrastructure.


# 26. Structural Clarifications, Adversarial Risk Mitigations, and Design Safeguards

This section is provided to explicitly address foreseeable regulatory, legal, political, competitive, and consumer-protection concerns that may arise from hostile or adversarial review of the YieldLoop protocol. Nothing in this section modifies, overrides, or expands the canonical rules defined elsewhere in this document. Its purpose is clarification, not redefinition.

---

## 26.1 YieldLoop Is Execution and Settlement Infrastructure, Not Asset Management

YieldLoop operates exclusively as non-custodial execution and settlement infrastructure.

The protocol:
- Executes user-authorized strategy logic
- Verifies objective outcomes at fixed cycle boundaries
- Settles results deterministically according to predefined rules

The protocol does **not**:
- Manage portfolios
- Select investments on behalf of users
- Adjust strategies during execution
- Intervene to improve outcomes
- Exercise discretionary judgment over user capital

All strategy parameters are explicitly authorized by the user prior to cycle initiation and are immutable for the duration of the cycle. Responsibility for participation, configuration choices, and risk exposure remains solely with the user.

---

## 26.2 AI-Guided Configuration Does Not Create Managerial Reliance

Any references to “AI” within YieldLoop refer strictly to **pre-cycle, rules-based configuration assistance**.

AI-guided configuration:
- Operates only before a cycle begins
- Selects parameters from predefined, governance-approved rule sets
- Does not predict markets
- Does not optimize for profit
- Does not adapt or reconfigure mid-cycle
- Does not influence settlement outcomes

AI components exist solely to reduce user configuration complexity. They do not introduce discretion, managerial control, or outcome dependency. Users explicitly authorize AI-guided configuration and retain full responsibility for its use.

---

## 26.3 Locked Cycles Exist for Accounting Integrity, Not Capital Control

Cycle-based fund locking exists exclusively to preserve deterministic accounting, prevent selective exits, and ensure verifiable profit measurement.

Locking:
- Is disclosed prior to deposit
- Is authorized explicitly by the user
- Applies uniformly to all vaults
- Cannot be altered by administrators or AI systems

Locked cycles do **not**:
- Enable discretionary fund control
- Permit protocol intervention
- Create custodial authority
- Guarantee outcomes

Funds remain in user-owned vaults at all times, subject only to the execution rules authorized by the user.

---

## 26.4 LOOP Is a Settlement Instrument, Not an Investment or Price-Supported Asset

LOOP functions solely as an internal settlement and accounting instrument representing verified net surplus from completed cycles.

LOOP:
- Is minted only after profit has already been realized
- Is fully backed by existing underlying assets
- Is redeemable immediately through deterministic settlement logic
- Does not confer governance rights
- Does not represent a claim on future profits
- Does not promise appreciation

The redemption mechanism exists to settle verified outcomes, not to support market prices. YieldLoop does not defend, target, stabilize, or intervene in secondary market pricing of LOOP.

---

## 26.5 Redemption Floor Is Accounting Infrastructure, Not a Price Guarantee

The redemption floor reflects existing backing held by the protocol at the time of redemption.

The protocol does not:
- Guarantee market value
- Support trading liquidity
- Intervene in price discovery
- Provide downside protection beyond existing backing

Redemption availability is a function of settlement finality, not a promise of future value or performance.

---

## 26.6 Overcollateralization Management Does Not Involve User Capital

Any overcollateralization management mechanisms apply **exclusively to protocol-owned assets** derived from realized fees or surplus after user settlement is complete.

The protocol never:
- Redeploys user principal
- Redeploys user profit
- Redeploys assets backing user-issued LOOP below required thresholds
- Rehypothecates user capital

User balances and settlement outcomes are finalized prior to any system-level redeployment activity. Overcollateralization management exists solely to prevent inefficient accumulation of idle protocol-owned capital while preserving redemption guarantees.

---

## 26.7 Fee Structure Reflects Execution Services, Not Outcome Promises

YieldLoop earns revenue only through a predefined performance fee applied **exclusively** to verified profit.

The protocol does not:
- Charge fees on losses
- Charge fees on idle capital
- Charge fees independent of outcomes
- Guarantee positive results

Fees compensate the protocol for execution, verification, and settlement infrastructure, not for producing returns.

---

## 26.8 Accessibility Does Not Imply Suitability or Jurisdictional Clearance

YieldLoop is a general-purpose protocol and does not assess:
- User sophistication
- Risk tolerance
- Legal eligibility
- Jurisdictional compliance

Users are solely responsible for determining whether participation is lawful and appropriate in their jurisdiction. YieldLoop does not provide legal, tax, or regulatory advice.

---

## 26.9 Exit Fees Are Operational, Not Restrictive

Any account closure or support-related fees exist solely to:
- Cover deterministic processing costs
- Prevent abusive automation
- Maintain operational integrity

Such fees are:
- Disclosed in advance
- Fixed and transparent
- Independent of performance outcomes
- Not designed to restrict access to user funds

---

## 26.10 Disclosure Supersedes Marketing

YieldLoop explicitly favors disclosure over promotion.

If profit cannot be verified, it is not reported.  
If risk exists, it is disclosed.  
If uncertainty remains, it is not concealed.

Participation in YieldLoop constitutes informed, voluntary use of non-custodial execution and settlement infrastructure operating under deterministic, verifiable rules.

---

### Design Intent Statement

YieldLoop is intentionally conservative by design. It prioritizes:
- Verifiable outcomes over projected yield
- Capital integrity over flexibility
- Determinism over discretion
- Transparency over optimization narratives

These choices are deliberate and define the protocol’s identity.
