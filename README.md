# snmp-docker

Ubuntu Xenial based Docker image for SNMP trap receiver, together with other SNMP tools.

To start

    docker run -d -p 162:162/udp --name snmptrap-receiver -v $PWD/snmp:/var/log/snmp lidaheemc/docker-snmp
    
Send a test trap

    docker exec snmptrap-receiver snmptrap -v 1 -c public localhost .1.3.6.1.6.3 "" 0 0 coldStart.0
    tail $PWD/snmp/trap.log

Sample output

```
2017-05-11 18:54:37 114c0914a3d1 [172.17.0.3] (via UDP: [127.0.0.1]:35522->[127.0.0.1]:162) TRAP, SNMP v1, community public
        iso.3.6.1.6.3 Cold Start Trap (0) Uptime: 0:00:00.00
```
