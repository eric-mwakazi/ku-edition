# 🚀 Automating Infrastructure with Ansible: My Experience at Nairobi DevOps 2025 🐳🚀 🚀 🌐☸️

<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/ansbleandngix.png'>

This project automates the setup of an EC2 instance with UFW, NGINX, and a custom welcome page using Ansible.

## Prerequisites

1. **Basic Knowledge**: Familiarity with Ansible commands and EC2 instance setup.
2. **EC2 Instance**: Ensure you have:
   - Created an EC2 instance (Ubuntu).
   - Generated an SSH key pair and set the private key permissions:
     ```sh
     chmod 400 path/to/your-key.pem
     ```
   - Obtained the public IP of the EC2 instance

3. **Install Ansible** (if not already installed): https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
4. **Install git** (if not already installed):

   https://git-scm.com/book/en/v2/Getting-Started-Installing-Git

## 🌐 AWS Setup Guides  

### 📽️ AWS Account Setup: Step by Step Guide for Beginners  
If you don't have a credit card, you can use the **M-Pesa App** to create a virtual card for account setup.  

[![Watch the video](https://img.youtube.com/vi/xi-JDeceLeI/0.jpg)](https://youtu.be/xi-JDeceLeI?si=itg_lSkWzhYDJ26C)  

---

### 📽️ Creating EC2 on AWS Console  

[![Watch the video](https://img.youtube.com/vi/86Tuwtn3zp0/0.jpg)](https://youtu.be/86Tuwtn3zp0)  

   
## Clone project from github
```
git clone https://github.com/eric-mwakazi/ku-edition.git
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

✔️ Update and upgrade packages

✔️ Install python3-six for Ansible compatibility

✔️ Configure DNS settings

✔️ Sets the hostname

✔️ Install and configure UFW firewall

✔️ Install and start Nginx

✔️ Deploy a welcome page

✔️ Reboot the instance

## Expected results
<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/play.png'> <br>
<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/play2.png'>

## Verification
After the playbook runs successfully, you can verify:
- NGINX is running by visiting the EC2 public IP in your browser.
- The custom welcome page is displayed.

Example:
```sh
http://<your-ec2-public-ip>
```
## Expected results
<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/ku-final.png'>
<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/msu-final.png'>
<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/uon-final.png'>

## Troubleshooting
- Ensure the private key has correct permissions (`chmod 400`).
- Verify Ansible can reach the instance with `ansible -i inventory/kube_inventory all -m ping`.

## Conclusion
This playbook automates setting up an EC2 instance with NGINX and UFW. Modify the `welcome_page.j2` template as needed for custom content.

## Stop the Servers and VMs:
Once you're done testing, remember to stop any unused EC2 instances or VMs to avoid unnecessary costs. In AWS, you can stop the instance directly from the EC2 dashboard.

## 📚 Resources

### 🎬 Video Tutorials

1. **Ansible Basics and Setup (YouTube Playlist)**  
   [![Ansible Basics and Setup](https://img.youtube.com/vi/2hVSpENzhwA/sddefault.jpg)](https://www.youtube.com/watch?v=2hVSpENzhwA&list=PL7iMyoQPMtAPZl58ovoOlxFxNPioSx838)  

2. **Deploying NGINX with Ansible (YouTube Playlist)**  
   [![Deploying NGINX with Ansible](https://img.youtube.com/vi/3RiVKs8GHYQ/sddefault.jpg)](https://www.youtube.com/watch?v=3RiVKs8GHYQ&list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70)  

### 📘 DevOps Books Repository  

- Check out my GitHub repository for DevOps resources and books:  
  [DevOps_Books Repository](https://github.com/eric-mwakazi/DevOps_Books) 🚀 

