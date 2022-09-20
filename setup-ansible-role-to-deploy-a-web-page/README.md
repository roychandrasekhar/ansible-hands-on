# Setup Ansible role to deploy a web page in Apache

1. Create ansible role
    SSH into Master machine
    ```
    cd /etc/ansible/roles/
    ansible-galaxy init apache --offline
    tree apache
    ```
    ![](https://i.imgur.com/1i3algo.png)

2. Install Apache in install.yml playbook in path
    ```
    vi /etc/ansible/roles/apache/tasks/install.yml
    ---
      - name: install apache2
        apt:
            name: apache2
            state: present
    ```
    ![](https://i.imgur.com/b5Tdw4u.png)

3. Create an html file in path
    ```
    cd /etc/ansible/roles/apache/files/
    echo "Welcome chandra, Ansible" > index.html
    ```
    ![](https://i.imgur.com/ZoD3RuQ.png)

4. Copy html file into worker machine specific directory by configure.yaml playbook
    ```
    vi /etc/ansible/roles/apache/tasks/configure.yml
    ---
      - name: Configure Website
        copy: src=index.html dest=/var/www/html
    ```
    ![](https://i.imgur.com/kKWpQ77.png)

5. Enable service in worker machine
    ```
    vi /etc/ansible/roles/apache/tasks/service.yml
    ---
      - name: starting apache2 service
        service:
            enabled: true
            name: apache2
            state: started
    ```
    ![](https://i.imgur.com/gKaizzk.png)

6. Finally add them all in main.yml file
    ```
    vi /etc/ansible/roles/apache/tasks/main.yml
    ---
    # tasks file for apache
    - include: install.yml
    - include: configure.yml
    - include: service.yml
    ```
    ![](https://i.imgur.com/grXcMuN.png)

7. Add role in site.yml file
    ```
    vi /etc/ansible/site.yml
    ---
      - hosts: slaveS1
        roles:
        - apache
    ```
    ![](https://i.imgur.com/sjlHhQO.png)

8. Run the playbook
    ```
    /etc/ansible$ ansible-playbook site.yml
    ```
    ![](https://i.imgur.com/mKdP5m6.png)

9. Curl your slaveS1 or IP of the worker machine
    ```
    curl http://192.168.56.106	
    ```
    ![](https://i.imgur.com/7f0llSv.png)

