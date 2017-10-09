---
title: aaaSolution como destino de OMS | Documentos de Microsoft
description: "Destinatarios de la solución es una característica de Operations Management Suite (OMS) que le permite toolimit administración soluciones tooa conjunto específico de agentes.  Este artículo se describe cómo toocreate una configuración de ámbito y aplicarla tooa soluciones."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 6f8c8109e0d9e282e18724bf8b673b10de8e498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-solution-targeting-in-operations-management-suite-oms-tooscope-management-solutions-toospecific-agents-preview"></a>Usar soluciones destinos en Operations Management Suite (OMS) agentes de toospecific de soluciones de administración de tooscope (versión preliminar)
Cuando se agrega un tooOMS de solución, se implementa automáticamente por tooall Windows y Linux agentes conectados tooyour análisis de registros área de trabajo predeterminada.  Puede que desee toomanage la cantidad de hello costos y límite de datos recopilada para una solución limitando tooa conjunto determinado de agentes.  Este artículo se describe cómo toouse **solución destinatarios** que es una característica OMS que le permite tooapply un ámbito tooyour soluciones.

## <a name="how-tootarget-a-solution"></a>¿Cómo tootarget una solución
Hay tres tootargeting pasos una solución como se describe en las secciones siguientes de Hola.  Tenga en cuenta que necesitará portal de OMS de Hola y Hola portal de Azure para otros pasos.


### <a name="1-create-a-computer-group"></a>1. Crear un grupo de equipos
Especificar equipos de Hola que desea tooinclude en un ámbito mediante la creación de un [grupo de equipos](../log-analytics/log-analytics-computer-groups.md) en análisis de registros.  grupo de equipos de Hello puede basarse en una búsqueda de registros o importado desde otros orígenes, como Active Directory o grupos WSUS. Como [se describe a continuación](#solutions-and-agents-that-cant-be-targeted), solo los equipos que están directamente conectados tooLog análisis se incluirán en el ámbito de Hola.

Una vez que tenga el grupo de equipos de hello creado en el área de trabajo, deberá incluirlo en una configuración de ámbito que puede ser tooone aplicado o más soluciones.
 
 
 ### <a name="2-create-a-scope-configuration"></a>2. Creación de una configuración de ámbito
 A **configuración de ámbito** incluye uno o más grupos de equipos y puede tener aplicado tooone o más soluciones. 
 
 Crear una configuración de ámbito usando Hola siguiendo el proceso.  

 1. En la consulta Hola portal de Azure, navegue demasiado**análisis de registros** y seleccione el área de trabajo.
 2. En Propiedades de Hola de área de trabajo de hello en **orígenes de datos del área de trabajo** seleccione **configuraciones de ámbito**.
 3. Haga clic en **agregar** toocreate una nueva configuración de ámbito.
 4. Escriba un **nombre** para la configuración de ámbito de Hola.
 5. Haga clic en **Seleccionar grupos de equipos**.
 6. Seleccione el grupo de equipos de Hola que creó y, opcionalmente, cualquier otro tooadd toohello configuración de grupos.  Haga clic en **Seleccionar**.  
 6. Haga clic en **Aceptar** configuración de ámbito de toocreate Hola. 


 ### <a name="3-apply-hello-scope-configuration-tooa-solution"></a>3. Solución de tooa de configuración de ámbito de Hola se aplican.
Una vez que tenga una configuración de ámbito, a continuación, puede aplicarla tooone o más soluciones.  Tenga en cuenta que aunque una sola configuración de ámbito se puede utilizar con varias soluciones, cada solución solo puede utilizar una configuración de ámbito.

Aplicar una configuración de ámbito mediante Hola siguiendo el proceso.  

 1. En la consulta Hola portal de Azure, navegue demasiado**análisis de registros** y seleccione el área de trabajo.
 2. En Propiedades de hello para el área de trabajo de hello seleccione **soluciones**.
 3. Haga clic en la solución de hello desea tooscope.
 4. En Propiedades de hello para la solución de hello en **orígenes de datos del área de trabajo** seleccione **como destino de la solución**.  Si no está disponible la opción de hello, a continuación, [esta solución no se puede destinar](#solutions-and-agents-that-cant-be-targeted).
 5. Haga clic en **Agregar configuración de ámbito**.  Si ya tiene una solución de toothis de configuración que se aplica esta opción estará disponible.  Debe quitar la configuración existente de hello antes de agregar otro.
 6. Haga clic en configuración de ámbito de Hola que ha creado.
 7. Hola de inspección **estado** de tooensure de configuración de Hola que muestra **correcto**.  Si el estado de hello indica un error, a continuación, haga clic en hello elipse toohello derecha configuración hello y seleccione **configuración del ámbito de edición** toomake cambios.

## <a name="solutions-and-agents-that-cant-be-targeted"></a>No se puede establecer el destino de soluciones y agentes.
Siguientes son los criterios de Hola para agentes y las soluciones que no se puede usar con la solución de destino.

- Solo se dirige a la solución aplica toosolutions que implementa tooagents.
- Solo se dirige a la solución aplica toosolutions proporcionado por Microsoft.  No se aplica toosolutions [creado por usted mismo o socios](operations-management-suite-solutions-creating.md).
- Solo puede filtrar los agentes que se conectan directamente tooLog análisis.  Soluciones implementarán automáticamente agentes tooany que forman parte de un grupo de administración de Operations Manager conectado o no están incluidos en una configuración de ámbito.

### <a name="exceptions"></a>Excepciones
No se puede usar como destino de la solución con hello después soluciones aunque se ajustan Hola indique criterios.

- Evaluación de estado del agente

## <a name="next-steps"></a>Pasos siguientes
- Obtener más información sobre soluciones de administración incluidos soluciones hello tooinstall disponible en el entorno en [área de trabajo de análisis de registros de Azure de agregar administración soluciones tooyour](../log-analytics/log-analytics-add-solutions.md).
- Para obtener más información sobre la creación de grupos de equipos, consulte [Grupos de equipos en búsquedas de registros en Log Analytics](../log-analytics/log-analytics-computer-groups.md).