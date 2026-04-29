# A Dockerfile is a declarative configuration file used to define the process 
# of building a Docker image in a reproducible and automated way within the 
# Docker ecosystem. It's a image, like a template to create a container

# Containers must be built either from the penultimate stable
# version of Alpine or Debian
FROM    debian:bullseye

# Container will make this port available
# 3306 it's MariaDB & MySQL standard port
EXPOSE  3306

# Update the system
# Avoid installing unnecessary packages
# Clean caches and avoid unnecessary files in the image
RUN     apt update && \
        apt install -y --no-install-recommends --no-install-suggests \
        mariadb-server && \
        rm -rf /var/lib/apt/lists/*

# Copy the configuration to container
COPY    conf/50-server.cnf /etc/mysql/mariadb.conf.d/

# Copy the setup to container to container
COPY    tools/setup.sh /bin/
RUN     chmod +x /bin/setup.sh

# Run setup.sh script with mysql_safe (MySQL wrapper) as argument
CMD     ["setup.sh", "mysql_safe"]