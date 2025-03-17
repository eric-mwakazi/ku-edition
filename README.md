# ku-edition
# Ansible Playbook: KU Edition

This project automates the setup of an EC2 instance with UFW, NGINX, and a custom welcome page using Ansible.

## Prerequisites

1. **Basic Knowledge**: Familiarity with Ansible commands and EC2 instance setup.
2. **EC2 Instance**: Ensure you have:
   - Created an EC2 instance (Ubuntu).
   - Generated an SSH key pair and set the private key permissions:
     ```sh
     chmod 400 path/to/your-key.pem
     ```
   - Obtained the public IP of the EC2 instance.
3. **Install Ansible** (if not already installed):
   ```sh
   sudo apt update && sudo apt install ansible -y
   ```

## Project Structure

```plaintext
.
├── inventory
│   └── kube_inventory
├── ku-edition.pem
├── playbook
│   ├── configure_vm.yml
│   └── welcome_page.j2
└── README.md
```

## Configuration

1. **Inventory Setup**:
   Edit `inventory/kube_inventory` and replace the placeholders with your EC2 details:
   ```ini
   [ku-ec2-node1]
   ku-web-server ansible_host=<your-ec2-public-ip> ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/your-key.pem
   ```

2. **Verify Ansible Installation**:
   ```sh
   ansible --version
   ```
   Ensure Ansible Core is installed (2.14 or higher).

3. **Test Connection**:
   Test the connection to the EC2 instance:
   ```sh
   ansible -i inventory/kube_inventory all -m ping
   ```

## Running the Playbook

Execute the following command to run the playbook:
```sh
ansible-playbook -i inventory/kube_inventory playbook/configure_vm.yml
```

This will:
- Update and upgrade packages.
- Install `python3-six`.
- Configure DNS.
- Set the hostname.
- Install and start UFW, allowing SSH, HTTP, and HTTPS.
- Install and start NGINX.
- Deploy the custom welcome page.
- Reboot the instance gracefully.

## Verification
After the playbook runs successfully, you can verify:
- NGINX is running by visiting the EC2 public IP in your browser.
- The custom welcome page is displayed.

Example:
```sh
http://<your-ec2-public-ip>
```

## Troubleshooting
- Ensure the private key has correct permissions (`chmod 400`).
- Verify Ansible can reach the instance with `ansible -i inventory/kube_inventory all -m ping`.

## Conclusion
This playbook automates setting up an EC2 instance with NGINX and UFW. Modify the `welcome_page.j2` template as needed for custom content.

## 📚 Resources

### 🎬 Video Tutorials

1. **Ansible Basics and Setup (YouTube Playlist)**  
   [![Ansible Basics and Setup](https://img.youtube.com/vi/2hVSpENzhwA/sddefault.jpg)](https://www.youtube.com/watch?v=2hVSpENzhwA&list=PL7iMyoQPMtAPZl58ovoOlxFxNPioSx838)  

2. **Deploying NGINX with Ansible (YouTube Playlist)**  
   [![Deploying NGINX with Ansible](https://img.youtube.com/vi/3RiVKs8GHYQ/sddefault.jpg)](https://www.youtube.com/watch?v=3RiVKs8GHYQ&list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70)  

### 📘 DevOps Books Repository  

- Check out my GitHub repository for DevOps resources and books:  
  [DevOps_Books Repository](https://github.com/eric-mwakazi/DevOps_Books) 🚀 


Happy automating! 🚀
