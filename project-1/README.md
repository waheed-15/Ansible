# Ansible Playbook Demo

## From your control node, run the following command to include the official project’s PPA (personal package archive) in your system’s list of sources:

*1. Run the below command*<br>

     sudo -E apt-add-repository ppa:ansible/ansible

*2. Insytall Ansible*<br>

    sudo apt update -y
    sudo apt install Ansible -y

<hr>

*3. Now create two instances in you aws account which we will be using as worker nodes.*<br>

![Alt text](./images/instance-creation.png)

<hr>

*4. Inventory file Setup*<br>

*The inventory file contains information about the hosts you’ll manage with Ansible*
*Create a file by name inventory.ini and store the public ip of all the worker nodes there.*

    sudo nano inventory.ini

![Alt text](./images/inventoryini.png)<br>

<hr>

*5. Create user and add password to the created user using the below commands.*<br>

    useradd <user-name>
    passwd <user-name>

![Alt text](./images/useradd.png)

<hr>

*6. switch to the created user and generate .ssh keys using the below commands.*<br>

    su <user-name>
    ssh-keygen -t rsa

![Alt text](./images/ssh-main.png)

<hr>

*7. Now login to each worker node and perform the same operation - ssh-keygen -t rsa.*<br>

<hr>

*8. Now copy the public key from the ansible server using the below command and paste that in .ssh/authorized_keys path of worker nodes.*<br>

    cat .ssh/id_rsa.pub

![Alt text](./images/idrsapub.png)

    vi .ssh/authorized_keys

![Alt text](./images/authorisedleys.png)

<hr>

*9. Now try to ping the worker nodes from ansible server using the below command.*<br>

    ansible myhosts -m ping -i inventory.ini

![Alt text](./images/ping.png)

<hr>

*10. Now lets try to copy a sample file to the worker nodes using ansible.*<br>

    ansible-playbook copy-file.yaml -i inventory.ini

*No files in server1:*<br>

![Alt text](./images/server1root.png)

*similarly in server2:*<br>

![Alt text](./images/server2root.png)

*files copied successfully:*

![Alt text](./images/copy-files.png)

![Alt text](./images/filesinserver.png)

<hr>

