---
title: "aaaDebug mediante registros de operación y el servicio de análisis de transmisiones | Documentos de Microsoft"
description: "Flujo de cómo toouse registros de operaciones de análisis"
keywords: registros de servicios
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a>Depuración de los trabajos de Análisis de transmisiones mediante registros de operaciones y servicios
Todos los servicios de Azure de alimentación operativa mensajes toousers toorecord detalles de registro a relacionados con operaciones de toomanagement. En el análisis de transmisiones de Azure, esta información puede usarse para fines de depuración como ver el estado del trabajo, el progreso del trabajo y el progreso de Hola de tootrack de mensajes de error de un trabajo con el tiempo de inicio tooprocessing toooutput.

## <a name="find-operation-logs-in-hello-azure-management-portal"></a>Buscar registros de operaciones en el portal de administración de Azure de Hola
A los registros de operaciones se puede acceder de dos maneras:  

* Panel de trabajo de análisis de transmisiones de Hola  
* Servicios de administración de portal de Azure clásico de Hola  

## <a name="dashboard-of-hello-stream-analytics-job"></a>Panel de trabajo de análisis de transmisiones de Hola
Un toohello de vínculo correspondiente registros de un trabajo de análisis de transmisiones se muestra en la pestaña del panel del trabajo de Hola. Si hace clic en ese vínculo, establece filtros Hola de una manera que muestra registros más recientes para ese trabajo.

  ![Selección de registros de servicios de administración](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a>Servicios de administración
toomanually navegar toohello registros de operaciones de análisis de transmisiones y otros servicios en el portal de Azure clásico de hello:

1. Haga clic en **servicios de administración de** en hello [portal de Azure clásico](https://manage.windowsazure.com).
2. Seleccione **análisis de transmisiones** para **tipo** y el nombre de Hola Hola del trabajo de para **nombre del servicio**.  
   
   ![Seleccionar el Análisis de transmisiones](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a>Buscar registros de auditoría en hello portal de Azure
toofind registros operativos para el trabajo de análisis de transmisiones en hello portal de Azure, haga clic en **examinar** y, a continuación, seleccione **registros de auditoría**.

  ![Selección de Stream Analytics en Azure Portal](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

Se abrirá una hoja con los últimos 7 días para todos los recursos de eventos de hello en su suscripción.  Puede filtrar eventos de toosee de un tipo de especificar o el período de tiempo, haga clic en hello **filtro** comando.

  ![Selección de Stream Analytics en Azure Portal](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a>Obtención de detalles de registro
Puede filtrar por intervalo de tiempo y registros de estado tooview hello para el trabajo.

En el portal de administración de Azure de hello, haga clic en hello **detalles** situado en la parte inferior de Hola de hello ventana tooview más detalles sobre un evento seleccionado. 

  ![Seleccionar detalles](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

Hola portal de Azure, haga clic en un toosee de entrada de registro Hola eventos detallados dentro de él.

  ![Selección de detalles en Azure Portal](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

Desde aquí, puede abrir hello **detalle** hoja haciendo clic en el evento de Hola.

  ![Selección de detalles en Azure Portal](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a>Depuración de un trabajo con error
En el portal de administración de Azure de hello, haga clic en el icono de búsqueda de Hola y escriba 'Error'. Esto genera todos los registros con errores. 

  ![Depuración de un trabajo con error](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

Hola portal de Azure, puede filtrar por nivel de mensaje tooview **crítico** eventos.

  ![Depuración en Azure Portal](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

Puede seleccionar cualquiera de los errores de Hola y haga clic en hello **detalles** para obtener más información sobre el error de Hola.  Algunos mensajes de error también proporcionan información acerca de cómo toomitigate Hola problema. 

  ![Detalles de la operación](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

Si necesita toocontact [compatibilidad](https://azure.microsoft.com/support/options/) o proporcionar información toohello equipo a través de hello [foro de MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), detalles de la operación de hello, tenga en cuenta específicamente Hola **Id. de correlación**. 

## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

