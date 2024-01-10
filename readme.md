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

# Dancing

> *SMB* (Server Message Block) - communication
protocol provides shared access to files, printers, and serial ports between endpoints on a network  
> port **445 TCP**  
> most often used with **NetBIOS** over TCP/IP (**NBT**)


> Using the SMB protocol an application **can access files at a remote server**, along with other resources such as printers

## OSI model

1. Physical
1. Data Link
1. Network
1. Transport
1. Session
1. Presentation
1. Application

## Linux scripts

- change shell
  - chsh -s /bin/bash

## Research

- scan open ports
  - `nmap -sV {IP}`
  - open ports
    - 135/tcp open  msrpc         Microsoft Windows RPC
    - 139/tcp open  netbios-ssn   Microsoft Windows netbios-ssn
    - 445/tcp open  microsoft-ds?
  - OS info
    - Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
- install smb client
- connect to target machine
  - `smbclient -L {IP}`
    - `-L` - list shared resources
    - shown shares
        - ADMIN$          Disk      Remote Admin
        - C$              Disk      Default share
        - IPC$            IPC       Remote IPC
        - WorkShares      Disk
  - try shares
    - `smbclient \\\\{IP}\\ADMIN$`
  - download file
    - `get name`

# Redeemer

## Notes

> **Redis** (**RE**mote **DI**ctionary **S**erver) - 'in-memory' database.  
> NoSQL key-value data store used as a database, cache, and message broker.  
> Typically used to cache data that is frequently requested for quick retrieval

## Research

- scan open ports
  - `nmap -p- -sV {IP}`
    - `-p-` - scan all ports from 1 to 65535
  - open ports
    - 6379/tcp open  redis   Redis key-value store 5.0.7
  - install redis-cli
    - `apt install redis-tools`
  - connect to target machine
    - `redis-cli -h {IP}`
    - `info` - show statistics
      - `db0` - one database with index `0`
    - `select 0` - select database with index `0`
    - `keys *` - list all the keys in the database
      - "stor"
      - "temp"
      - "numb"
      - "flag"
    - `get {key}` - show value for the key
