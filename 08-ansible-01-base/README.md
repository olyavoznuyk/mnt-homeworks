### Домашнее задание к занятию 1 «Введение в Ansible»
## Основная часть
Попробуйте запустить playbook на окружении из test.yml, зафиксируйте значение, которое имеет факт some_fact для указанного хоста при выполнении playbook.
Найдите файл с переменными (group_vars), в котором задаётся найденное в первом пункте значение, и поменяйте его на all default fact.
Воспользуйтесь подготовленным (используется docker) или создайте собственное окружение для проведения дальнейших испытаний.
Проведите запуск playbook на окружении из prod.yml. Зафиксируйте полученные значения some_fact для каждого из managed host.
Добавьте факты в group_vars каждой из групп хостов так, чтобы для some_fact получились значения: для deb — deb default fact, для el — el default fact.
Повторите запуск playbook на окружении prod.yml. Убедитесь, что выдаются корректные значения для всех хостов.
При помощи ansible-vault зашифруйте факты в group_vars/deb и group_vars/el с паролем netology.
Запустите playbook на окружении prod.yml. При запуске ansible должен запросить у вас пароль. Убедитесь в работоспособности.
Посмотрите при помощи ansible-doc список плагинов для подключения. Выберите подходящий для работы на control node.
В prod.yml добавьте новую группу хостов с именем local, в ней разместите localhost с необходимым типом подключения.
Запустите playbook на окружении prod.yml. При запуске ansible должен запросить у вас пароль. Убедитесь, что факты some_fact для каждого из хостов определены из верных group_vars.
Заполните README.md ответами на вопросы. Сделайте git push в ветку master. В ответе отправьте ссылку на ваш открытый репозиторий с изменённым playbook и заполненным README.md.
Предоставьте скриншоты результатов запуска команд.

## Ответы на задания:

Значение, которое имеет факт some_fact

```
playbook git:(MNT-video) ansible-playbook -i inventory/test.yml site.yml 

PLAY [Print os facts] ************************************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************************
ok: [localhost]

TASK [Print OS] ******************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ****************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": 12
}

PLAY RECAP ***********************************************************************************************************************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

```

Назначение нового значения some_fact

```
playbook git:(MNT-video) ansible-playbook -i inventory/test.yml site.yml

PLAY [Print os facts] ************************************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************************
ok: [localhost]

TASK [Print OS] ******************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ****************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "all default fact"
}

PLAY RECAP ***********************************************************************************************************************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

```

Запуск окружения и з    апуск playbook на окружении prod.yml

```
playbook git:(MNT-video) ✗ docker run --rm --name "ubuntu" -d pycontribs/ubuntu:latest sleep 3600
Unable to find image 'pycontribs/ubuntu:latest' locally
latest: Pulling from pycontribs/ubuntu
423ae2b273f4: Pull complete 
de83a2304fa1: Pull complete 
f9a83bce3af0: Pull complete 
b6b53be908de: Pull complete 
7378af08dad3: Pull complete 
Digest: sha256:dcb590e80d10d1b55bd3d00aadf32de8c413531d5cc4d72d0849d43f45cb7ec4
Status: Downloaded newer image for pycontribs/ubuntu:latest
da3b3250e7270f955245f4bed31f4becbe41727396932a3bafc7ff9826df2a83
➜ playbook git:(MNT-video) ✗ docker run --rm --name "centos7" -d pycontribs/centos:7 sleep 3600
Unable to find image 'pycontribs/centos:7' locally
7: Pulling from pycontribs/centos
2d473b07cdd5: Pull complete 
43e1b1841fcc: Pull complete 
85bf99ab446d: Pull complete 
Digest: sha256:b3ce994016fd728998f8ebca21eb89bf4e88dbc01ec2603c04cc9c56ca964c69
Status: Downloaded newer image for pycontribs/centos:7
51981acd6df6ee44f278d7275b2096077cc95ebd89ae8cd4ccdc9a789d0ae726
➜  playbook git:(MNT-video) ✗ docker ps
CONTAINER ID   IMAGE                      COMMAND        CREATED          STATUS          PORTS     NAMES
da3b3250e727   pycontribs/ubuntu:latest   "sleep 3600"   16 seconds ago   Up 14 seconds             ubuntu
➜  playbook git:(MNT-video) ✗ docker ps
CONTAINER ID   IMAGE                      COMMAND        CREATED          STATUS          PORTS     NAMES
51981acd6df6   pycontribs/centos:7        "sleep 3600"   7 seconds ago    Up 6 seconds              centos7
da3b3250e727   pycontribs/ubuntu:latest   "sleep 3600"   27 seconds ago   Up 25 seconds             ubuntu
➜  playbook git:(MNT-video) ✗ ansible-playbook -i inventory/prod.yml site.yml                       

PLAY [Print os facts] ************************************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************************
ok: [centos7]
ok: [ubuntu]

TASK [Print OS] ******************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ****************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el"
}
ok: [ubuntu] => {
    "msg": "deb"
}

PLAY RECAP ***********************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

```
Новые факты в group_vars для групп хостов.

```
➜  playbook git:(MNT-video) ✗ ansible-playbook -i inventory/prod.yml site.yml

PLAY [Print os facts] ************************************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************************
ok: [centos7]
ok: [ubuntu]

TASK [Print OS] ******************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ****************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP ***********************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
```

Запуск playbook с окружением prod.yml и ключом --ask-vault-pass для запроса пароля шифрования.

```
➜  playbook git:(MNT-video) ✗ ansible-vault encrypt group_vars/deb/examp.yml 
New Vault password: 
Confirm New Vault password: 
Encryption successful
➜  playbook git:(MNT-video) ✗ ansible-vault encrypt group_vars/el/examp.yml 
New Vault password: 
Confirm New Vault password: 
Encryption successful
➜  playbook git:(MNT-video) ✗ ansible-playbook -i inventory/prod.yml site.yml                       

PLAY [Print os facts] ************************************************************************************************************************************************************************
ERROR! Attempting to decrypt but no vault secrets found
➜  playbook git:(MNT-video) ✗ ansible-playbook -i inventory/prod.yml site.yml --ask-vault-pass
Vault password: 

PLAY [Print os facts] ************************************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************************
ok: [centos7]
ok: [ubuntu]

TASK [Print OS] ******************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ****************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP ***********************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

Новая группа хостов с именем local в prod.yml и запуск playbook на окружении prod.yml

```
➜  playbook git:(MNT-video) ✗ ansible-doc -t connection --list | grep "on control"
ansible.builtin.local          execute on controller                       
➜  playbook git:(MNT-video) ✗ ansible-playbook -i inventory/prod.yml site.yml --ask-vault-pass
Vault password: 

PLAY [Print os facts] ************************************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************************
ok: [centos7]
ok: [ubuntu]
ok: [localhost]

TASK [Print OS] ******************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}
ok: [localhost] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ****************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}
ok: [localhost] => {
    "msg": "all default fact"
}

PLAY RECAP ***********************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

