---
title: "una solución de administración de OMS aaaBuild | Documentos de Microsoft"
description: "Soluciones de administración de amplían la funcionalidad de Hola de Operations Management Suite (OMS) proporcionando escenarios de administración empaquetada que los clientes pueden agregar área de trabajo OMS tootheir.  Este artículo proporciona detalles sobre cómo puede crear toobe de soluciones de administración usan en su propio entorno o estará disponible tooyour clientes."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dea4c0d9e608d9fe4aa41088705958c9fe999372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-build-a-management-solution-in-operations-management-suite-oms-preview"></a>Diseño y compilación de una solución de administración en Operations Management Suite (OMS) (versión preliminar)
> [!NOTE]
> La versión de la documentación para crear soluciones de administración de OMS está actualmente en fase preliminar. Cualquier esquema que se describe a continuación es toochange de asunto.

[Soluciones de administración de](operations-management-suite-solutions.md) amplían la funcionalidad de Hola de Operations Management Suite (OMS) proporcionando escenarios de administración empaquetada que los clientes pueden agregar área de trabajo OMS tootheir.  Este artículo presenta un toodesign proceso básico y generar una solución de administración que es adecuada para los requisitos más comunes.  Si estás nuevas soluciones de administración de toobuilding, a continuación, puede utilizar este proceso como punto de partida y, a continuación, aprovechar los conceptos de Hola para soluciones más complejas que los requisitos evolucionan.

## <a name="what-is-a-management-solution"></a>¿Qué es una solución de administración?

Soluciones de administración contienen OMS y recursos de Azure que funcionan conjuntamente tooachieve un escenario de supervisión determinado.  Se implementan como [plantillas de administración de recursos](../azure-resource-manager/resource-manager-template-walkthrough.md) que contienen los detalles de cómo tooinstall y configurar sus recursos independientes cuando se instala la solución de Hola.

Hola estrategia básica es la solución de administración de toostart mediante la creación de componentes individuales de hello en el entorno de Azure.  Una vez que tenga funcionalidad Hola funciona correctamente, se pueden iniciar empaquetarlos en un [archivo de solución de administración](operations-management-suite-solutions-solution-file.md). 


## <a name="design-your-solution"></a>Diseño de la solución
modelo más común de Hola para una solución de administración se muestra en hello siguiente diagrama.  diferentes componentes de Hello en este modelo se tratan en hello siguiente.

![Información general de la solución OMS](media/operations-management-suite-solutions/solution-overview.png)


### <a name="data-sources"></a>Orígenes de datos
Hola empezar a diseñar una solución consiste en determinar los datos de Hola que necesite del repositorio de análisis de registros de Hola.  Estos datos pueden ser recopilados por un [origen de datos](../log-analytics/log-analytics-data-sources.md) o [otra solución](operations-management-suite-solutions.md), o la solución necesite tooprovide Hola proceso toocollect lo.

Hay varias maneras de orígenes de datos que se pueden recopilar en el repositorio de análisis de registros de hello, como se describe en [orígenes de datos de análisis de registros](../log-analytics/log-analytics-data-sources.md).  Esto incluye eventos de registro de eventos de Windows hello o generados por Syslog además tooperformance contadores para los clientes de Windows y Linux.  También puede recoger datos de recursos de Azure recopilados por Azure Monitor.  

Si necesita datos que no son accesibles a través de cualquiera de los orígenes de datos disponibles de hello, puede usar hello [API de recopilador de datos HTTP](../log-analytics/log-analytics-data-collector-api.md) que le permite repositorio de análisis de registros de toowrite datos toohello desde cualquier cliente que puede llamar a un resto API.  Hola forma más común de recopilación de datos personalizado en una solución de administración es toocreate una [runbook en automatización de Azure](../automation/automation-runbook-types.md) que recopila datos de hello necesaria de recursos de Azure o externos y utiliza Hola toowrite API del recopilador de datos repositorio de toohello.  

### <a name="log-searches"></a>Búsqueda de registros
[Búsquedas de registro](../log-analytics/log-analytics-log-searches.md) son tooextract usado y analizar los datos en el repositorio de análisis de registros de Hola.  Se utilizan vistas y las alertas en suma tooallowing Hola usuario tooperform análisis ad hoc de los datos en el repositorio de Hola.  

Debe definir las consultas que le resulte útil toohello usuario incluso si no se utilizan con las vistas o las alertas.  Estos serán toothem disponible como búsquedas guardadas en el portal de Hola y también puede incluirlos en un [parte de la visualización de lista de consultas](../log-analytics/log-analytics-view-designer-parts.md#list-of-queries-part) en la vista personalizada.

### <a name="alerts"></a>Alertas
[Alertas de análisis de registros](../log-analytics/log-analytics-alerts.md) identifican los problemas a través de [búsquedas de registro](#log-searches) con datos de hello en el repositorio de Hola.  Y notificar al usuario de Hola o ejecutan automáticamente una acción en respuesta. Debe identificar las diferentes condiciones de alerta para la aplicación e incluir reglas de alerta correspondientes en el archivo de solución.

Si el problema de hello potencialmente puede corregirse con un proceso automatizado, a continuación, normalmente creará un runbook en automatización de Azure tooperform esta corrección.  Los servicios de Azure más pueden administrarse con [cmdlets](/powershell/azure/overview) qué runbook Hola aprovecharía tooperform esta funcionalidad.

Si la solución requiere funcionalidad externa de alerta de respuesta tooan, a continuación, puede usar un [webhook respuesta](../log-analytics/log-analytics-alerts-actions.md).  Esto le permite toocall un servicio web externo enviar información de la alerta de Hola.

### <a name="views"></a>Vistas
Vistas de análisis de registros son toovisualize usa datos del repositorio de análisis de registros de Hola.  Cada solución normalmente contendrá una sola vista con un [icono](../log-analytics/log-analytics-view-designer-tiles.md) que se muestra en el panel principal del usuario de Hola.  vista de Hello puede contener cualquier número de [elementos de visualización](../log-analytics/log-analytics-view-designer-parts.md) tooprovide diferentes visualizaciones de usuario de toohello de los datos recopilados de Hola.

Se [crear vistas personalizadas con el Diseñador de vistas de hello](../log-analytics/log-analytics-view-designer.md) que más adelante puede exportar para su inclusión en el archivo de solución.  


## <a name="create-solution-file"></a>Creación del archivo de solución
Una vez que haya configurado y probado los componentes de Hola que va a formar parte de la solución, puede [crear el archivo de solución](operations-management-suite-solutions-solution-file.md).  Va a implementar componentes de la solución de hello en un [plantilla del Administrador de recursos](../azure-resource-manager/resource-group-authoring-templates.md) que incluye un [recursos de solución](operations-management-suite-solutions-solution-file.md#solution-resource) con relaciones toohello Hola a otros recursos de archivo.  


## <a name="test-your-solution"></a>Prueba de la solución
Mientras se desarrolla la solución, deberá tooinstall y probarlo en el área de trabajo.  Puede hacerlo mediante cualquiera de los métodos disponibles de hello demasiado[probar e instalar plantillas de administrador de recursos](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="publish-your-solution"></a>Publicación de la solución
Una vez que haya finalizado y probado la solución, puede hacer que toocustomers disponible a través de cualquier Hola siguientes orígenes.

- **Plantillas de inicio rápido de Azure**.  [Plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/) es un conjunto de plantillas de administrador de recursos aportados por la Comunidad de Hola a través de GitHub.  Puede hacer que la solución disponible por la siguiente información en hello [guía para colaborar en](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE).
- **Azure Marketplace**.  Hola [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/) permite toodistribute y vender la solución tooother a los desarrolladores, ISV y los profesionales de TI.  Puede obtener información sobre cómo toopublish su tooAzure solución Marketplace en [cómo toopublish y administrar una oferta de hello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).



## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[crear un archivo de solución](operations-management-suite-solutions-solution-file.md) para la solución de administración.
* Obtenga información acerca de los detalles de Hola de [plantillas del Administrador de recursos de Azure de creación](../azure-resource-manager/resource-group-authoring-templates.md).
* Búsqueda de [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates) para obtener ejemplos de diferentes plantillas de Resource Manager.