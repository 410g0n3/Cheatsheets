- Print routing table
    
    `get router info routing-table all`

- Print routing table to destination
    
    `get router info routing-table detail <destination-IP>`

- Mostrar configuración

    `show full-configuration`

- Mostrar información del sistema
    
    `get sys status`
    
- Configurar system log:
    
    ```bash
    config log syslogd setting
      set server [IP]
      set port [port]
      set status enable
    end
    ```
    
- Activar LLDP
    
    ```bash
    config sys global
    set lldp-transmission enable
    set lldp-reception enable
    end
    ```
    
- Mostrar tabla arp
    
    ```bash
    get sys arp
    
    #### Acotando búsqueda ####
    get sys arp | grep "nombre red"
    ``` 
    
- Mostrar todas las rutas
    
    `get router info routing-table database`
    
- Cargar backup
    
    `execute backup config ftp [nombre_archivo].cfg <ip> <usuario> <password>`
    
- Ejecutar ping y opciones
    
    ```bash
    exec ping <IP>
    
    exec ping-options data-size <bytes_int>
    exec ping-options repeat-count <repeat_int>
    exec ping-options source {auto | <interface_ipv4}
    exec ping-options timeout <seconds_int>
    exec ping-options tos {<service_type>}
    exec ping-options ttl <hops_int>
    exec ping-options view-settings`
    ```
    
- Ejecutar traceroute
    
    `exec traceroute <IP>`
    
- Ver reservas DHCP
    
    ```bash
    config system dhcp server
    show
    edit [x]
    ```
    
- Diagnose sniffer
    
    ```bash
    diag sniff packet any "dest xxx.xxx.xxx.xxx"
    diag sniff packet any "host xxx.xxx.xxx.xxx"
    diag sniff packet any "host x.x.x.x and dest x.x.x.x"
    ```
    
    https://github.com/yuriskinfo/cheat-sheets/blob/master/cheat-sheets/Fortigate-debug-diagnose-complete-cheat-sheet.adoc
    
- Túneles
    
    ```bash
    # levantar tunel`
    execute vpn ipsec tunnel up [Insert Phase 2 name] [Insert phase 1 name]
    ``` 
    
    refer: https://docs.fortinet.com/document/fortigate/6.0.0/cli-reference/695050/vpn-ipsec-tunnel-up
    
- Mostrar rutas
    
    `get router info routing-table all`
    
    https://community.fortinet.com/t5/FortiGate/Technical-Tip-Routing-in-FortiGate-route-lookup-process/ta-p/194047