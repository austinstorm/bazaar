# Pull base image.
FROM ubuntu:14.04

# Install.
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential && \
  apt-get install -y software-properties-common && \
  apt-get install -y byobu curl git htop man unzip vim wget && \
  rm -rf /var/lib/apt/lists/*
  
RUN echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    useradd -u 5001 -G users,sudo -d /home/user --shell /bin/bash -m user && \
    echo "secret\nsecret" | passwd user && apt-get clean

RUN usermod -u 1000 user

USER user

EXPOSE 4200

ENV CODENVY_WEB_SHELL_PORT 4200

# Define default command.
CMD ["bash"]

EXPOSE 8000
ENV CODENVY_APP_PORT_8000_HTTP 8000

RUN mkdir /tmp/application /home/user/application

VOLUME ["/home/user/application"]

ENV CODENVY_APP_BIND_DIR /home/user/application

# ADD $app$/requirements.txt /tmp/application/requirements.txt

#RUN cd /tmp/application && \
#     sudo virtualenv /env && \
#     sudo /env/bin/pip install -r requirements.txt

# Make the terminal... non-interactive?
ENV DEBIAN_FRONTEND noninteractive

# 1. Update permissions recursively
# 2. Make newly created files accessible for anyone
# 3. Start application
  CMD sudo chmod a+rw -R /home/user/application/ && \
    umask 0 && \
    sudo bash /home/user/application/scripts/bootstrap.sh