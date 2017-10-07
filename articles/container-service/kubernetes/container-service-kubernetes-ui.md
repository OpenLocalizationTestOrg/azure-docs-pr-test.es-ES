---
title: "aaaManage Kubernetes de Azure de clúster con la interfaz de usuario web | Documentos de Microsoft"
description: Con hello Kubernetes web interfaz de usuario en el servicio de contenedor de Azure
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a>Con hello Kubernetes web interfaz de usuario con el servicio de contenedor de Azure

## <a name="prerequisites"></a>Requisitos previos
En este tutorial se da por supuesto que ha [creado un clúster de Kubernetes con Azure Container Service](container-service-kubernetes-walkthrough.md).


También se supone que dispone de hello Azure CLI 2.0 y `kubectl` herramientas instaladas.

Puede probar si tiene hello `az` instalada mediante la ejecución de la herramienta:

```console
$ az --version
```

Si no tienes hello `az` herramienta instalada, se ofrecen instrucciones [aquí](https://github.com/azure/azure-cli#installation).

Puede probar si tiene hello `kubectl` instalada mediante la ejecución de la herramienta:

```console
$ kubectl version
```

Si no tiene la herramienta `kubectl` instalada, puede ejecutar:

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a>Información general

### <a name="connect-toohello-web-ui"></a>Conecte la interfaz de usuario de web toohello
Para iniciar la interfaz de usuario de web de hello Kubernetes ejecutando:

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

Se debería abrir un web explorador configurado tootalk tooa segura proxy que se conecta la interfaz de usuario de la web de Kubernetes toohello de equipo local.

### <a name="create-and-expose-a-service"></a>Creación y exposición de un servicio
1. En la interfaz de usuario del web Kubernetes hello, haga clic en **crear** botón en hello superior derecho de la ventana.

    ![Interfaz de usuario de creación de Kubernetes](./media/container-service-kubernetes-ui/create.png)

    Se debería abrir un cuadro de diálogo en el que puede comenzar a crear la aplicación.

2. Asígnele el nombre hello `hello-nginx`. Hola de uso [ `nginx` contenedor de Docker](https://hub.docker.com/_/nginx/) e implementar tres réplicas de este servicio web.

    ![Cuadro de diálogo de creación de pod de Kubernetes](./media/container-service-kubernetes-ui/nginx.png)

3. En **Service** (Servicio), seleccione **External** (Externo) y escriba el puerto 80.

    Esta configuración equilibra la carga toohello tres réplicas de tráfico.

    ![Cuadro de diálogo de creación del servicio de Kubernetes](./media/container-service-kubernetes-ui/service.png)

4. Haga clic en **implementar** toodeploy estos contenedores y los servicios.

    ![Implementación de Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a>Visualización de los contenedores
Tras hacer clic en **implementar**, Hola interfaz de usuario muestra una vista de su servicio tal y como se implementa:

![Estado de Kubernetes](./media/container-service-kubernetes-ui/status.png)

Puede ver estado de Hola de cada objeto Kubernetes en círculo hello en el lado izquierdo de saludo de la interfaz de usuario, en **pod**. Si es un círculo parcialmente completo, objeto de hello todavía está implementando. Cuando un objeto está totalmente implementado, muestra una marca de verificación verde:

![Implementación de Kubernetes](./media/container-service-kubernetes-ui/deployed.png)

Una vez que todo funciona, haga clic en uno de los detalles de toosee pod sobre Hola ejecutando el servicio web.

![Pod de Kubernetes](./media/container-service-kubernetes-ui/pods.png)

Hola **pod** vista, puede ver información acerca de los contenedores de hello en pod hello, así como recursos de CPU y memoria de hello usados por los contenedores:

![Recursos de Kubernetes](./media/container-service-kubernetes-ui/resources.png)

Si no ve los recursos de hello, puede necesitar toowait unos minutos para hello toopropagate de datos de supervisión.

registros de hello toosee para el contenedor, haga clic en **ver registros**.

![Registros de Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a>Visualización del servicio
En suma toorunning los contenedores, hello Kubernetes UI ha creado una referencia externa `Service` que proporciona un contenedor de toohello carga equilibrador toobring tráfico en el clúster.

En el panel de navegación izquierdo de hello, haga clic en **servicios** tooview todos los servicios (debería haber sólo uno).

![Servicios de Kubernetes](./media/container-service-kubernetes-ui/service-deployed.png)

En la vista, debería ver un extremo externo (dirección IP) que se ha asignado el servicio tooyour.
Si hace clic en esa dirección IP, debería ver el contenedor de Nginx que se ejecuta detrás del equilibrador de carga.

![vista de nginx](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a>Cambio del tamaño del servicio
En suma tooviewing los objetos en Hola interfaz de usuario, puede editar y actualizar objetos de la API de Kubernetes Hola.

En primer lugar, haga clic en **implementaciones** Hola dejado la implementación de Hola de toosee de panel de navegación para el servicio.

Una vez que esté en esa vista, haga clic en el conjunto de réplicas de hello y, a continuación, haga clic en **editar** en la barra de navegación superior de hello:

![Edición de Kubernetes](./media/container-service-kubernetes-ui/edit.png)

Editar hello `spec.replicas` campo toobe `2`y haga clic en **actualización**.

Esto hace que número Hola de réplicas toodrop tootwo mediante la eliminación de uno de los conjuntos de pod.

 

