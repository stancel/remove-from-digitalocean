remove-from-digitalocean
=========

Ansible role that removes DigitalOcean droplets (VPS) and DNS entries for given entries.


How to Use
------------

To use this playbook just run this command.

	1. ansible-galaxy install -r requirements.yml -p roles/  - Assumes you have external roles install
	2. Create a file called .vault_pass in this folder and put a random string in it for decrypting your sensitive variables. Something like: QSkngTv#KTJ=WXpg6qVR
	3. Fill out needed variables in vars/all_vars.yml and vars/vault.yml files
	4. ansible-vault encrypt vars/vault.yml   #Encrypt the sensitive variables
	5. ansible-playbook master.yml -e @vars/all_vars.yml -e @vars/vault.yml -i hosts/production


Requirements
------------

Used for personal / internal use. Must use DigitalOcean for the hosting and DNS networking features for this to be applicable.

Variables
------------

The droplet name as shown in DigitalOcean GUI. This is usually the hostname of the machine as well unless it was changed.
```
	host_name: "Fill in"
```
The Fully Qualified Domain Name that you would like to remove from the DigitalOcean DNS  system.
```
	server_fqdn: "Fill in"
```
Your DigitalOcean API token
```
	digital_ocean_api_token: "{{ lookup('env', 'DO_API_TOKEN') }}"
```

Roles
------------

	- stancel.remove_digitalocean_dns_entries	
	- stancel.remove_digitalocean_droplet	

Additional Info
------------

I have setup a bash profile alias to allow calling the playbook and choosing whether to reboot (yes/no as the first parameter argument)

```
alias remove-digitalocean='function _remove-digitalocean() { cd /Users/Brad/DevOps/Ansible_Playbooks/playbooks/remove-from-digitalocean; ansible-playbook master.yml --inventory-file=/Users/Brad/.ansible/hosts -e @vars/all_vars.yml --extra-vars "host_name=$1 server_fqdn=$2"; };_remove-digitalocean'
```



