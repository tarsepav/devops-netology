1. cd встроенная внутренняя команда окружения. Думаю, чтобы не создавать новый процесс при каждом её вызове, как с внешними приложениями.

2. grep string file -c

3.
vagrant@vagrant:~$ pstree -p

           systemd(1)─┬─VBoxService(971)─┬─{VBoxService}(975)
           │                  ├─{VBoxService}(976)
           │                  ├─{VBoxService}(977)
           │                  ├─{VBoxService}(978)

4.
ls -l > /dev/pts1

5.

           vagrant@vagrant:~$ cat 1.txt
line1
line2
line3

           vagrant@vagrant:~$ echo line > 2.txt

           vagrant@vagrant:~$ cat 2.txt
line

           vagrant@vagrant:~$ cat < 1.txt > 2.txt

           vagrant@vagrant:~$ cat 2.txt
line1
line2
line3

6.
Да, можно

           echo send from PTY to TTY > /dev/tty1

7. 
Создается дескриптор 5, переводится в stdout (1), при вводе echo netology переводится в д5, затем в stdout.

8.
vagrant@vagrant:~$ sdfad 4>&2 2>&1 1>&4 | grep command -c

           1

9.
Переменные окружения

printenv

10.
/proc/PID/cmdline – аргументы командной строки   
/proc/PID/exe -  является символьной ссылкой на исполненный бинарный файл

11.
grep sse /proc/cpuinfo
SSE 4_2

12.
Чтобы успешно подключаться по ssh к себе же ( на локалхост) нужно добавить публичный ключ (~/.ssh/id_rsa.pub) в конец файла ~/.ssh/authorized_keys

13.

 vagrant@vagrant:~$ ps -a
    PID TTY          TIME CMD
   1048 tty1     00:00:00 bash
   1131 tty1     00:00:00 top
   1132 pts/0    00:00:00 ps

 vagrant@vagrant:~$ reptyr 1131

14. 
tee производит вывод входного параметра в stdout и в файл (т.к. имеет права root) 
