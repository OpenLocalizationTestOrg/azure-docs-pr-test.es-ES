---
title: "aaaService integración con el mapa con System Center Operations Manager | Documentos de Microsoft"
description: "Mapa de servicio es una solución de Operations Management Suite que detecta automáticamente los componentes de la aplicación en Windows y mapas y sistemas Linux Hola comunicación entre los servicios. Este artículo describe el uso de mapa de servicio tooautomatically crear diagramas de aplicación distribuida en Operations Manager."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a>Integración de Mapa de servicio con System Center Operations Manager
  > [!NOTE]
  > Esta característica está en versión preliminar pública.
  > 
  
Mapa de servicio de Operations Management Suite detecta los componentes de la aplicación en los sistemas Windows y Linux y comunicación de hello entre los servicios se asigna automáticamente. Mapa de servicio le permite tooview el camino de Hola de servidores que pensar en ellos, como sistemas interconectados que ofrecen servicios críticos. Mapa de servicio muestra las conexiones entre servidores, los procesos y los puertos a través de cualquier arquitectura conectado de TCP, sin ninguna configuración necesaria además de la instalación de Hola de un agente. Para obtener más información, vea hello [documentación del mapa de servicio](operations-management-suite-service-map.md).

Con esta integración entre System Center Operations Manager y el mapa de servicio, puede crear automáticamente diagramas de aplicación distribuida en Operations Manager que se basan en los mapas de dependencia dinámica hello en mapa de servicio.

## <a name="prerequisites"></a>Requisitos previos
* Un grupo de administración de Operations Manager que administra un conjunto de servidores.
* Un área de trabajo de Operations Management Suite con hello solución de mapa de servicio habilitada.
* Un conjunto de servidores (al menos uno) que se está administrando mediante Operations Manager y enviar datos tooService mapa. Se admiten los servidores de Windows y Linux.
* Una entidad de servicio con acceso toohello suscripción de Azure que está asociado con el área de trabajo de hello Operations Management Suite. Para obtener más información, consulte demasiado[crear una entidad de servicio](#creating-a-service-principal).

## <a name="install-hello-service-map-management-pack"></a>Instalar el módulo de administración de hello mapa de servicio
Habilitar la integración de hello entre Operations Manager y mapa de servicio mediante la importación de paquete de módulos de administración de hello Microsoft.SystemCenter.ServiceMap (Microsoft.SystemCenter.ServiceMap.mpb). agrupación de Hello contiene Hola después de módulos de administración:
* Microsoft Service Map Application Views
* Microsoft System Center Service Map Internal
* Microsoft System Center Service Map Overrides
* Microsoft System Center Service Map

## <a name="configure-hello-service-map-integration"></a>Configurar la integración del mapa de servicio Hola
Después de instalar el módulo de administración de hello mapa de servicio, un nuevo nodo, **Service Map**, se muestra bajo **Operations Management Suite** en hello **administración** panel. 

tooconfigure integración con el mapa de servicio, Hola siguientes:

1. Asistente de configuración de hello tooopen, Hola **Introducción al servicio de mapa** panel, haga clic en **Agregar área de trabajo**.  

    ![Panel de información general de Mapa de servicio](media/oms-service-map/scom-configuration.png)

2. Hola **configuración de la conexión** ventana, escriba el nombre del inquilino de Hola o ID, Id. de aplicación (también conocido como nombre de usuario de Hola o clientID) y contraseña de entidad de servicio de hello y, a continuación, haga clic en **siguiente**. Para obtener más información, consulte demasiado[crear una entidad de servicio](#creating-a-service-principal).

    ![ventana de configuración de la conexión de Hello](media/oms-service-map/scom-config-spn.png)

3. Hola **selección de suscripción** ventana, seleccione Hola suscripción de Azure, el grupo de recursos de Azure (Hola uno que contiene el área de trabajo de hello Operations Management Suite) y área de trabajo de Operations Management Suite y, a continuación, haga clic en **Siguiente**.

    ![Hola área de trabajo de configuración de Operations Manager](media/oms-service-map/scom-config-workspace.png)

4. Hola **selección de grupo de la máquina** ventana, decide qué grupos de máquinas de mapa de servicio que desee toosync tooOperations Manager. Haga clic en **agregar o quitar grupos de máquinas**, seleccione los grupos de lista de Hola de **grupos disponibles de máquina**y haga clic en **agregar**.  Cuando haya terminado la selección de grupos, haga clic en **Aceptar** toofinish.
    
    ![Hola grupos de máquina de configuración de Operations Manager](media/oms-service-map/scom-config-machine-groups.png)
    
5. Hola **selección de servidor** ventana, se puede configurar Hola grupo de servidores de mapa de servicio con servidores de Hola que desea toosync entre Operations Manager y mapa de servicio. Haga clic en **Agregar o quitar servidores**.   
    
    Para toobuild de integración de hello un diagrama de la aplicación distribuida para un servidor, debe ser servidor hello:

    * Administrado por Operations Manager
    * Administrado por Service Map
    * Aparecen en hello grupo de servidores de mapa de servicio

    ![Hola grupo de configuración de Operations Manager](media/oms-service-map/scom-config-group.png)

6. Opcional: Seleccione toocommunicate de grupo de recursos de servidor de administración de hello con Operations Management Suite y, a continuación, haga clic en **Agregar área de trabajo**.

    ![Hola grupo de recursos de configuración de Operations Manager](media/oms-service-map/scom-config-pool.png)

    Podría tardar un minuto tooconfigure y registrar el área de trabajo de hello Operations Management Suite. Una vez configurado, Operations Manager inicia la primera sincronización de mapa de servicio Hola de Operations Management Suite.

    ![Hola grupo de recursos de configuración de Operations Manager](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a>Supervisión del Mapa de servicio
Después de conecta el área de trabajo de hello Operations Management Suite, una nueva carpeta, mapa de servicio, se muestra en hello **supervisión** panel de consola de Operations Manager Hola.

![panel de supervisión de Operations Manager de Hola](media/oms-service-map/scom-monitoring.png)

carpeta de mapa de servicio de Hello consta de cuatro nodos:
* **Alertas activas**: enumera todas las alertas activas de hello acerca de la comunicación de hello entre Operations Manager y mapa de servicio.  Tenga en cuenta que estas alertas no son están sincronizados tooOperations Administrador de alertas de Operations Management Suite. 

* **Servidores**: enumera los servidores de hello supervisado que están configuran toosync de mapa de servicio.

    ![panel de servidores de supervisión de Operations Manager Hola](media/oms-service-map/scom-monitoring-servers.png)

* **Vistas de dependencia de grupo de máquinas**: muestra todos los grupos de máquinas que se sincronizan desde Service Map. Puede hacer clic en cualquier grupo tooview su diagrama de aplicaciones distribuidas.

    ![diagrama de aplicaciones distribuidas de Operations Manager de Hola](media/oms-service-map/scom-group-dad.png)

* **Vistas de la dependencia de servidor**: muestra todos los servidores que se sincronizan desde Mapa de servicio. Puede hacer clic en cualquier servidor tooview su diagrama de aplicaciones distribuidas.

    ![diagrama de aplicaciones distribuidas de Operations Manager de Hola](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a>Editar o eliminar área de trabajo de Hola
Puede editar o eliminar área de trabajo de hello configurado a través de hello **Introducción al servicio de mapa** panel (**administración** panel > **Operations Management Suite**  >  **Mapa de servicio**). Puede configurar solo un área de trabajo de Operations Management Suite por ahora.

![panel de área de trabajo de Operations Manager editar Hola](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a>Configuración de reglas e invalidaciones
Una regla, _Microsoft.SystemCenter.ServiceMapImport.Rule_, se crea información de captura tooperiodically de mapa de servicio. intervalos de sincronización de toochange, puede configurar las invalidaciones de regla de hello (**Authoring** panel > **reglas** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).

![ventana de propiedades de Hello invalidaciones de Operations Manager](media/oms-service-map/scom-overrides.png)

* **Enabled**: sirve para habilitar o deshabilitar las actualizaciones automáticas. 
* **IntervalMinutes**: restablecer Hola tiempo que transcurre entre las actualizaciones. intervalo de saludo predeterminado es una hora. Si desea toosync server mapas con más frecuencia, puede cambiar el valor de Hola.
* **Tiempos de espera**: restablecer la longitud de Hola de tiempo antes de que agota el tiempo de espera de solicitud de saludo. 
* **TimeWindowMinutes**: ventana de tiempo de restablecimiento de Hola para consultar datos. El valor predeterminado es de 60 minutos. valor máximo de Hello permitido por el mapa de servicio es 60 minutos.

## <a name="known-issues-and-limitations"></a>Problemas conocidos y limitaciones

diseño actual Hello presenta siguiente Hola problemas y limitaciones:
* Sólo se puede conectar el área de trabajo de tooa único Operations Management Suite.
* Aunque es posible agregar servidores toohello grupo de servidores de mapa de servicio manualmente a través de hello **Authoring** panel, mapas de Hola para esos servidores no se sincronizan inmediatamente.  Se sincronizarán de mapa de servicio durante el siguiente ciclo de sincronización de Hola.
* Si realiza cambios toohello distribuidas aplicación diagramas creados por el módulo de administración de hello, esos cambios se sobrescribirán probablemente en la próxima sincronización de hello con mapa de servicio.

## <a name="create-a-service-principal"></a>Creación de una entidad de servicio
Para obtener documentación oficial de Azure acerca de cómo crear una entidad de servicio, consulte:
* [Uso de Azure PowerShell para crear una entidad de servicio](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Uso de la CLI de Azure para crear a una entidad de servicio](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [Crear a una entidad de servicio mediante Hola portal de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a>Comentarios
¿Quiere hacernos llegar algún comentario acerca de Mapa de servicio o esta documentación? Visite nuestra [página Voz del usuario](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), donde puede sugerir características o votar sugerencias existentes.
