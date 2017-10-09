---
title: "cuenta de automatización de Azure de análisis de registros aaaUnlink | Documentos de Microsoft"
description: "Este artículo proporciona información general sobre cómo toounlink la automatización de Azure de la cuenta de un área de trabajo OMS."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a>¿Cómo toounlink la automatización de la cuenta de un área de trabajo de análisis de registros

Automatización de Azure se integra con análisis de registros toonot solo compatibilidad con la supervisión proactiva de los trabajos de runbook a través de todas las cuentas de automatización, pero también es necesario cuando se importa Hola siguiendo las soluciones que dependan de análisis de registros:

* [Administración de actualizaciones](../operations-management-suite/oms-solution-update-management.md)
* [Seguimiento de cambios](../log-analytics/log-analytics-change-tracking.md)
* [Inicio y detención de máquinas virtuales durante las horas de trabajo](automation-solution-vm-management.md)
 
Si decide que ya no desea toointegrate su cuenta de automatización con análisis de registros, puede desvincular la cuenta directamente desde Hola portal de Azure.  Antes de continuar, primero deberá soluciones de hello tooremove que se ha mencionado anteriormente, en caso contrario, este proceso se impedirá continuar.  Tema de Hola de revisión para solución concreta Hola ha importado pasos de hello toounderstand necesarios tooremove lo.  

Después de quitar estas soluciones pueden realizar Hola siguiendo los pasos toounlink su cuenta de automatización.

## <a name="unlink-workspace"></a>Unlink workspace (Desvincular área de trabajo)

1. En hello portal de Azure, abra su cuenta de automatización y, en la hoja de cuenta de automatización de hello, en la hoja de la cuenta de hello, seleccione **desvincular el área de trabajo**.<br><br> ![Opción para desvincular el área de trabajo](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)<br><br>  
2. En la hoja de hello desvincular área de trabajo, haga clic en **desvincular el área de trabajo**.<br><br> ![Hoja Unlink workspace (Desvincular área de trabajo)](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).<br><br>  Recibirá un aviso de comprobar que se va tooproceed.<br><br>
3. Mientras la automatización de Azure intenta toounlink cuenta de hello en el área de trabajo de análisis de registros, puede seguir el progreso de hello en **notificaciones** en el menú de Hola.

Si ha usado la solución de administración de actualizaciones de hello, opcionalmente, puede que desee hello tooremove siguientes elementos que ya no son necesarios después de quitar la solución de Hola.

* Actualice las programaciones.  Cada uno tendrá nombres que coinciden con las implementaciones de actualizaciones de hello creaste)

* Grupos de trabajo híbrido creados para la solución de Hola.  Cada uno de ellos se denominarán del mismo modo demasiado machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).

Si usa máquinas virtuales de inicio/detención de Hola durante la solución de fuera del horario comercial, opcionalmente, puede que desee hello tooremove siguientes elementos que ya no son necesarios después de quitar la solución de Hola.

* Programaciones de runbook de inicio y detención de máquinas virtuales 
* Runbooks de inicio y detención de máquinas virtuales
* Variables   

## <a name="next-steps"></a>Pasos siguientes

tooreconfigure su toointegrate de cuenta de automatización con análisis de registros de OMS, consulte [reenviar el estado del trabajo y flujos de trabajo de automatización tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md). 
