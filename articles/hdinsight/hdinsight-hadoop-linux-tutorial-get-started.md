---
title: aaaGet a trabajar con Hadoop y Hive en HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate HDInsight clústeres y consultar datos con Hive."
keywords: "introducción a hadoop, hadoop linux, inicio rápido de hadoop, introducción a hive, inicio rápido en hive"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6a12ed4c-9d49-4990-abf5-0a79fdfca459
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: 3d96d78121200ebda3626dd2c3885e3ddacd546d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hadoop-tutorial-get-started-using-hadoop-in-hdinsight"></a>Tutorial de Hadoop: introducción al uso de Hadoop en HDInsight

Obtenga información acerca de cómo toocreate [Hadoop](http://hadoop.apache.org/) clústeres de HDInsight, y cómo trabajos toorun Hive en HDInsight. [Apache Hive](https://hive.apache.org/) es componente más popular de hello en el ecosistema de Hadoop de Hola. Actualmente HDInsight tiene [siete tipos diferentes de clúster](hdinsight-hadoop-introduction.md#overview). Cada uno de estos tipos de clúster es compatible con un conjunto de componentes diferente. Todos los tipos de clúster son compatibles con Hive. ¿Para obtener una lista de componentes compatibles en HDInsight, vea [cuáles son las novedades en las versiones de clúster de Hadoop Hola proporcionadas por HDInsight?](hdinsight-component-versioning.md)  

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>Requisitos previos
Antes de empezar este tutorial, debe contar con lo siguiente:

* **Suscripción de Azure**: toocreate una cuenta de evaluación gratuita de un mes, examinar demasiado[azure.microsoft.com/free](https://azure.microsoft.com/free).

## <a name="create-cluster"></a>Crear clúster

La mayoría de los trabajos de Hadoop son trabajos por lotes. Crear un clúster, ejecutar algunos de estos trabajos y, a continuación, Eliminar clúster Hola. En esta sección, se crea un clúster de Hadoop en HDInsight mediante una [plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). No es necesario tener experiencia en el uso de la plantilla de Resource Manager para seguir este tutorial. Para otros métodos de creación del clúster y la comprensión de propiedades de hello usados en este tutorial, vea [HDInsight crear clústeres](hdinsight-hadoop-provision-linux-clusters.md). Utilice selector de hello en la parte superior de Hola de hello página toochoose las opciones de creación de clúster.

plantilla de administrador de recursos de Hello usado en este tutorial se encuentra en [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/). 

1. Haga clic en hello siguientes toosign de imagen en tooAzure y plantilla de administrador de recursos abiertos Hola Hola portal de Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-ssh-password%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Escriba o seleccione Hola siguientes valores:
   
    ![HDInsight Linux cómo empezar plantilla del Administrador de recursos en el portal](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "Hadoop implementar clústeres en HDInsigut utilizando Hola portal de Azure y una plantilla de administrador del grupo de recursos").
   
    * **Suscripción**: seleccione su suscripción de Azure.
    * **Grupo de recursos**: cree un grupo de recursos o seleccione uno existente.  Un grupo de recursos es un contenedor de componentes de Azure.  En este caso, grupo de recursos de hello contiene clúster de HDInsight de Hola y cuenta de almacenamiento de Azure de hello dependiente. 
    * **Ubicación**: seleccione una ubicación de Azure donde desee toocreate el clúster.  Elija un tooyou más cerca de la ubicación para mejorar el rendimiento. 
    * **Tipo de clúster**: seleccione **Hadoop** para este tutorial.
    * **Nombre del clúster**: escriba un nombre para el clúster de Hadoop de Hola.
    * **Nombre de inicio de sesión y la contraseña del clúster**: nombre de inicio de sesión predeterminado de hello es **administración**.
    * **SSH username y password**: nombre de usuario de hello predeterminada es **sshuser**.  Puede cambiarlo. 
     
    Algunas propiedades han sido codificado de forma rígida en la plantilla de Hola.  Puede configurar estos valores de plantilla de Hola.

    * **Ubicación**: Hola ubicación del clúster de Hola y recurso compartido de cuenta de almacenamiento dependientes Hola Hola misma ubicación que el grupo de recursos de Hola.
    * **Versión del clúster**: 3.5
    * **Tipo de sistema operativo**: Linux
    * **Número de nodos de trabajo**: 2

     Cada clúster depende de una [cuenta de Azure Storage](hdinsight-hadoop-use-blob-storage.md) o de una [cuenta de Azure Data Lake](hdinsight-hadoop-use-data-lake-store.md). Se conoce como cuenta de almacenamiento predeterminada de Hola. Clúster de HDInsight y su cuenta de almacenamiento predeterminada deben estar colocados en hello misma región de Azure. Eliminación de clústeres no eliminar la cuenta de almacenamiento de Hola. 
     
     Para más información acerca de estas propiedades, consulte [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

3. Seleccione **muestro mi conformidad toohello términos y condiciones indicadas anteriormente** y **Pin toodashboard**y, a continuación, haga clic en **compra**. Verá un nuevo icono titulado **implementación de plantilla de implementación de** en el panel del portal Hola. Se tarda aproximadamente toocreate de aproximadamente 20 minutos de un clúster. Una vez creado el clúster de hello, título de Hola de mosaico de hello es modificada toohello nombre de grupo de recursos especificado. Y portal de hello abre automáticamente el grupo de recursos de hello en una nueva hoja. Puede ver clúster Hola y almacenamiento predeterminado de hello enumerados.
   
    ![Introducción a HDInsight Linux: grupo de recursos](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-resource-group.png "Grupo de recursos de clúster de Azure HDInsight").

4. Haga clic en clúster Hola clúster nombre tooopen hello en una nueva hoja.

   ![Introducción a HDInsight Linux: configuración del clúster](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-cluster-settings.png "Propiedades de clúster de HDInsight")


## <a name="run-hive-queries"></a>Ejecución de consultas de Hive
[Apache Hive](hdinsight-use-hive.md) es componente más popular de hello usado en HDInsight. Hay muchas maneras de toorun trabajos de Hive en HDInsight. En este tutorial, utilice hello Ambari Hive vista desde el portal de Hola. Para conocer otros métodos de enviar trabajos de Hive, consulte [Usar Hive y HiveQL con Hadoop en HDInsight para analizar un archivo log4j de Apache de muestra](hdinsight-use-hive.md).

1. En la captura de pantalla anterior hello, haga clic en **panel clúster**y, a continuación, haga clic en **panel de clúster de HDInsight**.  También puede examinar demasiado **https://&lt;ClusterName >. azurehdinsight.net**, donde &lt;nombreDeClúster > es clúster Hola que creó en la anterior sección tooopen Ambari de Hola.
2. Escriba el nombre de usuario de hello Hadoop y la contraseña que especificó en la sección anterior de Hola. el nombre de usuario de Hello predeterminada es **administración**.
3. Abra **vista Hive** tal y como se muestra en la siguiente captura de pantalla de hello:
   
    ![Selección de vistas de Ambari](./media/hdinsight-hadoop-linux-tutorial-get-started/selecthiveview.png "Menú de vistas de Hive de HDInsight").
4. Hola **Editor de consultas** sección de página de hello, Hola pegar siguiendo las instrucciones de HiveQL en la hoja de cálculo de hello:
   
        SHOW TABLES;
   
   > [!NOTE]
   > Hive requiere un punto y coma.       
   > 
   > 
5. Haga clic en **Ejecutar**. A **resultados del proceso de consulta** sección debe aparecer debajo de hello Editor de consultas y mostrar información sobre el trabajo de Hola. 
   
    Cuando haya finalizado la consulta de hello, Hola **resultados del proceso de consulta** sección muestra los resultados de Hola de operación de Hola. Verá una tabla denominada **hivesampletable**. Esta tabla de Hive de ejemplo incluye todos los clústeres de HDInsight de Hola.
   
    ![Vistas de Hive de HDInsight](./media/hdinsight-hadoop-linux-tutorial-get-started/hiveview.png "Editor de consultas de vistas de Hive de HDInsight").
6. Repita los pasos 4 y Hola de toorun paso 5 después de consulta:
   
        SELECT * FROM hivesampletable;
   
   > [!TIP]
   > Hola Nota **guardar resultados** desplegable Hola superior izquierda de hello **resultados del proceso de consulta** sección; puede usar este resultados de hello tooeither descarga o guardar tooHDInsight almacenamiento como un archivo CSV.
   > 
   > 
7. Haga clic en **historial** tooget una lista de trabajos de Hola.

Después de haber completado un trabajo de Hive, puede [exportar base de datos de SQL Server o una base de datos SQL de hello resultados tooAzure](hdinsight-use-sqoop-mac-linux.md), también puede [visualizar los resultados de hello mediante Excel](hdinsight-connect-excel-power-query.md). Para obtener más información acerca del uso de Hive en HDInsight, vea [HiveQL con Hadoop en HDInsight tooanalyze un archivo de ejemplo Apache log4j y uso de Hive](hdinsight-use-hive.md).

## <a name="clean-up-hello-tutorial"></a>Limpiar el tutorial Hola
Después de completar el tutorial de hello, puede que desee clúster de hello toodelete. Con HDInsight, los datos se almacenan en Almacenamiento de Azure, por lo que puede eliminar un clúster de forma segura cuando no está en uso. También se le cargará por un clúster de HDInsight aunque no esté en uso. Puesto que los cargos de Hola de clúster de hello son muchas veces más que los cargos de hello para el almacenamiento, conviene económico toodelete clústeres cuando no están en uso. 

> [!NOTE]
> Usar [Data Factory de Azure](hdinsight-hadoop-create-linux-clusters-adf.md), puede crear clústeres de HDInsight a petición y configurar un TimeToLive configuración demasiado eliminar clústeres Hola automáticamente. 
> 
> 

**toodelete Hola Hola o clúster cuenta de almacenamiento predeterminada**

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Desde el panel del portal hello, haga clic en el icono de hello con nombre de grupo de recursos de Hola que utilizó cuando creó el clúster de Hola.
3. Haga clic en **eliminar** en Hola hoja toodelete Hola recursos grupo de recursos, que contiene el clúster de Hola y cuenta de almacenamiento predeterminada de hello; o haga clic en el nombre del clúster hello en hello **recursos** icono y, a continuación, haga clic en **Eliminar** en la hoja de clúster de Hola. Tenga en cuenta al eliminar el grupo de recursos de hello elimina la cuenta de almacenamiento de Hola. Si desea que la cuenta de almacenamiento de tookeep hello, elija clúster toodelete Hola.

## <a name="troubleshoot"></a>Solución de problemas

Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo toocreate una HDInsight basados en Linux mediante una plantilla de administrador de recursos del clúster y cómo tooperform consultas de Hive básicas.

toolearn más información acerca de análisis de datos con HDInsight, vea Hola siguientes artículos:

* toolearn más sobre el uso de Hive con HDInsight, incluido cómo las consultas tooperform Hive desde Visual Studio, vea [uso de Hive con HDInsight][hdinsight-use-hive].
* toolearn sobre Pig, datos tootransform de usar un idioma, vea [uso de Pig con HDInsight][hdinsight-use-pig].
* toolearn sobre MapReduce, una manera toowrite los programas que procesan datos en Hadoop, vea [MapReduce de uso con HDInsight][hdinsight-use-mapreduce].
* toolearn sobre el uso de herramientas de HDInsight de Hola para los datos de Visual Studio tooanalyze en HDInsight, vea [Introducción al uso de Hadoop de Visual Studio tools para HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).

Si está listo toostart trabajar con sus propios datos y necesita tooknow Obtenga más información sobre cómo HDInsight almacena los datos o datos tooget en HDInsight, vea la siguiente de hello:

* Para más información sobre cómo HDInsight usa Azure Storage, consulte [Uso de Azure Storage con HDInsight](hdinsight-hadoop-use-blob-storage.md).
* Para obtener información acerca de cómo tooupload tooHDInsight de datos, vea [cargar datos tooHDInsight][hdinsight-upload-data].

Si desea más información acerca de crear o administrar un clúster de HDInsight toolearn, vea Hola siguiente:

* toolearn acerca de cómo administrar el clúster de HDInsight basados en Linux, consulte [HDInsight administrar clústeres con Ambari](hdinsight-hadoop-manage-ambari.md).
* toolearn más información acerca de las opciones de Hola que puede seleccionar al crear un clúster de HDInsight, vea [HDInsight crear en Linux con opciones personalizadas](hdinsight-hadoop-provision-linux-clusters.md).
* Si está familiarizado con Linux y Hadoop, pero desea tooknow detalles acerca de Hadoop en HDInsight de hello, consulte [trabajar con HDInsight en Linux](hdinsight-hadoop-linux-information.md). Este artículo proporciona información como:
  
  * Direcciones URL para los servicios hospedados en clúster de hello, por ejemplo, Ambari y WebHCat
  * ubicación de Hola de ejemplos en el sistema de archivos local de Hola y archivos de Hadoop
  * uso de Hola de Azure Storage (WASB) en lugar de HDFS como almacén de datos predeterminado de Hola

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


