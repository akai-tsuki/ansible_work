# ansible_work

These are sample playbook files for my study.

## pacemaker

```
$ ansible-playbook -i hosts-ha-cluster.yml 00-download.yml
$ ansible-playbook -i hosts-ha-cluster.yml 10-pacemaker-install.yml
```

I referred to this page for some playbook files to install pacemaker.  
https://github.com/kskmori/ansible-pacemaker
