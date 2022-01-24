1.
<img src="https://github.com/tarsepav/netology_devops/blob/main/img/1.JPG"></img>
2.
<img src="https://github.com/tarsepav/netology_devops/blob/main/img/2.JPG"></img>
5.
<img src="https://github.com/tarsepav/netology_devops/blob/main/img/5.JPG"></img>

6.
config.vm.provider "virtualbox" do |v|
  v.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
end

config.vm.provider "virtualbox" do |v|
  v.memory = 1024
  v.cpus = 2
end

7.
<img src="https://github.com/tarsepav/netology_devops/blob/main/img/7.JPG"></img>
<img src="https://github.com/tarsepav/netology_devops/blob/main/img/7.1.JPG"></img>
8.
не сохранять в истории строки, начинающиеся с пробела и дубликаты

9.
Цикличное выполнение команды с подстановкой аргументов из списка "от до"

10.
touch {1..100000}
300000-не удасться, превышение размеров списка аргументов.

11. Проверяет существует ли директория /tmp, возвращает истину или ложь

12.
<img src="https://github.com/tarsepav/netology_devops/blob/main/img/12.JPG"></img>

13. Команда at принимает дату и время ( runtime ), когда вы хотите выполнить задание, как параметр командной строки, и команду, которая должна быть выполнена из стандартного ввода.

batch или его псевдоним at -b планирует задания и выполняет их в пакетной очереди, если позволяет уровень загрузки системы. По умолчанию задания выполняются, когда средняя загрузка системы ниже 1,5. Значение нагрузки можно указать при вызове демона atd
