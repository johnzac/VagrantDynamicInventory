# ansible_projects
vagrantDynamicInventory:
An ansible bootstapping role for using ansible to deploy to various vagrant machines in a local network. The ansible
master would need ssh access to all machines hosting the vagrant machines. The role would create a vagrant inventory
file with the public ip's of all vagrant machines running on the hosts( to be provided in the inventory when running the
playbook) if the vagrant machines are assigned public ip's( bridged networking). If the vagrant machines are not using
bridged networking, the role can set up the inventory so that ansible uses the remote host ip and port vagrant binds to
to connect to the machines. It will modify the iptables rules in the remote hosts ans would need root access for this. More
information is provided in the ansible README.
