## <a name="prepare-your-raspberry-pi"></a>Preparación de su Raspberry Pi

### <a name="install-raspbian"></a>Instalación de Raspbian

Si se trata de hello primera vez que usa el instalador de plataforma de frambuesa, necesita tooinstall hello Raspbian SO mediante NOOBS en tarjeta SD de hello incluida en el kit de Hola. Hola [frambuesa Pi Software guía] [ lnk-install-raspbian] describe cómo tooinstall un sistema operativo en el instalador de plataforma de frambuesa. Este tutorial se da por supuesto que ha instalado el sistema operativo de hello Raspbian en el instalador de plataforma de frambuesa.

> [!NOTE]
> tarjeta de Hello SD incluida en hello [Microsoft Azure IoT Starter Kit para frambuesa Pi 3] [ lnk-starter-kits] ya tiene NOOBS instalado. Se puede iniciar Hola frambuesa Pi de esta tarjeta y elija tooinstall hello Raspbian OS.

### <a name="set-up-hello-hardware"></a>Configurar el hardware de Hola

Este tutorial usa sensor hello BME280 incluido en hello [Microsoft Azure IoT Starter Kit para frambuesa Pi 3] [ lnk-starter-kits] toogenerate los datos de telemetría. Utiliza un tooindicate LED cuando Hola frambuesa Pi procesa una invocación de método desde el panel de la solución de Hola.

componentes de Hello en el panel de pan de hello son:

- LED rojo
- Resistencia de 220 ohmios (rojo, rojo, marrón)
- Sensor de BME280

Hola siguiente diagrama muestra cómo tooconnect su hardware:

![Configuración de hardware para Raspberry Pi][img-connection-diagram]

Hello tabla siguiente resume las conexiones de Hola de componentes de hello frambuesa Pi toohello en breadboard hello:

| Raspberry Pi            | Placa de pruebas             |Color         |
| ----------------------- | ---------------------- | ------------- |
| GND (patilla 14)            | Patilla -ve de LED (18A)      | Púrpura          |
| GPCLK0 (patilla 7)          | Resistencia (25A)         | Naranja          |
| SPI_CE0 (patilla 24)        | CS (39A)               | Azul          |
| SPI_SCLK (patilla 23)       | SCK (36A)              | Amarillo        |
| SPI_MISO (patilla 21)       | SDO (37A)              | Blanco         |
| SPI_MOSI (patilla 19)       | SDI (38A)              | Verde         |
| GND (patilla 6)             | GND (35A)              | Negro         |
| 3.3 V (patilla 1)           | 3Vo (34A)              | Rojo           |

el programa de instalación del hardware de Hola de toocomplete, debe:

- Conecte la fuente de alimentación de toohello de frambuesa Pi incluida en el kit de Hola.
- Conectar su red de tooyour de frambuesa Pi con cable de Ethernet de hello incluido en el kit. Como alternativa, puede configurar [Conectividad inalámbrica][lnk-pi-wireless] para su Raspberry Pi.

Ahora ha completado el programa de instalación de hardware de Hola de su Pi frambuesa.

### <a name="sign-in-and-access-hello-terminal"></a>Inicio de sesión y terminal Hola

Tiene dos tooaccess de opciones un entorno de terminal en su Pi frambuesa:

- Si tiene un teclado y supervisar tooyour conectado frambuesa Pi, puede usar hello Raspbian GUI tooaccess una ventana de terminal.

- Línea de comandos de acceso hello en el instalador de plataforma de frambuesa mediante SSH desde el equipo de escritorio.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Usar una ventana de terminal en hello GUI

las credenciales predeterminadas de Hola para Raspbian son nombre de usuario **pi** y la contraseña **frambuesa**. En la barra de tareas de Hola Hola GUI, puede iniciar hello **Terminal** utilidad mediante el icono de Hola que parece un monitor.

#### <a name="sign-in-with-ssh"></a>Inicio de sesión con SSH

Puede utilizar SSH para acceso de línea de comandos tooyour frambuesa Pi. artículo de Hello [SSH (Secure Shell)] [ lnk-pi-ssh] describe cómo tooconfigure SSH en el instalador de plataforma de frambuesa y cómo tooconnect de [Windows] [ lnk-ssh-windows] o [Linux y Mac OS][lnk-ssh-linux].

Inicie sesión con el nombre de usuario **pi** y la contraseña **raspberry**.

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a>Opcional: Compartir una carpeta en su Raspberry Pi

Si lo desea, puede que desee tooshare una carpeta en el instalador de plataforma de frambuesa con el entorno de escritorio. Compartir una carpeta permite toouse su editor de texto preferido del escritorio (como [código de Visual Studio](https://code.visualstudio.com/) o [texto fundamentales](http://www.sublimetext.com/)) tooedit archivos en el instalador de plataforma de frambuesa en lugar de usar `nano` o `vi`.

tooshare una carpeta con Windows, configurar un servidor de Samba en hello frambuesa Pi. O bien, usar integrada de hello [SFTP](https://www.raspberrypi.org/documentation/remote-access/) servidor con un cliente SFTP en el escritorio.

### <a name="enable-spi"></a>Habilitación de SPI

Antes de poder ejecutar la aplicación de ejemplo de Hola, debe habilitar bus interfaz periféricos serie (SPI) Hola Hola frambuesa Pi. Hola frambuesa Pi se comunica con dispositivos de hello BME280 sensor a través Hola bus SPI. Usar hello el archivo de configuración de comando tooedit Hola siguiente:

```sh
sudo nano /boot/config.txt
```

Busque la línea de saludo:

`#dtparam=spi=on`

- línea de hello toouncomment, delete hello `#` al principio de Hola.
- Guarde los cambios (**O Ctrl**, **ENTRAR**) y salga del editor hello (**Ctrl-X**).
- tooenable SPI, reinicie Hola frambuesa Pi. Reiniciar el sistema desconecta terminal hello, necesita toosign de nuevo cuando se reinicia Hola frambuesa Pi:

  ```sh
  sudo reboot
  ```


[img-connection-diagram]: media/iot-suite-raspberry-pi-kit-prepare-pi/rpi2_remote_monitoring.png

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/