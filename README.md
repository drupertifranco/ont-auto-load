# Configuracion de Auto-Load OLT HW MA5600T / MA5683T / MA5800-X15

## Indice
- [Configuracion de servidor FTP o TFTP](#id1)
- [Configuracion de servicio TFTP/FTP en la OLT](#id2)
- [Cargando el archivo de la versión ONT](#id3)
    - [Consulta la versión actual de ONT](#id3.1)
    - [Seleccione el paquete de archivos en formato .bin](#id3.2)
    - [Seleccione la ONT que desea actualizar](#id3.3)
    - [Inicie la actualización](#id3.4)
    - [Consulta el progreso de carga](#id3.5)
- [Cargue automáticamente el archivo de versión ONT](#id4)
    - [Configure la política de carga automática de ONT](#id4.1)
    - [Comprueba el progreso de la carga](#id4.2)
- [Referencias](#id5)
---

## Configuracion de servidor FTP o TFTP<a name="id1"></a>
### Descarga del servicio tftpd
- https://bitbucket.org/phjounin/tftpd64/downloads/
### Descarga del servicio FTP Filezila
- https://filezilla-project.org/download.php?platform=win64&type=server
- 
## Configuracion de servicio TFTP/FTP en la OLT <a name="id2"></a>
### Metodo 1
``` 
MA5683T(config)#file-server auto-load ont-file primary SERVER_IP PROTOCOL PATH
```
> TIP: Dejar el archivo en la carpeta root o en tal caso selecionar la carpeta root donde este el archivo que desea cargar
### Metodo 2
``` 
MA5683T(config)#diagnose
MA5683T(diagnose)%%ont-load info program G_ONU_XXX-enc.bin ftp X.X.X.X FTP_USER FTP_PASS
MA5683T(diagnose)%%ont-load info program G_ONU_XXX-enc.bin tftp X.X.X.X
```
## Cargando el archivo de la versión ONT <a name="id3"></a>
```
MA5683T(diagnose)%%ont-load select FRAME/SLOT PORT-ID ONT-ID
```
### Consulta la versión actual de ONT 
```
MA5683T(diagnose)%%display ont version FRAME_ID SLOT_ID PORT_ID ONT_ID
```
### Cargado por lote
```
MA5683T(diagnose)%%ont-load select FRAME/SLOT PORT-ID ONT-ID_1
MA5683T(diagnose)%%ont-load select FRAME/SLOT PORT-ID ONT-ID_2
                               ...
MA5683T(diagnose)%%ont-load select FRAME/SLOT PORT-ID ONT-ID_n
``` 
### Inicie la actualización

```
MA5683T(diagnose)%%ont-load start
```
El progreso de carga tiene los siguientes puntos clave: 10%, 20%, 80% y 100%, que representan respectivamente las fases de carga de ONT.

- 0 - 10% : cargando en el host;
- 10% - 20% : Cargado en un tablero.
- 20% - 80% : cargado a la ONT;
- 80% - 100% : La carga está completa.

### Consulta el progreso de carga
```
MA5683T(diagnose)%%display ont-load select
MA5683T(diagnose)%%display ont-load result
```
## Cargue automáticamente el archivo de versión ONT

### Metodo 1
``` 
MA5683T(config)#file-server auto-load ont-file primary SERVER_IP PROTOCOL PATH
```
> TIP: Dejar el archivo en la carpeta root o en tal caso selecionar la carpeta root donde este el archivo que desea cargar

### Configure la política de carga automática de ONT
```
MA5683T(config)%%ont auto-load ONT_MODEL Target_Version file_name 
```
#### Ver la tarea de auto-load
```
MA5683T(config)%%display ont ont-load config all
```
### Consulta el progreso de carga
```
MA5683T(diagnose)%%display ont-load select
MA5683T(diagnose)%%display ont-load result
```
### Reinicio de ONT
```
MA5683T(config-if-gpon-0/0)#ont reset PORT-ID ONT-ID
```
# Videos
- https://youtu.be/EW3zzOxMU90
- https://youtu.be/smK1_ht0xys
- https://youtu.be/AbHTeRLZMJE
- https://youtu.be/m2sRpT6_xXA
# Referencias

- https://forum.huawei.com/enterprise/es/%C2%BFC%C3%B3mo-se-carga-un-archivo-de-actualizaci%C3%B3n-de-ONT/thread/667241296923869184-667212890693840896
- https://halny.com/knowledge-base/ont-halny-upgrade-on-huawei-ma5600t-ma5683t-ma5800-x15/
