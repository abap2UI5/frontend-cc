# AGENTS.md — AI Assistant Guide for abap2UI5 samples-embed-control

> This file follows the cross-tool AGENTS.md convention and is the single
> agent instruction file of this repository. `CLAUDE.md` next to it is a
> pointer at this file, nothing more.

## Do Not Open Pull Requests Here

This is a **delivery repository**, like
[abap2UI5/frontend](https://github.com/abap2UI5/frontend). It delivers the
example apps of
[abap2UI5/embed-control](https://github.com/abap2UI5/embed-control) - host
apps that run abap2UI5 apps in `z2ui5.embed.Container` controls - the way
apps use the npm package `@abap2ui5/embed-control`. On the branch
`standard`: a UI5 freestyle app in `freestyle/`, also as the BSP
`Z2UI5_HOST` to try the control on a real system with a plain abapGit pull,
a Fiori elements app with the control in a custom section of its object
page in `fiori-elements/`, a Fiori elements app for OData V2 with the
control in an object page extension and the RAP service it reads in
`fiori-elements-v2/`, and a generic UI Integration Card for SAP Build Work
Zone in `card/`. On the branch `rap`: that RAP service and the OData V2 app
as BSP `Z2UI5_HOST_FE`, for one abapGit pull on a system with RAP.
Its content is written by automation, and `guard` fails every pull request
by default. Work out where a change belongs first:

* **The example apps, the control, the build, the README** → not here.
  They live in embed-control: `examples/freestyle`,
  `examples/fiori-elements`, `examples/fiori-elements-v2` (with its RAP
  service in `abap/`) and `examples/card` (which become `freestyle/`,
  `fiori-elements/`, `fiori-elements-v2/`, `card/` and the BSPs of both
  branches), `packages/embed-control`
  (published to npm, where the branch takes it from),
  `scripts/build-bsp.mjs`, which builds the tree, and `delivery/README.md`,
  the README of `main` and of the branch.
* **The abap2UI5 frontend and its `?z2ui5-bundle`, the BSP tooling** → not
  here either: `app/webapp`, `z2ui5_cl_ui5_http_handler` and `tools/` of
  [abap2UI5/abap2UI5](https://github.com/abap2UI5/abap2UI5). The branch
  carries no copy of the frontend - the control loads it from the system -
  and the build takes the tools from abap2UI5's main.
* **`standard`, `rap`, and `result/` and `README.md` on `main`** → not
  here. embed-control's `frontend_deploy` writes the trees into
  `result/standard` and `result/rap` and the README into `README.md` on
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
| `standard` | `freestyle/`, `fiori-elements/`, `fiori-elements-v2/` and `card/` - the examples as UI5 projects, `@abap2ui5/embed-control` an npm dependency. `src/` - the freestyle app as the BSP `Z2UI5_HOST` (`src/02`): the app at its root, the control from npm in `thirdparty/z2ui5/embed/`, the ICF nodes `/sap/bc/ui5_ui5/sap/z2ui5_host` and `/sap/bc/bsp/sap/z2ui5_host`; abapGit reads nothing else. The Fiori elements app for OData V4 and the card have no BSP - the app needs its OData service, which only the example's mockserver has, and a card is deployed to its host. `VERSION` names the embed-control commit, the version of the package and the abap2UI5 tools it was built from |
| `rap` | `src/01` - the RAP service of `fiori-elements-v2` (CDS view entity, metadata extension, service definition, OData V2 binding) and the abap2UI5 app `Z2UI5_CL_EMBED_COUNTRY` it starts. `src/02` - the Fiori elements app for OData V2 as the BSP `Z2UI5_HOST_FE`, without its mock service, the control from npm in `thirdparty/z2ui5/embed/`, the ICF nodes `/sap/bc/ui5_ui5/sap/z2ui5_host_fe` and `/sap/bc/bsp/sap/z2ui5_host_fe`. For a system with RAP (SAP S/4HANA 2020 or later), next to `standard` or alone. `VERSION` as on `standard`. The successor of abap2UI5-addons/fiori-elements-integration |

The control on the branch is always a published version of the package:
the build installs it from npm, and embed-control delivers only from a
commit whose control is that version - after every publish, and on changes
to the examples, the build or the README.

It needs abap2UI5 1.145.0 or later in the system: the control loads the
frontend from that system's `/sap/bc/z2ui5?z2ui5-bundle`. The Fiori elements
apps and the card need the first abap2UI5 release after 1.145.0, whose
embedded frontend leaves the URL hash to the host - the object page routes
by it, and so does SAP Build Work Zone. So does the branch `rap`.

The branches `standard_v2`, `cloud`, `cloud_v2` and `prototype` were deleted
on 2026-09-29, after the first delivery of `standard` with the control from
npm. The first three carried a copy of the frontend at a pinned commit, the
last one was the hand-made trial of today's `standard`; nothing builds them
any more.

The repository was called `frontend-cc` until its rename; GitHub redirects
the old name, and the `deliver` workflow runs only under the new one.

**Language:** English for all docs, commit messages, PRs and issues. All text
files are LF-only.

## Validation

Nothing is built or checked here. embed-control's `ci` builds the tree on
each pull request there (`npm run bsp`, which also runs abap2UI5's BSP page
invariants); its `frontend_deploy` runs the same build, with the control
from npm, before it delivers.
