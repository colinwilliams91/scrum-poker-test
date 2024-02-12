# Helpful GH Automations for Agile

## GitFlow PR and Issue Templates:
- This repository contains very simple outlines for PRs and New Issues
- PRs
  - Summary
  - Repro
  - References
- Issues
  - Summary
  - References
  - Solution

## Actions:
- This repository implements a strategy I developed for a "Bridge Branch"
- The purpose of this "Bridge-Branch" is to act as an intermediary between feature development and `main`
  - It requires clean code and intention as it bypasses PR and code review
  - The concept is the "Bridge" should be highly isolated and not touch anything that other feature development may overwrite
- The Actions work two-fold:
  1. [auto_merge_bridge_to_main.yaml](https://github.com/colinwilliams91/helpful-gh-automations/actions/workflows/auto_merge_bridge_to_main.yaml) On push to designated "Bridge-Branch, automatically merged to `main`
  2. [auto_sync_main_to_bridge.yaml](https://github.com/colinwilliams91/helpful-gh-automations/actions/workflows/auto_sync_main_to_bridge.yaml) On any merge into `main`, changes are merged into "Bridge-Branch" to ensure no merge conflicts when the other Action fires

## How to Use:
- Bootstrap a repository from this template OR create a `.github/workflows` directory in your project root and copy/paste the two files I list below into it.
- Navigate to your projects "Settings" view on Github
- Click the "Actions" dropdown-section in the left-side toolbar
- Scroll to "Workflow permissions" and toggle "Read and write permissions" and "Allow GitHub Actions to create and approve pull requests"
  - You may need to perform this in the "Organization Settings" level above your repository if it is inside of one to establish default permissions across the group's repositories first
- Create a branch parallel to `main` (like a `development` or `staging` branch) (this will be your "Bridge-Branch") on the remote
- Plug the name of that branch into the places where `your-bridge-branch` exists in the [auto_merge_bridge_to_main.yaml](https://github.com/colinwilliams91/helpful-gh-automations/blob/main/.github/workflows/auto_merge_bridge_to_main.yaml) file
- Plug the name of that branch into the places where `your-bridge-branch` exists in the [auto_sync_main_to_bridge.yaml](https://github.com/colinwilliams91/helpful-gh-automations/blob/main/.github/workflows/auto_sync_main_to_bridge.yaml) file

## Test:
- Create a new feature branch
  - Make a small change like a "hello world" `.md`, `.sh` or any extremely simple file
  - Push it to the remote
  - Merge it into `main`
- Checkout the "Bridge-Branch" you created to ensure those new changes are reflected on this branch as well
- While checked out on the "Bridge-Branch"
  - Make another small change
  - Push that change to the remote "Bridge-Branch"
- Checkout `main` to ensure those changes are reflected here

You should also be able to view the Actions working here: https://github.com/your-organization?/your-repo/actions or by clicking the Actions tab on the view for your repo on GH.
