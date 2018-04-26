# Documentation

+ [Quickstart](#Quickstart);
+ [Example host file](#Ex1);
+ [Playbook variables](#Table1);

## <a name="Quickstart"></a> Quickstart

[Install ansible](http://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) on the your host
Install python on the servers  
Install required rolles:  
```sh
$ ansible-galaxy install jdauphant.nginx
$ ansible-galaxy install jdauphant.ssl-certs
$ git clone https://github.com/wunzeco/ansible-java && mv ansible-java ~/.ansible/roles/wunzeco.java
$ git clone https://github.com/wunzeco/ansible-jenkins && mv ansible-jenkins ~/.ansible/roles/wunzeco.jenkins
```
Clone this repository in your directory:

```sh
$ git clone https://github.com/zedit/ansible-jenkinsmaster_jenkinsslave 
$ cd ansible-jenkinsmaster_jenkinsslave
```
Create directories ./files/ssl/  
Put certificates in the directory ./files/ssl/  
Specify host addresses in the file /etc/ansible/hosts  
In the playbook play.yaml you can override varibales according to the [table](#Table1), if it's needed  
Ansible hosts file placed in /etc/ansible/  
Execute command  

```sh
$ ansible-playbook play.yaml --extra-vars "ansible_sudo_pass=yourPassword"
```

#### <a name="Ex1"></a> Example hosts file:

```sh
[jenkinsmaster]
192.168.122.123 ansible_ssh_port=22 ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa

[jenkinslave]
192.168.122.77 ansible_ssh_port=22 ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
```

#### <a name="Table1"></a> Playbook variables
| Variable name | Variables description | Default Value |
| ------------- | --------------------- | ------------- |
| ssl_certs_local_privkey_path | path to your privite key | 'files/ssl/web.key' |
| ssl_certs_local_cert_path | path to your privite certificate | 'files/ssl/web.crt' |
| ssl_certs_common_name | certificate common name | 'web' |
| ssl_certs_path_owner | owner of the directory | 'root' | 
| ssl_certs_path_group | group | 'root' |   
| ssl_certs_path | directory on the server, where will be placed certificates | '/etc/ssl/web' |
| ssl_certs_privkey_path | path to private ket on the server | '/etc/ssl/web/web.key' |
| ssl_certs_cert_path | path to certificate on the server | '/etc/ssl/web/web.crt' |
