---
title: aaaUse Apache Storm con Power BI - HDInsight de Azure | Documentos de Microsoft
description: "Creación de un informe de Power BI usando datos de una topología de C# que se ejecuta en un clúster de Apache Storm en HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a>Usar datos de Power BI toovisualize de una topología de Apache Storm

Power BI permite toovisually mostrar datos como informes. Este documento proporciona un ejemplo de cómo toouse Apache Storm en HDInsight toogenerate datos para Power BI.

> [!NOTE]
> Hello pasos de este documento se basan en un entorno de desarrollo de Windows con Visual Studio. proyecto compilado Hola puede ser enviado tooa clúster de HDInsight basados en Linux. Solo los clústeres basados en Linux creados con posterioridad al 28/10/2016 admiten topologías SCP.NET.
>
> toouse una topología de C# con un clúster basado en Linux, Hola de actualización de paquetes de Microsoft.SCP.Net.SDK NuGet utilizado por el tooversion proyecto 0.10.0.6 o superior. versión de Hola del paquete de hello también debe coincidir con la versión principal de Hola de Storm instalado en HDInsight. Por ejemplo, en las versiones de HDInsight 3.3 y 3.4 se usa Storm 0.10.x, mientras que en HDInsight 3.5 se usa Storm 1.0.x.
>
> Topologías de C# en clústeres basados en Linux deben usar .NET 4.5 y usar toorun Mono en clúster de HDInsight Hola. La mayoría funcionará. Sin embargo debe comprobar hello [Mono compatibilidad](http://www.mono-project.com/docs/about-mono/compatibility/) documento para detectar posibles incompatibilidades.
>
> Para obtener una versión de Java de este proyecto que funciona con HDInsight basado en Windows o en Linux, vea [Procesamiento de eventos desde Azure Event Hubs con Storm en HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="prerequisites"></a>Requisitos previos

* Un usuario de Azure Active Directory con acceso a [Power BI](https://powerbi.com).
* Un clúster de HDInsight. Para más información, vea [Introducción a los ejemplos de Storm Starter para análisis de macrodatos en HDInsight basado en Linux](hdinsight-apache-storm-tutorial-get-started-linux.md).

  > [!IMPORTANT]
  > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio (uno de hello siguiendo las versiones)

  * Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)
  * Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio Community 2013](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * Visual Studio 2017 (cualquier edición)

* Hola HDInsight Tools para Visual Studio: vea [Introducción al uso de hello HDInsight Tools para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) para obtener información sobre la información de instalación.

## <a name="how-it-works"></a>Cómo funciona

Este ejemplo contiene una topología de Storm en C# que genera de forma aleatoria los datos de registro de Internet Information Services (IIS). Estos datos se escriben tooa base de datos SQL y, a partir de ahí es toogenerate usa informes de Power BI.

Hola después de implementar archivos Hola funcionalidad principal de este ejemplo:

* **SqlAzureBolt.cs**: escribe la información que se produce en hello Storm topología tooSQL base de datos.
* **IISLogsTable.sql**: Hola Transact-SQL instrucciones que se utilizan toogenerate Hola base de datos que Hola datos se almacenan en.

> [!WARNING]
> Crear tabla de hello en la base de datos SQL antes de iniciar la topología de hello en el clúster de HDInsight.

## <a name="download-hello-example"></a>Descargar el ejemplo hello

Descargar hello [ejemplo HDInsight C# Storm Power BI](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi). toodownload, ya sea bifurcar/clone mediante [git](http://git-scm.com/), o usar hello **descargar** toodownload vínculo .zip archivo Hola.

## <a name="create-a-database"></a>Crear una base de datos

1. toocreate una base de datos, siga los pasos de Hola Hola [tutorial de base de datos SQL](../sql-database/sql-database-get-started.md) documento.

2. Conectar toohello base de datos Hola siguiente pasos de hello [conectar tooa base de datos SQL con Visual Studio](../sql-database/sql-database-connect-query.md) documento.

3. En el Explorador de objetos, haga clic en la base de datos de Hola y seleccione **nueva consulta**. Pegar contenido Hola de hello **IISLogsTable.sql** archivo incluido en hello descargaste el proyecto en la ventana de consulta de hello y, a continuación, utilice Ctrl + Mayús + E tooexecute Hola consulta. Debería recibir un mensaje que Hola comandos que se completó correctamente.

## <a name="configure-hello-sample"></a>Configurar el ejemplo hello

1. De hello [portal de Azure](https://portal.azure.com), seleccione la base de datos SQL. De hello **Essentials** sección de hoja de base de datos SQL hello, seleccione **mostrar cadenas de conexión de base de datos**. De la lista de Hola que aparece, copie hello **ADO.NET (autenticación de SQL)** información.

2. Ejemplo de Hola abierta en Visual Studio. De **el Explorador de soluciones**, abra hello **App.config** de archivos y, a continuación, busque Hola siguiente entrada:

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    Reemplace hello **TOBEFILLED ##** valor con la cadena de conexión de base de datos de Hola se copió en el paso anterior de Hola. Reemplace **{su\_username}** y **{su\_contraseña}** con hello username y password para base de datos de Hola.

3. Guarde y cierre los archivos de saludo.

## <a name="deploy-hello-sample"></a>Implementar el ejemplo hello

1. De **el Explorador de soluciones**, contextual hello **StormToSQL** de proyecto y seleccione **enviar tooStorm en HDInsight**. Clúster de HDInsight seleccione Hola de hello **clúster de Storm** cuadro de diálogo de lista desplegable.

   > [!NOTE]
   > Puede tardar unos segundos hello **clúster de Storm** toopopulate de lista desplegable con nombres de servidor.
   >
   > Si se le solicite, escriba las credenciales de inicio de sesión de hello para la suscripción de Azure. Si tiene más de una suscripción, inicie sesión en toohello uno que contiene el aluvión en clúster de HDInsight.

2. Cuando se ha enviado la topología de hello, Hola __Visor de la topología__ aparece. tooview esta topología, entrada de SqlAzureWriterTopology Hola seleccione de la lista de Hola.

    ![topologías de Hello, con la topología de hello seleccionado](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    Puede usar esta información de toosee de vista en la topología de hello, o haga doble clic en un componente de tooa específico de entrada (por ejemplo, hello SqlAzureBolt) toosee información de topología de Hola.

3. Después de hello topología se ejecutó durante unos minutos, ventana de consulta SQL toohello devuelto usar base de datos de toocreate Hola. Reemplace las instrucciones existentes de hello con hello después de consulta:

        select * from iislogs;

    Utilice Ctrl + Mayús + E tooexecute Hola de consultas y se debe recibir resultados toohello similar datos siguientes:

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    Estos datos se ha escrito de topología de Storm Hola.

## <a name="create-a-report"></a>Creación de un informe

1. Conectar toohello [conector de base de datos de SQL Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) para Power BI. 

2. Dentro de **Bases de datos**, seleccione **Obtener**.

3. Seleccione **Azure SQL Database** y luego **Conectar**.

    > [!NOTE]
    > Se le pedirá toodownload Hola Power BI Desktop toocontinue. Si es así, utilice Hola siguiendo los pasos tooconnect:
    >
    > 1. Abra Power BI Desktop y seleccione __Obtener datos__.
    > 2  Seleccione __Azure__ y luego __Azure SQL Database__.

4. Escriba Hola información tooconnect tooyour base de datos de SQL Azure. Puede encontrar esta información visitando hello [portal de Azure](https://portal.azure.com) y seleccione la base de datos SQL.

   > [!NOTE]
   > También puede establecer intervalo de actualización de Hola y filtros personalizados mediante **habilitar opciones avanzadas** de hello el diálogo de conexión.

5. Una vez conectado, verá un nuevo conjunto de datos con hello que mismo nombre como base de datos de Hola que se ha conectado. Seleccione toobegin de conjunto de datos de hello diseñar un informe.

6. De **campos**, expanda hello **IISLOGS** entrada. toocreate proviene de un informe que enumera Hola URI, active la casilla de verificación de Hola para **URISTEM**.

    ![Creación de un informe](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. A continuación, arrastre **método** toohello informes. Hola de Hello informe actualizaciones toolist proviene y método HTTP correspondiente de hello usa para hello solicitud HTTP.

    ![agregar datos sobre métodos Hola](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. De hello **visualizaciones** columna, seleccione hello **campos** icono y, a continuación, seleccione Hola flecha abajo junto demasiado**método** en hello **valores**sección. Seleccione toodisplay se accedió a un recuento de cuántas veces un URI, **recuento**.

    ![Cambiar el número de tooa de métodos](./media/hdinsight-storm-power-bi-topology/count.png)

9. A continuación, seleccione hello **gráfico de columnas apiladas** toochange cómo se muestra información de Hola.

    ![Variación tooa series apiladas](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. informe de toosave hello, seleccione **guardar** y escriba un nombre para el informe de Hola.

## <a name="stop-hello-topology"></a>Detener la topología de Hola

topología de Hello continúa toorun hasta que lo detenga o eliminar Hola Storm en clúster de HDInsight. toostop Hola topología, lleve a cabo Hola pasos:

1. En Visual Studio, devolver Visor de la topología de toohello y seleccione la topología de Hola.

2. Seleccione hello **Kill** topología de botón toostop Hola.

    ![Kill botón en la topología de hello resumen](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Eliminación del clúster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Pasos siguientes

En este documento, aprendió cómo toosend datos desde un tooSQL de topología de Storm base de datos, a continuación, visualizar los datos de hello con Power BI. Para obtener información acerca de cómo toowork con otras tecnologías de Azure con Storm en HDInsight, vea Hola siguiente documento:

* [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md)
