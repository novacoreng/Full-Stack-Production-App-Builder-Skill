# GitHub
Inspect status, branch, remote, and secrets before committing. Create checkpoint commits at locked phases. Run required tests/builds before push, never commit secrets, push only when authorized, and verify the remote branch and commit SHA.


## QA-before-commit rule
Do not commit merely to make progress appear complete. After remediation, inspect the diff, exclude secrets/generated artifacts, run targeted tests plus required regression, complete available runtime/device/browser/API verification, then commit the verified phase. Report and verify the remote commit SHA. Preserve Git history.
