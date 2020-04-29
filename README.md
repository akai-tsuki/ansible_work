# ansible_work

These are sample playbook files for my study.

## pacemaker

Download rpm to install repogitory

```
[root@pm01 ansible_work]# ansible-playbook -i hosts-ha-cluster.yml 00-download.yml
```

### Install

```
[root@pm01 ansible_work]# ansible-playbook -i hosts-ha-cluster.yml 10-pacemaker-install.yml --list-tasks --tags install

playbook: 10-pacemaker-install.yml

  play #1 (hacluster): hacluster        TAGS: []
    tasks:
      pacemaker-install : exclude Pacemaker packages in CentOS repository       TAGS: [install, never]
      pacemaker-install : Copy Pacemaker repository package to nodes    TAGS: [install, never, test]
      pacemaker-install : install the repository package        TAGS: [install, never]
      pacemaker-install : cleanup yum cache     TAGS: [install, never]
      pacemaker-install : install Pacemaker packages    TAGS: [install, never]
      pacemaker-install : make sure Pacemaker services are disabled in systemd  TAGS: [install, never]
      pacemaker-install : create corosync.conf for multicast    TAGS: [install, never]
      pacemaker-install : create corosync.conf for unicast      TAGS: [install, never]
      pacemaker-install : generate authkey on the first host    TAGS: [install, never]
      pacemaker-install : fetch authkey to local temporally     TAGS: [install, never]
      pacemaker-install : distribute authkey to all nodes       TAGS: [install, never]
      pacemaker-install : remove copied authkey in local        TAGS: [install, never]
      pacemaker-install : config /etc/sysconfig/pacemaker       TAGS: [install, never]
      pacemaker-install : copy corosync.service to customize    TAGS: [install, never]
      pacemaker-install : configure corosync.service    TAGS: [install, never]
      pacemaker-install : copy pacemaker.service to customize   TAGS: [install, never]
      pacemaker-install : configure pacemaker.service   TAGS: [install, never]
      pacemaker-install : check if firewalld is enabled TAGS: [install, never]
      pacemaker-install : allow Pacemaker/Corosync communication through firewalld (permanent)  TAGS: [install, never]
      pacemaker-install : allow Pacemaker/Corosync communication through firewalld (runtime)    TAGS: [install, never]
[root@pm01 ansible_work]#
```

### Start

```
[root@pm01 ansible_work]# ansible-playbook -i hosts-ha-cluster.yml 10-pacemaker-install.yml --list-tasks --tags start

playbook: 10-pacemaker-install.yml

  play #1 (hacluster): hacluster        TAGS: []
    tasks:
      pacemaker-install : Start pacemaker       TAGS: [never, start]
      pacemaker-install : wait for Pacemaker startup completion TAGS: [never, start]
[root@pm01 ansible_work]#
```

### Load crm

```
[root@pm01 ansible_work]# ansible-playbook -i hosts-ha-cluster.yml 10-pacemaker-install.yml --list-tasks --tags load-crm

playbook: 10-pacemaker-install.yml

  play #1 (hacluster): hacluster        TAGS: []
    tasks:
      pacemaker-install : Copy crm file for Pacemaker   TAGS: [load-crm, never]
      pacemaker-install : Execute crm_mon       TAGS: [load-crm, never]
      pacemaker-install : Show crm_mon  TAGS: [load-crm, never]
      pacemaker-install : Load crm file for Pacemaker   TAGS: [load-crm, never]
[root@pm01 ansible_work]#
```

### Stop

```
[root@pm01 ansible_work]# ansible-playbook -i hosts-ha-cluster.yml 10-pacemaker-install.yml --list-tasks --tags stop

playbook: 10-pacemaker-install.yml

  play #1 (hacluster): hacluster        TAGS: []
    tasks:
      pacemaker-install : check if Pacemaker service is presented       TAGS: [clear-cib, never, stop]
      pacemaker-install : stop Pacemaker service if exists      TAGS: [clear-cib, never, stop]
[root@pm01 ansible_work]#
```

### Clear cib

```
[root@pm01 ansible_work]# ansible-playbook -i hosts-ha-cluster.yml 10-pacemaker-install.yml --list-tasks --tags clear-cib

playbook: 10-pacemaker-install.yml

  play #1 (hacluster): hacluster        TAGS: []
    tasks:
      pacemaker-install : check if Pacemaker service is presented       TAGS: [clear-cib, never, stop]
      pacemaker-install : stop Pacemaker service if exists      TAGS: [clear-cib, never, stop]
      pacemaker-install : erase the CIB TAGS: [clear-cib, never]
[root@pm01 ansible_work]#
```

I referred to this page for some playbook files to install pacemaker.  
https://github.com/kskmori/ansible-pacemaker
