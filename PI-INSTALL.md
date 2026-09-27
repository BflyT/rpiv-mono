# Install the todo status fork with Pi

This branch packages the existing `feat/todo-failure-and-user-handoff` changes as a Git-installable Pi package. The root `pi` manifest loads **only** `packages/rpiv-todo/index.ts`; other monorepo extensions are not loaded. The upstream workspace structure and dependency lockfile are retained. The development-only `prepare: husky` hook is omitted on this installation branch because Pi installs Git packages with `npm install --omit=dev`, where Husky is unavailable.

```sh
pi install git:github.com/BflyT/rpiv-mono@pi-todo-install
```

Do not enable the original `npm:@juicesharp/rpiv-todo` or a local todo copy at the same time. Remove its configuration entry first (back up settings). Restart Pi or run `/reload` after installing.

The fork supports `pending`, `in_progress`, `failed`, `awaiting_user`, `completed`, and `deleted`. Failed and awaiting-user tasks require an explanation. Older versions do not support the two new states; do not downgrade sessions with those states without reviewing their task history.

Node.js >=22.19.0 and npm >=11 are recommended; this repository uses npm workspaces. Git must be installed. Dependencies are installed for the monorepo, even though only todo is exposed to Pi.

For a reproducible deployment, replace the branch ref in the install source with a verified commit SHA.
