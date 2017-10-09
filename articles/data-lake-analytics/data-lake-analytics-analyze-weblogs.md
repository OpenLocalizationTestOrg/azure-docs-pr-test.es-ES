---
title: "registros de sitio Web de aaaAnalyze con análisis de Data Lake de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo sitio Web de tooanalyze registros con análisis de Data Lake. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 3a196735-d0d9-4deb-ba68-c4b3f3be8403
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: d27aaca95ed2b643cfed7a17b0066bf7fa4a1bf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a>Análisis de registros de sitios web mediante Azure Data Lake Analytics
Obtenga información acerca de cómo tooanalyze registros de sitio Web mediante el análisis de Data Lake, especialmente en averiguar qué remitentes tuvo errores cuando prueba los sitios Web de hello toovisit.

## <a name="prerequisites"></a>Requisitos previos
* **Visual Studio 2015 o Visual Studio 2013**.
* **[Data Lake Tools para Visual Studio](http://aka.ms/adltoolsvs)**.

    Una vez instalado Data Lake Tools para Visual Studio, verá un **Data Lake** elemento Hola **herramientas** menú en Visual Studio:

    ![Menú de Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* **Conocimientos básicos de hello Data Lake Tools para Visual Studio y análisis de Data Lake**. tooget iniciado, vea:

  * [Desarrollo de scripts U-SQL mediante Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* **Una cuenta de Análisis de Data Lake.**  Consulte [Creación de una cuenta de Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
* **Cargar la cuenta de análisis de Data Lake de toohello de datos de ejemplo de Hola.** Vea [archivos de datos de ejemplo de toocopy](data-lake-analytics-get-started-portal.md).

    un trabajo de análisis de Data Lake toorun, necesitará algunos datos. Aunque Hola Data Lake Tools es compatible con la carga de datos, utilizará toomake de datos de ejemplo de Hola tooupload portal Hola este tutorial toofollow más fácil.

## <a name="connect-tooazure"></a>Conectar tooAzure
Antes de que puede compilar y probar cualquier script U-SQL, debe conectarse primero tooAzure.

**tooconnect tooData Lake Analytics**

1. Abra Visual Studio.
2. Haga clic en **Data Lake > Opciones y configuración**.
3. Haga clic en **inicio de sesión**, o **Cambiar usuario** si alguien ha iniciado sesión en y siga las instrucciones de Hola.
4. Haga clic en **Aceptar** tooclose diálogo de opciones y configuración de Hola.

**toobrowse sus cuentas de análisis de Data Lake**

1. En Visual Studio, presione **CTRL+ALT+S** para abrir el **Explorador de servidores**.
2. En el **Explorador de servidores**, expanda **Azure** y después **Data Lake Analytics**. Verá una lista de las cuentas de Análisis de Data Lake, si las hay. No se puede crear cuentas de análisis de Data Lake de studio Hola. toocreate una cuenta, consulte [empezar a trabajar con análisis de Data Lake de Azure mediante el Portal de Azure](data-lake-analytics-get-started-portal.md) o [empezar a trabajar con análisis de Data Lake de Azure con Azure PowerShell](data-lake-analytics-get-started-powershell.md).

## <a name="develop-u-sql-application"></a>Desarrollo de aplicaciones U-SQL
Una aplicación U-SQL es principalmente un script U-SQL. toolearn más información acerca de T-SQL, consulte [empezar a trabajar con U-SQL](data-lake-analytics-u-sql-get-started.md).

Puede agregar aplicación toohello de adición operadores definidos por el usuario.  Para obtener más información, consulte [Desarrollo de operadores U-SQL definidos por el usuario para trabajos de Análisis de Data Lake](data-lake-analytics-u-sql-develop-user-defined-operators.md).

**toocreate y enviar un trabajo de análisis de Data Lake**

1. Haga clic en hello **archivo > Nuevo > proyecto**.
2. Seleccione el tipo de proyecto de U-SQL de Hola.

    ![nuevo proyecto de Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. Haga clic en **Aceptar**. Visual Studio crea una solución con un archivo Script.usql.
4. Escriba Hola siguiente secuencia de comandos en el archivo de hello Script.usql:

        // Create a database for easy reuse, so you don't need tooread from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from hello weblog file with hello correct schema.
        DROP FUNCTION IF EXISTS SampleDBTutorials.dbo.WeblogsView;
        CREATE FUNCTION SampleDBTutorials.dbo.WeblogsView()
        RETURNS @result TABLE
        (
            s_date DateTime,
            s_time string,
            s_sitename string,
            cs_method string,
            cs_uristem string,
            cs_uriquery string,
            s_port int,
            cs_username string,
            c_ip string,
            cs_useragent string,
            cs_cookie string,
            cs_referer string,
            cs_host string,
            sc_status int,
            sc_substatus int,
            sc_win32status int,
            sc_bytes int,
            cs_bytes int,
            s_timetaken int
        )
        AS
        BEGIN

            @result = EXTRACT
                s_date DateTime,
                s_time string,
                s_sitename string,
                cs_method string,
                cs_uristem string,
                cs_uriquery string,
                s_port int,
                cs_username string,
                c_ip string,
                cs_useragent string,
                cs_cookie string,
                cs_referer string,
                cs_host string,
                sc_status int,
                sc_substatus int,
                sc_win32status int,
                sc_bytes int,
                cs_bytes int,
                s_timetaken int
            FROM @"/Samples/Data/WebLog.log"
            USING Extractors.Text(delimiter:' ');
            RETURN;
        END;

        // Create a table for storing referrers and status
        DROP TABLE IF EXISTS SampleDBTutorials.dbo.ReferrersPerDay;
        @weblog = SampleDBTutorials.dbo.WeblogsView();
        CREATE TABLE SampleDBTutorials.dbo.ReferrersPerDay
        (
            INDEX idx1
            CLUSTERED(Year ASC)
            DISTRIBUTED BY HASH(Year)
        ) AS

        SELECT s_date.Year AS Year,
            s_date.Month AS Month,
            s_date.Day AS Day,
            cs_referer,
            sc_status,
            COUNT(DISTINCT c_ip) AS cnt
        FROM @weblog
        GROUP BY s_date,
                cs_referer,
                sc_status;

    Hola toounderstand T-SQL, vea [empezar a trabajar con el idioma de Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).    
5. Agregue un nuevo proyecto de tooyour de script U-SQL y escriba Hola siguiente:

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. Cambiar script U-SQL de la primera toohello atrás y siguiente toohello **enviar** botón, especifique la cuenta de análisis.
7. En el **Explorador de soluciones**, haga clic con el botón derecho en **Script.usql** y después haga clic en **Build Script** (Compilar script). Comprobar los resultados de hello en el panel de salida de hello.
8. En el **Explorador de soluciones**, haga clic con el botón derecho en **Script.usql** y después haga clic en **Submit Script** (Enviar script).
9. Comprobar hello **cuenta Analytics** es hello uno donde desea toorun Hola trabajo y, a continuación, haga clic en **enviar**. Resultados de envío y vínculo de trabajo están disponibles en hello Data Lake Tools para la ventana de resultados de Visual Studio cuando se completa el envío de Hola.
10. Espere hasta que el trabajo de Hola se completa correctamente.  Si se produce un error en el trabajo de hello, probablemente falta archivo de código fuente de Hola.  Vea la sección Requisitos previos de Hola de este tutorial. Para obtener más información sobre la solución de problemas, consulte [Supervisión y solución de problemas con trabajos de Análisis de Azure Data Lake](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).

    Cuando se completa el trabajo de hello, verá Hola después de pantalla:

    ![análisis de data lake analizar registros web registros de sitios web](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. Ahora repita los pasos del 7 al 10 para **Script1.usql**.

**salida del trabajo hello toosee**

1. De **Explorador de servidores**, expanda **Azure**, expanda **análisis de Data Lake**, expanda y su cuenta de análisis de Data Lake **decuentasdealmacenamiento**, haga clic en la cuenta de almacenamiento de datos Lake Hola predeterminada y, a continuación, haga clic en **Explorer**.
2. Haga doble clic en **ejemplos** tooopen Hola carpeta y, a continuación, haga doble clic en **salidas**.
3. Haga doble clic en **UnsuccessfulResponsees.log**.
4. También puede hacer doble clic archivo de salida de hello dentro de la vista de gráfico de Hola de trabajo de hello en orden toonavigate directamente toohello de salida.

## <a name="see-also"></a>Otras referencias
tooget a trabajar con análisis de Data Lake con herramientas diferentes, vea:

* [Introducción a Análisis de Data Lake mediante el Portal de Azure](data-lake-analytics-get-started-portal.md)
* [Introducción a Análisis de Data Lake mediante Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Introducción a Análisis de Data Lake mediante .NET SDK](data-lake-analytics-get-started-net-sdk.md)
