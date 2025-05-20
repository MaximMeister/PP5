# PP5

## Goal

In this exercise you will:

* Use Git **locally** on your own machine: create branches, make commits, and merge them back.
* Set up and interact with a **bare** Git repository on an SSH‐accessible server (e.g. **vorlesungsserver**, or any machine you have SSH access to).
* Push and pull to/from **GitHub** and the **THGA GitLab** server.
* Practice **forking** an existing repo, making changes, and submitting a **Pull Request** (on GitHub) or **Merge Request** (on GitLab).

**Important:** Start a stopwatch when you begin and work uninterruptedly for **90 minutes**. Once time is up, stop immediately and document exactly where you had to pause.

---

## Workflow

1. **Fork** this repository
2. **Modify & commit** your solution
3. **Submit your link for Review**

---

## Prerequisites

* Several starter repos are available here:
  [https://github.com/orgs/STEMgraph/repositories?q=Git%3A](https://github.com/orgs/STEMgraph/repositories?q=Git%3A)
* Ensure you have **SSH access** to a remote server (e.g., “vorlesungsserver”).
* Throughout, consult Git’s built-in man-pages (`git help <command>`) for explanations and options.

---

## Tasks

### Task 1: Local Git – Branching & Merging

1. Create a new directory in your home directory and initialize a repository in it. 
2. In one of your cloned repos, initialize a new branch called `feature-1`.
3. On `feature-1`, create a file `feature.txt` containing a short description of what you’re doing.
4. Commit your changes, then switch back to `master` (or `main`), and merge `feature-1` into your `master`.
5. Resolve any merge conflicts (if they arise) by hand, then commit the merge. 

**Your Commands & Output**

```bash
# Paste here the sequence of git commands you ran
# and the relevant terminal output (e.g., branch listing, merge messages)
```
  
    maxm@XPS-15-9520:~$ mkdir ~/git-test
    maxm@XPS-15-9520:~$ cd ~/git-test
    maxm@XPS-15-9520:~/git-test$ git init
    Initialized empty Git repository in /home/maxm/git-test/.git/
  
    maxm@XPS-15-9520:~/git-test$ git checkout -b feature-1
    Switched to a new branch 'feature-1'
  
    maxm@XPS-15-9520:~/git-test$ echo "Dies dient als eine kurze Beschreibung der Textdatei:        feature.txt" > feature.txt
  
    maxm@XPS-15-9520:~/git-test$ git config --global user.name "Maxim Meister"
    maxm@XPS-15-9520:~/git-test$ git config --global user.email "maxim.meister@stud.thga.com"
  
    maxm@XPS-15-9520:~/git-test$ git add feature.txt
    maxm@XPS-15-9520:~/git-test$ git commit -m "Die Textdatei feature.txt mit Beschreibung derer    wurde hinzugefügt"
    [feature-1 (root-commit) 96e37de] Die Textdatei feature.txt mit Beschreibung derer wurde         hinzugefügt
     1 file changed, 1 insertion(+)
     create mode 100644 feature.txt
  
    maxm@XPS-15-9520:~/git-test$ git checkout master
    Switched to branch 'master'
    maxm@XPS-15-9520:~/git-test$ git merge feature-1
    Updating 0000000..96e37de
    Fast-forward
     feature.txt | 1 +
     1 file changed, 1 insertion(+)
     create mode 100644 feature.txt
    maxm@XPS-15-9520:~/git-test$ git log
    commit 96e37dee3138ac76afe853d7a3e6f8381ac300b3 (HEAD -> feature-1)
    Author: Maxim Meister <maxim.meister@stud.thga.com>
    Date:   Mon May 19 13:50:52 2025 +0200
  
      Die Textdatei feature.txt mit Beschreibung derer wurde hinzugefügt
    maxm@XPS-15-9520:~/git-test$
    
---

### Task 2: Bare Repository on an SSH Server

1. On your SSH server (e.g., “vorlesungsserver”), create a **bare** repo at `~/repos/myproject.git`:

   ```bash
   ssh youruser@vorlesungsserver \
     "mkdir -p ~/repos/myproject.git && cd ~/repos/myproject.git && git init --bare"
   ```
2. On your local machine, add it as a remote named `origin-ssh`:

   ```bash
   git remote add origin-ssh youruser@vorlesungsserver:~/repos/myproject.git
   ```
3. Push your `master` branch to `origin-ssh`, then clone it into a fresh directory to verify.

**Your Commands & Output**

```bash
# Paste here the push & clone commands and outputs
```

    
    user87@vorlesung:~$ "mkdir -p ~/repos/myproject.git && cd ~/repos/myproject.git && git init --bare"
    -bash: mkdir -p ~/repos/myproject.git && cd ~/repos/myproject.git && git init --bare: No such file or directory
    user87@vorlesung:~$ ls
    local_copy.txt  login_tasks.sh  projects  scp4
    user87@vorlesung:~$ ls -la
    total 52
    drwx------   6 user87 user87 4096 May 19 18:11 .
    drwxr-xr-x 161 root   root   4096 Apr 20 16:35 ..
    -rw-------   1 user87 user87  941 May 19 18:25 .bash_history
    -rw-r--r--   1 user87 user87  220 Apr  2 12:56 .bash_logout
    -rw-r--r--   1 user87 user87 3550 May 19 06:17 .bashrc
    -rw-r--r--   1 user87 user87    0 Apr  2 12:56 .cloud-locale-test.skip
    drwxr-xr-x   3 user87 user87 4096 May 19 18:11 .local
    -rw-r--r--   1 user87 user87   10 May 19 07:36 local_copy.txt
    -rwxr-xr-x   1 user87 user87  729 May 19 06:55 login_tasks.sh
    -rw-r--r--   1 user87 user87  807 Apr  2 12:56 .profile
    drwxr-xr-x   2 user87 user87 4096 May 19 06:16 projects
    drwxr-xr-x   4 user87 user87 4096 May 19 07:38 scp4
    drwx------   2 user87 user87 4096 May 19 18:25 .ssh
    -rw-------   1 user87 user87 2304 May 19 06:55 .viminfo
    user87@vorlesung:~$ mkdir -p ~/repos/myproject.git && cd ~/repos/myproject.g
    it && git init --bare
    hint: Using 'master' as the name for the initial branch. This default branch name
    hint: is subject to change. To configure the initial branch name to use in all
    hint: of your new repositories, which will suppress this warning, call:
    hint:
    hint:   git config --global init.defaultBranch <name>
    hint:
    hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
    hint: 'development'. The just-created branch can be renamed via this command:
    hint:
    hint:   git branch -m <name>
    Initialized empty Git repository in /home/user87/repos/myproject.git/
    user87@vorlesung:~/repos/myproject.git$ cd
    user87@vorlesung:~$ tree -d ~
    /home/user87
    ├── projects
    ├── repos
    │   └── myproject.git
    │       ├── branches
    │       ├── hooks
    │       ├── info
    │       ├── objects
    │       │   ├── info
    │       │   └── pack
    │       └── refs
    │           ├── heads
    │           └── tags
    └── scp4
        ├── backup
        └── destination
    
    16 directories
    user87@vorlesung:~$ exit
    logout
    Connection to 128.140.85.215 closed.
    maxm@XPS-15-9520:~$ cd git-test/
    maxm@XPS-15-9520:~/git-test$ git remote add origin-ssh vorlesung:~/repos/myproject.git
    maxm@XPS-15-9520:~/git-test$ git push origin-ssh master
    error: src refspec master does not match any
    error: failed to push some refs to 'vorlesung:~/repos/myproject.git'
    maxm@XPS-15-9520:~/git-test$ git branch
    * feature-1
    maxm@XPS-15-9520:~/git-test$ git remote add origin-ssh user87@128.140.85.215:~/repos/myproject.git
    error: remote origin-ssh already exists.
    maxm@XPS-15-9520:~/git-test$ git push origin-ssh master
    error: src refspec master does not match any
    error: failed to push some refs to 'vorlesung:~/repos/myproject.git'
    
    maxm@XPS-15-9520:~/git-test$ git checkout -b master
    Switched to a new branch 'master'
    maxm@XPS-15-9520:~/git-test$ git push origin-ssh master
    Enumerating objects: 3, done.
    Counting objects: 100% (3/3), done.
    Delta compression using up to 20 threads
    Compressing objects: 100% (2/2), done.
    Writing objects: 100% (3/3), 329 bytes | 329.00 KiB/s, done.
    Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    To vorlesung:~/repos/myproject.git
     * [new branch]      master -> master
    maxm@XPS-15-9520:~/git-test$ cd ~
    mkdir git-clone-test
    cd git-clone-test
    git clone vorlesung:~/repos/myproject.git
    Cloning into 'myproject'...
    remote: Enumerating objects: 3, done.
    remote: Counting objects: 100% (3/3), done.
    remote: Compressing objects: 100% (2/2), done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    Receiving objects: 100% (3/3), done.

---

### Task 3: GitHub & THGA GitLab

1. On [GitHub](github.com), create a new empty repo under your account named `myproject-gh`.
2. On [THGA GitLab](gitlab.thga.de), create a new project named `myproject-gl`.
3. In your local repository, add these as remotes:

   ```bash
   git remote add github  git@github.com:YOUR_USERNAME/myproject-gh.git
   git remote add gitlab  git@gitlab.thga.de:YOUR_USERNAME/myproject-gl.git
   ```
4. Push your `master` branch to both `github` and `gitlab` remotes.

> Hint: You are just adding two more bare-remotes to your already existing repository!

**Your Commands & Output**

```bash
# Paste here the remote‐adding & push outputs
```

**Terminalverlauf für Github**
    
    maxm@XPS-15-9520:mkdir -p ~/git-clone-test
    maxm@XPS-15-9520:~/git-clone-test$ tree -d ~
    /home/maxm
    ├── git-clone-test
    │   └── myproject
    ├── git-test
    └── scp_test
    
    5 directories

*Auszug des Terminals, für den ertsen Versuch zu Verbindung mit github, anschließend mit ssh*

            maxm@XPS-15-9520:~/git-clone-test$ ls -la
            total 12
            drwxr-xr-x  3 maxm maxm 4096 May 19 22:52 .
            drwxr-x--- 10 maxm maxm 4096 May 19 22:52 ..
            drwxr-xr-x  3 maxm maxm 4096 May 19 22:52 myproject
            maxm@XPS-15-9520:~/git-clone-test$ cd
            maxm@XPS-15-9520:~$ cd git-test/
            maxm@XPS-15-9520:~/git-test$ git remote add github                       
            https://github.com/MaximMeister/myproject-gh.git
            maxm@XPS-15-9520:~/git-test$ git push -u github master
            Username for 'https://github.com':
            MaximMeisterPassword for 'https://github.com':
            remote: No anonymous write access.
            fatal: Authentication failed for 'https://github.com/MaximMeister/myproject-gh.git/'
            maxm@XPS-15-9520:~/git-test$ git push -u github master
            Username for 'https://github.com': MaximMeister
            Password for 'https://MaximMeister@github.com':
            remote: Support for password authentication was removed on August 13, 2021.
            remote: Please see https://docs.github.com/get-started/getting-started-with-        
            git/about-  
            remote-repositories#cloning-with-https-urls for information on currently       
            recommended modes of authentication.
            fatal: Authentication failed for 'https://github.com/MaximMeister/myproject-gh.git/'
            maxm@XPS-15-9520:~/git-test$ maxm@XPS-15-9520:~/git-test$ git push -u github master
            Username for 'https://github.com': MaximMeister
            Password for 'https://MaximMeister@github.com':
            remote: Support for password authentication was removed on August 13, 2021.
            remote: Please see https://docs.github.com/get-started/getting-started-with-      
            git/about- remote-repositories#cloning-with-https-urls for information on currently             recommended modes of authentication.
            fatal: Authentication failed for 'https://github.com/MaximMeister/myproject-gh.git/'

    maxm@XPS-15-9520:~/git-test$ cd
    maxm@XPS-15-9520:~$ cat ~/.ssh/id_ed25519.pub
    ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIGRt/WAGCaCq5oTzkbmHaPad2KNTUk/P0BAso7DM2sEt maxm2@ssh
    maxm@XPS-15-9520:~$ ssh -T git@github.com
    The authenticity of host 'github.com (140.82.121.4)' can't be established.
    ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
    This key is not known by any other names.
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
    Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
    Hi MaximMeister! You've successfully authenticated, but GitHub does not provide shell access.
    
    
    maxm@XPS-15-9520:~/git-test$ git remote set-url github git@github.com:MaximMeister/myproject-gh.git
    maxm@XPS-15-9520:~/git-test$ git remote add github git@github.com:MaximMeister/myproject-gh.git
    error: remote github already exists.
    maxm@XPS-15-9520:~/git-test$ git branch
      feature-1
    * master
    maxm@XPS-15-9520:~/git-test$ git push -u github master
    Enumerating objects: 3, done.
    Counting objects: 100% (3/3), done.
    Delta compression using up to 20 threads
    Compressing objects: 100% (2/2), done.
    Writing objects: 100% (3/3), 329 bytes | 329.00 KiB/s, done.
    Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    To github.com:MaximMeister/myproject-gh.git
     * [new branch]      master -> master
    branch 'master' set up to track 'github/master'.

    **Terminalverlauf für Gitlab**
    
    maxm@XPS-15-9520:~/git-test$ git remote add gitlab  [git@gitlab.thga.de](mailto:git@gitlab.thga.de)\:maxim.meister/myproject-gl.git
    -bash: syntax error near unexpected token `('
    maxm@XPS-15-9520:~/git-test$ git remote add gitlab  git@gitlab.thga.de:maxim.meister/myproject-gl.git
    maxm@XPS-15-9520:~/git-test$ git push -u gitlab master
    The authenticity of host 'gitlab.thga.de (195.37.5.155)' can't be established.
    ED25519 key fingerprint is SHA256:4+4+prKVzsU8Bw0eBjkbBm86bl9+OinZJIidEMGHpqc.
    This key is not known by any other names.
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
    Warning: Permanently added 'gitlab.thga.de' (ED25519) to the list of known hosts.
    Enumerating objects: 3, done.
    Counting objects: 100% (3/3), done.
    Delta compression using up to 20 threads
    Compressing objects: 100% (2/2), done.
    Writing objects: 100% (3/3), 329 bytes | 164.00 KiB/s, done.
    Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    To gitlab.thga.de:maxim.meister/myproject-gl.git
     * [new branch]      master -> master
    branch 'master' set up to track 'gitlab/master'.
    maxm@XPS-15-9520:~/git-test$ maxm@XPS-15-9520:~/git-test$ git push -u github master
    Enumerating objects: 3, done.
    Counting objects: 100% (3/3), done.
    Delta compression using up to 20 threads
    Compressing objects: 100% (2/2), done.
    Writing objects: 100% (3/3), 329 bytes | 329.00 KiB/s, done.
    Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    To github.com:MaximMeister/myproject-gh.git
     * [new branch]      master -> master
    branch 'master' set up to track 'github/master'.
    maxm@XPS-15-9520:~/git-test$ git remote add gitlab  [git@gitlab.thga.de](mailto:git@gitlab.thga.de)\:maxim.meister/myproject-gl.git
    -bash: syntax error near unexpected token `('
    maxm@XPS-15-9520:~/git-test$ git remote add gitlab  git@gitlab.thga.de:maxim.meister/myproject-gl.git
    maxm@XPS-15-9520:~/git-test$ git push -u gitlab master
    The authenticity of host 'gitlab.thga.de (195.37.5.155)' can't be established.
    ED25519 key fingerprint is SHA256:4+4+prKVzsU8Bw0eBjkbBm86bl9+OinZJIidEMGHpqc.
    This key is not known by any other names.
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
    Warning: Permanently added 'gitlab.thga.de' (ED25519) to the list of known hosts.
    Enumerating objects: 3, done.
    Counting objects: 100% (3/3), done.
    Delta compression using up to 20 threads
    Compressing objects: 100% (2/2), done.
    Writing objects: 100% (3/3), 329 bytes | 164.00 KiB/s, done.
    Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    To gitlab.thga.de:maxim.meister/myproject-gl.git
     * [new branch]      master -> master
    branch 'master' set up to track 'gitlab/master'.
    

---

### Task 4: Fork, Modify, and Pull/Merge Request

1. On GitHub, **fork** one of the repos from the STEMgraph org.
2. Clone your fork locally, create a branch `pp5-changes`, and make a small change (e.g., update the README).
3. Commit and push `pp5-changes` to **your** fork, then open a **Pull Request** against the original repo.
4. Repeat on THGA GitLab: fork another students repository, clone, branch, change, push, and open a **Merge Request**. If your peers opened a merge request to your repository, review and merge or decline it!

**Your PR/MR Links & Descriptions**

* GitHub PR: *paste URL and a one-sentence summary*
    https://github.com/STEMgraph/474307f2-a30c-4639-9379-298bf1a4c00b/pull/1

    https://github.com/STEMgraph/474307f2-a30c-4639-9379-298bf1a4c00b/pull/2/files#diff-            b335630551682c19a781afebcf4d07bf978fb1f8ac04c6bf87428ed5106870f5
  
* GitLab MR: *paste URL and a one-sentence summary*

    https://gitlab.thga.de/279789/myproject-gl/-/merge_requests/2

---

**Remember:** Stop working after **90 minutes** and record where you stopped!
