Chegou a hora de você executar o que foi visto na aula! Para isso, execute os passos listados abaixo.

---

**1)** Depois de todo o bloco que você já criou para a instalação das dependências, crie uma base de dados MySQL. Seus parâmetros indicam o nome do banco, o login do MySQL (que por padrão, no Ubuntu, é  **root** ) e o  *state* , que nesse caso indica uma criação de banco:

```
- name:'Cria o banco do MySQL'
  mysql_db:
    name: wordpress_db
    login_user: root
    state: presentCOPIAR CÓDIGO
```

**2)** Em seguida, adicione outra  *task* , mas para criar um usuário do MySQL. Seus parâmetros indicam o usuário que será utilizado para autenticar, o nome do usuário a ser criado, a sua senha, seus privilégios e o  *state* , que nesse caso indica uma criação de usuário:

```
- name:'Cria o usuário do MySQL'
  mysql_user:
    login_user: root
    name: wordpress_user
    password:12345
    priv:'wordpress_db.*:ALL'
    state: presentCOPIAR CÓDIGO
```

Há também diversas outras opções e combinações que podemos fazer, tudo está disponível na [documentação do Ansible](http://docs.ansible.com/ansible/latest/index.html).

**3)** Por fim, rode o  *Playbook* :

```
ansible-playbook -i hosts provisioning.yml
```
