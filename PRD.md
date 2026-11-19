# Jenesis — Product Requirements Document (PRD)

**Document status:** Product baseline  
**Version:** 1.0  
**Last updated:** 19 November 2026  
**Repository:** `david-nunoo-afrane/Jenesis`  
**Primary platform:** Android  
**Companion platform:** Responsive Progressive Web App (PWA), planned after the Android foundation

---

## 1. Executive summary

Jenesis is an AI-powered personal life operating system. It helps a person organise information and responsibilities across everyday life, understand relevant context, make better decisions, and follow through on commitments.

**Product promise:** Jenesis helps the user remember what matters, understand what is happening, decide what to do next, and follow through — with the user's permission and control.

Jenesis is not intended to be only a chatbot, calendar, notes app, or habit tracker. It is a connected personal assistant whose value comes from combining useful context across life categories while preserving user agency, privacy, and transparency.

The product will use a **hybrid AI architecture**: cloud AI for tasks that benefit from stronger models and connectivity, and on-device AI where device capability, model quality, and privacy requirements make local processing practical. The first release must not depend on on-device model execution.

The initial implementation prioritises an Android application. A PWA will follow as a companion experience. Both platforms should share the same account, backend, data model, AI orchestration, integrations, and synchronisation layer.

## 2. Vision, mission, and product principles

### 2.1 Vision

Make personal organisation and follow-through feel coherent: one trusted place that understands the user's context across life, without taking control away from them.

### 2.2 Mission

Help users capture, organise, retrieve, understand, plan, and act on personal information through a context-aware assistant and connected life-management tools.

### 2.3 Product principles

1. **User control first.** The user decides what Jenesis can access, remember, automate, and change.
2. **Useful context, not indiscriminate collection.** Store only information that has a clear purpose and an appropriate retention basis.
3. **One coherent experience.** Life categories should work together without becoming a cluttered collection of disconnected apps.
4. **Proactive, not noisy.** Notifications should be timely, relevant, explainable, and configurable.
5. **Honest AI.** Distinguish known facts, estimates, suggestions, and actions. Never claim an action succeeded until the system confirms it.
6. **Privacy and security by design.** Enforce permissions in application code and backend policy, not merely through model instructions.
7. **Accessible and dependable.** Prioritise clear language, responsive layouts, offline tolerance, and recoverable errors.
8. **Incremental delivery.** Ship a reliable core before adding advanced automation, integrations, or local models.

## 3. Users and jobs to be done

### 3.1 Primary user

A person who wants help managing the moving parts of everyday life: schedules, tasks, learning, goals, notes, relationships, finances, and relevant environmental or device context.

The product should be understandable to a non-technical user while remaining capable enough to support complex workflows over time.

### 3.2 Core jobs

- Capture a thought, task, event, reminder, or piece of information quickly.
- Ask questions and receive answers informed by relevant personal context.
- Remember important details across conversations and retrieve them later.
- See what is coming up and decide what deserves attention.
- Track goals and routines without maintaining several disconnected tools.
- Receive useful alerts when something important changes.
- Review, correct, export, or delete personal information.
- Understand when AI is making an inference or proposing an action.

## 4. Scope and release priorities

Priorities use the following definitions:

- **P0 — Core release:** required for the first dependable Android release.
- **P1 — Expansion:** valuable capabilities added after the core is stable.
- **P2 — Advanced:** capabilities that depend on stronger infrastructure, permissions, device support, or validated demand.

### 4.1 P0 — First usable Android release

- Account creation, sign-in, sign-out, and account recovery.
- Minimal app shell and adaptive navigation.
- Home dashboard with a useful overview and quick capture.
- AI assistant connected through a secure backend.
- Persistent, categorised memory with user review and correction.
- Basic tasks, events, and reminders.
- Weather information and configurable meaningful-change alerts, subject to a reliable provider and location permission.
- Notification preferences and permission explanations.
- Privacy controls and explicit approval for consequential actions.
- Local cache, basic offline viewing/capture where feasible, and reliable sync.
- Loading, empty, offline, permission-denied, and error states.
- Automated tests for critical flows and backend access controls.

### 4.2 P1 — Life modules and broader access

- Academics and learning workspace.
- Goals, milestones, and habits.
- Notes, knowledge, and project organisation.
- People and relationship context.
- Personal finance records and budgeting support.
- Voice capture and voice interaction.
- PWA companion with shared account and data.
- More advanced reminders and user-configured automations.

### 4.3 P2 — Advanced intelligence and integrations

- On-device language models and local inference where supported.
- More capable multimodal input and understanding.
- Deeper third-party integrations.
- Android device diagnostics and device-context features.
- Advanced proactive recommendations and multi-step workflows.

P2 items must not be represented as universally available. Capability depends on device hardware, Android version, permissions, provider availability, and user settings.

## 5. Experience architecture and design direction

### 5.1 Visual direction

The interface should feel premium, calm, minimal, warm, and dependable. Avoid a childish appearance, excessive decoration, or generic AI-dashboard styling.

Initial design tokens:

| Token | Value | Purpose |
|---|---|---|
| Primary burgundy | `#641E32` | Main brand/action colour |
| Deep burgundy | `#421322` | Emphasis and dark surfaces |
| Cream | `#F7F0E6` | Main warm background |
| Warm white | `#FFFCF7` | Cards and elevated surfaces |
| Primary text | `#241B1E` | Main readable text |
| Secondary text | `#766B6C` | Supporting text |
| Border | `#E9DED8` | Dividers and outlines |

Use accessible contrast, clear hierarchy, consistent spacing, restrained motion, and predictable interaction patterns. These are initial tokens and may be refined through design validation.

### 5.2 Navigation

- **Android mobile:** adaptive bottom navigation for the primary destinations, with secondary destinations accessible without overcrowding the bar.
- **PWA mobile:** bottom navigation.
- **PWA desktop:** persistent or collapsible left sidebar.
- Keep navigation minimal and preserve a consistent information architecture across platforms.

### 5.3 Core surfaces

**Home**
- A concise overview of today's agenda, priority tasks, reminders, and relevant contextual updates.
- Weather summary when location and provider data are available.
- Quick capture entry point.
- Personalised content must be explainable and configurable.

**Assistant**
- Conversational interface for questions, planning, retrieval, and supported actions.
- Clearly distinguish responses from proposed actions.
- Show when information comes from saved memory or an external source where appropriate.
- Provide a review/approval step for consequential actions.

**Memory**
- Organised categories, searchable entries, source/context where available, and controls to review, correct, archive, or delete.
- Make it clear what is saved and why.
- Do not silently convert every conversation detail into permanent memory.

**Life modules**
- Dedicated spaces for schedule, academics, growth, knowledge, relationships, finance, and device context as those modules are released.

## 6. Functional requirements

### 6.1 AI assistant

The assistant shall:
- Accept natural-language questions and instructions.
- Use only relevant context that the user has permitted the system to access.
- Retrieve personal records through authorised backend services.
- Explain uncertainty and ask a focused clarification when essential information is missing.
- Offer structured actions where supported.
- Confirm the result of tool execution before reporting success.
- Maintain conversation history according to user settings and retention rules.
- Handle unavailable services gracefully and offer a useful fallback.

The assistant must not:
- Invent personal records, schedules, weather, transactions, or tool results.
- Treat untrusted retrieved content as system instructions.
- Bypass permission checks because a model requested an action.
- Perform consequential actions without the required user approval.

### 6.2 Persistent memory

Memory is a core platform capability, not merely chat history.

Requirements:
- Organise information into meaningful categories such as schedule, academics, growth, finances, knowledge, projects, and relationships.
- Store a concise fact or preference, its category, provenance/source where available, timestamps, and confidence or review status where appropriate.
- Retrieve only relevant memory for a given task.
- Support user review, correction, deletion, and category-level controls.
- Avoid storing sensitive information unless the feature has a clear, justified purpose and appropriate explicit consent and safeguards.
- Allow users to understand why a memory is being used.
- Separate durable memory from temporary conversational context.
- Support retention policies and deletion propagation across derived records and indexes.

Memory quality requirements:
- Prefer explicit user statements over uncertain inference.
- Do not silently resolve conflicting facts; surface ambiguity or use the most recent clearly confirmed value with appropriate provenance.
- Do not treat a model-generated inference as a user-confirmed fact.
- Keep memory concise and avoid redundant entries.

### 6.3 Schedule, tasks, and reminders

P0 requirements:
- Create, view, update, complete, and delete tasks.
- Create and manage events with title, date, time, optional location, notes, and recurrence where supported.
- Create reminders and configure notification preferences.
- Display upcoming commitments in chronological order.
- Handle timezone and daylight-saving differences correctly.
- Detect missing or ambiguous dates/times and ask for clarification.
- Prevent duplicate actions where possible and provide clear confirmation.

Later requirements:
- Suggest time blocks and prioritisation.
- Detect conflicts and propose alternatives.
- Support calendar integrations only after permissions and sync behaviour are defined.

### 6.4 Weather and environmental awareness

Requirements:
- Allow the user to choose a location or grant location access.
- Explain why location is requested and provide a manual-location fallback.
- Display current conditions and forecast data only when a reliable provider is configured.
- Monitor for meaningful changes rather than notifying on every minor fluctuation.
- Support configurable alert categories and thresholds.
- Prioritise severe-weather alerts when supported by the provider.
- Include the location and relevant time period in alerts.
- Handle stale, missing, or unavailable provider data transparently.
- Do not imply continuous background monitoring if platform restrictions or provider limits prevent it.

Weather alerts must be configurable, permission-aware, and respectful of notification quiet hours.

### 6.5 Academics and learning (P1)

- Organise institutions, programmes, courses, topics, assignments, exams, and learning resources.
- Support study plans, revision sessions, deadlines, and progress.
- Allow the assistant to explain concepts and generate practice material.
- Keep source material and user-created notes distinguishable.
- Avoid presenting generated academic content as authoritative without verification.

### 6.6 Growth, goals, and habits (P1)

- Create goals with descriptions, target dates, milestones, and progress.
- Create recurring habits and log completion.
- Display progress without shaming language.
- Let users pause, edit, or archive goals and habits.
- Offer suggestions based on user-approved context.

### 6.7 Knowledge, notes, and projects (P1)

- Capture and organise notes, ideas, links, and project information.
- Support search and contextual retrieval.
- Link related notes and projects where useful.
- Preserve source references for imported information.
- Provide export and deletion controls.

### 6.8 People and relationships (P1)

- Allow users to maintain voluntarily supplied contact context, important dates, and follow-up reminders.
- Keep relationship information private and user-controlled.
- Do not infer sensitive traits or make manipulative recommendations.
- Do not contact people on the user's behalf without explicit approval.

### 6.9 Personal finance (P1)

- Support manual recording and categorisation of income, expenses, budgets, and savings goals.
- Make calculations transparent and allow correction.
- Treat financial information as sensitive.
- Do not initiate transfers, payments, or purchases.
- Any future financial integrations require explicit opt-in, secure provider authorisation, and clear revocation controls.

### 6.10 Device intelligence (P2)

Where Android APIs, hardware, and permissions allow, provide useful device information such as battery status, connectivity, storage, and selected diagnostics.

- Explain each permission and why it is needed.
- Collect the minimum information required.
- Clearly label unavailable or unsupported capabilities.
- Do not imply access to restricted system, SIM, carrier, or device data.
- Never bypass Android security boundaries or user consent.

## 7. Hybrid AI architecture

### 7.1 Architecture principle

Use cloud AI and on-device AI as complementary execution paths behind a common orchestration layer.

**Cloud AI**
- Primary path for the initial release.
- Handles complex reasoning, long-context tasks, and capabilities not practical locally.
- All provider credentials remain on the server.
- Requests should be minimised and scoped to relevant context.

**On-device AI**
- Introduced later when supported by device capability and model quality.
- Suitable for selected offline, low-latency, or privacy-sensitive tasks.
- Must have clear fallback behaviour when local execution is unavailable.
- Must not be a prerequisite for core product functionality.

### 7.2 AI orchestration

The orchestration layer shall:
1. Receive the user's request.
2. Identify intent and the minimum required context.
3. Check permissions and consent.
4. Retrieve authorised memory and records.
5. Select an appropriate model or deterministic service.
6. Validate any proposed tool call against a server-side allowlist and schema.
7. Require approval for actions classified as consequential.
8. Execute permitted actions.
9. Verify the outcome.
10. Return a transparent result and record an appropriate audit event.

Model output is untrusted input. The backend, not the model, is the authority for identity, permissions, validation, and action execution.

### 7.3 Provider independence

Use a provider adapter so model vendors can be changed without rewriting product features. Track provider availability, latency, errors, and cost. Avoid unnecessary vendor lock-in.

## 8. Autonomy and approval policy

Actions should be classified by risk.

- **Read-only:** retrieve or summarise authorised information.
- **Low-impact reversible:** create or update a draft, task, or note when the user has enabled that behaviour.
- **Consequential:** send a message, share information, make a payment, book or purchase something, submit a form, or make an externally visible change.
- **Destructive:** permanently delete important data, revoke access, or perform an irreversible operation.

Rules:
- Read-only actions may proceed within granted permissions.
- Low-impact actions may proceed only within clearly configured user preferences and must be logged.
- Consequential actions require explicit, informed confirmation immediately before execution.
- Destructive actions require explicit confirmation and a clear explanation of consequences; use a recovery window where feasible.
- No hidden or implied authorisation.
- The user must be able to inspect pending approvals and revoke future permissions.

## 9. Privacy, security, and governance

Security is a release requirement, not a later enhancement.

### 9.1 Authentication and authorisation
- Use a reputable authentication service.
- Enforce row-level access controls on user-owned data.
- Verify identity and permissions server-side for every protected operation.
- Never trust client-supplied user IDs as proof of ownership.

### 9.2 Secrets and provider credentials
- Store AI provider keys and privileged credentials only in server-side secret storage.
- Never embed privileged keys in the Android application or PWA bundle.
- Rotate exposed credentials and document environment configuration.

### 9.3 Data protection
- Minimise collection and retention.
- Encrypt data in transit and use platform/provider encryption at rest.
- Avoid logging sensitive message content, credentials, or unnecessary personal data.
- Provide clear privacy disclosures and consent flows.
- Support data export and account deletion.
- Propagate deletion to derived memory, search indexes, and caches where applicable.

### 9.4 AI-specific security
- Treat user uploads, retrieved pages, integrations, and tool outputs as untrusted.
- Defend against prompt injection and data exfiltration.
- Validate tool arguments against strict schemas.
- Apply least-privilege access to tools.
- Keep an audit trail for sensitive operations.
- Never let model text override backend policy.

### 9.5 User controls
Users must be able to:
- Review and correct saved memory.
- Disable or limit categories of memory.
- Control location and notification permissions.
- Review connected integrations and revoke access.
- Review pending and completed consequential actions.
- Export or delete their data.

## 10. Data architecture — conceptual entities

The implementation may refine names and relationships, but the data model should account for:

- **Profile:** account preferences, timezone, locale, and settings.
- **Conversation / Message:** assistant and user conversation history.
- **Memory / Memory source:** categorised durable facts, provenance, confidence/review state, and lifecycle.
- **Task:** actionable item, status, priority, due date, and ownership.
- **Event:** scheduled commitment, time range, timezone, recurrence, and location.
- **Reminder:** trigger, delivery channel, and notification state.
- **Goal / Milestone:** desired outcome, target, and progress.
- **Habit / Habit entry:** recurring behaviour and completion records.
- **Note / Project:** knowledge items and project context.
- **Course / Learning item:** academic organisation and progress.
- **Person:** user-supplied relationship context and follow-up details.
- **Transaction / Budget:** user-entered financial records and limits.
- **Location:** saved or temporary location with consent and purpose.
- **Notification preference:** categories, thresholds, quiet hours, and channels.
- **Integration / Permission:** external connection and granted scopes.
- **Approval:** proposed action, risk class, decision, and expiry.
- **Tool execution:** validated request, execution state, and verified result.
- **Audit event:** security- and action-relevant history.
- **Sync metadata:** versioning, conflict handling, and sync state.

All user-owned records must have explicit ownership and access-control rules. Avoid storing duplicated personal data when a reference will suffice.

## 11. Notifications and proactive intelligence

Notifications should help users act, not compete for attention.

Requirements:
- User-configurable categories, quiet hours, and delivery preferences.
- Deduplication and sensible rate limits.
- Meaningful thresholds for changing conditions.
- Clear title, context, timestamp, and suggested next step where useful.
- Deep links to the relevant Jenesis screen.
- Respect operating-system notification permissions.
- Graceful behaviour when background execution is restricted.
- No notification should imply a completed action unless completion is verified.

## 12. Platform requirements

### 12.1 Android — primary platform

Preferred implementation:
- Kotlin.
- Jetpack Compose.
- Room for local persistence and offline-friendly data.
- WorkManager for deferrable background work.
- Android notification APIs for reminders and alerts.
- Secure storage for appropriate local credentials/tokens.
- Repository and service layers to keep UI separate from business logic.

Requirements:
- Support a clearly defined minimum Android version after device testing.
- Adapt to different screen sizes and accessibility settings.
- Request runtime permissions only when needed and explain them.
- Handle process death, connectivity loss, and background restrictions.
- Keep secrets out of the client.
- Use a reliable sync strategy with conflict handling.

### 12.2 PWA — companion platform

Planned implementation:
- Responsive web application with installable PWA behaviour.
- Shared authentication, backend, AI orchestration, and data model.
- Bottom navigation on mobile and sidebar on desktop.
- Offline caching only for data that is safe and useful to retain locally.
- Clearly communicate browser limitations for background work, notifications, and device access.

The PWA must not claim parity with Android capabilities that browsers do not expose.

## 13. Non-functional requirements

- **Reliability:** core navigation and saved records should remain usable during temporary network failures where cached data is available.
- **Performance:** prioritise fast app launch, responsive navigation, and progressive loading.
- **Accessibility:** readable typography, sufficient contrast, screen-reader labels, scalable text, and touch targets.
- **Maintainability:** modular architecture, documented interfaces, and automated checks.
- **Scalability:** data ownership and service boundaries should support additional modules without a rewrite.
- **Observability:** structured error reporting and operational metrics without leaking sensitive content.
- **Portability:** provider adapters and documented deployment configuration.
- **Cost control:** quotas, usage tracking, caching where appropriate, model routing, and limits on expensive operations.

Initial performance targets should be established through baseline testing rather than treated as guarantees before measurement.

## 14. Integrations

Integrations should be introduced only when they materially improve a user workflow.

For each integration:
- Explain the value and data requested.
- Request only necessary scopes.
- Store tokens securely on the backend where possible.
- Provide disconnect and revocation controls.
- Handle provider outages, rate limits, and revoked credentials.
- Do not send data to an integration without the user's permission.

Potential future categories include calendars, email, cloud storage, weather, maps, and financial data providers. No specific provider is mandatory for the initial architecture.

## 15. Analytics and success measures

Measure product usefulness and reliability, not merely engagement volume.

Candidate metrics:
- Successful onboarding and first-value completion.
- Successful creation and retrieval of tasks, events, and memories.
- Memory correction and deletion success.
- Reminder delivery and action completion rates.
- Weather alert relevance and opt-out rates.
- Assistant task completion rate and verified tool success rate.
- Error rate, crash-free sessions, sync success, and latency.
- User trust signals, including permission revocation and privacy-control usage.
- AI cost per active user and cost per completed task.

Analytics must be privacy-conscious, documented, and avoid collecting sensitive content unnecessarily.

## 16. Delivery roadmap

### Phase 0 — Foundation
- Confirm repository structure, engineering conventions, and build pipeline.
- Establish Android project, design tokens, app shell, and navigation.
- Configure backend environments, authentication, and access controls.
- Add automated formatting, linting, and tests.

**Exit criteria:** clean build, working authentication flow, documented setup, and verified user-data isolation.

### Phase 1 — Core personal assistant
- Implement assistant interface and secure server-side AI gateway.
- Add conversation persistence.
- Add categorised memory with review/correction controls.
- Add tasks, events, and reminders.
- Add home dashboard and quick capture.

**Exit criteria:** user can capture, retrieve, and manage core information; AI can use permitted context; sensitive actions are gated.

### Phase 2 — Context and dependable alerts
- Add weather provider adapter and location settings.
- Add meaningful-change thresholds and notification preferences.
- Improve offline cache and sync recovery.
- Expand tests, observability, and security review.

**Exit criteria:** weather data is clearly timestamped, alerts respect permissions/settings, and offline/error states are understandable.

### Phase 3 — Life modules
- Add academics, growth, knowledge, relationships, and finance in prioritised increments.
- Validate each module with real workflows before broadening scope.

### Phase 4 — PWA companion
- Deliver responsive mobile and desktop PWA.
- Reuse backend contracts and shared data.
- Document browser-specific limitations.

### Phase 5 — Advanced intelligence
- Evaluate local models and on-device processing.
- Add deeper integrations and device intelligence only after security, feasibility, and user value reviews.

## 17. Testing and definition of done

A feature is not complete merely because its primary screen renders.

Each feature should include:
- Unit tests for business rules and validation.
- Integration tests for repositories, backend services, and permissions.
- UI tests for critical user journeys.
- Loading, empty, error, offline, and permission-denied states.
- Accessibility checks.
- Security review appropriate to the data and action risk.
- Documentation for setup, configuration, and operational behaviour.

Critical end-to-end journeys:
1. Create an account and complete onboarding.
2. Capture a task and retrieve it later.
3. Create an event and receive its reminder when permitted.
4. Save, inspect, correct, and delete a memory.
5. Ask the assistant a question requiring authorised personal context.
6. Attempt an unauthorised action and verify it is blocked.
7. Lose connectivity and recover without silently losing saved work.
8. Configure or disable weather alerts and location access.
9. Export or delete account data through supported controls.

## 18. Risks and mitigations

| Risk | Mitigation |
|---|---|
| Scope becomes too broad | Enforce P0/P1/P2 priorities and release gates |
| AI produces inaccurate personal claims | Ground answers in retrieved records, expose uncertainty, and allow correction |
| Sensitive data is exposed | Server-side authorisation, RLS, minimisation, secret management, and security tests |
| AI provider costs become unsustainable | Usage limits, routing, caching, monitoring, and provider abstraction |
| Background work is restricted by Android | Use supported APIs, explain limitations, and avoid promising continuous execution |
| Weather data is stale or unavailable | Timestamp data, show provider status, and suppress unsupported alerts |
| Offline edits conflict | Version records, define conflict resolution, and make sync status visible |
| Integrations increase attack surface | Least privilege, explicit consent, token security, and revocation |
| Too many notifications reduce trust | Meaningful thresholds, deduplication, quiet hours, and user controls |

## 19. Assumptions and open decisions

The following should be confirmed during implementation rather than silently assumed:
- Exact minimum Android version and supported device matrix.
- Final backend deployment and environment strategy.
- Initial AI provider and cost/usage limits.
- Weather provider, coverage, and alert capabilities for target locations.
- Exact PWA delivery timing.
- Data retention defaults and account-deletion propagation details.
- Whether any integrations are required for the first public release.
- Accessibility and localisation requirements for the first release.

The project should prefer free tiers and open-source tools where practical, but must not compromise security or reliability to avoid a small operational cost. Any service with usage limits or pricing changes must be documented.

## 20. Repository and engineering governance

- This PRD defines product intent and scope; it does not replace technical architecture, database, security, or implementation documents.
- Keep separate maintained documents for architecture, database schema, security, roadmap, and agent/developer instructions as the codebase matures.
- Every implementation task should reference the relevant requirement and include acceptance criteria.
- Agents must inspect existing code before changing it.
- Avoid multiple agents editing the same files concurrently.
- Use small, reviewable changes and run relevant tests before merging.
- Never commit secrets, private keys, production tokens, or real personal data.
- Record important architectural decisions and reasons in an ADR (Architecture Decision Record).
- Update documentation when behaviour or interfaces change.

## 21. Public beta acceptance criteria

A public beta should not be declared ready until:
- Authentication and user-data isolation have been tested.
- P0 journeys work on the supported Android device matrix.
- Memory is reviewable and correctable.
- Assistant tool execution is permission-checked and verified.
- Consequential actions require explicit confirmation.
- Notifications respect user and OS settings.
- Weather and other external data are timestamped and failure-aware.
- Offline and sync behaviour is tested and documented.
- Critical defects are resolved or explicitly accepted.
- Privacy disclosures, support path, and data export/deletion behaviour are available.
- A backup, recovery, and incident-response approach exists for production data.

## 22. Product definition of success

Jenesis succeeds when users can trust it as a useful, coherent companion for everyday life: it remembers only what is appropriate, retrieves the right context, helps users decide what to do, and follows through accurately when authorised.

The measure of success is not how much the assistant speaks or how many features exist. It is whether the product consistently reduces friction, improves follow-through, and preserves user trust.

---

## Appendix A — Requirement priority index

| Capability | Priority |
|---|---|
| Authentication and account | P0 |
| App shell, navigation, and home | P0 |
| Secure cloud AI assistant | P0 |
| Categorised persistent memory | P0 |
| Tasks, events, reminders | P0 |
| Weather and meaningful alerts | P0, provider-dependent |
| Privacy, permissions, and approvals | P0 |
| Offline cache and sync foundations | P0 |
| Academics and learning | P1 |
| Goals and habits | P1 |
| Notes, knowledge, and projects | P1 |
| People and relationships | P1 |
| Personal finance | P1 |
| Voice interaction | P1 |
| PWA companion | P1 |
| On-device AI | P2 |
| Advanced multimodal workflows | P2 |
| Deep device intelligence | P2 |
| Advanced third-party integrations | P2 |

## Appendix B — Glossary

- **Durable memory:** user information intentionally retained beyond a single conversation.
- **Context retrieval:** selecting relevant authorised information to support a request.
- **Orchestration layer:** service that coordinates models, data retrieval, tools, permissions, and verification.
- **PWA:** Progressive Web App, an installable web application with browser-defined capabilities.
- **RLS:** Row-Level Security, database policies that restrict which records a user can access.
- **Consequential action:** an action that affects another person, an external service, money, privacy, or an important/irreversible record.
- **Verified result:** an outcome confirmed by the system or destination service, not merely claimed by a model.
