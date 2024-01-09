FROM alpine:3.18.5

# update packages
RUN apk update

# install openvpn
RUN apk add --update --no-cache openvpn

# install nmap and dependencies
RUN apk add --update --no-cache nmap
RUN apk add --update --no-cache nmap-scripts

# install packages set with
# - telnet
RUN apk add --update --no-cache busybox-extras

COPY /scripts/ /scripts/

# patch ipv6 support
RUN chmod +x /scripts/patch-sysctl-ipv6.sh
RUN /scripts/patch-sysctl-ipv6.sh

# connect to vpn on startup
ENTRYPOINT ["sh", "/scripts/connect-to-vpn.sh"]
