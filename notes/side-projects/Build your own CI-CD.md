# Build your own CI/CD

A fun side project that teaches you how CI/CD systems like GitHub Actions and Azure Pipelines actually work under the hood — they're just orchestrated shell scripts with an event system.

## Core idea

At their core, CI/CD systems are:
1. An **event source** that detects git activity
2. A **queue** that serialises those events into jobs
3. A **runner** that spins up a clean environment and executes shell scripts
4. A **status reporter** that writes results back to the forge

## Git hooks as the event source

Git has built-in server-side hooks. The key one is `post-receive`, which fires on the server after every push:

```sh
# .git/hooks/post-receive
while read old_sha new_sha ref; do
  branch="${ref#refs/heads/}"
  if [ "$branch" = "main" ]; then
    ./scripts/deploy.sh
  fi
done
```

It receives `old_sha new_sha refname` on stdin for every updated ref — enough to reconstruct branch name, what changed, new branch vs update, etc.

## PR events

PRs are a forge concept, not a git concept. Git only knows refs and commits. To handle PR events on a self-hosted forge:
- Represent PRs as refs (GitHub uses `refs/pull/<N>/head` internally)
- Fire `post-receive` when that ref is created/updated
- Detect the pattern in your hook and route to the right script

## DIY stack layers

| Layer | DIY equivalent |
|---|---|
| Event source | `post-receive` hook |
| Webhook/queue | Small HTTP server + job queue (e.g. Redis) |
| Runner | Docker container — run your `.sh`, exit |
| Status reporting | Forge API or `refs/statuses/...` |

## Reference implementation

**Gitea + Woodpecker CI** is the closest open-source minimal stack — worth reading the source to see how each layer is wired together.
