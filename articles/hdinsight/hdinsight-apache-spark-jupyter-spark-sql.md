---
title: "clúster de aaaCreate un Apache Spark en HDInsight de Azure | Documentos de Microsoft"
description: "Inicio rápido de HDInsight Spark en forma de clúster toocreate un Apache Spark en HDInsight."
keywords: "inicio rápido para spark,spark interactivo,consulta interactiva,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a>Creación de un clúster de Apache Spark en Azure HDInsight

En este artículo, aprenderá cómo agrupar toocreate un Apache Spark en HDInsight de Azure. Para obtener información sobre Spark en HDInsight, consulte [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md).

   ![Diagrama de inicio rápido que describe los pasos toocreate un clúster de Apache Spark en HDInsight de Azure](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "inicio rápido de Spark con Apache Spark en HDInsight. Pasos que ilustran cómo crear un clúster y ejecutar una consulta Spark interactiva")

## <a name="prerequisites"></a>Requisitos previos

* **Una suscripción de Azure**. Antes de comenzar este tutorial, debe tener una suscripción a Azure. Consulte la página [Cree su cuenta gratuita de Azure hoy mismo](https://azure.microsoft.com/free).

## <a name="create-hdinsight-spark-cluster"></a>Creación de un clúster de HDInsight Spark

En esta sección, creará un clúster de HDInsight Spark mediante una [plantilla de Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/). Para conocer otros métodos de creación de clústeres, consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

1. Haga clic en hello después de la plantilla de imagen tooopen Hola Hola portal de Azure.         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Escriba Hola siguientes valores:

    ![Creación de un clúster de HDInsight Spark mediante una plantilla de Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Creación de un clúster de HDInsight Spark mediante una plantilla de Azure Resource Manager")

    * **Suscripción**: seleccione su suscripción de Azure para este clúster.
    * **Grupo de recursos**: cree un grupo de recursos o seleccione uno existente. Grupo de recursos es toomanage usa recursos de Azure para sus proyectos.
    * **Ubicación**: seleccione una ubicación para el grupo de recursos de Hola. plantilla de Hello usa esta ubicación para crear clúster Hola así en cuanto al almacenamiento de clúster predeterminado de Hola.
    * **ClusterName**: escriba un nombre para el clúster de HDInsight de Hola que desea toocreate.
    * **Versión de Spark**: seleccione **2.0** como versión de Hola que desea tooinstall en clúster de Hola.
    * **Nombre de inicio de sesión y la contraseña del clúster**: nombre de inicio de sesión predeterminado de hello es administrador.
    * **Nombre de usuario y contraseña de SSH**.

   Anote estos valores.  Se necesita más adelante en el tutorial Hola.

3. Seleccione **muestro mi conformidad toohello términos y condiciones indicadas anteriormente**, seleccione **Pin toodashboard**y, a continuación, haga clic en **compra**. Puede ver un icono nuevo llamado Envío de implementación para la implementación de plantilla. Toma clúster de hello toocreate alrededor de 20 minutos.

Si surge un problema con la creación de clústeres de HDInsight, podría deberse a que no tienen Hola permisos adecuados toodo por lo que. Consulte [Requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters) para más información.

> [!NOTE]
> Este artículo crea un clúster de Spark que use [almacenamiento de Blobs de almacenamiento de Azure como Hola clúster](hdinsight-hadoop-use-blob-storage.md). También puede crear un clúster de Spark que use [almacén de Azure Data Lake](hdinsight-hadoop-use-data-lake-store.md) como almacenamiento predeterminado de Hola. Consulte [Creación de un clúster de HDInsight con el Almacén de Data Lake mediante el Portal de Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).
>
>

## <a name="run-a-hive-query-using-spark-sql"></a>Ejecución de una consulta de Hive con Spark SQL

Cuando usas configurado para el clúster de HDInsight Spark Jupyter notebook, obtendrá un valor preestablecido `sqlContext` que puede usar consultas de Hive toorun usar Spark SQL. En esta sección, aprenderá cómo toostart Jupyter notebook y, a continuación, ejecutar una consulta de Hive básica.

1. Abra hello [portal de Azure](https://portal.azure.com/).

2. Si ha elegido el panel de toohello de toopin Hola clúster, haga clic en icono de clúster de Hola desde la hoja de clúster de hello panel toolaunch Hola.

    Si no ancla panel Hola clúster toohello, desde el panel izquierdo de hello, haga clic en **clústeres de HDInsight**y, a continuación, haga clic en clúster de Hola que creó.

3. En **Quick links** (Vínculos rápidos), haga clic en **Cluster dashboards** (Paneles de clúster) y después en **Jupyter Notebook**. Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.

   ![Abrir Jupyter notebook toorun interactivo Spark SQL consulta](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "consultas Jupyter Abrir Bloc de notas toorun interactivo Spark SQL")

   > [!NOTE]
   > También puede tener acceso a Jupyter notebook de hello para el clúster por abrir Hola siguiente dirección URL en el explorador. Reemplace **CLUSTERNAME** con nombre hello del clúster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Cree un cuaderno. Haga clic en **Nuevo** y, luego, en **PySpark**.

   ![Crear una consulta de Spark SQL interactiva de Jupyter notebook toorun](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "crear una consulta Jupyter notebook toorun interactiva Spark SQL")

   Un nuevo bloc de notas se crea y se abre con el nombre de hello Untitled(Untitled.pynb).

4. Haga clic en nombre de Bloc de notas de hello en la parte superior de Hola y escriba un nombre descriptivo si desea.

    ![Proporcione un nombre para hello Jupter Bloc de notas toorun Spark consulta interactiva de](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "proporcione un nombre para hello Jupter Bloc de notas toorun Spark consulta interactiva desde")

5.  Siguiente de Hola de pegar código en una celda vacía y, a continuación, presione **MAYÚS + ENTRAR** código de hello toorun. En el siguiente código de hello `%%sql` (mágico de sql llamado hello) indica preestablecido Hola de Jupyter notebook toouse `sqlContext` consulta de Hive toorun Hola. consulta de Hello recupera Hola 10 primeras filas de una tabla de Hive (**hivesampletable**) que está disponible de forma predeterminada en todos los clústeres de HDInsight.

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    ![Consulta de Hive en HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Consulta de Hive en HDInsight Spark")

    Para obtener más información sobre hello `%%sql` hello y magia preestablecido contextos, consulte [Jupyter núcleos disponibles para un clúster de HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

    > [!NOTE]
    > Cada vez que ejecute una consulta en Jupyter, el título de ventana de explorador web muestra un **(estado ocupado)** estado junto con el título de hello Bloc de notas. También verá un toohello siguiente círculo sólido **PySpark** texto en la esquina superior derecha de Hola. Una vez completado el trabajo de hello, cambia el círculo hueco tooa.
    >
    >
    
6. pantalla de bienvenida debe actualizar el resultado de la consulta de tooshow Hola.

    ![Consulta de Hive en HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Consulta de Hive en HDInsight Spark")

7. Apagar los recursos de clúster de hello Bloc de notas toorelease Hola después de que haya terminado de ejecutar la aplicación hello. toodo es así, de hello **archivo** menú en el Bloc de notas de hello, haga clic en **cerrar y detener la**.

8. Si tiene previsto toocomplete pasos de hello en un momento posterior, asegúrese de que eliminar el clúster de HDInsight de Hola que creó en este artículo. 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a>Paso siguiente 

En este artículo ha aprendido cómo toocreate una HDInsight Spark clúster y ejecutando un Spark SQL básicas de consulta. Avanzar toohello siguiente artículo toolearn cómo toouse una HDInsight Spark clúster toorun realizar consultas interactivas en datos de ejemplo.

> [!div class="nextstepaction"]
>[Ejecución de consultas interactivas en un clúster de HDInsight Spark](hdinsight-apache-spark-load-data-run-query.md)



