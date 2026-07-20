---
name: meeting-room
description: Use when the user invokes /Meeting-room or explicitly asks to start 会议室 with real virtual-team agents taking turns, questioning each other, and reaching decisions. During an active meeting, also use for /补充, /暂停, /继续, /纠正, /约束, /邀请, /散会, and @ROLE or @all responsibility assignment. Every participant must be a real sub-agent; never simulate meeting roles.
---

# Meeting Room

Run a structured multi-role meeting using real virtual-team agents. Keep the main agent as the host and coordinator only.

## Slash Command Invariant

Require an explicit supported slash command to change meeting state or the participant set. Before interpreting intent, read the leading token of the message or each separate command line.

```text
supported_commands = {
  /Meeting-room, /补充, /暂停, /继续,
  /纠正, /约束, /邀请, /散会
}

if leading_token not in supported_commands:
    do not change meeting state
    do not add or remove participants
```

Natural language without a supported leading slash command remains ordinary meeting content, even when its meaning resembles a command. Therefore `暂停一下` does not pause, `邀请 UI 加入` does not add UI, and `散会吧` does not end the meeting.

Treat the retired `+@ROLE` form as ordinary content containing an `@ROLE` responsibility tag. It must never add a participant. If that role is absent, follow the absent-role responsibility rule and do not spawn it.

## Shared Context Invariant

Keep all active meeting agents in one shared information context. For every user message received while the meeting is active, perform this sequence before any role-specific processing:

```text
active_agents = every spawned meeting agent that has not been closed
for each agent in active_agents:
    send_input(agent, complete_original_user_message)
```

Do not parse `@ROLE` tags before completing this broadcast. A message containing `@PM` is still sent in full to SA, TPM, QA, and every other active agent. Treat any stage-one recipient list smaller than `active_agents` as a protocol violation.

## Invocation

Treat `/Meeting-room` as the meeting-room invocation. Strip the prefix and use the remainder as the meeting topic.

## Mandatory Real-Agent Rule

- Spawn one real sub-agent for every selected participant.
- Never role-play, impersonate, or locally simulate PM, SA, TPM, UI, BE, FE, QA, SRE, or any other participant.
- Keep the main agent limited to agenda control, context relay, turn management, transcript presentation, synthesis, and agent cleanup.
- If multi-agent tools are unavailable, do not run the meeting. State that real-agent execution is unavailable.
- If a required role cannot be spawned, do not substitute a simulated role. Report the unavailable role and ask the user whether to remove or replace it.

Use these current virtual-team agent types:

- PM: `pm`
- SA: `sa`
- TPM: `tpm`
- UI: `ui`
- BE: `be`
- FE: `fe`
- QA: `qa`
- SRE: `sre`

## Role Selection

Use the roles named by the user. Otherwise choose the smallest useful group:

- Business extraction or rewrite discovery: PM, SA, TPM, QA.
- Requirement review: PM, TPM, QA, SA.
- Architecture review: SA, BE, FE, SRE, QA, TPM.
- UI or product experience review: PM, UI, FE, QA, TPM.
- Delivery readiness review: TPM, BE, FE, QA, SRE.
- Full review: PM, SA, TPM, UI, BE, FE, QA, SRE.

Explain any role added beyond the user's requested list before spawning it.

## Meeting Procedure

1. Build a meeting packet containing the topic, objective, background, constraints, participants, decision target, expected output, and round rules.
2. Spawn every selected role as a real sub-agent before opening statements begin.
3. Ask each agent independently for its opening position, evidence, risks, and questions.
4. Present each agent's labeled response to the user without replacing distinct viewpoints with one generic summary.
5. Send the combined transcript to all agents and collect cross-questions directed at named roles.
6. Route each question to its target agent and collect answers and revised positions.
7. For complex meetings, ask every agent for a final objection before locking decisions.
8. Have the host publish consensus, disagreements, decisions, risks, open questions, and action items.
9. Close all spawned agents after the meeting ends.

## Live User Intervention Protocol

Use explicit slash commands for meeting control under the Slash Command Invariant. Execute a command when it appears as the leading token of a user message or a separate command line and the context shows the user is issuing it. Do not execute slash text that is quoted, negated, shown as an example, or discussed as syntax.

Apply these commands:

- `/补充 <content>`: Add the content to shared meeting background. Broadcast it to all active agents and require later reasoning to incorporate it. Do not interrupt active work unless it invalidates that work.
- `/暂停 [reason]`: Stop opening new rounds and advancing decisions. Tell all active agents to hold, keep their sessions available, and wait for the user.
- `/继续 [content]`: Resume a paused meeting. Broadcast accumulated updates and optional content before starting the next round. If the meeting is not paused, treat the content as an instruction without changing state.
- `/纠正 <content>`: Mark the superseded fact or assumption as invalid, interrupt affected agents, relay the correction, and request revised conclusions.
- `/约束 <content>`: Add a hard requirement or boundary, interrupt conflicting work, and require an explicit compliance check in later responses.
- `/邀请 <ROLE...>`: Add and onboard one or more real role agents under Mid-Meeting Participant Addition.
- `/散会`: Broadcast the command, end the entire meeting, close every spawned agent, and publish the best available minutes including unresolved items. Ignore role tags; the host performs closure directly.

Allow one command per line and process multiple command lines in order. Ask a concise question when required command content or target roles are missing. Do not assign behavior to unknown slash commands.

## Visibility And Responsibility

Use `@PM`, `@SA`, `@TPM`, `@UI`, `@BE`, `@FE`, `@QA`, and `@SRE` to assign responsibility, not to create private messages. Match role tags case-insensitively and allow multiple tags in one message.

- Enforce the Shared Context Invariant above for every message. Never use role tags to filter the broadcast recipient list.
- Process each message in exactly two stages:
  1. Send the complete original user message, including its role tags, to every active agent.
  2. Parse role tags and send a separate responsibility instruction to each tagged active agent.
- The stage-one recipient list must always equal the complete active-participant list. This remains true when only one role is tagged or when a tagged role is absent.
- Treat tagged active agents as responsible responders. They must process the content associated with their tags and provide a response or action result.
- Treat untagged agents as informed observers. They may incorporate the message into later reasoning, but must not take over the tagged agent's assigned response unless the host requests collaboration.
- Treat `@all` case-insensitively as responsibility assignment to every currently active participant. It does not add missing roles and does not change the shared-visibility rule.
- For shared wording such as `@PM @SA 评估影响`, assign the same following content to both tagged roles.
- For separate clauses such as `@PM 梳理需求；@SA 评估架构`, assign each role its associated clause while still broadcasting the complete original message to everyone.
- When `@all` and role-specific clauses coexist, apply `@all` only to its associated clause and preserve each role-specific assignment. For example, `@all 阅读背景；@PM 更新需求` makes everyone responsible for reading the background and PM responsible for the update.
- Without a role tag, broadcast to everyone and let the host select responders from the meeting agenda and the message's meaning.
- Do not spawn a role merely because it was tagged. If the tagged role is not participating, still send the complete original message to every current participant, report that the responsible role is absent, and wait for direction.
- Preserve the original message in the shared transcript. Strip role tags only from the role-specific assignment sent to each responsible agent.
- For `/散会`, first send the complete original message to every active agent, then ignore every role tag and have the host close all agents directly.

Examples:

- With active PM, SA, TPM, and QA, `@PM 更新需求边界` is visible in full to PM, SA, TPM, and QA; only PM owns the requested update.
- With the same participants, `@all 检查自己的结论` is visible to and requires a response from PM, SA, TPM, and QA.
- With the same participants, `@UI 检查页面入口` is still visible in full to PM, SA, TPM, and QA; no agent owns the response because UI is absent, so the host reports the missing participant.

Before acting, briefly acknowledge the interpreted intent, responsible roles, shared visibility, and resulting meeting state. Keep a short intervention log for the final minutes.

## Mid-Meeting Participant Addition

Use `/邀请 ROLE` to add real virtual-team agents to the active meeting. Accept role names separated by spaces, commas, Chinese list separators, or repeated role arguments, such as `/邀请 UI`, `/邀请 UI FE`, or `/邀请 UI、FE`. Match supported role names case-insensitively.

For each addition request:

1. Broadcast the complete original user message to every existing active agent under the Shared Context Invariant.
2. Resolve every requested role against the supported real agent types.
3. Do not spawn a duplicate when a requested role is already active. Report that it is already present and treat any following substantive content as its assignment.
4. Spawn the requested real agent. If spawning fails or the role is unavailable, do not simulate it and do not add it to the participant list.
5. Send the new agent an onboarding packet containing the topic, objective, participants, original meeting packet, complete user interventions, material role statements, current transcript or faithful context, confirmed decisions, constraints, disagreements, open questions, and current meeting state.
6. Ask the new agent to acknowledge the context, identify any role-specific concern, and state whether existing conclusions need to be reopened.
7. Add the agent to `active_agents` only after successful spawning and onboarding. From then on, include it in every full-message broadcast.
8. Notify all participants that the new role joined and surface its first response to the user before continuing the next round.
9. Preserve the current state. Adding a participant while paused must not resume the meeting automatically.

A plain `@ROLE` assigns responsibility but never adds a missing participant. Only `/邀请 ROLE` adds one. Do not treat `+@ROLE` or a natural-language invitation without `/邀请` as an add-participant command.

## Symbol Vocabulary

- `/Meeting-room`: start the meeting-room plugin.
- `/补充`, `/暂停`, `/继续`, `/纠正`, `/约束`, `/散会`: control the active meeting.
- `/邀请 ROLE`: invite and onboard one or more real role agents during the meeting.
- `@ROLE`: make an active role responsible for the associated content; everyone still sees the full message.
- `@all`: make every active participant responsible for the associated content.

Do not support punctuation-only aliases or the retired `+@ROLE` invitation form.

## Host Rules

- Broadcast each complete user message to every active agent before interpreting or dispatching `@ROLE` assignments.
- Keep turns concise and labeled by role.
- Preserve meaningful disagreement and prevent repeated points.
- Separate facts, assumptions, opinions, and decisions.
- Keep participant output visible to the user throughout the meeting.
- Do not claim consensus until the real agents have seen the relevant transcript and responded.
- Do not continue past a user-confirmation checkpoint when one was requested.

## Final Minutes

```markdown
**Meeting Summary**
Topic:
Objective:
Participants:

**Consensus**
- ...

**Decisions**
- ...

**Disagreements**
- ...

**Risks**
- ...

**Open Questions**
- ...

**User Interventions**
- Intent, target roles, and impact on the meeting.

**Action Items**
- Owner: action, due/trigger if known.
```

Keep the minutes concise, but retain role-specific disagreements and unresolved questions.
