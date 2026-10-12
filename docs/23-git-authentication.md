# Git authentication

A worker needs access to your repository to clone it, push branches, open pull requests and let the
AI run `git` / `gh` / `glab`. **Git authentication** decides where that access comes from. It's set
**per project**: in the creation wizard's Git section, and afterwards in **Git › Configuration**.
Changing it needs the git-configuration permission (ADMIN/PM by default, grantable to a member), and a
change reaches the running workers immediately.

## The methods

| Method | Provider | Credential | Token lifetime | Recommended |
| --- | --- | --- | --- | --- |
| **GitHub App** | GitHub (incl. Enterprise) | Your GitHub App's ID + private key, stored encrypted in 4PM | ~1 hour, **one per job**, revoked when the job ends | ✅ for GitHub |
| **GitLab service account** | GitLab | A service account's personal access token, stored encrypted in 4PM | A new repo-limited token **per job**, revoked when it ends (max 48 h) | ✅ for GitLab |
| **GitLab token** | GitLab | A group or project access token, stored encrypted in 4PM | Long-lived — the same token every job | Works; flagged long-lived |
| **Self-managed** | Any | The worker's own `gh` / `glab` login (or, on rented workers, an SSH deploy key) | Long-lived, **full permissions of that account** | Only with a dedicated, limited account |

With the server-managed methods (the first three), the **secret never reaches the worker**: the worker
asks 4PM for a token each time git needs one.

## GitHub App

1. Register a GitHub App in your GitHub account or organization with **Contents** and **Pull
   requests** permissions (**read & write**), and install it on the owner(s) of the project's repos
   (including submodules). If you also want GitHub issue sync to reuse the App, add **Issues: read &
   write**.
2. In the project, choose **GitHub App**, enter the **App ID**, upload the **private key (.pem)**, and —
   for GitHub Enterprise — the API URL.
3. **Test connection** checks three things for each repo (and submodule): the GitHub API can be reached,
   the App **installation** is found, and it has **write access**. A repo showing *Not installed* or
   *Missing permissions* can't be reached until you install the App on it or grant Contents + Pull
   requests.

Bonuses: the Git tab can read **origin** (branches, PRs, commits) without a worker online, rules can
watch PRs being merged or closed, and GitHub **issue sync** can reuse the same App.

## GitLab service account

1. Create a GitLab **service account** (free, no billable seat) in the top-level group or instance, add it
   as a **Maintainer** of the project's repositories, and create a personal access token for it with the
   **`api`** scope.
2. In the project, choose **GitLab service account**, enter the **group path** and that token (turn on
   *self-managed GitLab* and set the host if you don't use gitlab.com).
3. **Test connection** creates and revokes one token to prove it works.

The service account's own token stays in 4PM; workers only receive short-lived, Developer-level tokens
for one repo.

## GitLab token

Create a **group (or project) access token** with the **`api`** and **`write_repository`** scopes. Choose
**GitLab token**, enter the **group path** and the token. **Test connection** checks that GitLab is
reachable, the token can access the group, and it can read the repo through the API. The Git tab then shows branches, merge requests and commits "via GitLab" even with no worker
online.

## Self-managed

The worker uses its own login:

- **Docker:** run `gh auth login` / `glab auth login` inside the container, or **mount** your host's gh/glab
  login (Customize › Mount gh/glab login).
- **Direct install:** whatever `gh` / `glab` / git credentials the machine's user has.

The worker hands that login's token to the agent's git and gh/glab. ⚠️ That's a long-lived token with
**everything** the account can do (every repo it can reach, workflows, org settings). Use a dedicated
account with access to only the repos it needs. If `gh` keeps its token in the system keyring, the
mounted folder holds no token — log in with `gh auth login --insecure-storage`, or inside the container.

## Troubleshooting

- **"Not provisioned" / clone fails** — fix the method or credential in **Git › Configuration** (it works
  even while the clone fails or the worker is offline), then **Retry**.
- **Push or PR fails with an auth error** — on the GitHub App, check the App is installed on that repo;
  on a GitLab token, check scopes and expiry; on Self-managed, check `gh auth status` on the worker.
- **A warning about long-lived credentials** — you're on GitLab token or Self-managed; consider the GitHub
  App or GitLab service account.

See also: [Git operations](./07-git-operations.md) · [Recommended setup](./22-recommended-setup.md).
