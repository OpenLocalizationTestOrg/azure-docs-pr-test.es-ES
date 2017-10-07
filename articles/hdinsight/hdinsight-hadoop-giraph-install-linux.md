---
title: aaaInstall y usar Giraph en HDInsight (Hadoop) - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo usar acciones de Script de clústeres de tooinstall Giraph en HDInsight basados en Linux. Acciones de script permiten clúster de hello toocustomize durante la creación, cambiando la configuración de clúster o instalar utilidades y servicios."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a>Instalar Giraph en clústeres de Hadoop de HDInsight y usar gráficos de Giraph tooprocess a gran escala

Obtenga información acerca de cómo tooinstall Giraph Apache en un clúster de HDInsight. característica de acción de secuencia de comandos de Hola de HDInsight le permite toocustomize el clúster mediante la ejecución de una secuencia de comandos de bash. Las secuencias de comandos pueden ser usado toocustomize clústeres durante y después de crear el clúster.

> [!IMPORTANT]
> pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="whatis"></a>¿Qué es Giraph?

[Apache Giraph](http://giraph.apache.org/) permite gráfico tooperform procesamiento por medio de Hadoop y puede utilizarse con HDInsight de Azure. Los gráficos modelan las relaciones entre los objetos. Por ejemplo, las conexiones de hello entre enrutadores de una red de gran tamaño como Hola Internet o las relaciones entre usuarios de redes sociales. Procesamiento de gráficos le permite tooreason acerca de las relaciones de hello entre los objetos en un gráfico, como:

* Identificar los posibles amigos según las relaciones actuales.

* Identifica la ruta más corta de hello entre dos equipos en una red.

* Calcular la clasificación de la página de Hola de páginas Web.

> [!WARNING]
> Componentes suministrados con clúster de HDInsight de hello son totalmente compatibles: Microsoft Support le ayuda a tooisolate y resolver los problemas relacionados toothese componentes.
>
> Componentes personalizados, como Giraph, reciban soporte comercialmente razonable toohelp toofurther solucionar el problema de Hola. Microsoft Support puede ser capaz de tooresolving problema de Hola. Si no es así, debe consultar las comunidades de código abierto donde grandes expertos en esa tecnología. Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Los proyectos de Apache también tienen sitios de proyecto en [http://apache.org](http://apache.org) (por ejemplo, [Hadoop](http://hadoop.apache.org/)).


## <a name="what-hello-script-does"></a>El script de Hola hace

Este script realiza Hola siguientes acciones:

* Instala Giraph demasiado`/usr/hdp/current/giraph`

* Hola copias `giraph-examples.jar` almacenamiento de archivos toodefault (WASB) para el clúster:`/example/jars/giraph-examples.jar`

## <a name="install"></a>Instalación de Giraph mediante acciones de script

Tooinstall de secuencia de comandos de ejemplo Giraph en un clúster de HDInsight está disponible en hello ubicación siguiente:

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

Esta sección proporciona instrucciones sobre cómo toouse Hola script de ejemplo al crear el clúster de Hola utilizando Hola portal de Azure.

> [!NOTE]
> Una acción de secuencia de comandos se puede aplicar mediante cualquiera de los siguientes métodos de hello:
> * Azure PowerShell
> * Hola CLI de Azure
> * Hola HDInsight .NET SDK
> * Plantillas de Azure Resource Manager
> 
> También puede aplicar tooalready de acciones de script clústeres en ejecución. Para obtener más información, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster-linux.md).

1. Empezar a crear un clúster mediante el uso de pasos de hello en [clústeres de HDInsight basados en Linux crear](hdinsight-hadoop-create-linux-clusters-portal.md), pero no se completó la creación.

2. En hello **configuración opcional** hoja, seleccione **acciones de Script**y proporcionar Hola siguiente información:

   * **NOMBRE**: escriba un nombre descriptivo para la acción de secuencia de comandos de Hola.

   * **URI del SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

   * **PRINCIPAL**: active esta entrada.

   * **TRABAJO**: deje esta opción desactivada.

   * **ZOOKEEPER**: deje esta opción desactivada.

   * **PARÁMETROS**: deje este campo en blanco.

3. Final de Hola de hello **acciones de Script**, usar hello **seleccione** configuración del botón toosave Hola. Por último, utilice hello **seleccione** situado en la parte inferior de Hola de hello **configuración opcional** información de configuración opcional de hoja toosave Hola.

4. Continuar con la creación de clúster de hello tal y como se describe en [clústeres de HDInsight basados en Linux crear](hdinsight-hadoop-create-linux-clusters-portal.md).

## <a name="usegiraph"></a>¿Cómo uso Giraph en HDInsight?

Una vez que se haya creado el clúster de hello, utilice Hola pasos toorun hello SimpleShortestPathsComputation ejemplo incluido con Giraph siguiente. Este ejemplo utiliza básica hello [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementación para buscar la ruta de acceso más corta de hello entre los objetos de un gráfico.

1. Conecte el clúster de HDInsight de toohello mediante SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Comando de uso Hola siguiente toocreate un archivo denominado **tiny_graph.txt**:

    ```bash
    nano tiny_graph.txt
    ```

    Usar hello después de texto como contenido de Hola de este archivo:

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    Estos datos describen una relación entre los objetos de un gráfico dirigido, con formato de hello `[source_id, source_value,[[dest_id], [edge_value],...]]`. Cada línea representa una relación entre un objeto `source_id` y uno varios objetos `dest_id`. Hola `edge_value` puede considerarse como la intensidad de Hola o distancia de conexión de hello entre `source_id` y `dest\_id`.

    Dibujar, y con el valor de hello (o peso) como la distancia de hello entre objetos, datos de hello podrían parecerse Hola siguiente diagrama:

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. archivo de hello toosave, use **CTRL+x**, a continuación, **Y**y, finalmente, **ENTRAR** tooaccept nombre de archivo de Hola.

4. Usar hello seguir los datos de hello toostore en el almacenamiento principal para el clúster de HDInsight:

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. Ejecutar el ejemplo de SimpleShortestPathsComputation Hola Hola siguiente comando:

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    en hello en la tabla siguiente se describen los parámetros de Hello utilizados con este comando:

   | Parámetro | Qué hace |
   | --- | --- |
   | `jar` |archivo de Hello jar que contiene ejemplos de hello. |
   | `org.apache.giraph.GiraphRunner` |clase Hello utiliza los ejemplos de hello toostart. |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |ejemplo de Hola que se utiliza. En este ejemplo, calcula la ruta de acceso más corta de hello entre el identificador 1 y todos los otros identificadores en el gráfico de Hola. |
   | `-ca mapred.job.tracker` |nodo principal de Hello para el clúster de Hola. |
   | `-vif` |Hola toouse de formato de entrada de datos de entrada de Hola. |
   | `-vip` |archivo de datos de entrada de Hello. |
   | `-vof` |formato de salida de Hello. En este caso, el identificador y el valor como texto sin formato. |
   | `-op` |ubicación de salida de Hello. |
   | `-w 2` |número de Hola de trabajadores toouse. En este ejemplo, 2. |

    Para obtener más información sobre estos y otros parámetros que se usan con Giraph ejemplos, vea hello [inicio rápido de Giraph](http://giraph.apache.org/quick_start.html).

6. Una vez que haya finalizado el trabajo de hello, resultados de Hola se almacenan en hello **/example/out/shotestpaths** directory. Hello nombres de archivo de salida comienzan por **parte-m -** y terminar con un número que indica hello en primer lugar, en segundo lugar, el archivo de etc.. Usar hello siguiendo la salida del comando tooview hello:

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    salida de Hello debe aparecer toohello similar siguiente texto:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    ejemplo de Hola a SimpleShortestPathComputation es toostart codificado con objeto de identificador 1 y buscar objetos de tooother de ruta de acceso más cortos de Hola. salida de Hello está en formato de Hola de `destination_id` y `distance`. Hola `distance` es el valor de hello (o peso) de los bordes de hello recorridos entre objeto identificador 1 y Hola Id. de destino.

    Visualizar estos datos, puede comprobar los resultados de Hola por las rutas de acceso más cortas de hello en viaje entre el identificador 1 y todos los demás objetos. Hola ruta de acceso más corta entre el identificador 1 y 4 de identificador es 5. Este valor es la distancia total de hello entre <span style="color:orange">identificador 1 y 3</span>y, a continuación, <span style="color:red">identificador 3 y 4</span>.

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a>Pasos siguientes

* [Instalación y uso de Hue en clústeres de HDInsight](hdinsight-hadoop-hue-linux.md).

* [Instalación de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install-linux.md).
