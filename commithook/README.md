# Setup Commit Hooks

![commit hook](https://github.com/user-attachments/assets/72fb696e-b86f-4744-9cfe-cfb31ebb0f97)

---

## Author Information
| Last Updated On | Version | Author           | Level           | Reviewer               |
|-----------------|---------|------------------|-----------------|------------------------|
| 11-08-2025      | V2.0    | Sunny Kumar      | Internal Review | Aman Raj               |
|                 |         | Sunny Kumar      | L0              | Shikha                 |
|                 |         | Sunny Kumar      | L1              | Kriti Nehra            |
|                 |         | Sunny Kumar      | L2              | Ashwini Singh/Deepak Nishad |

---

<details>
  <summary><strong>Table of Contents</strong></summary>

- [Introduction](#introduction)  
- [Goal](#goal)  
- [Why Commit Hooks](#why-commit-hooks)
- [Workflow](#workflow)
- [Step-by-step Setup Guide](#step-by-step-setup-guide)
- [Demo: Review the Behavior](#demo-review-the-behavior)
- [FAQ](#faq)  
- [Contact Information](#contact-information)  
- [References](#references)  
- [Conclusion](#conclusion)

</details>

---

## Introduction

This document explains how to enforce that every commit message is mapped to a JIRA ticket using Git hooks. We will set up local hooks that block commits if the message does not contain the required JIRA key. For the demo, we enforce the presence of `JIRA-2` (you can generalize this to any `PROJECT-<number>` later).

---

## Goal

- Enforce that every commit message contains a JIRA ticket reference.  
- Demo policy: commit message must contain `JIRA-2`.

Note: Technically, validating the commit message is the job of the `commit-msg` hook (because `pre-commit` runs before the message is finalized). We will wire a minimal `pre-commit` (optional) and a strict `commit-msg` validator to achieve the requirement reliably.

---

## Why Commit Hooks

- **Quality Gates**: Prevents non-compliant commit messages.  
- **Traceability**: Ensures commits can be traced back to JIRA tasks.  
- **Automation-friendly**: Improves CI/CD and code review discipline.

---

## Workflow

```mermaid
graph TD
    A[Developer executes 'git commit'] --> B{Pre-commit hook exists?};
    B -- Yes --> C[Run pre-commit checks (fast)];
    C --> D{Commit-msg hook exists?};
    B -- No --> D;
    D -- Yes --> E[Validate commit message (JIRA mapping)];
    E -- Valid --> F[Commit object created];
    E -- Invalid --> G[Commit aborted with error];
    D -- No --> F;
```

---

## Step-by-step Setup Guide

These steps assume you have an existing Git repository.

### 1) Create the `commit-msg` hook (required)

Create a file at `.git/hooks/commit-msg` with the following content and make it executable:

```bash
#!/usr/bin/env bash
set -euo pipefail

# commit-msg receives the path to the temporary commit message file as $1
COMMIT_MSG_FILE="$1"

# Demo rule: require JIRA-2 in the commit message
# You can change REQUIRED_TICKET to a project-wide pattern if needed
REQUIRED_TICKET="${REQUIRED_TICKET:-JIRA-2}"

COMMIT_MESSAGE_CONTENT=$(cat "$COMMIT_MSG_FILE")

if ! grep -E -q "(^|[^A-Z0-9-])${REQUIRED_TICKET}([^A-Z0-9-]|$)" <<< "$COMMIT_MESSAGE_CONTENT"; then
  echo "ERROR: Commit message must include the ticket '${REQUIRED_TICKET}'." >&2
  echo "Example: ${REQUIRED_TICKET}: Short, descriptive message" >&2
  exit 1
fi

# If you prefer to accept any JIRA ticket, comment the block above and use:
# PROJECT_KEY="${PROJECT_KEY:-JIRA}"
# if ! grep -E -q "${PROJECT_KEY}-[0-9]+" <<< "$COMMIT_MESSAGE_CONTENT"; then
#   echo "ERROR: Commit message must include a ${PROJECT_KEY}-<number> ticket (e.g., ${PROJECT_KEY}-123)." >&2
#   exit 1
# fi

exit 0
```

Make it executable:

```bash
chmod +x .git/hooks/commit-msg
```

### 2) (Optional) Create a `pre-commit` hook

While `pre-commit` cannot see the final commit message, you may still add quick checks here (formatting, linting, secrets scan). Create `.git/hooks/pre-commit`:

```bash
#!/usr/bin/env bash
set -euo pipefail

# Example fast checks (add what your project needs)
# echo "Running pre-commit quick checks..."
# npm run -s lint 2>/dev/null || true
# npm run -s format:check 2>/dev/null || true

exit 0
```

Make it executable:

```bash
chmod +x .git/hooks/pre-commit
```

### 3) (Optional) Auto-suggest the ticket with `prepare-commit-msg`

If you always work on a single ticket, you can pre-fill the message with `JIRA-2: ` so developers don’t forget to add it. Create `.git/hooks/prepare-commit-msg`:

```bash
#!/usr/bin/env bash
set -euo pipefail

MSG_FILE="$1"
DEFAULT_TICKET="${REQUIRED_TICKET:-JIRA-2}"

# Prepend ticket if it is not already present
if ! grep -E -q "(^|[^A-Z0-9-])${DEFAULT_TICKET}([^A-Z0-9-]|$)" "$MSG_FILE"; then
  sed -i "1s/^/${DEFAULT_TICKET}: /" "$MSG_FILE"
fi
```

Make it executable:

```bash
chmod +x .git/hooks/prepare-commit-msg
```

---

## Demo: Review the Behavior

Assume you have staged changes.

- Valid commit (contains `JIRA-2`):

```bash
git commit -m "JIRA-2: fix navbar alignment on mobile"
# Output: commit created successfully
```

- Invalid commit (missing `JIRA-2`):

```bash
git commit -m "fix navbar alignment on mobile"
# Output:
# ERROR: Commit message must include the ticket 'JIRA-2'.
# Example: JIRA-2: Short, descriptive message
# (commit aborted)
```

- Override the ticket via environment (optional):

```bash
REQUIRED_TICKET=JIRA-999 git commit -m "JIRA-999: hotfix for prod issue"
```

---

## FAQ

- Q: Can I enforce any JIRA ticket instead of only `JIRA-2`?  
  A: Yes. Replace the strict check with the generalized pattern (`PROJECT_KEY-<number>`) in the script (see commented section), or pass `PROJECT_KEY=ABC` via environment.

- Q: Are hooks shared automatically with the team?  
  A: No. Files in `.git/hooks` are not committed. Use tools like Husky, Lefthook, or a bootstrap script to distribute hooks.

- Q: Can developers bypass hooks?  
  A: Locally, `--no-verify` skips client hooks. Consider adding a server-side `pre-receive` or `update` hook to enforce on the remote as well.

---

## Contact Information

| Name        | Email                                  |
|-------------|----------------------------------------|
| Sunny Kumar | sunny.kumar.snaatak@mygurukulam.co     |

---

## References

| Link                                                                                                           | Description                                      |
|----------------------------------------------------------------------------------------------------------------|--------------------------------------------------|
| [https://www.atlassian.com/git/tutorials/git-hooks](https://www.atlassian.com/git/tutorials/git-hooks)         | Atlassian Git Hooks Tutorial                     |
| [https://www.geeksforgeeks.org/git/git-hooks/](https://www.geeksforgeeks.org/git/git-hooks/)                   | GeeksforGeeks Guide on Git Hooks                 |

---

## Conclusion

- We established a reliable client-side enforcement using a `commit-msg` hook to require `JIRA-2` in commit messages.  
- Optional `pre-commit` and `prepare-commit-msg` hooks improve the developer experience.  
- For team-wide enforcement, pair this with server-side hooks or a shared hook manager.

