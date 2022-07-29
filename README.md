# july-2022
#### BOA DevOps basic Sesion from 28th to 30th July, followed by an Exam
#### Topics to be covered
1. git & github
2. ansible
3. Jenkins
4. Jenkins & Git Integration
5. Jenkins & GitHub Integration
5. Jenkins & Ansible Integration

#### working with GIT `local repository`
##### setup author details
1. `git config --global user.email "your-mail-id"`
2. `git config --global user.name "your-github-account-name"`

##### adding first commit
1. Add some file and add some data or data in README.md. Save the file
2. `git status`
```
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```
3. `git add file-name-you-have-update`
4. `git status`
```
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md
```
5. Check logs before commit: `git log --oneline`
6. Commit changes: `git commit -m "my first commit"`
6. Check the logs again there is a new entry
6. Check status again
```
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
##### In order to add or commit the file in single command use:
```
git commit -am "updated the steps for activity 1"
```
##### updating code in the remote repository
```
git push origin main
```
#### There is a concept/feature in GitHub to block direct PUSH to the protected branches and all changes should route via `Pull Request` and can be enabled for Administrators as well
#### Branching & Pull Requests (Review)
##### Working with branches
1. Create new branch with latest version of current branch: `git branch feature-1`
2. Switch to the new branch: `git switch feature-1`
3. Check logs: `git log --oneline`
```
e6180c4 (HEAD -> feature-1, main) updated about protected branches
c8e1f9f (origin/main, origin/HEAD) updated about protected branches
9e415ae update with push command
4398e3d updated the steps for activity 1
be44b7d updated course topics
a0187b6 Initial commit
```
4. Add some new changes and commit them
5. Check logs in new branch: `git log --oneline`
```
e206107 (HEAD -> feature-1) updated about branches
e6180c4 (main) updated about protected branches
c8e1f9f (origin/main, origin/HEAD) updated about protected branches
9e415ae update with push command
4398e3d updated the steps for activity 1
be44b7d updated course topics
a0187b6 Initial commit
```
6. Check the logs in `main` branch: `git log --oneline main`, in output the latest commit is missing as it was being done in the new branch
```
e6180c4 (main) updated about protected branches
c8e1f9f (origin/main, origin/HEAD) updated about protected branches
9e415ae update with push command
4398e3d updated the steps for activity 1
be44b7d updated course topics
a0187b6 Initial commit
```
7. PUSH changes feature-1 changes to the REMOTE: `git push origin feature-1`
#### Getting the changes pushed by other in the remote branch to the local branch using `pull`
1. Switch the branch to update the code: `git switch main`
2. Check current log: `git log --oneline`
```
e6180c4 (HEAD -> main) updated about protected branches
c8e1f9f (origin/main, origin/HEAD) updated about protected branches
9e415ae update with push command
4398e3d updated the steps for activity 1
be44b7d updated course topics
a0187b6 Initial commit
```
3. Pull changes from remote source branch, in current scenerio, `main`: `git pull origin main`
4. Check the logs again: `git log --oneline`
```
3fe1709 (HEAD -> main, origin/main, origin/HEAD) Merge pull request #1 from kul-boa/feature-1
f89645e (origin/feature-1, feature-1) updated about branches
e206107 updated about branches
e6180c4 updated about protected branches
c8e1f9f updated about protected branches
9e415ae update with push command
4398e3d updated the steps for activity 1
be44b7d updated course topics
a0187b6 Initial commit
```
#### delete local branch
1. `git branch`
2. `git branch -d feature-1`
3. `git branch`

## Ansible: Infrastructure Configuration Management
1. Login to the server
2. Change hostname: `sudo hostnamectl set-hostname kmayer && bash`