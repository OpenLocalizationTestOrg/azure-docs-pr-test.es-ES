---
title: "clústeres de aaaInstall eso es todo en HDInsight Linux de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall ya está preparado y Airpal en Hadoop de HDInsight basados en Linux clústeres mediante acciones de Script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a>Instalación y uso de Presto en clústeres de Hadoop para HDInsight

En este tema, aprenderá cómo tooinstall eso es todo en Hadoop de HDInsight clústeres mediante la acción de secuencia de comandos. También aprenderá cómo tooinstall Airpal en un clúster de HDInsight Presto existente.

> [!IMPORTANT]
> Hello pasos en este documento, es necesario un **clúster de Hadoop de HDInsight 3.5** que usa Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Para más información, consulte las [versiones de HDInsight](hdinsight-component-versioning.md).

## <a name="what-is-presto"></a>¿Qué es Presto?
[Presto](https://prestodb.io/overview.html) es un motor de consultas SQL de distribución rápida para macrodatos. Presto es adecuado para las consultas interactivas de petabytes de datos. Para obtener más información sobre componentes de Hola de ya está preparado y cómo funcionan juntos, consulte [conceptos listo](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).

> [!WARNING]
> Componentes suministrados con clúster de HDInsight de hello son totalmente compatibles y Microsoft Support le ayudarán tooisolate y resolver los problemas relacionados toothese componentes.
> 
> Componentes personalizados, por ejemplo, eso es todo, reciban soporte comercialmente razonable toohelp toofurther solucionar el problema de Hola. Esto podría producir en resolver el problema de hello ni pedir que tooengage canales disponibles para hello abrir tecnologías de origen donde se encuentra la amplia experiencia para que la tecnología. Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Los proyectos de Apache también tienen sitios de proyecto en [http://apache.org](http://apache.org) (por ejemplo, [Hadoop](http://hadoop.apache.org/)).
> 
> 


## <a name="install-presto-using-script-action"></a>Instalación de Presto con una acción de script

Esta sección proporciona instrucciones sobre cómo el script de ejemplo de Hola toouse al crear un nuevo clúster mediante Hola portal de Azure. 

1. Iniciar el aprovisionamiento de un clúster mediante el uso de pasos de hello en [clústeres de HDInsight basados en Linux aprovisionar](hdinsight-hadoop-create-linux-clusters-portal.md). Asegúrese de crear el clúster hello mediante hello **personalizado** flujo de creación de clúster. Debe asegurarse de ese clúster Hola que creas cumple Hola según los requisitos.

    a. Tiene que ser un clúster Hadoop con HDInsight versión 3.5.

    b. Almacenamiento de Azure, debe usar como almacén de datos de Hola. Aún no se admite el uso de Presto en un clúster que utiliza el almacén de Azure Data Lake como opción de almacenamiento de Hola. 

    ![Creación de un clúster de HDInsight usando las opciones personalizadas](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. En hello **configuración avanzada** hoja, seleccione **acciones de Script**y proporcionar información de Hola a continuación:
   
   * **NOMBRE**: escriba un nombre descriptivo para la acción de secuencia de comandos de Hola.
   * **URI de script de Bash**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`
   * **PRINCIPAL**: active esta opción.
   * **TRABAJADOR**: active esta opción.
   * **ZOOKEEPER**: desactive esta casilla
   * **PARÁMETROS**: deje este campo en blanco.


3. Final de Hola de hello **acciones de Script** hoja, haga clic en hello **seleccione** configuración del botón toosave Hola. Por último, haga clic en hello **seleccione** situado en la parte inferior de Hola de hello **configuración avanzada** información de configuración de hoja toosave Hola.

4. Continuar aprovisionamiento clúster Hola tal y como se describe en [clústeres de HDInsight basados en Linux aprovisionar](hdinsight-hadoop-create-linux-clusters-portal.md).

    > [!NOTE]
    > Azure PowerShell, Hola CLI de Azure, hello HDInsight .NET SDK o plantillas del Administrador de recursos de Azure también pueden ser utilizados tooapply acciones de script. También puede aplicar tooalready de acciones de script clústeres en ejecución. Para obtener más información, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster-linux.md).
    > 
    > 

## <a name="use-presto-with-hdinsight"></a>Uso de Presto con HDInsight

Realizar Hola siguiendo los pasos toouse eso es todo en un clúster de HDInsight después de haber instalado mediante pasos de Hola se ha descrito anteriormente.

1. Conecte el clúster de HDInsight de toohello mediante SSH:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
     

2. Inicie Hola shell listo mediante el siguiente comando de Hola.
   
        presto --schema default

3. Ejecute una consulta en una tabla de ejemplo, **hivesampletable**, que está disponible en todos los clústeres de HDInsight de forma predeterminada.
   
        select count (*) from hivesampletable;
   
    De forma predeterminada, los conectores [Hive](https://prestodb.io/docs/current/connector/hive.html) y [TPCH](https://prestodb.io/docs/current/connector/tpch.html) para Presto ya están configurados. Conector de subárbol es instalación de Hive de toouse configurado Hola instalada de forma predeterminada, por lo que todas las tablas de Hola de subárbol se verán automáticamente en eso es todo.

    Para obtener una descripción detallada de cómo puede utilizar Presto, consulte la [documentación de Presto](https://prestodb.io/docs/current/index.html).

## <a name="use-airpal-with-presto"></a>Uso de Airpal con Presto

[Airpal](https://github.com/airbnb/airpal#airpal) es una interfaz de consulta de código abierto basada en web para Presto. Para más información sobre Airpal, consulte la [documentación de Airpal](https://github.com/airbnb/airpal#airpal).

En esta sección, veremos los pasos de hello demasiado**instalar Airpal en hello edgenode** de un clúster de Hadoop de HDInsight, que ya tiene eso es todo instalado. Esto garantiza que esa interfaz de consulta de hello Airpal web está disponible a través de Internet de Hola.

1. Mediante SSH, conecte el nodo principal de toohello Hola del clúster de HDInsight que tenga instalado Presto:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Una vez conectado, ejecute el siguiente comando de Hola.

        sudo slider registry  --name presto1 --getexp presto 
   
    Debería ver una salida similar Hola siguiente:

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. De salida de hello, anote el valor de Hola para hello **valor** propiedad. Lo necesitará al instalar Airpal en hello edgenode de clúster. Desde la salida de hello anteriormente, el valor de Hola que necesitará es **10.0.0.12:9090**.

4. Utilizar una plantilla de hello  **[aquí](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate una HDInsight edgenode de clúster y proporcione los valores de hello tal y como se muestra en la siguiente captura de pantalla de Hola.

    ![Instalación de Airpal en el clúster de HDInsight con Presto](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. Haga clic en **Comprar**.

6. Una vez realizados cambios hello toohello aplicada configuración del clúster, puede obtener acceso a interfaz web de hello Airpal utilizando Hola pasos.

    a. En la hoja de clúster de hello, haga clic en **aplicaciones**.

    ![Inicio de Airpal en el clúster de HDInsight con Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    b. De hello **instalado aplicaciones** hoja, haga clic en **Portal** contra airpal.

    ![Inicio de Airpal en el clúster de HDInsight con Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    c. Cuando se le solicite, escriba credenciales de administrador de Hola que especificó al crear el clúster de Hadoop de HDInsight de Hola.

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a>Personalización de una instalación de Presto en un clúster de HDInsight

Después de haber instalado ya está preparado en un clúster de Hadoop de HDInsight, puede personalizar Hola instalación toomake cambios como la configuración de memoria de actualización, cambiar los conectores, etcetera. Realizar Hola siguiendo los pasos toodo así.

1. Mediante SSH, conecte el nodo principal de toohello Hola del clúster de HDInsight que tenga instalado Presto:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Realice los cambios de configuración en el archivo hello `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`. Para más información sobre la configuración de presto, consulte [Presto Configuration Options for YARN-Based Clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html) (Opciones de configuración de Presto para clústeres basados en YARN).

3. Detener y eliminar la instancia de ejecución actual de Hola de eso es todo.

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. Inicie una nueva instancia de eso es todo con la personalización de Hola.

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. Espere toobe de instancia nueva de hello listo y anote la dirección del coordinador listo.


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a>Generación de datos de pruebas comparativas para clústeres de HDInsight que ejecutan Presto

TPC-DS es Hola estándar del sector para medir el rendimiento de Hola de muchos sistemas de soporte técnico de decisión, incluidos los sistemas de grandes cantidades de datos. Puede usar Presto en los datos de toogenerate de clústeres de HDInsight y evaluar la manera en que compara con sus propios datos de prueba comparativa de HDInsight. Para más información, consulte [esta página](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).



## <a name="see-also"></a>Consulte también
* [Instalación y uso de Hue en clústeres de HDInsight](hdinsight-hadoop-hue-linux.md). El matiz es una interfaz de usuario que hace más fácil toocreate, ejecute web y guarde los trabajos de Pig y Hive, así como examinar almacenamiento predeterminado de hello para el clúster de HDInsight.

* [Instalación de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install-linux.md). Utilice tooinstall de personalización de clúster de clústeres de Giraph en Hadoop de HDInsight. Giraph permite gráfico tooperform procesamiento por medio de Hadoop y puede utilizarse con HDInsight de Azure.

* [Instalación de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install-linux.md). Utilice tooinstall de personalización de clúster de clústeres de Solr en Hadoop de HDInsight. Solr permite operaciones de búsqueda eficaces tooperform en los datos almacenados.

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
