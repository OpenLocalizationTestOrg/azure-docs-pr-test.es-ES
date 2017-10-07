---
title: "Preguntas más frecuentes de IoT Suite aaaAzure | Documentos de Microsoft"
description: "Preguntas más frecuentes sobre el Conjunto de aplicaciones de IoT"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a>Preguntas más frecuentes sobre el Conjunto de aplicaciones de IoT

Vea también, Hola generador conectados específicos [preguntas más frecuentes sobre](iot-suite-faq-cf.md).

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a>¿Dónde puedo encontrar el código fuente de Hola para soluciones de hello preconfigurado?

código fuente de Hola se almacena en hello después de repositorios de GitHub:
* [Solución preconfigurada de supervisión remota][lnk-remote-monitoring-github]
* [Solución preconfigurada de mantenimiento predictivo][lnk-predictive-maintenance-github]
* [Solución preconfigurada de fábrica conectada](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a>¿Cómo puedo actualizar toohello versión más reciente de la solución preconfigurada supervisión remota Hola que usa Hola características de administración de dispositivos de centro de IoT?

* Si implementa una solución preconfigurada de sitio de https://www.azureiotsuite.com/ hello, siempre se implementa una nueva instancia de la versión más reciente de Hola de solución de Hola.
* Si implementa una solución preconfigurada con línea de comandos de hello, puede actualizar una implementación existente con el nuevo código. Vea [implementación de nube] [ lnk-cloud-deployment] en hello GitHub [repositorio][lnk-remote-monitoring-github].

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a>¿Cómo se puede agregar compatibilidad para un nuevo dispositivo método toohello solución preconfigurada de supervisión remota?

Consulte la sección de hello [agregar compatibilidad con un simulador de toohello método nuevo] [ lnk-add-method] en hello [personalizar una solución preconfigurada] [ lnk-customize] artículo.

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a>dispositivo simulado Hola está omitiendo los cambios de la propiedad deseada, ¿por qué?
Hola supervisión remota preconfigurado soluciones, código de hello simulada del dispositivo solo usa hello **Desired.Config.TemperatureMeanValue** y **Desired.Config.TelemetryInterval** las propiedades adecuadas Hola tooupdate informó de propiedades. Todos los demás cambios de propiedades deseadas se omiten.

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a>El dispositivo no aparece en la lista de Hola de dispositivos en el panel de la solución de hello, ¿por qué?

lista de Hola de dispositivos en el panel de la solución de hello utiliza una lista de Hola de tooreturn de consulta de dispositivos. Actualmente, una consulta no puede devolver más de 10 000 dispositivos. Intente realizar los criterios de búsqueda de hello para la consulta más restrictiva.

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a>¿Cuál es la diferencia de hello entre eliminar un grupo de recursos en hello Azure portal y haga clic en Eliminar en una solución preconfigurada en azureiotsuite.com?

* Si elimina la solución de hello preconfigurado en [azureiotsuite.com][lnk-azureiotsuite], eliminar todos los recursos de hello aprovisionados al crear soluciones de hello preconfigurado. Si ha agregado el grupo de recursos de toohello de recursos adicionales, también se eliminan estos recursos. 
* Si elimina el grupo de recursos de Hola Hola [portal de Azure][lnk-azure-portal], sólo se eliminar recursos de hello en ese grupo de recursos. También necesita toodelete aplicación de Azure Active Directory hello asociado a soluciones de hello preconfigurado en hello [portal de Azure clásico][lnk-classic-portal].

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a>¿Cuántas instancias del Centro de IoT se pueden aprovisionar en una suscripción?

De forma predeterminada, puede aprovisionar [10 centros de IoT Hub por suscripción][link-azuresublimits]. Puede crear un [incidencia de soporte técnico de Azure] [ link-azuresupportticket] tooraise este límite. Como resultado, desde cada disposiciones de solución preconfigurada un nuevo centro de IoT, solo puede aprovisionar una too10 había preconfigurado soluciones en una suscripción determinada. 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a>¿Cuántas instancias de Azure Cosmos DB se pueden aprovisionar en una suscripción?

Cincuenta. Puede crear un [incidencia de soporte técnico de Azure] [ link-azuresupportticket] tooraise Esto limitará, pero de forma predeterminada, solo puede aprovisionar 50 instancias de base de datos de Cosmos por suscripción. 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a>¿Cuántas API de Mapas de Bing gratis se pueden aprovisionar en una suscripción?

Dos. Solo puede crear dos planes de Mapas de Bing para empresa de nivel 1 de transacciones internas en una suscripción de Azure. solución de supervisión remota Hola se aprovisiona con plan Hola interno las transacciones de nivel 1 de forma predeterminada. Como resultado, solo puede aprovisionar tootwo remoto de supervisión de soluciones en una suscripción sin modificaciones.

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a>Tengo una implementación de soluciones de supervisión remota con un mapa estático, ¿cómo se puede agregar un mapa Bing interactivo?

1. Obtenga la QueryKey de Bing Maps API for Enterprise en [Azure Portal][lnk-azure-portal]: 
   
   1. Navegue toohello grupo de recursos donde es la API de Bing Maps para Enterprise en hello [portal de Azure][lnk-azure-portal].
   2. Haga clic en **Toda la configuración** y después en **Administración de claves**. 
   3. Verá dos claves: **MasterKey** y **QueryKey**. Copiar valor de Hola para **QueryKey**.
      
      > [!NOTE]
      > ¿No tiene una cuenta de la API de Mapas de Bing para empresa? Crear uno en hello [portal de Azure] [ lnk-azure-portal] haciendo clic en + nuevo, buscando la API de Bing Maps para Enterprise y seguir solicita toocreate.
      > 
      > 
2. Deslice hacia abajo de código más reciente de Hola de hello [-IoT-remoto-supervisión de Azure][lnk-remote-monitoring-github].
3. Ejecutar a una variable local o implementación Hola instrucciones de implementación de línea de comandos en carpeta de /docs/ de hello en el repositorio de hello en la nube. 
4. Una vez se haya ejecutado una variable local o en la nube implementación, busque en la carpeta raíz para Hola *. archivo user.config creado durante la implementación. Abra este archivo en un editor de texto. 
5. Valor de hello tooinclude copió desde de la línea de siguiente Hola de cambio su **QueryKey**: 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a>¿Puedo crear una solución preconfigurada si tengo Microsoft Azure para DreamSpark?

En este momento, no se puede crear una solución preconfigurada con una cuenta de [Microsoft Azure para DreamSpark][lnk-dreamspark]. Sin embargo, puede crear una [cuenta de evaluación gratuita de Azure][lnk-30daytrial] en un par de minutos, lo que le permite crear una solución preconfigurada.

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a>¿Puedo crear una solución preconfigurada si tengo alguna suscripción del Proveedor de soluciones en la nube (CSP)?

En este momento, no se puede crear una solución preconfigurada con una suscripción del Proveedor de soluciones en la nube (CSP). Sin embargo, puede crear una [cuenta de evaluación gratuita de Azure][lnk-30daytrial] en un par de minutos, lo que le permite crear una solución preconfigurada.

### <a name="how-do-i-delete-an-aad-tenant"></a>¿Cómo se eliminan inquilinos de AAD?

Consulte la entrada del blog de Eric Golpe [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant] (Tutorial para la eliminación de inquilinos de Azure AD).

### <a name="next-steps"></a>Pasos siguientes

También puede explorar algunas de hello otras características y capacidades de hello IoT preconfigurado soluciones:

* [Información general de la solución preconfigurada de mantenimiento predictivo][lnk-predictive-overview]
* [Introducción a la solución preconfigurada de fábrica conectada](iot-suite-connected-factory-overview.md)
* [Seguridad de IoT de hello masa][lnk-security-groundup]

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
