---
title: "clúster de Azure DC/OS aaaMonitor - Datadog | Documentos de Microsoft"
description: "Supervise un clúster del servicio de contenedores de Azure con Datadog. Usar Hola DC/OS web UI toodeploy hello Datadog agentes tooyour clúster."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenedores, DC/OS, Docker Swarm, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a>Supervisión de un clúster de DC/OS de Azure Container Service con Datadog
En este artículo se implementará nodos de agente de Datadog agentes tooall hello en el clúster de servicio de contenedor de Azure. Necesita una cuenta con Datadog para esta configuración. 

## <a name="prerequisites"></a>Requisitos previos
[Implemente](container-service-deployment.md) y [conecte](../container-service-connect.md) un clúster configurado por Azure Container Service. Explorar hello [interfaz de usuario de maratón](container-service-mesos-marathon-ui.md). Vaya demasiado[http://datadoghq.com](http://datadoghq.com) tooset una cuenta de Datadog. 

## <a name="datadog"></a>Datadog
Datadog es un servicio de supervisión que recopila datos de supervisión de los contenedores dentro del clúster del servicio de contenedor de Azure. Datadog tiene un panel de integración de Docker donde puede ver las métricas específicas dentro de los contenedores. Las métricas que se recopilan de los contenedores están organizadas por CPU, memoria, red y E/S. Datadog divide las métricas en contenedores e imágenes. Un ejemplo del programa Hola a qué interfaz de usuario parece para CPU uso esté por debajo.

![Interfaz de usuario de Datadog](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a>Configuración de una implementación de Datadog con Marathon
Estos pasos le mostrarán cómo tooconfigure e implementar aplicaciones de Datadog tooyour clúster con maratón. 

Acceda a la interfaz de usuario de DC/OS mediante [http://localhost:80/](http://localhost:80/). Una vez en hello navegar por la interfaz de usuario del controlador de dominio/OS toohello "Universo" que se encuentra en hello inferior izquierdo y, a continuación, busque "Datadog" y haga clic en "Instalar".

![Paquete de Datadog dentro de hello universo de DC/OS](./media/container-service-monitoring/datadog1.png)

Ahora toocomplete Hola configuración necesitará una cuenta de Datadog o una cuenta de prueba gratuita. Una vez que ha iniciado sesión en el sitio Web de Datadog toohello buscar toohello izquierda y vaya tooIntegrations ->, a continuación, [API](https://app.datadoghq.com/account/settings#api). 

![Clave de API de Datadog](./media/container-service-monitoring/datadog2.png)

A continuación, escriba la clave de API en configuración de Datadog de hello en hello universo de DC/OS. 

![Configuración de Datadog Hola universo de DC/OS](./media/container-service-monitoring/datadog3.png) 

Hola por encima de la configuración de instancias se establecen too10000000 por lo que cada vez que se agrega un nuevo nodo de clúster toohello Datadog implementará automáticamente un nodo de toothat de agente. Se trata de una solución provisional. Una vez haya instalado el paquete de hello debe navegar por el sitio Web de Datadog toohello atrás y busque "[paneles](https://app.datadoghq.com/dash/list)." Desde allí, verá los paneles de integración y personalizados. Hola [panel Docker](https://app.datadoghq.com/screen/integration/docker) tendrá todas las métricas de contenedor de Hola que necesita para supervisar el clúster. 

