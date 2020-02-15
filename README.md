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

## Start Tor

```bash
# tor
```

SOCKS5 available on 127.0.0.1:9050
