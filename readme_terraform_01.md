1.1
	
  1. Пока ТЗ не описано четко и возможно внесение множества изменений, и пока заказчик один, думаю стоит выбрать изменяемый тип инфраструктуры, чтобы не пересобирать среду при малейшем изменении. Когда будет обазначено более четкое ТЗ, перейти на не изменияемую инфраструктуру.
	
  2. На начальном этапе лучше выбрать облачную инфраструктуру, без центрального сервера.
	
  3. Можно использовать связку Terraform и Ansible, для них установка агентов не требуется.
	
  4. Да, например Terraform и Ansible.
	
1.2 Terraform, Ansible, Packer, Docker + AWS или YC.

1.3 Да, если для какой-то конкретной задачи или процесса больше подойдет альтернативный инмтрумент.

2.

<img src="https://github.com/tarsepav/devops-netology/blob/main/src/snap701.png"></img>

3.

		vagrant@server1:~$ sudo mkdir -p /usr/local/tf/11
		vagrant@server1:~$ cd /usr/local/tf/11
		vagrant@server1:/usr/local/tf/11$ sudo wget https://releases.hashicorp.com/terraform/0.11.14/terraform_0.11.14_linux_amd64.zip
		--2022-08-01 14:11:30--  https://releases.hashicorp.com/terraform/0.11.14/terraform_0.11.14_linux_amd64.zip
		Resolving releases.hashicorp.com (releases.hashicorp.com)... 151.101.114.49
		Connecting to releases.hashicorp.com (releases.hashicorp.com)|151.101.114.49|:443... connected.
		HTTP request sent, awaiting response... 200 OK
		Length: 12569267 (12M) [application/zip]
		Saving to: ‘terraform_0.11.14_linux_amd64.zip’

		terraform_0.11.14_l 100%[===================>]  11.99M  1.37MB/s    in 15s     

		2022-08-01 14:11:46 (823 KB/s) - ‘terraform_0.11.14_linux_amd64.zip’ saved [12569267/12569267]

		vagrant@server1:/usr/local/tf/11$ sudo unzip terraform_0.11.14_linux_amd64.zip
		Archive:  terraform_0.11.14_linux_amd64.zip
		  inflating: terraform               
		vagrant@server1:/usr/local/tf/11$ sudo rm terraform_0.11.14_linux_amd64.zip
		vagrant@server1:/usr/bin$ sudo ln -s /usr/local/tf/11/terraform /usr/bin/terraform11
		vagrant@server1:/usr/bin$ sudo chmod ugo+x /usr/bin/terraform*
		vagrant@server1:/usr/bin$ cd ~
		vagrant@server1:~$ terraform --version
		Terraform v1.2.6
		on linux_amd64
		vagrant@server1:~$ terraform11 --version
		Terraform v0.11.14

		Your version of Terraform is out of date! The latest version
		is 1.2.6. You can update by downloading from www.terraform.io/downloads.html
		vagrant@server1:~$ 
