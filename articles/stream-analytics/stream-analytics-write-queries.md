---
title: "aaaHow toowrite consultas de análisis de transmisiones | Documentos de Microsoft"
description: "Escritura de consultas en Análisis de transmisiones y datos de consulta | segmento de ruta de aprendizaje."
keywords: "¿Cómo toowrite consultas, consultar los datos, escribir una consulta, escribir consultas"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a>Cómo toowrite las consultas de análisis de transmisiones
Escribir consultas para el flujo de procesamiento de la lógica de análisis de transmisiones de Azure se implementa como una "consulta permanente" que se define antes de que un trabajo se inicia y se ejecuta con datos alcanzar trabajo Hola. transformación de datos de Hola se expresa en un lenguaje de consulta similar a SQL, que es en gran medida un subconjunto de T-SQL con algunos agregan extensiones de lenguaje como [ventana](https://msdn.microsoft.com/library/azure/dn835019.aspx) utiliza semántica temporal tooexpress.

## <a name="writing-queries"></a>Escritura de consultas:
1. En su trabajo de análisis de transmisiones en el portal de administración de Azure de hello, haga clic en **consulta**.
   
    ![Seleccionar consulta](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    Hola Portal de Azure, haga clic en **consulta**.
   
    ![Vista previa de selección de consulta](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. Nuevos trabajos tienen un toohelp de plantilla de consulta ayudarle a comenzar. consulta de Hello plantilla realiza un "acceso directo" de consulta que proyecta todos los campos de eventos de entrada en la salida de hello.  
   
   * Si ha definido al menos una entrada y salida para el trabajo, puede reemplazar el marcador de posición de Hola "[YourOutputAlias]" y "[YourInputAlias]" campos con alias de Hola Hola de entrada y salida que desea usar en primer lugar. Además, todavía puede crear y probar la consulta en hello Portal clásico de Azure sin definir entradas y salidas de trabajo de Hola.
   * Si desea tooperform procesamiento más complejo que un acceso directo simple, puede editar la definición de la consulta de Hola. tooget a trabajar con consultas de creación, eche un vistazo a algunas consultas comunes se capturan patrones [aquí](stream-analytics-stream-analytics-query-patterns.md).  
   
   ![Ventana de datos de consulta](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a>consultar los datos de toovalidate funciona:
Puede probar que la consulta se comporta según lo esperado mediante la ejecución en el Explorador de hello en uno o más archivos JSON locales que contiene los datos de prueba. Esto no iniciar el trabajo de Hola o tiene las implicaciones de facturación.

> [!NOTE]
> Actualmente no se admite la prueba de consultas en el Explorador de hello Portal de Azure.  
> 
> 

1. Asegúrese de que no hay ningún error en la consulta de hello (en caso contrario Hola prueba botón se deshabilitará) y, a continuación, haga clic en botón de prueba de Hola.  
   
   ![Prueba de datos de consulta](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. Es posible que los archivos toospecify solicitadas para cada una de las entradas de hello hace referencia en la consulta de Hola. En este ejemplo, la consulta de la plantilla de Hola se deja como-es, por lo que está pidiendo al cuadro de diálogo de Hola para una entrada denominada "yourinputalias".  
   
   ![Consulta de datos de prueba](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. Examinar el archivo de prueba de tooa. Varios archivos de ejemplo están disponibles en [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) y también puede recuperar los datos de ejemplo de sus propias entradas de flujo de datos a través de la función de datos de ejemplo en la pestaña de entradas de Hola Hola.  
   
   ![Entrada de consulta](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. Después de cerrar el cuadro de diálogo de hello, la consulta se ejecutará sobre datos de prueba de Hola y verá los resultados de hello en parte inferior de Hola de página de la consulta de Hola.  
   
   ![Resumen de la consulta](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

