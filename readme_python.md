# Домашнее задание к занятию "4.2. Использование Python для решения типовых DevOps задач"

## Обязательные задания

1. Есть скрипт:
    ```python
    #!/usr/bin/env python3
    a = 1
    b = '2'
    c = a + b
    ```
    * Какое значение будет присвоено переменной c?  
      * `TypeError: unsupported operand type(s) for +: 'int' and 'str'`
    * Как получить для переменной c значение 12?
      *   
    ```python
    usr/bin/env python3
    a = 1
    b = '2'
    c = str(a) + b
    ```
      * Как получить для переменной c значение 3?
        *   
    ```python
    usr/bin/env python3
    a = 1
    b = '2'
    c = a + int(b)
    ```

2. Мы устроились на работу в компанию, где раньше уже был DevOps Engineer. Он написал скрипт, позволяющий узнать, какие файлы модифицированы в репозитории, относительно локальных изменений. Этим скриптом недовольно начальство, потому что в его выводе есть не все изменённые файлы, а также непонятен полный путь к директории, где они находятся. Как можно доработать скрипт ниже, чтобы он исполнял требования вашего руководителя?

    ```python
    #!/usr/bin/env python3

    import os

    bash_command = ["cd ~/netology/sysadm-homeworks", "git status"]
    result_os = os.popen(' && '.join(bash_command)).read()
    is_change = False
    for result in result_os.split('\n'):
        if result.find('modified') != -1:
            prepare_result = result.replace('\tmodified:   ', '')
            print(prepare_result)
            break

    ```
   1. `break` лишний
   2. `is_change = False` лишний
   
   ```python
   #!/usr/bin/env python3
   
   import os
   
   bash_command = ["cd ~/netology/sysadm-homeworks", "git status", "pwd"]
   result_os = os.popen(' && '.join(bash_command)).read()
   #is_change = False
   git_path = result_os.split('\n')
   for result in git_path:
       if result.find('modified') != -1:
            prepare_result = result.replace('\tmodified:   ', '')
            print(os.path.join(git_path[-2], prepare_result))
            #break
   ```
3. Доработать скрипт выше так, чтобы он мог проверять не только локальный репозиторий в текущей директории, а также умел воспринимать путь к репозиторию, который мы передаём как входной параметр. Мы точно знаем, что начальство коварное и будет проверять работу этого скрипта в директориях, которые не являются локальными репозиториями.
   1. Если аргументы передаются в скрипт, то они будут использованы в качестве пути, если нет, тогда каталог будет использован каталог откуда запущен скрипт.
   2. Т.к. теперь путь к репозиторию формируется в процессе работы его можно более просто обрабатывать для формирования полного пути к изменённым файлам.
   3. Проверка является ли каталог локальным репозиторием осуществляется через перенаправление `stderr` в `stdout` и далее разбирается в условной конструкции
   ```python
   #!/usr/bin/env python3
   
   import os
   import sys
   
   repo_dir = os.getcwd()
   if len(sys.argv)>=2:
        repo_dir = sys.argv[1]
   
   bash_command = ["cd " + repo_dir, "git status 2>&1"]
   result_os = os.popen(' && '.join(bash_command)).read()
   git_path = result_os.split('\n')
   for result in git_path:
        if result.find('fatal') != -1:
            print(f"The {repo_dir} directory is not Git repository")
            break
        elif result.find('modified') != -1:
            prepare_result = result.replace('\tmodified:   ', '')
            print(os.path.join(repo_dir, prepare_result))            
   ```

4. Наша команда разрабатывает несколько веб-сервисов, доступных по http. Мы точно знаем, что на их стенде нет никакой балансировки, кластеризации, за DNS прячется конкретный IP сервера, где установлен сервис. Проблема в том, что отдел, занимающийся нашей инфраструктурой очень часто меняет нам сервера, поэтому IP меняются примерно раз в неделю, при этом сервисы сохраняют за собой DNS имена. Это бы совсем никого не беспокоило, если бы несколько раз сервера не уезжали в такой сегмент сети нашей компании, который недоступен для разработчиков. Мы хотим написать скрипт, который опрашивает веб-сервисы, получает их IP, выводит информацию в стандартный вывод в виде: <URL сервиса> - <его IP>. Также, должна быть реализована возможность проверки текущего IP сервиса c его IP из предыдущей проверки. Если проверка будет провалена - оповестить об этом в стандартный вывод сообщением: [ERROR] <URL сервиса> IP mismatch: <старый IP> <Новый IP>. Будем считать, что наша разработка реализовала сервисы: drive.google.com, mail.google.com, google.com.  
   1. Скрипт и пример работы
   ```python
   #!/usr/bin/env python3
   
   import socket
   import time as t
   
   url_list = ["drive.google.com", "mail.google.com", "google.com"]
   url_dict = dict.fromkeys(url_list)
   print("+++++++++++++")
   while 1==1:
       for url in url_list:
           check_addr = socket.gethostbyname(url)
           if check_addr == url_dict.get(url):
               print(f'{url} - {check_addr}')
           else:
               print(f'[ERROR] <{url}> IP mismatch: <{url_dict.get(url)}> <{check_addr}>')
               url_dict[url] = check_addr
       print("+++++++++++++")
       t.sleep(2)
   ```
   ```python
   /home/tarsepav/PycharmProjects/urlCheck/venv/bin/python /home/tarsepav/PycharmProjects/urlCheck/main.py 
    
    +++++++++++++
    drive.google.com - 173.194.222.194
    mail.google.com - 216.58.210.133
    google.com - 216.58.209.174
    +++++++++++++
   ```
