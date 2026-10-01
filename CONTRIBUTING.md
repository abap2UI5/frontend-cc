# Contributing

Pull requests against `main` are welcome - the examples, their tests, the
build of the branches and the README live here.

| You want to … | Go to |
|---|---|
| change an example - `freestyle/`, `fiori-elements/`, `fiori-elements-v2/`, `card/` - or its README | here, `main` |
| change the RAP service and the abap2UI5 app of the branch `rap` | here, `fiori-elements-v2/abap` |
| change how the branches are built | here, `scripts/build-bsp.mjs` and `.github/workflows/deliver.yaml` |
| change the control | [abap2UI5/embed-control](https://github.com/abap2UI5/embed-control), `packages/embed-control` - the examples take it from npm, so a change arrives here with its release |
| change the abap2UI5 frontend, `?z2ui5-bundle`, the BSP tooling | [abap2UI5/abap2UI5](https://github.com/abap2UI5/abap2UI5), `app/webapp`, `z2ui5_cl_ui5_http_handler`, `tools/` |

**Never against `standard` or `rap`.** The `deliver` workflow rewrites both
on every push to `main`, as one commit on top of it built from `main`'s
content - a commit made on a branch is gone with the next delivery.

Before you push: `npm ci`, `npm run lint`, `npm run format:check`,
`npm run abaplint`, `npm run build`, and - with an abap2UI5 backend on port
3000 - `npx playwright test`. CI runs the same, and `npm run bsp`.

A change here is also tested by abap2UI5/embed-control's CI, with the
control of its `main`: keep the examples working with the published control
and with the next one.
