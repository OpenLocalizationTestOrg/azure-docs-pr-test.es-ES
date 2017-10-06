---
title: "aaaAzure servicio de análisis de eventos de tejido con OMS | Documentos de Microsoft"
description: "Obtenga información sobre cómo visualizar y analizar eventos con OMS para la supervisión y el diagnóstico de clústeres de Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 526519293e70982c95e31241465b87f190096f74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-oms"></a>Análisis y visualización de eventos con OMS

Operations Management Suite (OMS) es una colección de servicios de administración que simplifican la supervisión y diagnósticos para aplicaciones y servicios hospedados en la nube de Hola. leer una descripción más detallada de OMS y lo que ofrece tooget [¿qué es OMS?](../operations-management-suite/operations-management-suite-overview.md)

## <a name="log-analytics-and-hello-oms-workspace"></a>Inicie sesión hello área de trabajo OMS y análisis

Log Analytics recopila datos de recursos administrados, incluidos un agente o una tabla de almacenamiento de Azure, y los mantiene en un repositorio central. datos de Hello, a continuación, pueden ser utilizados para el análisis, alertas y visualización, o la exportación aún más. Log Analytics admite eventos, datos de rendimiento u otros datos personalizados.

Cuando se configura OMS, tendrá acceso tooa específica *área de trabajo OMS*, desde donde los datos se pueden consultar o visualizar en los paneles.

Después de que se reciben datos mediante el análisis de registros, OMS tiene varias *soluciones de administración de* que son soluciones preestablecida toomonitor los datos entrantes, escenarios de tooseveral personalizado. Puede tratarse de un *servicio de análisis de tejido* solución y un *contenedores* solución, que son toodiagnostics Hola dos de los más importantes y supervisión al usar clústeres de Service Fabric. Hay varios otros así que merece la pena examinar y OMS también permite la creación de hello de soluciones personalizadas, que puede leer más sobre [aquí](../operations-management-suite/operations-management-suite-solutions.md). Cada solución que elija toouse para un clúster se configurará en hello misma área de trabajo OMS, junto con el análisis de registros. Áreas de trabajo permiten paneles personalizados y la visualización de datos y datos de toohello de las modificaciones que desee toocollect, procesar y analizar.

## <a name="setting-up-an-oms-workspace-with-hello-service-fabric-solution"></a>Configuración de un área de trabajo OMS con hello soluciones de tejido de servicio

Se recomienda que incluya Hola soluciones de tejido de servicio en el área de trabajo OMS, puesto que ofrece un panel de información útil muestra hello diversos canales de registro entrantes de nivel de plataforma y de aplicaciones de Hola y Hola capaz de tooquery Service Fabric específico registros. Aquí es el aspecto de una solución de Fabric relativamente simple, se con una sola aplicación implementada en el clúster de hello:

![Solución SF en OMS](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-solution.png)

Hay dos tooprovision de formas y configurar un área de trabajo OMS, ya sea a través de una plantilla de administrador de recursos o directamente desde Azure Marketplace. Utilice primero hello cuando va a implementar un clúster, y Hola este último si ya tiene un clúster implementado con diagnósticos habilitados.

### <a name="deploying-oms-using-a-resource-management-template"></a>Implementación de OMS con una plantilla de Resource Manager

Esto sucede durante la fase de creación de clúster de hello - al implementar un clúster con un administrador de recursos, plantilla de hello, también puede crear una nueva área de trabajo OMS, agregar hello tooit de soluciones de tejido de servicio y configurar tooread datos desde el almacenamiento adecuado de Hola tablas.

>[!NOTE]
>Para este toowork diagnóstico tiene toobe habilitado para tooexist de tablas de almacenamiento de Azure de Hola para OMS / información de tooread de análisis de registros en de.

[Aquí](https://azure.microsoft.com/resources/templates/service-fabric-oms/) hay una plantilla de ejemplo que puede usar y modificar según sea necesario, donde se realizan las acciones anteriores. En caso de Hola que desea definir la opcionalidad como más, hay unas pocas plantillas más que proporcionan diferentes opciones dependiendo de que en el proceso de hello puede ser de configuración de un área de trabajo OMS, pueden encontrarse en [Service Fabric y OMS plantillas](https://azure.microsoft.com/resources/templates/?term=service+fabric+OMS).

### <a name="deploying-oms-using-through-azure-marketplace"></a>Implementación de OMS a través de Azure Marketplace

Si prefiere tooadd un área de trabajo OMS después de haber implementado un clúster, diríjase tooAzure Marketplace y busque *"Análisis de tejido de servicio"*. Solo debe haber un recurso que aparece, dentro de la categoría de "Supervisión de la administración de +" Hola, visto a continuación:

![SF Analytics en OMS con Marketplace](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-analytics.png)

Al hacer clic en **Crear**, se le pedirá que especifique un área de trabajo de OMS. Haga clic en **Seleccione un área de trabajo** y después en **Crear un área de trabajo**. Rellenar las entradas de hello necesario: Hola único requisito aquí es que suscripción Hola Hola debe ser el área de trabajo OMS hello y clúster de Service Fabric Hola igual. Después de haber validado las entradas, el área de trabajo de OMS se implementará en unos minutos. Mientras que acaba de implementar, creación de hello de hoja de solución de Service Fabric Hola todavía permanecerá abierta. Asegúrese de que Hola la misma área de trabajo se muestra en *área de trabajo de OMS* y posicionamiento **crear** en parte inferior de hello, tooadd Hola el área de trabajo de Service Fabric solución toohello.

## <a name="using-hello-oms-agent"></a>Uso de hello agente de OMS

Se recomienda toouse EventFlow y WAD como soluciones de agregación porque permiten que un toodiagnostics enfoque más modular y supervisión. Por ejemplo, si desea que los resultados de EventFlow toochange, no requiere ningún cambio tooyour real la instrumentación, solo un archivo de configuración de modificación sencilla tooyour. Si, sin embargo, decide tooinvest en el uso de OMS y están dispuestos toocontinue usarlo para el análisis de eventos (no tiene toobe Hola solo plataforma use, pero en su lugar ese será al menos una de las plataformas de hello), recomendamos que explore configurar hello [</C0>agentedeOMS<spanclass="notranslate">](../log-analytics/log-analytics-windows-agents.md).</span> También debe utilizar a agente de OMS Hola al implementar el clúster de tooyour de contenedores, tal y como se describe a continuación.

proceso de Hola para hacer esto es relativamente fácil, ya que solo tiene tooadd Hola agente como conjunto de escalas de máquina virtual plantilla de administrador de recursos de extensión tooyour, asegurándose de que se instala en cada uno de los nodos. Encontrará una plantilla de administrador de recursos de ejemplo que implementa el área de trabajo OMS de hello con hello soluciones de tejido de servicio (como anteriormente) y agrega Hola agente tooyour nodos de clústeres que ejecutan [Windows](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Windows) o [Linux](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Linux).

ventajas de Hola de esto son siguiente hello:

* Más datos en el lado de contadores y las métricas de rendimiento de Hola
* Datos tooconfigure sencilla que se recopilan de Hola de clúster y realizar cambios tooit sin tener que volver a implementar las aplicaciones o clúster de hello, ya que cambia la configuración del agente de hello toohello puede realizarse desde el área de trabajo OMS de Hola y simplemente restablece a agente Hola de forma automática. tooconfigure Hola OMS agente toopick los contadores de rendimiento específicos, área de trabajo vaya toohello **Inicio > Configuración > datos > contadores de rendimiento de Windows** y elegir datos de Hola que le gustaría toosee recopilado
* Mostrarán datos más rápido que la necesidad de toobe almacenado antes de que se va a recogido por OMS / análisis de registros
* La supervisión de contenedores es mucho más sencilla, ya que puede seleccionar registros de Docker (como stdout o stderror) y estadísticas (métricas de rendimiento de los niveles de contenedor y nodos).

Hola aquí en la consideración principal es que puesto que es un agente, se implementará en el clúster junto con todas las aplicaciones, por lo que habrá algunas toohello mínimo afectan al rendimiento de las aplicaciones en clúster de Hola.

## <a name="monitoring-containers"></a>Supervisión de contenedores

Al implementar el clúster de Service Fabric tooa de contenedores, se recomienda que hello clúster se ha configurado con el agente OMS de Hola y se ha agregado ese Hola solución contenedores tooenable de área de trabajo OMS de tooyour supervisión y diagnósticos. Aquí es qué contenedores Hola solución aspecto en un área de trabajo:

![Panel de OMS básico](./media/service-fabric-diagnostics-event-analysis-oms/oms-containers-dashboard.png)

agente de Hello habilita la recopilación de Hola de varios registros específicos de contenedores que se pueden consultar en OMS, o utilizar los indicadores de rendimiento de toovisualized. los tipos de registro de Hello que se recopilan son:

* ContainerInventory: muestra información acerca de la ubicación, nombre e imágenes del contenedor
* ContainerImageInventory: información acerca de las imágenes implementadas, lo que incluye sus identificadores o tamaños
* ContainerLog: registros de error concretos, registros de docker (stdout, etc.) y otras entradas
* ContainerServiceLog: comandos de demonio de docker que se han ejecutado
* Rendimiento: contadores de rendimiento incluido contenedor cpu, memoria, tráfico de red, la e/s de disco y métricas personalizadas de hello hospedan máquinas

Este artículo tratan Hola pasos necesarios tooset la supervisión para el clúster de contenedor. más información acerca de la solución de contenedores de OMS, toolearn desproteger sus [documentación](../log-analytics/log-analytics-containers.md).

tooset seguridad Hola soluciones de contenedor en el área de trabajo, asegúrese de que tiene el agente de OMS Hola implementado en los nodos del clúster siguiendo los pasos de hello mencionados anteriormente. Una vez que el clúster de hello esté listo, implemente un tooit del contenedor. Tenga en cuenta que Hola primera vez una imagen de contenedor es tooa implementado clúster, se aplican varias imágenes de hello toodownload de minutos dependiendo de su tamaño.

En Azure Marketplace, busque *contenedores* y cree un recurso de contenedores (bajo Hola supervisión y administración de categoría).

![Adición de la solución Containers](./media/service-fabric-diagnostics-event-analysis-oms/containers-solution.png)

En el paso de creación de hello, solicita un área de trabajo OMS. Seleccione Hola uno que se creó con la implementación de hello anterior. Este paso agrega una solución de contenedores en el área de trabajo OMS y se detecta automáticamente por el agente OMS Hola implementado por plantilla de Hola. agente de Hello empezará a recopilar datos en procesos de contenedores de hello en clúster de Hola y menos de 15 minutos o por lo tanto, debería ver la solución de hello claro seguridad con datos, como en la imagen de hello del panel de hello anterior de.


## <a name="next-steps"></a>Pasos siguientes

Explorar Hola después toocustomize de herramientas y opciones de OMS, que necesita un tooyour de área de trabajo:

* En el caso de los clústeres locales, OMS ofrece una puerta de enlace (hacia delante Proxy HTTP) que puede ser utilizados toosend datos tooOMS. Obtenga más información en [conectar equipos sin tooOMS el acceso a Internet mediante Hola puerta de enlace de OMS](../log-analytics/log-analytics-oms-gateway.md)
* Configurar OMS tooset [automatizada alertas](../log-analytics/log-analytics-alerts.md) tooaid en la detección y diagnóstico
* Obtener las nociones básicas de hello [Iniciar búsqueda y la consulta](../log-analytics/log-analytics-log-searches.md) que ofrece características como parte del análisis de registros
