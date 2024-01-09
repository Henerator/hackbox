FROM ubuntu:24.04

# update and install packages
RUN apt-get update \
  && apt-get install -y iputils-ping \
  && apt-get install -y openvpn \
  && apt-get install -y nmap \
  && apt-get install -y telnet \
  && apt-get install -y lftp \
  && apt-get install -y smbclient \
  && rm -rf /var/lib/apt/lists/*

COPY /scripts/ /scripts/

# patch ipv6 support
RUN /scripts/patch-sysctl-ipv6.sh

# connect to vpn on startup
ENTRYPOINT ["sh", "/scripts/connect-to-vpn.sh"]
