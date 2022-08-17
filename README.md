# vite-bug-repro-ssr-pnp

A reproduction of broken SSR with CommonJS dependencies and Yarn PnP.

`app` (a workspace) depends on `pkg-a` (another workspace) which depends on `locale` (a CommonJS npm dependency).

SSR crashes with `ReferenceError: module is not defined` from `locale`.

Reproduction steps:
```bash
corepack enable
yarn install
yarn node app/server.mjs
open http://localhost:5173
```

Note that this does *not* error without PnP:
```bash
corepack enable
yarn config set nodeLinker node-modules
yarn install
yarn node app/server.mjs
open http://localhost:5173
```

It is also worth noting that this does *not* error if the npm CJS package is a *direct* dependency of `app`.
