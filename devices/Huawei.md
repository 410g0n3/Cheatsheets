- Acceder modo configuracion
    
    `system-view`

- Listar las MACs etiquetadas en una VLAN ID

    `display mac-address vlan [ID]`

- Listar información del dispositivo
  
  `show version`
  
  `display interface Gi 0/0/1`

  `display esn`

  `display device manufacture-info`

- LLDP

  ```bash
  lldp enable
  display lldp neighbor brief
  display lldp neighbor
  ```

-  Config NTP

    ```bash
    ntp-service server disable
    ntp-service ipv6 server disable
    ntp-service unicast-server 193.145.15.15
    clock timezone Bern,Rome,Stockholm,Vienna add 01:00:00
    clock daylight-saving-time Bern,Rome,Stockholm,Vienna one-year 00:02 2022-03-27 02:00 2022-10-31 01:00
    ```

- VLAN
  
  ```bash
  system-view
  vlan [vlan id]
  description [escribir descripcion]
  quit

  # Access mode
  system-view
  int gi 0/0/[numero puerto]
  port link-type access
  port default vlan [vlan id]

  # Trunk
  system-view
  int gi 0/0/[numero puerto]
  port link-type trunk
  port trunk allow-pass vlan [vlan id]
  port trunk pvid vlan [vlan id]
  ```

- SNMP
  
  ```bash
  snmp-agent
  snmp-agent community read <community>
  snmp-agent sys-info version v2c
  snmp-agent mib-view included 1 dod
  snmp-agent mib-view included 1 internet
  snmp-agent mib-view included 1 mib-2
  snmp-agent trap enable
  ``` 
  https://support.huawei.com/enterprise/en/doc/EDOC1100137933/dab469bd/snmp-configuration-commands

- Transceiver info

  `display transceiver diagnosis interface gi [x/x/x]`

- LACP

  ```bash
  [HUAWEI] sysname SwitchA
  [SwitchA] interface eth-trunk 1
  [SwitchA-Eth-Trunk1] mode lacp
  [SwitchA-Eth-Trunk1] quit
  [SwitchA] interface gigabitethernet 0/0/1
  [SwitchA-GigabitEthernet0/0/1] eth-trunk 1
  [SwitchA-GigabitEthernet0/0/1] quit
  [SwitchA] interface gigabitethernet 0/0/2
  [SwitchA-GigabitEthernet0/0/2] eth-trunk 1
  [SwitchA-GigabitEthernet0/0/2] quit
  [SwitchA] interface eth-trunk 1
  [SwitchA-Eth-Trunk1] port link-type trunk
  [SwitchA-Eth-Trunk1] port trunk allow-pass vlan 10 20
  [SwitchA-Eth-Trunk1] quit
  ```

- Config web user

  ```bash
  [HUAWEI] aaa
  [HUAWEI-aaa]local-user [nombre-usuario] password irreversible-cipher [Contraseña-usuario]
  [HUAWEI-aaa]local-user [nombre-usuario] privilege level [0-15]
  Warning: This operation may affect online users, are you sure to change the user privilege level ?[Y/N]Y
  [HUAWEI-aaa]local-user [nombre-usuario] service-type http
  [HUAWEI-aaa]quit
  ```