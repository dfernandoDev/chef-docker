# docker image build -t --rm dfernando/ubuntu1604:chefdk .

FROM ubuntu:16.04

MAINTAINER Dinesh Fernando <dfernando@live.com>

ARG ubuntu_version=16.04
ARG chef_version=3.8.14
ARG chef_file=chefdk_${chef_version}-1_amd64.deb
ARG chef_url=https://packages.chef.io/files/stable/chefdk/${chef_version}/ubuntu/${ubuntu_version}/${chef_file}

#RUN echo "chef-url = ${chef_url}"
#RUN echo "chef-file = ${chef_file}"

RUN apt-get clean && \
    apt-get update && apt-get install --no-install-recommends -y openssh-server less vim curl wget sudo && \
    rm -rf /var/lib/apt/lists/*

RUN useradd -ms /bin/bash dinesh && \
	adduser dinesh sudo

WORKDIR /home/dinesh

#RUN wget --no-check-certificate https://packages.chef.io/files/stable/chefdk/3.8.14/ubuntu/16.04/chefdk_3.8.14-1_amd64.deb

RUN curl -O "${chef_url}" && \
	chown -R dinesh:dinesh /home/dinesh && \
    dpkg -i "${chef_file}" && \
    rm "${chef_file}"

USER dinesh
RUN echo 'eval "$(chef shell-init bash)"' >> ~/.bash_profile

WORKDIR /home/dinesh/chef-repo

# docker run -it -v /Users/dinesh/Documents/simpli.fi/dev/dinesh_challenge:/home/dinesh/chef-repo dfernando/ubuntu1604 bash