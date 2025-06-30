---
type: docs
url: "hub/docs/folder/Technical-Guide"
---

# Introduction

This guide describes the structured branching model used to integrate GIMP development updates into the Artbox project.

## Contents

- [Updating Artbox to GIMP Dev](#updating-artbox-to-gimp-dev)
   - [Step 1: Construct the Common Base](#step-1-construct-the-common-base)
   - [Step 2: Construct Feature Branches from the Common Base](#step-2-construct-feature-branches-from-the-common-base)
   - [Step 3: Construct Artbox from the Common Base and Feature Branches](#step-3-construct-artbox-from-the-common-base-and-feature-branches)
- [Convert Branches](#convert-branches)
   - [Example of a Compound Convert Branch: convert-paintbrush-all-merged](#example-of-a-compound-convert-branch-convert-paintbrush-all-merged)
- [Feature Branches](#feature-branches)
   - [Example of a Compound Feature Branch: feature-paintbrush-options](#example-of-a-compound-feature-branch-feature-paintbrush-options)
- [Notes](#notes)

## Branch Development Flow for GIMP to Artbox

The development process follows a structured branching model where the GIMP development branch serves as the foundation. The 'convert-to-artbox' branch is created from GIMP Dev and serves as the common base for all feature branches. These feature branches contribute to the final 'artbox' branch, which represents the integrated work from all features.

### Updating Artbox to GIMP Dev

To keep Artbox up-to-date with the GIMP development branch, we follow a structured process divided into three main steps

#### Step 1: Construct the Common Base

- **Reset the Common Base:** Reset the 'convert-to-artbox' branch to the latest commit from the GIMP master branch.
- **Rebase the Convert Branches:** Rebase the convert branches to the GIMP master branch.
- **Merge Convert Branches:** Merge all relevant convert branches into the 'convert-to-artbox' branch.
- **Squash Commit History:** Squash the commit history of these merges into a single commit to simplify history.

#### Step 2: Construct Feature Branches from the Common Base

- **Update the Common Base:** Ensure that the 'convert-to-artbox' branch is up to date with the latest changes.
- **Clone and Layer Commits:**
  - Clone the 'convert-to-artbox' branch.
  - Pick and apply commits from each existing feature branch onto this clone.
- **Replace Old Feature Branches:**
  - Delete the old feature branches.
  - Rename the cloned branches to replace the old feature branches.
- **Repeat for All Feature Branches:** Perform the above steps for each feature branch that needs updating.

#### Step 3: Construct Artbox from the Common Base and Feature Branches

- **Reset Artbox Branch:** Reset the 'artbox' branch to the 'convert-to-artbox' branch to incorporate the latest changes.
- **Merge Updated Feature Branches:** Merge all updated feature branches into the 'artbox' branch to consolidate the changes.
- **Squash Commit History:** Squash the commit history of these merges into a single commit to simplify history.

### Convert Branches

A convert branch is used to adjust the latest GIMP master branch to support the Artbox feature branches or to make specific changes to the default GIMP application. These branches are merged into a single 'convert-to-artbox' branch, which serves as the common base layer.

The current strategy is to place any heavily modified file that supports multiple feature branches—through the addition of new data structures—into a convert branch. This approach helps consolidate overlapping changes in one place, while maintaining the core code that performs the main functions in separate feature branches.

#### Identifying Conflicts

Updating Artbox to the GIMP development branch involves identifying any conflicts or changes introduced by GIMP that overlap with Artbox changes.

- First Stage Conflict: Rebasing the convert branches to GIMP master branch.
- Second Stage Conflict: Cherry-picking the merges from feature branches onto the new common branch.

These conflicts can be resolved fairly easily due to the automated construction process and granularity of the changes.

### Feature Branches

Feature branches are concerned with the core code implementation of a new feature. They may rely upon a convert branch to have paved the way with additional GUI options, preferences or other global variables.

### Notes

The key difference between a feature branch and a convert branch is that feature branches build on top of the convert-to-artbox branch. In contrast, a convert branch is an adjustment made directly to the GIMP development master branch.
