FROM nerdzeu/base

# Create vagrant user and group

RUN pacman-db-upgrade && \
    pacman --noconfirm -S openssh

RUN groupadd vagrant &&\
    useradd vagrant -g vagrant -G wheel -s /bin/bash&&\
    echo "vagrant:vagrant" | chpasswd &&\
    mkdir -pm 700 /home/vagrant/.ssh &&\
    wget --no-check-certificate 'https://raw.github.com/mitchellh/vagrant/master/keys/vagrant.pub' -O /home/vagrant/.ssh/authorized_keys &&\
    chmod 0600 /home/vagrant/.ssh/authorized_keys &&\
    chown -R vagrant /home/vagrant/.ssh && \
    ssh-keygen -A -q -t rsa -N '' && \
    echo "vagrant: ALL" >> /etc/hosts.allow && \
    echo "UsePAM no" > /etc/ssh/sshd_config

EXPOSE 22

ENTRYPOINT su - postgres -c 'pg_ctl -D /var/lib/postgres/data -l /dev/null start' && \
        /usr/bin/php-fpm --pid /run/php-fpm/php-fpm.pid && \
        /usr/bin/nginx -g 'pid /run/nginx.pid; error_log stderr;' && \
        /usr/bin/sshd -D && \
	sleep infinity