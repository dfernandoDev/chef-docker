# docker image build -t dfernando/ubuntu1604:chef .
# docker image build --rm=true --no-cache -t dfernando/ubuntu1604:chef .

FROM ubuntu:16.04

MAINTAINER Dinesh Fernando <dfernando@live.com>

ARG ubuntu_version=16.04
ARG chef_version=12.19.31
ARG chef_file=chef-server-core_${chef_version}-1_amd64.deb
ARG chef_url=https://packages.chef.io/files/stable/chef-server/12.19.31/ubuntu/16.04/${chef_file}

#RUN echo "chef-url = ${chef_url}"
#RUN echo "chef-file = ${chef_file}"

RUN apt-get clean all && \
	apt-get update && \
	apt-get install -y curl git htop mlocate net-tools openssh-client openssh-server procps upstart util-linux ntp && \
	rm -rf /var/lib/apt/lists/*

WORKDIR /root

RUN curl -O "${chef_url}"  && \
	dpkg -i "${chef_file}" && \
	rm "${chef_file}"

#CMD chef-server-ctl reconfigure

# docker run -it -p 443:443 --name chef-server --hostname chef-server.dfernando.com dfernando/ubuntu1604:chef bash
# docker run -d -p 443:443 --name chef-server --hostname chef-server.dfernando.com dfernando/ubuntu1604:chef