# Run Playbook

```
$ ansible-playbook -e 'ansible_python_interpreter=python3' --become --inventory=docker-host, deploy.yml --key-file ~/.ssh/key.pem
```
