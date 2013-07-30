ruci
====

Small utility for mass backup / restoring of OpenWrt routers configurations.

Dependencies
============

on local host: [hg | git] , uci

on both local and remote host: ssh, scp, tar

Getting uci for yourself is really easy:
(compilation is a breeze)

    uci git clone git://nbd.name/uci.git

...or simply redefine `getIpFromUciConfig()`

Usage
=====

```
 Usage: $0 push [-n] [-f|-q] [-w secs] [-i <host>] NAME [[-i <host>] NAME] ...
        $0 pull [-z] [-i <host>] NAME [[-i <host>] NAME] ...
        $0 confirm NAME [NAME] ...
        $0 status [-f] [-i <host>] NAME [[-i <host>] NAME] ...
 
 Manage remote uci configuration in NAME(s)
 
  -w, --wait NUM       After applying configuration, wait for NUM seconds
                     before reboot.
  -i, --ip HOST              Override the IP used for pull, push, status...
                     Applies only to the next NAME specified in command line.
  -n, --no-reboot    Prevent rebooting after pushing and applying configuration.
  -z, --gzip       Use gzip compression on incoming network traffic during pull.
                     Better perfomance on slow links, at the expense of high cpu load.
  -f, --full       Push (or check) whole /overlay instead of just /overlay/etc.
                     Increases network traffic = slower perfomance.
                     Useful to check for package installs or removals
                     or to push a complete overlay to a clean install of openwrt.
  -q, --quick      Push only a small subset of files in /etc that don't need reboot,
                     such as /etc/hosts. Implies -n, overrides -f.
```

