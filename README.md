# Proxmox Windows Server VM Automation

This project automates the creation of a Windows Server virtual machine in Proxmox VE using best-practice configurations.

## Why I built this

While working in my home lab and data center environment, I noticed that creating Windows Server VMs in Proxmox requires repeating the same manual steps.

This script standardizes the process and reduces setup time.

## What this script does

* Creates a VM using Q35 (modern hardware)
* Enables UEFI (OVMF)
* Adds TPM 2.0 support
* Attaches Windows ISO
* Attaches VirtIO drivers
* Uses VirtIO disk and network for performance
* Enables QEMU Guest Agent

## Requirements

* Proxmox VE host access
* Windows Server ISO uploaded
* VirtIO ISO uploaded
* Storage configured (example: local-lvm)
* Network bridge (example: vmbr0)

## Example usage

```bash
./scripts/create-windows-server-vm.sh \
  --vmid 200 \
  --name winserver2025 \
  --memory 8192 \
  --cores 4 \
  --sockets 1 \
  --disk 120 \
  --bridge vmbr0 \
  --storage local-lvm \
  --iso-store local \
  --win-iso "Windows_Server_2025.iso" \
  --virtio-iso "virtio-win.iso"
```

## After creating the VM

Start it:

```bash
qm start 200
```

Open the console and install Windows.

If the disk is not visible:

* Load driver from VirtIO ISO
* Select storage driver
* Continue installation

## Use cases

* Home lab environments
* Active Directory testing
* Automation practice
* Infrastructure standardization

## Author

Built as part of my infrastructure and automation learning journey.
