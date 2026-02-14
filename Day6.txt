Ansible Installation in Ubuntu
Step 1: Update Package List
sudo apt update

Step 2: Install Ansible
sudo apt install ansible -y

Step 3: Verify Installation
ansible --version
If installed correctly, the Ansible version details will be displayed.

# Ansible Apache Deployment – Commands
1. Clone Repository
git clone https://github.com/jagadeeshkanna97/ansible-k.git
cd ansible-k

2. Set Key Permission
chmod 400 ubuntudevops.pem

3. Test SSH Connection
ssh -i ubuntudevops.pem ubuntu@54.82.36.187

4. Test Ansible Connectivity
ansible -i inventory.ini slaves -m ping


Expected Output:

SUCCESS => {
    "ping": "pong"
}

5. Run Ansible Playbook
ansible-playbook -i inventory.ini apache-playbook.yml

6. Verify Apache Service (Inside EC2)
sudo systemctl status apache2

7. Access Website

Open in browser:

http://54.82.36.187
