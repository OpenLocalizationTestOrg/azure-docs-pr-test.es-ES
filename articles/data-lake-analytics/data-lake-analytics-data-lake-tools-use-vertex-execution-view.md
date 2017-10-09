---
title: "Hola aaaUse vista de ejecución de vértices de Data Lake Tools para Visual Studio | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola trabajos de análisis de Data Lake tooexam de vista de la ejecución de vértices."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a>Usar hello vista de ejecución de vértices en Data Lake Tools para Visual Studio
Obtenga información acerca de cómo toouse Hola trabajos de análisis de Data Lake tooexam de vista de la ejecución de vértices.

## <a name="prerequisites"></a>Requisitos previos

Se necesitan conocimientos básicos del uso de Data Lake Tools para secuencia de comandos de Visual Studio toodevelop U-SQL.  Vea [Tutorial: Desarrollo de scripts U-SQL mediante Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).

## <a name="open-hello-vertex-execution-view"></a>Hola Abrir vista de ejecución de vértices
Abra un trabajo de U-SQL en Data Lake Tools para Visual Studio. Haga clic en **vista de ejecución de vértices** en la esquina izquierda inferior de Hola. Es posible que los perfiles de tooload solicitadas en primer lugar y puede tardar algún tiempo, según la conectividad de red.

![Vista de ejecución de vértices de Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a>Comprensión de la vista de ejecución de vértices
Hola vértices ejecución vista tiene tres partes:

![Vista de ejecución de vértices de Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

Hola **selector de vértices** en permite izquierdo Hola seleccionar vértices características (como top 10 datos leer, o elija por fase). Uno de los filtros usados con más frecuencia hello es hello toosee **vértices en la ruta crítica**. Hola **ruta crítica** Hola cadena más larga de vértices de un trabajo de SQL U. Ruta de acceso crítica Hola de descripción es útil para optimizar los trabajos mediante la comprobación de los vértices lleva tiempo más largo de Hola.
  
![Vista de ejecución de vértices de Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

panel del centro superior de Hello muestra hello **ejecutando el estado de todos los vértices de hello**.
  
![Vista de ejecución de vértices de Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

panel de Hello inferior central muestra información sobre cada vértice:
* Nombre del proceso: nombre de Hola de instancia de vértices Hola. Se compone de distintas partes de StageName|VertexName|VertexRunInstance. Por ejemplo, vértices de hello SV7_Split .v1 [62] significa Hola segunda instancia en ejecución (.v1, índice que empieza por 0) del número de vértices 62 en fase SV7_Split.
* Lectura de datos total/escrito: datos de hello estaban leídos/escritos por este vértice.
* Estado de estado y de salida: Hola estado final cuando finaliza el vértice de Hola.
* Tipo de código o con errores de salida: error de Hola cuando vértices Hola produce un error.
* Motivo de creación: ¿Por qué vértices Hola se crean.
* Latencia de la cola de latencia/PN de recursos latencia o proceso: Hola tiempo de hello vértices toowait para los recursos, datos de tooprocess y toostay en cola Hola.
* GUID de proceso/creador: El GUID de vértice de ejecución actual de Hola o su autor.
* Versión: una instancia Hola N-ésimo de hello ejecutando vértices (sistema de hello puede programar nuevas instancias de un vértice por diversos motivos, por ejemplo, conmutación por error, de proceso redundancia, etcetera).
* Hora de creación de la versión
* Crear inicio tiempo o proceso en cola tiempo o proceso inicio tiempo o proceso completado de procesar tiempo: cuando inicia el proceso de vértices Hola creación; proceso de vértices de hello cuando inicia tooqueue; Hola cuando cierta vértices proceso comienza; Cuando Hola vértices se ha completado.

## <a name="next-steps"></a>Pasos siguientes
* información de diagnóstico de toolog, consulte [acceso a registros de diagnóstico para el análisis de Azure Data Lake](data-lake-analytics-diagnostic-logs.md)
* toosee una consulta más compleja, vea [sitio Web de analizar registros con análisis de Azure Data Lake](data-lake-analytics-analyze-weblogs.md).
* Detalles del trabajo tooview, consulte [trabajo utilizar un explorador y la vista de trabajos de trabajos de análisis de Azure Data lake](data-lake-analytics-data-lake-tools-view-jobs.md)
