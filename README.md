# A vagrant memcache box
```bash
vagrant up
```
```bash
vagrant provision --provision-with ansible
```

```bash
ansible-playbook \
  -i ansible/inventories/hosts.ini \
  -u vagrant \
  --private-key=../*-fe/.vagrant/machines/default/virtualbox/private_key \
  ansible/memcache_php.yml
```