ansible-role-gocd
=============

Ansible Playbook to install GoCD and this role will be install latest version of GoCD server and agent.

This is multi roles repo, one role for server and one role for agent and one role for comman.

GoCD is an open source build and release tool from Thoughtworks.

Product details are available at http://www.go.cd .  Source available at https://github.com/GoCD/GoCD

# requirements
* 2 servers one for GoCD server and another one for GoCD agent

## Host file configuration
 On hosts file, you have to give server IP address under the [server] group and you have to give agent IP address under the [agents] group. Becasue the role should run based on the hosts group names. if you chaged the hosts file group names, please give the same in site.yml file.

## Database details:
- It will be install Postgresql 14 version.

installation instructions
=========================

This repository is organized as a multi-role playbook. You must reference following to run the roles.
```yml
- hosts: all
  become: yes
  roles:
    - common
  vars:
    GOCD_USER:
    GOCD_USERID: 
    GOCD_GROUP:
    GOCD_GROUPID:
    GOCD_DATABASE:
    GOCD_DATABASE_USER:
    GOCD_DATABASE_PASSWORD:
 
- hosts: server
  become: yes
  roles:
    - server
  vars:
    GOCD_USER: 
    GOCD_USERID: 
    GOCD_GROUP:
    GOCD_GROUPID: 
    GOCD_SHELL:
    GOCD_PASS:

- hosts: agents
  become: yes
  roles:
    - agent
  vars:
    GOCD_USER: 
    GOCD_GROUP:
    GO_SERVER_IP: 
```

# Variables:
 ### *Note: The below variable's values are default. If you need to change the default valuse, you can pass the variable and valuse on "site.yml", like above example formate*

## Command role default varibale valuse
| variable name | default value | description |
| ------------- | ------------- | ----------- |
| `GOCD_USER` | `go` | `It's a default user name` |
| `GOCD_USERID` | `5000` | `It's a default userID` |
| `GOCD_GROUP` | `gocd` | `It's a default group name` |
| `GOCD_GROUPID` | `5000` | `It's a default groupID` |
| `GOCD_SHELL` | `/bin/bash` | `It's a default shell for user` |
| `GOCD_PASS` | `go_pass` | `It's a default user passwor, it encrypted by SHA512.` |

*note: If you chage the default GOCD_PASS password, please encrypt then pass the encrypted result as a variable valuse, then only it should work. Use the below command to encript the password*
  ``` 
  python3 -c 'import crypt; print(crypt.crypt("password", crypt.mksalt(crypt.METHOD_SHA512)))'
  ```

## Server role default varibale valuse
| variable name | default value | description |
| ------------- | ------------- | ----------- |
| `GOCD_USER` | `go` | `It's a default user name` |
| `GOCD_GROUP` | `gocd` | `It's a default group name` |
| `GOCD_DATABASE` | `gocd_database` | `It's a default DB name` |
| `GOCD_DATABASE_USER` | `gocd_database_user` | `It's a default DB user name` |
| `GOCD_DATABASE_PASSWORD` | `gocd_database_password` | `It's a default DB password` |

## Agent role default varibale valuse
| variable name | default value | description |
| ------------- | ------------- | ----------- |
| `GOCD_USER` | `go` | `It's a default user name` |
| `GOCD_GROUP` | `gocd` | `It's a default group name` |
| `GO_SERVER_IP` | `NULL` | `Must be given the GO_server_IP for integrate go-server and go-agent` | 

*note: `GO_SERVER_IP` is must*

## Contributing
Don't hesitate to create a pull request
