---
title: "clúster de Azure Kubernetes aaaMonitor - administración de operaciones | Documentos de Microsoft"
description: "Supervisión de un clúster de Kubernetes en Azure Container Service utilizando Microsoft Operations Management Suite"
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
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a>Supervisión de un clúster de Azure Container Service con Microsoft Operations Management Suite (OMS)

## <a name="prerequisites"></a>Requisitos previos
En este tutorial se da por supuesto que ha [creado un clúster de Kubernetes con Azure Container Service](container-service-kubernetes-walkthrough.md).

También se supone que dispone de hello `az` cli de Azure y `kubectl` herramientas instaladas.

Puede probar si tiene hello `az` instalada mediante la ejecución de la herramienta:

```console
$ az --version
```

Si no tienes hello `az` herramienta instalada, se ofrecen instrucciones [aquí](https://github.com/azure/azure-cli#installation).  
Como alternativa, puede usar [Shell en la nube de Azure](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), que tiene hello `az` cli de Azure y `kubectl` herramientas ya instaladas automáticamente.  

Puede probar si tiene hello `kubectl` instalada mediante la ejecución de la herramienta:

```console
$ kubectl version
```

Si no tiene la herramienta `kubectl` instalada, puede ejecutar:
```console
$ az acs kubernetes install-cli
```

tootest si tiene claves kubernetes instaladas en la herramienta kubectl puede ejecutar:
```console
$ kubectl get nodes
```

Si hello por encima de los errores de comando out, necesita claves de clúster de tooinstall kubernetes en la herramienta kubectl. Puede hacerlo con hello siguiente comando:
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a>Supervisión de contenedores con Operations Management Suite (OMS)

Microsoft Operations Management (OMS) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura en la nube y local. Solución de contenedor es una solución de análisis de registros de OMS, que le ayuda a ver el inventario de contenedor de hello, rendimiento y los registros en una sola ubicación. Puede auditar, solucionar los contenedores viendo Hola registros en una ubicación centralizada y encontrar con ruido consumiendo exceso contenedor en un host.

![](media/container-service-monitoring-oms/image1.png)

Para obtener más información acerca de la solución de contenedor, consulte toothe [análisis de registros de solución de contenedor](../../log-analytics/log-analytics-containers.md).

## <a name="installing-oms-on-kubernetes"></a>Instalación de OMS en Kubernetes

### <a name="obtain-your-workspace-id-and-key"></a>Obtención de la clave y el identificador de área de trabajo
Para el servicio OMS agente tootalk toohello Hola debe toobe configurado con un identificador de área de trabajo y una clave de área de trabajo. cuenta de Id. de área de trabajo de hello tooget y clave necesita toocreate un OMS <https://mms.microsoft.com>. Siga Hola pasos toocreate una cuenta. Una vez que haya terminado de crear cuenta de hello, necesita tooobtain el identificador y la clave haciendo clic en **configuración**, a continuación, **orígenes conectados**y, a continuación, **servidores Linux**, tal y como se muestra a continuación.

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a>Instalar a agente OMS de hello mediante un DaemonSet
DaemonSets usan Kubernetes toorun una sola instancia de un contenedor en cada host de clúster de Hola.
Son perfectos para ejecutar agentes de supervisión.

Aquí es hello [archivo DaemonSet YAML](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes). Guárdelo con el nombre archivo tooa `oms-daemonset.yaml` y reemplazar los valores de marcador de posición de Hola para `WSID` y `KEY` con el Id. de área de trabajo y la clave en el archivo hello.

Cuando haya agregado su Id. de área de trabajo y la configuración de DaemonSet toohello clave, puede instalar agente OMS de hello en el clúster con hello `kubectl` herramienta de línea de comandos:

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a>Instalar agente OMS Hola usar un secreto Kubernetes
tooprotect el Id. de área de trabajo OMS y la clave que se puede usar Kubernetes secreto como parte del archivo DaemonSet YAML.

 - Copiar script de Hola, archivo de plantilla secreto y Hola archivo DaemonSet YAML (de [repositorio](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) y asegúrese de que se encuentren en hello mismo directorio. 
      - Script de generación de secretos: secret-gen.sh
      - Plantilla de secretos: secret-template.yaml
   - Archivo DaemonSet YAML: omsagent-ds-secrets.yaml
 - Ejecutar script de Hola. script de Hola le pedirá Hola Id. de área de trabajo de OMS y la clave principal. Por favor, inserte y script de Hola creará un archivo yaml secreto para que pueda ejecutar.   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - Crear pod de secretos de hello ejecutando Hola siguiente:``` kubectl create -f omsagentsecret.yaml ```
 
   - toocheck, ejecute hello siguiente: 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - Ejecute ``` kubectl create -f omsagent-ds-secrets.yaml ``` para crear el daemon-set de omsagent

### <a name="conclusion"></a>Conclusión
Eso es todo. Después de unos minutos, debe tener datos toosee pueda fluir tooyour panel de OMS.
