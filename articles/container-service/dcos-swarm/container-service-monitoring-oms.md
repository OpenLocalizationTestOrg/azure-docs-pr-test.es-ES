---
title: "clúster de Azure DC/OS aaaMonitor - administración de operaciones | Documentos de Microsoft"
description: "Uso de Microsoft Operations Management Suite para supervisar un clúster DC/OS de Azure Container Service."
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a>Uso de Operations Management Suite para supervisar un clúster DC/OS de Azure Container Service

Microsoft Operations Management Suite (OMS) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura local y en la nube. Solución de contenedor es una solución de análisis de registros de OMS, que le ayuda a ver el inventario de contenedor de hello, rendimiento y los registros en una sola ubicación. Puede auditar, solucionar los contenedores viendo Hola registros en una ubicación centralizada y encontrar con ruido consumiendo exceso contenedor en un host.

![](media/container-service-monitoring-oms/image1.png)

Para obtener más información acerca de la solución de contenedor, consulte toothe [análisis de registros de solución de contenedor](../../log-analytics/log-analytics-containers.md).

## <a name="setting-up-oms-from-hello-dcos-universe"></a>Configuración de OMS desde el universo de Hola DC/OS


Este artículo se supone que ha configurado un controlador de dominio/OS y ha implementado aplicaciones de contenedor de web simple en el clúster de Hola.

### <a name="pre-requisite"></a>Requisito previo
- [Suscripción de Microsoft Azure](https://azure.microsoft.com/free/) (se puede obtener de gratis).  
- Configuración de área de trabajo de Microsoft OMS (consulte el "paso 3" a continuación)
- [CLI de DC/OS](https://dcos.io/docs/1.8/usage/cli/install/) instalada.

1. En el panel de DC/OS hello, haga clic en el universo de y busque 'OMS' tal y como se muestra a continuación.

![](media/container-service-monitoring-oms/image2.png)

2. Haga clic en **Instalar**. Aparecerá un pop con información de versión OMS de Hola y un **Instalar paquete** o **instalación avanzada** botón. Al hacer clic en **instalación avanzada**, lo que provoca toohello **propiedades de configuración específicas de OMS** página.

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. En este caso, se le pedirá hello tooenter `wsid` (Hola Id. de área de trabajo OMS) y `wskey` (Hola OMS clave principal para el Id. de área de trabajo de hello). tooget ambos `wsid` y `wskey` necesita una cuenta OMS en toocreate <https://mms.microsoft.com>. Siga Hola pasos toocreate una cuenta. Una vez haya terminado de crear cuenta de hello, tendrá que tooobtain su `wsid` y `wskey` haciendo clic en **configuración**, a continuación, **orígenes conectados**y, a continuación, **servidores Linux** , tal y como se muestra a continuación.

 ![](media/container-service-monitoring-oms/image5.png)

4. Seleccionar Hola número OMS instancias que desee y haga clic en botón de hello 'Revisar e instalar'. Por lo general, le interesará toohave Hola número de OMS instancias toohello igual de la máquina virtual tiene en el clúster de agente. Agente de OMS para Linux es instala como contenedores individuales en cada máquina virtual que desea toocollect información de supervisión y la información del registro.

## <a name="setting-up-a-simple-oms-dashboard"></a>Configuración de un panel de OMS

Una vez que ha instalado Hola agente de OMS para Linux en máquinas virtuales de hello, el siguiente paso es tooset de panel de OMS Hola. Hay dos toodo formas esto: Portal de OMS o Portal de Azure.

### <a name="oms-portal"></a>Portal de OMS 

Inicie sesión en el portal de OMS toohello (<https://mms.microsoft.com>) y vaya toohello **Galería de soluciones**.

![](media/container-service-monitoring-oms/image6.png)

Una vez que esté en hello **Galería de soluciones**, seleccione **contenedores**.

![](media/container-service-monitoring-oms/image7.png)

Una vez que haya seleccionado Hola soluciones de contenedor, verá de mosaico en la página del panel de información general de OMS Hola Hola. Una vez que se indizan los datos del contenedor de hello ingestión, verá icono Hola rellenado con información sobre los iconos de vista de la solución.

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a>Portal de Azure 

Portal de inicio de sesión tooAzure en <https://portal.microsoft.com/>. Vaya a **Marketplace**, seleccione **Supervisión y administración** y haga clic en **See All** (Ver todo). A continuación, escriba `containers` en la búsqueda. Verá "contenedores" en los resultados de búsqueda de Hola. Seleccione **Contenedores** y haga clic en **Crear**.

![](media/container-service-monitoring-oms/image9.png)

Cuando haga clic en **Crear**, le preguntará por el área de trabajo. Seleccione el área de trabajo o si no tiene uno, cree uno nuevo.

![](media/container-service-monitoring-oms/image10.PNG)

Una vez que haya seleccionado el área de trabajo, haga clic en **Crear**.

![](media/container-service-monitoring-oms/image11.png)

Para obtener más información acerca de hello soluciones de contenedor de OMS, consulte toothe [análisis de registros de solución de contenedor](../../log-analytics/log-analytics-containers.md).

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a>¿Cómo tooscale agente de OMS con ACS DC/OS 

En caso de que necesita toohave instalado el agente de OMS en el número de nodos real de Hola o se escalado VMSS mediante la adición de más máquinas virtuales, puede hacerlo mediante el escalado hello `msoms` servicio.

Puede ir tooMarathon o hello pestaña servicios de interfaz de usuario de controlador de dominio/OS y escalar verticalmente el número de nodos.

![](media/container-service-monitoring-oms/image12.PNG)

Esta acción implementará nodos tooother que aún no ha implementado a agente de OMS Hola.

## <a name="uninstall-ms-oms"></a>Desinstalación de MS OMS

toouninstall MS OMS escriba Hola siguiente comando:

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a>¡Queremos saber!
¿Qué funciona? ¿Qué falta? ¿Qué más ¿necesita para este toobe útil para usted? Háganos saber en <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.

## <a name="next-steps"></a>Pasos siguientes

 Ahora que ha configurado OMS toomonitor los contenedores,[ver el panel de contenedor](../../log-analytics/log-analytics-containers.md).
