---
title: "clúster de Azure DC/OS aaaManage con la API de REST de maratón | Documentos de Microsoft"
description: "Implementar el clúster de servicio de contenedor de Azure DC/OS tooan de contenedores mediante Hola API de REST de maratón."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Mesos, Azure
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a>Administración de contenedores de DC/OS a través de la API de REST de maratón Hola
Controlador de dominio/OS proporciona un entorno para implementar y ampliar las cargas de trabajo en clúster, mientras la abstracción de hardware subyacente Hola. Por encima de DC/OS hay un marco que administra la programación y ejecución de cargas de trabajo de proceso. Aunque los marcos están disponibles para muchas cargas de trabajo populares, este documento ofrece una introducción crear y ajustar la escala de las implementaciones de contenedor mediante el uso de API de REST de maratón Hola. 

## <a name="prerequisites"></a>Requisitos previos

Antes de trabajar con estos ejemplos, necesita un clúster de DC/OS configurado en el servicio Contenedor de Azure. También necesita clúster de toothis de conectividad remota de toohave. Para obtener más información sobre estos elementos, vea Hola siguientes artículos:

* [Implementación de un clúster del servicio Contenedor de Azure](container-service-deployment.md)
* [Conexión de clúster del servicio de contenedor de Azure tooan](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a>Hola de acceso a las API del controlador de dominio/OS
Cuando se haya conectado toohello clúster de servicio de contenedor de Azure, puede tener acceso a través del puerto http://localhost:local Hola DC/OS y las API de REST relacionadas. ejemplos de Hello en este documento se supone que está realizando un túnel en el puerto 80. Por ejemplo, se pueden alcanzar los puntos de conexión de maratón hello en URI a partir de `http://localhost/marathon/v2/`. 

Para obtener más información sobre Hola varias API, consulte la documentación de Mesosphere de Hola de hello [API maratón](https://mesosphere.github.io/marathon/docs/rest-api.html) y [Chronos API](https://mesos.github.io/chronos/docs/api.html)y la documentación de Apache de hello [Mesos API del programador ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).

## <a name="gather-information-from-dcos-and-marathon"></a>Recopilación de información de DC/OS y Marathon
Antes de implementar el clúster de contenedores toohello DC/OS, recopilar información sobre clústeres de DC/OS hello, como nombres de Hola y el estado de los agentes de Hola DC/OS. toodo por lo tanto, consultar hello `master/slaves` punto de conexión de hello API de REST de DC/OS. Si todo va bien, consulta Hola devuelve una lista de agentes de DC/OS y varias propiedades para cada uno.

```bash
curl http://localhost/mesos/master/slaves
```

Ahora, utilice Hola maratón `/apps` toocheck de punto de conexión de clúster de DC/OS de toohello de las implementaciones de aplicación actual. Si se trata de un nuevo clúster, verá una matriz vacía para las aplicaciones.

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a>Implementación de un contenedor con formato Docker
Implementar contenedores con Docker formato a través de la API de REST de maratón hello mediante un archivo JSON que describe la implementación de hello prevista. Hello en el ejemplo siguiente implementa a un agente Nginx contenedor tooa privado en clúster de Hola. 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy un contenedor con formato Docker, almacene el archivo JSON de hello en una ubicación accesible. Contenedor siguiente, de hello toodeploy, ejecute el siguiente comando de Hola. Especificar nombre de hello del archivo JSON de hello (`marathon.json` en este ejemplo).

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

salida de Hello es siguiente de toohello similar:

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

Ahora, si consulta maratón para las aplicaciones, esta nueva aplicación aparece en la salida de hello.

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a>Alcanzar contenedor Hola

Puede comprobar que hello que nginx se ejecuta en un contenedor en uno de los agentes privados de hello en clúster de Hola. host de hello toofind y el puerto donde se está ejecutando el contenedor de hello, consultar maratón hello las tareas en ejecución: 

```bash
curl localhost/marathon/v2/tasks
```

Busca el valor de Hola de `host` en la salida de hello (una dirección IP similar demasiado`10.32.0.x`) y el valor de Hola de `ports`.


Ahora, realizar una administración de toohello de conexión de terminal (no una conexión de túnel) SSH FQDN de clúster de Hola. Una vez conectado, asegúrese de hello después de la solicitud, sustituyendo los valores correctos de Hola de `host` y `ports`:

```bash
curl http://host:ports
```

Hola Nginx salida de servidor es similar a continuación toohello:

![Nginx desde el contenedor](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a>Escalado de los contenedores
Puede usar Hola maratón API tooscale out o escala en las implementaciones de aplicaciones. En el ejemplo anterior de hello, ha implementado una instancia de una aplicación. Vamos a ajustar el tamaño toothree instancias de una aplicación. toodo por lo tanto, crear un archivo JSON mediante Hola después de texto JSON y almacenarla en una ubicación accesible.

```json
{ "instances": 3 }
```

Desde la conexión de túnel, ejecute hello después tooscale comando aplicación Hola.

> [!NOTE]
> Hola URI es http://localhost/marathon/v2/apps/ seguido por Id. de Hola de hello tooscale de aplicación. Si utilizas muestra de Hola a Nginx que se proporciona aquí, Hola URI sería http://localhost/marathon/v2/apps/nginx.
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

Por último, consultar punto de conexión de hello maratón para las aplicaciones. Verá que ahora hay tres contenedores de Nginx.

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a>Comandos de PowerShell equivalentes
Puede realizar las mismas acciones mediante comandos de PowerShell en un sistema Windows.

toogather información sobre clústeres de DC/OS hello, como nombres de agente y el estado del agente, ejecute hello siguiente comando:

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

Implementar contenedores con Docker formato a través de maratón mediante un archivo JSON que describe la implementación de hello prevista. Hello en el ejemplo siguiente implementa contenedor Nginx de hello, enlazar el puerto 80 de Hola DC/OS agente tooport 80 del contenedor de Hola.

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy un contenedor con formato Docker, almacene el archivo JSON de hello en una ubicación accesible. Contenedor siguiente, de hello toodeploy, ejecute el siguiente comando de Hola. Especificar archivo JSON de toohello de ruta de acceso de hello (`marathon.json` en este ejemplo).

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

También puede utilizar Hola maratón API tooscale out o escala en las implementaciones de aplicaciones. En el ejemplo anterior de hello, ha implementado una instancia de una aplicación. Vamos a ajustar el tamaño toothree instancias de una aplicación. toodo por lo tanto, crear un archivo JSON mediante Hola después de texto JSON y almacenarla en una ubicación accesible.

```json
{ "instances": 3 }
```

Siguiente ejecución Hola comando tooscale aplicación Hola:

> [!NOTE]
> Hola URI es http://localhost/marathon/v2/apps/ seguido por Id. de Hola de hello tooscale de aplicación. Si utilizas ejemplo de Hola Nginx proporcionado aquí, Hola URI sería http://localhost/marathon/v2/apps/nginx.
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a>Pasos siguientes
* [Obtenga más información acerca de los puntos de conexión de hello Mesos HTTP](http://mesos.apache.org/documentation/latest/endpoints/)
* [Obtenga más información acerca de la API de REST de maratón Hola](https://mesosphere.github.io/marathon/docs/rest-api.html)

