# nmcli

nmcli has an IMHO rediculouse way to name interfaces.
in my environments i keep them identical to get not confused.

in case i add new connection i always specify ifname *and* con-name with the identical name!


## generic overview
```bash
nmcli con show
```

## reload when ifcfg-files edite manualy
```bash
nmcli con reload
```

## vlan tagged interface + bridge for each vlan

  * one vlan per use case
  * for each vlan a brigde (e.g. to setup VMs for dedicated VLANs)
  
```bash
#!/usr/bin/env bash
 
vlanNames=(wan lan dmz)
vlanIds=( 5 10 100 )
lastOctet="100"
firstOctets="192.168"
parentNic="eth0"
 
DEBUG="echo"
 
for i in "${!vlanNames[@]}"
do
  vName=${vlanNames[$i]}
  vId=${vlanIds[$i]}
  vNic="{parentNic}.${vId}"
  ip4Addr="${firstOctets}.${vId}.${lastOctet}/24"
  
  $DEBUG  nmcli con add type bridge ifname $vName con-name $vName ip4 $ip4Addr
  $DEBUG  nmcli con add type vlan   ifname $vNic  con-name $vNic  dev $parentNic id $vId master $vName slave-type bridge
 
done
```
