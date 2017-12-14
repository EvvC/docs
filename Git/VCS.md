# Система контроля версия

## Преимущества
- Всегда доступна резервная копия на любую точку развития проекта. Всегда есть возможность откатиться назад
- В системе видно кто, когда и зачем внес правки (**ДОЛЖЕН** присутствовать комментарий с кратким описанием изменений. Если изменения связаны с задачей в кор. портале - писать номер задачи)
- Благодаря комментариям проще следить за историей проекта, понимать когда и зачем был внедрен функционал и как он должен работать.

0. Зарегистрироваться на [GitLab](https://gitlab.com/) и прислать логин [@saundefined](https://github.com/saundefined)
1. Создаем Git-репозиторий
2. Открываем проект в PhpStorm
Меню VCS -> Integrate VCS
VCS -> Git -> Remotes Добавляем удаленный репозиторий ссылкой вида https://username@bitbucket.org/prominado/project_name.ru.git
Содаем .gitignore с содержимым
````bash
.idea
.htaccess
/bitrix/
/upload/
.txt
*.log
*.xml
.gitignore
/.access.php
/.top.menu.php
urlrewrite.php
*.config
````

3. Созадем первый коммит
Правой кнопкой по корню проекта
Добавляем все файлы в гит: Git -> Add
Опять правой кнопкой по корню Git -> Commit Directory
Пишем комментарий -> Commit & Push

4. Качаем изменения
Правой кнопкой по корню -> Git -> Pull

5. Настраиваем сервер
Заходим по ssh в папку проекта
````bash
ssh user@host.ru
````

Создаем ssh-ключи, чтобы не вводить каждый раз пароль и изменения подтягивались по крону
````bash
cd ~/
mkdir .ssh
cd .ssh

ssh-keygen
````

passphrase оставляем пустой

после окончания генерации ключа вводим:

````bash
cat ~/.ssh/id_rsa.pub
````

получившийся ключ добавляем сюда: https://gitlab.com/profile/keys

переходим в папку с проектом, инициируем Git и добавляем к нему удаленный репозиторий
````bash
cd ~/www/host.ru
git init
git remote add origin git@bitbucket.org/prominado/project_name.ru.git
````

получаем изменения
````bash
git fetch
git checkout master
````

дальше вешаем на крон каждую минуту
````bash
cd ~/www/host.ru/ && git fetch
cd ~/www/host.ru/ && git reset --hard origin/master
````

Теперь, если какие то изменения попадают в нашу мастер ветку, то они автоматически попадают на сайт :)