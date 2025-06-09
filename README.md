## Ansible Multi-Node Configuration Using VirtualBox - Konnecta Task

---

## 1- Virtual Machines Configuration

| Role             | IP Address     |
|------------------|----------------|
| Control Machine  | 192.168.56.103 |
| Frontend Machine | 192.168.56.102 | 
| Docker Machine   | 192.168.56.104 |

> All machines are Ubuntu-based VMs set up via VirtualBox with NAT a& host-only networking.
>
> All machines have ansible sudo user created in them with no passwords configration
>  
---

## 2- SSH Configuration

From the **Control Machine** (`192.168.56.103`):

1. Generate SSH key:
```bash
ssh-keygen -t rsa -b 4096 -C "ansible@control-"
```
2. Copy the public key to the remote server
```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ansible@192.168.56.102
ssh-copy-id -i ~/.ssh/id_rsa.pub ansible@192.168.56.104
```
3. Verify you can SSH without a password
```bash
ssh ansible@192.168.56.102
ssh ansible@192.168.56.104
```

## 3- Running the Playbooks

Frontend Machine - NGINX Setup
```bash
ansible-playbook -i inventory.ini frontend.yml
```
![Frontend Excution](https://github.com/user-attachments/assets/b3d22582-de80-467e-addc-94d77ded50e0)

Docker Machine - Docker + Redis Setup
```bash
ansible-playbook -i inventory.ini docker.yml
```
![Docker Excution](https://github.com/user-attachments/assets/df790058-aac5-4803-a3bc-a278152a4057)


