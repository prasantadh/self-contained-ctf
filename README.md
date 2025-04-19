# Lab setup using Vagrant and Ansible

Experiments in hosting the infrastructure for HackTheBox like machines
for teaching pentesting. The current setup brings up one Kali machine
that starts `NUMBER_OF_SESSIONS` vnc servers available over `192.168.56.2`
port `8000 + connection`. The default `NUMBER_OF_SESSIONS` is 3 so
will be available on port `8001, 8002, 8003`.

The system will also bring up `NUMBER_OF_TEAMS` ubuntu machine with
IP `192.168.56.{200 + team}`. The default `NUMBER_OF_TEAMS` is 1
so the ubuntu machine is available over at `192.168.56.201`

## Installation

1. Install [Vagrant](https://developer.hashicorp.com/vagrant/downloads)
2. Install VirtualBox:
  ```bash
  sudo apt update
  sudo apt install -y virtualbox virtualbox-ext-pack
  ```
3. Install Ansible:
  ```bash
  sudo apt install -y pipx
  pipx install --include-deps ansible
  ```
4. Install [`vagrant-none-communicator`](https://github.com/soapy1/vagrant-none-communicator):
  ```bash
  vagrant plugin install vagrant-none-communicator
  ```

## Startup

```bash
vagrant up --no-provision
vagrant provision
```

## Shutdown

```bash
vagrant halt
```

## Delete

```bash
vagrant destroy -f
```

## Troubleshooting

```bash
# when memory allocation fails, 
# it is because vagrant cache is full you can drop them using
sudo sh -c "echo 3 > /proc/sys/vm/drop_caches"
```
