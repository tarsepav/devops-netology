# Домашнее задание к занятию "4.3. Языки разметки JSON и YAML"

## Обязательные задания

1. Мы выгрузили JSON, который получили через API запрос к нашему сервису:
	```
    { "info" : "Sample JSON output from our service\t",
        "elements" :[
            { "name" : "first",
            "type" : "server",
            "ip" : 7175 
            },
            { "name" : "second",
            "type" : "proxy",
            "ip : 71.78.22.43
            }
        ]
    }
	```
Нужно найти и исправить все ошибки, которые допускает наш сервис
   1. Не хватает ковычек`"ip" : "71.78.22.43"`. "ip" : 7175` - что-то не так с выгруженным ip (точки потерялись?)


2. В прошлый рабочий день мы создавали скрипт, позволяющий опрашивать веб-сервисы и получать их IP. К уже реализованному функционалу нам нужно добавить возможность записи JSON и YAML файлов, описывающих наши сервисы. Формат записи JSON по одному сервису: { "имя сервиса" : "его IP"}. Формат записи YAML по одному сервису: - имя сервиса: его IP. Если в момент исполнения скрипта меняется IP у сервиса - он должен так же поменяться в yml и json файле.
   1. Добавил импорт бибоиотек и запись данных в файл
   ```python
   #!/usr/bin/env python3
   
   import socket
   import time as t
   import json
   import yaml
   
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
               with open(url + '.json', 'w') as js:
                   js.write(json.dumps({url: check_addr}))
               with open(url + '.yml', 'w') as ym:
                   ym.write(yaml.dump([{url: check_addr}]))
       print("+++++++++++++")
       t.sleep(2)
   ```
