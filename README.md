# My Ansible Scripts
Tools for managing and automating my personal applications:

* Configuration of Servers/VPS
* Deployment of Applications

These tools primarily use [Ansible](http://www.ansibleworks.com), which
handles configuration-management, application deployment, cloud provisioning,
ad-hoc task-execution, and multinode orchestration - including trivializing things
like zero downtime rolling updates with load balancers.

Read the documentation and more at http://ansible.com/

Applications currently supported are:

* Skitty (NodeJS)

This repository is organised in to:

```
├── apps # App-specific tasks
│   ├── skitty
│   │   ├── group_vars # App-specific variables
│   │   │   └── all
│   │   ├── instance_vars # Environment-specific variables
│   │   │   └── prod.yml
│   │   ├── node_vars # Nodejs-specific variables
│   │   │   └── main.yml
│   │   ├── plugdj_vars # Plug.dj-specific variables
│   │   │   └── main.yml
│   │   └── roles # App-specific roles
│   │       ├── skitty_app
│   │       ├── skitty_appserver
│   │       └── deploy
├── hosts # Environment hosts
│   ├── prod
│   └── vagrant
```

Each app has a set of Ansible playbooks which are typically named:

* deploy.yml - For deploying the application
* configure.yml - For running configuration management on the hosts

# Getting Set Up
1. [Install Ansible](http://docs.ansible.com/intro_installation.html)
2. Clone Repo

```git clone git@github.com:hect1c/ansible_scripts.git```

# Running a playbook
Ansible groups operations in to 'playbooks' - essentially a group of tasks
performed sequentially which will do some specific operation.

Typically, apps in my ansible_scripts have the following playbooks:

* configure - configuration management for the server, ensures all dependencies
  are installed, etc.
* deploy - deployment of the application

To run a playbook, use a command like:

```ansible-playbook app/dotcom/configure.yml -i hosts/env```
```ansible-playbook app/dotcom/deploy.yml -i hosts/env```

where the first parameter is the path to the playbook, and the second (-i)
is the path the hosts inventory (this will specify what environments you're
running the playbook on).

Make sure to first review the *_vars folders of the apps and that they have the
desired appropriate values