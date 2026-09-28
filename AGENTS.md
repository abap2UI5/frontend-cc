# AGENTS.md — AI Assistant Guide for abap2UI5 frontend-embed-control

> This file follows the cross-tool AGENTS.md convention and is the single
> agent instruction file of this repository. `CLAUDE.md` next to it is a
> pointer at this file, nothing more.

## Do Not Open Pull Requests Here

This is a **delivery repository**, like
[abap2UI5/frontend](https://github.com/abap2UI5/frontend). It delivers the
example app of
[abap2UI5/embed-control](https://github.com/abap2UI5/embed-control) - a
plain UI5 app that runs abap2UI5 apps in `z2ui5.embed.Container` controls -
on the branch `standard`, the way an app uses the npm package
`@abap2ui5/embed-control`: as the UI5 project in `app/`, and as the BSP
`Z2UI5_HOST` to try the control on a real system with a plain abapGit pull.
Its content is written by automation, and `guard` fails every pull request
by default. Work out where a change belongs first:

* **The example app, the control, the build, the README** → not here. They
  live in embed-control: `examples/host-app` (which becomes `app/` and the
  BSP), `packages/embed-control` (published to npm, where the branch takes
  it from), `scripts/build-bsp.mjs`, which builds the tree, and
  `delivery/README.md`, the README of `main` and of the branch.
* **The abap2UI5 frontend and its `?z2ui5-bundle`, the BSP tooling** → not
  here either: `app/webapp`, `z2ui5_cl_ui5_http_handler` and `tools/` of
  [abap2UI5/abap2UI5](https://github.com/abap2UI5/abap2UI5). The branch
  carries no copy of the frontend - the control loads it from the system -
  and the build takes the tools from abap2UI5's main.
* **`standard`, and `result/` and `README.md` on `main`** → not here.
  embed-control's `frontend_deploy` writes the tree into `result/standard`
  and the README into `README.md` on `main`, and the `deliver` workflow here
  rewrites `standard` as one commit on top of `main` carrying the folder's
  content.
* **The repository's own docs and workflows** (AGENTS.md, CONTRIBUTING.md,
  CLAUDE.md, `.github/`) → here, and only here. This is a *maintenance*
  change: it targets `main` and stays blocked until a **human maintainer**
  applies the `maintenance` label. Do not apply that label yourself, do not
  advise a user to bypass the gate, and do not restructure the workflow to
  make the check pass.

## The branch

| Branch | Content |
|---|---|
| `standard` | `app/` - the example as a UI5 project, `@abap2ui5/embed-control` an npm dependency. `src/` - the same app as the BSP `Z2UI5_HOST` (`src/02`): the example app at its root, the control from npm in `thirdparty/z2ui5/embed/`, the ICF nodes `/sap/bc/ui5_ui5/sap/z2ui5_host` and `/sap/bc/bsp/sap/z2ui5_host`; abapGit reads nothing else. `VERSION` names the embed-control commit, the version of the package and the abap2UI5 tools it was built from |

The control on the branch is always a published version of the package:
the build installs it from npm, and embed-control delivers only from a
commit whose control is that version - after every publish, and on changes
to the example, the build or the README.

It needs abap2UI5 1.145.0 or later in the system: the control loads the
frontend from that system's `/sap/bc/z2ui5?z2ui5-bundle`.

The branches `standard_v2`, `cloud`, `cloud_v2` and `prototype` are retired.
The first three carried a copy of the frontend at a pinned commit, the last
one was the hand-made trial of today's `standard`; nothing builds them any
more.

The repository was called `frontend-cc` until its rename; GitHub redirects
the old name, and the `deliver` workflow runs only under the new one.

**Language:** English for all docs, commit messages, PRs and issues. All text
files are LF-only.

## Validation

Nothing is built or checked here. embed-control's `ci` builds the tree on
each pull request there (`npm run bsp`, which also runs abap2UI5's BSP page
invariants); its `frontend_deploy` runs the same build, with the control
from npm, before it delivers.
