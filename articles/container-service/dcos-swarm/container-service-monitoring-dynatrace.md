---
title: "clúster de Azure DC/OS aaaMonitor - Dynatrace | Documentos de Microsoft"
description: "Supervisión de un clúster de Azure Container Service DC/OS con Dynatrace. Implementar hello Dynatrace OneAgent mediante el panel de Hola DC/OS."
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: Contenedores, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a>Supervisión de un clúster DC/OS de Azure Container Service con Dynatrace SaaS/Managed
En este artículo, le mostraremos cómo hello toodeploy [Dynatrace](https://www.dynatrace.com/) Hola a OneAgent toomonitor todos los nodos de agente en el clúster de servicio de contenedor de Azure. Necesita una cuenta con Dynatrace SaaS/Managed para esta configuración. 

## <a name="dynatrace-saasmanaged"></a>Dynatrace SaaS/Managed
Dynatrace es una solución de supervisión nativa en la nube para entornos de clúster y contenedor muy dinámicos. Le permite toobetter optimizar las implementaciones de contenedor y las asignaciones de memoria mediante datos de uso en tiempo real. Permite indicar automáticamente los problemas de infraestructura y aplicación proporcionando una línea de base automatizada, la correlación de problemas y la detección de la causa raíz.

Hola siguiente figura se muestra hello Dynatrace UI:

![Interfaz de usuario de Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a>Requisitos previos 
[Implementar](container-service-deployment.md) y [conectar](./../container-service-connect.md) clúster tooa configurado mediante el servicio de contenedor de Azure. Explorar hello [interfaz de usuario de maratón](container-service-mesos-marathon-ui.md). Vaya demasiado[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset una cuenta de Dynatrace SaaS.  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a>Configuración de una implementación de Dynatrace con Marathon
Estos pasos le mostrarán cómo tooconfigure e implementar aplicaciones de Dynatrace tooyour clúster con maratón.

1. Acceda a la interfaz de usuario de DC/OS mediante [http://localhost:80/](http://localhost:80/). Una vez en hello interfaz de usuario del controlador de dominio/OS, navegue toohello **universo** ficha y, a continuación, busque **Dynatrace**.

    ![Dynatrace en Universe (Universo) en DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. configuración de hello toocomplete, necesita una cuenta de Dynatrace SaaS o una cuenta de prueba gratuita. Una vez que ha iniciado sesión en el panel de Dynatrace hello, seleccione **Dynatrace implementar**.

    ![Integración de PaaS de configuración de Dynatrace](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. En la página de hello, seleccione **configurar la integración de PaaS**. 

    ![Token de la API de Dynatrace](./media/container-service-monitoring-dynatrace/api-token.png) 

4. Escriba el símbolo (token) de API en hello Dynatrace OneAgent configuración dentro de Hola DC/OS universo. 

    ![Configuración de Dynatrace OneAgent Hola universo de DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. Establecer instancias de hello toohello número de nodos piensa toorun. Establece a un número mayor también funciona, pero el controlador de dominio/OS seguirá intentando toofind nuevas instancias hasta que realmente se alcanza ese número. Si lo prefiere, también puede establecer este valor tooa como 1000000. En este caso, cada vez que se agrega un nuevo nodo clúster toohello, Dynatrace implementa automáticamente un agente toothat nuevo nodo, a un precio de Hola de DC/OS probar constantemente instancias adicionales de toodeploy.

    ![Configuración de Dynatrace Hola DC/universo de SO-instancias](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a>Pasos siguientes

Una vez haya instalado el paquete de hello, desplácese atrás toohello Dynatrace panel. Puede explorar las métricas de uso distintos de Hola para contenedores de hello en el clúster. 
