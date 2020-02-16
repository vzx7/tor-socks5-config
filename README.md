### TOR configuration as SOCKS5 proxy

## Install Tor
```bash
# pacman -S tor
```
## Add configuration

```bash
#/etc/tor/torrc

SOCKSPort 9050
ControlPort 9051
CookieAuthentication 1
ExitPolicy reject *:*                             # don't change this unless you really know what you are doing
ExcludeExitNodes {ru},{by},{cn}                   # Exclude unwanted regions for proxies
### Performance ###
AvoidDiskWrites 1                                 ## SSD wear reduction
DisableAllSwap 1                                  ## tor.service must be running as root
HardwareAccel 1                                   ## Using OpenSSL Hardware Support
NumCPUs 2                                         ## Running in two threads
```

## Start Tor as root

```bash
# Execute as root
tor
```

SOCKS5 available on 127.0.0.1:9050

## Start Tor as  [chroot](https://en.wikipedia.org/wiki/Chroot) (recommended)


```bash
# Let's give execution privileges for torchroot-setup.sh
chmod u+x torchroot-setup.sh

# Execute the script torchroot-setup.sh
./torchroot-setup.sh
```

Need to fix the configuration /opt/torchroot/etc/tor/torrc

**DisableAllSwap  0**

And finally, we start

```bash
chroot --userspec=tor:tor /opt/torchroot /usr/bin/tor
```

## Conclusion

This configuration only works as a proxy through the tor network. If you want to run the full tor node, you need to expand ExitPolicy, as well as other parameters. 
[Documentation](https://2019.www.torproject.org/docs/documentation.html)
