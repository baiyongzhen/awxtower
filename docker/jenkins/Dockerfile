FROM jenkins/jenkins:lts

USER root
#
# DOCKER INSTALLATION FOR DEBIAN
#
RUN curl -fsSL https://get.docker.com -o get-docker.sh && \
sh get-docker.sh
# RUN usermod -aG docker jenkins

#
# Misc. Tools INSTALLATION
# Python 2, 3 and respective modules,
# jq
#
RUN apt-get update && apt-get install -y python-pip \
 	&& apt-get install -y python3 python3-setuptools \
	&& apt install -y python3-pip \
	&& pip3 install requests \
	&& pip3 install six \
	&& apt-get install -y python-yaml jq \
    && rm -rf /var/lib/apt/lists/*

#
# Jenkins plugins
#
RUN /usr/local/bin/install-plugins.sh \
  windows-slaves \
  matrix-auth \
  matrix-project \
  antisamy-markup-formatter \
  script-security \
  pipeline-model-declarative-agent \
  pipeline-stage-step \
  pipeline-input-step \
  slack \
  git \
  blueocean \
  ansible-tower

COPY ref /usr/share/jenkins/ref

USER jenkins
ENV JENKINS_USER admin
ENV JENKINS_PASS admin

#
# Skip initial setup
#
ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false