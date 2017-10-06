---
title: "aaaGet iniciado con análisis de Data Lake de Azure mediante el portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo crear un trabajo de análisis de Data Lake mediante SQL U toouse hello toocreate portal Azure una cuenta de análisis de Data Lake y enviar el trabajo de Hola. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a>Introducción al uso de Azure Portal por parte de Azure Data Lake Analytics
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Obtenga información acerca de cómo toouse Hola cuentas de análisis de Azure Data Lake de Azure toocreate portal, definir trabajos en [U-SQL](data-lake-analytics-u-sql-get-started.md)y enviar el servicio de análisis de Data Lake toohello de trabajos. Para obtener más información acerca de Análisis de Data Lake, consulte [Información general sobre Análisis de Azure Data Lake](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Requisitos previos

Para comenzar este tutorial, es preciso tener una **suscripción a Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-a-data-lake-analytics-account"></a>Creación de una cuenta de Análisis de Data Lake

Ahora, se creará un análisis de Data Lake y un almacén de Data Lake cuenta Hola mismo tiempo.  Este paso es sencillo y sólo tarda aproximadamente toofinish de 60 segundos.

1. Inicio de sesión toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **Nuevo** >  **Datos y análisis** > **Data Lake Analytics**.
3. Seleccione los valores de hello siguientes elementos:
   * **Nombre**: nombre de la cuenta de Data Lake Analytics (solo se permiten letras minúsculas y números).
   * **Suscripción**: elija la suscripción de Azure usada para la cuenta de análisis de Hola Hola.
   * **Grupo de recursos**. seleccione un grupo de recursos de Azure existente o cree uno nuevo.
   * **Ubicación**. Seleccione un centro de datos de Azure para la cuenta de análisis de Data Lake Hola.
   * **Almacén de Data Lake**: siga Hola instrucción toocreate una nueva cuenta de almacén de Data Lake o seleccione uno existente. 
4. Si lo desea, seleccione un plan de tarifa para la cuenta de Data Lake Analytics.
5. Haga clic en **Crear**. 


## <a name="your-first-u-sql-script"></a>El primer script U-SQL

Hola después de texto es un script U-SQL muy simple. Todo lo que hace es definir un conjunto de datos pequeño script de Hola y, a continuación, escriba ese conjunto de datos a almacén de Data Lake de toohello de forma predeterminada como un archivo denominado `/data.csv`.

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a>Envío de un trabajo de U-SQL

1. En la cuenta de análisis de Data Lake hello, haga clic en **nuevo trabajo**.
2. Pegue en texto hello de hello script U-SQL mostrado anteriormente. 
3. Haga clic en **Enviar trabajo**.   
4. Espere hasta que cambie de estado de trabajo de hello demasiado**correcto**.
5. Si se produce un error en el trabajo de hello, consulte [supervisar y solucionar problemas de trabajos de análisis de Data Lake](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).
6. Haga clic en hello **salida** ficha y, a continuación, haga clic en `data.csv`. 

## <a name="see-also"></a>Otras referencias

* tooget a desarrollar aplicaciones SQL U, consulte [scripts U T-SQL desarrollar con Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* toolearn T-SQL, vea [empezar a trabajar con el lenguaje de Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).
* Para conocer las tareas de administración, consulte [Administración de Azure Data Lake Analytics mediante el Azure Portal](data-lake-analytics-manage-use-portal.md).
