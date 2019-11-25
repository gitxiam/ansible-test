# ansible-test
Приветсвую, будущие коллеги!
Здесь происходит следующее:

1. Устанавливается Ansible на облачный сервер с CentOS и еще один сервер для экспериментов.
В group_vars/servers указывается, что пользователь, выполняющий на целевой системе - root.

2. Создается файл hosts, проект маленький сделал только одну группу из одного хоста
3. По условию скопировал наработки из Galaxy, можно установить следующим образом:

ansible-galaxy install -r requirements.yml

4. Galaxy-роли bertvv.mariadb и bertvv.httpd конфигурируется, как в соответсвующих дирекориях в папке roles.
В роли bertvv.mariadb в defaults создается база для wordpress и пользователь работающий с базой CMS. Там, где в открытом виде появляется пароль от БД - конфиг шифруется ansible-vault.

5. Создаётся дополнительная роль для получения нужной версии php (php_depend):

cd /etc/ansible/roles
ansible-galaxy init php_depend

Роль добавляет дополнительные репозитории и указывает на желаемую версию php 5.6, затем устанавливается php и php-mysql

6. Роли для установки wordpress создавались следующим способом:

ansible-galaxy init wp-dependencies
ansible-galaxy init wp-install-config

- wp-dependencies хранит в себе данные для подключения, шифруется ansible-vault (остался от самописного примера, что я брал за основу)
- wp-install-config создает папку с исходниками под wordpress , тянет по url последнюю версию 
wordpress, копирует в /var/www/html файлы CMS-ки, копирует заранее приготовленный конфиг, настраивает права доступа 
 и затем ждет 20 секунд и перезагружает сервер, чтобы убедиться, что он работает и после внезапной перезагрузки не перестанет работать.
 В конце один fail, как раз из-за перезагрузки сервера.

7. Для запуска всех ролей последовательно необходимо запустить playbook_total.yaml:

ansible-playbook -i hosts playbook_total.yaml

8. Заходим по адресу в hosts: http://157.230.113.238/ и видим пустой сайт на wordpress. 
Первого пользователя Wordpress я настроил сам, больше там ничего интересного нет.
