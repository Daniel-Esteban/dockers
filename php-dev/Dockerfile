FROM docker.io/fedora

ENV PATH /container/bin:$PATH
ENV TERM xterm-256color

# Updating dependencies, installing Apache and cleaning dnf caches to reduce container size
RUN dnf -y update
RUN dnf -y install httpd
RUN dnf -y install php
RUN dnf -y install zsh
RUN dnf -y install git
RUN dnf -y install vim
RUN dnf clean all

RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# create working directory
RUN mkdir /container
RUN mkdir -p /container/app /container/bin
RUN chgrp -R apache /container

# set workdir
WORKDIR /container

# open port 80
EXPOSE 80

# custom .zshrc
RUN mv /root/.zshrc /root/.zshrc.old
ADD .zshrc /root/.zshrc

# custom httpd.conf
RUN mv /etc/httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf.old
ADD httpd.conf /etc/httpd/conf/httpd.conf

# add some files
ADD up.sh bin/up.sh
ADD README.md README.md


RUN chmod -v +x bin/up.sh

CMD ["bin/up.sh"]
