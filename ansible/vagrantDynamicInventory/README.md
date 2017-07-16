Role Name
=========
Saves inventory information about vagrant hosts within machines specified in the inventory file. Can work with vagrant machines set up with bridge networking( saving public ip of machine to vagrant inventory) or private networking( saving host ip and port vagrant listens on). In case of vagrant machines that do not have a public ip, the script will need root access to the machine running the vagrant hosts for modifying iptables.  

Requirements
------------

Script would need root access to the host machines if vagrant is not set up to obtain a public ip by bridging. It uses jinja2 ipaddr filter to check if the returned values are ip addresses, so the ansible master machine would need to have python netaddr library installed. https://pypi.python.org/pypi/netaddr

Role Variables
--------------
The following variables can be set in the vars directory
eth - The vagrant interface to check for the public ip address. This is almost always eth1 which is the default value.
vagrant_inventory_file - The file into which vagrant inventory information is to be saved. The script appends host information into this file. Make sure it has login parameters set up.
ansible_master_static_ip - The public ip of the machine from which the script is run. This is used to alter iptable rules to allow connection from the ansible master to the ports vagrant binds to in host machines. 
connection_mode - Can be either 'Public' or 'PortForward' . Public in case the vagrant machines are assigned a public ip and you'd want to connect to the vagrant machines using the public ip. PortForward if the vagrant machines don't have a public ip and you want to connect to them via the port they bind to.


Example Playbook
----------------
An example of how the initial vagrant inventory file should be is in tests folder. You can run the playbook from the tests folder by running
ansible-playbook test.yml --extra-vars='vagrant_inventory_file="/etc/ansible/roles/vagrantDynamicInventory/tests/vagrantInventory"' --extra-vars='connection_mode="PortForward"'


License
-------

BSD

