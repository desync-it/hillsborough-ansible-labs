# Hillsborough College - Ansible

This lab covers the basics of Ansible with a git setup portion


## Introduction

Before we get into configuring and deploying ansible we need to get familiar with git

### Git

#### Terms
```yaml
- term: branch
  description: A branch is a line of development

- term: commit
  description: |
    A single point in the Git history, the entire history of a project 
    is represented as a set of interrelated commits.

- term: head
  description: A named reference to the commit at the tip of a branch.

- term: origin
  description: The default upstream repository.

- term: fetch
  description: |
    Fetching a branch means to get the branch’s head ref from a remote repository, 
    to find out which objects are missing from the local object database.

- term: push
  description: Push contents from local to origin

- term: pull
  description: Pulling a branch means to fetch it and merge it 

- term: merge
  description: Bring the contents of another branch into another branch.

```

Reference [gitglossary - A Git Glossary](https://git-scm.com/docs/gitglossary)

#### Basic commands

```yaml
- name: git clone
  description: Clone a repository into a new directory

- name: git pull
  description: Fetch from and integrate with another repository or a local branch

- name: git checkout
  description: Switch branches or restore working tree files

- name: git switch
  description: Switch branches
``` 

##### Install Git

1. RHEL/CentOS/Fedora
```bash
$ sudo dnf install git
```

##### Configure Git
There are two ways to configure your git identity locally or globally. 

When configure your git identity locally do
```bash
$ git config --local user.name "username"
$ git config --local user.email "username@domain.com"
```

When configure your git identity globally do
```bash
$ git config --global user.name "username"
$ git config --global user.email "username@domain.com"
```

##### Clone lab repository
```bash
# Clone via https
$ git clone https://github.com/desync-it/hillsborough-ansible-labs.git
```

```bash
# Clone via ssh
$ git clone git@github.com:desync-it/hillsborough-ansible-labs.git
```
