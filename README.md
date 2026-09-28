# Hillsborough College - Ansible


## Introduction

This lab covers the basics of Ansible and using git.

__Development Terms__
```yaml
- term: Instantiate
  description: |
    Create an active object that is based on a predefined blueprint or idea.

- term: Feature 
  description: |
    A distinct piece of functionality or standalone capability built into 
    a software application to deliver specific value or utility to the user.

- term: Bug
  description: |
    An unexpected flaw, error, or fault in the source code or system architecture 
    of an application that causes it to produce incorrect output, crash, or behave 
    in ways unintended.

- term: Regression
  description: |
    An unexpected flaw or system failure introduced into previously working 
    functionality as a result of recent code changes or updates.

- term: Refinement
  description: |
    The collaborative process of reviewing, clarifying, and breaking down broad 
    product requirements or high-level goals into clear, actionable, and estimated 
    work items ready for implementation.
```

Now let's get into git!

## What is Git?

As a quick recap, Git is distributed version control system designed to track changes in source code and manage project files over time. 
Think of git as an account book that tracks every single change from birth to death of a repository.

### Git workflow: The Three States
The most important part to remember about Git is it has three main states that your files can reside in: modified, staged, and committed:

  * Modified means that you have changed the file but have not committed it to your database yet.
  * Staged means that you have marked a modified file in its current version to go into your next commit snapshot.
  * Committed means that the data is safely stored in your local database.

### Getting a Git Repository
You typically obtain a Git repository in one of two ways:

  * You can take a local directory that is currently not under version control, and turn it into a Git repository, or
  * You can clone an existing Git repository from elsewhere.

### Git terms
```yaml
- term: repository
  description: |
    A collection of refs together with an object database 
    containing all objects which are reachable from the refs.

- term: refs
  description: |
    A name that points to an object name or another ref ( aka reference ).

- term: object
  description: The unit of storage in Git. 

- term: commit
  description: |
    A single point in the Git history, the entire history of a project 
    is represented as a set of interrelated commits. Think of a commmit
    as a change to a bunch of objects at a point in time.

- term: branch
  description: |
     A branch is a line of development that forks off a main branch or 
     a subsequent branch.

- term: head
  description: A named reference to the commit at the tip of a branch.

- term: origin
  description: The upstream repository relative to the local repository

- term: fetch
  description: |
    Downloads remote commits, tags, and refs into local remote-tracking 
    branches (e.g., origin/main).

- term: pull
  description: |
    Downloads remote commits AND immediately merges them into your active 
    local branch.

- term: push
  description: Push contents from local to origin

- term: merge
  description: Bring the contents of another branch into another branch.
```

### Basic git commands

Below is a list of basic git commands to get us started

```yaml
- name: git clone
  description: Clone a repository into a new directory

- name: git pull
  description: Fetch from and integrate with another repository or a local branch

- name: git checkout
  description: |
    Switch branches or restore working tree files; When the arguemnt -b
    a new branch is named <new-branch>, starts at the current commit and 
    instantiates the new branch.
  
- name: git switch
  description: |
     Switch to a specified branch. The working tree and the index are updated 
     to match the branch. All new commits will be added to the tip of this branch.
```
---

##### Environment Setup 

Assuming the environemt is [Fedora 44 workstation](https://fedoraproject.org/workstation/download/)

First we need to generate an ssh key
```bash
~$ ssh-keygen -t ed25519
Generating public/private ed25519 key pair.
Enter passphrase for "ed25519" (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in file
Your public key has been saved in file.pub
The key fingerprint is:
SHA256:53chxo7XFs7+DO43KMmicXayRGlBYiJGI2t3KMqevR8 user@localhost.localdomain
The key's randomart image is:
+--[ED25519 256]--+
| ..= . o .       |
|  + + o o        |
| + o .   .       |
|+ o .     o.     |
|..      S+. + o  |
|. o     oo + = o |
| o . E . =+.= O  |
|    . . =.+* * +.|
|   ... .... ..+o+|
+----[SHA256]-----+
```

__Add the ed25519 generated key to the__ `$HOME/.ssh/authorized_keys` __file__
```bash
~$ cat $HOME/.ssh/id_ed25519.pub >> $HOME/.ssh/authorized_keys
~$ cat $HOME/.ssh/authorized_keys 
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILT3AbXdI7DvwPrAJqhNm8QJGpcSe+mR9uIrQJiGgNZj user@localhost.localdomain
```

__As a dependency for ansible we need to assert sshd is running__
```bash
~$ systemctl enable --now sshd
~$ sudo systemctl enable --now sshd
Created symlink '/etc/systemd/system/multi-user.target.wants/sshd.service' → '/usr/lib/systemd/system/sshd.service'.
~$ sudo systemctl status sshd
● sshd.service - OpenSSH server daemon
     Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; preset: disabled)
    Drop-In: /usr/lib/systemd/system/service.d
             └─10-timeout-abort.conf
     Active: active (running) since Mon 2026-09-28 09:02:51 EDT; 28s ago
 Invocation: ce960ec6dd274435a0ee64d0e8d83751
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 12828 (sshd)
      Tasks: 1 (limit: 9336)
     Memory: 1.2M (peak: 1.5M)
        CPU: 8ms
     CGroup: /system.slice/sshd.service
             └─12828 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

Sep 28 09:02:51 demovm systemd[1]: Starting sshd.service - OpenSSH server daemon...
Sep 28 09:02:51 demovm sshd[12828]: Server listening on 0.0.0.0 port 22.
Sep 28 09:02:51 demovm sshd[12828]: Server listening on :: port 22.
Sep 28 09:02:51 demovm systemd[1]: Started sshd.service - OpenSSH server daemon.
```

__Install ansible and ansible-lint__
```bash
~$ sudo dnf -y install ansible ansible-lint
```

__Install Git__
```bash
~$ sudo dnf -y install git
```

__Now we can Clone the lab, collection and container repository__
```bash
~$ git clone https://github.com/desync-it/hillsborough-ansible-labs.git ansible
~$ git clone https://github.com/desync-it/hillsborough-collection.git
~$ git clone https://github.com/desync-it/hillsborough-webserver.git 
```

## References
1. [container/hillsborough-webserver](https://github.com/desync-it/hillsborough-webserver)
2. [collection/hillsborough-collection](https://github.com/desync-it/hillsborough-collection)
3. [Git Glossary](https://git-scm.com/docs/gitglossary)
4. [About Ansible Lint](https://docs.ansible.com/projects/lint)
