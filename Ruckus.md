- Mostrar interfaces resumen

`show interface brief`

- Nombrar puerto

`config terminal
interface ethe 1/1/18
port-name <DESCRIPCION>`

- Configure VLAN

```bash
config terminal
vlan <id-vlan>
untagged ethernet 1/1/18
```

- Mostrar por qué puerto está aprendiendo según filtro

`show mac-address | include <MAC>`

- Mostrar dispositivos conectados vía LLDP

`show lldp neighbors`

- Guardar

`write memory`

- Configurar puerto en híbrido (trunk + pvid) ([Configuring Dual Mode on a Ruckus ICX](https://www.youtube.com/watch?v=_E-Ft6EEZdA))

```bash
# se deben taggear ambas vlans primero
vlan 10
tagged ether 1/1/10
vlan 20
tagged ether 1/1/10

# acceder a la interfaz
interface ether <...>
# y después marcar lo que entiendo como pvid con el dualmode
dual-mode <ID vlan>
``` 