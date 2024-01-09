# Setup Docker VM

- use alpine image
- install openvpn package
- set `privileged` mode for container
- set `stdin_open` mode for container
- set `tty` mode for container
- patch `/etc/sysctl.conf` file to support ipv6
- restart sysctl `sysctl -p`
- conect to vpn

# Meow

- ping target machine
- install `nmap`
  - nmap = network mapper
- install `nmap-scripts`
- install `telnet`
  - use busybox-extras
  - [documentation](https://techviewleo.com/how-to-install-telnet-on-alpine-linux/)
- scan target machine
  - run `nmap -sV {IP}`
    - `V` - show versions
  - `telnet` - remote management of other hosts on the network
  - telnet port = `23`
- try telnet connection
  - run `telnet {IP}`
  - typical user names
    - admin
    - root
