This test setup aims towards setting up an environment with a Droplet with postgresql db and connecting to it from a local machine with PGadmin4, QGIS 3.0 and Notepad++. For further use of this test environment one should set up extra security.

1) Spin up Ubuntu 16 Droplet (https://www.digitalocean.com/). First time with droplet IP and user `root` and droplet password (sent to your mail).

2) Set up Droplet (use Putty or local terminal), user and Add Public Key Authentication (optional - delete password login 
https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04. I jumped the steps about ssh-copy-id eller cat to server and copy-paste content of public key (right-click on public key and open with txt editor) instead from C:/users/Username/.ssh, where the key is generated.

3) Now you should be able to access the server from your local machine with putty or terminal. With Putty access with IP + user/pass og SSH access. With terminal write `SSH username@IP` (the first login ask for info).

4) Install nodejs og npm (I only used the first step "How To Install the Distro-Stable Version for Ubuntu")
https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04

5) Install postgresql (I stoped the tutorial at "Create and Delete Tables")
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-16-04

6) Install pgadmin på local windows

7) Prepare postgres for remote connection (OBS! no security steps are taking into consideration)
- On the server go to /etc/postgresql/9.1/main/ and `sudo nano pg_hba.conf` and insert at the buttom `host all all 0.0.0.0/0 md5`. Save and exit.
- On the server go to /etc/postgresql/9.1/main/ and `sudo nano postgresql.conf` and replace `#listen_addresses = 'localhost'` with `listen_addresses = '*'` Save and exit.

8) End by restarting postgresql with the commmand `sudo service postgresql restart`

9) If necessary open relevant port (in this case default port 5432) in windows firewall (remeber security aspects...)
http://www.tomshardware.co.uk/faq/id-3114787/open-firewall-ports-windows.html

10) Install Postgis Extention on PostgreSQL: 
https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-postgis-on-ubuntu-14-04

11) Remote connect with PGadmin4 with droplet IP, the created user and password. If connectiong fails on authentification then go to login to server, connect to postgress with `sudo -u postgres psql` and run query `CREATE USER myuser WITH ENCRYPTED PASSWORD 'secret';`

12) For easier file editing download Notepad ++ and connect with SFTP by:
- Install plugin `NppFTP`
- Run `Show NppFTP Window` --> run `Profile Setting`
- Add new profile
- Insert following settings
      - Hostname: Droplet IP
      - Connection type: SFTP
      - Port: 22
      - username: Created user or root
      - password: Created pass for user
      - Uncheck "Ask for password"
      - Close and connect to profile
      - If all folders does not show double-click on the "folder" `\`
      
   
