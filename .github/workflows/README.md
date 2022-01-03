# Centralized Workflows

This folder contains workflows/GitHub Actions available to be reused across the Flosports organization.

## How to use

1. Within your own repo, create a `{{fileName}}.yml` file within the `.github/workflows` file path. Ex: `.github/workflows/actions.yml`
2. Within the `.yml` file, give your action set a name and triggers.
    ```YAML
    name: 'Auto Actions'
    on:
    pull_request:
        types: [opened, ready_for_review]
    ```
    See [GitHub Actions documentation](https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions) for more on the syntax and what triggers make sense to utilize with `on` for your repo and chosen actions.

3. Create and name a set of jobs to use. The `uses:` path should be the path to the action you wish to use from this repository.
   ```YAML
    jobs:
        add-reviews:
            name: Auto Assign
            uses: flocasts/.github/.github/workflows/assign-reviewers.yml@main
  
        link_ticket:
            name: Link Ticket
            uses: flocasts/.github/.github/workflows/link-ticket.yml@main
    ```

## Available Actions

### Auto Assign Reviewers
##### Path: `flocasts/.github/.github/workflows/assign-reviewers.yml@main`
A pass through to [Auto Assign Action by Kentaro](https://github.com/kentaro-m/auto-assign-action#readme). Please follow the documentation there on creating an `auto-assign.yml` with the correct reviewers/assignees for your repository. This will need to be configured/added on a per-repository basis.
### Auto Add JIRA Links
##### Path: `flocasts/.github/.github/workflows/link-ticket.yml@main`
Uses branch names to automatically populate JIRA conventions on an opened pull request. The branch name must begin with the name of the JIRA ticket. Should be used with `on: pull_request`. Includes the following:
1. Adds JIRA link into the description of a pull request. This includes cleaning up if any ticket reference is already at the beginning of the PR title. Just hit "Open Pull Request!" 
2. Appends JIRA ticket number to the beginning of the Pull Request title.

Handles the following branch naming styles:
- FLO-123
- FLO-123-feature-desciption
- FLO-123/feature-description

If there is another branch naming convention that (a) you've verified does not work and (b) you would like added, contact Solomon Duncan!
