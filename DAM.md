**statuproject**

#### **Set network on guardium**

1. ```
   1. On the central manager, set the IP mode to IPv4 by running the CLI command **store system ipmode ipv4**.
   
      **Important:** Do not restart the network until you complete step [2](https://www.ibm.com/docs/en/guardium/11.1?topic=modes-enable-ipv4#task_z3h_dtb_cjb__setup_ipv4).
   
   2. Set up IPv4 by running the following CLI commands.
   
      1. **store system hostname <hostname>**
   
         Where <hostname> can be resolved by the DNS for IPv4 addresses.
   
      2. **store system domain <domain name>**
   
         Where <domain> is the domain name of your network.
   
      3. **store network interface ip <IP address>**
   
         Where <IP address> is the primary IPv4 address of your Guardium system in Classless Inter-Domain Routing (CIDR) notation. For example, `store network interface ip 9.70.145.77/24`.
   
      4. **store network routes defaultroute <IP address>**
   
         Where <IP address> is the IPv4 address of the default router.
   
      5. **store network resolvers <IP address>**
   
         Where IP address is one or more IPv4 addresses for your DNS servers.
   
   3. Restart the network configuration by running the CLI command **restart network**.
   ```

**license activate on cm and Collector**

```tex
login to CM
https://192.168.73.160:8443
and go to license and active CM license then active db product key

Login to Collector
https192.168.73.161:8443
and go to license and active Colectorlicense then active db product 
```



**trust betwen servers**

```
 On collectors and CM and aggregator
# store system shared secret 123
```

**on Central manager**

```
store unit type manager

```



**install package on database****

```
yum install perl

yum install net-tools

yum install perl-version perl-Data-Dumper

```

**download stap & gim**

```
https://www.ibm.com/support/fixcentral
```

**on centos Database**

```bash
1- copy gim & gim.sh on centos server

2- chmod +x guard-bundle-GIM-10.6.0.0_r105601_v10_6_1-rhel-7-linux-x86_64.gim.sh  

./guard-bundle-GIM-10.6.0.0_r105601_v10_6_1-rhel-7-linux-x86_64.gim.sh -- --dir /usr/local/guardium --tapip  192.168.73.162 --sqlguardip 192.168.73.160 --perl /usr/bin  --install_customed_bundles 
```



**check Gim verify to CM**

```
login to CM
https://192.168.73.160:8443

Manage > GIM process monitor
```



**install STAP on CM**

```
upload and then import module
Manage > upload Modules 
then upload gim file stap

and then for install this module go to module > step up by clinet > choss bundle >
and then install stap

check status not install - Pending install - failed - installed

in installation way add 
Optional parameters
sql guard 
ip  = Collector ip
*)if 2 collectors , STAP_ADDITIONAL_SQLGUARD_IPS = other colelctors

if failed installation,  check version of stap

to marahele nasbe stap , atap ham nasb mishe ke bayad ro server kernel-devel instlal bashe
sudo yum install kernel-devel-*

```

**collector**

```
and then check collector that this server detect db server
```

**for trust between collector and CM**

```bash
 On collector and CM

# store system shared secret 123
```

**initialaze central manager and collector**

```
on central manager , i do type central manager
# store unit type manager
then relogin to web and check : 
goshe samte rast : 
machin type : Central Manager - Aggregator

on collector
Login to Collector
https://192.168.73.161:8443
setup > Central Manager >  Registration	and load balance > add host ip and port of central manager = 192.168.73.160 8443

then relogin to web cosole and check 
```



### **Update  cm 10.0 version to 11.0**

```
run this command on CM
#fileserver <client_ip> 3600

type in browser :
#https://192.168.73.160:8445/
```

**upgrade process**

go to manage > central management

![Screenshot (10)](C:\Users\m_baousi\Downloads\MEGA\Security\Screenshot (10).png)

![Screenshot (11)](C:\Users\m_baousi\Downloads\MEGA\Security\Screenshot (11).png)

Status of upgrade 10 to 11

![Screenshot (12)](C:\Users\m_baousi\Downloads\MEGA\Security\Screenshot (12).png)



**Upgrade GIM and Stap agent from V10 To Ver11**

```
1 - download GIM and stap from support IBS

2 - search > upload modules > browse > upload couple of moudles > import

3 - Manage > module instalation > step by client > install stap and gim 11
 notice : when update stap , STAP_SQLGUARD_IP = collector ip
 if 2 collectors , STAP_ADDITIONAL_SQLGUARD_IPS = other colelctors
```

**and then go to DB server and check version of stap and GIM**



![Screenshot (13)](C:\Users\m_baousi\Downloads\MEGA\Security\Screenshot (13).png)



**and then update collector Guardium from central manager**

```
Manage > central maneger > patch distribution > and then install patch 9997 , 300
```

![Screenshot (14)](C:\Users\m_baousi\Downloads\MEGA\Security\Screenshot (14).png)

select 9997 and install patch and then select 300 and then install patch now





**verify install patch on collector**

```
manage > maintrance > general > installed patch
```

 

**check install patch on collector**

```
show system patch installed
```



**update pache on central manager from cli**

```
store system patch install sys now
```

![Screenshot (15)](C:\Users\m_baousi\Downloads\MEGA\Security\Screenshot (15).png)

and install patch number

**check update central manager from cli**

![Screenshot (16)](C:\Users\m_baousi\Downloads\MEGA\Security\Screenshot (16).png)

and install patch number



**unlock user and password**

```
when admin user lock you can enter to console with accessmgr user and guardium password

if dont enter to console

#support reset-password accessmgr
Password for accessmgr account have been successfully reset using keyword: 1-3656089-5-5

#unlock accessmgr 

#unlock admin

and try again 
```

**PATH KTAP log on db Server** 

```
if not loaded KTAP module have to read logs
 # less /usr/local/modules/KTAP/current/KTAP.log
 [Sun Feb 28 03:11:54 2021] -I- KTAP finished execution successfully
```



![Screenshot (17)](C:\Users\m_baousi\Downloads\MEGA\Security\Screenshot (17).png)

**uninstall gim** 

```
/opt/guardium/modules/GIM/current/uninstall.pl /opt/guardium/ 
```

**change gim clinet**

```
/opt/guardium/modules/UTILS/11.2.0.10_r109349_1-1607232964/files/bin/configurator.sh --set GIM_CLIENT_IP 172.16.65.231
```



**change gim server ip (CM)**

```
/opt/guardium/modules/UTILS/11.2.0.10_r109349_1-1607232964/files/bin/configurator.sh --set GIM_URL**  192.168.73.160
```



**check gim client info**

```
/opt/guardium/modules/UTILS/11.2.0.10_r109349_1-1607232964/files/bin/configurator.sh --get GIM
```



**check gim status , restart stop start**

```
##  systemctl status guard_gim
```

**delete unit type manager**

```
## delete unit type

Use this command to clear one or more unit type attributes. Note that not all unit type attributes can be cleared by using this command. See the table, located after the **store unit type** command, for more information.
```

##### show network interface status

```
Use this command to display the physical link status of a network interface.
Syntax

## show network interface status esn192
```

**stop restart status stap on shell**

```
/opt/guardium/modules/STAP/11.2.0.10_r109349_1-1607238943/guard-config-update --stop stap
/opt/guardium/modules/STAP/11.2.0.10_r109349_1-1607238943/guard-config-update --start stap
```

**modify stap**

```
sudo /opt/guardium/modules/STAP/11.2.0.10_r109349_1-1607238943/guard-config-update --add-sqlguard 172.16.65.231
sudo /opt/guardium/modules/STAP/11.2.0.10_r109349_1-1607238943/guard-config-update --add-sqlguard 172.16.65.231
sudo /opt/guardium/modules/STAP/11.2.0.10_r109349_1-1607238943/guard-config-update --set-tap-ip 192.168.73.161
```

**check log stap and gim**

```
less /opt/guardium/modules/GIM/11.2.0.10_r109349_1-1607232961/GIM.log
```

**uninstall all package**

```
 /opt/guardium/modules/GIM/current/uninstall.pl
```

**install gim module**

```
mkdir  /opt/guardium/

bash /data/informix/guard-bundle-GIM-11.3.0.0_r109764_v11_3_1-rhel-7-linux-x86_64.gim.sh -- --dir /opt/guardium/modules --tapip 172.16.65.231 --sqlguardip 192.168.73.160 --install_customed_bundles --perl /usr/bin/
```

**ktap reset**

```
/opt/guardium/modules/KTAP/11.3.0.0_r109764_1-1618978651/guard_ktap_stat reset
```

**uninstall stap**

```
#age mogheye install stap failed dad bekhatere ine ke ktap hanoz be kernel chasbide o bayad system reboot beshe
befor uninstall ktap from GUI must be rmmod ktap from kernel
<STAP directory>/KTAP/guard_ktap_loader stop
<STAP directory>/KTAP/guard_ktap_loader uninstall
rmmod ktap_109764 or modprobe -r ktap_109764
```

informix after reset for redundancy

```
after reboot server

1- oninit -PHYv <restart services>

if successfully started

2- onmode -d secondary guardiumdb <secondary>

3- onstat -g dri 
```

**if policy not work**

```
There are several things you can check when receiving "no traffic" alert.

1) For the server IP generating no traffic alert, is the STAP status active? If the STAP is inactive for any reason, or all STAPs are inactive (which means inspection-core is stopped), there would be no traffic collected.

For more information about inactive STAP, please refer to the following technote:
[What to do if you get Guardium "Inactive S-TAPs Since" alerts](http://www-01.ibm.com/support/docview.wss?uid=swg21698838)

2) Is no traffic from certain DB server a expected result? If there is indeed no traffic from the server at that time period (low traffic period), this would not be a concern.

3) What is the "Max Timestamp" in the alert text? Did some planned events happen on the server at that time?

4) Check the STAP configuration parameters. For example, if you are using load balancing, the traffic may had been sent to other collector. Is there any change to STAP configuration during that time? For example, if port range in inspection engine configuration was modified to a wrong value, it will cause no traffic.

5) Check the current installed policy on the collector. If the policy was set or changed to selective-audit policy? Or does it have rules like "ignore STAP session"? That may lead to the result of no traffic.
```

#### check open port from Guardium (telnet)

```
support show port open 192.168.72.250 22
```



### change ip address cm and colector

```
/opt/guardium/modules/UTILS/11.2.0.10_r109349_1-1607232964/files/bin/configurator.sh --set GIM_URL  192.168.73.160

 /opt/guardium/modules/UTILS/11.3.0.0_r109764_1-1623059447/files/bin/configurator.sh --set GIM_URL 10.10.5.35

 /opt/guardium/modules/UTILS/11.3.0.0_r109764_1-1623059447/files/bin/configurator.sh --set GIM_CLIENT_IP <database ip address>

check 
/opt/guardium/modules/UTILS/11.3.0.0_r109764_1-1623059447/files/bin/configurator.sh --get GIM

systemctl restart guard_gim
systemctl restart guard_upguard


change stap client parameter
cd /opt/guardium/modules/STAP/11.3.0.0_r109764_1-1623060001
nano guard_tap.ini

tap_ip=192.168.72.250
sqlguard_ip=192.168.73.161
tap_identifier=oracle_192.168.72.250(1521,1521,DB_0)
change this parameter

re install stap from GUI
```



#### question 10

```
A Guardium administrator needs to upgrade BUNDLE-STAP on a Linux server to the latest version using GIM. What parameter should the administrator set to ensure the upgrade will not require a reboot of the server? Options:C. KTAP_LIVE_UPDATE=Y 
```



oracle native enryption

```
1- authorized user
/opt/guardium/modules/ATAP/current/files/bin/guardctl authorize-user oracle
User 'oracle' is already authorized.

2-print and storing parameter
cd /opt/guardium/modules/STAP/11.3.0.0_r109764_1-1629635398
/opt/guardium/modules/STAP/current/guard_discovery guard_tap.ini  --print_output

 /opt/guardium/modules/ATAP/current/files/bin/guardctl --db-instance=orcl --db-user=oracle --db-type=oracle --db-base=/home/oracle --db-bits=64 --db-home=/root
/u01/app/oracle/product/12.2.0.1/db_1/ --db-version=12 store-conf

3- dump parameter
/opt/guardium/modules/ATAP/current/files/bin/guardctl --db-instance=orcl dump-params

4- shutdown oracle 
sql> shutdown normal

5- active command run
/opt/guardium/modules/ATAP/current/files/bin/guardctl --db-instance=orcl --db-user=oracle --db-type=oracle --db-base=/home/oracle --db-bits=64 --db-home=/root
/u01/app/oracle/product/12.2.0.1/db_1/ --db-version=12 activate


6- if problem - first deactive
 /opt/guardium/modules/ATAP/current/files/bin/guardctl --db-instance=orcl --db-user=oracle --db-type=oracle --db-base=/home/oracle/ --db-bits=64 --db-home=/root/u01/app/oracle/product/12.2.0.1/db_1/ --db-version=12 deactivate

```



snmp

```
store system snmp query community guardiumsnmp
```

tcpdump

```
support store tcpdump on <type> <period> <loglimit> [interface] [IP] [port] [protocol]

Turns on TCPDUMP utility. After period ends, results file tcpdump.tar.gz can be found via fileserver. The /var partition must have at least 15GB of free space.

Where:

- <type> - dump type, 'headers' (only headers captured) or 'raw' (whole packets captured)
- <period> - dump period, NUMBER[SUFFIX], where optional SUFFIX may be 's' for seconds, 'm' for minutes (default)
- <loglimit> - dump logfile limit, from 1 to 6 gigabytes
- Optional filter arguments:
  - [interface] - network interface name (default the primary interface)
  - [IP] - IP address
  - [port] - port
  - [protocol] - protocol, 'tcp', 'udp', 'ip', 'ip6', 'arp', 'rarp', 'icmp' or 'icmp6'

Example

​```plaintext
support store tcpdump on headers 10m 1 
​```



Example to capture raw packets on port 25 for 1 minute:
collector.ibm.com> support store tcpdump on raw 1m 1 25
Starting tcpdump...
```

syslog

```
show remotelog test
```

password expiration change

```
store password expiration** **[cli | guardcli1 - guardcli5 | gui] <days>**


```

#### clean report log from to

```
support clean DAM_data full_details  2021-06-01 2021-07-01
```

#### disk is full

```
#after purge data
restart stopped_services

#check disk full
support show db-status used %
If the result is 90% or more the GUI should be stopped automatically by auto stop services

#show usage disk
show filesystem usage
Directory                        Size
------------------- -----------------
database                 18,109.14 MB
insights_mongo              494.56 MB
log                         101.17 MB
gim                           0.02 MB
ok

#check konid engine khamosh bashe o process list haro baresi konid
stop inspection-core 
support show db-processlist running

#if there is a problem where the GUI keeps going down every five minutes, then consider switching the auto_stop_services_when_full to off

#support show large_files 10 0: Shows files larger than 10MB older than 0 days. Consider the largest ones for removal first.

```



## clean log data



```
From CLI, run these commands and examine the output.
support show db-top-tables all
support show large_files 500 0

support must_gather sniffer_issues


support show db-status used %
91%
ok


support show db-top-tables all
 Table Size (M) | I/D % |  Unused(M) | Est. Rows | Name
 -------------- | ----- |  --------- | --------- | ----------
          91305 |    10 |         44 |  35822083 | GDM_POLICY_VIOLATIONS_LOG
          21665 |     6 |         38 |   7503249 | GDM_CONSTRUCT_TEXT

support clean DAM_data policy_violations  2022-01-10 2022-09-03

support clean DAM_data full_details 2022-01-10 2022-09-03


##If there isn't enough disk space to purge a single day from a single table, use this grdapi to purge data in smaller chunks.

guard.com> grdapi get_purge_batch_size
ID=0
Purge Batch Size = 200000
ok
guard.com> grdapi set_purge_batch_size batchSize=100
ID=0
ok
guard.com> grdapi get_purge_batch_size
ID=0
Purge Batch Size = 100
ok
guard.com> 

##then set Purge Batch Size = 200000
```



**why my guardium internal database filling**

https://www.ibm.com/support/pages/why-my-guardium-internal-database-filling



zabbix reset pass 

```
1. Login to Zabbix MySQL/MariaDB Password.**

Use the following command to login the MySQL/MariaDB server as root. Please provide the password for root user.
# mysql -uroot -p
[![Mysql_mariaDB_login](https://1.bp.blogspot.com/-dkYqcpGoFJ0/X0T3V3hfUNI/AAAAAAAALgY/oAaNUyemy5Y1XLoZWwfB0iP4b8P1qnSAwCLcBGAsYHQ/w640-h178/Mysql_mariaDB_login.PNG)](https://1.bp.blogspot.com/-dkYqcpGoFJ0/X0T3V3hfUNI/AAAAAAAALgY/oAaNUyemy5Y1XLoZWwfB0iP4b8P1qnSAwCLcBGAsYHQ/s991/Mysql_mariaDB_login.PNG)


**2. After entering the password, use the following MySQL commands to reset the Zabbix Admin user password.**


mysql> use zabbix;


mysql> update zabbix.users set passwd=md5('zabbix') where alias='Admin';


mysql> quit;
```

Refrence : 
https://www.ibm.com
