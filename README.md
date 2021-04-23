# ACI Port Hunter

The aci-port-hunter is a collective of ansible tasks that will find unused ports on an ACI fabric, and disable them. 

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

Tested working with Ansible 3.3

Debian
```
sudo apt install python3-pip
sudo -H pip3 install ansible
sudo -H pip3 install jmespath
```


### Installation of Playbook
Be advised, this playbook contains `vars_prompt` and requires user input

```
Copy the playbook folder to your ansible controller
```

### Execution

From within the aci-port-hunter folder, issue one of the following commands.


To find unused ports
```
ansible-playbook -i aci_hosts findports-aci.yml
```

To shut the unused ports found after running findports-aci.yml
```
ansible-playbook -i aci_hosts shutports-aci.yml
```

Upon execution, the playbook will ask for the user input.


### Details

Running `findports-aci.yml` will query your fabric for ports that are operationally down, and in a discovery state.  It will display this list of interfaces in the terminal window, as well as create a list of these interfaces in a file, in a folder called `ansible_intf_list`, in your users home directory. The users home directory is referenced with `~/`.  The contents of this file can be examined, reviewed, and even edited, although it should be noted any edits need to be formated and look nearly identical with what was originally outputted.

Running `shutports-aci.yml` will load and examine the outputted interface list from `findports-aci.yml` in your users home directory, and procede to disable (blacklist) those interfaces.

This tool was split into two functioning roles to account for the need of a change management approval process.  


### Built With

* [Ansible](https://www.ansible.com/)
* [Jmespath](https://jmespath.org/)
* [jinja2](https://jinja2docs.readthedocs.io/en/stable/)


### Authors

* **James Kayser** - *Initial work* - [kayserj](https://github.com/kayserj)

### License

GNU GPLv3


