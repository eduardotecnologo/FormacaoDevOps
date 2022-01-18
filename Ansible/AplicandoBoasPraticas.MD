Chegou a hora de você executar o que foi visto na aula! Para isso, execute os passos listados abaixo.

---

**1)** Garante que a maquina virtual está rodando (`vagrant up`). Você pode ver o status (`poweroff`, `running`) da VM `vagrant status`.

**2)** Dentro do pasta do projeto crie o arquivo de  *Playbook* , chamado **provisioning.yml** e escreva o conteúdo abaixo, repare nos 3 hífens iniciais:

```
---
- hosts: all
  tasks:
    - shell:'echo hello > /vagrant/world.txt'COPIAR CÓDIGO
```

**3)** Abra o diretório do curso no terminal e execute o comando abaixo para utilizar o **Playbook** criado:

```
ansible-playbook provisioning.yml -u vagrant -i hosts --private-key .vagrant/machines/wordpress/virtualbox/private_keyCOPIAR CÓDIGO
```

**4)** Teste se o script funcionou logando na máquina virtual:

```
vagrant sshCOPIAR CÓDIGO
```

E execute o comando:

```
ls /vagrant/COPIAR CÓDIGO
```

Verifique se o arquivo **world.txt** foi criado. Execute o atalho **CTRL + C** para deslogar.

**5)** Modifique o arquivo  **provisioning.yml** , deixando-o conforme abaixo:

```
---
- hosts: all
  tasks:
    - name:'Instala o PHP5'
      apt:
        name: php5
        state: latest
      become: yesCOPIAR CÓDIGO
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
      become: yes
```


Na aula aprendemos como definir varias dependências no playbook através `{{ item }}` e `with_items`.

Exemplo com `with_items`:

```
- name:'Instala pacotes do sistema operacional'
      apt:
        name:'{{ item }}'
        state: latest
      become: yes
      with_items:
        - php5
        - apache2
        - libapache2-mod-php5COPIAR CÓDIGO
```

As versões mais recentes do Ansible descontinuaram ( *deprecated* ) essa forma de laço a favor de um nova sintaxe mais enxuta.

Abaixo o exemplo do mesmo laço mas agora listando os pacotes pelo `name`:

```
- name:'Instala pacotes do sistema operacional'
      apt:
        name:
        - php5
        - apache2
        - libapache2-mod-php5
        state: latest
      become: yes
```


Nesta aula, aprendemos:

* Como deixar nosso código mais enxuto com o uso de **`item`** e **`with_items`**
* Como configurar nosso projeto para lidar com chaves privadas diferentes
