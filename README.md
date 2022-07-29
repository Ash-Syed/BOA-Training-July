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
##### Installing ansible on ubuntu:20.04
1. `sudo apt-get update -y`
2. `sudo apt-get install -y ansible`
3. `ansible --version`
4. `sudo ls -ltr /etc/ansible/`
##### Setting up `inventory` and `ansible.cfg`
1. `mkdir ansible && cd ansible`
2. Get system private IP using: `hostname -i`, copy the first string like: `172.31.18.37`
3. add the same in `inventory` file, create the file if doesn't exist
4. Let's try to ping: `ansible all -m ping`
```
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'
```
5. Create `ansible.cfg` in the current directory
```
touch ansible.cfg
echo "[defaults]" >> ansible.cfg
echo "inventory = ~/ansible/inventory" >> ansible.cfg
echo "host_key_checking = False" >> ansible.cfg
```
6. `ansible all -m ping`
```
172.31.18.157 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: ubuntu@172.31.18.157: Permission denied (publickey).",
    "unreachable": true
}
```
##### In order to fix the above error for the local system update the inventory file as shown below and the run `ansible all -m ping` to test the connection
```
172.31.18.157 ansible_connection=local
```
##### for the external server, authentication (with password or password less is required).
##### for password less authentication, add the `privete_key` path in the `ansible.cfg` to setup the connection with server as show below
```
[defaults]
inventory = ~/ansible/inventory
host_key_checking = False
private_key_file = ~/ansible/kul.pem
```
##### Creating first playbook with the name `install_docker.yaml`
```
- name: Install Docker
  hosts: all

  become: yes

  tasks:
  - name: install dependency packages
    package:
      name:
      - ca-certificates
      - curl
      - gnupg
      - lsb-release
      state: present
      update_cache: yes
```
##### Runthe playbook using: `ansible-playbook install_docker.yaml`
##### updated playbook with docker installation steps
```
- name: Install Docker
  hosts: kul

  become: yes

  tasks:
  - name: install dependency packages
    package:
      name:
      - ca-certificates
      - curl
      - gnupg
      - lsb-release
      state: present
      update_cache: yes
  - name: install docker
    package:
      name: docker.io
      state: present
  - name: update owner for /var/run/docker.sock
    file:
      path: /var/run/docker.sock
      state: file
      owner: ubuntu
```
