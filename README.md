# cloud-init-proxmox

## Setup

```bash
wget https://cloud-images.ubuntu.com/jammy/current/jammy-server-cloudimg-amd64.img
```

```bash
qm create 8001 --memory 4096 --core 2 --name ubuntu-cloud-22.04.1 --net0 virtio,bridge=vmbr0
```

```bash
qm importdisk 8001 jammy-server-cloudimg-amd64.img localprox1
```

```bash
qm set 8001 --scsihw virtio-scsi-pci --scsi0 localprox1:vm-8001-disk-0
```

```bash
qm set 8001 --ide2 localprox1:cloudinit
```

```bash
qm set 8001 --boot c --bootdisk scsi0
```

```bash
qm set 8001 --serial0 socket --vga serial0
```

## First VM

```bash
sudo apt-get install qemu-guest-agent
sudo systemctl start qemu-guest-agent
```

```bash
sudo apt update && sudo apt upgrade
```

## References

- [Techno Tim - Perfect Proxmox Template with Cloud Image and Cloud Init](https://docs.technotim.live/posts/cloud-init-cloud-image/) [(video)](https://www.youtube.com/watch?v=shiIi38cJe4)
- [Proxmox - QEM Guest Agent](https://pve.proxmox.com/wiki/Qemu-guest-agent)