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


Go to Secret engine > Enable

![image](https://github.com/user-attachments/assets/4cbadb86-7610-4905-a276-1668e4a56427)

Select a KV (A normal key value pair) and Enable and Create Secret

![image](https://github.com/user-attachments/assets/b53157b1-58e9-4ff1-ae5d-9df7efa377f6)


![image](https://github.com/user-attachments/assets/579f9397-bc86-4110-994a-1267b2c2831b)


Go to Access and Enable new method

![image](https://github.com/user-attachments/assets/2cc2f49f-5088-4d1e-b0c5-e98e4fbbba06)

Select App role and Enable and to create role we need to use CLI, User Interface is not supported.

Go to CLI and Crate Policy

	vault policy write terraform - <<EOF
	path "*" {
	capabilities = ["list", "read"]
	}
	
	path "secrets/data/*" {
	capabilities = ["create", "read", "update", "delete", "list"]
	}
	
	path "sunny-kv/data/*" {
	capabilities = ["create", "read", "update", "delete", "list"]
	}
	
	
	path "secret/data/*" {
	capabilities = ["create", "read", "update", "delete", "list"]
	}
	
	path "auth/token/create" {
	capabilities = ["create", "read", "update", "list"]
	}
	EOF


  	vault write auth/approle/role/terraform \
      		secret_id_ttl=10m \
      		token_num_uses=10 \
      		token_ttl=20m \
      		token_max_ttl=30m \
      		secret_id_num_uses=40 \
      		token_policies=terraform


	vault read auth/approle/role/terraform/role-id

	vault write -f auth/approle/role/terraform/secret-id

Now, we got our secret ID's and access key ID

![image](https://github.com/user-attachments/assets/392f6caa-c643-488c-9859-19425c937a86)


Create main.tf 

	provider "vault" {
		address = "44.211.168.189:8200"
		skip_child_token = true
	
		auth_login {
			path = "auth/approle/login"
	
			parameters = {
				role_id = "2ae6f39a-512f-a13f-ed4e-eef8b8aba9ae"
				secret_id = "e4fb0c1e-39e9-32fe-ecdc-43a80d51e1bc"
			}
		}
	}






