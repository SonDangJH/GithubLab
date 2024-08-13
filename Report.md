Difference between reset and revert

 - Suppose there are 3 commits A B C
 - Git reset —hard C~2 will remove B from the commit history

 - If using git revert C
 - Git will create a commit that reverses commit C, causing the changes in commit C to be lost, but commit C still exists in history. 
 - A rollback commit will invalidate the changes brought by commit C but does not cause commit C to be lost in the commit history


Difference between merge and rebase
    - Suppose there is a main branch and a feature branch
    - The main branch has 3 commits. A B C
    - Feature branch has 2 commits D E

  - Git merge will create a new commit, commit F, mark merge and combine the two branches, now the history has a branch.

  - Git rebase will create new commits D' E' so that these commits feel like they were just committed after commit C, then git will move Comat D' E' directly into the main branch: we will have A B C D 'E' looks more linear


  - It should be noted that rebase seems more dangerous and is only suitable for personal projects, or before a pull request if you want to clean up commit histories
  - If we assume the feature branch is shared and someone relies on the feature branch to work, rebasing is dangerous and will create serious conflicts.
  - Furthermore, when rebasing, the commit history has been modified, so tracking the commit history again is difficult
