# Asible role for base docker setup

Created for Ubuntu

## Usage

Add to ansible playbook following:

    - import_role:
        name: dr.docker
      vars:
        # add users to docker group
        drd_users: ["{{def_user}}"]
        # (yes/no) create additional docker network
        drd_create_network: no
        # new network name
        drd_net_name: custom
        # new network interface (default to docker1)
        drd_interface: docker1
        # new network host ip with subnet bit mask (/24 = 255.255.255.0)
        drd_net: 172.16.0.1/24
      tags: ['docker']
      become: yes

if you need more flexibility use next params:

        # next fills based on drd_net, but you can override
        drd_ip: "{{drd_net|ipaddr(1)|ipaddr('address')}}"
        drd_netmask: "{{drd_net|ipaddr('netmask')}}"
        drd_network: "{{drd_net|ipaddr('network')}}"

## Default parameters

Discover in `defaults/main.yml`

## Requirements

installed python `netaddr` lib

    pip install -U netaddr

or

    sudo apt-get install python-netaddr