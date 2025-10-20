# Examination 7 - MariaDB installation

To make a dynamic web site, many use an SQL server to store the data for the web site.

[MariaDB](https://mariadb.org/) is an open-source relational SQL database that is good
to use for our purposes.

We can use a similar strategy as with the _nginx_ web server to install this
software onto the correct host(s). Create the playbook `07-mariadb.yml` with this content:

    ---
    - hosts: db
      become: true
      tasks:
        - name: Ensure MariaDB-server is installed.
          ansible.builtin.package:
            name: mariadb-server
            state: present07

# QUESTION A

Make similar changes to this playbook that we did for the _nginx_ server, so that
the `mariadb` service starts automatically at boot, and is started when the playbook
is run.

Svar:
När man installerar en server (t.ex. MariaDB) räcker det inte att bara installera paketet.
Man måste också:

Starta tjänsten direkt (så att den börjar köra nu).

Aktivera den vid boot (så att den startar automatiskt när servern startas om).
I playbooken görs det med:

ansible.builtin.service:
  name: mariadb
  state: started        # ser till att tjänsten är igång just nu   
  enabled: true         # ser till att tjänsten startar automatiskt vid systemstart (boot)


# QUESTION B

When you have run the playbook above successfully, how can you verify that the `mariadb`
service is started and is running?

Svar:
systemctl status mariadb
systemctl is-active mariadb    # ska visa "active"
systemctl is-enabled mariadb   # ska visa "enabled"
ps aux | grep -i mariadb       #visar processen mariadbd (PID 16470) som körs
ss -ltnp   | grep 3306         #visar att port 3306 lyssnar.  

Det bevisar att tjänsten är igång och nåbar.”


# BONUS QUESTION

How many different ways can use come up with to verify that the `mariadb` service is running?

Svara:
Det finns flera olika sätt att verifiera att mariadb kör:

systemctl status mariadb – visar status.

systemctl is-active / is-enabled – visar om tjänsten är aktiv och startar vid boot.

ps aux | grep -i mariadb – visar processen.

ss -ltnp | grep 3306 – visar om porten lyssnar.

mysqladmin ping eller mariadb -e "SELECT 1;" – testar funktion.

journalctl -u mariadb – kolla loggar.

Kolla socketfilen /var/lib/mysql/mysql.sock.
