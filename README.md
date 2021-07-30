# unbound

## Logging in Unboud:

    mkdir -p /var/log/unbound
    chown unbound:unbound /var/log/unbound
    touch /var/log/unbound/unbound.log
    chown unbound:unbound /var/log/unbound/unbound.log


## AppArmor
[AppArmor](https://www.apparmor.net/) - Linux kernel security module
 
Stil problem with "error: Could not open logfile /var/log/unbound/unbound.log: Permission denied"
So to fix the issue, we have to edit the settings:
    
    vim /etc/apparmor.d/local/usr.sbin.unbound

Add this line (Here you should write a path to your "unbound.log" file. ):
    
    # Site-specific additions and overrides for usr.sbin.unbound.<br>
    # For more details, please see /etc/apparmor.d/local/README.<br>
    /var/log/unbound/unbound.log rw,`

Reload apparmor config and restart unbound services:
    
    apparmor_parser -r /etc/apparmor.d/usr.sbin.unbound 
    service unbound restart

