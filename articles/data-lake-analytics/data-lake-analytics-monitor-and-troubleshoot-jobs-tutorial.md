---
title: "trabajos de análisis de Azure Data Lake aaaTroubleshoot mediante el Portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola trabajos de análisis de Data Lake tootroubleshoot de Portal de Azure. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a>Solución de problemas de trabajos de Análisis de Azure Data Lake mediante el Portal de Azure
Obtenga información acerca de cómo toouse Hola trabajos de análisis de Data Lake tootroubleshoot de Portal de Azure.

En este tutorial, se la instalación de un problema de archivo de origen que faltan y utilizar hello Azure Portal tootroubleshoot Hola problema.

## <a name="submit-a-data-lake-analytics-job"></a>Envío de un trabajo de Análisis de Data Lake

Enviar Hola después de trabajo U-SQL:

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
Hola definido en el script de Hola de archivo de origen es **/Samples/Data/SearchLog.tsv1**, donde debería ser **/Samples/Data/SearchLog.tsv**.


## <a name="troubleshoot-hello-job"></a>Solucionar problemas de trabajo de Hola

**toosee Hola a todos los trabajos**

1. En el portal de Azure hello, haga clic en **Microsoft Azure** en la esquina superior izquierda de Hola.
2. Haga clic en el icono de hello con su nombre de cuenta de análisis de Data Lake.  Resumen de trabajos de Hola se muestra en hello **administración del trabajo** icono.

    ![Administración de trabajos de Análisis de Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    trabajo de Hello administración le ofrece una vista de estado del trabajo de Hola. Observe que hay un trabajo con error.
3. Haga clic en hello **administración del trabajo** icono trabajos de hello toosee. trabajos de Hola se clasifican en **ejecutando**, **en cola**, y **finalizado**. Verá que el trabajo con errores en hello **finalizado** sección. Deberá ser primera de ellas en la lista de Hola. Cuando tiene una gran cantidad de trabajos, haga clic en **filtro** toohelp se toolocate trabajos.

    ![Trabajos de filtro de Análisis de Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. Haga clic en trabajo con error Hola de detalles del trabajo de Hola Hola lista tooopen en una nueva hoja:

    ![Trabajos con error de Análisis de Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    Hola aviso **reenviar** botón. Después de corregir el problema de hello, puede volver a enviar el trabajo de Hola.
5. Haga clic en la parte resaltada de detalles de hello anterior captura de pantalla tooopen Hola error.  Verá algo parecido a lo siguiente:

    ![Detalles de trabajos con error de Análisis de Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    Indica que no se encuentra la carpeta de origen de Hola.
6. Haga clic en **Duplicar script**.
7. Hola de actualización **FROM** siguiente toohello de ruta de acceso:

    "/ Samples/Data/SearchLog.tsv"
8. Haga clic en **Enviar trabajo**.

## <a name="see-also"></a>Otras referencias
* [Información general de Análisis de Azure Data Lake](data-lake-analytics-overview.md)
* [Introducción a Análisis de Azure Data Lake mediante Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Introducción a Análisis de Azure Data Lake y a U-SQL mediante Visual Studio](data-lake-analytics-u-sql-get-started.md)
* [Administración de Análisis de Azure Data Lake mediante el Portal de Azure](data-lake-analytics-manage-use-portal.md)
