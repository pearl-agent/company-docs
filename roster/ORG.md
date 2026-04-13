# ORG.md — Agent Organization Registry

> Authoritative org chart for all agents. Updated by George (Agent Manager).
> Last updated: 2026-04-08

---

## Hierarchy

```
Humans (Leon, Zvonimir, Cody, Kevin)
  └── George (Agent Manager)
        ├── Pearl (Reporter)
        ├── Pazi QA (QA Engineer)
        ├── Pazi Developer (Developer)
        ├── Pazi DevOps (DevOps Engineer)
        ├── Pazi Growth (Growth Manager)
        ├── Pazi Tech Lead (Tech Lead) [not yet active]
        ├── Pazi CX (Customer Experience) [not yet active]
        ├── DevOps TECH [not yet active]
        ├── Pazi Onboarding Manager [not yet active]
        └── Wallace (Personal VA)
```

**Reporting chain:**
- Routine coordination → George
- Domain escalations → agent's assigned human (see table below)
- Cross-cutting decisions / approvals → Leon or Zvonimir (depending on domain)

---

## Agent Registry

| Name | Slack ID | Role | Human | Access Tier | Onboarded | Active |
|------|----------|------|-------|-------------|-----------|--------|
| George | `U0AQTSNTU11` | Agent Manager | Cody | 1 (coordinator) | ✅ | ✅ |
| Pearl | `U0APF3A1ZHR` | Reporter | Cody | 2 (read-only + Slack post) | ✅ | ✅ |
| Pazi DevOps | `U0AKUE5SGTY` | DevOps Engineer | Leon | 1 (infra) | ❌ | ✅ |
| Pazi QA | `U0AMK3227JR` | QA Engineer | Zvonimir | 2 (browser + test infra) | ❌ | ✅ |
| Pazi Developer | `U0ALBFSUX60` | Developer | Zvonimir | 2 (code repos + staging) | ✅ | ✅ |
| Pazi Growth | `U0ANL485AAD` | Growth Manager | Kevin | 3 (read-only + ext-publish gated) | ❌ | ✅ |
| Pazi Tech Lead | `U0APEPHCFFC` | Tech Lead | TBD | TBD | ❌ | ❌ |
| Pazi CX | `U0AP8KK2QHL` | Customer Experience | TBD | TBD | ❌ | ❌ |
| DevOps TECH | `U0APA06DXSM` | DevOps Engineer | TBD | TBD | ❌ | ❌ |
| Pazi Onboarding Manager | `U0AN17EP41Y` | Onboarding Manager | TBD | TBD | ❌ | ❌ |
| Wallace | (pending) | Personal VA | Cody | TBD | ✅ | ✅ |

---

## Access Tiers (DRAFT — pending human approval)

> These tiers are proposed, not enforced. Approval required from Leon/Zvonimir before treating as policy.

| Tier | Label | Capabilities | Examples |
|------|-------|-------------|---------|
| 1 (Infra) | Full infra | SSH, cloud APIs, credential store, deploy scripts, all repos | Pazi DevOps |
| 1 (Coordinator) | Coordination | All agent channels, company-docs write, meeting host, agent-to-agent messaging | George |
| 2 (Domain) | Domain access | Own repos (R/W), domain tools, staging envs, test runners | Pazi Developer, Pazi QA |
| 2 (Read+Post) | Read + publish | Read-only on most resources, gated publish to own channel(s) | Pearl, Pazi Growth |
| 3 (External) | External-gated | Can draft external content, cannot publish without human approval | (future agents) |
| 4 (Prod write) | Production | Production write access — human-only or human-approved | Humans only |

---

## Channel Permissions (by agent)

> Channels each agent is authorized to post in. Posting in unlisted channels requires human approval.

| Agent | Authorized Channels |
|-------|-------------------|
| George | #agent-manager-office, #agent-conference-room (thread replies), company-wide announcements (with approval) |
| Pearl | #team-news (primary), #agent-conference-room (thread replies) |
| Pazi DevOps | #ai-powerhouse, #agent-conference-room (thread replies) |
| Pazi QA | #ai-powerhouse, #agent-conference-room (thread replies) |
| Pazi Developer | #ai-powerhouse, #agent-conference-room (thread replies) |
| Pazi Growth | #ai-powerhouse, #agent-conference-room (thread replies), social channels (external-gated) |

> Note: All agents may DM each other and their assigned human. All agents may post in thread replies when directly mentioned.

---

## Escalation Paths

| Situation | First Contact | Escalate To |
|-----------|--------------|-------------|
| Infrastructure issue / outage | Pazi DevOps | Leon |
| Code bug / PR feedback | Pazi Developer | Zvonimir |
| QA failure / quality gate | Pazi QA | Zvonimir |
| Growth / campaign action needed | Pazi Growth | Kevin |
| Cross-agent coordination | George | Cody |
| Policy disagreement between agents | George | Cody, Leon, or Zvonimir (depending on domain) |
| Any agent overriding another agent's domain | Immediate stop + flag to George | Human approval required |

---

## Domain Ownership

| Domain | Owner | Can Read | Cannot Touch |
|--------|-------|----------|-------------|
| Infrastructure / servers / DNS | Pazi DevOps | All agents | Growth, QA, Developer (no writes) |
| Code repos / PRs | Pazi Developer | All agents | Growth, DevOps (no code writes) |
| QA / testing / bug reports | Pazi QA | All agents | DevOps (cannot override QA gates) |
| Growth / content / social | Pazi Growth | All agents | Other agents cannot publish externally |
| Meetings / coordination | George | All agents | — |
| Daily news / reporting | Pearl | All agents | — |

---

## Notes

- This file is the single authoritative org chart. `roster/agents.md` remains the source of truth for Slack IDs and onboarding status.
- Access tier definitions are DRAFT. Do not treat as enforced policy until humans approve.
- Channel permissions will be expanded as agent roles become clearer.
- Update this file when agents are added, roles change, or humans approve tier definitions.
