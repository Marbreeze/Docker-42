# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Dockerfile                                         :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: mstratu <marvin@42.fr>                     +#+  +:+       +#+         #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2019/09/30 14:52:09 by mstratu           #+#    #+#              #
#    Updated: 2019/09/30 15:03:01 by mstratu          ###   ########.fr        #
#                                                                              #
# **************************************************************************** #


FROM debian:latest


RUN DEBIAN_FRONTEND=noninteractive \
		apt-get update -y && \
		apt-get upgrade -y && \
		apt-get install bzip2 -y && \
		apt-get install apt-utils -y && \
		apt-get autoremove -y && \
    	apt-get clean

# Sets the TeamSpeak Version to download as an ENV variable

ENV TSV=3.0.13.8


# Download and install TeamSpeak 3 at root ./
# http://dl.4players.de/ts/releases/3.0.13.8/teamspeak3-server_linux_amd64-3.0.13.8.tar.bz2

ADD http://dl.4players.de/ts/releases/${TSV}/teamspeak3-server_linux_amd64-${TSV}.tar.bz2 ./

# 1. Uses the tar tool to -x extract -f the file in -j c mode with bzip2(1)
#    refer to man tar
# 2. Moves the teamspeak folder to the linux add-on packages directory /opt
#    refer to https://www.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/opt.html
# 3. Removes the teamspeak.tar.bz2 file since it's not needed anymore.
#

RUN tar jxf teamspeak3-server_linux_amd64-$TSV.tar.bz2 && \
	mv teamspeak3-server_linux_amd64 /opt/teamspeak && \
	rm teamspeak3-server_linux_amd64-$TSV.tar.bz2

# Add the start script to run the server

ADD ./start_server /start_server

### Difference between tcp and udp
# There are two types of Internet Protocol (IP) traffic. They are TCP or
# Transmission Control Protocol and UDP or User Datagram Protocol. TCP is
# connection oriented – once a connection is established, data can be sent
# bidirectional. UDP is a simpler, connectionless Internet protocol. Multiple
# messages are sent as packets in chunks using UDP.
#
# UDP is suitable for applications that need fast, efficient transmission,
# such as games. UDP's stateless nature is also useful for servers that answer
# small queries from huge numbers of clients.
#
# 9987 default voice
# 10011 server query
# 30033 file transport

EXPOSE 10011
EXPOSE 30033
EXPOSE 9987/udp

# Grant permissions to /start_server

RUN chmod 777 /start_server && \
	useradd teamspeak && \
	mkdir /data && \
	chown teamspeak:teamspeak /data

# Create the volume that will hold all data and

VOLUME ["/data"]
USER teamspeak
CMD [ "/start_server" ]

