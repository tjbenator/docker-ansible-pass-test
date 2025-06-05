
This is a test to pull secrets from [Password Store](https://www.passwordstore.org/) and pass them through into a docker compose using Ansible.

# Password Store Setup
* `sudo apt install pass`
* `gpg --full-generate-key`
 * Key type: `RSA`
 * Key size: `4096`
 * Expiry: `0`
 * Provide your name/email
* Initialize pass using the key you generated `pass init "$(gpg --list-secret-keys --keyid-format LONG | grep '^sec' | awk '{print $2}' | cut -d'/' -f2)"`

Ansible will automatically create credentials and store them in Password Store. After running the playbook you can view credentials by using `pass list` and `pass get [folder]`

# Ansible Setup

* `cd [repo]`
* `python3 -m venv .venv`
* `source .venv/bin/activate`
* `pip install -r requirements.txt`
* `ansible-playbook playbook.yml`
* You will be asked for your `gpg` key passphrase which will unlock `pass` if it's locked.
* Wait a few seconds for the database to start then navigate to http://localhost:80
* You should be presented with a page to enter your sites title and enter a username/password (for wordpress itself).
