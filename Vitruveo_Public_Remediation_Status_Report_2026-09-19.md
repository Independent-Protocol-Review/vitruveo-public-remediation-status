# Vitruveo Public Remediation Status Report

**Follow-up date:** September 19, 2026  
**Scope:** Vitruveo protocol, Scope/bridge, public release engineering, governance/control disclosures, Pretrend/TrendPlay, and public explorer condition  
**Method:** Public-source follow-up. No unauthorized access, exploitation, asset movement, or destructive testing was performed.

## Executive conclusion

The July 15, 2026 public-source protocol review and the July 26, 2026 Scope/bridge supplement remain materially unresolved in the public record.

The most important fact is unchanged: the public `Vitruveo/vitruveo-protocol` repository is still at commit `ba0ef28d9844b84cd114b638b541c241af33e345`, dated January 25, 2026 - the same commit reviewed in July. The repository still has no GitHub releases. Because the reviewed protocol source has not moved, none of the protocol findings that depended on that source can be considered remediated by a later public protocol patch.

Scope has had limited product maintenance since the July supplement, with its latest public commit dated August 7, 2026. That update added gas funding for empty destination wallets during bridge claims. It did not add wallet-signed authorization to the notarization route. The current public route still accepts an `account`, `sourceChainId`, and token selection; uses server-held notary keys; reads the supplied account's escrow; signs a destination receipt; and clears the source escrow. On public-source evidence, SCOPE-01 remains open unless a materially different production service is privately deployed and independently demonstrated.

Several Scope data/disclosure findings also remain visible in current public source: tokenomics still hard-codes `500_000_000` as total supply, still consumes the first `api/v2/addresses` response without visible pagination, Reflect still sends 1 VTRU to the VIBE address to cause explorer indexing, and the public contract page remains far short of the complete deployment/role registry requested in the July supplement.

There is still no public finding-by-finding remediation docket linking the reported issues to owners, patches, regression tests, deployment evidence, and independent closure. The Scope repository currently has no security policy and no published security advisories. The protocol repository has no public issues or pull requests establishing a remediation program.

Pretrend and TrendPlay represent real application/product work, but they do not constitute repair of the underlying protocol findings. The public Pretrend repository has not moved since July 23, 2026, while the live site continues to market TrendPlay and a planned oracle architecture. The site's own roadmap still describes Q4 2026 as the point to complete development and launch the oracle. The investor page remains active and describes a planned SAFT, a token-based investment model, and an 80% team/investor versus 20% community ownership allocation. Those facts demonstrate product/fundraising activity; they do not demonstrate closure of the July protocol or bridge findings.

No finding reviewed here is marked **CLOSED**.

## Evidence bundle reviewed

The uploaded evidence bundle was opened and inventoried. Its SHA-256 is:

`2d6a535172a0e14835de907359a68410519693a0e57ec8dfecb88fe39821dbcd`

It contains the July protocol review, Scope/bridge supplement, preliminary code review, community-control transfer action list, North Star/Pretrend requirements review, and CEO question sets. The two principal baselines for this follow-up are:

- `Vitruveo_Public_Source_Review_Discord_Scrubbed(1).txt` - July 15, 2026.
- `Vitruveo_Scope_Bridge_Findings_Supplement_Discord_Scrubbed(1).txt` - public-material status through July 26, 2026.

The original reports expressly avoided allegations of theft, fraud, criminal conduct, hidden surveillance, or confirmed exploitation. This follow-up maintains the same evidentiary standard.

## Current public platform status

### Protocol repository

Public repository: `https://github.com/Vitruveo/vitruveo-protocol`

Current public head remains:

`ba0ef28d9844b84cd114b638b541c241af33e345`  
Commit message: `add stats and retry`  
Commit date: January 25, 2026.

Current public release list: empty.

The current source still contains the same Batch Send `tx.origin` funding/impersonation pattern reviewed in July. HOST still performs validator-side HTTP operations and signs the generated body with the validator key. RNG/Shuffle remains the same implementation reviewed in July. The custom EVM precompile routing remains in the same audited commit. The workflow still targets `master` while the repository's default/deployed development branch is `main`, uses a self-hosted runner, and runs old `actions/checkout@v2` and `actions/setup-go@v2` actions.

**Finding consequence:** VTRU-01 through VTRU-11 have no later public protocol commit from which a repair can be established. Findings that require deployment evidence also remain unclosed because no signed release, reproducible binary evidence, validator-version inventory, activation record, or independent retest was located in the reviewed public material.

### Scope and bridge

Public repository: `https://github.com/Vitruveo/vtru-scope`

Latest public commit observed:

`e89a125016be7bb20331039b0671bf1c5d30bc60`  
Commit date: August 7, 2026.  
Purpose: fund gas for empty destination wallets during a bridge claim and adjust BNB gas display precision.

Current public `/api/bridge/notarize` behavior still has no demonstrated wallet-signature challenge, authenticated session, nonce, or proof that the HTTP requester controls the supplied account. The route constructs wallets from server-side Vitruveo and BSC notary private keys, reads escrow for the supplied account, signs a destination receipt, and calls `zeroEscrow(account)` on the source chain. It then returns the receipt data to the requester.

The August 7 change expanded the route's operational behavior by optionally funding the destination account before claim; it did not close the authorization/recovery concern identified as SCOPE-01.

Current Scope tokenomics source still includes `const TOTAL_SUPPLY = 500_000_000;`. It still fetches `https://explorer.vitruveo.ai/api/v2/addresses` and maps `data.items` without visible traversal of subsequent pages. Five fixed addresses are still treated as Treasury, Operations, Ecosystem, Validators, and Liquidity in the tokenomics interface.

Current Reflect source explicitly sends 1 VTRU from the connected account to the VIBE wallet and says the purpose is to cause the explorer to index the account.

The current contracts page lists only a limited subset of ecosystem contracts and does not constitute the requested complete registry of networks, proxies, implementations, deployment transactions, current role holders, upgrades, audit state, and decommissioned addresses.

### Public security/remediation process

As reviewed on September 19:

- `Vitruveo/vitruveo-protocol` shows no public issue or pull-request remediation docket.
- `Vitruveo/vtru-scope` shows no ordinary open issues tied to the July findings.
- Scope has one currently visible open pull request, an older Vercel-generated React Server Components CVE update from December 2025, unrelated to the reported Vitruveo findings.
- Scope's GitHub security page reports no `SECURITY.md` security policy and no published security advisories.

This does not prove private remediation work does not exist. It means no public closure trail sufficient to mark the findings closed was identified.

## Finding status matrix

| ID | September 19 status | Public basis |
|---|---|---|
| VTRU-01 Batch Send origin authority | **OPEN** | Exact audited protocol head unchanged; current source still uses transaction origin as funding/caller identity. |
| VTRU-02 HOST validator signing scope | **OPEN / CONDITIONAL** | Same protocol commit and signing design; no later public repair or independent closure. |
| VTRU-03 HOST SSRF exposure | **OPEN / CONDITIONAL** | Same HOST implementation; no public egress-policy or code remediation evidence. |
| VTRU-04 irreversible external side effects | **OPEN** | Same HOST execution architecture; no public finality/simulation-safe redesign. |
| VTRU-05 HOST resource amplification | **OPEN** | Same retry/goroutine architecture; no public bounded durable queue redesign. |
| VTRU-06 RNG/Shuffle for wagering | **OPEN** | Same audited implementation; no public VRF/commit-reveal or adversarial replacement. |
| VTRU-07 STATICCALL boundary | **OPEN** | Exact audited EVM/precompile routing commit unchanged. |
| VTRU-08 validator-key isolation | **OPEN / NOT PUBLICLY CLOSED** | No later protocol commit or documented isolated signing-key redesign. |
| VTRU-09 CI branch/release gate | **OPEN** | Current workflow still targets `master`; repo default branch is `main`. |
| VTRU-10 release engineering | **OPEN** | No GitHub releases; no public signed binary/SBOM/reproducible-build closure found. |
| VTRU-11 `0x...FF` compatibility migration | **NOT PUBLICLY CLOSED** | No later public migration/activation inventory found. |
| SCOPE-01 notarization authorization/recovery | **OPEN** | Current route still accepts an arbitrary supplied account without visible wallet-signed requester authorization. |
| SCOPE-02 centralized bridge notary keys | **OPEN** | Current route still constructs source/destination notary wallets from server-held private keys. |
| BRIDGE-01 privileged bridged-token administration | **NOT PUBLICLY CLOSED** | Required current role-holder, threshold, timelock and upgrade-history proof not located. |
| BRIDGE-02 refund/remainder accounting | **NOT PUBLICLY CLOSED** | No finding-specific patch/test/deployment/independent closure located. |
| BRIDGE-03 recipient blocklist logic | **NOT PUBLICLY CLOSED** | No finding-specific patch/test/deployment/independent closure located. |
| BRIDGE-04 `totalSupply` semantics | **NOT PUBLICLY CLOSED** | No finding-specific patch/test/deployment/independent closure located. |
| SCOPE-03 hard-coded supply | **OPEN** | Current tokenomics source still hard-codes 500,000,000. |
| SCOPE-04 address pagination | **OPEN** | Current tokenomics source consumes one returned `items` set without visible pagination. |
| SCOPE-05 multisig proof | **OPEN / NOT PUBLICLY VERIFIED** | Fixed treasury-category addresses remain; signer/threshold/provenance proof not located. |
| SCOPE-06 WalletFactory/MutexWallet custody assurance | **NOT PUBLICLY CLOSED** | Exact deployed-source/audit/control proof required by July report not located. |
| SCOPE-07 complete transaction history | **NOT PUBLICLY CLOSED** | No independent evidence of complete deployment-to-present history was located. |
| SCOPE-08 staking-statistics integrity | **PARTIAL / NOT CLOSED** | Scope code changed around CoreStakeV2, but no finding-specific regression test and independent closure exists. |
| SCOPE-09 native holder count | **OPEN / NOT PUBLICLY VERIFIED** | Explorer/indexing limitations remain material; no complete-state holder method located. |
| SCOPE-10 Reflect 1-VTRU transfer | **OPEN / INTENTIONAL** | Current Reflect code still transfers 1 VTRU to VIBE for indexing. |
| SCOPE-11 transformed/capped display values | **NOT RE-ESTABLISHED IN THIS FOLLOW-UP** | Prior finding retained as unclosed until exact current affected surface is independently rechecked. |
| SCOPE-12 contract disclosure registry | **OPEN** | Current contracts page remains incomplete relative to requested registry. |

**Closed findings: none.**

## Blockchain/explorer condition on September 19

The public Vitruveo website currently advertises chain ID 1490, a 5-second block time, and the public RPC/explorer. The public Blockscout explorer, however, currently presents stale or internally inconsistent information: it reports latest displayed blocks and transactions as approximately three weeks old, while also showing a total-block count that does not cleanly match the displayed latest block number.

This is a material observability problem. It may indicate explorer/indexer failure, chain liveness trouble, a data-refresh problem, or some combination. This follow-up does **not** label the chain halted because a direct independent JSON-RPC liveness test was not available in this environment. The discrepancy should be treated as a new operational item requiring direct RPC checks from several independent networks and comparison against multiple validators.

## Governance/control update

Vertical Foundation's current public site describes itself as the body governing and funding Vitruveo. It says the Foundation carries protocol development, treasury, long-term growth, manages the validator network, oversees validator onboarding, stewards a multisig treasury, and sets protocol direction.

Those statements are useful descriptions of claimed authority, but the page reviewed does not itself supply the legal chain of title, current GitHub owners, multisig signers and threshold, validator operator inventory, release-authority matrix, bridge/notary key holders, or executed transfer instruments needed to independently establish community control.

The July community-control transfer plan therefore remains relevant. Moving repositories alone would not satisfy it.

## Pretrend/TrendPlay update

Pretrend is now a real public-facing product effort, not merely artwork. Its site promotes TrendPlay and describes an oracle/notary/marketplace architecture. However, the public repository `techbubble/pretrend-website` still shows July 23, 2026 as its last public push.

The current Pretrend site says Q4 2026 is the milestone to complete development and launch the oracle. At the same time, other current copy describes Vitruveo as computing every trend natively and settling every market on-chain. Those statements should be reconciled with a concrete deployment registry and receipt trail before the complete system is represented as independently verifiable production infrastructure.

The investor page remains active. It says Pretrend is bootstrapping, is open to one or two angel investors, expects a seed round structured as a SAFT, calls Pretrend a token play, and describes 20% community versus 80% team/investor ownership. This is not evidence of wrongdoing. It is evidence that fundraising and token/economic design are advancing while the underlying July protocol/bridge remediation still lacks public closure.

## Overall determination

The September 19 follow-up does **not** support the statement that no work at all has occurred. There has been Scope maintenance, a live Pretrend/TrendPlay effort, current marketing/developer pages, and ongoing ecosystem positioning.

It **does** support this narrower and stronger statement:

> **No critical or high protocol/bridge finding from the July public-source reviews can be marked closed from the public evidence reviewed on September 19, 2026. Product and marketing activity has continued, but a finding-by-finding remediation, release, deployment, governance, and independent-verification trail remains absent.**

That is the conclusion that should be published.

## Public disclosure boundary

Do not publish a working exploit recipe, exact request sequence for a live vulnerable endpoint, private-key material, nonpublic credentials, or instructions intended to interfere with the chain or bridge. The public report can describe the missing authorization/control, affected component, severity, current source evidence, and required closure standard without enabling misuse.

The detailed original evidence bundle should be retained intact for evidentiary purposes, but it should not automatically be uploaded wholesale to a public repository while live issues remain. Create a public-safe package and keep an unredacted technical appendix available to responsible maintainers, counsel, auditors, or other authorized reviewers.

## Recommended publication record

Primary source locations reviewed September 19, 2026:

- Vitruveo GitHub organization: `https://github.com/Vitruveo`
- Protocol repository: `https://github.com/Vitruveo/vitruveo-protocol`
- Scope repository: `https://github.com/Vitruveo/vtru-scope`
- Scope security page: `https://github.com/Vitruveo/vtru-scope/security`
- Vitruveo site: `https://www.vitruveo.ai/`
- Vitruveo explorer: `https://explorer.vitruveo.ai/`
- Vertical Foundation: `https://www.verticalfoundation.net/`
- Pretrend: `https://www.pretrend.ai/`
- Pretrend investors page: `https://www.pretrend.ai/investors/`

## Closure standard going forward

A finding should move to **CLOSED** only when the public record identifies the responsible owner, affected versions, repair commit, regression test, successful complete build/test evidence, exact deployed contract/binary identity, coordinated deployment or activation evidence, independent retest, and a closure note describing residual risk.

Anything less should remain **OPEN**, **PARTIAL**, or **NOT PUBLICLY VERIFIABLE**.
