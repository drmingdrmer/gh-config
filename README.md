# gh-config
Shared github-related config for repository in this organization. See: https://github.com/probot/settings

# Usage

**[Install the app](https://github.com/apps/settings)**.

To add config to a repo in this organization, add file `.github/settings.yml`:

```yaml
# inherit configs already defined in this common repo.
_extends: gh-config

# repo specific configs, label definition for issues and pulls.
labels:
  - name: bug
    color: CC0000
  - name: feature
    color: 336699
  - name: first-timers-only
    color: 88dd88
    # include the old name to rename and existing label
    oldname: Help Wanted
```

Commit it into the MAIN branch(`master` I guess), then the github app probot-config will automatically apply it.


# Settings

> This paragraph is copied from [probot/settings](https://github.com/probot/settings):

All top-level settings are optional. Some plugins do have required fields.

```yaml
# These settings are synced to GitHub by https://probot.github.io/apps/settings/

repository:
  # See https://developer.github.com/v3/repos/#edit for all available settings.

  # The name of the repository. Changing this will rename the repository
  name: repo-name

  # A short description of the repository that will show up on GitHub
  description: description of repo

  # A URL with more information about the repository
  homepage: https://example.github.io/

  # A comma-separated list of topics to set on the repository
  topics: github, probot

  # Either `true` to make the repository private, or `false` to make it public.
  private: false

  # Either `true` to enable issues for this repository, `false` to disable them.
  has_issues: true

  # Either `true` to enable projects for this repository, or `false` to disable them.
  # If projects are disabled for the organization, passing `true` will cause an API error.
  has_projects: true

  # Either `true` to enable the wiki for this repository, `false` to disable it.
  has_wiki: true

  # Either `true` to enable downloads for this repository, `false` to disable them.
  has_downloads: true

  # Updates the default branch for this repository.
  default_branch: master

  # Either `true` to allow squash-merging pull requests, or `false` to prevent
  # squash-merging.
  allow_squash_merge: true

  # Either `true` to allow merging pull requests with a merge commit, or `false`
  # to prevent merging pull requests with merge commits.
  allow_merge_commit: true

  # Either `true` to allow rebase-merging pull requests, or `false` to prevent
  # rebase-merging.
  allow_rebase_merge: true

# Labels: define labels for Issues and Pull Requests
labels:
  - name: bug
    color: CC0000
  - name: feature
    color: 336699
  - name: first-timers-only
    # include the old name to rename an existing label
    oldname: Help Wanted

# Milestones: define milestones for Issues and Pull Requests
milestones:
  - title: milestone-title
    description: milestone-description
    # The state of the milestone. Either `open` or `closed`
    state: open

# Collaborators: give specific users access to this repository.
collaborators:
  - username: bkeepers
    # Note: Only valid on organization-owned repositories.
    # The permission to grant the collaborator. Can be one of:
    # * `pull` - can pull, but not push to or administer this repository.
    # * `push` - can pull and push, but not administer this repository.
    # * `admin` - can pull, push and administer this repository.
    permission: push

  - username: hubot
    permission: pull

# NOTE: The APIs needed for teams are not supported yet by GitHub Apps
# https://developer.github.com/v3/apps/available-endpoints/
teams:
  - name: core
    permission: admin
  - name: docs
    permission: push

branches:
  - name: master
    # https://developer.github.com/v3/repos/branches/#update-branch-protection
    # Branch Protection settings. Set to null to disable
    protection:
      # Required. Require at least one approving review on a pull request, before merging. Set to null to disable.
      required_pull_request_reviews:
        # The number of approvals required. (1-6)
        required_approving_review_count: 1
        # Dismiss approved reviews automatically when a new commit is pushed.
        dismiss_stale_reviews: true
        # Blocks merge until code owners have reviewed.
        require_code_owner_reviews: true
        # Specify which users and teams can dismiss pull request reviews. Pass an empty dismissal_restrictions object to disable. User and team dismissal_restrictions are only available for organization-owned repositories. Omit this parameter for personal repositories.
        dismissal_restrictions:
          users: []
          teams: []
      # Required. Require status checks to pass before merging. Set to null to disable
      required_status_checks:
        # Required. Require branches to be up to date before merging.
        strict: true
        # Required. The list of status checks to require in order to merge into this branch
        contexts: []
      # Required. Enforce all configured restrictions for administrators. Set to true to enforce required status checks for repository administrators. Set to null to disable.
      enforce_admins: true
      # Required. Restrict who can push to this branch. Team and user restrictions are only available for organization-owned repositories. Set to null to disable.
      restrictions:
        users: []
        teams: []
```
