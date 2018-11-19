# Prepare for qnib/k8s-device-plugin-gpu

In order to use the [qnib/k8s-device-plugin-gpu]()
 - cuda needs to be installed
 - the devices have to be visible
 - a configuration file (`/etc/qnib-device-plugin/gpu.ini`) needs to be in place

## External resources
A couple of ansible roles needs external binaries.
- **docker** Swaps out the docker daemon and containerd with an experimental version to support GPUs
- **rcuda** installs files necessary to run rCUDA container. To use them the rCUDA tar ball is needed.

## Install

Make a copy (`ec2`) ot the `ec2.example` and adjust the IP addresses as well as the settings for `rcuda`, `docker` and the device plugin.

The ansible script was written against Ubuntu 18.04, please make sure you use this operating system.

```
$ ansible-playbook  -e 'ansible_python_interpreter=python3' \
                    --become deploy.yml [--key-file ssh-key.pem] \
                    --inventory=ec2 -l 10.0.0.2
```
