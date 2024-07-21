Vault is developed by Hashicorp.

Hashicorp is different products listed below:
1. Terraform
2. Consul
3. Nomad
4. Boundary
5. Packer
6. Vagrant
7. Waypoint

* Vault manages Secrets and Protect Sensitive Data.
* Provides a Single source of Secrets for both Humans and Machines.


Installation:

		sudo apt update -y
		sudo apt update && sudo apt install gpg
		wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
		gpg --no-default-keyring --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg --fingerprint
		echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
		sudo apt update -y
		sudo apt install vault -y
		vault server -dev -dev-listen-address="0.0.0.0:8200"
		vault 		# validate if showing options means installed correctly

  		export VAULT_ADDR='http://0.0.0.0:8200'

Note: Leave the page of Installation as it is, Open new terminal

![image](https://github.com/user-attachments/assets/da038195-cd9c-48ec-8bb9-4197152f71d7)

Open with Public Ip:8200

Token > Paste Token from Installation Page





