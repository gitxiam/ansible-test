# ansible-test
Приветсвую, будущие коллеги!
Это мой обновляемый репозиторий для демонстрации опыта эксплуатации Ansible. Здесь есть коммиты от @Ctacfs, за что ему огромное спасибо, специально их не удалял, чтобы отработать rebase в git.
Данный набор ролей позволяет установить крайнюю версию wordpress на базе httpd, php 5.7, MariaDB.

Для запуска плейбука необходимо установить ansible, настроить защищенное соединение с целевым сервером и запустить playbook_total.yaml

ansible-playbook -i hosts playbook_total.yaml --ask-vault-pass

Пароль можно найти у меня в резюме.

Я запускал на этом сервере: http://157.230.113.238/ . После запуска playbook, последующей конфигурации и преднамеренной перезагрузки сервера, мы видим страницу конфигурации первого пользователя. Сейчас по ссылке пустой сайт, первого пользователя Wordpress я настроил сам, больше там ничего интересного нет (пока).
