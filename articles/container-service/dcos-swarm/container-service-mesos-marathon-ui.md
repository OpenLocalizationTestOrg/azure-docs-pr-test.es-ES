---
title: "clúster de Azure DC/OS aaaManage con interfaz de usuario de maratón | Documentos de Microsoft"
description: "Implementar el servicio de Cluster Server de contenedores tooan servicio de contenedor de Azure mediante el uso de la interfaz de usuario de web de maratón Hola."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a>Administrar un clúster de servicio de contenedor de Azure DC/OS a través de la interfaz de usuario de web de maratón Hola
Controlador de dominio/OS proporciona un entorno para implementar y ampliar las cargas de trabajo en clúster, mientras la abstracción de hardware subyacente Hola. Por encima de DC/OS hay un marco que administra la programación y ejecución de cargas de trabajo de proceso.

Mientras los marcos están disponibles para muchas cargas de trabajo populares, este documento describe cómo tooget introducción sobre cómo implementar contenedores con maratón. 


## <a name="prerequisites"></a>Requisitos previos
Antes de trabajar con estos ejemplos, necesita un clúster de DC/OS configurado en el servicio Contenedor de Azure. También necesita clúster de toothis de conectividad remota de toohave. Para obtener más información sobre estos elementos, vea Hola siguientes artículos:

* [Implementación de un clúster del servicio Contenedor de Azure](container-service-deployment.md)
* [Conectar el clúster del servicio de contenedor de Azure tooan](../container-service-connect.md)

> [!NOTE]
> En este artículo se da por supuesto que está realizando un túnel clúster de DC/OS toohello a través de su puerto local 80.
>

## <a name="explore-hello-dcos-ui"></a>Explorar Hola interfaz de usuario del controlador de dominio/OS
Con un túnel de Shell seguro (SSH) [establece](../container-service-connect.md), examinar toohttp://localhost/. Esto carga la interfaz de usuario de web de Hola DC/OS y muestra información sobre el clúster de hello, como los recursos usados, activos agentes y servicios en ejecución.

![Interfaz de usuario de DC/OS](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a>Explorar Hola maratón UI
Hola toosee maratón de interfaz de usuario, busque toohttp://localhost/marathon. Desde esta pantalla, puede iniciar un nuevo contenedor u otra aplicación en clúster del servicio de contenedor de Azure DC/OS Hola. También puede ver información acerca de cómo ejecutar contenedores y aplicaciones.  

![Interfaz de usuario de Marathon](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a>Implementación de un contenedor con formato Docker
toodeploy un nuevo contenedor mediante el uso de maratón, haga clic en **crear aplicación**y escriba Hola siguiente información en las fichas del formulario hello:

| Campo | Valor |
| --- | --- |
| ID |nginx |
| Memoria | 32 |
| Imagen |nginx |
| Red |Bridged |
| Puerto de host |80 |
| Protocol |TCP |

![Nueva interfaz de usuario de la aplicación: General](./media/container-service-mesos-marathon-ui/dcos4.png)

![Nueva interfaz de usuario de la aplicación: Contenedor de Docker](./media/container-service-mesos-marathon-ui/dcos5.png)

![Nueva interfaz de usuario de la aplicación: Detección de servicios y puertos](./media/container-service-mesos-marathon-ui/dcos6.png)

Si desea toostatically mapa Hola contenedor tooa puerto en el agente de hello, deberá toouse modo de JSON. toodo cambiar por lo tanto, Asistente para la nueva aplicación Hola demasiado**JSON modo** mediante el uso de alternancia de Hola. A continuación, escriba Hola después de la configuración en hello `portMappings` sección de definición de la aplicación hello. Este ejemplo enlaza el puerto 80 de hello contenedor tooport 80 del agente de Hola DC/OS. Puede volver a cambiar el modo JSON del Asistente después de realizar este cambio.

```none
"hostPort": 80,
```

![Nueva interfaz de usuario de la aplicación: Ejemplo con el puerto 80](./media/container-service-mesos-marathon-ui/dcos13.png)

Si desea que las comprobaciones de mantenimiento tooenable, establezca una ruta de acceso en hello **comprobaciones de mantenimiento** ficha.

![Interfaz de usuario para nueva aplicación: comprobaciones de estado](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

clúster de DC/OS Hola se implementa con conjunto de agentes públicos y privados. Para hello toobe tooaccess capaz de las aplicaciones de clúster de hello Internet, deberá a agente pública de toodeploy Hola aplicaciones tooa. toodo por lo tanto, seleccione hello **opcional** ficha del Asistente para nueva aplicación de Hola y escriba **slave_public** para hello **aceptado recursos Roles**.

Haga clic en **Create Application** (Crear aplicación).

![Nueva interfaz de usuario de la aplicación: Configuración del agente público](./media/container-service-mesos-marathon-ui/dcos14.png)

En página principal de maratón de hello, podrá ver el estado de implementación de hello para el contenedor de Hola. Inicialmente verá un estado **Deploying** (Implementando). Después de una implementación correcta, Hola cambios de estado demasiado**ejecutando**.

![Página principal de la interfaz de usuario de Marathon: Estado de la implementación del contenedor](./media/container-service-mesos-marathon-ui/dcos7.png)

Cuando se cambia (http://localhost/) de la interfaz de usuario de la web de DC/OS toohello atrás, verá que se está ejecutando una tarea (en este caso, un contenedor con Docker formato) en clúster de Hola DC/OS.

![Interfaz de usuario, tarea que se ejecuta en el clúster de hello web de DC/OS](./media/container-service-mesos-marathon-ui/dcos8.png)

nodo del clúster hello toosee Hola tarea se ejecuta en, haga clic en hello **nodos** ficha.

![Interfaz de usuario web de DC/OS: nodo de clúster de la tarea](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a>Alcanzar contenedor Hola

En este ejemplo, se ejecuta la aplicación de hello en un nodo de agente pública. Alcanzar la aplicación hello de hello internet examinando toohello agente FQDN del clúster de hello: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, donde:

* **DNSPREFIX** es Hola prefijo DNS que proporcionó al implementar el clúster de Hola.
* **REGIÓN** es región hello en el que se encuentra el grupo de recursos.

    ![Nginx de Internet](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a>Pasos siguientes
* [Trabajar con el controlador de dominio/OS y Hola maratón API](container-service-mesos-marathon-rest.md)

* Profundización en el servicio de contenedor de Azure con Mesos Hola

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
