# How agents work on this board

Agents move the cards on the 5G-MAG boards. People can follow the same rules. Each issue is one requirement: one clause of a 3GPP specification, for one component (for example the AS), read at one release, with its cases. It is drawn from the specification alone and starts as Not audited. The board column (Status) says where it stands.

## The statuses, and who may move a card

| Status | Meaning | Set by | Next |
| --- | --- | --- | --- |
| Not audited | Filed from the specification. Nothing is known yet about the code | the filing tool | the audit moves it to Backlog, Verifying or Needs review |
| Backlog | The audit found a gap: a case is Absent, Differs from the specification, or the specification is inconsistent | the audit | In progress |
| In progress | Someone is building it | whoever claimed it | In review, or back to Backlog when the claim is released |
| In review | A pull request is open | the author, when opening it | Verifying, or back to In progress |
| Verifying | Every case reads as Implemented (by the audit, or after a merge). Waiting for the cross-check | the auditor or the author | Supported, or back to In progress or Backlog |
| Supported | Cross-checked by someone other than the author, and read as implemented on `main`. The issue is closed | the verifier | none |
| Needs review | The readers could not settle it. A person decides | the audit | a person only |
| On hold | Parked | a person | a person only |

## Audit (Not audited)

1. Pick an issue with the Status Not audited and no assignee. Take the feature or component you were asked to work on. Assign yourself and comment `auditing` with the name of the agent or run. If someone else is already assigned, pick another issue.
2. Read the clause at the pinned version with the command in the issue. The sentences in the table are quotes, not the whole clause.
3. Find the code of the component in the repositories listed under [Where the code is](README.md#where-the-code-is), at the head of `main`. Judge each case:
   - **Implemented**: the code does what the case says.
   - **Differs from the specification**: the code does something, and it is not what the case says.
   - **Absent**: nothing in the code does it.
   - **Specification inconsistent**: the case cannot be built as written (it contradicts another clause or itself). Say which clause.
   - **Not applicable**: the case does not fall on this component (the statement was placed here by the reading rules by mistake). Say why. A person checks these; they do not count as a gap.
4. Post the audit report (below). Then set the Status: any Absent, Differs or Inconsistent case, Backlog; every case Implemented (or Not applicable), Verifying; a case you cannot settle, Needs review.

A code reading is not a run. Say in the report which cases you also ran, and which you only read.

### The audit report

One comment on the issue, in this form. It is what the Website reads for the case table of this requirement.

````
Audit of #<issue>, <specification> <version> clause <x.y.z>, component <AF|AS|Client|App Provider>
Code: <repository>@<commit> (main), read on <date>. Run or read only: <which>.

| Case id | Verdict | What the code does | Evidence |
| --- | --- | --- | --- |
| <id> | Implemented / Differs from the specification / Absent / Specification inconsistent / Not applicable | <one sentence, in plain words> | <path:line in a public repository, or the test name> |

Decision: <Backlog | Verifying | Needs review>. Why: <one line>.
````

Evidence is the file and line (or the test) in a public 5G-MAG repository. For a private repository give the test name only. Everything on this board is public.

## Build (Backlog)

1. Pick an issue with the Status Backlog, no assignee, and not On hold. Claim it: assign yourself, set the Status to In progress, and comment `claimed` with the name of the agent or run. If someone else is already assigned, pick another issue. The first assignee keeps it.
2. Read the whole issue and the audit report. Implement each case that is Absent or Differs, in the repository named in the audit report, with one test per case.
3. Open the pull request, link the issue, quote each clause as `Basis: <specification> <version> clause <x.y.z>: "<sentence>"`, name the test that covers each case, run `3gpp-verify --commits <base>..HEAD --strict`, and set the Status to In review.
4. When it is merged, set the Status to Verifying.

## Cross-check (Verifying)

Someone other than the author of the code or of the audit report does this. Re-read each case against the clause at the pinned version. Run the named tests on the base and the head commit and check that each fails without the change and passes with it; for a case the audit found Implemented, check the evidence in the report and run the existing tests that cover it. Run `3gpp-verify --commits <base>..HEAD --strict` on the pull request, if there is one. Then tick the cases in the issue, post the verification report, set the Status to Supported and close the issue. If a case does not hold, comment why and set the Status back to In progress (or Backlog if nobody is building it).

### The verification report

The cross-check ends with a comment on the issue, from the verifier, in this form. It is the evidence for the move to Supported. A card without it does not move.

````
Verification of #<issue>, <specification> <version> clause <x.y.z>
Base: <commit>. Head: <commit>. Pull request: <link, or none when the audit found every case Implemented>.

| Case id | Test | Fails on base | Passes on head | Clause re-read |
| --- | --- | --- | --- | --- |
| <id> | <test name> | yes: <command, result> | yes: <command, result> | yes, at <version> |

Cases the audit found Implemented: evidence checked and existing tests pass: <command, result>.
3gpp-verify --commits <base>..HEAD --strict: <result, or not applicable>.
Decision: Supported. (or: back to In progress, cases <ids> do not hold because <reason>.)
````

The verifier runs the tests itself. A report that only repeats what the author or the auditor wrote is not a verification.

## Rules

- Never edit the machine block under **For an agent** or the table of cases. Comment instead. The tick list is ticked only by the verifier.
- Never cross-check your own work, and never set Supported on it. The auditor and the verifier of a card are not the same agent.
- Never move a card into or out of On hold. Needs review is set by the audit; only a person moves a card out of it.
- If an issue looks wrong (the specification says something else, or a case does not apply), comment with the clause and the reason and leave the Status. A person decides.
- Write each status change as a comment: `Status: <from> to <to>. Why: <one line>. Evidence: <audit report, pull request, test names, commit>`.
- Everything here is public. No secrets, no personal data, and no specification text beyond the quoted sentences.
