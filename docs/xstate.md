# Links:
  - [XState Docs](https://xstate.js.org/docs/)
  - [React Hooks for XState](https://github.com/statelyai/xstate/tree/main/packages/xstate-react)

The point of using a state machine here is to simplify reasoning about the page state.  Most React frontends that don't tackle state in a sane way end up with hacky solutions involving arcane logic combinations and frequent bugs and regressions.

The biggest impact on me was reading the part of the article "[Guidelines for State Machines and XState](https://kyleshevlin.com/guidelines-for-state-machines-and-xstate#why-booleans-are-a-misguided-approach)". This helped me understand the core case for using XState.

Building went smoothly after taking time to first [diagram out the expected state](https://drive.google.com/file/d/1h4CYZMlyiMd9dfZMvM1M_BOakN-ZMfTJ/view?usp=sharing), then validate it with the [xstate visualizer tool](https://stately.ai/viz/5c89a732-fc17-4716-aaad-957d0b7487fa#)
Refactoring involved taking values created by `setState` and updated with `useEffect` and migrating them to the xstate machine, in stages:

1. Button UI
2. Initializing the editor for new documents and existing ones
3. Retrieving existing documents

--- 

There is a perspective that is being developed while working on this project and reading more XState content:

State machines can help clarify both the internal state of the user interface, and the **visual state** of the user interface.

---

A good line of inquiry when building with XState in complex frontends is, "What needs to be stable while other things change? Something? Nothing?" This will expose what can be nested and what should be parallel.

---

My favorite part of using Xstate is the refactoring.  Once the inventory of intended events is built in and the UI is hooked up with `send` statements, any refactors in the state machine that keep the inventory of possible events intact will likely be limited to the frontend only.

for code examples:
src/ListingEditor/ListingEditorMachine.ts
f79c4146818ad5e51eeaec3460118a14bf87fe1e before refactor
d66300c after refactor


