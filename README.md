## Running Ansible

Name: Examples from Codehub's Ansible Course

Author: Kostas Makedos

Email: kostas.makedos@gmail.com

### Introduction
This repository contains some examples from Ansible Course as it was first delivered in 2023-2024.
The idea was to have a simple way to test Ansible playbooks against different targets without having the need
to run several different VMs.
For this reason we are using Docker containers as targets.

In the repository there is a folder called TargetDockers which contains some Dockerfiles and
a Makefile.
Instructions on how to spin one or more containers are given below.

### Prerequisites
You need to checkout this repository in a Linux/Unix system that has Ansible available.
You will also need to have access to Docker containers from the same machine, meaning you have to be able to run Docker containers there.

### Installing Ansible
If you want to install Ansible in a Debian-based system you would execute: `sudo apt-get install ansible`, while
in Red-Hat based system: `yum install ansible` or `dnf install ansible`.

### Check if you have Docker running
A simple `docker ps` command should give you the following output:

`CONTAINER ID   IMAGE           COMMAND                  CREATED          STATUS          PORTS`

If this is not the output and you have an error message, then consider adding yourself to the docker group:

`sudo adduser xxxxx docker`

`sudo usermod -aG docker xxxxx`

### Start Target Dockers
Start in the Target Dockers folder:

`cd TargetDockers`

and then execute:
`make`

This command will start two containers, one called debian-01 and one called fedora-01.
At the end of the output you will find a small snippet to be put in your ~/.ssh/config file and it looks like this:
```
---CUT HERE---
Host debian-01
        HostName localhost
        Port 10122
Host fedora-01
        HostName localhost
        Port 20122
---CUT HERE---
```

Just copy the section between the `--CUT HERE--` lines and add it in your ~/.ssh/config file.

If you want to stop TargetDockers run a `make clean` command.

If you want to spin up more containers, execute the `make` command with a NUMBER argument.
E.g:
```
make NUMBER=02
```
This command will create two more containers, `debian-02` and `fedora-02Just copy the section between the `--CUT HERE--` lines and add it in your ~/.ssh/config file.

If you want to stop TargetDockers run a `make clean` command.

If you want to spin up more containers, execute the `make` command with a NUMBER argument.
E.g:
```
make NUMBER=02
```
This command will create two more containers, `debian-02` and `fedora-02`.

Similarly:
```
make NUMBER=03
```
This command will create two more containers, `debian-03` and `fedora-03`.

And if you want to delete a specific pair of containers:
```
make clean NUMBER=03
```

### Running the examples

Now its time to run the examples.
Each example has an inventory file inside its folder structure:

`chapter03/inventory/containers.ini`

Use this file as an inventory file if you want to run all the examples.

The file:

`chapterxx/inventory/local.ini`

Is referring to your local WSL machine.
So if you run against this file, you will change your WSL installation and not our ephemeral containers.

Example command:

```ansible-playbook -i inventory/containers.ini run.yml```

This command can run for almost all examples in this repository except maybe the last one.
