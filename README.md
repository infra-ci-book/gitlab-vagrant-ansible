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
cd ~/vagrant/infra-ci
vagrant up gitlab
vagrant up gitlab-runner
    ```
### Install GitLab
Running `gitlab.yml` to install GitLab to gitlab machine.

```
git clone https://github.com/infra-ci-book/gitlab-vagrant-ansible.git
cd gitlab-vagrant-ansible
ansible-playbook -i hosts/gitlab gitlab.yml
```

### Install GitLab Runner
1. Access to `http://192.168.33.10` and configure password to login.

1. Grab the shared-Runner token on the `admin/runners` page

1. Edit 'hosts/gitlab-runner/inventory' and configure shared-Runner token in `[gitlab-runner:vars]` section.

    ```
    [gitlab-runner:vars]
    # ...
    gitlab_runner_registration_token='xxxxxxxxxxxxx'
    ```

1. Running `gitlab-runner.yml` to install GitLab Runner to gitlab-runner machine.

    ```
    ansible-playbook -i hosts/gitlab-runner gitlab-runner.yml
    ```

## License

Apache-2.0


