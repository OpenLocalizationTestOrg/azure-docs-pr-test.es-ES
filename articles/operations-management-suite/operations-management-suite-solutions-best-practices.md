---
title: "prácticas recomendadas de solución de aaaOMSManagement | Documentos de Microsoft"
description: 
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
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 08cf1c101e301d24fb5c2bf4bc02a978e508a198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-management-solutions-in-operations-management-suite-oms-preview"></a>Procedimientos recomendados para crear soluciones de administración en Operations Management Suite (OMS) (versión preliminar)
> [!NOTE]
> La versión de la documentación para crear soluciones de administración de OMS está actualmente en fase preliminar. Cualquier esquema que se describe a continuación es toochange de asunto.  

En este artículo se presentan procedimientos recomendados para [crear un archivo de solución de administración](operations-management-suite-solutions-solution-file.md) en Operations Management Suite (OMS).  Esta información se actualizará a medida que se detecten procedimientos recomendados adicionales.

## <a name="data-sources"></a>Orígenes de datos
- Los orígenes de datos se pueden [configurar con una plantilla de Resource Manager](../log-analytics/log-analytics-template-workspace-configuration.md), pero no deben incluirse en un archivo de solución.  Hola motivo es que la configuración de orígenes de datos no es actualmente idempotentes, lo que significa que la solución podía sobrescribir la configuración existente en el área de trabajo del usuario de Hola.<br><br>Por ejemplo, la solución puede requerir eventos de advertencia y Error de registro de eventos de aplicación Hola.  Si se especifica como un origen de datos en la solución, corre el riesgo de quitar eventos de información si el usuario de hello tenía esto configurado en su área de trabajo.  Si incluye todos los eventos, puede estar recopilando eventos de información excesivo en el área de trabajo del usuario de Hola.

- Si la solución requiere que los datos de uno de los orígenes de datos estándar de hello, debe definirlo como requisito previo.  Estado en la documentación de ese cliente hello debe configurar origen de datos de Hola por sí solas.  
- Agregar un [comprobación de flujo de datos](../log-analytics/log-analytics-view-designer-tiles.md) recopila mensaje tooany se ve en su solución tooinstruct Hola de usuario en orígenes de datos que toobe necesidad configurado para toobe de datos necesarios.  Este mensaje se muestra en el icono Hola de vista de hello cuando no se encuentran los datos necesarios.


## <a name="runbooks"></a>Runbooks
- Agregar un [programación de automatización](../automation/automation-schedules.md) para cada runbook de la solución que necesita toorun según una programación.
- Incluir hello [IngestionAPI módulo](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) en su toobe solución usa runbooks escribir repositorio de análisis de registros de datos toohello.  Configurar la solución de hello demasiado[referencia](operations-management-suite-solutions-solution-file.md#solution-resource) este recurso, por lo que TI permanece si se quita la solución de Hola.  Esto permite varias soluciones tooshare Hola módulo.
- Use [las variables de automatización](../automation/automation-schedules.md) tooprovide valores solución toohello que los usuarios pueden agregar toochange posteriormente.  Incluso si solución hello toocontain configurado Hola variable, su valor puede cambiarse.

## <a name="views"></a>Vistas
- Todas las soluciones deben incluir una sola vista que se muestra en el portal del usuario de Hola.  Hello vista puede contener varios [elementos de visualización](../log-analytics/log-analytics-view-designer-parts.md) tooillustrate diferentes conjuntos de datos.
- Agregar un [comprobación de flujo de datos](../log-analytics/log-analytics-view-designer-tiles.md) recopila mensaje tooany se ve en su solución tooinstruct Hola de usuario en orígenes de datos que toobe necesidad configurado para toobe de datos necesarios.
- Configurar la solución de hello demasiado[contienen](operations-management-suite-solutions-solution-file.md#solution-resource) Hola vista para que se quita si se quita la solución de Hola.

## <a name="alerts"></a>Alertas
- Definir lista de destinatarios de Hola como un parámetro en el archivo de solución de Hola para que usuario Hola puede definirlos al instalar soluciones de Hola.
- Configurar la solución de hello demasiado[referencia](operations-management-suite-solutions-solution-file.md#solution-resource) de reglas de alerta para que el usuario pueda cambiar su configuración.  Puede que deseen toomake cambios como modificar la lista de destinatarios de hello, cambiar el umbral de Hola de alerta de Hola o deshabilitar la regla de alerta de Hola. 


## <a name="next-steps"></a>Pasos siguientes
* Recorra el proceso básico de Hola de [diseñar y crear una solución de administración](operations-management-suite-solutions-creating.md).
* Obtenga información acerca de cómo demasiado[crear un archivo de solución](operations-management-suite-solutions-solution-file.md).
* [Agregar las búsquedas guardadas y alertas](operations-management-suite-solutions-resources-searches-alerts.md) tooyour solución de administración.
* [Agregar vistas](operations-management-suite-solutions-resources-views.md) tooyour solución de administración.
* [Agregar los runbooks de automatización y otros recursos](operations-management-suite-solutions-resources-automation.md) tooyour solución de administración.

