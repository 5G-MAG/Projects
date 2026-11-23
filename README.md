# Projects

The detailed work items of the 5G-MAG projects, as issues on public kanban boards. The high-level roadmaps stay in [5G-MAG/Roadmaps](https://github.com/5G-MAG/Roadmaps).

- **Boards:** [5GMS](https://github.com/orgs/5G-MAG/projects/77) (more projects will follow).
- **What an issue is:** one requirement, as the Website's Implementation status pages group them: a feature, then a requirement (one clause of a 3GPP specification for one component), then its cases (the sentences, items and table rows of the clause that fall on that component). Each issue quotes its cases, says how to read the clause at the pinned version, and says what has to be true for the card to move on. Issues are generated from the specifications alone by the baseline workflow in [Standards2Deployments](https://github.com/5G-MAG/Standards2Deployments/tree/main/baseline), and start as Not audited: the code is read by the audit, not by the filing.
- **Who moves the cards:** agents and people, by [the rules in AGENTS.md](AGENTS.md).
- **Who creates issues:** 5G-MAG only. The repository limits issue creation to collaborators.

## Where the code is

The audit looks for the code of a component here. These are the public 5GMS repositories; the audit report names the one it read.

| Component | What it is | Repositories |
| --- | --- | --- |
| AF | 5GMS Application Function | [rt-5gms-application-function](https://github.com/5G-MAG/rt-5gms-application-function) |
| AS | 5GMS Application Server | [rt-5gms-application-server](https://github.com/5G-MAG/rt-5gms-application-server) |
| Client | 5GMS client: Media Session Handler, Media Stream Handler, common library, 5GMS-Aware Application | [rt-5gms-media-session-handler](https://github.com/5G-MAG/rt-5gms-media-session-handler), [rt-5gms-media-stream-handler](https://github.com/5G-MAG/rt-5gms-media-stream-handler), [rt-5gms-common-android-library](https://github.com/5G-MAG/rt-5gms-common-android-library), [rt-5gms-application](https://github.com/5G-MAG/rt-5gms-application) |
| App Provider | 5GMS Application Provider | [rt-5gms-application-provider](https://github.com/5G-MAG/rt-5gms-application-provider), with the tools and examples in [rt-5gms-examples](https://github.com/5G-MAG/rt-5gms-examples) |

## The board fields

Status (the stages in AGENTS.md), Feature, Document, Component (AF, AS, Client, App Provider), Profile (downlink 5GMSd, uplink 5GMSu, or both), Clause, Code repository (set by the audit) and Cases (how many).
