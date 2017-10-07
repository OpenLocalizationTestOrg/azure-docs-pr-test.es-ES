---
title: "alertas de aaaCreating en análisis de registros de OMS | Documentos de Microsoft"
description: "Alertas de análisis de registros identificar información importante en el repositorio OMS y se pueden proactivamente avisarle de problemas o invocar acciones tooattempt toocorrect ellos.  Este artículo describe cómo toocreate una regla de alerta y las diferentes acciones de Hola de detalles que pueden tomar."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: 3d035b2426dda9645b19e6c993dc26a2d95a2a78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-alert-rules-in-log-analytics"></a>Uso de reglas de alertas en Log Analytics
Las alertas se crean mediante reglas de alerta que ejecutan automáticamente búsquedas de registros a intervalos regulares.  Crean un registro de alertas si los resultados de hello coincide con determinados criterios.  regla de Hello, a continuación, ejecutar de forma automática una o más de las acciones tooproactively recibir una notificación de alerta de Hola o invocar otro proceso.   

Este artículo describe Hola procesos toocreate y editar reglas de alerta mediante el portal de OMS Hola.  Para obtener más información acerca de hello distintas configuraciones y cómo tooimplement requiere lógica, consulte [conceptos básicos sobre alertas en el análisis de registros](log-analytics-alerts.md).

>[!NOTE]
> Actualmente no se puede crear o modificar una regla de alerta con hello portal de Azure. 

## <a name="create-an-alert-rule"></a>Crear una regla de alerta

toocreate una regla de alerta mediante el portal de OMS hello, primero debe crear una búsqueda de registros de registros de Hola que se debe invocar alerta Hola.  Hola **alerta** botón, a continuación, estará disponible para que pueda crear y configurar la regla de alerta de Hola.

>[!NOTE]
> Actualmente se puede crear un máximo de 250 reglas de alertas en un área de trabajo de OMS. 

1. En la página de información general de OMS de hello, haga clic en **búsqueda de registros**.
2. Cree una nueva consulta de búsqueda de registros o seleccione una búsqueda de registros guardada. 
3. Haga clic en **alerta** en parte superior de Hola Hola de hello página tooopen **Agregar regla de alerta** pantalla.
4. Configurar regla de alerta de hello con información de [detalles de reglas de alerta](#details-of-alert-rules) a continuación.
6. Haga clic en **guardar** regla de alerta de toocomplete Hola.  Se iniciará la ejecución de inmediato.


## <a name="edit-an-alert-rule"></a>Edición de una regla de alerta
Puede obtener una lista de todas las reglas de alerta en hello **alertas** menú análisis de registros **configuración**.  

![Administrar alertas](./media/log-analytics-alerts/configure.png)

1. Hola Hola select de consola OMS **configuración** icono.
2. Seleccione **Alertas**.

Puede realizar varias acciones desde esta vista.

* Deshabilitar una regla seleccionando **desactivar** tooit siguiente.
* Editar una regla de alerta, haga clic en el icono de lápiz hello tooit siguiente.
* Quitar una regla de alerta, haga clic en hello **X** tooit siguiente de icono. 

## <a name="details-of-alert-rules"></a>Detalles sobre las reglas de alerta
Al crear o editar una regla de alerta en el portal de OMS hello, trabajará con hello **Agregar regla de alerta** o **Editar regla de alerta** página.  Hola las tablas siguientes describe los campos de hello en esta pantalla.

![Regla de alerta](media/log-analytics-alerts/add-alert-rule.png)

### <a name="alert-information"></a>Información de alertas
Se trata de la configuración básica de la regla de alerta de Hola y alertas de Hola que crea.

| Propiedad | Descripción |
|:--- |:---|
| Nombre | Único nombre tooidentify Hola regla de alerta. Este nombre se incluye en las alertas creadas por regla Hola.  |
| Descripción | Descripción opcional de la regla de alerta de Hola. |
| Severity |Gravedad de las alertas creadas por esta regla. |

### <a name="search-query-and-time-window"></a>Ventana de consulta y ventana de tiempo
ventana de consulta y tiempo de búsqueda de Hello que devuelve registros de Hola que son evaluada toodetermine si se crean las alertas.

| Propiedad | Descripción |
|:--- |:---|
| Consulta de búsqueda | Se trata de una consulta de Hola que se va a ejecutar.  registros de Hello devueltos por esta consulta será toodetermine usado si se crea una alerta.<br><br>Seleccione **usar consulta de búsqueda actual** toouse Hola consulta actual o seleccione una búsqueda guardada de la lista de hello existente.  sintaxis de consulta de Hola se proporcionan en el cuadro de texto de Hola donde puede modificar si es necesario. |
| Período de tiempo |Especifica el intervalo de tiempo de Hola para consulta de Hola.  Hola consulta devuelve solo los registros que se crearon dentro de este intervalo de hello hora actual.  Puede ser cualquier valor entre 5 minutos y 24 horas.  Debe ser igual o mayor que toohello frecuencia de alerta.  <br><br> Por ejemplo, si hello vez ventana se establece too60 minutos y consulta de Hola que se ejecuta a la 1:15 P.M., se devolverá únicamente los registros que se han creado entre 12:15 P.M. y la 1:15 PM. |

Al proporcionar el período de tiempo de hello para la regla de alerta de hello, se mostrará el número de Hola de los registros existentes que coincidan con los criterios de búsqueda de Hola para ese período de tiempo.  Esto puede ayudarle a determinar la frecuencia de Hola que le indicará Hola número de resultados esperados.

### <a name="schedule"></a>Schedule
Define la frecuencia con hello consulta de búsqueda se ejecuta.

| Propiedad | Descripción |
|:--- |:---|
| Frecuencia de alertas | Especifica la frecuencia con hello se debe ejecutar consulta. Puede ser cualquier valor entre 5 minutos y 24 horas. Debe ser igual tooor menor que el período de tiempo de Hola.  Si el valor de hello es mayor que el período de tiempo de hello, a continuación, se arriesga a registros que falta.<br><br>Por ejemplo, considere la posibilidad de una ventana de tiempo de 30 minutos y una frecuencia de 60 minutos.  Si se ejecuta la consulta de Hola a las 1:00, devuelve registros entre la 1:00 P.M. y de 12:30.  Hola próxima vez que se ejecutaría consulta hello es 2:00 cuando devolvería registros entre la 1:30 y las 2:00.  Nunca se evaluarán los registros creados entre la 1:00 y la 1:30. |


### <a name="generate-alert-based-on"></a>Generación de alerta según
Define Hola se deben crear criterios que se va a evaluar en resultados de Hola de toodetermine de consulta de búsqueda de hello si una alerta.  Estos detalles será diferentes en función de tipo hello de regla de alerta que seleccione.  Puede obtener detalles de hello tipos diferentes de regla de alerta de [conceptos básicos sobre alertas en el análisis de registros](log-analytics-alerts.md).

| Propiedad | Descripción |
|:--- |:---|
| Suprimir alertas | Al activar la supresión de regla de alerta de hello, acciones de regla de Hola se deshabilitan durante un período definido de tiempo después de crear una nueva alerta. regla de Hello todavía se está ejecutando y crea registros de alerta si se cumplen los criterios de Hola. Se trata de tooallow tiempo problema de hello toocorrect sin ejecutar acciones duplicadas. |

#### <a name="number-of-results-alert-rules"></a>Reglas de alerta para número de resultados

| Propiedad | Descripción |
|:--- |:---|
| Número de resultados |Se crea una alerta si el número de Hola de registros devueltos por la consulta de hello es cualquiera **mayor** o **menor** Hola valor que proporcione.  |

#### <a name="metric-measurement-alert-rules"></a>Reglas de alertas para medición de métricas

| Propiedad | Descripción |
|:--- |:---|
| Valor agregado | Valor de umbral que cada valor de agregado en los resultados de hello debe superar toobe considera una infracción. |
| Activación de alerta según | número de Hola de infracciones de una alerta toobe creado.  Puede especificar **Total de infracciones** para cualquier combinación de infracciones en los resultados de hello establecido o **infracciones consecutivas** toorequire que Hola infracciones se debe producir en muestras consecutivas. |

### <a name="actions"></a>Acciones
Las reglas de alerta, siempre se creará una [alerta registro](#alert-records) cuando se cumpla el umbral de Hola.  También puede definir uno o más de las respuestas toobe ejecutar como enviar un correo electrónico o iniciar un runbook.



#### <a name="email-actions"></a>Acciones de correo electrónico
Acciones de correo electrónico envíen un correo electrónico con los detalles de Hola de tooone alerta Hola o más destinatarios.

| Propiedad | Descripción |
|:--- |:---|
| Notificación por correo electrónico |Especifique **Sí** si desea que un toobe de correo electrónico que se enviará cuando se desencadene la alerta de Hola. |
| Asunto |Asunto de correo electrónico de Hola.  No se puede modificar el cuerpo de saludo del mensaje de Hola. |
| Recipients |Direcciones de todos los destinatarios de correo electrónico.  Si especifica más de una dirección y, a continuación, direcciones de hello independiente con un punto y coma (;). |

#### <a name="webhook-actions"></a>Acciones de webhook
Las acciones de Webhook permiten tooinvoke un proceso externo a través de una única solicitud HTTP POST.

| Propiedad | Descripción |
|:--- |:---|
| webhook |Especifique **Sí** si desea toocall un webhook cuando se desencadene la alerta de Hola. |
| Dirección URL de Webhook |dirección URL de Hola de hello webhook. |
| Incluir la carga personalizada de JSON |Seleccione esta opción si desea que la carga de tooreplace Hola predeterminado con una carga personalizada. |
| Especificar la carga JSON personalizada |carga personalizada de Hola Hola webhook.  Consulte la sección anterior para obtener más información. |

#### <a name="runbook-actions"></a>Acciones de runbook
Las acciones de runbook inician un runbook en Automatización de Azure. 

>[!NOTE]
> Debe tener instalada en el área de trabajo para este toobe de acción habilitada la solución de automatización de Hola. 


| Propiedad | Descripción |
|:--- |:---|
| Runbook | Especifique **Sí** si desea toostart un runbook de automatización de Azure cuando se desencadene la alerta de Hola.  |
| Cuenta de Automation | Especifica la cuenta de automatización que están seleccionados los runbooks de Hola.  Se trata de una cuenta de acción de Hola que se vinculó el área de trabajo de toohello. |
| Seleccionar un runbook | Seleccione runbook Hola desea toostart cuando se crea una alerta. |
| Ejecutar en | Seleccione **Azure** toorun Hola runbook en la nube de Hola.  Seleccione **Hybrid worker** toorun Hola runbook en un agente con [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) instalado.  |




## <a name="next-steps"></a>Pasos siguientes
* Instalar hello [solución de administración de alertas](log-analytics-solution-alert-management.md) recopilan de alertas de tooanalyze creado en el análisis de registros junto con las alertas de System Center Operations Manager (SCOM).
* Obtenga más información sobre las [búsquedas de registros](log-analytics-log-searches.md) que pueden generar alertas.
* Complete un tutorial para [configurar un webhook](log-analytics-alerts-webhooks.md) con una regla de alerta.  
* Obtenga información acerca de cómo toowrite [runbooks en automatización de Azure](https://azure.microsoft.com/documentation/services/automation) problemas tooremediate identificados por las alertas.

