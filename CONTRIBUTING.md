# Contributing

**This repository does not take manual pull requests. Contribute to
[abap2UI5/reuse-custom-control](https://github.com/abap2UI5/reuse-custom-control)
or [abap2UI5/abap2UI5](https://github.com/abap2UI5/abap2UI5) instead.**

`abap2UI5/frontend-cc` is a delivery repository, built the way
[abap2UI5/frontend](https://github.com/abap2UI5/frontend) is. Everything it
ships is produced somewhere else and written here by a machine:

| Content | Written by | A hand-made change here … |
|---|---|---|
| `result/` and `README.md` on `main` | reuse-custom-control's `frontend_cc_deploy` workflow | is overwritten on the next delivery |
| every branch | the `deliver` workflow, which rewrites each branch as one commit on top of `main` carrying its `result/<branch>` content | is discarded on the next delivery |

The failure is not loud: the change is reviewed, merged and works - until an
unrelated delivery wipes it, with nothing in the history to say why. That is
why the convention is enforced by CI (`guard`) rather than trusted.

## Where a change belongs

| You want to … | Go to |
|---|---|
| change the example app | reuse-custom-control, `examples/host-app` |
| change the control | reuse-custom-control, `packages/reuse-custom-control/src` |
| change how the branches are built, or their README | reuse-custom-control, `scripts/build-branches.mjs`, `delivery/README.md` |
| change the abap2UI5 frontend, the BSP tooling, the ABAP handler | abap2UI5, `app/webapp`, `tools/`, `frontend/abap` - then bump `A2UI5_PIN` in reuse-custom-control |
| report a bug or request a feature | [reuse-custom-control issues](https://github.com/abap2UI5/reuse-custom-control/issues) or [abap2UI5 issues](https://github.com/abap2UI5/abap2UI5/issues) |
| maintain this repository's own docs or workflows | here, as a **maintenance pull request** |

## Maintenance pull requests

This repository's own docs - `AGENTS.md`, `CONTRIBUTING.md`, `CLAUDE.md` -
and its workflows are the one thing maintained here. Such a pull request
still starts locked: `guard` fails it until a maintainer applies the label

> `maintenance`

which re-runs the check. `result/` and `README.md` stay blocked even with the
label.
