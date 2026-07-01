# Ansible Lab

This project sets up a lab environment with **four endpoints** (servers) and a **workstation** using **Vagrant**. The lab is designed for **Ansible testing and practice**, providing a controlled environment to work with Ansible playbooks, modules, and automation tasks.

## Table of Contents

- [Overview](#overview)
- [Lab Setup](#lab-setup)
- [System Details](#system-details)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Providers](#providers)
- [Troubleshooting](#troubleshooting)

## Overview

This lab environment contains:

- **Workstation**: A Fedora VM where you will run Ansible commands.
- **4 Endpoints (servers)**: Target servers for Ansible automation (mixed OS).

The environment uses **Vagrant** to automate the creation of these VMs, which are then connected for testing Ansible roles, playbooks, and configurations.

## Lab Setup

| VM | IP | OS | Role |
|----|----|----|------|
| workstation | 192.168.33.50 | Fedora 44 | Ansible control node |
| server1 | 192.168.33.51 | CentOS Stream 10 | Managed node |
| server2 | 192.168.33.52 | CentOS Stream 10 | Managed node |
| server3 | 192.168.33.53 | CentOS Stream 10 | Managed node |
| server4 | 192.168.33.54 | Ubuntu 26.04 LTS | Managed node |

## System Details

- **Workstation VM**:
  - Username: `user`
  - Password: `user`

- **Endpoints 1-4 (servers)**:
  - Username: `ansible`
  - Password: `ansible`

## Prerequisites

Before setting up the lab, ensure you have the following installed:

- **Vagrant**: [Install Vagrant](https://www.vagrantup.com/docs/installation)
- **A virtualization provider** (one of):
  - [libvirt/KVM](https://libvirt.org/) + `vagrant plugin install vagrant-libvirt`
  - [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
  - [VMware Desktop](https://www.vmware.com/) + `vagrant plugin install vagrant-vmware-desktop`

## Installation

1. **Clone the Repository**:

   ```bash
   git clone <repository-url>
   cd Ansible_lab
   ```

2. **Start the Environment**:

    ```bash
    # Uses your default provider (set via VAGRANT_DEFAULT_PROVIDER)
    vagrant up

    # Or specify a provider explicitly
    vagrant up --provider=libvirt
    vagrant up --provider=virtualbox
    vagrant up --provider=vmware_desktop
    ```

    This will automatically create and configure the four endpoint VMs and the workstation VM.

3. **SSH into the Workstation**:

    ```bash
    vagrant ssh workstation
    ```

## Usage

* Switch to the lab user on the workstation:

    ```bash
    su - user
    ```

* Running Ansible Playbooks: From the workstation, you can execute Ansible commands and playbooks against the four endpoints.

    Example: Run the Ansible `ping` module to check connectivity:

    ```bash
    ansible all -m ping
    ```

* SSH shortcuts are preconfigured. You can reach servers with:

    ```bash
    ssh s1   # connects to server1 (CentOS) as ansible user
    ssh s2   # connects to server2 (CentOS) as ansible user
    ssh s3   # connects to server3 (CentOS) as ansible user
    ssh s4   # connects to server4 (Ubuntu) as ansible user
    ```

* Inventory File: The inventory for Ansible should be configured to include the four endpoints.

    Example inventory:

    ```ini
    [servers]
    server1 ansible_host=192.168.33.51 ansible_user=ansible
    server2 ansible_host=192.168.33.52 ansible_user=ansible
    server3 ansible_host=192.168.33.53 ansible_user=ansible
    server4 ansible_host=192.168.33.54 ansible_user=ansible
    ```

## Providers

The Vagrantfile supports multiple virtualization providers. Set your default globally:

```bash
export VAGRANT_DEFAULT_PROVIDER=libvirt    # for KVM/QEMU
export VAGRANT_DEFAULT_PROVIDER=virtualbox # for VirtualBox
export VAGRANT_DEFAULT_PROVIDER=vmware_desktop # for VMware
```

| Provider | Plugin Required | Notes |
|----------|----------------|-------|
| libvirt (KVM) | `vagrant-libvirt` | Recommended on Linux |
| VirtualBox | None (built-in) | Cross-platform |
| VMware Desktop | `vagrant-vmware-desktop` | Requires license |

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

If synced folders fail with libvirt, ensure `rsync` is installed on your host.

Enjoy practicing Ansible with this controlled lab setup!
