# Configuracion de Auto-Load OLT ZTE C300

1. **Conexión a la OLT**:
   - Conéctate a la OLT mediante Telnet o SSH. La dirección IP de fábrica suele ser `136.1.1.100`, con el usuario y contraseña predeterminados `zte`.
     ```shell
     telnet 136.1.1.100
     ```

2. **Acceso a Modo Privilegiado**:
   - Una vez conectado, ingresa al modo privilegiado.
     ```shell
     Username: zte
     Password: zte
     ZXAN> enable
     Password: zxr10
     ZXAN#
     ```

3. **Configuración del Servidor FTP**:
   - Configura un servidor FTP donde almacenarás el firmware. Asegúrate de que el servidor esté accesible desde la OLT.

4. **Carga del Firmware al Servidor FTP**:
   - Sube el archivo de firmware al servidor FTP. Luego, desde la OLT, utiliza el siguiente comando para descargar el firmware:
     ```shell
     ZXAN# file download version * ftp://usuario:contraseña@ip/ruta
     ```

5. **Verificación de la Descarga**:
   - Verifica que el archivo de firmware se haya descargado correctamente.
     ```shell
     ZXAN# show file
     ```

6. **Actualización del Firmware**:
   - Inicia la actualización del firmware en las ONTs conectadas.
     ```shell
     ZXAN# upgrade ont all version *
     ```

7. **Reinicio de la OLT**:
   - Reinicia la OLT para aplicar la actualización.
     ```shell
     ZXAN# reboot
     ```

8. **Verificación de la Actualización**:
   - Verifica que todas las ONTs hayan recibido y aplicado el nuevo firmware correctamente.
     ```shell
     ZXAN# show ont version
     ```

(0)(https://www.smartolt.com/zte-olt-initial-setup.html)
(1) ZTE OLTs Initial Setup - Smart OLT. https://www.smartolt.com/zte-olt-initial-setup.html.
(2) Configurar OLT Huawei en Portal SmartOlt. https://www.youtube.com/watch?v=WnjUEqA0TX4.
(3) Integrando uma OLT Huawei ao sistema SMARTOLT (vídeo atualizado). https://www.youtube.com/watch?v=l7nwXEjXua0.
(4) Configurando servidor TR069 no Smartolt. https://www.youtube.com/watch?v=wz9mem8gHbg.
(5) GitHub - drupertifranco/ont-auto-load: El proceso de auto-carga de una .... https://github.com/drupertifranco/ont-auto-load.
(6) Connection Setup Instructions - Smart OLT. https://www.smartolt.com/setup_instructions_amz.html.
(7) undefined. https://bitbucket.org/phjounin/tftpd64/downloads/.
(8) undefined. https://filezilla-project.org/download.php?platform=win64&type=server.
(9) undefined. https://youtu.be/EW3zzOxMU90.
(10) undefined. https://youtu.be/smK1_ht0xys.