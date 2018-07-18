This test setup aims towards setting up an docker environment with a Droplet with postgresql db /postgis and Cartodb and connecting to it from a local machine with PGadmin4, QGIS 3.0 and Notepad++. For further use of this test environment one should set up extra security.

1) Spin up Ubuntu 16 Droplet (https://www.digitalocean.com/). First time with droplet IP and user root and droplet password (sent to your mail).

2) Set up Droplet (use Putty or local terminal), user and Add Public Key Authentication (optional - delete password login https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04. I jumped the steps about ssh-copy-id eller cat to server and copy-paste content of public key (right-click on public key and open with txt editor) instead from C:/users/Username/.ssh, where the key is generated.

3) Now you should be able to access the server from your local machine with putty or terminal. With Putty access with IP + user/pass og SSH access. With terminal write SSH username@IP (the first login ask for info).

4) Now run docker container with this guide --> https://hub.docker.com/r/sverhoeven/cartodb/
What I did (Credit to sverhoeven in the link above):
- `sudo apt-get update`
- `apt install docker.io`
- `docker run -d -p 80:80 -h cartodb.localhost sverhoeven/cartodb`
- `docker stop <docker id>`
- `docker run -d -p 80:80 -h <insert the Droplet IP> sverhoeven/cartodb`
- Wait a copule of minuts
- Go to `<Droplet IP>` in browser - CartoDB should be up and running
- IMPORTANT! Persistent data with the following below (make setup so that data does not delete when container is rebooted). Ran all command from root directory:
- `docker create --name cartodb_pgdata sverhoeven/cartodb`
- Change to directory to save the Postgresql data dir (cartodb_pgdata) of the CartoDB image
-`docker cp cartodb_pgdata:/var/lib/postgresql $PWD/cartodb_pgdata`
-`docker rm -f cartodb_pgdata`
-  Inside container cartodb_pgdata is owned by postgres (uid=105 (NOW 103!)) user, it should be owned by same user on the local filesystem
-`sudo chown -R 105.105 $PWD/cartodb_pgdata` OBS! Default owner is changed on carto project so that postgresql owner in docker is now set to 103. So run `sudo chown -R 103.103 $PWD/cartodb_pgdata`. Check owner on docker by 1) starting `docker run -d -p 80:80 -h <insert the Droplet IP> sverhoeven/cartodb`, 2) run `docker exec -it <docker id>`, 3) go to var/lib and run `stat postgresql/`, 4) See owner Uid
- After this the CartoDB container will have a database that stays filled after restarts. The CartoDB container can be stop and started with 1) see docker alias with `docker ps`, 2) then run `docker stop <docker id>`
- Start container with restart policy `--restart always` with the following command `docker run --restart always -d -p 80:80 -h <insert the Droplet IP> -v $PWD/cartodb_pgdata:/var/lib/postgresql sverhoeven/cartodb`
#Redirect to https
- Go to container root with the command `docker exec -it <container id> bash`
- Install text editor nano with ´apt-get´ and then ´apt-get install nano´
- Follow guide https://www.digitalocean.com/community/tutorials/how-to-configure-nginx-with-ssl-as-a-reverse-proxy-for-jenkins for setting up https
