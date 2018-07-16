This test setup aims towards setting up an docker environment with a Droplet with postgresql db /postgis and Cartodb and connecting to it from a local machine with PGadmin4, QGIS 3.0 and Notepad++. For further use of this test environment one should set up extra security.

1) Spin up Ubuntu 16 Droplet (https://www.digitalocean.com/). First time with droplet IP and user root and droplet password (sent to your mail).

2) Set up Droplet (use Putty or local terminal), user and Add Public Key Authentication (optional - delete password login https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04. I jumped the steps about ssh-copy-id eller cat to server and copy-paste content of public key (right-click on public key and open with txt editor) instead from C:/users/Username/.ssh, where the key is generated.

3) Now you should be able to access the server from your local machine with putty or terminal. With Putty access with IP + user/pass og SSH access. With terminal write SSH username@IP (the first login ask for info).

4) Now run docker container with this guide --> https://hub.docker.com/r/sverhoeven/cartodb/
What I did (Credit to sverhoeven in the link above):
- `sudo apt-get update`
- `apt install docker.io`
- `docker run -d -p 80:80 -h cartodb.localhost sverhoeven/cartodb`
- `docker run -d -p 80:80 -h <insert the Droplet IP> sverhoeven/cartodb`
- Wait a copule of minuts
- Go to `<Droplet IP>` in browser - CartoDB should be up and running
