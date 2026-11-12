# Домашнее задание к занятию "`Название занятия`" - `Фамилия и имя студента`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. В личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания
1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

systemctl status tuned
cat /etc/motd
total 12
drwxr-xr-x 3 root root 4096 Nov 12 12:05 .
drwxr-xr-x 5 root root 4096 Nov 12 12:05 ..
drwxr-xr-x 7 root root 4096 Feb  9  2024 kafka_2.13-3.7.0
● tuned.service - Dynamic System Tuning Daemon
     Loaded: loaded (/usr/lib/systemd/system/tuned.service; enabled; preset: enabled)
     Active: active (running) since Thu 2026-11-12 12:06:12 UTC; 41s ago
 Invocation: e328f2fd227647e8a8b61e279b157e29
       Docs: man:tuned(8)
             man:tuned.conf(5)
             man:tuned-adm(8)
   Main PID: 8570 (tuned)
      Tasks: 4 (limit: 1699)
     Memory: 18.8M (peak: 21.5M)
        CPU: 721ms
     CGroup: /system.slice/tuned.service
             └─8570 /usr/bin/python3 /usr/sbin/tuned -l -P
Добро пожаловать в систему!
Это сообщение изменено с помощью Ansible.



---

### Задание 2

vboxuser@TimofeevKirillAndreevich:~/docker-hw/sys-pattern-homework$ ansible-playbook motd.yml -K
BECOME password: 
[WARNING]: No inventory was parsed, only implicit localhost is available
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [Change MOTD Greeting with Host Info] *******************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************************************
ok: [localhost]

TASK [Update /etc/motd] **************************************************************************************************************************************************************************************************************
[WARNING]: Deprecation warnings can be disabled by setting `deprecation_warnings=False` in ansible.cfg.
[DEPRECATION WARNING]: INJECT_FACTS_AS_VARS default to `True` is deprecated, top-level facts will not be auto injected after the change. This feature will be removed from ansible-core version 2.24.
Origin: /home/vboxuser/docker-hw/sys-pattern-homework/motd.yml:6:19

4   become: yes
5   vars:
6     motd_message: |
                    ^ column 19

Use `ansible_facts["fact_name"]` (no `ansible_` prefix) instead.

changed: [localhost]

PLAY RECAP ***************************************************************************************************************************************************************************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

vboxuser@TimofeevKirillAndreevich:~/docker-hw/sys-pattern-homework$ cat /etc/motd
==========================================
Добро пожаловать на хост!

IP-адрес: 10.0.2.15
Hostname: TimofeevKirillAndreevich

Хорошего дня, системный администратор!
==========================================



---

### Задание 3

vboxuser@TimofeevKirillAndreevich:~/docker-hw/sys-pattern-homework$ ansible-playbook role_apache.yml -K
BECOME password: 
[WARNING]: No inventory was parsed, only implicit localhost is available
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [Configure Apache web server with system facts] *********************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************************************
ok: [localhost]

TASK [apache_web : Install Apache web server] ****************************************************************************************************************************************************************************************
ok: [localhost]

TASK [apache_web : Ensure Apache is started and enabled] *****************************************************************************************************************************************************************************
changed: [localhost]

TASK [apache_web : Configure index.html with system facts] ***************************************************************************************************************************************************************************
[WARNING]: Deprecation warnings can be disabled by setting `deprecation_warnings=False` in ansible.cfg.
[DEPRECATION WARNING]: INJECT_FACTS_AS_VARS default to `True` is deprecated, top-level facts will not be auto injected after the change. This feature will be removed from ansible-core version 2.24.
Origin: /home/vboxuser/docker-hw/sys-pattern-homework/roles/apache_web/templates/index.html.j2

Use `ansible_facts["fact_name"]` (no `ansible_` prefix) instead.

changed: [localhost]

TASK [apache_web : Ensure port 80 is open in UFW (if installed)] *********************************************************************************************************************************************************************
changed: [localhost]

TASK [apache_web : Check website availability] ***************************************************************************************************************************************************************************************
[DEPRECATION WARNING]: INJECT_FACTS_AS_VARS default to `True` is deprecated, top-level facts will not be auto injected after the change. This feature will be removed from ansible-core version 2.24.
Origin: /home/vboxuser/docker-hw/sys-pattern-homework/roles/apache_web/tasks/main.yml:31:10

29 - name: Check website availability
30   ansible.builtin.uri:
31     url: "http://{{ ansible_default_ipv4.address | default('localhost') }}"
            ^ column 10

Use `ansible_facts["fact_name"]` (no `ansible_` prefix) instead.

ok: [localhost]

RUNNING HANDLER [apache_web : Restart Apache] ****************************************************************************************************************************************************************************************
changed: [localhost]

PLAY RECAP ***************************************************************************************************************************************************************************************************************************
localhost                  : ok=7    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

vboxuser@TimofeevKirillAndreevich:~/docker-hw/sys-pattern-homework$ curl -I http://localhost
HTTP/1.1 200 OK
Date: Thu, 12 Nov 2026 12:31:55 GMT
Server: Apache/2.4.66 (Ubuntu)
Last-Modified: Thu, 12 Nov 2026 12:31:37 GMT
ETag: "2a3-660137e2241ac"
Accept-Ranges: bytes
Content-Length: 675
Vary: Accept-Encoding
Content-Type: text/html

