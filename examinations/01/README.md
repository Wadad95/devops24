# Examination 1 - Understanding SSH and public key authentication

Connect to one of the virtual lab machines through SSH, i.e.

    $ ssh -i deploy_key -l deploy webserver

Study the `.ssh` folder in the home directory of the `deploy` user:

    $ ls -ld ~/.ssh

Look at the contents of the `~/.ssh` directory:

    $ ls -la ~/.ssh/

## QUESTION A

What are the permissions of the `~/.ssh` directory?

Svar:
Rättigheterna är drwx------ (700), vilket betyder att bara användaren deploy har full åtkomst till mappen, medan andra användare inte har någon åtkomst.

Why are the permissions set in such a way?

Svar:
Det är för att skydda filerna i .ssh-mappen, som kan innehålla känsliga filer som privata nycklar. Om andra användare hade tillgång skulle det kunna innebära en säkerhetsrisk.

## QUESTION B

What does the file `~/.ssh/authorized_keys` contain?

Svar:
Den innehåller publika SSH-nycklar från andra datorer eller användare som är godkända att ansluta till den här användaren utan lösenord.

## QUESTION C

When logged into one of the VMs, how can you connect to the
other VM without a password?

Svar:
Jag kan använda ssh-keygen för att skapa en SSH-nyckel på den första VM:n, och sedan använda ssh-copy-id för att kopiera den publika nyckeln till den andra VM:n. Då kan jag ansluta med SSH utan att behöva skriva lösenord.

### Hints:

* man ssh-keygen(1)
* ssh-copy-id(1) or use a text editor

## BONUS QUESTION

Can you run a command on a remote host via SSH? How?

Svar:

Ja, jag kan skriva kommandot direkt efter SSH-kommandot, till exempel:
ssh deploy@192.168.121.42 ls -la
Det kör kommandot på fjärrmaskinen och visar resultatet i min terminal.