# apple-banana

This repository is the code repository that the `bash#8` software factory works in. It is currently a fresh, empty project: there is no application code yet, only this README. As work items are implemented, their changes will land here through the factory's pull request workflow described below.

## What is the factory?

A software factory is a team of agents that automates the software development lifecycle for this repository, from an incoming request to a merged pull request. A foreman agent orchestrates the workflow and delegates each stage to a specialized subagent. The factory does not replace human judgment: it stops at defined gates for approval and hands every pull request to a human to merge.

## Agent roles

- **Foreman**: orchestrates the factory workflow, dispatches each stage to the right subagent, communicates with the requester, and keeps the work moving from request to hand-off.
- **Triage**: researches a request, reproduces bugs when needed, and creates or updates the tracked work item with its findings, complexity, and any ambiguity that needs a spec.
- **Spec**: resolves ambiguity before implementation starts by interviewing the requester and writing a product and/or technical spec, committed to a draft pull request for approval.
- **Implement**: makes the change the work item (and spec, if one exists) describes, verifies it works, and delivers it as a pull request ready for review.
- **Review**: adversarially reviews a pull request against the work item and spec, and reports findings for either automatic rework or human decision.

## How work enters the factory

Work reaches the factory through these automations:
- Slack app mentions in a channel.
- Slack direct messages to the factory.
- Linear agent sessions.
- GitHub agent mentions or assignment on an issue or pull request labeled `factory:bash-8`.
- GitHub pull request closed or merged, which the factory uses to close out tracked work.

## Workflow

1. A request enters the factory through one of the automations above.
2. The foreman triages the request when its cause or scope is not yet known, producing a tracked work item.
3. For work with real ambiguity, the foreman asks the requester if a spec is needed. If they agree, the spec agent interviews the requester and commits a spec to a draft pull request. **The requester must approve the spec before implementation starts.**
4. The implement agent makes the change, verifies it, and delivers a pull request.
5. The review agent adversarially reviews the change. Findings that need human judgment are posted on the pull request; unambiguous findings are sent back to the implement agent to fix automatically.
6. The foreman hands the pull request to the requester. **A human always decides if and when to merge it** — the factory never merges its own pull requests.
7. When the pull request merges, the factory closes out the tracked work item.

## Conventions

- Factory branches are named `factory/<short-slug>`.
- Pull requests open as drafts and are marked ready for review once the change is verified.
- Every pull request and issue that goes through the factory workflow carries the label `factory:bash-8`.
- The factory never merges its own pull requests; a human always merges.
