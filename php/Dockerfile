FROM docker.io/fedora

# Updating dependencies, installing Apache and PHP and cleaning dnf caches to reduce container size
RUN dnf -y update
RUN dnf -y install httpd
RUN dnf -y install php
RUN dnf clean all


# create working directory
RUN mkdir /container
RUN mkdir -p /container/app /container/bin
RUN chgrp -R apache /container

# set workdir
WORKDIR /container

# open port 80
EXPOSE 80

# custom httpd.conf
RUN rm /etc/httpd/conf/httpd.conf
ADD httpd.conf /etc/httpd/conf/httpd.conf

# add some files
ADD up.sh bin/up.sh

RUN chmod -v +x bin/up.sh

CMD ["bin/up.sh"]
