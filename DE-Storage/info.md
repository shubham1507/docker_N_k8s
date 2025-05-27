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