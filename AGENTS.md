# How agents work on this board

Agents move the cards on the 5G-MAG boards. People can follow the same rules. Each issue here is one section of a 3GPP specification, read at one release, with the cases it contains. The board column (Status) says where it stands.

## The statuses, and who may move a card

| Status | Meaning | Set by | Next |
| --- | --- | --- | --- |
| Not audited | Filed from the specification. Nothing is known yet about the code | the filing tool | the audit moves it to Backlog, Supported or Needs review |
| Backlog | The audit found a gap: a case is Absent, Differs from the specification, or the specification is inconsistent | the audit | In progress |
| In progress | Someone is building it | whoever claimed it | In review, or back to Backlog when the claim is released |
| In review | A pull request is open | the author, when opening it | Verifying, or back to In progress |
| Verifying | Merged. Waiting for the cross-check on `main` | the author, when it is merged | Supported, or back to In progress |
| Supported | Cross-checked, and read as implemented on `main`. The issue is closed | someone other than the author | none |
| Needs review | The readers could not settle it. A person decides | the audit | a person only |
| On hold | Parked | a person | a person only |

Until the audit tool exists, the moves out of Not audited are made by the owners of the 5G-MAG organisation.

## Pick, claim, build

1. Pick an issue with the Status Backlog, no assignee, and not On hold. Take the feature or component you were asked to work on.
2. Claim it: assign yourself, set the Status to In progress, and comment `claimed` with the name of the agent or run. If someone else is already assigned, pick another issue. The first assignee keeps it.
3. Read the whole issue: the cases, the repository named under **Build it in**, and **Build it, and cross-check it**. Read the requirement at the pinned version with the commands in the issue. The sentences in the table are quotes, not the whole clause.
4. Build it in the repository named, with one test per case that is Absent or Differs. For a case marked Not audited, first find out what the code does and say so in the pull request.
5. Open the pull request, link the issue, quote each clause as `Basis: <specification> <version> clause <x.y.z>: "<sentence>"`, name the test that covers each case, and set the Status to In review.
6. When it is merged, set the Status to Verifying.

## Cross-check (someone other than the author)

Re-read each case against the clause at the pinned version. Check that the named test fails without the change and passes with it. Run `3gpp-verify --commits <base>..HEAD --strict` on the pull request. Then tick the cases in the issue, comment what you checked, set the Status to Supported and close the issue. If a case does not hold, comment why and set the Status back to In progress.

## Rules

- Never edit the machine block under **For an agent**, the Verdict labels, or the tables of cases. Comment instead.
- Never cross-check your own work, and never set Supported on it.
- Never move a card into or out of Needs review or On hold.
- If an issue looks wrong (the specification says something else, or a case does not apply), comment with the clause and the reason and leave the Status. A person decides.
- Write each status change as a comment: `Status: <from> to <to>. Why: <one line>. Evidence: <pull request, test names, commit>`.
- Everything here is public. No secrets, no personal data, and no specification text beyond the quoted sentences.
