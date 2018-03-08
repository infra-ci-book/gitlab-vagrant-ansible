[![Build Status](https://travis-ci.org/infra-ci-book/gitlab-vagrant-ansible.svg?branch=master)](https://travis-ci.org/infra-ci-book/gitlab-vagrant-ansible)

# gitlab-vagrant-ansible
This repository contains [Ansible](https://www.ansible.com/) roles and
playbooks to install [GitLab](https://about.gitlab.com/) and
[GitLab Runner](https://docs.gitlab.com/runner/).

## Requirements

Install base dependencies:

Requirements:

- Ansible >= 2.4.0.0
- CentOS >= 7.4
- Vagrant >= 2.0.1
- VirtualBox >= 5.2

----

CentOS:

```
yum -y update
yum -y install ansible
reboot
```

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

In order for GitLab to display correct repository clone links
to your users it needs to know the URL under which it is reached by your users.

```
gitlab_external_url: "http://localhost"
```

```
gitlab_runner_coordinator_url: 'https://localhost/ci'
```

## Dependencies

- [bootstrap-host](https://github.com/infra-ci-book/bootstrap-host)

## Installation

This assumes that you've installed the base dependencies and you're running on
CentOS.

### Booting Vagrant VMs
At first, booting Vagrant VMs for GitLab and GitLab Runner is required.

```
cd ~/vagrant/infraci
vagrant up gitlab
vagrant up gitlab-runner
```

### Install GitLab and Runner
Running `site.yml` to install GitLab to gitlab machine.

```
cd ~/
git clone https://github.com/infra-ci-book/gitlab-vagrant-ansible.git
cd gitlab-vagrant-ansible
ansible-playbook site.yml
```

### Login to GitLab 

Defalut user/password is `root/password`.


## License

Apache-2.0


