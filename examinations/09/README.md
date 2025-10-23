# Examination 9 - Use Ansible Vault for sensitive information

In the previous examination we set a password for the `webappuser`. To keep this password
in plain text in a playbook, or otherwise, is a huge security hole, especially
if we publish it to a public place like GitHub.

There is a way to keep sensitive information encrypted and unlocked at runtime with the
`ansible-vault` tool that comes with Ansible.

https://docs.ansible.com/ansible/latest/vault_guide/index.html

*IMPORTANT*: Keep a copy of the password for _unlocking_ the vault in plain text, so that
I can run the playbook without having to ask you for the password.

# QUESTION A

Make a copy of the playbook from the previous examination, call it `09-mariadb-password.yml`
and modify it so that the task that sets the password is injected via an Ansible variable,
instead of as a plain text string in the playbook.

Svar:
Jag började med att kopierade förra playbooken och döpte kopian till 09-mariadb-config.yml 

Tog bort lösenordet i klartext från vars: i playbooken.

La till en hänvisning till en separat variabelfil med vars_files: på play-nivå.

Skapade filen vars/password.yml och la bara själva hemligheten där som variabeln db_pass.

Verifiering:

ansible-playbook 09-mariadb-config.yml --syntax-check → playbook: 09-mariadb-config.yml → vilket visar att syntaxen i playbooken är korrekt och att Ansible kunde läsa in filen utan problem.

ansible-playbook 09-mariadb-config.yml --check → Kör idempotent utan fel

Normal körning gav ok och changed=0 när allt redan var konfigurerat.

# QUESTION B

When the [QUESTION A](#question-a) is solved, use `ansible-vault` to store the password in encrypted
form, and make it possible to run the playbook as before, but with the password as an
Ansible Vault secret instead.

Svar:
Jag krypterat variabelfilen med Ansible Vault och visade hur man kör playbooken med --vault-password-file "ansible-playbook 09-mariadb-config.yml --vault-password-file .vault-pass.txt" så att allt fungerar utan att visa hemligheten i klartext.

Jag verifierade lösningen med --syntax-check, --check och normal körning; resultatet var idempotent och utan fel.