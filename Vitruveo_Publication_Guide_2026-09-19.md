# Publishing the Vitruveo Review Safely and Permanently

## Recommended publication structure

Create a new neutral GitHub organization or use a deliberately separate technical-review account that has no branding or repository relationship to PFN, BarnBoard, or other unrelated projects. A repository name such as `vitruveo-public-review` or `vitruveo-remediation-status` is descriptive without making an accusation in the repository title.

Suggested repository layout:

```
README.md
reports/
  Vitruveo_Public_Remediation_Status_Report_2026-09-19.pdf
  Vitruveo_Public_Remediation_Status_Report_2026-09-19.md
findings/
  finding-status.csv
sources/
  PUBLIC_SOURCE_INDEX.md
integrity/
  SHA256SUMS.txt
  DISCLOSURE_TIMELINE.md
private-not-published/
  README.txt
```

Do **not** commit an unredacted live-exploit appendix or credentials. Keep the original evidence ZIP offline or in access-controlled storage. Publish only material that explains the vulnerability class and remediation status without giving a ready-made attack sequence.

## Publication sequence

1. Create the neutral GitHub repository and commit the Markdown report, PDF, finding matrix, source index, disclosure timeline, and SHA-256 manifest.
2. Create a signed or clearly versioned GitHub Release, for example `v2026.09.19`, and attach the PDF and public evidence package.
3. Enable GitHub Pages for a simple human-readable landing page that links to the release and status matrix.
4. Archive the GitHub release through Zenodo to obtain a DOI and timestamped scholarly-style citation. This gives the report a durable identifier even if GitHub later changes.
5. Upload the same public-safe PDF and hash manifest to the Internet Archive. Optionally pin the files to IPFS or Arweave for content-addressed persistence.
6. Post a short neutral notice in the Vitruveo Discord and any other relevant community channel, linking to the immutable release rather than pasting exploit detail into chat.
7. Send the unredacted technical appendix privately to the responsible operator/maintainer and, if appropriate, an independent auditor or counsel. Keep a dated delivery record.
8. Update the repository by adding closure records. Do not silently rewrite the original report. Add a new dated report or append a signed correction/changelog.

## Recommended public notice

> **Vitruveo public-source remediation follow-up - September 19, 2026:** I rechecked the public protocol, Scope/bridge, governance, explorer, and Pretrend material against the July 2026 technical reviews. I did not find public evidence sufficient to close any of the critical/high protocol or bridge findings. Product activity has continued, but the protocol repository remains on the same reviewed commit and a finding-by-finding repair, regression-test, deployment, and independent-closure trail is still not public. The report is evidence-based, does not allege criminal conduct, and intentionally omits exploit instructions for issues that may remain live.

## Where to publish

**Canonical technical record:** GitHub repository + GitHub Release.  
**Permanent citation:** Zenodo DOI tied to the release.  
**Independent archive:** Internet Archive.  
**Content-addressed copy:** IPFS or Arweave, optional.  
**Community distribution:** Vitruveo Discord, X, relevant developer/security communities, linking back to the canonical release.  
**Private disclosure channel:** direct email/message to the operator/CEO and any independent auditor, with the unredacted technical appendix only.

## Defamation and accuracy discipline

Use statements that can be demonstrated from source and public records. Prefer phrases such as `current public source shows`, `no public closure evidence was identified`, `critical if reproduced against the live service`, and `not publicly verifiable`. Do not state that a person stole funds, committed fraud, intentionally concealed defects, or refused to repair something unless you have independent evidence establishing that specific claim.

Separate motive from evidence. It is supportable to say that fundraising/product activity continued while remediation remained unclosed. It is not necessary to claim the motive for doing so.

## Integrity and update policy

Never replace an old public report without preserving the old hash and release. If a factual error is found, publish a correction that identifies the old statement, the new evidence, and the corrected conclusion. If a finding is fixed, publish the repair commit, test, deployed artifact, independent retest, and closure date next to the original finding.
