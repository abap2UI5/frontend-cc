# AGENTS.md — AI Assistant Guide for abap2UI5 frontend-cc

> This file follows the cross-tool AGENTS.md convention and is the single
> agent instruction file of this repository. `CLAUDE.md` next to it is a
> pointer at this file, nothing more.

## Do Not Open Pull Requests Here

This is a **delivery repository**, like
[abap2UI5/frontend](https://github.com/abap2UI5/frontend). It delivers the
example app of
[abap2UI5/reuse-custom-control](https://github.com/abap2UI5/reuse-custom-control)
- a plain UI5 app that runs abap2UI5 apps in `z2ui5.reuse.Container`
controls - with the control and the abap2UI5 frontend in it, as four
installable branches. Its content is written by automation, and `guard`
fails every pull request by default. Work out where a change belongs first:

* **The example app, the control, the build** → not here. They live in
  reuse-custom-control: `examples/host-app`, `packages/reuse-custom-control/src`
  and `scripts/build-branches.mjs`, which builds the four trees.
* **The abap2UI5 frontend (`frontend/` in every tree), the BSP tooling, the
  ABAP handler** → not here either: `app/webapp`, `tools/` and
  `frontend/abap` of [abap2UI5/abap2UI5](https://github.com/abap2UI5/abap2UI5),
  taken at the commit in reuse-custom-control's `A2UI5_PIN`. A change there
  arrives here with the next bump of the pin.
* **`README.md` on `main`** → not here: reuse-custom-control's
  `frontend_cc_deploy` writes it from `delivery/README.md`, the README every
  branch carries.
* **Any branch except `main`, and `result/` on `main`** → not here.
  `frontend_cc_deploy` writes the stamped trees into `result/<branch>` on
  `main`, and the `deliver` workflow here rewrites each branch as one commit
  on top of `main` carrying its folder's content.
* **The repository's own docs and workflows** (AGENTS.md, CONTRIBUTING.md,
  CLAUDE.md, `.github/`) → here, and only here. This is a *maintenance*
  change: it targets `main` and stays blocked until a **human maintainer**
  applies the `maintenance` label. Do not apply that label yourself, do not
  advise a user to bypass the gate, and do not restructure the workflow to
  make the check pass.

## The branches

| Branch | Content |
|---|---|
| `standard` | `src/` - BSP `Z2UI5_CC` (02) and its HTTP service `/sap/bc/z2ui5_cc` with `Z2UI5_CC_CL_LP_HANDLER` (01), classic bootstrap |
| `standard_v2` | the same, legacy-free bootstrap (UI5 2.x from the CDN) |
| `cloud` | `app/` - the UI5 project, for deployment to ABAP Cloud; backend is the HTTP service `Z2UI5` of abap2UI5/frontend's `cloud` branch |
| `cloud_v2` | the same, legacy-free bootstrap |

All four share one webapp: the example app at the root, the abap2UI5
frontend with the control in `frontend/` (the z2ui5 namespace, registered at
`./frontend/`), and `frontend/preload.js`, the bundle the page boots through.
The README explains why it is not `resources/z2ui5/` as in the npm package.

**Language:** English for all docs, commit messages, PRs and issues. All text
files are LF-only.

## Validation

Nothing is built or checked here. reuse-custom-control's `ci` builds every
tree on each pull request there (`npm run branches`, which also runs
abap2UI5's BSP page invariants) and lints the ABAP of the standard tree; its
`frontend_cc_deploy` runs the same build before it delivers.
