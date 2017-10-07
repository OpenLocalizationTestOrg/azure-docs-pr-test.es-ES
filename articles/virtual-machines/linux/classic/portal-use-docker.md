---
title: "Extensión de máquina virtual de Docker para Linux aaaUsing | Documentos de Microsoft"
description: "Describe Docker y las extensiones de máquinas virtuales de Azure de Hola y cómo toocreate máquinas virtuales de Azure que son hosts de docker mediante Hola CLI de Azure en el modelo de implementación clásica."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a>Uso de hello extensión de máquina virtual de Docker con hello portal de Azure clásico
> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

[Docker](https://www.docker.com/) es uno de hello más populares enfoques de virtualización que utiliza [contenedores Linux](http://en.wikipedia.org/wiki/LXC) en lugar de máquinas virtuales como una manera de aislar los datos y calcular en recursos compartidos. Puede utilizar la extensión de máquina virtual Docker Hola administrado por [agente Linux de Azure] toocreate una máquina virtual de Docker que hospeda cualquier número de contenedores para las aplicaciones en Azure.

> [!NOTE]
> Este tema describe cómo toocreate una máquina virtual Docker desde Hola portal de Azure clásico. toosee toocreate una VM de Docker en línea de comandos de hello, vea [cómo toouse Hola extensión de máquina virtual Docker de hello Azure interfaz de línea de comandos (CLI de Azure)]. toosee un análisis de alto nivel de los contenedores y sus ventajas, vea hello [Docker alto nivel Pizarra](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a>Crear una nueva máquina virtual de hello Galería de imágenes
Hola primer paso requiere una máquina virtual de Azure desde una imagen de Linux que admite Hola extensión de máquina virtual de Docker, mediante una imagen de Ubuntu 14.04 LTS de hello Galería de imágenes como una imagen de servidor de ejemplo y Ubuntu 14.04 escritorio como un cliente. En el portal de hello, haga clic en **+ nuevo** Hola inferior izquierda esquina toocreate una nueva instancia de máquina virtual y seleccione una imagen de Ubuntu 14.04 LTS de selecciones de hello disponibles o de hello completa Galería de imágenes, tal y como se muestra a continuación.

> [!NOTE]
> Actualmente, sólo Ubuntu 14.04 LTS las imágenes más recientes de julio de 2014 admiten Hola extensión de máquina virtual de Docker.
> 
> 

![Creación de una imagen Ubuntu](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a>Creación de certificados de Docker
Después de Hola se ha creado la máquina virtual, asegúrese de que Docker está instalado en el equipo cliente. (Para obtener detalles, consulte [Instrucciones de instalación de Docker](https://docs.docker.com/installation/#installation)).

Crear archivos de certificado y la clave para la comunicación de Docker según demasiado de hello[ejecutar Docker con https] y colocarlas en hello  **`~/.docker`**  directorio en el equipo cliente.

> [!NOTE]
> Hola extensión de máquina virtual de Docker en el portal de hello actualmente requiere credenciales que están codificados con base64.
> 
> 

En la línea de comandos de hello, use  **`base64`**  o favorito otra codificación temas de herramienta toocreate con codificación base64. Si hace esto con un sencillo conjunto de archivos de certificado y la clave podría ser toothis similar:

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a>Agregar extensión de máquina virtual Docker Hola
tooadd Hola extensión de máquina virtual de Docker, busque la instancia VM de Hola que ha creado y desplácese hacia abajo demasiado**extensiones** y haga clic en él toobring las extensiones de máquina virtual, tal y como se muestra a continuación.

> [!NOTE]
> Esta funcionalidad se admite en el portal de vista previa de hello solo: https://portal.azure.com/
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a>Adición de una extensión
Haga clic en hello **+ agregar** toodisplay Hola posibles extensiones de VM, puede agregar toothis máquina virtual.

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a>Seleccione Hola extensión de máquina virtual Docker
Elija Hola extensión de máquina virtual de Docker, que ofrece una descripción de Docker de Hola y vínculos importantes, y, a continuación, haga clic en **crear** en el procedimiento de instalación de hello inferior toobegin Hola.

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a>Adición de los archivos de certificado y clave:
Hola campos de formulario, escriba las versiones con codificación base64 de Hola de su certificado de CA, el certificado de servidor y la clave del servidor, tal y como se muestra en el siguiente gráfico de Hola.

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> Tenga en cuenta que (como en Hola anterior imagen) Hola 2376 se rellena de forma predeterminada. Puede escribir cualquier extremo aquí, pero Hola siguiente paso será tooopen seguridad Hola coincidencia de punto de conexión. Si cambia de forma predeterminada hello, asegúrese de tooopen seguro seguridad Hola que coincidan con el extremo en el paso siguiente de saludo.
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a>Agregar Hola extremo de comunicación de Docker
Al ver el grupo de recursos de Hola que haya creado, seleccione Hola grupo de seguridad de red asociado a la máquina virtual y haga clic en **reglas de seguridad de entrada** tooview Hola reglas como se muestra aquí.

![](media/portal-use-docker/AddingEndpoint.png)

Haga clic en **+ agregar** tooadd otra regla y en caso de hello predeterminado, escriba un nombre para el extremo de hello (en este ejemplo, **Docker**) y 2376 'intervalo de puertos del destino'. Establecer mostrando de valor de protocolo de hello **TCP**y haga clic en **Aceptar** regla de toocreate Hola.

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a>Comprobación del cliente de Docker y del host de Docker de Azure
Busque y copie Hola nombre de dominio de la máquina virtual y en línea de comandos de hello del equipo cliente, tipo `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (donde *dockerextension* se sustituye por hello subdominio para la máquina virtual).

resultado de Hello debe aparecer toothis similar:

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

Cuando se haya completado Hola por encima de los pasos, ahora tiene un host Docker totalmente funcional que se ejecuta en una máquina virtual de Azure, configurado toobe conectado tooremotely desde otros clientes.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
Está listo toogo toohello [Guía de usuario de Docker] y usar la máquina virtual Docker. Si desea tooautomate creación de hosts de Docker en máquinas virtuales de Azure a través de la interfaz de línea de comandos, vea [cómo toouse Hola extensión de máquina virtual Docker de hello Azure interfaz de línea de comandos (CLI de Azure)]

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[cómo toouse Hola extensión de máquina virtual Docker de hello Azure interfaz de línea de comandos (CLI de Azure)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[agente Linux de Azure]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[ejecutar Docker con https]:http://docs.docker.com/articles/https/
[Guía de usuario de Docker]:https://docs.docker.com/userguide/
