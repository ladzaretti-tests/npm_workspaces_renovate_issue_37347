# minimal-reproduction-template

## Current behavior

When Renovate runs on the this project with workspaces, it opens two separate PRs for the `uuid` dependency in the workspace:

- https://github.com/ladzaretti-tests/npm_workspaces_renovate_issue_37347/pull/2
- https://github.com/ladzaretti-tests/npm_workspaces_renovate_issue_37347/pull/4

<details><summary>Logs</summary>
  
```
DEBUG: packageFiles with updates
{
  "baseBranch": "main"
  "config": {
    "npm": [
      {
        "deps": [
          {
            "currentValue": "2.1472.0",
            "currentVersion": "2.1472.0",
            "currentVersionAgeInDays": 669,
            "currentVersionTimestamp": "2023-10-06T18:32:02.073Z",
            "datasource": "npm",
            "depName": "aws-sdk",
            "depType": "dependencies",
            "fixedVersion": "2.1472.0",
            "isSingleVersion": true,
            "lockedVersion": "2.1472.0",
            "mostRecentTimestamp": "2024-11-06T20:03:49.151Z",
            "packageName": "aws-sdk",
            "prettyDepType": "dependency",
            "registryUrl": "https://registry.npmjs.org",
            "sourceUrl": "https://github.com/aws/aws-sdk-js",
            "versioning": "npm",
            "warnings": [],
            "updates": [
              {
                "bucket": "non-major",
                "newVersion": "2.1692.0",
                "newValue": "2.1692.0",
                "releaseTimestamp": "2024-11-06T20:03:49.151Z",
                "newVersionAgeInDays": 272,
                "newMajor": 2,
                "newMinor": 1692,
                "newPatch": 0,
                "updateType": "minor",
                "isBreaking": false,
                "libYears": 1.0851061351471334,
                "branchName": "renovate/aws-sdk-2.x"
              }
            ]
          }
        ],
        "extractedConstraints": {
          "npm": ">=7"
        },
        "lockFiles": [
          "package-lock.json"
        ],
        "managerData": {
          "hasPackageManager": false,
          "npmLock": "package-lock.json",
          "npmrcFileName": null,
          "packageJsonName": "",
          "workspaces": [
            "./workspaces/workspace"
          ],
          "workspacesPackages": [
            "./workspaces/workspace"
          ],
          "yarnZeroInstall": false
        },
        "packageFile": "package.json",
        "skipInstalls": true
      },
      {
        "deps": [
          {
            "currentValue": "11.1.0",
            "currentVersion": "8.0.0",
            "currentVersionAgeInDays": 1924,
            "currentVersionTimestamp": "2020-04-29T20:42:26.823Z",
            "datasource": "npm",
            "depName": "uuid",
            "depType": "dependencies",
            "fixedVersion": "8.0.0",
            "isSingleVersion": true,
            "lockedVersion": "8.0.0",
            "mostRecentTimestamp": "2025-02-19T18:16:11.602Z",
            "packageName": "uuid",
            "prettyDepType": "dependency",
            "registryUrl": "https://registry.npmjs.org",
            "sourceUrl": "https://github.com/uuidjs/uuid",
            "versioning": "npm",
            "warnings": [],
            "updates": [
              {
                "bucket": "non-major",
                "newVersion": "8.3.2",
                "newValue": "8.3.2",
                "releaseTimestamp": "2020-12-08T20:38:36.233Z",
                "newVersionAgeInDays": 1701,
                "newMajor": 8,
                "newMinor": 3,
                "newPatch": 2,
                "updateType": "minor",
                "isBreaking": false,
                "libYears": 0.6109515921486555,
                "branchName": "renovate/uuid-8.x"
              },
              {
                "bucket": "major",
                "newVersion": "11.1.0",
                "newValue": "11.1.0",
                "releaseTimestamp": "2025-02-19T18:16:11.602Z",
                "newVersionAgeInDays": 167,
                "newMajor": 11,
                "newMinor": 1,
                "newPatch": 0,
                "updateType": "major",
                "isBreaking": true,
                "isLockfileUpdate": true,
                "libYears": 4.810680643677068,
                "branchName": "renovate/uuid-11.x-lockfile"
              }
            ]
          }
        ],
        "extractedConstraints": {
          "npm": ">=7"
        },
        "lockFiles": [
          "package-lock.json"
        ],
        "managerData": {
          "hasPackageManager": false,
          "npmLock": "package-lock.json",
          "npmrcFileName": null,
          "packageJsonName": "workspace1",
          "workspacesPackages": [
            "./workspaces/workspace"
          ],
          "yarnZeroInstall": false
        },
        "packageFile": "workspaces/workspace/package.json",
        "skipInstalls": true
      }
    ]
  }
}
```

</details>

## Expected behavior
Renovate should respect the workspace's own locked dependency version. 
In this case:
- The workspace should keep `uuid@11.1.0` as declared and locked in its own `node_modules`.
- Renovate should not treat the root hoisted version `uuid@8.x` as the locked version for all workspaces.
## Link to the Renovate issue or Discussion

- https://github.com/renovatebot/renovate/discussions/37347
