requirements
1. ansible on yout host
2. python on the servers
```sh
$ ansible-galaxy install jdauphant.nginx
$ ansible-galaxy install jdauphant.ssl-certs
$ git clone https://github.com/wunzeco/ansible-java && mv ansible-java ~/.ansible/roles/wunzeco.java
$ git clone https://github.com/wunzeco/ansible-jenkins && mv ansible-jenkins ~/.ansible/roles/wunzeco.jenkins
$ git clone OUR_REPO
$ cd OUR_REPO
```
put certificates in the directory ./files/ssl/
specify host addresses in the file /etc/ansible/hosts

example:

```sh
[jenkinsmaster]
192.168.122.123 ansible_ssh_port=22 ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa

[jenkinslave]
192.168.122.77 ansible_ssh_port=22 ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
```

in the play.yaml override varibales if it's needed
      ssl_certs_local_privkey_path: 'files/ssl/web.key' - path to your privite key
      ssl_certs_local_cert_path: 'files/ssl/web.crt'    - path to your privite certificate
      ssl_certs_common_name: 'web'                      - 
      ssl_certs_path_owner: 'root'                      - owner of the directory 
      ssl_certs_path_group: 'root'                      - group
      ssl_certs_path: '/etc/ssl/web'                    - directory on the server, where will be placed certificates
      ssl_certs_privkey_path: '/etc/ssl/web/web.key'    - path to private ket on the server
      ssl_certs_cert_path: '/etc/ssl/web/web.crt'       - path to certificate on the server
ansible-playbook play.yaml --extra-vars "ansible_sudo_pass=yourPassword"
