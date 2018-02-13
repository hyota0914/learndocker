FROM jenkins:2.60.3

USER root
RUN apt-get update \
    && apt-get install -y \
       apt-transport-https \
       ca-certificates \
       curl \
       gnupg2 \
       software-properties-common \
       sudo
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers

RUN curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | sudo apt-key add -
RUN add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
    $(lsb_release -cs) \
    stable"
RUN apt-get update \
    && apt-get install -y \
       docker-ce

RUN curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose; \
    chmod +x /usr/local/bin/docker-compose

COPY plugins.txt /usr/share/jenkins/ref/
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/ref/plugins.txt

USER jenkins

