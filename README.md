# To Start we will need an Ubuntu os and, install Docker, Docker-compose on Ubuntu with the following codes:

```
sudo apt update
Sudo apt upgrade
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add –
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt install docker-ce
Sudo apt install docker-compose
Installing MariaDB for client access:
Sudo apt install MariaDB-client

```

## The repository will be cloned from Zak’s github, with the following code:
git clone https://github.com/Zohan/maxscale-docker.git
after we will direct to maxscale directory. “ /maxscale/maxscale-docker/maxscale# “ and run the following command:


```
docker-compose build
docker-compose up -d
```
Starting maxscale_master1_1 ... done

Starting maxscale_master2_1 ... done

Starting maxscale_maxscale_1 ... done


###
Then we will edit the docker-compose.yml in maxscale directory:
nano docker-compose.yml
then we will edit the example.cnf file inside the maxscale.cnf.d file:
nano example.cnf
 
Now it is time to create our SQL shard files inside the master directory:
/maxscale/maxscale-docker/maxscale/sql/master#
Then we will nano the shard1.sql inside the directory and place the codes inside.
The same process will be done for shard2.sql inside master2 directory.
After creating this, we will stop all the containers and again run the following command to pull the new settings
Docker-compose up -d
After this we will list the servers with the following command:
docker-compose exec maxscale maxctrl list servers
####



To run maxctrl in the container to see the status of the cluster:
```
$ docker-compose exec maxscale maxctrl list servers
┌─────────┬─────────┬──────┬─────────────┬─────────────────┬──────────┐
│ Server  │ Address │ Port │ Connections │ State           │ GTID     │
├─────────┼─────────┼──────┼─────────────┼─────────────────┼──────────┤
│ server1 │ master  │ 3306 │ 0           │ Master, Running │ 0-3000-5 │
├─────────┼─────────┼──────┼─────────────┼─────────────────┼──────────┤
│ server2 │ slave1  │ 3306 │ 0           │ Slave, Running  │ 0-3000-5 │
├─────────┼─────────┼──────┼─────────────┼─────────────────┼──────────┤
│ server3 │ slave2  │ 3306 │ 0           │ Running         │ 0-3000-5 │
└─────────┴─────────┴──────┴─────────────┴─────────────────┴──────────┘

```
For connecting to DB:
mariadb -umaxuser -pmaxpwd -h 127.0.0.1 -P 4000

```

Refrences:
the repository was forked from Dr.Zak
the Readme.md file was edited from Dr.Zak
