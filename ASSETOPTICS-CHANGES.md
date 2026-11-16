# AssetOptics changes to Portwood 3.63.0

This branch is Portwood 3.63.0 (tag `v3.63.0-free`, commit `b74ef55`) with test-only changes, so the unmanaged deploy passes `RunLocalTests` in customer orgs. No runtime code is changed. Tag: `v3.63.0-free-ao1`.

| Test | Failed in | Why | Change |
|---|---|---|---|
| `DocGenCurrencyTest.singleCurrencyOrgSkipsAllCurrencyMachinery` | multi-currency orgs | assumes a single-currency org | returns early when `UserInfo.isMultiCurrencyOrganization()` |
| `DocGenFontTest` (4 methods) | orgs with User sharing set to Private | the Standard User font admin can't see the font author user | the author is looked up before `System.runAs` (`fontAuthor()`) |
| `DocGenSignatureTests.testSendPin_success`, `testSendPin_expiredToken` | orgs that can't send email (sandboxes on "System email only") | sending the PIN email fails | returns early when `Messaging.reserveSingleEmailCapacity` throws (`canSendEmail()`) |

Found while validating in the `rpm-cpg` partial sandbox, 2026-11-16 (7 of 2,310 tests failed; the rest passed).
