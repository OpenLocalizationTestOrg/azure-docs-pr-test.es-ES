---
title: "aaaCopy datos tooand de WASB en el almacén de Data Lake con Distcp | Documentos de Microsoft"
description: "Usar Distcp herramienta toocopy datos tooand almacenamiento de Blobs tooData Lake del almacén de Azure"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a>Usar Distcp toocopy datos entre los Blobs de almacenamiento de Azure y almacén de Data Lake
> [!div class="op_single_selector"]
> * [Uso de DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [Uso de AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Una vez haya creado un clúster de HDInsight con la cuenta de acceso de almacén de Data Lake tooa, también puede usar herramientas de ecosistema de Hadoop como Distcp toocopy datos **tooand de** un almacenamiento de clúster de HDInsight (WASB) en una cuenta de almacén de Data Lake. Este artículo proporciona instrucciones sobre cómo tooachieve esto.

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este artículo, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Una cuenta de Almacén de Azure Data Lake**. Para obtener instrucciones sobre cómo toocreate un, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md)
* **Clúster de HDInsight de Azure** con acceso tooa cuenta de almacén de Data Lake. Consulte [Creación de un clúster de HDInsight con Data Lake Store mediante el Portal de Azure](data-lake-store-hdinsight-hadoop-use-portal.md). Asegúrese de que habilitar Escritorio remoto para el clúster de Hola.

## <a name="do-you-learn-fast-with-videos"></a>¿Obtener información más rápidamente con vídeos?
[Vea este vídeo](https://mix.office.com/watch/1liuojvdx6sie) acerca de cómo toocopy datos entre los Blobs de almacenamiento de Azure y almacén de Data Lake mediante DistCp.

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a>Usar Distcp desde un clúster de HDInsight de Linux

Un clúster de HDInsight que se incluye con la utilidad Distcp hello, que puede ser utilizados toocopy datos de orígenes diferentes en un clúster de HDInsight. Si ha configurado el almacén de hello HDInsight clúster toouse Data Lake como un almacenamiento adicional, hello Distcp utilidad se puede utiliza tooand de datos de cuadro toocopy desde una cuenta del almacén de Data Lake. En esta sección veremos cómo toouse Hola Distcp utilidad.

1. Desde el escritorio, use SSH tooconnect toohello clúster. Vea [clúster de HDInsight basados en Linux de conectar tooa](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md). Ejecute comandos de Hola desde el símbolo del sistema de hello SSH.

2. Compruebe si puede tener acceso a Hola Blobs de almacenamiento de Azure (WASB). Ejecute el siguiente comando de hello:

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    Esto debería proporcionar una lista de contenido de blob de almacenamiento de Hola.
3. De forma similar, compruebe si tiene acceso a cuenta de almacén de Data Lake Hola de clúster de Hola. Ejecute el siguiente comando de hello:

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    Esto debería proporcionar una lista de archivos o carpetas en hello cuenta de almacén de Data Lake.
4. Usar datos de toocopy de Distcp de WASB tooa cuenta de almacén de Data Lake.

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    Esto copiará el contenido de Hola de hello **/ejemplo/datos/gutenberg/** carpeta en WASB demasiado**/myfolder** Hola cuenta de almacén de Data Lake.
5. Asimismo, utilice Distcp toocopy datos de almacén de Data Lake cuenta tooWASB.

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    Esto copiará el contenido de Hola de **/myfolder** Hola almacén de Data Lake cuenta demasiado**/ejemplo/datos/gutenberg/** carpeta en WASB.

## <a name="performance-considerations-while-using-distcp"></a>Consideraciones de rendimiento sobre el uso de DistCp

Porque DistCp's menor granularidad es un único archivo, establecer número máximo de Hola de copias simultáneas es hello toooptimize de parámetro más importante con el almacén de Data Lake. Esto se controla estableciendo el número de Hola de asignadores ('m ') parámetro en la línea de comandos de Hola. Este parámetro especifica el número máximo de Hola de asignadores que será usado toocopy datos. El valor predeterminado es 20.

**Ejemplo**

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a>¿Cómo se determina el número de Hola de asignadores toouse?

A continuación hay algunas instrucciones que puede usar.

* **Paso 1: Determinar la memoria total de YARN** -Hola primer paso es clúster toodetermine hello YARN memoria disponible toohello donde ejecutar trabajo de DistCp Hola. Esta información está disponible en el portal de Ambari Hola asociada Hola clúster. Navegue tooYARN y ver Hola configuraciones pestaña toosee hello YARN memoria. tooget hello YARN memoria total, multiplicar Hola de memoria YARN por nodo con el número de Hola de nodos tienen en el clúster.

* **Paso 2: Calcular el número de Hola de asignadores** -Hola valo **m** es toohello igual cociente de la memoria total de YARN dividido por hello tamaño del contenedor YARN. Hola información de tamaño del contenedor YARN está disponible en el portal de Ambari Hola también. Navegue tooYARN y vista Hola configuraciones ficha Hola tamaño de contenedor YARN se muestra en esta ventana. Hola tooarrive ecuación en el número de Hola de asignadores (**m**) es

        m = (number of nodes * YARN memory for each node) / YARN container size

**Ejemplo**

Supongamos que tiene un 4 nodos D14v2s en clúster de Hola y que está tratando de tootransfer 10TB de datos de 10 carpetas diferentes. Cada una de las carpetas de hello contienen diferentes cantidades de datos y tamaños de archivo hello dentro de cada carpeta son diferentes.

* Memoria total de YARN - de hello portal Ambari determinar esa memoria YARN hello es 96GB para un nodo de D14. Por lo tanto, la memoria de YARN total para el clúster de 4 nodos es: 

        YARN memory = 4 * 96GB = 384GB

* Número de asignadores - de hello portal Ambari determinar que ese tamaño de contenedor YARN hello es 3072 para un nodo de clúster D14. Por lo tanto, el número de asignadores es:

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

Si otras aplicaciones utilizan la memoria, puede elegir la utilización de tooonly parte de la memoria de hilo de su clúster para DistCp.

### <a name="copying-large-datasets"></a>Copia de grandes conjuntos de datos

Cuando desplaza el tamaño de Hola de hello toobe de conjunto de datos es muy grande (por ejemplo, > 1TB) o si tiene muchas carpetas distintas, considere la posibilidad de usar varios trabajos de DistCp. Es probable que no hay ninguna mejora de rendimiento, pero se propagan trabajos hello, por lo que si se produce un error en cualquier trabajo, solo tendrá que toorestart ese trabajo específico en lugar de trabajo completo de Hola.

### <a name="limitations"></a>Limitaciones

* DistCp intenta a asignadores toocreate que son similares en el rendimiento de toooptimize de tamaño. Aumentar el número de Hola de asignadores puede no siempre aumentar el rendimiento.

* DistCp es tooonly limitado el uno asignador por cada archivo. Por lo tanto, no debería tener más asignadores que archivos. Puesto que DistCp solo puede asignar al asignador de un archivo de tooa, esto limita la cantidad de Hola de simultaneidad que puede ser archivos de gran tamaño toocopy usado.

* Si tiene un pequeño número de archivos de gran tamaño, a continuación, se deben dividir en una toogive de fragmentos de archivo de 256MB se más simultaneidad posible. 
 
* Si va a copiar de una cuenta de almacenamiento de blobs de Azure, se puede limitar el trabajo de copia en lado de almacenamiento de blobs de Hola. Esto disminuirá el rendimiento de Hola de su trabajo de copia. toolearn más información acerca de los límites de Hola de almacenamiento de blobs de Azure, consulte los límites de almacenamiento de Azure en [suscripción de Azure y límites de servicio](../azure-subscription-service-limits.md).

## <a name="see-also"></a>Otras referencias
* [Copiar los datos de almacén de Blobs de Azure almacenamiento Lake tooData](data-lake-store-copy-data-azure-storage-blob.md)
* [Protección de los datos en el Almacén de Data Lake](data-lake-store-secure-data.md)
* [Uso de Análisis de Azure Data Lake con el Almacén de Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Uso de HDInsight de Azure con el Almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
