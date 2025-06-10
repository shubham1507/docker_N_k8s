#Docker area, this is where data reside

docker volume ls

sudo ls -l /var/lib/docker/volumes/

total 24
brw------- 1 root root  8, 2 May 26 20:29 backingFsBlockDev
-rw------- 1 root root 32768 May 26 20:29 metadata.db

docker volume create nginx-data

docker volume inspect nginx-data

docker container run -d --name nginx-demo -v nginx-data:/usr/share/nginx/html -p 8090:80 nginx
docker container run -d --name nginx-demo -v nginx-data:/usr/share/nginx/html:ro -p 8090:80 nginx

----------------------------------

docker info => gives  Docker Root Dir: /var/snap/docker/common/var-lib-docker
volumes stores under this


sudo ls -l /var/snap/docker/common/var-lib-docker
[sudo] password for lenovo: 
total 64
drwx--x--x  5 root root  4096 Dec 10 21:57 buildkit
drwx--x--x  3 root root  4096 Dec 10 21:55 containerd
drwx--x---  2 root root  4096 May 29 10:47 containers
-rw-------  1 root root    36 Dec 10 21:55 engine-id
drwx------  3 root root  4096 Dec 10 21:55 image
drwxr-x---  3 root root  4096 Dec 10 21:55 network
drwx--x--- 20 root root 20480 May 29 10:47 overlay2
drwx------  4 root root  4096 Dec 10 21:55 plugins
drwx------  2 root root  4096 May 29 10:28 runtimes
drwx------  2 root root  4096 Dec 10 21:55 swarm
drwx------  2 root root  4096 May 29 10:29 tmp
drwx-----x  3 root root  4096 May 29 10:28 volumes
lenovo@snj:~/Documents/docker_N_k8s$ 

ALL VOLUMES will be located at /var/snap/docker/common/var-lib-docker/volumes

docker volume
docker volume ls
docker volume inspect dryrun-vol

ONCE THE VOL created NOW lets CREATE A CONTAINER and MAP A VOLUME TO IT

docker container run -d --name nginx-demo -v dryrun-vol:/usr/share/nginx/html -p 8090:80 nginx
root@snj:~# ls -l /var/snap/docker/common/var-lib-docker/volumes/dryrun-vol/_data
total 8
-rw-r--r-- 1 root root 497 Apr 16 17:31 50x.html
-rw-r--r-- 1 root root 615 Apr 16 17:31 index.html

1. IF WE UPDATE /var/snap/docker/common/var-lib-docker/volumes/dryrun-vol/_data/index.html

it will be reflected in dryrun-vol:/usr/share/nginx/html

2. ATTACH SINGLE VOL TO MULTI_CONTAINER

3. IF CNTR deleted VOLUME ASSOCIATED with persists

        enovo@snj:~$ docker container stop nginx-demo nginx-demo2
        nginx-demo
        nginx-demo2
        docker container rm nginx-demo nginx-demo2
        nginx-demo
        nginx-demo2
        docker volume ls
        DRIVER    VOLUME NAME
        local     dryrun-vol
        local     nginx-data
        lenovo@snj:~
        sudo  ls -l /var/snap/docker/common/var-lib-docker/volumes/dryrun-vol/_data
        [sudo] password for lenovo: (THIS SHOWS the VOL is still there)
        total 8
        -rw-r--r-- 1 root root 497 Apr 16 17:31 50x.html
        -rw-r--r-- 1 root root  35 May 29 12:32 index.html

4. MOUNT THE VOL TO CONTAINER AS READ ONLY

earlier

            docker container run -d --name nginx-demo2 -v dryrun-vol:/usr/share/nginx/html -p 9090:80 nginx
            84c785369ec2874142b666d0538b403f1926e3b9eb2f2c3a2fe0655bc612999c
            docker container exec -it nginx-demo2 bash
            root@84c785369ec2:/# cat /usr/share/nginx/html/index.html  
            <h1> ADDED NEW DATA to nginx </h1>
            root@84c785369ec2:/# echo "<h1> ADDED NEW DATA to nginx v2</h1>" > /usr/share/nginx/html/index.html
            root@84c785369ec2:/# 

WITH RO 

            docker container run -d --name nginx-demo_Read_Only -v dryrun-vol:/usr/share/nginx/html:ro -p 9191:80 nginx
                a548a0d53f348cda2db2fa7850e815fc17ee49e502121ff430f836532df8d226
                docker container exec -it nginx-demo_Read_Only bash
                root@a548a0d53f34:/# cat /usr/share/nginx/html/index.html
                <h1> ADDED NEW DATA to nginx v2</h1>
                root@a548a0d53f34:/# echo "<h1> ADDED NEW DATA to nginx v2</h1>" > /usr/share/nginx/html/index.html
                bash: /usr/share/nginx/html/index.html: Read-only file system
                root@a548a0d53f34:/# 

5. WHILE CREATING THE CONTAINER WE CAN CREATE VOLUME DYNAMICALLY

            docker volume ls
            DRIVER    VOLUME NAME
            local     dryrun-vol
            local     nginx-data
            docker container run -d --name dynamic-container -v dynamic-vol:/usr/share/nginx/html nginx
            387369dcab1ec50df7d32d1c641a8e89a2b75653deb91a9abe90f32eb7e72203
            docker volume ls
            DRIVER    VOLUME NAME
            local     dryrun-vol
            local     dynamic-vol
            local     nginx-data
            docker ps
            CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS             PORTS                                   NAMES
            387369dcab1e   nginx     "/docker-entrypoint.…"   10 seconds ago      Up 8 seconds       80/tcp                                  dynamic-container
            a548a0d53f34   nginx     "/docker-entrypoint.…"   About an hour ago   Up About an hour   0.0.0.0:9191->80/tcp, :::9191->80/tcp   nginx-demo_Read_Only
            84c785369ec2   nginx     "/docker-entrypoint.…"   About an hour ago   Up About an hour   0.0.0.0:9090->80/tcp, :::9090->80/tcp   nginx-demo2
            


6. DELETE VOL without DELETING ASSOCIATED CONTAINER

    we can remove only unused vol

    docker volume prune

========================================

UNDERSTANDING JENKNS DEPLOYMENT USING VOLUME MOUNT ARCH

1. Created a Jenkins container attached vol jenkins-data

docker container run -d --name jenkins-server -p 8090:8080 -v jenkins-data:/var/jenkins_home jenkins/jenkins:lts

2. Stop and delete 

docker container stop jenkins-server
jenkins-server
docker container rm  jenkins-server
jenkins-server
docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

3. check the vol 
docker volume ls
DRIVER    VOLUME NAME
local     jenkins-data


4. Recreate the new container with old vol
docker container run -d --name jenkins-server_bkp -p 8091:8080 -v jenkins-data:/var/jenkins_home jenkins/jenkins:lts

===========================

UNDERSTANDING THE BIND MOUNT sce 1

BIND mount

1. docker container run -d --name nginx-bind_mnt-demo -v /nginx-bind_mnt-data:/usr/share/nginx/html nginx
   docker container run -d --name nginx-bind_mnt-demo -v /<src>:<dst> nginx


=========================================

UNDERSTANDING JENKINS DEPLOYMENT USING BIND MNT

sudo mkdir -p /jenkins-data
sudo chown -R 1000:1000 /jenkins-data
sudo chmod -R 775 /jenkins-data

docker container run -d --name jenkins-server -v /jenkins-data:/var/jenkins_home -p8090:8080 jenkins/jenkins:lts


docker rm -f jenkins-server
sudo rm -rf /jenkins-data



docker container run -d --name jenkins-server -u root -v /jenkins-data:/var/jenkins_home -p8090:8080 jenkins/jenkins:lts
docker logs -f jenkins-server

==========================

DOCKER tmpfs mount => A cntnr where we are storing sensitive info and will be wiped off once the container restarted


docker container run -d --name nginx-tmpfs-demo --tmpfs /var/tmp nginx
61de74550c534e328a46a604afe790d7789a920dc4733e28faa6f2123e9acc20

docker container ps

CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS          PORTS                                                  NAMES
61de74550c53   nginx                 "/docker-entrypoint.…"   21 seconds ago   Up 19 seconds   80/tcp                                                 nginx-tmpfs-demo
780c31dc3906   jenkins/jenkins:lts   "/usr/bin/tini -- /u…"   38 minutes ago   Up 38 minutes   50000/tcp, 0.0.0.0:8090->8080/tcp, :::8090->8080/tcp   jenkins-server

docker exec -it nginx-tmpfs-demo bash

root@61de74550c53:/# cd /var/tmp
root@61de74550c53:/var/tmp# ls
root@61de74550c53:/var/tmp# touch file{1..5}
root@61de74550c53:/var/tmp# ls -l
total 0
-rw-r--r-- 1 root root 0 Jun  1 06:57 file1
-rw-r--r-- 1 root root 0 Jun  1 06:57 file2
-rw-r--r-- 1 root root 0 Jun  1 06:57 file3
-rw-r--r-- 1 root root 0 Jun  1 06:57 file4
-rw-r--r-- 1 root root 0 Jun  1 06:57 file5

docker container stop nginx-tmpfs-demo
nginx-tmpfs-demo
docker ps -a
docker exec -it nginx-tmpfs-demo bash
Error response from daemon: container 61de74550c534e328a46a604afe790d7789a920dc4733e28faa6f2123e9acc20 is not running
docker container start nginx-tmpfs-demo
nginx-tmpfs-demo
docker exec -it nginx-tmpfs-demo bash
root@61de74550c53:/# ls
bin   dev		   docker-entrypoint.sh  home  lib64  mnt  proc  run   srv  tmp  var
boot  docker-entrypoint.d  etc			 lib   media  opt  root  sbin  sys  usr
root@61de74550c53:/# cd var/tmp
root@61de74550c53:/var/tmp# ls
root@61de74550c53:/var/tmp# ls -l
total 0
root@61de74550c53:/var/tmp# 


docker container run -d --name nginx-mount_tmpfs-demo --mount type=tmpfs,dst=/var/tmp,tmpfs-size=1024,tmpfs-mode=700 nginx

====================================

POINTS TO REMEMBER WHILE USING STORAGE

====================================

IMPLEMENT DOCKER VOL WITH NFS SERVER

sudo apt install -y nfs-kernel-server

sudo chown -R nobody:nogroup /nfs-data/ 
ls -ld
drwxr-x--- 50 lenovo lenovo 4096 May 30 15:27 .
ls -ld /nfs-data/ 
drwxr-xr-x 2 nobody nogroup 4096 Jun  2 11:21 /nfs-data/
ls -l /nfs-data/ 
total 0

sudo vi /etc/exports
#add below line
/nfs-data 192.168.1.40(rw,sync,no_subtree_check,no_root_squash)

sudo exportfs -av
#exporting 192.168.1.40:/nfs-data

sudo systemctl restart nfs-kernel-server
sudo systemctl status nfs-kernel-server


docker container run -d --name jenkins-cicd --mount 'type=volume,src=jenkins-data,dst=/var/jenkins_home,volume-driver=local,volume-opt=type=nfs,volume-opt=device=:/nfs-data,"volume-opt=o=addr=192.168.1.50,rw,nfsvers=4,async"' jenkins/jenkins:lts


