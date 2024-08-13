
We have 2 big branch call master (to hold test features for test site) & production. 
Ex1: --------------------------------------------------------------------------------------

- (Ap & Ev) When we are creating new feature, what branch should we based on and why?

Suppose production A B C D
        master     A B C D E F

+ Suppose we are creating new feature and that feature does not based on any other feature
 - Create a new branch feature/new_feature based on master branch and develop on this branch

   * git checkout -b feature/new_feature master


+ Suppose we just want to release only that new feature on production, but do not want to release other feature on master branch
 - Find the feature/featureD branch that does not exist the feature you do not want to release.
 - Create new branch feature/new_feature base on feature/featureD (A B C D) and develop on this branch

   * git checkout -b feature/new_feature feature/featureD    


+ Suppose we are creating a feature that rely on commit F, but you do not want to release the feature on commit E
 - Find the based branch contains commit F but not commit E (eg feature/featureF)
 - Create new branch based on that branch and develop on in
    * git checkout -b feature/new_feature feature/featureF
    


Ex2: ------------------------------------------------------------------------------------
 (Ap) If we have a feature branch that haven't been merged to production and that branch have bug, what course of action are you going to do with Git to before resolving the bug?

+ Suppose that bug is just exist in the commit that every other branch does not have
 - Create new branch based from the bug branch and resolve bug
 - Merge fix bug branch into the feature branch
   * git checkout -b fix/bug_branch feature/bug_feature
   * git checkout feature/bug_feature
   * git merge fix/bug_branch

+ Suppose that bug is exist on a commit that exist in some branch based on this bug branch feature/featureA and feature/featureB
 - Find the branch that all the bug branch is based on the bug commit, eg bug is in commit C, find the branch that feature/featureA and feature/featureB based on the commit C
 - Create new branch based on that branch and fix
 - Merge that fix bug branch into the based branch
   * git checkout -b fix/bug_branch feature/based_branch
   * git checkout feature/based_branch
   * git merge fix/bug_branch


Ex3: ------------------------------------------------------------------------------------
If someone accidentally merge a feature (feature/delete-user) onto production and have a list of commitId ended with (0492978, fc9348c, k101100), then another commit (a1fsas8) is added on top of the production branch. How do we remove that merged feature? 

Way 1:
- Find the branch that only contains a1fsas8 call feature/a1fsas8
- reset all the wrong commit in production
    * git checkout production
    * git reset --hard HEAD~4
- merge the feature/a1fsas8 into production
    * git merge feature/a1fsas8

Way 2:
- Create new branch that only contains commit a1fsas8
    * git checkout -b new_branch a1fsas8
- Remove all the wrong commit in production
    * git checkout production
    * git reset --hard HEAD~4
- cherry_pick nhánh new_branch vào production
    * git cherry_pick new_branch

Way 3:
- Find the branch that only contains a1fsas8 call feature/a1fsas8
- reset all the wrong commit in production
    * git checkout production
    * git reset --hard HEAD~4
- rebase the feature/a1fsas8 on production
    * git checkout feature/a1fsas8
    * git rebase production

Way 4:
- Creating new branch to fix, revert all the wrong commit and merge into the feature branch
 * git checkout -b hotfix-revert-feature
 * git revert k101100
 * git revert fc9348c
 * git revert 0492978
 * git checkout production
 * git merge hot fix-revert-feature




