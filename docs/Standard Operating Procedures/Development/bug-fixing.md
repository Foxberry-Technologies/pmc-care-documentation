# Bugs & Hotfixes
GitLab Workflow for Fixing Coding Bugs using GitFlow Convention

This documentation outlines the process of fixing coding bugs using the GitLab platform and following the GitFlow convention. GitLab provides a powerful set of tools for version control and collaboration, and the GitFlow convention helps maintain a structured and organized workflow for managing code changes.

## Prerequisites

- Basic understanding of Git version control.
- Familiarity with the GitFlow branching model.
- Access to a GitLab repository.

## GitFlow Overview

GitFlow is a branching model that defines a set of branching and merging strategies to manage code changes. It involves two main branches: `master` and `develop`, along with several supporting branches for feature development and bug fixes.

- `master`: Represents the production-ready codebase. Only stable and tested code is merged into this branch.
- `develop`: The integration branch where features and bug fixes are merged before being thoroughly tested.
- Feature branches: Created for developing new features and are branched off from the `develop` branch.
- Bug fix branches: Similar to feature branches but created specifically for fixing bugs.

## Bug Fix Workflow

Follow these steps to fix coding bugs using the GitLab platform and adhering to the GitFlow convention:

### Step 1: Create a Bug Fix Branch

1. Ensure you are on the `develop` branch:
   ```
   git checkout develop
   ```

2. Pull the latest changes from the remote repository:
   ```
   git pull origin develop
   ```

3. Create a new bug fix branch named `bug/bug-name`:
   ```
   git checkout -b bug/bug-name
   ```

### Step 2: Fix the Bug

1. Make necessary code changes to fix the bug on the bug fix branch.
2. Regularly commit your changes with meaningful commit messages:
   ```
   git commit -m "Fix issue with feature X causing Y"
   ```

### Step 3: Push Bug Fix Branch

1. Push the bug fix branch to the remote repository:
   ```
   git push origin bug/bug-name
   ```

### Step 4: Create a Merge Request

1. Visit your GitLab repository.
2. Click on the "Merge Requests" tab.
3. Click the "New Merge Request" button.
4. Set the source branch as `bug/bug-name` and the target branch as `develop`.
5. Add a descriptive title and description for the merge request.
6. Assign relevant reviewers and label the merge request appropriately.
7. Click the "Submit merge request" button.

### Step 5: Review and Resolve Feedback

1. Reviewers will provide feedback on the merge request.
2. Address and resolve feedback by making necessary changes to the bug fix branch.
3. Commit and push the changes.

### Step 6: Merge the Bug Fix

1. Once the merge request is approved and all feedback is addressed, click the "Merge" button on GitLab.
2. Choose the option to "Delete source branch" since the bug fix branch is no longer needed.

### Step 7: Update Local Repository

1. Switch back to the `develop` branch:
   ```
   git checkout develop
   ```

2. Pull the latest changes from the remote repository:
   ```
   git pull origin develop
   ```

### Step 8: Release Deployment

Bug fixes in the `develop` branch will eventually be merged into the `master` branch during a release cycle.

## Conclusion

Following the GitFlow convention and using GitLab's collaborative features provides a structured and efficient workflow for fixing coding bugs. This ensures that code changes are well-organized, reviewed, and tested before being merged into the production-ready `master` branch.