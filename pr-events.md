## PR Events

GitHub Actions will fire for PRs ([pull_request](https://help.github.com/en/actions/reference/events-that-trigger-workflows#pull-request-event-pull_request)),
but [Pull request events for forked
repositories](https://help.github.com/en/actions/reference/events-that-trigger-workflows#pull-request-events-for-forked-repositories)

> When you create a pull request from a forked repository to the base repository,
> GitHub sends the `pull_request` event to the base repository and no pull request events occur on the forked repository.

> Workflows don't run on forked repositories by default. You must enable GitHub Actions in the Actions tab of the forked repository.

> The permissions for the `GITHUB_TOKEN` in forked repositories is read-only.
> For more information about the `GITHUB_TOKEN`, see "[Virtual environments for GitHub
Actions](https://help.github.com/en/actions/reference/virtual-environments-for-github-hosted-runners)."

### In English

1. Commits in forked repositories won't have run the hook, which means they may have spelling errors.
1. When the PR is created in this repository, it won't have permission to comment, which means you won't be able to see the cool PR comment.

## Proposed strategy to address this

Instead of relying on a PR event,
I'm going to try to run a `schedule` event which looks for PRs from foreign repositories which have been updated since the last time the event was run.
And that event will run the spell checker and then comment on the PR.
