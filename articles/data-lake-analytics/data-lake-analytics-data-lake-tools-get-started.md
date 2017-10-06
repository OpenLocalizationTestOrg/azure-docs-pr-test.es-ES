---
title: las secuencias de comandos de aaaDevelop U-SQL mediante Data Lake Tools para Visual Studio | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall Data Lake Tools para Visual Studio y cómo las secuencias de comandos SQL U toodevelop y prueba."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a>Desarrollo de scripts U-SQL mediante Data Lake Tools para Visual Studio
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


Obtenga información acerca de cómo las cuentas de análisis de Azure Data Lake de toocreate de toouse Visual Studio, definir trabajos en [U-SQL](data-lake-analytics-u-sql-get-started.md)y enviar el servicio de análisis de Data Lake toohello de trabajos. Para obtener más información acerca de Análisis de Data Lake, consulte [Información general sobre Análisis de Azure Data Lake](data-lake-analytics-overview.md).


## <a name="prerequisites"></a>Requisitos previos

* **Visual Studio**: se admiten todas las ediciones, excepto Express.
    * Visual Studio 2017
    * Visual Studio 2015
    * Visual Studio 2013
* **Microsoft Azure SDK para .NET** versión 2.7.1, o posterior.  Instalar mediante hello [instalador de plataforma Web](http://www.microsoft.com/web/downloads/platform.aspx).
* Una cuenta de **Data Lake Analytics**. toocreate una cuenta, consulte [empezar a trabajar con análisis de Data Lake de Azure mediante el portal de Azure](data-lake-analytics-get-started-portal.md).

## <a name="install-azure-data-lake-tools-for-visual-studio"></a>Instalación de Herramientas de Azure Data Lake para Visual Studio 

Descargue e instale Azure Data Lake Tools para Visual Studio [desde el centro de descarga de hello](http://aka.ms/adltoolsvs). Después de la instalación tenga en cuenta que:
* Hola **Explorador de servidores** > **Azure** nodo contiene un **análisis de Data Lake** nodo. 
* Hola **herramientas** menú tiene un **Data Lake** elemento.

## <a name="connect-tooan-azure-data-lake-analytics-account"></a>Conectar con cuenta de análisis de Azure Data Lake tooan

1. Abra Visual Studio.
2. Abra el Explorador de servidores, para lo que debe seleccionar **Vista** > **Explorador de servidores**.
3. Haga clic con el botón derecho en **Azure**. A continuación, seleccione **conectar tooMicrosoft suscripción de Azure** y siga las instrucciones de Hola.
4. En el Explorador de servidores, seleccione **Azure** > **Data Lake Analytics**. Verá una lista de las cuentas de Data Lake Analytics.


## <a name="write-your-first-u-sql-script"></a>Escriba el primer script U-SQL

Hola después de texto es un script U-SQL simple. Define un conjunto de datos pequeño y escrituras de almacén de forma predeterminada Data Lake de conjunto de datos toohello como un archivo denominado `/data.csv`.

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

### <a name="submit-a-data-lake-analytics-job"></a>Envío de un trabajo de Análisis de Data Lake

1. Seleccione **Archivo** > **Nuevo** > **Proyecto**.

2. Seleccione hello **U-SQL proyecto** escriba y, a continuación, haga clic en **Aceptar**. Visual Studio crea una solución con un archivo **Script.usql**.

3. Pegue el script anterior de hello en hello **Script.usql** ventana.

4. En la esquina superior izquierda de Hola de hello **Script.usql** ventana, especifique la cuenta de análisis de Data Lake Hola.

    ![Enviar proyecto U-SQL de Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. En la esquina superior izquierda de Hola de hello **Script.usql** ventana, seleccione **enviar**.
6. Comprobar hello **cuenta Analytics**y, a continuación, seleccione **enviar**. Resultados de envío están disponibles en hello Data Lake Tools para resultados de Visual Studio, una vez completada la presentación de Hola.

    ![Enviar proyecto U-SQL de Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. toosee hello más reciente trabajo estado y la actualización de pantalla de bienvenida, haga clic en **actualizar**. Cuando se realiza correctamente el trabajo de hello, muestra hello **trabajo gráfico**, **las operaciones de metadatos**, **historial de estado**, y **diagnósticos**:

    ![Gráfico de rendimiento del trabajo de Data Lake Analytics de U-SQL Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * **Resumen de trabajo** muestra Hola resumen del trabajo de Hola.   
   * **Detalles del trabajo** muestra información más específica sobre el trabajo de hello, incluidos los script de Hola, los recursos y los vértices.
   * **Gráfico de trabajo** muestra el progreso de Hola de trabajo de Hola.
   * **Las operaciones de metadatos** muestra todas las acciones de Hola que se realizaron en el catálogo de hello U-SQL.
   * **Datos** muestra todas las entradas de Hola y salidas.
   * **Diagnósticos** proporciona un análisis avanzado para la optimización de rendimiento y la ejecución del trabajo.

### <a name="toocheck-job-state"></a>estado del trabajo toocheck

1. En el Explorador de servidores, seleccione **Azure** > **Data Lake Analytics**. 
2. Expanda el nombre de la cuenta de hello análisis de Data Lake.
3. Haga doble clic en **Trabajos**.
4. Seleccione el trabajo de Hola que ha enviado anteriormente.

### <a name="toosee-hello-output-of-a-job"></a>salida de hello toosee de un trabajo

1. En el Explorador de servidores, buscar trabajo toohello que ha enviado.
2. Haga clic en hello **datos** ficha.
3. Hola **salidas de trabajo** ficha, seleccione hello `"/data.csv"` archivo.

## <a name="next-steps"></a>Pasos siguientes

* [Prueba y depuración de trabajos U-SQL mediante la ejecución local y el SDK de U-SQL para Azure Data Lake](data-lake-analytics-data-lake-tools-local-run.md)
* [Depuración de trabajos U-SQL](data-lake-analytics-debug-u-sql-jobs.md)
* [Usar hello Azure Data Lake Tools para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)
