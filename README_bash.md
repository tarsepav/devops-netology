1.
+ Переменная с будет равна a+b поскольку она умолчанию определена как строковая переменная.
+ Переменная d будет равна 1+2 поскольку a и b это простые числовые значения, а bash выводит выражение как последовательность переменных и знак +здесь выводится как текст.
+ Переменная e будет равна 3 поскольку выражение заключено в двойные скобки и bash уже может посчитать формулу

2.

      while ((1==1))
      do
        curl https://localhost:4757
        if (($? != 0))
        then
          sleep 1
          date >> curl.log
        else
                echo site is available!
        fi
      done
      
  3.
  
      #!/usr/bin/env bash
      ip=("192.168.0.1" "173.194.222.113" "87.250.250.24")
      port=80
      q=0
      while (($q < 5))
      do
        for i in ${ip[@]}
          do
            date >> nc.log
            nc -zv $i $port &>> nc.log
          done
          ((q++))
      done
      
 4.
   
      #!/usr/bin/env bash
      ip=("192.168.0.1" "173.194.222.113" "87.250.250.24")
      port=80

      while ((1==1))
      do
      for i in ${ip[@]}
        do
          nc -zv $i $port
          if (($? != 0))
          then
            echo $i > error
            exit 1
          fi
        done
      done
