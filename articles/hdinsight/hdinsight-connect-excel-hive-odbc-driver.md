---
title: aaaConnect tooHadoop de Excel con hello Hive ODBC Driver - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooset seguridad y el uso Hola controlador ODBC de Microsoft Hive tooquery para datos de Excel en los clústeres de HDInsight de Microsoft Excel."
keywords: Excel en Hadoop, Excel en Hive, ODBC de Hive
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: f01f89e7d4203c739d56079dc589fc11f4aa2174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a>Conectar Excel tooHadoop en HDInsight de Azure con hello Hive controlador ODBC de Microsoft

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Solución de grandes cantidades de datos de Microsoft integra los componentes de Microsoft Business Intelligence (BI) con los clústeres de Apache Hadoop que se han implementado por hello HDInsight de Azure. Un ejemplo de esta integración es el almacenamiento de datos de hello capacidad tooconnect Excel toohello subárbol de un clúster de Hadoop en HDInsight con hello controlador Microsoft Hive Open Database Connectivity (ODBC).

También es posible tooconnect datos de hello asociadas a un clúster de HDInsight y otros orígenes de datos, incluidas otra (no-HDInsight) Hadoop clústeres, de Excel utilizando Hola complemento Microsoft Power Query para Excel. Para obtener información sobre cómo instalar y usar Power Query, consulte [tooHDInsight conectar Excel con Power Query][hdinsight-power-query].

> [!NOTE]
> Mientras Hola los pasos de este artículo puede utilizarse con cualquier una Linux o clúster de HDInsight basados en Windows, Windows se requiere para estación de trabajo de cliente de Hola.
> 
> 

**Requisitos previos**:

Antes de comenzar este artículo, debe tener Hola siguientes elementos:

* **Un clúster de HDInsight**. toocreate uno, vea [empezar a trabajar con HDInsight de Azure][hdinsight-get-started].
* **Un equipo** con Office Professional Plus 2013, Office 365 Pro Plus, Excel 2013 Standalone u Office Professional Plus 2010.

## <a name="install-microsoft-hive-odbc-driver"></a>Instalación de Microsoft Hive ODBC Driver
Descargue e instale Microsoft Hive ODBC Driver de hello [centro de descarga de][hive-odbc-driver-download].

Este controlador se puede instalar en las versiones de 32 bits o 64 bits de Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 y Windows Server 2012. controlador de Hello permite tooAzure conexión HDInsight (versión 1.6 y versiones posterior) y el emulador de HDInsight de Azure (v.1.0.0.0 y versiones posteriores). Deberá instalar versión de Hola que coincida con la versión de Hola de aplicación Hola que utilice el controlador ODBC de Hola. Para este tutorial, se usa el controlador de Hola de Office Excel.

## <a name="create-hive-odbc-data-source"></a>Creación de un origen de datos de Hive ODBC
Hello pasos siguientes muestran cómo toocreate un origen de datos ODBC de Hive.

1. Desde Windows 8 o Windows 10, presione la pantalla de inicio de hello Windows tooopen clave hello y, a continuación, escriba **orígenes de datos**.
2. Haga clic en **Configurar orígenes de datos ODBC (32 bits)** o **Configurar orígenes de datos ODBC (64 bits)**, en función de la versión de Office de que se trate. Si usa Windows 7, elija **Orígenes de datos ODBC (32 bits)** u **Orígenes de datos ODBC (64 bits)** en **Herramientas administrativas**. Verá hello **Administrador de orígenes de datos ODBC** cuadro de diálogo.
   
    ![Administrador de orígenes de datos ODBC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configuración de un DSN mediante el Administrador de orígenes de datos ODBC")

3. Desde el servidor DNS del usuario, haga clic en **agregar** tooopen hello **Create New Data Source** asistente.
4. Elija **Microsoft Hive ODBC Driver** y, después, haga clic en **Finalizar**. Verá hello **configuración de DNS de controlador de ODBC de Hive de Microsoft** cuadro de diálogo.
5. Escriba o seleccione Hola siguientes valores:
   
   | Propiedad | Description |
   | --- | --- |
   |  Data Source Name |Proporcionar a un origen de datos de nombre tooyour |
   |  Host |Escriba &lt;NombreClústerHDInsight>.azurehdinsight.net. Por ejemplo, myHDICluster.azurehdinsight.net |
   |  Port |Use <strong>443</strong>. (Este puerto se ha cambiado de too443 563). |
   |  Base de datos |Use el <strong>valor predeterminado</strong> |
   |  Mechanism |Seleccione <strong>Azure HDInsight Service</strong> |
   |  User Name |Escriba el nombre de usuario HTTP del clúster de HDInsight. el nombre de usuario de Hello predeterminada es <strong>administración</strong>. |
   |  Password |Escriba la contraseña del usuario del clúster de HDInsight. |
   
    </table>
   
    Hay algunos toobe parámetros importantes en cuenta al hacer clic en **opciones avanzadas**:
   
   | Parámetro | Description |
   | --- | --- |
   |  Use Native Query |Cuando se selecciona, el controlador ODBC de hello no intentará tooconvert TSQL en HiveQL. Solo debe usarla si está totalmente seguro de que va a enviar instrucciones de HiveQL puras. Cuando se conecte tooSQL servidor o base de datos de SQL Azure, debe dejar desactivada. |
   |  Rows fetched per block |Al capturar un gran número de registros, ajustar este parámetro puede ser necesario tooensure óptimo rendimiento. |
   |  Default string column length, Binary column length, Decimal column scale |longitudes de tipo de datos de Hola y precisiones pueden afectar a cómo se devuelven los datos. Hacen que toobe información incorrecta devuelve debido tooloss de precisión o truncamiento. |

    ![Opciones avanzadas](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Opciones de configuración avanzada de DSN")

1. Haga clic en **prueba** origen de datos de tootest Hola. Cuando el origen de datos de hello está configurado correctamente, muestra *pruebas completadas correctamente!*.
2. Haga clic en **Aceptar** tooclose Hola Probar cuadro de diálogo. nuevo origen de datos Hola se indicarán en hello **Administrador de orígenes de datos ODBC**.
3. Haga clic en **Aceptar** Asistente de hello tooexit.

## <a name="import-data-into-excel-from-hdinsight"></a>Importación de datos en Excel desde HDInsight
Hello pasos siguientes describen Hola forma tooimport que los datos de una tabla de Hive en un libro de Excel con el origen de datos ODBC de Hola que creó en la sección anterior de Hola.

1. Abra un libro de Excel nuevo o existente.
2. De hello **datos** , haga clic en **obtener datos**, haga clic en **desde otros orígenes**y, a continuación, haga clic en **de ODBC** toolaunch hello ** Asistente para la conexión de datos**.
   
    ![Apertura del Asistente para la conexión de datos](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Apertura del Asistente para la conexión de datos")
4. Nombre que creó en la última sección de Hola de origen de datos de hello seleccione y, a continuación, haga clic en **Aceptar**.
5. Escriba el nombre de usuario de Hadoop (nombre predeterminado de hello es admin) Hola contraseña y, a continuación, haga clic en **conectar**.
6. En el explorador, expanda **HIVE**, expanda **predeterminado**, haga clic en **hivesampletable** y, finalmente, haga clic en **Cargar**. Tarda unos segundos antes de que los datos lleguen tooExcel importado.

    ![Navegador de ODBC de Hive de HDInsight](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Abrir Asistente para la conexión de datos")


## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido cómo toouse Hola datos de tooretrieve del controlador ODBC de Microsoft de Hive de hello HDInsight Service en Excel. De forma similar, puede recuperar datos de hello HDInsight Service en la base de datos SQL. También es datos tooupload posibles en un HDInsight Service. toolearn más información, vea:

* [Análisis de la información de retraso de vuelos con HDInsight][hdinsight-analyze-flight-data]
* [Cargar datos tooHDInsight][hdinsight-upload-data]
* [Uso de Sqoop con HDInsight][hdinsight-use-sqoop]

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


