# handy-sshd
[![CI](https://github.com/nwtgck/handy-sshd/actions/workflows/ci.yml/badge.svg)](https://github.com/nwtgck/handy-sshd/actions/workflows/ci.yml)

Portable SSH Server

## Install on Ubuntu/Debian

```bash
wget https://github.com/nwtgck/handy-sshd/releases/download/v0.2.0/handy-sshd-0.2.0-linux-amd64.deb
sudo dpkg -i handy-sshd-0.2.0-linux-amd64.deb 
```

## Install on Mac

```bash
brew install nwtgck/handy-sshd/handy-sshd
```

Get more executables in [the releases](https://github.com/nwtgck/handy-sshd/releases).

## Examples

```bash
# Listen on 2222 and accept user name "john" with password "mypassword"
handy-sshd -p 2222 --user "john:mypassword"
```

```bash
# Listen on 2222 and accept user name "john" without password
handy-sshd -p 2222 --user "john:"
```

```bash
# Listen on 2222 and accept users "john" and "alice" without password
handy-sshd -p 2222 --user "john:" --user "alice:"
```

```bash
# Listen on unix domain socket
handy-sshd --unix-socket /tmp/my-unix-socket --user "john:"
```

## Permissions
**All permissions are allowed when nothing is specified.** There are some permissions.
* --allow-direct-tcpip
* --allow-execute
* --allow-sftp
* --allow-tcpip-forward

Specifying `--allow-direct-tcpip` and `--allow-execute` for example allows only them.
The log shows "allowed: " and "NOT allowed: " permissions as follows.

```console
$ handy-sshd --user "john:" --allow-direct-tcpip --allow-execute
2023/08/09 20:49:35 INFO listening on :2222...
2023/08/09 20:49:35 INFO allowed: "direct-tcpip", "execute"
2023/08/09 20:49:35 INFO NOT allowed: "tcpip-forward", "sftp"
```

## --help

```
Portable SSH server

Usage:
  handy-sshd [flags]

Flags:
      --allow-direct-tcpip    client can use local forwarding and SOCKS proxy
      --allow-execute         client can use shell/interactive shell
      --allow-sftp            client can use SFTP and SSHFS
      --allow-tcpip-forward   client can use remote forwarding
  -h, --help                  help for handy-sshd
      --host string           SSH server host (e.g. 127.0.0.1)
  -p, --port uint16           SSH server port (default 2222)
      --shell string          Shell
      --unix-socket string    Unix-domain socket
      --user stringArray      SSH user name (e.g. "john:mypassword")
  -v, --version               show version
```
