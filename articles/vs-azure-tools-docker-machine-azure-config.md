---
title: "aaaCreate Docker se hospeda en Azure con Docker máquina | Documentos de Microsoft"
description: "Describe el uso de los hosts de máquina Docker toocreate docker en Azure."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a>Creación de hosts de Docker en Azure con docker-machine
Ejecuta [Docker](https://www.docker.com/) contenedores requiere un demonio de docker host VM ejecución Hola.
Este tema se describe cómo hello toouse [máquina docker](https://docs.docker.com/machine/) comando toocreate nuevas máquinas virtuales de Linux, configurada con hello demonio de Docker, se está ejecutando en Azure. 

**Nota:** 

* *Este artículo depende de la versión 0.9.0-rc2 de docker-machine, o de una versión superior*
* *Se admitirán los contenedores de Windows a través de la máquina de docker en hello futuro próximo*

## <a name="create-vms-with-docker-machine"></a>Creación de VM con la máquina de Docker
Crear máquinas virtuales del host docker en Azure con hello `docker-machine create` comando con hello `azure` controlador. 

Hola controlador Azure requiere el identificador de suscripción. Puede usar hello [CLI de Azure](cli-install-nodejs.md) o hello [Portal de Azure](https://portal.azure.com) tooretrieve su suscripción de Azure. 

**Uso de hello Portal de Azure**

* Seleccione **suscripciones** de hello izquierdo página y copiar Hola Id. de suscripción.

**Uso de hello CLI de Azure**

* Tipo ```azure account list``` y el Id. de suscripción de Hola de copia.

Tipo `docker-machine create --driver azure` toosee Hola opciones y sus valores predeterminados.
También puede ver hello [documentación del controlador de Azure Docker](https://docs.docker.com/machine/drivers/azure/) para obtener más información. 

Hello siguiente ejemplo se basa en hello [valores predeterminados](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), pero si lo desea establecer estos valores: 

* dns de Azure para nombre de hello asociado con la dirección IP pública de Hola y certificados generados. Este es el nombre DNS de saludo de la máquina virtual. Hola VM puede, a continuación, con seguridad detener, versión IP dinámicas de Hola y proporcionar Hola capacidad tooreconnect después Hola vm se inicia de nuevo con una dirección IP nueva. prefijo del nombre de Hello debe ser único para esa región UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.
* abrir el puerto 80 en hello VM para el acceso a internet saliente
* tamaño de almacenamiento de máquina virtual tooutilize más rápido premium hello
* almacenamiento Premium usarse como disco de máquina virtual de Hola

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a>Elección de un host de Docker con una docker-machine
Una vez que tenga una entrada en la máquina de docker para el host, puede establecer el host predeterminado de hello cuando ejecuta comandos de docker.

## <a name="using-powershell"></a>Con PowerShell
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a>Con Bash
```bash
eval $(docker-machine env MyDockerHost)
```

Ahora puede ejecutar comandos de docker en host especificado Hola

```
docker ps
docker info
```

## <a name="run-a-container"></a>Ejecución de un contenedor
Con un host configurado, ahora puede ejecutar un tootest de servidor web simple si el host se configuró correctamente.
Aquí se usa una imagen de nginx estándar, especifique que debe escuchar en el puerto 80, y que si se reinicia la máquina virtual del host de hello, contenedor Hola reiniciarán también (`--restart=always`). 

```bash
docker run -d -p 80:80 --restart=always nginx
```

salida de Hello debe tener un aspecto similar Hola siguiente:

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a>Contenedor de prueba Hola
Examine los contenedores en ejecución mediante `docker ps`:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

Toosee hello y ejecución de contenedor, tipo `docker-machine ip <VM name>` tooenter de dirección IP toofind hello en el Explorador de hello:

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Ejecución del contenedor ngnix](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a>Resumen
Con docker-machine se pueden aprovisionar fácilmente hosts de Docker en Azure para las validaciones de host de Docker individuales.
Para la producción de hospedaje de contenedores, vea hello [servicio de contenedor de Azure](http://aka.ms/AzureContainerService)

toodevelop .NET Core aplicaciones con Visual Studio, vea [Docker Tools para Visual Studio](http://aka.ms/DockerToolsForVS)

