This description aims towards setting up a TEST environment with a Droplet with postgresql db and connecting to it from a local machine with PGadmin4, QGIS 3.0 and Notepad++. For further use of this test environment one should set up extra security.

1) Spin up Droplet, Set up Droplet, user and Add Public Key Authentication (optional - delete password login 
https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04. Jump step about ssh-copy-id eller cat to server and copy-paste content of public key instead 

2) Now you should be able to access the server from your local machine with putty or terminal. With Putty access with IP + user/pass og SSH access. With terminal write `SSH username@IP` (the first login ask for info).

3) Install nodejs og npm
https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04

4) Install postgresql
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-16-04

5) Install pgadmin på local windows

6) Prepare postgres for remote connection (OBS! no security steps are taking into consideration)
- On the server go to /etc/postgresql/9.1/main/ and `sudo nano pg_hba.conf` and insert at the buttom: host all all 0.0.0.0/0 md5. Save and exit.
- On the server go to /etc/postgresql/9.1/main/ and `sudo nano postgresql.conf` and replace `listen_addresses = 'localhost'` with `listen_addresses = '*'` Save and exit.

6.1) /etc/postgresql/9.1/main/pg_hba.conf (sudo nano pg_hba.conf) og indsæt nederst:
host all all 0.0.0.0/0 md5
 
Gem og exit
6.2) /etc/postgresql/9.1/main/pg_hba.conf (sudo nano pg_hba.conf) og indsæt/ændre til:
listen_addresses = '*' (UDEN # forrest)
 
Nu kan der connectes
