## Prerequisites for creating an Ubuntu 22.04 LTS (with Docker) Template on Proxmox using Packer

1. Install Packer on your machine.

Add the HashiCorp GPG key.
```
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
```

Add the official HashiCorp Linux repository.
```
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
```

Update and install:
```
sudo apt-get update && sudo apt-get install packer
```

2. A Proxmox host with SSH access.
   
3. Create a `credentials.pkr.hcl` file located inside `~/infra/packer/proxmox` defining the following:

```
proxmox_api_url = "https://proxmox-url:8006/api2/json"

proxmox_api_token_id = "proxmox-user@pam!packer"

proxmox_api_token_secret = "proxmox-api"
```

## Usage

```
cd ~/infra/packer/proxmox/ubuntu-server-jammy

packer build -var-file='./credentials.pkr.hcl' ./ubuntu-server-jammy.pkr.hcl
```
