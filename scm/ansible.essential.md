---
author: Artem Zhivushko
title: ansible.essential
create: 2024-03-27 01:32:11
tags:
  - ZeroToHero
  - DevSecOps
  - ansible
---

# Ansible

## inventory

> [!info] инвентарь определяет управляемые узлы, которые вы автоматизируете, с группами, чтобы вы могли запускать задачи автоматизации на нескольких хостах одновременно.

> [!warning] Даже если вы не определяете какие-либо группы в файле инвентаря, Ansible создает две группы по умолчанию: `all` и `ungrouped`.

> [!tip] yaml
> ```yaml
> ungrouped:
>   hosts:
>     mail.example.com:
> webservers:
>   hosts:
>     foo.example.com:
>     bar.example.com:
> dbservers:
>   hosts:
>     one.example.com:
>     two.example.com:
>     three.example.com:
> east:
>   hosts:
>     foo.example.com:
>     one.example.com:
>     two.example.com:
> west:
>   hosts:
>     bar.example.com:
>     three.example.com:
> prod:
>   children:
>     east:
> test:
>   children:
>     west:
> ```

> [!tip] ini
> ```ini
> ungrouped.example.com                        # An ungrouped host
> 
> [dbservers]
> one.example.com
> two.example.com
> three.example.com
> 
> [webservers]                                 # A group called webservers
> beta.example.com ansible_host = 10.0.0.5     # ssh to 10.0.0.5
> github.example.com ansible_ssh_user = abc    # ssh as user abc
> 
> [clouds]
> cloud.example.com fileuser = alice           # fileuser is a host variable
> 
> [moscow]
> beta.example.com                             # Host (DNS will resolve)
> telecom.example.com                          # Host (DNS will resolve)
> 
> [dev1:children]                              # dev1 is a group containing
> webservers                                   # All hosts in group webservers
> clouds                                       # All hosts in group clouds
> ```

> [!tip] Ansible Host Patterns
> ```bash
> all                  # all hosts in inventory
> *                    # all hosts in inventory
> ungrouped            # all hosts in inventory not appearing within a group
> 10.0.0.*             # all hosts with an IP starting 10.0.0.*
> webservers           # the group webservers
> webservers:!moscow   # only hosts in the group webservers, without group moscow
> webservers:&moscow   # only hosts in the group's webservers and moscow
> ```

## Check connecting to hosts, server name or group

```bash
ansible -m ping <HOSTS, SERVER_NAME or GROUP>
```

## Ansible playbooks - это файлы сценариев
> содержат информацию о том, какого результата и на каких машинах нужно достичь

- vars: <переменные, которые нужно использовать при выполнении скрипта>;
- sudo: <выполнение команды от лица другого пользователя, как правило суперпользователя root, параметр принимает значения yes и no>;
- gather_facts: <сбор или отказ от сбора информации о хостах, значение по умолчанию — yes: Ansible собирает данные о серверах, если не указать обратное>.

```yaml
---                                                    # (начало документа)
- name: Update web servers                             # <имя сценария>
  hosts: webservers                                    # <имя сервера, к которому надо применить изменения>
  remote_user: root                                    # <имя пользователя для авторизации в системе на сервере; в новых версиях используется параметр remote_user, в старых — просто user>

  tasks:                                               # <состояние, к которому нужно привести сервер>
  - name: Ensure apache is at the latest version       # <имя задачи>
    ansible.builtin.yum:
      name: httpd
      state: latest

  - name: Write the apache config file
    ansible.builtin.template:
      src: /srv/httpd.j2
      dest: /etc/httpd.conf

- name: Update db servers
  hosts: databases
  remote_user: root

  tasks:
  - name: Ensure postgresql is at the latest version
    ansible.builtin.yum:
      name: postgresql
      state: latest

  - name: Ensure that postgresql is started
    ansible.builtin.service:
      name: postgresql
      state: started
```

## Roles - инструмент Ansible, для более быстрого решения типовых задач

### Role directory structure

```
roles/
    common/               # this hierarchy represents a "role"
        tasks/            #
            main.yml      #  <-- tasks file can include smaller files if warranted
        handlers/         #
            main.yml      #  <-- handlers file
        templates/        #  <-- files for use with the template resource
            ntp.conf.j2   #  <------- templates end in .j2
        files/            #
            bar.txt       #  <-- files for use with the copy resource
            foo.sh        #  <-- script files for use with the script resource
        vars/             #
            main.yml      #  <-- variables associated with this role
        defaults/         #
            main.yml      #  <-- default lower priority variables for this role
        meta/             #
            main.yml      #  <-- role dependencies
        library/          # roles can also include custom modules
        module_utils/     # roles can also include custom module_utils
        lookup_plugins/   # or other types of plugins, like lookup in this case

    webtier/              # same kind of structure as "common" was above, done for the webtier role
    monitoring/           # ""
    fooapp/               # ""
```

- ``tasks/main.yml`` - the main list of tasks that the role executes.
- ``handlers/main.yml`` - handlers, which may be used within or outside this role.
- ``library/my_module.py`` - modules, which may be used within this role (see :ref:`embedding_modules_and_plugins_in_roles` for more information).
- ``defaults/main.yml`` - default variables for the role (see :ref:`playbooks_variables` for more information). These variables have the lowest priority of any variables available and can be easily overridden by any other variable, including inventory variables.
- ``vars/main.yml`` - other variables for the role (see :ref:`playbooks_variables` for more information).
- ``files/main.yml`` - files that the role deploys.
- ``templates/main.yml`` - templates that the role deploys.
- ``meta/main.yml`` - metadata for the role, including role dependencies and optional Galaxy metadata such as platforms supported.
