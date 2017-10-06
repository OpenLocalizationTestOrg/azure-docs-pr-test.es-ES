---
title: "contenedores de saldo de aaaLoad en clúster de Azure DC/OS | Documentos de Microsoft"
description: "Equilibrio de carga en varios contenedores en un clúster DC/OS de Azure Container Service."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenedores, microservicios, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a>Equilibrio de carga de contenedores en un clúster DC/OS de Azure Container Service
En este artículo, exploraremos cómo toocreate un equilibrador de carga interno en un controlador de dominio/OS administra el servicio de contenedor de Azure mediante maratón LB. Esta configuración permite que se tooscale sus aplicaciones horizontalmente. También permite tootake ventaja de clústeres de hello agente públicas y privadas mediante la colocación de los equilibradores de carga en los clústeres pública de Hola y los contenedores de la aplicación en clúster privada Hola. En este tutorial, hizo lo siguiente:

> [!div class="checklist"]
> * Configurar un equilibrador de carga de Marathon
> * Implementar una aplicación con el equilibrador de carga de Hola
> * Configurar Azure Load Balancer

Necesita un controlador de dominio ACS/OS hello toocomplete de clúster de los pasos de este tutorial. Si es necesario, este [script de ejemplo](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) puede crear uno.

Este tutorial requiere hello Azure CLI versión 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a>Introducción al equilibrio de carga

Hay dos capas de equilibrio de carga en un clúster DC/OS de Azure Container Service : 

**El equilibrador de carga Azure** proporciona puntos de entrada públicos (Hola acceder los que los usuarios finales). Una carga Equilibrada de Azure se proporciona automáticamente mediante el servicio de contenedor de Azure y es, de forma predeterminada, tooexpose configurado puerto 8080, 80 y 443.

**Hola equilibrador de carga de maratón (maratón lb)** instancias de toocontainer de solicitudes que dan servicio a estas solicitudes de entrada de las rutas. A medida que se escalan contenedores Hola proporcionar nuestro servicio web, se adapta dinámicamente Hola maratón-lb. Este equilibrador de carga no se proporciona de forma predeterminada en el servicio de contenedor, pero resulta fácil tooinstall.

## <a name="configure-marathon-load-balancer"></a>Configuración de un equilibrador de carga de Marathon

Equilibrador de carga de maratón reconfigura dinámicamente basándose en los contenedores de Hola que se han implementado. También es resistente toohello pérdida de un contenedor o un agente - si esto ocurre, Apache Mesos reinicia el contenedor de hello en otra parte y se adapta maratón lb.

Ejecute hello después de equilibrador de carga de comando tooinstall Hola maratón en clúster del agente de hello pública.

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a>Implementación de una aplicación de carga equilibrada

Ahora que tenemos el paquete de maratón lb hello, podemos implementar un contenedor de la aplicación que se desea equilibrar tooload. 

En primer lugar, obtenga Hola FQDN de los agentes de hello expuesto públicamente.

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

A continuación, cree un archivo denominado *web.json hello* y copia en hello siguiendo el contenido. Hola `HAPROXY_0_VHOST` etiqueta necesita toobe actualizado con hello FQDN de Hola DC/agentes del sistema operativo. 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

Usar Hola DC/OS CLI toorun Hola aplicación. De forma predeterminada maratón implementa Hola Hola aplicación toohello privada del clúster. Esto significa que Hola por encima de la implementación solo es accesible a través de un equilibrador de carga, que normalmente es el comportamiento deseado de Hola.

```azurecli-interactive
dcos marathon app add hello-web.json
```

Una vez que se ha implementado la aplicación hello, examinar toohello FQDN de aplicación con equilibrio de carga de hello agent clúster tooview.

![Imagen de la aplicación de carga equilibrada](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a>Configuración de Azure Load Balancer

De forma predeterminada, Azure Load Balancer expone los puertos 80, 8080 y 443. Si usa uno de estos tres puertos (tal como lo hacemos en hello ejemplo anterior), no hay nada que necesita toodo. Debe ser capaz de toohit el agente de FQDN del equilibrador de carga, y cada vez que actualice, podrá alcance uno de los servidores web de tres en un modo round-robin. 

Si utiliza un puerto diferente, debe tooadd round robin regla y un sondeo del equilibrador de carga de hello para el puerto de Hola que usó. Puede hacerlo desde hello [CLI de Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), con los comandos de hello `azure network lb rule create` y `azure network lb probe create`.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido acerca de equilibrio de carga en ACS con maratón hello y carga de Azure equilibradores incluidos Hola siguientes acciones:

> [!div class="checklist"]
> * Configurar un equilibrador de carga de Marathon
> * Implementar una aplicación con el equilibrador de carga de Hola
> * Configurar Azure Load Balancer

Avanzar toohello toolearn de tutorial siguiente sobre la integración de almacenamiento de Azure con controlador de dominio/OS en Azure.

> [!div class="nextstepaction"]
> [Montaje del recurso compartido de archivos de Azure en un clúster de DC/OS](container-service-dcos-fileshare.md)