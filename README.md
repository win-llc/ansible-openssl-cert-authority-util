# Ansible OpenSSL Certificate Authority (CA) Util Scripts

## Requirements

- Ansible
- Python 3

## Setup

pip3 install --upgrade pip
pip3 install cryptography
ansible-galaxy collection install -r requirements.yml

## Usage

### Setup CA
ansible-playbook --become setup_ca.yml -e 'ansible_python_interpreter=/usr/bin/python3'

### Generate Server Certificate
ansible-playbook --become gen_server_cert.yml -e 'ansible_python_interpreter=/usr/bin/python3' -e "server_fqdn=test.winllc-dev.com"

### Generate User Certificate
ansible-playbook --become gen_user_cert.yml -e 'ansible_python_interpreter=/usr/bin/python3' -e "user_cn='Test User 2'"

### Revoke Certificate
ansible-playbook --become revoke_cert.yml -e 'ansible_python_interpreter=/usr/bin/python3' --extra-vars "cert_file=<Name of file in ca/intermediate/certs/>"

### Teardown Generated Files and Directories
ansible-playbook --become teardown.yml -e 'ansible_python_interpreter=/usr/bin/python3'

## Generated Files
- PKCS#12 files are generated and saved in the ./pkcs12 directory. The default password is 'password'.
- CRLs are saved in the ./crl directory.