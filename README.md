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