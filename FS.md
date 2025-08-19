# S5800 Series

https://img-en.fs.com/file/user_manual/s5800-series-switches-cli-reference-guide.pdf

# S3950 Series

https://img-en.fs.com/file/user_manual/s3950-4t12s-switch-configuration-guide.pdf

# S3900 Series

https://resource.fs.com/mall/doc/20240506155005y6cilr.pdf

# S3400 Series (PoE)

https://img-en.fs.com/file/user_manual/s3400-48t4sp-switch-cli-reference-guide.pdf

### Upgrade Firmware & Web

1. Abrimos cualquier programa que nos permita hacer de servidor TFTP ([MobaXterm](https://mobaxterm.mobatek.net/download.html) o [Tftpd64](https://pjo2.github.io/tftpd64/)). Importante: tener en cuenta el directorio donde se encuentran los archivos a transferir
2. Conectamos por CLI (consola o ssh)
```bash
dir
# comprobamos que estan los ficheros Web.wrp y Switch.bin
# borramos los archivos actuales
delete 'Web.wrp'
delete 'Switch.bin'
# copiamos los archivos
copy tftp flash Switch.bin <IP servidor> Switch.bin
copy tftp flash Web.wrp <IP servidor> Web.wrp
# reiniciamos el switch
reboot
```
4. Comprobamos que las versiones son las que corresponden. Tanto de firmware como de interfaz web.

- Config interface batch

```bash
config
interface range eth-0-1 - 16
<comando>
```

- Configure ssh access in S3400 PoE switch's

```bash
username <user> login mode ssh
username privilege 15
end
```

- Config username and password

`username testname privilege 4 password 123abc<>`

# Configure stack S3900-R

https://img-en.fs.com/file/user_manual/s3900-48t6s-r-switch-stacking-configuration-guide.pdf
