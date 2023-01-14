# 1password-linux


### Instalation missing key

```
curl -sS https://downloads.1password.com/linux/keys/1password.asc | gpg --import
```



### Connection issue 

```
[ERROR] ..... Couldn't connect to the sign-in address you provided. Check the address and your network connection, then try again.
```

Software that relies on glibc's `getaddrinfo` (or similar) will work out of the box, since, by default, `/etc/nsswitch.conf` is configured to use `nss-resolve` if it is available.

To provide domain name resolution for software that reads `/etc/resolv.conf` directly, such as web browsers and GnuPG, systemd-resolved has four different modes for handling the file—stub, static, uplink and foreign. They are described in `systemd-resolved` § /ETC/RESOLV.CONF. We will focus here only on the recommended mode, i.e. the stub mode which uses /run/systemd/resolve/stub-resolv.conf.

`/run/systemd/resolve/stub-resolv.conf` contains the local stub `127.0.0.53` as the only DNS server and a list of search domains. This is the recommended mode of operation that propagates the systemd-resolved managed configuration to all clients. To use it, replace /etc/resolv.conf with a symbolic link to it:

```
ln -rsf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf
```

https://wiki.archlinux.org/title/Domain_name_resolution

