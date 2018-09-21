# openshift_ansible_centos

In this setup we are using 1 Master and 1 Node configuration

## Setting up Centos Servers
Create volume according to Openshift Origin document https://docs.okd.io/latest/install/prerequisites.html

### Yum Repo
 1. Copy all the files in /etc/yum.repos.d from centos docker container to same location on the servers
 2. Create no password ssh login for root

### DNS Names
 1. Add all the dns names to the host file in /etc/hosts for all the servers
 2. Update hostname using hostnamectl command
 3. Restart the servers

### Installing nessary Packages
 `yum install epel-release ansible git NetworkManager -y`
 `easy_install pip`
 `pip install --upgrade ansible`

### Clone Openshift repo
 ```
    git clone https://github.com/openshift/openshift-ansible
    cd openshift-ansible
    git checkout release-3.10
 ```
### Deploying the cluster
 Create host file for ansible to use and run the following commands
 ```
    ansible-playbook -i hosts openshift-ansible/playbooks/prerequisites.yml --private-key=~/.ssh/devops_dsa -v
    ansible-playbook -i hosts openshift-ansible/playbooks/deploy_cluster.yml --private-key=~/.ssh/devops_dsa -v
 ```

