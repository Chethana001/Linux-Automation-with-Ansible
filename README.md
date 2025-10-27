# Linux-Automation-with-Ansible
Ansible is a free tool that automates tasks like setting up software or managing servers. It uses simple instructions in "playbooks" to control multiple computers without needing extra software. This repo is for learning and sharing Ansible playbooks to make IT tasks easier and faster.
## What is Ansible?
Ansible is a free, easy to use tool that helps you manage and automate tasks on computers, servers, or cloud systems. It simplifies things like installing software, setting up servers, or deploying apps by letting you write simple instructions in files called "playbooks." These playbooks use plain, human-readable language (YAML) to tell Ansible what to do.\
Think of Ansible as a smart assistant that can talk to many computers at once without needing extra software installed on them. It uses a secure connection (SSH) to get the job done, making it fast and lightweight.
## Why use ansible
* __Saves time__ : Automates repetitive tasks, like setting up multiple servers.
* __esay to learn__ : Uses simple instructions anyone can understand.
* __No extra software__ : Works directly with your systems.
* __Flexible__ : Handles Linux, Windows, or cloud platforms like AWS or Azure.
* __Reliable__ : Ensures tasks are done the same way every time, avoiding mistakes.
## Example Use Cases
* Setting up a web server on 10 machines with one command.
* Automatically installing updates across all your computers.
* Deploying an app to a cloud platform without manual work.
## Install Ansible
We are use 3 virtual matchines, one matchines is server or workstation and other 2 are named as ansi1 and ansi2 and we are using centos stream 9 operating system.\
First u need to install epel-release

<img width="582" height="26" alt="image" src="https://github.com/user-attachments/assets/05f0ec25-2750-410d-b0fd-539274e5f9cb" />

Sometimes if this error will be happen

<img width="874" height="89" alt="image" src="https://github.com/user-attachments/assets/2b4db54d-2c8d-46d2-8974-372c2556a371" />

This happens because the EPEL (Extra Packages for Enterprise Linux) repository package (epel-release) cannot be found by yum, the package manager.
To fix this, first check ur centos version use the specific command.

After fixing the EPEL installation, retry installing Ansible as described earlier

<img width="584" height="25" alt="image" src="https://github.com/user-attachments/assets/0a507c29-0557-427d-a604-c4d7d22944f8" />

If ansible dosen't install install ansible-core. After that u can check ur ansible version.

<img width="1270" height="240" alt="image" src="https://github.com/user-attachments/assets/5939b983-007c-48ff-826d-1b232f587e4f" />


<b><i>Now u should make server can ssh other nodes without passwords.</i></b> 
## Write a Playbook
* __Purpose__ : A playbook is like a recipe that tells Ansible what to do (e.g., install software, start services).
* __Why It’s Needed__ : Ansible uses human-readable YAML files to automate tasks, making it repeatable and easy to share.

### Creates a workspace

Edit /etc/ansible/ansible.cfg

<img width="975" height="377" alt="image" src="https://github.com/user-attachments/assets/1df0b6bd-4ba7-4d21-a14b-3141925ab1b5" />

Make directory called myplaybooks and make file call inventory and edit like this.

<img width="302" height="103" alt="image" src="https://github.com/user-attachments/assets/a5f9a329-c92b-4b0c-8cc7-7b17cdabcf79" />

Now test onnectivity to all hosts defined in an inventory file.If successful, you might see 

<img width="711" height="321" alt="image" src="https://github.com/user-attachments/assets/3c5c8070-dc82-43be-94a4-3f774bfb4c56" />

Sometimes this error will show you.

<img width="1714" height="321" alt="image" src="https://github.com/user-attachments/assets/f400173f-ace3-41e1-9be1-441e84700c90" />

We can fix this error edit inventory file like this

<img width="626" height="73" alt="image" src="https://github.com/user-attachments/assets/868d2994-e83c-484f-b206-6c1b94cd4b84" />

Now u should make this.

<img width="440" height="116" alt="image" src="https://github.com/user-attachments/assets/241a0d3c-ff3c-40ac-825f-2eeea140997b" />

This is particularly useful when working with Ansible or other tasks involving text editing.

## Deploy Apache Web Server
Lets make Ansible playbook for automating the deployment and management of an Apache web server.

<img width="365" height="326" alt="image" src="https://github.com/user-attachments/assets/390bdc8e-d207-4252-ad69-12214843bb47" />

This YAML file is an Ansible playbook that specifies tasks to automate the installation, configuration, and management of the Apache web server (httpd) on target hosts.\
YAML (Yet Another Markup Language), a human-readable data serialization standard. Ansible uses YAML for playbooks, and the file must start with --- to indicate it’s a YAML document.\


<b>What This Playbook Does</b>

* Installs Apache: Ensures the httpd package is present on all target hosts.
* Starts Apache: Activates the httpd service and keeps it running.
* Enables Apache: Configures the service to start automatically on boot.
* This automation is useful for setting up a web server environment consistently across multiple machines.

After that Execute it with the command

<img width="1703" height="415" alt="image" src="https://github.com/user-attachments/assets/183aa7e0-6792-49f0-9ca5-65db78450f12" />


Check if Apache is installed and running on the target hosts.

If the playbook fails , debug with <b><i>ansible-playbook -i inventory web.yml -vvv</i></b> for more details.

This playbook is a basic example to get you started with Ansible automation.

### Examples

* Update every package

<img width="414" height="285" alt="image" src="https://github.com/user-attachments/assets/8140c4fe-2130-41e0-be2c-f44fa5d83aec" />

* Create a group called developers and two users dev1 and dev2

<img width="736" height="361" alt="image" src="https://github.com/user-attachments/assets/1acdf704-a84e-4d9e-ad6b-5f53c5bd03b9" />

## Ansible Vault
Ansible Vault is a feature in Ansible that helps you keep sensitive information—like passwords, API keys, or other secrets—safe and secure.

### Create a Vault File

Create file and edite like this,

<img width="240" height="58" alt="image" src="https://github.com/user-attachments/assets/00088131-fc5a-49cd-bf98-c0877a70ac90" />


After that encrypt this file.

<b><i>ansible-vault encrypt secret.yml</i></b>

Include the vault file in your playbook using vars_files

<img width="730" height="420" alt="image" src="https://github.com/user-attachments/assets/8b204852-a8c6-4e68-a711-4476f8a5d8f3" />

Run the playbook with the vault password: <b><i>ansible-playbook -i inventory playbook.yml --ask-vault-pass</i></b>

<img width="1705" height="388" alt="image" src="https://github.com/user-attachments/assets/5bf20857-8d81-4c74-870d-411a4b36732f" />


Since you’ve been working with Ansible (e.g., the ansible all -m ping and the Apache playbook), you might need to automate tasks that require secrets (like SSH passwords or API keys). Ansible Vault ensures these stay secure while letting you automate safely.



















