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

# Fawn

> **FTP** (File Transfer Protocol) is a standard communication protocol used to transfer
> computer files from a server to a client on a computer network. FTP is built on a
> client–server model architecture using separate control and data connections between
> the client and the server. FTP users may authenticate themselves with a clear-text
> sign-in protocol, generally in the form of a username and password.
> **However, they can connect anonymously** if the server is configured to allow it. For secure transmission
> that protects the username and password and encrypts the content, FTP is often secured
> with SSL/TLS (FTPS) or replaced with SSH File Transfer Protocol (SFTP).

> **FTPS** - encrypted FTP with SSL/TLS

> **SFTP** - encrypted FTP with SSH-tunneling

> typical misconfiguration for running FTP services allows an anonymous account
> to access the service like any other authenticated user

> By having ports, you can have one IP address handling multiple
services, as it adds another layer of distinction

- scan open ports
  - `21` - FTP
- install ftp client (`lftp`)
- connect to the server `lftp {IP}`
  - response code `230` - the server sends a 230 code in response to a command that has provided sufficient credentials to the server to grant the user access to the FTP server
- user `anonymous` user name
- use `get` command to download file
