# Create an Ubuntu 22.04 (with Docker) Template on Proxmox with Packer

## Prerequisites

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
   
Create a `credentials.pkr.hcl` file located inside `~/infra/packer/proxmox` defining the following:

   ```
   proxmox_api_url = "https://proxmox-url:8006/api2/json"

   proxmox_api_token_id = "proxmox-user@pam!packer"

   proxmox_api_token_secret = "proxmox-api"
   ```

## Usage
   Change to the correct directory.
   ```
   cd ~/infra/packer/proxmox/ubuntu-server-jammy
   ```
   Run the following to build the template.
   ```
   packer build -var-file='./credentials.pkr.hcl' ./ubuntu-server-jammy.pkr.hcl
   ```
