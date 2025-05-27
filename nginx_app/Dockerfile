# Base Image
FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Install Nginx
RUN apt-get update && \
    apt-get install -y nginx && \
    rm -rf /var/lib/apt/lists/*

# Create non-root user
RUN groupadd -r nginxuser && useradd -r -g nginxuser nginxuser

# Create and fix permissions for directories needed by Nginx
RUN mkdir -p /var/www/html /var/lib/nginx /var/log/nginx /run/nginx /tmp && \
    chown -R nginxuser:nginxuser /var/www/html /var/lib/nginx /var/log/nginx /run/nginx /tmp

# Update default site to use port 8090
RUN sed -i 's/80 default_server/8090 default_server/' /etc/nginx/sites-available/default && \
    sed -i 's|root /var/www/html;|root /var/www/html;|' /etc/nginx/sites-available/default

# Update nginx.conf to set pid file in /tmp and access log in /var/log/nginx
RUN sed -i 's|pid /run/nginx.pid;|pid /tmp/nginx.pid;|' /etc/nginx/nginx.conf && \
    sed -i 's|access_log /var/log/nginx/access.log;|access_log /var/log/nginx/access.log;|' /etc/nginx/nginx.conf && \
    sed -i 's|error_log /var/log/nginx/error.log;|error_log /var/log/nginx/error.log;|' /etc/nginx/nginx.conf

# Add custom index.html
RUN echo 'Welcome to Nginx deployment on host: ubuntunginxserver' > /var/www/html/index.html

# Expose port 8090
EXPOSE 8090

# Set working directory
WORKDIR /var/www/html

# Switch to non-root user
USER nginxuser

# Start Nginx
CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
