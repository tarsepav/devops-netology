1. Что бы не указывать не указывать авторизационный токен в коде надо воспользоваться следующей командой
    
      
        export YC_TOKEN=`yc iam create-token`
        
2. Создать свой образ ami можно при помощи Packer

  Конфигурация terraform:

  1. [main.tf](https://github.com/tarsepav/devops-netology/blob/main/terraform-02/main.tf)
  1. [output.tf](https://github.com/tarsepav/devops-netology/blob/main/terraform-02/output.tf)
  1. [variables.tf](https://github.com/tarsepav/devops-netology/blob/main/terraform-02/variables.tf)
  1. [versions.tf](https://github.com/tarsepav/devops-netology/blob/main/terraform-02/versions.tf)
