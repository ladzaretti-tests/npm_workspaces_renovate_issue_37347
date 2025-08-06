# minimal-reproduction-template

## Current behavior

When Renovate runs on the this project with workspaces, it opens two separate PRs for the `uuid` dependency in the workspace:

- https://github.com/ladzaretti-tests/npm_workspaces_renovate_issue_37347/pull/2
- https://github.com/ladzaretti-tests/npm_workspaces_renovate_issue_37347/pull/4

## Expected behavior
Renovate should respect the workspace's own locked dependency version. 
In this case:
- The workspace should keep `uuid@11.1.0` as declared and locked in its own `node_modules`.
- Renovate should not treat the root hoisted version `uuid@8.x` as the locked version for all workspaces.
## Link to the Renovate issue or Discussion

- https://github.com/renovatebot/renovate/discussions/37347
