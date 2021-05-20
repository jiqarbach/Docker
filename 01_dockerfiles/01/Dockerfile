FROM debian
ENV TS3SERVER_LICENSE=accept
RUN su root
RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install wget -y
RUN apt-get install bzip2
RUN wget http://dl.4players.de/ts/releases/3.13.2/teamspeak3-server_linux_amd64-3.13.2.tar.bz2
RUN tar -xvf teamspeak3-server_linux_amd64-3.13.2.tar.bz2
RUN rm -f teamspeak3-server_linux_amd64-3.13.2.tar.bz2
EXPOSE 9987/udp 10011/tcp 30033/tcp
WORKDIR teamspeak3-server_linux_amd64
ENTRYPOINT sh ts3server_minimal_runscript.sh start
