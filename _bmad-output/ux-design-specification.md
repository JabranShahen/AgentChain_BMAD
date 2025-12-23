---
stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8, 9]
inputDocuments:
  - "{project-root}/_bmad-output/prd.md"
workflowType: 'ux-design'
lastStep: 0
project_name: 'AgentChain'
user_name: 'Jabra'
date: '2025-12-22'
---
# UX Design Specification AgentChain

**Author:** Jabra
**Date:** 2025-12-22

---

<!-- UX design content will be appended sequentially through collaborative workflow steps -->

## Executive Summary

### Project Vision

AgentChain is a web-native, deterministic BMAD platform that exposes agent personas and workflows through a .NET API and a React UI. The UX emphasizes intentional, role-based interaction, menu-driven workflows, and inspectable, repeatable outcomes.

### Target Users

- **Primary:** BMAD-fluent technical users interacting with role-based agents (PM, Architect, Analyst, Dev, etc.).
- **Secondary:** Operators, support engineers, and API integrators who need traceability, diagnostics, and programmatic access.

### Key Design Challenges

- Make agent selection intentional and unambiguous (no generic “blank chat” entry).
- Preserve clarity of agent identity across sessions and workflows.
- Support fast, confident interaction for highly technical users (optimize for clarity and speed over onboarding).
- Keep UX desktop-first while ensuring mobile remains readable and functional.

### Design Opportunities

- Reinforce role-based intent with a clear agent catalog and pre-chat selection.
- Use menu-driven flows to reduce ambiguity and increase user confidence.
- Make sessions and outcomes inspectable to build trust.

### UX Principle: Intentional Agent Selection

AgentChain prioritizes intentional, role-based interaction over free-form exploration.  
Users should always know which agent they are interacting with and why before any conversation begins.

## Core User Experience

### Defining Experience

The core experience is intentional, role-based workflow initiation: users select a BMAD agent and start a structured workflow immediately. The dominant interaction is “choose the right agent and run the right workflow,” not free-form chat.

### Platform Strategy

- Web-only, desktop-first.
- No native mobile apps for MVP.
- No offline support; continuous connectivity assumed.
- Tooling platform focus: clarity and reliability over content consumption.

### Effortless Interactions

- Agent greeting and menu shown automatically on session start.
- Session created implicitly when interaction begins.
- Conversation history preserved per session.
- Menus reappear automatically on invalid or ambiguous input.
- Active agent/workflow state always visible.
- Unknown commands never execute; user receives a clear explanation.

### Critical Success Moments

- Landing → Agent selection (agents clearly visible, role intent obvious).
- Agent selected → Menu display (deterministic, understandable options).
- Menu choice → Workflow execution (selection resolves correctly).
- Workflow completion → Output (clear artifact, unambiguous success/failure).

If users must ask “Did that actually work?”, the experience fails.

### Experience Principles

- **Intentionality over exploration:** always choose an agent before interaction.
- **Guided confidence:** menus make actions explicit and predictable.
- **Determinism builds trust:** identical configs produce identical behavior.
- **Clarity over cleverness:** show state, show outcomes, avoid ambiguity.
- **User effort goes to decisions, not mechanics.**

## Desired Emotional Response

### Primary Emotional Goals

- **Clarity** on entry: users immediately understand what the system is and what they can do.
- **Confidence** in structure: the system feels intentional and well-designed.
- **Control** over action: users choose the agent and workflow, not the system.

### Emotional Journey Mapping

- **Landing:** clarity, confidence, control.
- **During workflow:** guided focus, trust, momentum.
- **After completion:** relief, satisfaction, confidence to reuse.

### Micro-Emotions

- Confidence vs confusion
- Trust vs skepticism
- Momentum vs stagnation
- Relief vs anxiety
- Satisfaction vs frustration

### Design Implications

- Strong role-based hierarchy to reinforce clarity and intent.
- Always-visible agent identity and workflow state.
- Deterministic menu behavior to build trust.
- Explicit progress and completion signals to maintain momentum.
- Clear error messaging to avoid anxiety.

### Emotional Design Principles

- **Intentionality over novelty:** this is a tool, not a toy.
- **Explainability builds trust:** show why and how outcomes occurred.
- **Reduce prompt anxiety:** guide choices instead of requiring invention.
- **Outcome confidence:** completion should feel decisive and useful.

## UX Pattern Analysis & Inspiration

### Inspiring Products Analysis

**GitHub (Issues / Projects / PRs)**  
- Strengths: explicit state, artifact-first workflows, visible audit trail, progressive disclosure.  
- Relevance: sessions ≈ issues, workflows ≈ PRs, transcripts ≈ audit trail.

**Linear**  
- Strengths: opinionated flows, low friction, minimal chrome, strong hierarchy.  
- Relevance: menu-driven interaction mirrors guided actions; constraints improve usability.

**VS Code**  
- Strengths: command-driven workflows, clear context, extensibility without chaos.  
- Relevance: agent menus ≈ command palette; agent context must always be visible.

### Transferable UX Patterns

- **Explicit state & outcomes:** always show status (running, succeeded, failed).  
- **Artifacts-first:** conversations tied to durable outputs.  
- **Progressive disclosure:** start simple, reveal detail on demand.  
- **Opinionated flows:** guide users to the “right” next step.  
- **Strong context cues:** always show active agent/workflow.

### Anti-Patterns to Avoid

- Blank chat entry with no context.  
- Hidden actions or ambiguous state.  
- Too many choices without guidance.  
- “Magic” outputs without traceability.

### Design Inspiration Strategy

**Adopt:**  
- Explicit state + artifacts-first (GitHub)  
- Opinionated guided flows (Linear)  
- Command/menu discovery (VS Code)

**Adapt:**  
- Progressive disclosure tuned for BMAD-fluent users.  
- Command palette concepts applied to agent menus.

**Avoid:**  
- Free-form prompt-first UI  
- Excess chrome or noisy UI that obscures intent

## Design System Foundation

### 1.1 Design System Choice

AgentChain will use a themeable, utility-first design system (Tailwind) as the foundation for the MVP. This balances speed of development with the ability to express a distinct, system-oriented visual identity.

### Rationale for Selection

- **Speed with control:** Tailwind enables rapid iteration without locking the UI into pre-opinionated patterns.
- **Palette alignment:** The existing role-based color palette maps cleanly into semantic tokens.
- **Developer-friendly:** Utility-first approach fits a highly technical team and reduces design ops overhead.
- **Future-proof:** A light token layer allows later evolution into a formal design system.

### Implementation Approach

- Use Tailwind as the base styling system.
- Define semantic tokens for roles, states, and UI surfaces.
- Keep components composable and lightweight for fast iteration.

### Customization Strategy

- Apply the provided palette as semantic tokens (role colors, state colors, surface levels).
- Ensure tokens support future light/dark variants and WCAG AA contrast.
- Avoid heavy component theming until patterns stabilize.

## 2. Core User Experience

### 2.1 Defining Experience

AgentChain is where users deliberately choose a role-based agent, run a guided workflow, and walk away with a concrete outcome — without guessing what to type or wondering what happened.  
“It’s like running a trusted playbook through an agent instead of prompting a chatbot.”

### 2.2 User Mental Model

**How users solve this today:**
- CLI/Codex interaction, ad-hoc prompts, copy/paste across tools.
- Users feel they must guess the right prompt and hope for consistent behavior.

**Mental model users bring into AgentChain:**
- Tool-like behavior, explicit choices, visible state, repeatable outcomes.

**Desired mental model shift:**
“I choose the agent and workflow; the system handles the rest.”

### 2.3 Success Criteria

Users say “this just works” when:
- The right agent is obvious at the start.
- Menus clearly show available actions.
- Workflows start and complete without retries.
- Outcomes are clear, usable, and inspectable.
- Errors are explicit and explainable.

### 2.4 Novel UX Patterns

This experience relies on established patterns:
- Menu-driven actions (command palette style).
- Guided workflows.
- Explicit state + completion signals.
- Artifact-first outcomes.

Minimal novelty:
- Agents are role-based systems with explicit menus/workflows (not free-form chat partners).

No novel interaction mechanics required.

### 2.5 Experience Mechanics

**Initiation:**
- User lands on AgentChain.
- Role-based agent options are visible immediately.
- User intentionally selects an agent; no blank chat.

**Interaction:**
- Agent greets in menu mode and displays actions.
- User selects a menu item (click or labeled option).
- Agent guides through a defined workflow with minimal questions.

**Feedback:**
- Active agent and workflow are always visible.
- Progress is shown step-by-step.
- Visual cues indicate activity, transitions, and waiting states.

**Completion:**
- Clear completion signal with success state.
- Output artifact is visible and usable.
- User can refine, save, reset, or start another workflow.
- Session remains inspectable and reusable.

## Visual Design Foundation

### Color System

- Use the provided role-based palette as semantic tokens (agent roles, states, surfaces).
- Emphasize high contrast and clear state signaling (active, success, error).
- Adjust tones as needed to ensure WCAG 2.1 AA compliance.

**Palette anchors (starting point):**
- Blues: #00AEEF, #0095D5, #4E7DA6, #2E4A62, #1F2A36
- Purples: #9B8CFF, #8B7FE6
- Yellows/Golds: #FFC933, #E0B432
- Greens: #4CD137, #44BD32
- Neutrals: #F5F6FA, #DCDDE1, #718093, #192A56
- Errors/Accents: #E84118, #C23616

### Typography System

**Tone:** professional, technical, utilitarian (developer tool / system console).  
**Primary font:** Inter (preferred), or Source Sans 3 / IBM Plex Sans.  
**Secondary mono:** JetBrains Mono or IBM Plex Mono for transcripts/technical output.  
**Content density:** short to medium text; optimize for scanability, clarity, hierarchy.

### Spacing & Layout Foundation

- Layout density: efficient and compact, not airy.  
- Spacing base unit: 8px.  
- Grid system: 12-column.  
- Avoid oversized cards and excessive padding; prioritize information density.

### Accessibility Considerations

- Maintain WCAG 2.1 AA contrast across all text and interactive elements.
- Ensure focus states are visible and consistent.
- Font sizes and line heights optimized for scanability in dense layouts.

## Design Direction Decision

### Design Directions Explored

- **A:** Console Grid (dashboard grid + workflow rail)
- **B:** Command Deck (minimal chrome, command-palette feel)
- **C:** Workflow Focus (single-column step flow)
- **D:** Catalog First (agent selection dominant)
- **E:** Split Pane Terminal (left intent, right outcomes)
- **F:** Inspector Mode (state/prompt/workflow panel)

### Chosen Direction

**Primary:** D + E  
**Influence:** B (minimal chrome), F (optional inspector panels)

### Design Rationale

- **D (Catalog First)** enforces intentional agent selection and role clarity.  
- **E (Split Pane Terminal)** mirrors the defining experience:  
  left = intent/control, right = evidence/outcome.  
- **B influence** keeps the UI restrained, dense, and tool-like.  
- **F influence** supports operator/support needs via optional inspector panels.

### Implementation Approach

- Primary layout: catalog + workflow controls on the left, transcript/artifacts on the right.  
- Minimal chrome and strong hierarchy; keep focus on agent/menu/workflow state.  
- Inspector panel as a toggleable side panel or secondary mode.

