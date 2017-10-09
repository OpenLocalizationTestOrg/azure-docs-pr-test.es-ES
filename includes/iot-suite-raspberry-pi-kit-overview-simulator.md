## <a name="overview"></a>Información general

En este tutorial, se realizará Hola pasos:

- Implemente una instancia de hello remoto supervisión solución preconfigurada tooyour suscripción de Azure. Este paso implementa y configura varios servicios de Azure automáticamente.
- Configure su toocommunicate de dispositivo con el equipo y la solución de supervisión remota Hola.
- Actualizar Hola ejemplo dispositivo código tooconnect toohello solución de supervisión y enviar telemetría simulada que se puede ver en el panel de la solución de Hola.

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial, necesita una suscripción activa de Azure.

> [!NOTE]
> En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para más información, consulte la [evaluación gratuita de Azure][lnk-free-trial].

### <a name="required-software"></a>Requisitos de software

Se necesita al cliente SSH en su tooenable de máquina de escritorio tooremotely acceso Hola la línea de comandos en hello frambuesa Pi.

- Windows no incluye ningún cliente SSH. Se recomienda usar [PuTTY](http://www.putty.org/).
- La mayoría de las distribuciones de Linux y Mac OS incluyen la utilidad SSH de línea de comandos de Hola. Para más información, consulte [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (SSH cuando se usa Linux o Mac OS).

### <a name="required-hardware"></a>Requisitos de hardware

Un equipo de escritorio tooenable tooconnect remotamente toohello la línea de comandos en hello frambuesa Pi.

[Kit de inicio de Microsoft IoT para Raspberry Pi 3][lnk-starter-kits] o componentes equivalentes. Este tutorial utiliza Hola siguientes elementos del kit de hello:

- Raspberry Pi 3
- Tarjeta MicroSD (con NOOBS)
- Un cable USB mini
- Un cable Ethernet

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/