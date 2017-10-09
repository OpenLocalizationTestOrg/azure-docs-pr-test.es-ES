---
title: "clúster de aaaMonitor un servicio de contenedor de Azure con Sysdig | Documentos de Microsoft"
description: "Supervise un clúster del servicio de contenedores de Azure con Sysdig."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenedores, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a>Supervisión de un clúster del servicio de contenedores de Azure con Sysdig
En este artículo, se implementará nodos de agente de Sysdig agentes tooall hello en el clúster de servicio de contenedor de Azure. Necesita una cuenta con Sysdig para esta configuración. 

## <a name="prerequisites"></a>Requisitos previos
[Implemente](container-service-deployment.md) y [conecte](../container-service-connect.md) un clúster configurado por Azure Container Service. Explorar hello [interfaz de usuario de maratón](container-service-mesos-marathon-ui.md). Vaya demasiado[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset una cuenta de Sysdig en la nube. 

## <a name="sysdig"></a>Sysdig
Sysdig es un servicio de supervisión que le permite toomonitor los contenedores dentro de su clúster. Sysdig se conoce toohelp a solucionar el problema, pero también tiene las métricas de supervisión básicas de CPU, red, memoria y E/S. Resulta fácil toosee qué contenedores se comportan Sysdig hello más difíciles o básicamente mediante Hola mayoría de CPU y memoria. Esta vista está en la sección "Introducción", que se encuentra actualmente en versión beta de Hola. 

![Interfaz de usuario de Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a>Configuración de una implementación de Sysdig con Marathon
Estos pasos le mostrarán cómo tooconfigure e implementar aplicaciones de Sysdig tooyour clúster con maratón. 

Obtener acceso a la interfaz de usuario del controlador de dominio/OS a través de [http://localhost: 80 /](http://localhost:80/) una vez en Hola DC/OS UI vaya toohello "Universo", que se encuentra en hello inferior izquierdo y, a continuación, busque "Sysdig."

![Sysdig en Universe en DC/OS](./media/container-service-monitoring-sysdig/sysdig1.png)

En la nube ahora configuración hello toocomplete necesita un Sysdig cuenta o una cuenta de prueba gratuita. Una vez que ha iniciado sesión en el sitio Web de toohello Sysdig en la nube, haga clic en su nombre de usuario y, en la página de hello verá la "clave de acceso". 

![Clave de API de Sysdig](./media/container-service-monitoring-sysdig/sysdig2.png) 

A continuación, escriba su clave de acceso en configuración de Sysdig de hello en hello universo de DC/OS. 

![Configuración de Sysdig Hola universo de DC/OS](./media/container-service-monitoring-sysdig/sysdig3.png)

Ahora establezca Hola instancias too10000000 por lo que cada vez que se agrega un nuevo nodo de clúster toohello Sysdig implementará automáticamente un agente toothat nuevo nodo. Se trata de un toomake solución provisional seguro que sysdig implementará a tooall nuevos agentes en clúster de Hola. 

![Configuración de Sysdig Hola DC/universo de SO-instancias](./media/container-service-monitoring-sysdig/sysdig4.png)

Una vez haya instalado el paquete de hello desplácese atrás toohello Sysdig UI y podrá métricas de uso diferentes de tooexplore capaz de Hola para contenedores de hello en el clúster. 

También puede paneles específicos de Mesos y Marathon a través del [nuevo Asistente de panel](https://app.sysdigcloud.com/#/dashboards/new).
