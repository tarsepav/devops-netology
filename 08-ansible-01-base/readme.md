0.

		vagrant@server1:~/homeworks/ansible/08-ansible-01-base$ ansible --version
		ansible 2.9.6

1.

		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ ansible-playbook -i inventory/test.yml site.yml

		PLAY [Print os facts] **********************************************************

		TASK [Gathering Facts] *********************************************************
		ok: [localhost]

		TASK [Print OS] ****************************************************************
		ok: [localhost] => {
			"msg": "Ubuntu"
		}

		TASK [Print fact] **************************************************************
		ok: [localhost] => {
			"msg": 12
		}

		PLAY RECAP *********************************************************************
		localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

2.

		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ grep -r some_fact group_vars/
		group_vars/el/examp.yml:  some_fact: "el"
		group_vars/deb/examp.yml:  some_fact: "deb"
		group_vars/all/examp.yml:  some_fact: 12
		
		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ sudo nano group_vars/all/examp.yml
		group_vars/all/examp.yml:  some_fact: 'all default fact'
		
3.
		docker-compose.yml
		
		version: '3'
		services:
		  centos7:
			image: pycontribs/centos:7
			container_name: centos7
			restart: unless-stopped
			entrypoint: "sleep infinity"

		  ubuntu:
			image: pycontribs/ubuntu
			container_name: ubuntu
			restart: unless-stopped
			entrypoint: "sleep infinity"

4.


		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ docker-compose up
		Pulling centos7 (pycontribs/centos:7)...
		7: Pulling from pycontribs/centos
		2d473b07cdd5: Already exists
		43e1b1841fcc: Pull complete
		85bf99ab446d: Pull complete
		Digest: sha256:b3ce994016fd728998f8ebca21eb89bf4e88dbc01ec2603c04cc9c56ca964c69
		Status: Downloaded newer image for pycontribs/centos:7
		Pulling ubuntu (pycontribs/ubuntu:)...
		latest: Pulling from pycontribs/ubuntu
		423ae2b273f4: Pull complete
		de83a2304fa1: Pull complete
		f9a83bce3af0: Pull complete
		b6b53be908de: Pull complete
		7378af08dad3: Pull complete
		Digest: sha256:dcb590e80d10d1b55bd3d00aadf32de8c413531d5cc4d72d0849d43f45cb7ec4
		Status: Downloaded newer image for pycontribs/ubuntu:latest
		Creating ubuntu  ... done
		Creating centos7 ... done
		Attaching to centos7, ubuntu
		
		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ docker-compose top
		centos7
		UID     PID    PPID    C   STIME   TTY     TIME          CMD      
		------------------------------------------------------------------
		root   25053   25004   0   19:56   ?     00:00:00   sleep infinity

		ubuntu
		UID     PID    PPID    C   STIME   TTY     TIME          CMD      
		------------------------------------------------------------------
		root   25046   25006   0   19:56   ?     00:00:00   sleep infinity
		

		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ ansible-playbook -i inventory/prod.yml -v site.yml
		Using /etc/ansible/ansible.cfg as config file

		PLAY [Print os facts] *****************************************************************************************************************************

		TASK [Gathering Facts] ****************************************************************************************************************************
		[DEPRECATION WARNING]: Distribution Ubuntu 18.04 on host ubuntu should use /usr/bin/python3, but is using /usr/bin/python for backward 
		compatibility with prior Ansible releases. A future Ansible release will default to using the discovered platform python for this host. See 
		https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information. This feature will be removed in version
		 2.12. Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
		ok: [ubuntu]
		ok: [centos7]

		TASK [Print OS] ***********************************************************************************************************************************
		ok: [centos7] => {
			"msg": "CentOS"
		}
		ok: [ubuntu] => {
			"msg": "Ubuntu"
		}

		TASK [Print fact] *********************************************************************************************************************************
		ok: [centos7] => {
			"msg": "el"
		}
		ok: [ubuntu] => {
			"msg": "deb"
		}

		PLAY RECAP ****************************************************************************************************************************************
		centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
		ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

5.

		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ sudo nano group_vars/deb/examp.yml
		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ sudo nano group_vars/el/examp.yml
		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ cat group_vars/el/examp.yml
		---
		  some_fact: "el default fact"
		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ cat group_vars/el/examp.yml
		---
		  some_fact: "el default fact"
		  
6.

		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ ansible-playbook -i inventory/prod.yml -v site.yml
		Using /etc/ansible/ansible.cfg as config file

		PLAY [Print os facts] *****************************************************************************************************************************

		TASK [Gathering Facts] ****************************************************************************************************************************
		[DEPRECATION WARNING]: Distribution Ubuntu 18.04 on host ubuntu should use /usr/bin/python3, but is using /usr/bin/python for backward 
		compatibility with prior Ansible releases. A future Ansible release will default to using the discovered platform python for this host. See 
		https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information. This feature will be removed in version
		 2.12. Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
		ok: [ubuntu]
		ok: [centos7]

		TASK [Print OS] ***********************************************************************************************************************************
		ok: [ubuntu] => {
			"msg": "Ubuntu"
		}
		ok: [centos7] => {
			"msg": "CentOS"
		}

		TASK [Print fact] *********************************************************************************************************************************
		ok: [centos7] => {
			"msg": "el default fact"
		}
		ok: [ubuntu] => {
			"msg": "deb default fact"
		}

		PLAY RECAP ****************************************************************************************************************************************
		centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
		ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

7.

		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ ansible-vault encrypt group_vars/deb/examp.yml
		New Vault password: 
		Confirm New Vault password: 
		Encryption successful
		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ ansible-vault encrypt group_vars/el/examp.yml
		New Vault password: 
		Confirm New Vault password: 
		Encryption successful
		
8.

		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ ansible-playbook -i inventory/prod.yml -v site.yml
		Using /etc/ansible/ansible.cfg as config file

		PLAY [Print os facts] *****************************************************************************************************************************
		ERROR! Attempting to decrypt but no vault secrets found
		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ ansible-playbook -i inventory/prod.yml site.yml --ask-vault-pass
		Vault password: 

		PLAY [Print os facts] *****************************************************************************************************************************

		TASK [Gathering Facts] ****************************************************************************************************************************
		[DEPRECATION WARNING]: Distribution Ubuntu 18.04 on host ubuntu should use /usr/bin/python3, but is using /usr/bin/python for backward 
		compatibility with prior Ansible releases. A future Ansible release will default to using the discovered platform python for this host. See 
		https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information. This feature will be removed in version
		 2.12. Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
		ok: [ubuntu]
		ok: [centos7]

		TASK [Print OS] ***********************************************************************************************************************************
		ok: [centos7] => {
			"msg": "CentOS"
		}
		ok: [ubuntu] => {
			"msg": "Ubuntu"
		}

		TASK [Print fact] *********************************************************************************************************************************
		ok: [centos7] => {
			"msg": "el default fact"
		}
		ok: [ubuntu] => {
			"msg": "deb default fact"
		}

		PLAY RECAP ****************************************************************************************************************************************
		centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
		ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

9.

		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ ansible-doc -t connection -l
		local        execute on controller                                                                                                            

10.

		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ sudo nano inventory/prod.yml
		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ cat inventory/prod.yml
		---
		  el:
			hosts:
			  centos7:
				ansible_connection: docker
		  deb:
			hosts:
			  ubuntu:
				ansible_connection: docker
		  local:
			hosts:
			  localhost:
				ansible_connection: local

11.

		vagrant@server1:~/homeworks/ansible/08-ansible-01-base/playbook$ ansible-playbook -i inventory/prod.yml site.yml --ask-vault-pass
		Vault password: 

		PLAY [Print os facts] *****************************************************************************************************************************

		TASK [Gathering Facts] ****************************************************************************************************************************
		ok: [localhost]
		[DEPRECATION WARNING]: Distribution Ubuntu 18.04 on host ubuntu should use /usr/bin/python3, but is using /usr/bin/python for backward 
		compatibility with prior Ansible releases. A future Ansible release will default to using the discovered platform python for this host. See 
		https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information. This feature will be removed in version
		 2.12. Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
		ok: [ubuntu]
		ok: [centos7]

		TASK [Print OS] ***********************************************************************************************************************************
		ok: [localhost] => {
			"msg": "Ubuntu"
		}
		ok: [centos7] => {
			"msg": "CentOS"
		}
		ok: [ubuntu] => {
			"msg": "Ubuntu"
		}

		TASK [Print fact] *********************************************************************************************************************************
		ok: [localhost] => {
			"msg": "all default fact"
		}
		ok: [centos7] => {
			"msg": "el default fact"
		}
		ok: [ubuntu] => {
			"msg": "deb default fact"
		}

		PLAY RECAP ****************************************************************************************************************************************
		centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
		localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
		ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

