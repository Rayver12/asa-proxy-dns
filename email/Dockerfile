FROM ubuntu:latest

RUN apt update -y
RUN apt upgrade -y

RUN apt install vim postfix dnsutils iputils-ping -y
RUN apt install dovecot-imapd dovecot-pop3d -y
RUN apt install syslog-ng -y

COPY main.cf /etc/postfix
COPY 10-auth.conf /etc/dovecot/conf.d/10-auth.conf
RUN useradd -c 'bob' -m bob
RUN useradd -c 'rafael' -m rafael
RUN useradd -c 'joao' -m joao
RUN useradd -c 'redes' -m redes
RUN echo "bob:redes" | chpasswd
RUN echo "rafael:redes" | chpasswd
RUN echo "joao:redes" | chpasswd
RUN echo "redes:redes" | chpasswd

CMD ["sh", "-c", "service syslog-ng start ; service postfix start ; service dovecot start ; tail -F /var/log/mail.log"]