---
title: "aaaAzure datos Lake almacén Hive rendimiento directrices de ajuste | Documentos de Microsoft"
description: "Directrices para la optimización del rendimiento de Hive en Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: e44daeb6ad3b64e893c709df63b56444a330729f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a>Guía para la optimización del rendimiento de Hive en HDInsight y Azure Data Lake Store

configuración predeterminada de Hola se establecieron tooprovide un buen rendimiento en muchos casos de uso diferentes.  Para las consultas de uso intensivo de E/S, subárbol puede ser un mejor rendimiento de tooget optimizada con ADLS.  

## <a name="prerequisites"></a>Requisitos previos

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Una cuenta de Almacén de Azure Data Lake**. Para obtener instrucciones sobre cómo toocreate un, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md)
* **Clúster de HDInsight de Azure** con acceso tooa cuenta de almacén de Data Lake. Consulte [Creación de un clúster de HDInsight con Data Lake Store mediante el Portal de Azure](data-lake-store-hdinsight-hadoop-use-portal.md). Asegúrese de que habilitar Escritorio remoto para el clúster de Hola.
* **Ejecución de Hive en HDInsight**.  toolearn acerca de cómo ejecutar trabajos de Hive en HDInsight, vea [uso Hive en HDInsight] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)
* **Directrices para la optimización del rendimiento en ADLS**.  Para conocer los conceptos generales de rendimiento, consulte [Guía para la optimización del rendimiento de Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance).

## <a name="parameters"></a>parameters

A continuación, incluimos hello tootune más importante de configuración para mejorar el rendimiento de ADLS:

* **Hive.tez.Container.Size** : cantidad de Hola de memoria usada por cada tareas

* **tez.grouping.min-size**: tamaño mínimo de cada asignador.

* **tez.grouping.min-size**: tamaño mínimo de cada asignador.

* **hive.exec.reducer.bytes.per.reducer**: tamaño de cada reductor.

**Hive.tez.Container.Size** -tamaño del contenedor de hello determina la cantidad de memoria está disponible para cada tarea.  Se trata de entrada principal de Hola para control de simultaneidad de hello en el subárbol.  

**tamaño de tez.GROUPING.min** : este parámetro permite un tamaño mínimo de hello tooset de cada asignador.  Si el número de Hola de asignadores que Tez elige es menor que el valor de Hola de este parámetro, Tez utilizará valor Hola establecido aquí.  

**tamaño de tez.GROUPING.max** : parámetro hello permite un tamaño máximo de hello tooset de cada asignador.  Si el número de Hola de asignadores que elige Tez es mayor que el valor de Hola de este parámetro, Tez utilizará valor Hola establecido aquí.  

**Hive.Exec.reducer.bytes.per.reducer** : este parámetro establece el tamaño de Hola de cada reductor.  De forma predeterminada, cada reductor tiene 256 MB.  

## <a name="guidance"></a>Guía

**Establecer hive.exec.reducer.bytes.per.reducer** : valor predeterminado de hello funciona bien cuando los datos de hello están sin comprimir.  Para los datos que se ha comprimido, debe reducir tamaño de hello del reductor Hola.  

**Set hive.tez.container.size**: en cada nodo, la memoria se especifica mediante yarn.nodemanager.resource.memory-mb y se debe establecer correctamente en el clúster de HDI de forma predeterminada.  Para obtener información adicional acerca de la configuración de memoria apropiada de hello en hilo, consulte este [registrar](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).

Cargas de trabajo intensivas de E/S pueden beneficiarse de paralelismo más reduciendo el tamaño del contenedor Tez Hola. Esto proporciona al usuario hello más contenedores que aumenta la simultaneidad.  Sin embargo, algunas consultas de Hive requieren una cantidad significativa de memoria (p. ej. MapJoin).  Si la tarea hello no tiene suficiente memoria, obtendrá un excepción de memoria insuficiente durante el tiempo de ejecución.  Si recibe excepciones por memoria insuficiente, debe aumentar la memoria de Hola.   

Hola simultáneas número de tareas en ejecución o paralelismo estarán enlazado por total de memoria YARN Hola.  número de Hola de contenedores YARN determinará cuántas tareas simultáneas puedan ejecutarse.  memoria de hilo de hello toofind por nodo, puede ir tooAmbari.  Navegue tooYARN y ver la ficha de configuraciones de Hola.  Hola memoria YARN se muestra en esta ventana.  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
rendimiento de clave tooimproving de Hello mediante ADLS es simultaneidad de hello tooincrease tanto como sea posible.  Tez calcula automáticamente el número de Hola de tareas que se debe crear por lo que no es necesario tooset lo.   

## <a name="example-calculation"></a>Cálculo de ejemplo

Supongamos que tiene un clúster D14 de 8 nodos.  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a>Limitaciones
**Limitación de ADLS** 

UIf aciertos Hola los límites de ancho de banda proporcionados por ADLS, tendría que empezar por errores en la tarea toosee. Esto puede identificarse observando los errores de limitación en los registros de tarea.  Puede reducir el paralelismo de Hola al aumentar el tamaño del contenedor Tez.  Si necesita más simultaneidad para su trabajo, póngase en contacto con nosotros.   

toocheck si están obteniendo limitados, deberá tooenable Hola registro de depuración en el lado del cliente de Hola. Así es cómo debe hacerlo:

1. Hola Put después de propiedad en las propiedades de log4j hello en la configuración de Hive. Esto puede hacerse desde Vista Ambari: log4j.logger.com.microsoft.azure.datalake.store=DEBUG reiniciar todos los nodos/servicio hello para el efecto de hello config tootake.

2. Si están obteniendo limitados, verá el código de error HTTP 429 hello en el archivo de registro de hello hive. archivo de registro del subárbol de Hello está en /tmp/&lt;usuario&gt;/hive.log

## <a name="further-information-on-hive-tuning"></a>Información adicional sobre la optimización de Hive

Estos son algunos blogs que le ayudará a optimizar las consultas de Hive:
* [Optimizar consultas de Hive para Hadoop en HDInsight](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [Troubleshooting Hive query performance](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/) (Solución de problemas de rendimiento de consultas de Hive)
* [Ignite talk on optimize Hive on HDInsight](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25) (Acalorada charla sobre la optimización de Hive en HDInsight)
