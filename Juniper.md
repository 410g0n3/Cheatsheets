```bash
# Comparar configuración antes de guardarla
show | compare

# Mostrar uptime
show system uptime

# Mostrar versión dispositivo y haiku
show version and haiku

# Mostrar información interfaz
show interfaces ge-0/0/0

# Mostrar información más extensa sobre la interfaz, como número de paquetes,
# errores, etc.
show interfaces extensive ge-0/0/0

# Mostrar configuración en vista "set"
show configuration | display set
show configuration | display set | match <string>

# Mostrar la configuración de algún protocolo en concreto, es decir,
# de bajos niveles según jerarquía
show configuration protocols lldp

# Mostrar todas las interfaces caídas
show interfaces terse ge-0/0/* | match down

# Revertir cambios, o volver a una versión en concreto
rollback
rollback *n*

# Aplicar cambios / necesidad de confirmación / añadir comentario 
# / ver comentarios / programarlos
commit
commit confirmed <minutes>
commit comment "<string>"
commit at "hh:mm:ss" or 

show system commit

# Mostrar la configuración actual y compararla con alguna versión en particular
show configuration | compare rollback *n

#* Editar la CLI
set cli timestamp
set cli screen-width 1000

# Mostrar flujo de paquetes en tiempo real
monitor interface traffic
monitor interface ge-0/0/0.0

# Herramienta MTR
traceroute monitor <IP>

# Bloquear candidate configuration para que otro usuario 
# no configure al mismo tiempo que tu
configure exclusive

# Mostrar rutas / según protocolo
show route 
show route brief
show route protocol bgp/ospf

# Para cambiar un valor de una interfaz como una IP
[edit interfaces et-1/2/3 unit 0 family inet]
rename address 10.8.9.7/24 to address 10.8.9.8/24

# Para calcar la configuración sobre otra intefaz
replace pattern xe-0/1/2 with xe-0/1/4

# Configurar una ruta estática IPv4
set routing-options static route <dst/cidr> next-hop <IP>

# Configurar una ruta estática IPv6
set routing-options **rib inet6.0** static route ...

# Crear VLAN
set vlans <nombre_VLAN> vlan-id <ID>

# Configurar VLAN
# Acceso / Trunk
set interface ge-0/0/1 unit 0 family ethernet-switching interface-mode access / trunk
# Añadir VLANs
set interface ge-0/0/1 unit 0 family ethernet-switching vlan members <name VLAN>

# Ver tabla MAC
show ethernet-switching table

# Configure NTP
set system ntp server 0.es.pool.ntp.org 

# Banner to display text before the login attempt
set system login message "<text>"

# Banner to display text after the login
set system login announcement "This is line 1\nThis is line2"

# Revisar alarmas (chassis LED)
show system alarms

# Mostrar la configuración en vista set pero jerarquicamentex1
show configuration firewall family inet filter <name> | display set relative

# Mirar estadísticas de policy's statements
show policy <name> statistics

# Revisar contador reglas firewall
show firewall counter <name term> filter <name filter>

# Proteger configuración de ser configurada
protect protocols lldp
unprotect protocols lldp

# Realizar comentarios en la configuración
annotate system "<string>"

edit protocols
annotate bgp "Dont touch"

# Gestion archivos
file list
file show
file delete

# Puedes guardar dos configuraciones en archivos de texto para 
# compararlas a posterior
show configuration | save <file_01>.txt

show configuration | compare <file_01>.txt

file compare files <file_01> <file_02>
# a = addition; c = change; d = deletion

# Cargar una configuración completa copy paste en modo jerarquia
load override <text file>
load override terminal

# Cargar una configuración simultáneamente
load merge <text file>
load merge terminal # from the top
load merge terminal relative # from level heriarchy

# Automatiza copias de seguridad cada commit
set system archival configuration transfer-on-commit
set system archival configuration archive-site "scp://<username>@<ip>:/<path" password <pass>

# Crea configuraciones que se aplican automaticamente a una jerarquía
set groups MTU_9192_GROUP interfaces <xe-*> mtu 9192
set interfaces apply-groups MTU_9192_GROUP
set interfaces xe-0/1/5 apply-groups-except MTU_9192_GROUP # todos menos este
show configuration interfaces xe-* | display inheritance no-comments

# Configurar en rango
edit interfaces interface-range INTERFACES_VLAN_50
set member-range ge-0/0/0 to ge-0/0/10
set member-range ge-0/[1-3]/*
set unit 0 family ethernet-switching vlan members FINANCE

# Mismo comando repetidamente (n) seg
show bgp summary | **refresh 2**

# Check who is logged on
show system users

# logout user
request system logout user <name>

# Config SNMP
set snmp description "<string>"
set snmp location "<string>"
set snmp contact "<string>"

set snmp community <string> authorization read-only
set snmp community <string> clients IP/CIDR

set snmp trap-group <string> version v2
# examples of categories of trap to choose:
# authentication, chassis, configuration, link, routing, services, vrrp-events
set snmp trap-group <string> categories chassis link
set snmp trap-group <string> target <IP>

## VRRP aka Routing Instances
# creamos la instancia
set routing-instances TEST_INSTANCE instance-type virtual-router

# asignamos las interfaces a la instancia
set routing-instances TEST_INSTANCE interface ge-0/0/2.0
set routing-instances TEST_INSTANCE interface ge-0/0/3.30

# se puede crear ruta estática
set routing-instances TEST_INSTANCE routing-options static route 0/0 next-hop <ip>

# y activar OSPF
set routing-instances TEST_INSTANCE protocols ospf area 0 interface ge-0/0/2.0
set routing-instances TEST_INSTANCE protocols ospf area 0 interface ge-0/0/3.30

# Packet Sniffer as tcpdump
monitor traffic interface ge-0/0/0.0

## Built-in help documents
# Mostrar las posibles configuraciones y una descripción
help apropos host-name

# un resumen de como configurarlo
help reference ospf area

# teoría de lo que hace el comando / usage guidelines for a topic or 
# configuration statement
help topic vlans private-vlan-qfx

# tip del día
help tip cli

```

## Filtering output

```bash
Possible completions:
append               Append output text to file
**count**                Count occurrences
**display**              Show additional kinds of information
except               Show only text that does not match a pattern
**find**                 Search for first occurrence of pattern
hold                 Hold text without exiting the --More-- prompt
last                 Display end of output only
**match**                Show only text that matches a pattern
no-more              Don't paginate output
refresh              Refresh a continuous display of the command
request              Make system-level requests
resolve              Resolve IP addresses
save                 Save output text to file
tee                  Write to standard output and file
trim                 Trim specified number of columns from start of line
```

## Shortcurts
1. Ctrl-a → moves you to the start
2. Ctrl-e → moves you to the end
3. Ctrl-w → delete an entire word at a time
4. Ctrl-k → delete everything from the cursor onward
5. Ctrl-x → delete the all characters from the command line
6. Ctrl-u → elimina la línea entera