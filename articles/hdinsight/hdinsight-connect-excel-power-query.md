---
title: aaaConnect tooHadoop de Excel con Power Query - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tootake ventaja de los componentes de business intelligence y se utiliza Power Query para Excel tooaccess datos almacenados en Hadoop en HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 01ad2f90-7520-44d9-8c16-4d936faaff9b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jgao
ms.openlocfilehash: 1213849f1bc04e0ed206750b80766ff2268664b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-by-using-power-query"></a>Conectar Excel tooHadoop mediante Power Query
Una característica clave de la solución de grandes cantidades de datos de Microsoft hello es la integración de Hola de componentes de Microsoft business intelligence (BI) con los clústeres de Hadoop en HDInsight de Azure. Un ejemplo principal es Hola capacidad tooconnect Excel toohello cuenta de almacenamiento de Azure que contiene datos de hello asociadas al clúster de Hadoop mediante el uso de Microsoft Power Query de hello para el complemento de Excel. Este artículo le guiará a través de cómo administran tooset seguridad y el uso de datos de Power Query tooquery asociados a un clúster de Hadoop con HDInsight.

### <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este artículo, debe tener Hola siguientes elementos:

* **Un clúster de HDInsight**. tooconfigure uno, vea [empezar a trabajar con HDInsight de Azure][hdinsight-get-started].
* **Una estación de trabajo** que ejecute Windows 7, Windows Server 2008 R2 o un sistema operativo posterior.
* **Office 2016, Office Profesional Plus 2013, Office 365 ProPlus, Excel 2013 Standalone u Office Professional Plus 2010**.

## <a name="install-power-query"></a>Instalación de Power Query
Power Query puede importar datos ofrecidos o generados por un trabajo de Hadoop ejecutado en un clúster de HDInsight.

En Excel 2016, Power Query se ha integrado en la cinta de opciones de datos de hello en hello Get & sección de transformación. Para versiones anteriores de Excel, descargue Microsoft Power Query para Excel de hello [Microsoft Download Center] [ powerquery-download] e instalarlo.

## <a name="import-hdinsight-data-into-excel"></a>Importación de datos de HDInsight a Excel
Hola complemento Power Query para Excel resulta fácil tooimport datos desde el clúster de HDInsight en Excel, donde pueden ser usado tooinspect, analizar y presentar datos Hola herramientas de BI como PowerPivot y asignación de energía.

**tooimport datos de un clúster de HDInsight**

1. Abra Excel.
2. Cree un libro vacío.
3. Lleve a cabo Hola siguiendo los pasos que se basa en la versión de Excel de hello:

    - Excel 2016

        - Haga clic en hello **datos** menú, haga clic en **obtener datos** de hello **obtener y transformar datos** la cinta de opciones, haga clic en **de Azure**y, a continuación, haga clic en  **Desde Azure HDInsight(HDFS)**.

        ![HDI.PowerQuery.SelectHdiSource](./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.excel2016.png)

    - Excel 2013/2010

        - Haga clic en hello **Power Query** menú, haga clic en **de Azure**y, a continuación, haga clic en **desde Microsoft Azure HDInsight**.
   
        ![HDI.PowerQuery.SelectHdiSource][image-hdi-powerquery-hdi-source]
       
        **Nota:** si no ve hello **Power Query** menú, ir demasiado**archivo** > **opciones** > **Add-Ins**y seleccione **complementos COM** de hello desplegable **administrar** cuadro final Hola de página Hola. Seleccione hello **vaya...**  botón y compruebe que ese cuadro Hola de hello Power Query para el complemento de Excel se ha comprobado.
       
        **Nota:** Power Query también le permite tooimport datos desde HDFS haciendo clic en **desde otros orígenes**.
4. Para **nombre-cuenta**, escriba Hola nombre de cuenta de almacenamiento de blobs de Azure Hola asociada al clúster y, a continuación, haga clic en **Aceptar**. Esta cuenta puede ser hello [cuenta de almacenamiento predeterminada](hdinsight-administer-use-management-portal.md#find-the-default-storage-account) o una cuenta de almacenamiento vinculado.  formato de Hello es *https://&lt;StorageAccountName >.blob.core.windows.net/*.
5. Para **clave de cuenta**, escriba la clave de Hola de hello cuenta de almacenamiento Blob y, a continuación, haga clic en **guardar**. (Debe tooenter Hola Hola de cuenta información solo primera vez que accede a este almacén.)
6. Hola **navegador** panel Hola deja de hello Editor de consultas, haga doble clic en el nombre del contenedor de almacenamiento de blobs de Hola. De forma predeterminada, el nombre del contenedor de Hola Hola mismo nombre como nombre del clúster Hola.
7. Busque **HiveSampleData.txt** en hello **nombre** columna (ruta de acceso de carpeta de hello es **... / hive/almacenamiento/hivesampletable/**) y, a continuación, haga clic en **binario** izquierda Hola de HiveSampleData.txt. HiveSampleData.txt incluye todos los clúster Hola. Opcionalmente, puede utilizar su propio archivo.
   
    ![HDI.PowerQuery.ImportData][image-hdi-powerquery-importdata]
8. Si lo desea, puede cambiar los nombres de columna de Hola. Cuando haya terminado, haga clic en **Aplicar y cerrar**.  datos de Hello ha sido cargado tooyour libro:
   
    ![HDI.PowerQuery.ImportedTable][image-hdi-powerquery-imported-table]

## <a name="next-steps"></a>Pasos siguientes
En este artículo, se habrá aprendido cómo toouse datos de Power Query tooretrieve de HDInsight en Excel. Del mismo modo, puede recuperar datos de HDInsight en Base de datos SQL de Azure. También es datos de posibles tooupload en HDInsight. toolearn más información, vea Hola siguientes artículos:

* [Conectar Excel tooHDInsight con hello Microsoft Hive ODBC Driver][hdinsight-ODBC]
* [Cargar datos tooHDInsight][hdinsight-upload-data]

[hdinsight-ODBC]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[image-hdi-powerquery-hdi-source]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.png
[image-hdi-powerquery-importdata]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importdata.png
[image-hdi-powerquery-imported-table]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importedtable.PNG

[powerquery-download]: http://go.microsoft.com/fwlink/?LinkID=286689
