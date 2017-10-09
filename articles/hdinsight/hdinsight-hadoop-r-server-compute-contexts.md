---
title: Opciones de contexto de aaaCompute de servidor de R en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de hello proceso distinto contexto opciones disponibles toousers con el servidor de R en HDInsight"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0deb0b1c-4094-459b-94fc-ec9b774c1f8a
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3b0d0cc3caa390797dcff8c73d66cd3ad78bcaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="compute-context-options-for-r-server-on-hdinsight"></a>Opciones de contexto de proceso para R Server en HDInsight (versión preliminar)

Microsoft R Server en HDInsight de Azure controla cómo se ejecutan las llamadas al establecer el contexto de proceso de Hola. Este artículo describe las opciones de Hola que están disponible toospecify si y la ejecución se ejecute en paralelo en núcleos del nodo del borde de Hola o clúster de HDInsight.

nodo de Hello borde de un clúster proporciona un lugar cómodo tooconnect toohello clúster y toorun los scripts de R. Con un nodo del borde, tienen funciones de opción de ejecución hello en paralelo distribuida Hola de ScaleR entre núcleos de Hola de servidores de nodos de hello borde. También puede ejecutar ellos en todos los nodos de Hola de clúster de hello mediante el uso del ScaleR Hadoop MapReduce o Spark contextos de proceso.

## <a name="microsoft-r-server-on-azure-hdinsight"></a>Microsoft R Server en Azure HDInsight
[Microsoft R Server en HDInsight de Azure](hdinsight-hadoop-r-server-overview.md) proporciona capacidades más recientes de hello para el análisis basado en R. Puede usar los datos que se almacenan en un contenedor HDFS en su [Azure Blob](../storage/common/storage-introduction.md "almacenamiento de blobs de Azure") cuenta de almacenamiento, un almacén de Data Lake o sistema de archivos de Linux local Hola. Puesto que R Server se basa en código abierto R, pueden aplicar Hola R aplicaciones que compilar cualquiera de los paquetes de código abierto R de hello 8000 +. También pueden usar las rutinas de hello en [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler), paquete de análisis de grandes cantidades de datos de Microsoft que se incluye con el servidor de R.  

## <a name="compute-contexts-for-an-edge-node"></a>Contextos de proceso de un nodo perimetral
En general, un script de R que se ejecuta en el servidor de R en el nodo del borde de Hola se ejecuta dentro de intérprete de R de hello en ese nodo. excepciones de Hello son los pasos que se llame a una función ScaleR. Hola ScaleR llamadas se ejecutan en un entorno de proceso que viene determinado por cómo establecer contexto de proceso de hello ScaleR.  Al ejecutar el script de R desde un nodo del borde, de los valores posibles de Hola Hola proceso contexto son:

- secuencial local (*‘local’*)
- paralelo local (*‘localpar’*)
- MapReduce
- Spark

Hola *'local'* y *'localpar'* opciones solo difieren en cómo **rxExec** se ejecutan las llamadas. Ejecutan otras llamadas a función rx de forma paralela en varios núcleos disponibles a menos que se especifique lo contrario mediante el uso de hello ScaleR **numCoresToUse** opción, por ejemplo `rxOptions(numCoresToUse=6)`. Las opciones de ejecución en paralelo ofrecen un rendimiento óptimo.

Hello en la tabla siguiente resume Hola que distintos contexto opciones tooset cómo se ejecutan las llamadas de proceso:

| Contexto de proceso  | Cómo tooset                      | Contexto de ejecución                        |
| ---------------- | ------------------------------- | ---------------------------------------- |
| Secuencial local | rxSetComputeContext(‘local’)    | Ejecución de ejecución en paralelo en núcleos Hola hello borde nodo del servidor de, excepto para las llamadas de rxExec, que se ejecutan en serie |
| Paralelo local   | rxSetComputeContext(‘localpar’) | Ejecución de ejecución en paralelo entre núcleos de Hola de servidores de nodos de hello borde |
| Spark            | RxSpark()                       | Ejecución distribuida a través de Spark en todos los nodos de Hola de clúster HDI de hello en paralelo |
| MapReduce       | RxHadoopMR()                    | Ejecución distribuida a través de MapReduce en todos los nodos de Hola de clúster HDI de hello en paralelo |

## <a name="guidelines-for-deciding-on-a-compute-context"></a>Directrices para decidir en un contexto de proceso

Hola tres opciones que elija que proporcionan la ejecución en paralelo de ejecución dependerá de naturaleza Hola de su trabajo de análisis, el tamaño de Hola y la ubicación de Hola de los datos. No hay ninguna fórmula simple que le indica que toouse de contexto de proceso. Sin embargo, hay algunos principios rectores que pueden ayudarle a realizar la elección correcta de Hola o, al menos, ayudar a delimitar las opciones antes de ejecutar una prueba comparativa. Estos principios rectores incluyen:

- sistema de archivos de Linux local Hello es más rápido que HDFS.
- Análisis repetidos son más rápidos si los datos de hello están locales, y si se encuentra en xdf..
- Es preferible toostream pequeñas cantidades de datos de un origen de datos de texto. Si la cantidad de Hola de datos es mayor, convertirla tooXDF antes del análisis.
- sobrecarga de Hola de copiar o nodo del borde toohello Hola datos para el análisis de transmisión por secuencias se convierte en imposible de administrar para grandes cantidades de datos.
- Spark es más rápido que MapReduce para el análisis de Hadoop.

Dados estos principios, hello las secciones siguientes ofrecen algunas reglas generales básicas para seleccionar un contexto de proceso.

### <a name="local"></a>Local
* Si la cantidad de Hola de tooanalyze de datos es pequeño y no requiere análisis repetidos, a continuación, lo transmita directamente en análisis de hello rutina con *'local'* o *'localpar'*.
* Si cantidad Hola de tooanalyze de datos es pequeño o mediano tamaño y requiere un análisis repetido, a continuación, copiar toohello sistema de archivos local, importar tooXDF y analizarlos a través de *'local'* o *'localpar'*.

### <a name="hadoop-spark"></a>Hadoop Spark
* Si la cantidad de Hola de tooanalyze de datos es grande, a continuación, impórtelo tooa trama de datos de Spark con **RxHiveData** o **RxParquetData**, o tooXDF en HDFS (a menos que el almacenamiento es un problema) y analizar mediante Hola Spark contexto de proceso.

### <a name="hadoop-map-reduce"></a>Hadoop MapReduce
* Usar contexto de proceso MapReduce Hola solo si se produce un problema con el contexto de proceso de hello Spark insuperables ya que es normalmente más lento.  

## <a name="inline-help-on-rxsetcomputecontext"></a>Ayuda insertada en rxSetComputeContext
Para obtener más información y ejemplos de ScaleR contextos de proceso, consulte en línea hello ayuda en R en el método de rxSetComputeContext hello, por ejemplo:

    > ?rxSetComputeContext

También puede hacer referencia toohello "[Guía de informática distribuida ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)" que está disponible en hello [R Server MSDN](https://msdn.microsoft.com/library/mt674634.aspx "R Server en MSDN") biblioteca.

## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido sobre opciones hello toospecify disponible si y cómo ejecución se ejecute en paralelo en núcleos del nodo del borde de Hola o clúster de HDInsight. toolearn más información acerca de cómo toouse R Server con HDInsight clústeres, vea Hola temas siguientes:

* [Información general sobre R Server en Hadoop](hdinsight-hadoop-r-server-overview.md)
* [Introducción a R Server en Hadoop](hdinsight-hadoop-r-server-get-started.md)
* [Agregar servidor RStudio tooHDInsight (si no se agregan durante la creación del clúster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opciones de Azure Storage para R Server en HDInsight](hdinsight-hadoop-r-server-storage.md)

