# Agent, thread, and access differences

**Baseline: October 26, 2026.** A dated reference for John's coordination decisions; behavior can change.

## Start here

- Keep **one existing task per outcome**; continue it with its files and decisions.
- Name the executor: **John's Mac and path**, or **a cloud configuration and repository/ref**. “Default” is context-dependent.
- Use a capable dot to coordinate; let the outcome's task own execution. A native child agent is a separate relationship.
- Keep canonical state in **Git, an issue, or a private archive**. Preserve working files beyond chat history.
- Treat **reading threads, sending instructions, and spawning children as three independent capabilities**. Sharing history does not transfer tools or authorization.
- Diagnose the missing layer. Repeated approval cannot create a missing tool. Ask once for the smallest concrete change.

**Evidence labels:** **Documented** = official source; **Observed** = operation/result recorded by the named observer; **Agent-reported** = another agent's account, not independently reproduced here; **Proposed** = recommended practice; **Unknown** = not established. The summary's coordination choices are **Proposed**.

## Independent axes

These labels describe different dimensions. Combining them does not yield a fixed permission bundle.

| Axis | What to record and what it means |
| --- | --- |
| Interface: Chat / Work / Codex | **Documented:** Chat emphasizes conversational help, Work longer tasks and deliverables, Codex technical work. Interface alone does not identify tools. [Product overview][product] |
| Home / project | **Documented:** Home starts without shared project context. Projects organize related chats and context; local projects can attach folders. This is organization, **not** the Personal/Business account boundary. Conversation sync does not upload an entire local folder. [Projects][projects] |
| Dot / ordinary task / native child | **Documented:** dots can coordinate separate cloud threads and local tasks. **Terminology here:** ordinary tasks own outcomes; native children use an agent's collaboration facility. Child coordination does not establish authority over unrelated chats. [Dots][dots] |
| User-started / delegated | Record who initiated the task and the creation operation if known. **Unknown:** creation path appears relevant to observed capability differences, but its causal mapping is unestablished. Neither user-created nor dot-created tasks have a universal messaging guarantee. |
| Local / worktree / cloud | **Documented:** Local uses a computer's project directory; Worktree isolates changes in a Git checkout on that computer; Cloud has a separate task workspace. A worktree is not a separate credential or account boundary. [Environments][modes] |
| Generic cloud / named configuration | Distinguish an unspecified cloud executor from a reusable configuration such as `skills-workshop`. **Documented:** a published configuration prepares separate task workspaces, not one shared live machine. Starting from that configuration does not automatically recover another task's uncommitted changes. [Codex Cloud][cloud] |
| Phone / Mac surface | **Documented:** the device used to issue or review a request need not execute it. Phone access to a connected computer differs from cloud execution. Opening a conversation on a Mac does not establish local execution. [Product overview][product] |
| Personal / organization workspace | **Documented:** workspace, role, provider account, and app permissions affect access. Record separately from Home/project and local/cloud. John's full entitlements are **unknown** here. [Connected apps][apps] |
| Skills / usable execution | **Observed here:** a skill can be installed, discoverable, and readable while its required runtime evidence remains unresolved. Check dependencies, metadata access, resolver compatibility, and action authorization separately; see the fourth case below. |

“Session” is ambiguous: specify whether it means the conversation, an execution process/workspace, or an authenticated browser/service session.

## What is shared—and what must be checked separately

| Resource | Useful distinction |
| --- | --- |
| Transcript / context | A task may receive history, a summary, or project instructions. That provides information, not another task's callable operations or authority. |
| Working files | Check the actual path, checkout, revision, and uncommitted state. Shared project context and conversation access do not establish file access. |
| Credentials | Identify the account/source without copying secrets into prompts. A Mac login does not automatically appear in a cloud browser. |
| Tools | Discover what this task can actually call. A skill describes a workflow; it does not by itself supply a missing operation. |
| Authorization | User consent for a specified action, backend access, filesystem/network boundaries, and service permissions must each support that action. |
| Lifecycle | Continuing a cloud task differs from starting another from its configuration. Preserve results outside transient execution state. |

**Documented anchors:** separate cloud files/browser sessions ([Dots][dots]); separate task files ([Codex Cloud][cloud]); plugin installation and approval preferences do not grant new service access ([Connected apps][apps]). This table is a diagnostic model.

## Access and messaging snapshot

**October 26, 2026.** “Available” means an operation was exposed, not that every destination accepts it. These are scoped observations, not universal product rules.

| Entity | Read / observe threads | Send / steer threads | Create tasks / native children |
| --- | --- | --- | --- |
| Parent dot | **Observed by parent:** investigation and linked reads succeeded | Send operation exposed; destinations still gated | Task creation observed; native children **unknown** |
| Investigation thread | **Unknown** | **Agent-reported:** could not identify/contact dot | **Unknown** |
| Linked thread | **Agent-reported:** reading/monitoring available | **Agent-reported:** `send_message_to_thread` absent | **Agent-reported:** own-subagent coordination available |
| Implement skills-manager issue 2 | **Observed:** parent dot reader → this task failed (backend placement-format compatibility); local Mac reader → this task succeeded. Its history also shows completed read calls. | Retrieved history contains completed send calls; no new delivery test | Retrieved history contains task creation and child activity |
| This dot-created Mac documentation task | **Observed by writer:** local supported read succeeded | Send operation exposed; untested | Task creation exposed; native source-review child completed |

**Observed by parent:** its catalog returned a local Mac as connected, attached, and authorized, and saved cloud configuration `skills-workshop` with repository ref `main`; no other targets returned. This proves discovery/launch prerequisites, not complete service access.

**Investigation case — agent-reported, parent read at 13:41 UTC:** the dot could not be identified/contacted; no provisioning or network-change request was submitted. Reported needs were HTTPS to `auth.openai.com` and HTTPS/WSS with CONNECT/Upgrade to `codex-cloud-backend.chatgpt.com`, preserving existing domains and archive credentials. Isolated device sign-in failed at the blocked auth endpoint before producing a URL/code. Active runtime credentials were unchanged; acquisition stayed stopped. Outbound connectivity, sign-in, and messaging discovery are distinct blockers. These diagnostics authorize no network/security change or login here.

**Linked case — agent-reported:** a completed turn said authorization was clear but the send tool was absent, with no known way to enable it. Own-child messaging and observing other chats remained available. The writer did not reproduce a denied send.

**Implementation case — route-specific evidence:** the parent's reader returned `AppServerBackendRequestError`, reporting “unsupported placement format version 1” for this post-cutover thread ID. That is a backend ID/placement compatibility failure, not owner-denied access. The writer's supported local `read_thread` then succeeded, returning host `local` and the title above. Historical calls establish scoped past capability, not unrestricted current messaging. No live task was steered or changed.

**Creation provenance:** the parent reports `parentThreadId: null` for both the linked thread and this task, which it demonstrably created through the dot. Null therefore cannot distinguish user-started from dot-created here. Record the observed create call or user's account of creation. This writer's inventory exposes `read_thread`, `send_message_to_thread`, and `create_thread`; it does not prove permission for every destination.

### Fourth case: visible skill, unresolved provenance

**Observed by writer:** the local `commit-provenance` skill was discoverable through `~/.agents/skills` and readable. Its helper ran but exited 1 with `commit-provenance: commit-provenance: no matching runtime turn metadata for this thread`. The initial commit paused before `git commit` was invoked.

| Layer | What this case establishes |
| --- | --- |
| Installed / discoverable / readable | The local skill's instructions were available; that alone did not make its workflow finishable. |
| Executable dependencies | The helper launched; follow-up checks found Bash, Python, jq, and Git. This does not validate every possible dependency or runtime path. |
| Runtime metadata access | The resolver obtained no matching current-turn evidence. This result does not establish that identity metadata is absent everywhere or that access was denied. |
| Resolver compatibility | **Unknown:** whether the runtime provides the expected representation and the resolver recognizes it. No causal diagnosis was established. |
| Action authorization | The local commit was authorized. The skill required resolved provenance; John explicitly waived that requirement for this one initial commit, with unavailable values marked `unknown`. |

The helper expects task/turn evidence for the **model identifier and reasoning effort**, plus **Desktop and bundled CLI versions** for its trailers. Follow-up read-only checks established Desktop `26.1021.31345` and CLI `0.164.0-alpha.11.1`. Matching turn metadata, model, and effort remained unresolved through this resolver. Valid Git identity stays unchanged; the waiver changes neither the helper nor future requirements.

**Known source attribution:** unresolved model/effort does not make the source of these changes unknown. John subsequently requested this fuller record and a follow-up correction commit:

| Provenance field | Value and evidence |
| --- | --- |
| Agent provider | **OpenAI agent**, established in the task context and John's clarification. |
| Creation path | **Initiated/delegated by dot**, observed by the parent when creating this task. |
| Coordination / model layer | **Cloud-based OpenAI agent coordinated through dot**, per John's clarification; distinct from the executor below. This does not identify the exact model. |
| Executor | **John's local Mac**, directly confirmed by `hostname`. |
| Working directory | **Local project directory**, directly confirmed by `pwd`. |
| Desktop / bundled CLI | `26.1021.31345` / `0.164.0-alpha.11.1`, independently checked read-only. |
| Exact model / reasoning effort | **Unknown through the resolver**; these unresolved fields do not erase the known attribution above. |

Original local commit `3b14ced0aae673d31906c7df1d135f80c83eacd8` is preserved locally. The public repository starts from a separate baseline with private thread identifiers and machine-specific paths removed. The attribution correction retains useful source metadata in this document and commit trailers without changing Git author/committer identity. Future records should retain known provider, creation path, task ID, and executor even when exact model or effort cannot be established.

**User-reported:** John had previously seen similar identity uncertainty with the dot. The relationship is **unknown**; this single task does not establish a rule for dot-created tasks.

## A practical two-lane approach

**Proposed — coordination lane:** use a capable dot/coordinator to select the existing outcome task, summarize decisions, read progress, and route authorized instructions. If sending is unavailable, provide a precise handoff for John or an authorized capable task. Avoid replacement tasks merely to escape blocked messaging.

**Proposed — execution lane:** one task owns each outcome, files, and verification. Choose by resource needs: Mac for local files/apps/sessions; named cloud setup for prepared repositories and cloud services. Continue the original task for unfinished changes. Use native children for bounded subtasks; record their results.

Keep task link, executor, revision/artifact path, result, and blocker with canonical state: Git for source and this reference, issues for status, private archives for sensitive material.

No monitoring or alerts are configured. Check on request/resume; recurring follow-up needs a separate automation.

## Exact blocker vocabulary

**Proposed reporting terms:** avoid “permissions problem” when a narrower diagnosis is available.

| Blocker | Meaning / next useful step |
| --- | --- |
| `MISSING_TOOL` | Required operation is absent. Identify a supported route or report the capability gap; repeated consent cannot add it. |
| `UNSUPPORTED_OPERATION` | Tool exists, but this action, target type, or backend is unsupported. Name that limitation. |
| `BACKEND_COMPATIBILITY` | Supported route rejects an ID/placement representation. Record the route/error; try another supported reader if authorized. |
| `AUTHENTICATION_REQUIRED` | Connection/sign-in is missing or expired. Identify the intended account and supported connection flow. |
| `RESOURCE_ACCESS_DENIED` | Service/backend explicitly rejects this account or action. Record the rejection and exact resource. |
| `SANDBOX_BOUNDARY` | Filesystem, network, or executor boundary prevents the operation. Name the path/domain and required action. |
| `APPROVAL_REQUIRED` | An otherwise supported action awaits a specific approval. Reuse valid existing authorization where applicable. |
| `APPROVAL_DENIED` | Human or automatic review rejected the action. Identify which and summarize its stated reason. |
| `ENVIRONMENT_UNAVAILABLE` | Required computer/configuration cannot presently be used. Record disconnected, missing, or otherwise reported state. |
| `CONTEXT_MISSING` | Needed facts or artifact identity are missing; this is not necessarily an access failure. |
| `PROVENANCE_UNRESOLVED` | Required attribution evidence was not resolved. Report expected/missing fields and the failed lookup separately from authorization. |
| `OUTCOME_UNCERTAIN` | Request may have executed but confirmation is missing. Inspect state before any retry. |

**Documented:** approval handling and sandbox boundaries are separate controls. Automatic review does not itself expand the sandbox. Available modes vary by environment and configuration. [Permissions][permissions]

### Minimal preflight and one useful access request

Before meaningful work, check:

1. Existing outcome task, intended deliverable, and canonical state location.
2. Explicit executor/configuration, workspace/account, and required files/services.
3. Available read, send, and child operations independently; perform only relevant harmless reads to verify access.
4. Existing authorization and the first concrete blocked action. Continue independent authorized work.

Use one compact request, with no secrets:

```text
Action + exact target:
Executor / workspace / account:
Blocker code + evidence or stated reason:
Completed work + saved location:
Outcome: not attempted | denied | pending | uncertain
Smallest needed decision/change + why existing authorization is insufficient:
```

After denial, retry only with materially new relevant evidence and known nonexecution. Check uncertain outcomes first. Report once; repeat a request only when something changes.

## Recording changes without erasing history

When capability changes, append date, task/host/configuration, evidence type, operation/target, previous/new results, and verification limits. Reference that entry when updating guidance; preserve earlier observations as dated facts. Never record secrets or private assistant notes.

Review the diff and commit only this document. Git preserves wording; this history explains why. A different task exposing a tool does not establish a rollout or its cause.

| Date | Change | Evidence / limits |
| --- | --- | --- |
| 2026-10-26 | Initial reference and three requested case studies | Official sources checked; local implementation-thread read succeeded after parent's compatibility failure. Parent observations, agent reports, and writer observations separated. No send test or permission change. |
| 2026-10-26 | Added skill usability and fourth provenance case | Recorded resolver failure, independently checked versions, and John's one-time initial-commit waiver permitting `unknown` fields. Skill and settings unchanged. |
| 2026-10-26 | Corrected incomplete source attribution in a follow-up | Preserved initial commit `3b14ced0aae673d31906c7df1d135f80c83eacd8`; recorded OpenAI/dot/task origin and Mac executor, retaining uncertainty only for unresolved fields. |
| 2026-10-26 | Made reader-route distinction explicit in the matrix | Implementation-thread row now records parent dot reader's backend placement-format failure and local Mac reader's successful read. |
| 2026-10-26 | Published technical reference | Removed private thread links/IDs, literal hostname, and user-specific paths; retained environment names, software versions, diagnostics, and useful source attribution. |

[product]: https://help.openai.com/en/articles/20001275-chatgpt-work-and-codex
[cloud]: https://help.openai.com/en/articles/20001545-using-codex-cloud
[apps]: https://help.openai.com/en/articles/11487775-connected-apps-in-chatgpt
[projects]: https://learn.chatgpt.com/docs/projects
[dots]: https://learn.chatgpt.com/docs/dots/computers-and-apps
[modes]: https://learn.chatgpt.com/docs/environments/modes
[permissions]: https://learn.chatgpt.com/docs/permission-modes
