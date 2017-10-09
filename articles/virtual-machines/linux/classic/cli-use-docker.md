---
title: "Hola aaaUsing extensión de máquina virtual de Docker para Linux en Azure"
description: "Describe Docker y extensiones de máquinas virtuales de Azure de Hola y muestra cómo tooprogrammatically crear máquinas virtuales en Azure que son hosts de docker desde la línea de comandos de hello mediante Hola CLI de Azure."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a>Uso de hello extensión de máquina virtual Docker de hello Azure interfaz de línea de comandos (CLI de Azure)
> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Para obtener información acerca del uso de extensión de máquina virtual Docker Hola con modelo de administrador de recursos de hello, consulte [aquí](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Este tema describe cómo toocreate una máquina virtual con hello extensión de máquina virtual Docker de hello service modo de administración (asm) de CLI de Azure en cualquier plataforma. [Docker](https://www.docker.com/) es uno de hello más populares enfoques de virtualización que utiliza [contenedores Linux](http://en.wikipedia.org/wiki/LXC) en lugar de máquinas virtuales como una manera de aislar los datos y calcular en recursos compartidos. Puede usar la extensión de máquina virtual Docker de Hola y Hola [agente Linux de Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate una máquina virtual de Docker que hospeda cualquier número de contenedores para las aplicaciones en Azure. toosee un análisis de alto nivel de los contenedores y sus ventajas, vea hello [Docker alto nivel Pizarra](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a>¿Cómo toouse Hola extensión de máquina virtual de Docker con Azure
extensión de máquina virtual Docker de hello toouse con Azure, debe instalar una versión de hello [interfaz de línea de comandos de Azure](https://github.com/Azure/azure-sdk-tools-xplat) (CLI de Azure) mayor que 0.8.6 (ya que de este hello escritura versión actual es 0.10.0). Puede instalar Hola CLI de Azure en Mac, Linux y Windows.

completar el proceso de Hello toouse Docker en Azure es sencillo:

* Instalar Hola CLI de Azure y sus dependencias en equipo Hola desde el que desea toocontrol Azure (en Windows, será una distribución de Linux que se ejecuta como una máquina virtual)
* Utilizar hello Azure CLI Docker comandos toocreate un host de máquina virtual Docker en Azure
* Utilice Hola local Docker comandos toomanage los contenedores de Docker en la VM de Docker en Azure.

### <a name="install-hello-azure-command-line-interface-azure-cli"></a>Instalar hello Azure interfaz de línea de comandos (CLI de Azure)
tooinstall y configurar Hola CLI de Azure, consulte [cómo tooinstall Hola interfaz de línea de comandos de Azure](../../../cli-install-nodejs.md). instalación de hello tooconfirm, tipo `azure` en línea de comandos de Hola y después de un breve momento debería ver Hola arte ASCII de CLI de Azure, que enumera Hola basic comandos tooyou disponible. Si funcionó correctamente la instalación de hello, debe ser capaz de tootype `azure help vm` y que uno de los comandos de hello aparecen es "docker".

> [!NOTE]
> Docker tiene herramientas para Windows, [Docker máquina](https://docs.docker.com/installation/windows/), que también puede utilizar la creación de hello tooautomate de un cliente que puede usar toowork con máquinas virtuales de Azure como hosts de docker.
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a>Conectar hello Azure CLI tootooyour cuenta de Azure
Antes de poder usar Hola CLI de Azure debe asociar las credenciales de cuenta de Azure con hello CLI de Azure en la plataforma. Hola sección [cómo tooconnect tooyour suscripción de Azure](../../../xplat-cli-connect.md) explica cómo tooeither descargar e importar su **.publishsettings** de archivos o asociar la CLI de Azure con un Id. de organización.

> [!NOTE]
> Hay algunas diferencias de comportamiento cuando se usa una o hello otros métodos de autenticación, por lo que sea seguro tooread Hola documento por encima de una funcionalidad diferente toounderstand Hola.
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a>Instalar a Docker y usar hello Docker extensión de máquina virtual de Azure
Siga hello [las instrucciones de instalación de Docker](https://docs.docker.com/installation/#installation) tooinstall Docker localmente en el equipo.

toouse Docker con máquinas virtuales de Azure, imagen de Linux de hello utilizada para hello VM debe tener hello [agente de VM de Linux de Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) instalado. Actualmente, solamente hay dos tipos de imágenes que proporcionan esto:

* Una imagen de Ubuntu desde la Galería de imágenes de Azure de Hola o
* Una imagen personalizada de Linux que se crearon con hello agente de VM de Linux de Azure instalado y configurado. Vea [agente de VM de Linux de Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener más información acerca de cómo toobuild una VM de Linux personalizado con hello agente de máquina virtual de Azure.

### <a name="using-hello-azure-image-gallery"></a>Uso de la Galería de imágenes de Azure de Hola
Desde una sesión de Terminal o intensiva de errores, usar hello después toolocate Hola imagen Ubuntu más reciente en hello VM Galería toouse escribiendo el comando de CLI de Azure

`azure vm image list | grep Ubuntu-14_04`

y seleccione uno de los nombres de imagen de hello, como `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, y comando de uso Hola siguiente toocreate una nueva máquina virtual con esa imagen.

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

donde:

* *&lt;nombre de la máquina virtual cloudservice&gt;*  es nombre Hola de hello VM que se convertirá en el equipo de host de contenedor de Docker de hello en Azure
* *&lt;nombre de usuario&gt;*  es Hola nombre de usuario del usuario de raíz predeterminado de Hola de hello VM
* *&lt;contraseña&gt;*  es contraseña Hola de hello *nombre de usuario* cuenta de que cumple los estándares de Hola de complejidad de Azure

> [!NOTE]
> Actualmente, una contraseña debe tener al menos 8 caracteres, contener minúscula y una letra mayúscula, un número y un carácter especial, como uno de los siguientes caracteres de hello: `!@#$%^&+=`. No, período de hello final Hola de hello anterior frase no es un carácter especial.
> 
> 

Si el comando de hello fue correcto, debería ver algo parecido a siguientes de hello, dependiendo de los argumentos precisa de Hola y opciones que se usó:

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> Crear una máquina virtual puede tardar unos minutos, pero una vez se ha proporcionado (es el valor de estado de hello `ReadyRole`) Hola inicia de Docker daemon (Hola servicio Docker) y se puede conectar el host de contenedor de Docker toohello.
> 
> 

Hola tootest VM de Docker han creado en Azure, tipo

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

donde  *&lt;vm-nombre--usó&gt;*  es Hola nombre de máquina virtual de Hola que utilizó en la llamada demasiado`azure vm docker create`. Debería ver algo similar toohello siguientes, que indica que la máquina virtual de Host de Docker está activo y en ejecución en Azure y esperando los comandos. 

Ahora puede probar tooconnect utilizando la información de su tooobtain de cliente de docker (en algunas configuraciones de cliente de Docker, tales como los de Mac, tal vez necesite toouse `sudo`):

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

Simplemente toobe seguro de que es todo en marcha, puede examinar hello VM para hello extensión Docker:

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a>Autenticación de máquina virtual de host de Docker
Además Hola Hola toocreating VM de Docker, `azure vm docker create` comando crea también automáticamente Hola certificados necesarios tooallow su host de contenedor de Azure Docker cliente equipo tooconnect toohello que mediante HTTPS, y Hola certificados se almacenan en ambos Hola máquinas cliente y el host, según corresponda. En los intentos posteriores, se reutiliza certificados existentes de Hola y se comparten con nuevo host de Hola.

De forma predeterminada, los certificados se colocan en `~/.docker`, y Docker será toorun configurado en el puerto **2376**. Si le gustaría toouse otro puerto o directorio, puede utilizar uno de los siguientes hello `azure vm docker create` opciones de línea de comandos tooconfigure los toouse un puerto diferente de la máquina virtual de host del contenedor Docker o certificados diferentes para conectar los clientes:

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

es toolisten configurado para Hello demonio de Docker en el host de Hola y autenticar las conexiones en hello especifican puerto mediante Hola certificados generados por Hola de cliente `azure vm docker create` comando. equipo de cliente Hello debe tener estos host certificados toogain acceso toohello Docker.

> [!NOTE]
> Un host en red que se ejecuta sin estos certificados será vulnerable tooanyone que puede tooconnect toohello máquina. Antes de modificar la configuración predeterminada de hello, asegúrese de que comprende Hola riesgos tooyour equipos y aplicaciones.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* Está listo toogo toohello [Guía de usuario de Docker] y usar la máquina virtual Docker. toocreate una máquina virtual basadas en Docker en el nuevo portal de hello, consulte [cómo toouse Hola extensión de máquina virtual de Docker con hello Portal].
* Hola extensión de máquina virtual de Azure Docker también es compatible con Docker Compose, que utiliza un tootake de archivo YAML declarativa una aplicación de modelado de desarrollador en cualquier entorno y generar una implementación coherente. Vea [empezar a trabajar con Docker y toodefine de crear y ejecutar una aplicación de contenedor múltiples en una máquina virtual de Azure].  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[cómo toouse Hola extensión de máquina virtual de Docker con hello Portal]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[Guía de usuario de Docker]:https://docs.docker.com/userguide/

[empezar a trabajar con Docker y toodefine de crear y ejecutar una aplicación de contenedor múltiples en una máquina virtual de Azure]:../docker-compose-quickstart.md
