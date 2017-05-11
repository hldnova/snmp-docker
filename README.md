# snmp-docker

Ubuntu Xenial based Docker image for SNMP trap receiver, together with other SNMP tools.

To start

    docker run docker run -d --name snmptrap-receiver -v $PWD/snmp:/var/log/snmp lidaheemc/docker-snmp
    
Send a test trap

    docker exec snmptrap-receiver snmptrap -v 1 -c public localhost .1.3.6.1.6.3 "" 0 0 coldStart.0
    tail $PWD/snmp/trap.log

Sample output

```
Received 39 byte packet from UDP: [127.0.0.1]:35522->[127.0.0.1]:162
0000: 30 25 02 01  00 04 06 70  75 62 6C 69  63 A4 18 06    0%.....public...
0016: 05 2B 06 01  06 03 40 04  AC 11 00 03  02 01 00 02    .+....@.........
0032: 01 00 43 01  00 30 00                                 ..C..0.

2017-05-11 18:54:37 114c0914a3d1 [172.17.0.3] (via UDP: [127.0.0.1]:35522->[127.0.0.1]:162) TRAP, SNMP v1, community public
        iso.3.6.1.6.3 Cold Start Trap (0) Uptime: 0:00:00.00
```
