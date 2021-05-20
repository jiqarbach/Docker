FROM ubuntu
ENV DEBIAN_FRONTEND noninteractive
RUN apt update
RUN apt install curl openssh-server ca-certificates postfix tzdata -y 
RUN curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash
RUN apt install gitlab-ce -y
WORKDIR /etc/gitlab
RUN mkdir -p /etc/gitlab/ssl/
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-selfsigned.key\
 -out /etc/ssl/certs/nginx-selfsigned.crt -subj "/C=MR/ST=KHOURIBGA/L=KHOURIBGA/O=1337/OU=1337/CN=0.0.0.0"
RUN openssl dhparam -out /etc/gitlab/ssl/dhparams.pem 2048
RUN chmod 600 /etc/gitlab/ssl/*
RUN echo "external_url 'https://0.0.0.0/'" >> gitlab.rb
RUN echo "nginx['redirect_http_to_https'] = true\nnginx['ssl_certificate'] = \"/etc/ssl/certs/nginx-selfsigned.crt\"\nnginx['ssl_certificate_key'] = \"/etc/ssl/private/nginx-selfsigned.key\"\nnginx['ssl_dhparam'] = \"/etc/gitlab/ssl/dhparams.pem\"" >> gitlab.rb
EXPOSE 22 443
ENTRYPOINT  ((/opt/gitlab/embedded/bin/runsvdir-start &) && service ssh start && gitlab-ctl reconfigure && (gitlab-ctl tail))
