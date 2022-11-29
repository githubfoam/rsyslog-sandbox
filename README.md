# rsyslog-sandbox


~~~~
In that order

>vagrant up vg-rsyslog-01

vg-rsyslog-01: Executing: /lib/systemd/systemd-sysv-install enable rsyslog
    vg-rsyslog-01: Listening on TCP 1468
    vg-rsyslog-01: tcp     LISTEN   0        25               0.0.0.0:1468          0.0.0.0:*       users:(("rsyslogd",pid=11037,fd=8))
    vg-rsyslog-01: tcp     LISTEN   0        25                  [::]:1468             [::]:*       users:(("rsyslogd",pid=11037,fd=9))
    vg-rsyslog-01: Nov 29 05:51:15 debian-10 kernel: [   14.539054] IPv6: ADDRCONF(NETDEV_CHANGE): eth0: link becomes ready
    vg-rsyslog-01: Nov 29 05:51:17 debian-10 kernel: [   16.577303] IPv6: ADDRCONF(NETDEV_UP): eth1: link is not ready
    vg-rsyslog-01: Nov 29 05:51:17 debian-10 kernel: [   16.582007] e1000: eth1 NIC Link is Up 1000 Mbps Full Duplex, Flow Control: RX
    vg-rsyslog-01: Nov 29 05:51:17 debian-10 kernel: [   16.582240] IPv6: ADDRCONF(NETDEV_CHANGE): eth1: link becomes ready
    vg-rsyslog-01: Nov 29 05:51:17 debian-10 kernel: [   17.060164] vboxsf: g_fHostFeatures=0x8000000f g_fSfFeatures=0x1 g_uSfLastFunction=29
    vg-rsyslog-01: Nov 29 05:51:17 debian-10 kernel: [   17.060201] vboxsf: Successfully loaded version 6.1.32 r149290
    vg-rsyslog-01: Nov 29 05:51:17 debian-10 kernel: [   17.060218] vboxsf: Successfully loaded version 6.1.32 r149290 on 4.19.0-20-amd64 SMP mod_unload modversions  (LINUX_VERSION_CODE=0x413ff)
    vg-rsyslog-01: Nov 29 05:51:49 vg-rsyslog-01 rsyslogd:  [origin software="rsyslogd" swVersion="8.1901.0" x-pid="354" x-info="https://www.rsyslog.com"] exiting on signal 15.
    vg-rsyslog-01: Nov 29 05:51:49 vg-rsyslog-01 rsyslogd: imuxsock: Acquired UNIX socket '/run/systemd/journal/syslog' (fd 3) from systemd.  [v8.1901.0]
    vg-rsyslog-01: Nov 29 05:51:49 vg-rsyslog-01 rsyslogd:  [origin software="rsyslogd" swVersion="8.1901.0" x-pid="11037" x-info="https://www.rsyslog.com"] start


>vagrant up vg-rsyslog-02


    vg-rsyslog-01: Listening on TCP 1468
    vg-rsyslog-01: tcp     LISTEN   0        25               0.0.0.0:1468          0.0.0.0:*       users:(("rsyslogd",pid=11037,fd=8))
    vg-rsyslog-01: tcp     LISTEN   0        25                  [::]:1468             [::]:*       users:(("rsyslogd",pid=11037,fd=9))
    vg-rsyslog-01: Nov 29 05:51:15 debian-10 kernel: [   14.539054] IPv6: ADDRCONF(NETDEV_CHANGE): eth0: link becomes ready
    vg-rsyslog-01: Nov 29 05:51:17 debian-10 kernel: [   16.577303] IPv6: ADDRCONF(NETDEV_UP): eth1: link is not ready
    vg-rsyslog-01: Nov 29 05:51:17 debian-10 kernel: [   16.582007] e1000: eth1 NIC Link is Up 1000 Mbps Full Duplex, Flow Control: RX
    vg-rsyslog-01: Nov 29 05:51:17 debian-10 kernel: [   16.582240] IPv6: ADDRCONF(NETDEV_CHANGE): eth1: link becomes ready
    vg-rsyslog-01: Nov 29 05:51:17 debian-10 kernel: [   17.060164] vboxsf: g_fHostFeatures=0x8000000f g_fSfFeatures=0x1 g_uSfLastFunction=29
    vg-rsyslog-01: Nov 29 05:51:17 debian-10 kernel: [   17.060201] vboxsf: Successfully loaded version 6.1.32 r149290
    vg-rsyslog-01: Nov 29 05:51:17 debian-10 kernel: [   17.060218] vboxsf: Successfully loaded version 6.1.32 r149290 on 4.19.0-20-amd64 SMP mod_unload modversions  (LINUX_VERSION_CODE=0x413ff)
    vg-rsyslog-01: Nov 29 05:51:49 vg-rsyslog-01 rsyslogd:  [origin software="rsyslogd" swVersion="8.1901.0" x-pid="354" x-info="https://www.rsyslog.com"] exiting on signal 15.
    vg-rsyslog-01: Nov 29 05:51:49 vg-rsyslog-01 rsyslogd: imuxsock: Acquired UNIX socket '/run/systemd/journal/syslog' (fd 3) from systemd.  [v8.1901.0]
    vg-rsyslog-01: Nov 29 05:51:49 vg-rsyslog-01 rsyslogd:  [origin software="rsyslogd" swVersion="8.1901.0" x-pid="11037" x-info="https://www.rsyslog.com"] start
    vg-rsyslog-01: Nov 29 05:58:14 vg-rsyslog-02 rsyslogd[6790]: [origin software="rsyslogd" swVersion="8.2102.0-10.el8" x-pid="6790" x-info="https://www.rsyslog.com"] exiting on signal 15.
    vg-rsyslog-01: Nov 29 05:58:14 vg-rsyslog-02 rsyslogd[32356]: [origin software="rsyslogd" swVersion="8.2102.0-10.el8" x-pid="32356" x-info="https://www.rsyslog.com"] start
    vg-rsyslog-01: Nov 29 05:58:14 vg-rsyslog-02 rsyslogd[32356]: imjournal: journal files changed, reloading...  [v8.2102.0-10.el8 try https://www.rsyslog.com/e/0 ]
    vg-rsyslog-01: Nov 29 05:58:14 vg-rsyslog-02 vagrant[32380]: Test message from the system vg-rsyslog-02
    vg-rsyslog-01: Nov 29 05:58:17 vg-rsyslog-02 rsyslogd[32356]: action 'action-8-builtin:omfwd' suspended (module 'builtin:omfwd'), retry 0. There should be messages before this one giving the reason for suspension. [v8.2102.0-10.el8 try https://www.rsyslog.com/e/2007 ]
    vg-rsyslog-01: Nov 29 05:58:20 vg-rsyslog-02 rsyslogd[32356]: action 'action-8-builtin:omfwd' suspended (module 'builtin:omfwd'), next retry is Tue Nov 29 05:58:50 2022, retry nbr 0. There should be messages before this one giving the reason for suspension. [v8.2102.0-10.el8 try https://www.rsyslog.com/e/2007 ]


    vg-rsyslog-01: Nov 29 05:58:14 vg-rsyslog-02 vagrant[32380]: Test message from the system vg-rsyslog-02
~~~~
