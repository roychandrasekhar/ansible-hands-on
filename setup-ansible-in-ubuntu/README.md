# Setup Ansible cluster environment in Virtual Box using Ubuntu

1. Setup 3 Ubuntu machine
2. Install Ansible in Master machine
    ```
   sudo apt-get update
   sudo apt install software-properties-common
   sudo apt-add-repository ppa:ansible/ansible
   sudo apt update
   sudo apt install ansible
    ```
    ![](https://i.imgur.com/8E0Zit6.png)

3. Install Python on all Client machine
   ```
   sudo apt-get update
   sudo apt-get install python
   ```
    ![](https://i.imgur.com/rmOLlkr.png)

4. Setting up Ansible Host in Master machine
    Add host entry in bottom of the file “/etc/ansible/hosts”

    ```
    [production]
    slaveP1 ansible-ssh-host=192.168.56.102

    [staging]
    slaveS1 ansible-ssh-host=192.168.56.106
    ```
    ![](https://i.imgur.com/icgBSe8.png)

5. Setup passwordless SSH connection from Master machine to all client machines from a fixed user from where you like to operate the worker machine. 

    Use  `ssh-copy-id username@clientmachine-ip`

6. Test Master client connection
    ```
    ansible -m ping all
    ansible -m ping production
    ansible -m ping slave1
    ```
    ![](https://i.imgur.com/SxZeAby.png)</br>
    ![](https://i.imgur.com/FhC8K1H.png)

