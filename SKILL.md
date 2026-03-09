---
name: generate-service-description
description: Generate or refresh a concise repo-level `service_description.md` by inspecting the codebase, runtime configuration, APIs, jobs, and integrations. Use when asked to create, update, validate, or improve a `service_description.md`, or when a repository needs a short service explainer that helps Codex and developers decide whether the repo is in scope for a change.
---

# Generate Service Description

## Overview

Generate a short, high-signal `service_description.md` for an application or service repository.
Base the document on local evidence from the repo rather than assumptions, and optimize for discovery, impact analysis, and fast triage.

## Workflow

1. Establish the service shape from obvious entry points.
- Read `README*`, `build.gradle*`, `settings.gradle*`, `pom.xml`, `Dockerfile*`, `application*.yml`, `application*.yaml`, and deployment/config files that reveal runtime, framework, ports, auth, topics, or external clients.
- Identify the language/framework, service name, base path, and whether the repo is API-only, worker-only, or mixed.

2. Map the public surface area.
- Inspect controllers, routers, GraphQL schemas, consumers, schedulers, and CLIs.
- Capture only the route families, event consumers/producers, job names, or command entry points that materially define what the service does.
- Prefer grouped summaries over exhaustive endpoint dumps.

3. Identify core ownership and data flow.
- Determine the main entities, workflows, and storage systems the service owns.
- Trace the high-level request or event flow from ingress to persistence to downstream publication.
- Call out the behavior that explains why the repo exists, not low-level implementation details.

4. Capture integrations and coupling.
- List significant downstream/upstream systems and why they are called.
- Include queues, topics, databases, search indexes, auth providers, and major internal dependencies when they shape change impact.
- Note likely cross-repo impact only when there is concrete evidence.

5. Draft `service_description.md`.
- Write for future discovery agents and developers, not end users.
- Keep the document concise, behavior-focused, and easy to scan.
- Use the section rubric in [references/service-description-rubric.md](./references/service-description-rubric.md).

6. Verify against the repo.
- Re-read the most important code/config sources and remove anything that is speculative.
- If an existing `service_description.md` is present, preserve useful sections but rewrite stale or vague content.
- Prefer omission over uncertain claims.

## Heuristics

- Prefer evidence from code and config over naming guesses.
- Prefer route families, jobs, and integrations over file-by-file implementation notes.
- Keep the purpose statement understandable in one paragraph.
- Keep ownership boundaries explicit: what this service owns, and what it delegates.
- Mention operational behavior only when it changes how the service should be modified or debugged.
- Avoid copying long config blocks, schema files, or controller listings verbatim.

## Fast Source Checklist

- Existing `service_description.md` files in sibling repos for style calibration
- `README*`
- `build.gradle*`, `pom.xml`, `settings.gradle*`
- `src/main/resources/application*.yml`
- controller/router packages
- client/integration packages
- scheduler/job/consumer/listener packages
- persistence/repository/model packages
- infra manifests only if they reveal public behavior or dependencies

## Output Rules

- Write or update exactly one repo-local `service_description.md` unless the user asks for more.
- Keep the document short enough to read in a few minutes.
- Favor headings and grouped bullets over dense prose.
- Include a maintenance section that says when the document should be updated.
- If the repo is not actually a service, adapt the title and purpose to the real unit of ownership instead of forcing microservice language.

## Reference

Read [references/service-description-rubric.md](./references/service-description-rubric.md) when drafting the document. It contains:
- a compact section template,
- guidance on what to include or skip,
- and a short checklist for keeping the file routing-focused rather than encyclopedic.
