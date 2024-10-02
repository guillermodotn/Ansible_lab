# Ansible Lab

This project sets up a lab environment with **three endpoints** (servers) and a **workstation** using **Vagrant**. The lab is designed for **Ansible testing and practice**, providing a controlled environment to work with Ansible playbooks, modules, and automation tasks.

## Table of Contents

- [Overview](#overview)
- [Lab Setup](#lab-setup)
- [System Details](#system-details)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Credentials](#credentials)
- [Troubleshooting](#troubleshooting)

## Overview

This lab environment contains:

- **Workstation**: A VM where you will run Ansible commands.
- **3 Endpoints (servers)**: Three VMs acting as target servers for Ansible automation.

The environment uses **Vagrant** to automate the creation of these VMs, which are then connected for testing Ansible roles, playbooks, and configurations.

## Lab Setup

1. **Workstation**: The workstation serves as the control node for Ansible.
2. **Endpoints**: The three servers serve as target machines for Ansible commands.

You will log into the **workstation** to execute Ansible commands against the three **servers**.

## System Details

- **Workstation VM**:
  - Username: `student`
  - Password: `student`

- **Endpoints 1, 2 & 3 (servers)**:
  - Username: `ansible`
  - Password: `ansible`

## Prerequisites

Before setting up the lab, ensure you have the following installed:

- **Vagrant**: [Install Vagrant](https://www.vagrantup.com/docs/installation)
- **VirtualBox**: [Install VirtualBox](https://www.virtualbox.org/wiki/Downloads) (or any other Vagrant provider)
- **Ansible**: [Install Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) (optional, if not using the preconfigured Vagrant environment)

## Installation

1. **Clone the Repository**:

   ```bash
   git clone <repository-url>
   cd ansible_lab
   ```

2. **Start the Environment**:

    Run the following command to bring up the Vagrant environment:

    ```bash
    vagrant up
    ```
    This will automatically create and configure the three endpoint VMs and the workstation VM.

3. **SSH into the Workstation**:

    Once the VMs are up, SSH into the workstation to start testing:

    ```bash
    vagrant ssh workstation
    ```


## Usage
* Running Ansible Playbooks: From the workstation, you can execute Ansible commands and playbooks against the three endpoints.

    Example: Run the Ansible `ping` module to check connectivity:

    ```bash
    ansible all -m ping
    ```

* Inventory File: The inventory for Ansible should be configured to include the three endpoints. This will be located on the workstation.

    Example inventory (/etc/ansible/hosts):

    ```ini
    [servers]
    endpoint1 ansible_host=192.168.50.4 ansible_user=ansible
    endpoint2 ansible_host=192.168.50.5 ansible_user=ansible
    endpoint3 ansible_host=192.168.50.6 ansible_user=ansible
    ```

## Credentials
* Workstation:
    * Username: `student`
    * Password: `student`

* Endpoints (servers):
    * Username: `ansible`
    * Password: `ansible`


## Troubleshooting
If Vagrant fails to start the environment, try running:

```bash
vagrant destroy -f && vagrant up
```

To stop and remove the environment:

```bash
vagrant halt
vagrant destroy
```

Enjoy practicing Ansible with this controlled lab setup!

