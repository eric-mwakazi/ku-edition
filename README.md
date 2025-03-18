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
   ### 📝 Note
   If you are following this on windows chmod command might not work on powershell or cmd.
   #### ⚙️ Solution:
   If you have vscode or git bash, right click and open the folder where your aws ssh key that was downloaded while creating the ec2 instances is with vscode or gitbash and use the terminals they provide to execute chmod command.
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

### 📝 Note
Remember to open port 22,80 and 443 while creating ec2 instance <br>
<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/firewall.png'>

## Clone project from github
```
git clone https://github.com/eric-mwakazi/ku-edition.git
```
## Open project in vscode
For easy in editing. I recommend using a text editor like vscode for that.<br>
On same terminal you cloned the project run `code ku-edition` or right click the folder ku-edition the select open with vscode.
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

   The `inventory/kube_inventory` file is an Ansible inventory file. An inventory file lists the servers Ansible will manage and how to connect to them. In this case, it's used to define EC2 instances to be configured.

   - `[ku-ec2-node1]`: Group name to organize servers.
   - `ku-web-server`: Alias for your EC2 instance
   - `ansible_host`: Public IP of the EC2 instance
   - `ansible_user`: User to log in as (e.g., ubuntu for Ubuntu EC2).
   - `ansible_ssh_private_key_file`: Path to your SSH private key for authentication.

   Edit `inventory/kube_inventory` and replace the placeholders with your EC2 details. If you have more than one node/vm feel free to add there details using the format used below:
   ```ini
   [ku-ec2-node1]
   ku-web-server ansible_host=<your-ec2-public-ip> ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/your-key.pem
   ```

2. **Verify Ansible Installation**:
   ```sh
   ansible --version
   ```
   Ensure `Ansible Core` is installed (2.14 or higher).

3. **Test Connection**:
   Test the connection to the EC2 instance:
   ```sh
   ansible -i inventory/kube_inventory all -m ping
   ```
Should return `SUCCESS` on all nodes inside the inventory file, else check if ip and ssh key file are correct and have correct permissions.<br>
<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/ping.png'>
## The Playbooks

### 📝 What is a Playbook?
An `Ansible Playbook` is a file that contains a list of instructions (called "plays") for automating tasks on remote machines. It’s like a recipe for Ansible, where you describe what you want to do, and Ansible takes care of the how.
<br><br>
* Playbooks are written in YAML format (we’ll cover YAML next!).
Each play targets a group of hosts and defines tasks to run on them — like installing software, configuring services, or setting up Kubernetes nodes.

### Example Playbook:
<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/play.png'> <br>
<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/play2.png'>

This will:

✔️ Update and upgrade packages

✔️ Install python3-six for Ansible compatibility

✔️ Configure DNS settings

✔️ Sets the hostname

✔️ Install and configure UFW firewall

✔️ Install and start Nginx

✔️ Deploy a welcome page

✔️ Reboot the instance

### Run the playbook
Execute the following command to run the playbook inside the root folder of the project:
```sh
ansible-playbook -i inventory/kube_inventory playbook/configure_vm.yml
```

## Expected results
<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/output.png'> <br>
<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/output1.png'><br>
<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/output2.png'>

## Verification
After the playbook runs successfully, you can verify:
- NGINX is running by visiting the EC2 public IP in your browser.
- The custom welcome page is displayed.

Example:
```sh
http://<your-ec2-public-ip>
```
## Expected results
<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/ku-final.png'> <br>
<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/msu-final.png'><br>
<img src='https://github.com/eric-mwakazi/ku-edition/blob/main/assets/uon-final.png'>

## Troubleshooting
- Ensure the private key has correct permissions (`chmod 400`).
- Verify Ansible can reach the instance with `ansible -i inventory/kube_inventory all -m ping`.

## 📣 Wrapping Up
With just a few commands, you’ve automated infrastructure setup, installed NGINX, configured firewall rules, and deployed a custom welcome page. Infrastructure automation saves time, reduces errors, and brings consistency to deployments.

## Stop the Servers and VMs:
Once you're done testing, remember to stop any unused EC2 instances or VMs to avoid unnecessary costs. In AWS, you can stop the instance directly from the EC2 dashboard.

## 📚 Resources
If you’d like to dive deeper into Ansible and automation, check out these resources:

### 🎬 Video Tutorials

1. **Ansible Basics and Setup (YouTube Playlist)**  
   [![Ansible Basics and Setup](https://img.youtube.com/vi/2hVSpENzhwA/sddefault.jpg)](https://www.youtube.com/watch?v=2hVSpENzhwA&list=PL7iMyoQPMtAPZl58ovoOlxFxNPioSx838)  

2. **Deploying NGINX with Ansible (YouTube Playlist)**  
   [![Deploying NGINX with Ansible](https://img.youtube.com/vi/3RiVKs8GHYQ/sddefault.jpg)](https://www.youtube.com/watch?v=3RiVKs8GHYQ&list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70)  

### 📘 DevOps Books Repository  

- Check out my GitHub repository for DevOps resources and books:  
  [DevOps_Books Repository](https://github.com/eric-mwakazi/DevOps_Books) 🚀 

## Conclusion
- Did it work? <br>
- Did not it work? <br>
- How was your experience using ansible for automation.<br>
- Have any idea of improvements? <br>

Kindly share your experience on social media tagging me on linkedin [@Eric mwakazi](https://www.linkedin.com/in/eric-mwakazi). and [@Nairobi DevOps Community](https://www.linkedin.com/groups/9351099/)

Huge thanks to the [@Nairobi DevOps Community](https://www.linkedin.com/groups/9351099/) and Kenyatta University for organizing such a fantastic event.<br>
It was an honor to share insights and learn from others passionate about DevOps and automation 🙌. <br><br>
#DevOps #Automation #Ansible #InfrastructureAsCode #NairobiDevOps #KenyattaUniversity<br>