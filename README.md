Vagrantfile and Ansible playbook for packer
====

Packer development environment on vagrant

## Requirement
* [VirtualBox](https://www.virtualbox.org/)
* [Vagrant](https://www.vagrantup.com/)
* [Ansible](http://www.ansible.com/)

## Installation
```bash
$ git clone git@github.com:shiwork/packer-vagrant.git
$ cd packer-vagrant
$ vagrant up
```

## Usage
Login vagrant
```bash
$ vagrant ssh
```

Add packer json file
```bash
$ touch config.json
$ vim config.json
```

Example config.json
```json
{
    "builders": [
        {
            "type": "docker",
            "image": "ubuntu:14.04",
            "export_path": "ubuntu.tar"
        }
    ],
    "provisioners": [
        {
            "type": "shell",
            "inline": ["echo test"]
        }
    ],
    "post-processors": [
        [
            {
                "type": "docker-import",
                "repository": "shiwork/ubuntu",
                "tag": "0.1"
            }
        ]
    ]
}
```

Build docker image
```bash
$ packer build config.json
```

## TIPS
### Use github/bitbucket access private key on vagrant
[config.ssh.forward_agent](http://docs-v1.vagrantup.com/v1/docs/config/ssh/forward_agent.html)

set up ssh-agent on host.
```bash
$ ssh-agent
$ ssh-add ~/.ssh/id_rsa # github/bitbucket access key
$ vagrant ssh
```
