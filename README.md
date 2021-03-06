# jailmanage

Manage FreeBSD jails


## Install

````
fetch -o /usr/local/sbin/jailmanage https://raw.githubusercontent.com/msimerson/jailmanage/master/jailmanage.sh
chmod 755 /usr/local/sbin/jailmanage
````


## Usage

````
$ ./jailmanage.sh 
   usage: ./jailmanage.sh [ jailname ]
    
   jailname also has several "special" jail names:

      all         - consecutively log into each jail 
      mergemaster - run mergemaster in each jail
      update      - run freebsd-update in each jail
      cleanup     - delete stale cached files
````

### Enter each jail

```sh
jailmanage all
```

### Upgrade FreeBSD version in every jail

```sh
jailmanage update
```

This runs a command like this command for each jail:

```sh
freebsd-update -b /jails/dns -f /jails/dns/etc/freebsd-update.conf install
```

If `jailmanage` detects that the jail is running an older major version of
FreeBSD than the host (ex: host is running 10.2 and jail is running 10.1),
then jailmanage will perform a binary upgrade of FreeBSD using these commands:  

```
freebsd-update -b /jails/dns -f /jails/dns/etc/freebsd-update.conf -r 10.2-RELEASE upgrade install
freebsd-update -b /jails/dns -f /jails/dns/etc/freebsd-update.conf install
freebsd-update -b /jails/dns -f /jails/dns/etc/freebsd-update.conf install
```

### Delete cached files

```
jailmanage cleanup
```

This command empties /var/cache/pkg and /var/db/freebsd-update in every jail.

