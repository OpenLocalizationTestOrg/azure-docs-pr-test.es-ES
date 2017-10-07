---
title: "aaaSet las alertas para las consultas de análisis de transmisiones | Documentos de Microsoft"
description: "Descripción de las entradas del Análisis de transmisiones"
keywords: "configuración de alertas"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/26/2017
ms.author: jeffstok
ms.openlocfilehash: 7b1d90d1468311186567c8518e0283ea6b88c3f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a>Configuración de alertas en Análisis de transmisiones de Azure
## <a name="introduction-monitor-page"></a>Introducción: Página de supervisión
Puede configurar alertas tootrigger una alerta cuando una métrica alcanza una condición que especifique. Por ejemplo, puede configurar una alerta para una condición como Hola siguiente:

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

Las reglas se puede configurar las métricas a través del portal de Hola o pueden configurarse [mediante programación](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) sobre datos de registros de operaciones.

## <a name="set-up-alerts-in-hello-azure-portal"></a>Configurar alertas en hello portal de Azure
1. Hola portal de Azure, abra el trabajo de análisis de transmisiones de hello para que desea toocreate una alerta. 

2. Hola **trabajo** hoja, haga clic en hello **supervisión** sección.  

3. Hola **métrica** hoja, haga clic en hello **Agregar alerta** comando.

      ![Configuración de Azure Portal](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. Escriba un nombre y una descripción.

5. Usar Hola selectores toodefine Hola condición bajo qué Hola se envía la alerta.

6. Proporciona información sobre dónde debe ir alerta Hola.

      ![Configuración de una alerta para un trabajo Azure Stream Analytics](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

Para obtener más información acerca de cómo configurar alertas en hello portal de Azure, consulte [recibir notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).  


## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Análisis de transmisiones de Azure](stream-analytics-get-started.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

