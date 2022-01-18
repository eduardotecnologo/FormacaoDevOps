1) Garante que a maquina virtual está rodando (vagrant up). Você pode ver o status (poweroff, running) da VM vagrant status.
2) Dentro do pasta do projeto crie o arquivo de Playbook, chamado provisioning.yml e escreva o conteúdo abaixo, repare nos 3 hífens iniciais:

```
---
- hosts: all
  tasks:
    - shell: 'echo hello > /vagrant/world.txt'
```

**3)** Abra o diretório do curso no terminal e execute o comando abaixo para utilizar o **Playbook** criado:

```
ansible-playbook provisioning.yml -u vagrant -i hosts --private-key .vagrant/machines/wordpress/virtualbox/private_key
```

**4)** Teste se o script funcionou logando na máquina virtual:

```
vagrant ssh
```

E execute o comando:

```
ls /vagrant/
```

Verifique se o arquivo **world.txt** foi criado. Execute o atalho **CTRL + C** para deslogar.

```
---
- hosts: all
  tasks:
    - name: 'Instala o PHP5'
      apt:
        name: php5
        state: latest
      become: yes
```


*Obs: Na versão mais recente do Ubuntu o PHP5 não está mais disponível. Neste caso você pode instalar o PHP 7 (`php`) junto com o `php-fpm`.*

Execute o rode o  *Playbook* :

```
ansible-playbook provisioning.yml -u vagrant -i hosts --private-key .vagrant/machines/wordpress/virtualbox/private_keyCOPIAR CÓDIGO
```

**6)** Adicione no seu **provisioning.yml** a instalação do **apache2** e do  **modphp** . Veja o resultado abaixo:

```
---
- hosts: all
  tasks:
    - name:'Instala o PHP5'
      apt:
        name: php5
        state: latest
      become: yes
    - name:'Instala o Apache2'
      apt:
        name: apache2
        state: latest
      become: yes
    - name:'Instala o modphp'
      apt:
        name: libapache2-mod-php5
        state: latest
      become: yesCOPIAR CÓDIGO
```

7) Teste se está tudo funcionando acessando o **IP** da máquina virtual, deverá exibir uma mensagem do Apache2!
