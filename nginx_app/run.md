docker build -t nginx-nonroot .


docker run -d -p 8090:8090 -v $(pwd)/html:/var/www/html nginx-nonroot
#Run Without Volume:
docker run -d -p 8090:8090 nginx-nonroot

