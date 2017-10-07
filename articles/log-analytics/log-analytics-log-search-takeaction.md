---
title: "aaaUser acción iniciada por Azure automatización de Runbook en análisis de registros | Documentos de Microsoft"
description: "Este artículo describe cómo toorun un runbook de automatización de un análisis de registros buscar resultados a petición."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 53c25431572babd5fd54bf964e4683077e2a4c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="take-action-with-an-automation-runbook-from-a-log-analytics-log-search-result"></a>Realizar acciones con un runbook de Automation desde un resultado de búsqueda de registros de Log Analytics

Desde un resultado de búsqueda de registros de análisis de registros de Azure, ahora puede seleccionar **actuar** toorun un runbook de automatización.  Hello runbook puede utilizarse tooremediate Hola problema o realizar alguna otra acción, como recopilar información de solución de problemas, envíe un correo electrónico o crear una solicitud de servicio. 

## <a name="components-and-features-used"></a>Componentes y características usados
* [Cuenta de Azure Automation](../automation/automation-offering-get-started.md)
* [Área de trabajo de Log Analytics](../log-analytics/log-analytics-overview.md)

## <a name="tooinitiate-runbook-from-log-search"></a>runbook tooinitiate de búsqueda de registros

acción de tootake en un evento e iniciar un runbook desde los resultados de búsqueda de registros, primero debe crear una búsqueda de registros y de resultados de hello puede invocar un runbook a petición.  Esto se puede lograr de la característica de búsqueda de registro de hello en hello Azure o [portal de OMS](../log-analytics/log-analytics-log-searches.md).  En este ejemplo, llevamos a cabo una búsqueda de registros de hello portal de Azure con una demostración básica de esta característica.

1. Hola portal de Azure, en el menú del concentrador de hello, haga clic en **más servicios** y seleccione **análisis de registros**.  
2. En la hoja de análisis de registros de hello, seleccione el área de trabajo de análisis de registros y en la hoja de área de trabajo de hello seleccione **búsqueda de registros**.  
3. En la hoja de la búsqueda de registros de hello, realice una búsqueda de registros.  
4. En resultados de la búsqueda de registro de hello, haga clic en izquierda de toohello de elipse Hola de uno de los campos de Hola y de la ventana emergente de hello, seleccione **actuar**.<br><br> ![Seleccionar Realizar acción a partir del resultado de búsqueda](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png) 
5. En la hoja de acción de hello Take, seleccione **ejecutar un runbook**y en hello **ejecutar un runbook** hoja puede seleccionar un runbook toorun.  Puede seleccionar cualquier runbook Hola cuenta de automatización que es el área de trabajo de análisis de registros de toohello vinculado.  Tenga en cuenta los siguiente hello:

    * Los runbooks se organizan por etiquetas.
    * Valores de parámetro de entrada del runbook se pueden seleccionar directamente de campos de Hola Hola del resultado de búsqueda.  Aparecerá una lista de lista desplegable para mostrar todos los campos disponibles de Hola de hello resultado tooselect desde.  
    * Puede elegir toorun Hola runbook en un [runbook worker híbrido](../automation/automation-hybrid-runbook-worker.md) que ha instalado en la máquina de Hola que tienes problemas de hello si tiene un grupo de Hybrid Runbook Worker correspondiente que contenga solo este equipo como miembro.  Si Hola nombre del grupo de Hybrid Worker Hola coincide con hello del equipo de Hola que se encuentra en el resultado de búsqueda de registro de hello, el grupo de Hola se selecciona automáticamente.    

6. Tras hacer clic en **ejecutar**, abrirá la hoja de trabajo de runbook de hello tooallow se tooreview Hola estado del trabajo de Hola.   

Si selecciona un runbook que estaba configurado toobe [llama desde una alerta de análisis de registros](../automation/automation-invoke-runbook-from-omsla-alert.md), tiene un parámetro de entrada llamado **WebhookData** decir **objeto** tipo.  Si el parámetro de entrada de hello es obligatorio, debe toopass Hola búsqueda resultados toohello runbook por lo que puede convertir la cadena con formato JSON de hello en un tipo de objeto que permite toofilter en elementos específicos que se hace referencia en las actividades de runbooks.  Puede hacer esto seleccionando **buscar resultados (objeto)** de lista desplegable de Hola.<br><br> ![Seleccionar el objeto de datos de webhook para el parámetro de runbook](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)   
    
## <a name="next-steps"></a>Pasos siguientes

* Hola de revisión [referencia de búsqueda de registro de análisis de registros](log-analytics-search-reference.md) tooview todos Hola buscar campos y facetas disponibles en el análisis de registros.
* toolearn cómo revisar automáticamente, tooinvoke un runbook de automatización [llamar a un runbook de automatización de Azure desde una alerta de análisis de registros de OMS](../automation/automation-invoke-runbook-from-omsla-alert.md).  
