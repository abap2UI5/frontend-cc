# Contributing

**This repository does not take manual pull requests. Contribute to
[abap2UI5/embed-control](https://github.com/abap2UI5/embed-control) or
[abap2UI5/abap2UI5](https://github.com/abap2UI5/abap2UI5) instead.**

`abap2UI5/frontend-embed-control` is a delivery repository, built the way
[abap2UI5/frontend](https://github.com/abap2UI5/frontend) is. Everything it
ships is produced somewhere else and written here by a machine:

| Content | Written by | A hand-made change here … |
|---|---|---|
| `result/` and `README.md` on `main` | embed-control's `frontend_deploy` workflow | is overwritten on the next delivery |
| the branch `standard` | the `deliver` workflow, which rewrites it as one commit on top of `main` carrying the `result/standard` content | is discarded on the next delivery |

The failure is not loud: the change is reviewed, merged and works - until an
unrelated delivery wipes it, with nothing in the history to say why. That is
why the convention is enforced by CI (`guard`) rather than trusted.

## Where a change belongs

| You want to … | Go to |
|---|---|
| change an example app - `freestyle/`, `fiori-elements/` and the BSP | embed-control, `examples/freestyle`, `examples/fiori-elements` |
| change the control | embed-control, `packages/embed-control` - the branch takes it from npm, so a change arrives here with its release |
| change how the branch is built, or its README | embed-control, `scripts/build-bsp.mjs`, `delivery/README.md` |
| change the abap2UI5 frontend, `?z2ui5-bundle`, the BSP tooling | abap2UI5, `app/webapp`, `z2ui5_cl_ui5_http_handler`, `tools/` - the branch carries no copy of the frontend, and the build takes the tools from abap2UI5's main |
| report a bug or request a feature | [embed-control issues](https://github.com/abap2UI5/embed-control/issues) or [abap2UI5 issues](https://github.com/abap2UI5/abap2UI5/issues) |
| maintain this repository's own docs or workflows | here, as a **maintenance pull request** |

## Maintenance pull requests

This repository's own docs - `AGENTS.md`, `CONTRIBUTING.md`, `CLAUDE.md` -
and its workflows are the one thing maintained here. Such a pull request
still starts locked: `guard` fails it until a maintainer applies the label

> `maintenance`

which re-runs the check. `result/` and `README.md` stay blocked even with the
label.
