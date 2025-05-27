FROM ubuntu:22.04
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y nginx netbase
COPY --chown=www-data:www-data demo.html index.html /usr/share/nginx/html/
COPY --chown=www-data:www-data demo.html index.html /var/www/html/
EXPOSE 80
ENTRYPOINT [ "nginx", "-g"]
CMD [ "daemon off;" ]



# lenovo@snj:~/Documents/docker_N_k8s$ docker image history ubuntu:22.04
# IMAGE          CREATED       CREATED BY                                      SIZE      COMMENT
# c42dedf797ba   3 weeks ago   /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B        
# <missing>      3 weeks ago   /bin/sh -c #(nop) ADD file:59e67123ba6a5d9ee…   77.9MB    
# <missing>      3 weeks ago   /bin/sh -c #(nop)  LABEL org.opencontainers.…   0B        
# <missing>      3 weeks ago   /bin/sh -c #(nop)  LABEL org.opencontainers.…   0B        
# <missing>      3 weeks ago   /bin/sh -c #(nop)  ARG LAUNCHPAD_BUILD_ARCH     0B        
# <missing>      3 weeks ago   /bin/sh -c #(nop)  ARG RELEASE                  0B        
# lenovo@snj:~/Documents/docker_N_k8s$ 


# FROM, RUN, LABEL, ENV, ARG, EXPOSE, COPY and ADD, ENTRYPOINT and CMD, SHELL and WORKDIR
# STOPSIGNAL and HEALTHCHECK, 
# docker volume ls
# docker container logs <container_name>
