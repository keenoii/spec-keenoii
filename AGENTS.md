# AGENTS GUIDELINES & INSTRUCTIONS

## 🚨 MANDATORY INSTRUCTION FOR ALL AI AGENTS
Every AI agent working in this repository MUST read and adhere strictly to:
1. [`START_HERE.md`](./START_HERE.md) - Project Onboarding & Workflow Guidelines
2. [`CONSTITUTION.md`](./CONSTITUTION.md) - AI Engineering Constitution (Config-Driven Modular Architecture with Single Source of Truth)

## Key Enforcement Rules:
- **Search Before Create**: Always search for existing components, services, types, hooks, or utilities before creating new ones.
- **Single Source of Truth**: Never duplicate configs, menus, routes, permissions, or schemas.
- **Config-Driven**: Move repeated and business variables to `src/config/` (`@/config/*`).
- **Modular Next.js Architecture**: Structure features under `src/modules/[feature]/` (`@/modules/*`) with dedicated `components/`, `services/`, `repositories/`, `schemas/`, `types/`, and `config/`.
- **UI Responsibility**: UI must only handle presentation, state, and user interactions. No direct DB queries or complex business logic in UI components.
- **Ask Before Assume**: Differentiate confirmed facts from assumptions. Ask for clarification when requirements are ambiguous.
