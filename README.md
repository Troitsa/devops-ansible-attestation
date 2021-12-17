# ELK Stack with Ansible

Создать ansible роли для развертки Elastic Stack, создать ansible playbook, применяющий соответствующие роли. Цель сбора логов - nginx на одной из виртуалок.

## Технические детали:

Elastic Stack роль. Забираем установочные архивы с адресов, представленных на основном сайте. Установить и сконфигурировать Elasticsearch, Kibana, filebeat


## Решение

Развернуто три машины на Яндекс.Cloud: 
* NAT-instance, 
* Nginx+filebeat, 
* ELK stack

![](https://i.imgur.com/E6MnpaL.png)

Заходим по ssh на NAT-instance, устанавливаем ansible:
```
sudo apt update
sudo apt install ansible
```

Копируем playbooks (через WinSCP)

Запускаем:

`sudo ansible-playbook -i hosts/elastic.hosts playbooks/playbook_elk_setup.yml`

![](https://i.imgur.com/7NVnvrx.png)

`sudo ansible-playbook -i hosts/elastic.hosts playbooks/playbook_nginx_filebeat.yml`

![](https://i.imgur.com/9zY5X0N.png)


Прокидываем порт на своем компьютере:

`start putty -ssh -L 55601:10.10.0.10:5601 dev@51.250.20.161`

Переходим в браузер, настраиваем индекс, читаем логи:

![](https://i.imgur.com/8TOg4iL.png)


