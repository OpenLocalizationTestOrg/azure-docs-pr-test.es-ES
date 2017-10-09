---
title: aaaTroubleshooting instancias de contenedor de Azure
description: "Obtenga información acerca de cómo tootroubleshoot problemas con instancias de contenedor de Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/03/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: dfec636a0a174c74a6f2e9d9c4da6e871f8d2fda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a>Solución de problemas en las implementaciones en Azure Container Instances

Este artículo muestra cómo tootroubleshoot problemas al implementar contenedores tooAzure instancias de contenedor. También se describen algunos problemas comunes de hello con que puede encontrarse.

## <a name="getting-diagnostic-events"></a>Obtención de eventos de diagnóstico

registros de tooview desde el código de aplicación dentro de un contenedor, puede usar hello [registros de contenedor az](/cli/azure/container#logs) comando. Pero si el contenedor no se implementa correctamente, necesitará información de diagnóstico de tooreview Hola con un proporcionada por el proveedor de recursos de hello instancias de contenedor de Azure. eventos de hello tooview para el contenedor, ejecute el siguiente comando de hello:

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

salida de Hello incluye propiedades básicas de hello del contenedor, junto con los eventos de implementación:

```bash
{
  "containers": [
    {
      "command": null,
      "environmentVariables": [],
      "image": "microsoft/aci-helloworld",
      ...

      "events": [
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:52+00:00",
        "lastTimestamp": "2017-08-03T22:12:52+00:00",
        "message": "Pulling: pulling image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Pulled: Successfully pulled image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Created: Created container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Started: Started container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      }
    ],
    "name": "helloworld",
      "ports": [
        {
          "port": 80
        }
      ],
    ...
  ]
}
```

## <a name="common-deployment-issues"></a>Problemas comunes de implementación

Hay algunos problemas comunes relacionados con la mayoría de los errores de implementación.

### <a name="unable-toopull-image"></a>No se puede toopull imagen

Si las instancias de contenedor de Azure están toopull no se puede la imagen inicialmente, reintentar durante algún tiempo antes de cancelar al final. Si no se puede extraer la imagen de hello, se muestran los eventos como Hola siguiente:

```bash
"events": [
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:31+00:00",
    "lastTimestamp": "2017-08-03T22:19:31+00:00",
    "message": "Pulling: pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:32+00:00",
    "lastTimestamp": "2017-08-03T22:19:32+00:00",
    "message": "Failed: Failed toopull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:33+00:00",
    "lastTimestamp": "2017-08-03T22:19:33+00:00",
    "message": "BackOff: Back-off pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  }
]
```

tooresolve, eliminar el contenedor de Hola y vuelva a intentar la implementación, pago mucha atención que ha escrito el nombre de la imagen de hello correctamente.

### <a name="container-continually-exits-and-restarts"></a>El contenedor continuamente se cierra y se reinicia

Actualmente, Azure Container Instances solo admite servicios de ejecución prolongada. Si el contenedor ejecuta toocompletion y se cierra, reinicia automáticamente y se ejecuta de nuevo. Si esto ocurre, se muestran eventos como los siguientes. Tenga en cuenta que el contenedor de Hola se inicia correctamente, a continuación, reinicia rápidamente. Hello contenedor instancias API incluye un `retryCount` propiedad que muestra cuántas veces un contenedor determinado se ha reiniciado.

```bash
"events": [
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:55+00:00",
    "lastTimestamp": "2017-08-03T22:23:22+00:00",
    "message": "Pulling: pulling image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:23:23+00:00",
    "message": "Pulled: Successfully pulled image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Created: Created container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Started: Started container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Created: Created container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Started: Started container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 13,
    "firstTimestamp": "2017-08-03T22:21:59+00:00",
    "lastTimestamp": "2017-08-03T22:24:36+00:00",
    "message": "BackOff: Back-off restarting failed container",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:22:13+00:00",
    "lastTimestamp": "2017-08-03T22:22:13+00:00",
    "message": "Created: Created container with id 72e347e891290e238135e4a6b3078748ca25a1275dbbff30d8d214f026d89220",
    "type": "Normal"
  },
  ...
```

> [!NOTE]
> Mayoría imágenes de contenedor para las distribuciones de Linux establecer un shell, como intensiva de errores, como comando de hello predeterminado. Puesto que una shell por sí misma no es un servicio de ejecución prolongada, estos contenedores se cierran inmediatamente y caen en un bucle de reinicio.

### <a name="container-takes-a-long-time-toostart"></a>Contenedor toma un toostart mucho tiempo

Si el contenedor tiene un toostart mucho tiempo, pero finalmente se realiza correctamente, inicie examinando el tamaño de saludo de la imagen del contenedor. Dado que instancias de contenedor de Azure, se extrae la imagen de contenedor a petición, tiempo de inicio de hello experimenta es tooits directamente relacionada con el tamaño.

Puede ver el tamaño de hello de la imagen de contenedor con hello CLI de Docker:

```bash
docker images
```

Salida:

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

Hola tookeeping clave tamaños de las imágenes pequeños es asegurarse de que la imagen final no contiene todo lo que no es necesario en tiempo de ejecución. Una manera de toodo con [compilaciones de varias etapas](https://docs.docker.com/engine/userguide/eng-image/multistage-build/). Compilaciones de varias etapas que sea fácil tooensure que imagen final hello contiene solo artefactos de Hola que necesita para la aplicación y no los de hello adicional de contenido que se requiere en tiempo de compilación.

Hola impacto forma tooreduce Hola de extracción de la imagen de hello en tiempo de inicio del contenedor es imagen de contenedor de hello toohost con hello del registro de contenedor de Azure en hello misma región que ha previsto toouse instancias de contenedor de Azure. Esto reduce la ruta de acceso de red de Hola Hola tootravel de necesidades de imagen de contenedor, lo que reduce significativamente el tiempo de descarga de Hola.
