---
title: repositorios de registro del contenedor de aaaAzure | Documentos de Microsoft
description: "¿Cómo toouse repositorios de registro de contenedor de Azure para las imágenes de Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Repositorios de Azure Container Registry

Los registros de contenedor de Azure son compatibles con un gran número de servicios y orquestadores. toomake, servicios de código fuente de hello tootrack más fáciles y los agentes desde la que se usa el ACR, hemos comenzamos utilizando el campo de encabezado de Docker de hello en el archivo de hello Docker.config.



## <a name="viewing-repositories-in-hello-portal"></a>Ver los repositorios en hello Portal

encabezados ACR Hola tener el formato de hello:
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* cloud: Azure, Azure Stack u otras nubes de Azure específicas del gobierno o el país. Aunque las nubes de gobierno y Azure Stack no se admiten actualmente, este parámetro permite la compatibilidad en el futuro.
* Servicio: el nombre del servicio de Hola.
* Optionalservicename: el parámetro opcional para los servicios con subservicios o toospecify una SKU (ex: aplicaciones web se corresponden con/app-servicio/aplicaciones web de Azure).

Orchestrators y servicios asociados son toouse recomienda toohelp de valores de encabezado específico con nuestro la telemetría. Los usuarios también pueden modificar valor Hola pasada toohello encabezado si así lo desean.

valores de Hello queremos ACR socios toouse toopopulate Hola "X-Meta-cliente de origen" campo son los siguientes:

| Nombre de servicio              | Encabezado                                |
| ------------------------- | ------------------------------------- |
| Azure Container Service   | azure/compute/azure-container-service |
| App Service - Web Apps    | azure/app-service/web-apps            |
| App Service - Logic Apps  | azure/app-service/logic-apps          |
| Batch                     | azure/compute/batch                   |
| Cloud Console             | azure/cloud-console                   |
| Functions                 | azure/compute/functions               |
| Internet of Things - Hub  | azure/iot/hub                         |
| HDInsight                 | azure/data/hdinsight                  |
| Jenkins                   | azure/jenkins                         |
| Machine Learning          | azure/data/machile-learning           |
| Service Fabric            | azure/compute/service-fabric          |
| VSTS                      | azure/vsts                            |


## <a name="next-steps"></a>Pasos siguientes
[Obtener más información sobre los registros y Hola admite servicios y orchestrators](container-registry-intro.md)
