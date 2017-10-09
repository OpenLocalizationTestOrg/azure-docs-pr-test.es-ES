---
title: "aaaAzure datos Lake almacén Spark Performance Tuning Guidelines | Documentos de Microsoft"
description: "Directrices para la optimización del rendimiento de Spark en Azure Data Lake Store"
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
ms.openlocfilehash: da1d172e9cb1199ad95605ea1718e78559f79650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-spark-on-hdinsight-and-azure-data-lake-store"></a>Guía para la optimización del rendimiento de Spark en HDInsight y Azure Data Lake Store

Al ajustar el rendimiento en Spark, necesita tooconsider Hola número de aplicaciones que se ejecutarán en el clúster.  De forma predeterminada, puede ejecutar 4 aplicaciones simultáneamente en el clúster HDI (Nota: saludo predeterminado es toochange asunto).  Puede decidir toouse menos aplicaciones para que pueda reemplazar la configuración predeterminada de Hola y utilizar más de clúster de Hola para esas aplicaciones.  

## <a name="prerequisites"></a>Requisitos previos

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Una cuenta de Almacén de Azure Data Lake**. Para obtener instrucciones sobre cómo toocreate un, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md)
* **Clúster de HDInsight de Azure** con acceso tooa cuenta de almacén de Data Lake. Consulte [Creación de un clúster de HDInsight con Data Lake Store mediante el Portal de Azure](data-lake-store-hdinsight-hadoop-use-portal.md). Asegúrese de que habilitar Escritorio remoto para el clúster de Hola.
* **Ejecutar el clúster de Spark en Azure Data Lake Store**.  Para obtener más información, vea [datos de uso HDInsight Spark clúster tooanalyze en almacén de Data Lake](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)
* **Directrices para la optimización del rendimiento en ADLS**.  Para conocer los conceptos generales de rendimiento, consulte [Guía para la optimización del rendimiento de Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance). 

## <a name="parameters"></a>parameters

Al ejecutar los trabajos de Spark, esta es la configuración de más importante de Hola que puede mejorar el rendimiento optimizadas tooincrease en ADLS:

* **Ejecutor de NUM** -Hola número de tareas simultáneas que se pueden ejecutar.

* **Memoria de ejecutor** -Hola cantidad de memoria asignada tooeach ejecutor.

* **Núcleos de ejecutor** -Hola número de núcleos asignados tooeach ejecutor.                     

**Ejecutor de NUM** Num ejecutor establecerá el número máximo de Hola de tareas que se pueden ejecutar en paralelo.  número real de Hola de tareas que se pueden ejecutar en paralelo está limitado por la memoria de Hola y recursos de CPU disponibles en el clúster.

**Memoria de ejecutor** es Hola cantidad de memoria que se asigna el ejecutor de tooeach.  memoria de Hello necesaria para cada elemento de ejecución es dependiente de trabajo de Hola.  Para operaciones más complejas, memoria de hello debe toobe superior.  En cambio, para las simples como la lectura y escritura, los requisitos de memoria serán menores.  Hola cantidad de memoria para cada elemento de ejecución puede verse en Ambari.  En Ambari, navegue tooSpark y ver la ficha de configuraciones de Hola.  

**Núcleos de ejecutor** Esto establece la cantidad de Hola de núcleos usados por ejecutor, que determina el número de Hola de subprocesos paralelos que se pueden ejecutar por ejecutor.  Por ejemplo, si ejecutor núcleos = 2, después cada ejecutor puede ejecutar 2 tareas paralelas en el ejecutor de Hola.  Hola ejecutor-núcleos necesitan dependerá trabajo Hola.  Los trabajos con muchas E/S no requieren una gran cantidad de memoria por tarea, por lo que cada ejecutor puede administrar más tareas paralelas.

De forma predeterminada, se definen dos núcleos YARN virtuales para cada núcleo físico cuando se ejecuta Spark en HDInsight.  Este número proporciona un buen equilibrio entre simultaneidad y la cantidad de cambios de contexto desde varios subprocesos.  

## <a name="guidance"></a>Guía

Mientras se ejecuta Spark toowork de las cargas de trabajo de análisis con los datos de almacén de Data Lake, le recomendamos que use hello más reciente HDInsight versión tooget Hola un rendimiento óptimo con almacén de Data Lake. Cuando el trabajo es más intensiva de E/S, ciertos parámetros pueden ser rendimiento tooimprove configurado.  Azure Data Lake Store es una plataforma de almacenamiento altamente escalable que puede controlar un alto rendimiento.  Si el trabajo de hello está compuesto principalmente de lectura o escritura, a continuación, aumenta la simultaneidad para tooand de E/S de almacén de Azure Data Lake podría mejorar el rendimiento.

Hay unos cuantos simultaneidad de tooincrease métodos generales para los trabajos de uso intensivo de E/S.

**Paso 1: Determinar las aplicaciones se ejecutan en el clúster** – debe conocer las aplicaciones se ejecutan en clúster de hello incluidos Hola actual.  valores predeterminados Hola para cada Spark configuración asume que hay 4 aplicaciones que se ejecutan simultáneamente.  Por lo tanto, solo tendrá el 25% del clúster de hello están disponibles para cada aplicación.  tooget un mejor rendimiento, puede invalidar los valores predeterminados de Hola cambiando el número de Hola de ejecutor.  

**Paso 2: Establecer la memoria de ejecutor** : hello lo primero que tooset es Hola ejecutor memoria.  memoria de Hello dependerá trabajo Hola que son toorun continuo.  Puede aumentar la simultaneidad asignando menos memoria a cada ejecutor.  Si ve excepciones por memoria insuficiente al ejecutar el trabajo, debe aumentar el valor Hola para este parámetro.  Una alternativa es tooget más memoria usando un clúster que tiene la mayor cantidad de memoria o aumentar el tamaño de hello del clúster.  Más memoria, habilitará más toobe ejecutor utilizado, lo que significa más de simultaneidad.

**Paso 3: Establecer ejecutor núcleos** – i/OS intensivas cargas de trabajo que no tienen operaciones complejas, es buena toostart con un alto número de núcleos de ejecutor tooincrease Hola tareas paralelas por ejecutor.  Establecer ejecutor núcleos too4 es un buen punto de partida.   

    executor-cores = 4
Aumentar Hola número de núcleos de ejecutor le proporcionará más paralelismo para que pueda experimentar con diferentes ejecutor-núcleos.  Para los trabajos que tienen operaciones más complejas, debería reducir el número de Hola de núcleos por ejecutor.  Si executor-cores se ha establecido en un número mayor que 4, puede que la recolección de elementos no utilizados sea ineficaz y el rendimiento se vea degradado.

**Paso 4: determine la cantidad de memoria YARN en el clúster**. Esta información está disponible en Ambari.  Navegue tooYARN y ver la ficha de configuraciones de Hola.  Hola memoria YARN se muestra en esta ventana.  
Nota: mientras estás en ventana hello, también puede ver tamaño de contenedor de hilo de hello predeterminado.  Hola tamaño de contenedor YARN es Hola igual a la memoria por cada parámetro de elemento de ejecución.

    Total YARN memory = nodes * YARN memory per node
**Paso 5: calcule num-executors**

**Calcular la restricción de memoria** -parámetro num ejecutor de hello está restringido por la memoria o CPU.  restricción de memoria de Hello viene determinado por la cantidad de Hola de memoria YARN disponible para la aplicación.  Tome la memoria total de YARN y divídala por la memoria del ejecutor.  restricción de Hello necesita toobe anular escalar para número de Hola de aplicaciones por lo que se divida por número de Hola de aplicaciones.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
**Calcular la restricción de CPU** -Hola restricción de CPU se calcula como Hola total núcleos virtuales divididos por el número de núcleos por ejecutor Hola.  Hay 2 núcleos virtuales para cada núcleo físico.  Restricción de memoria toohello similar, tenemos división por número de Hola de aplicaciones.

    virtual cores = (nodes in cluster * # of physical cores in node * 2)
    CPU constraint = (total virtual cores / # of cores per executor) / # of apps
**Establecer num ejecutor** : parámetro num ejecutor de hello se determina teniendo Hola mínimo de restricciones de memoria de Hola y Hola CPU. 

    num-executors = Min (total virtual Cores / # of cores per executor, available YARN memory / executor-memory)   
El hecho de establecer un número mayor de ejecutores no tiene por qué aumentar el rendimiento.  Debe tener en cuenta que al agregar más ejecutores pondrá una sobrecarga adicional a cada ejecutor que agregue, lo que podría reducir el rendimiento.  Ejecutor de NUM está limitado por los recursos de clúster de Hola.    

## <a name="example-calculation"></a>Cálculo de ejemplo

Supongamos que actualmente tiene un clúster compuesto de 8 nodos D4v2 ejecución 2 aplicaciones incluidas Hola que va toorun.  

**Paso 1: Determinar las aplicaciones se ejecutan en el clúster** – sabe que tiene 2 aplicaciones en el clúster, incluidos los Hola uno va toorun.  

**Paso 2: establezca executor-memory**. En este ejemplo, determinamos que 6 GB de memoria de ejecutor serán suficientes para trabajos con uso intensivo de E/S.  

    executor-memory = 6GB
**Paso 3: Establecer ejecutor núcleos** : puesto que se trata de un trabajo de uso intensivo de E/S, podemos establecer número de Hola de núcleos para cada too4 ejecutor.  Configuración de núcleos por toolarger ejecutor de 4 puede causar problemas de la colección de elementos no utilizados.  

    executor-cores = 4
**Paso 4: Determinar la cantidad de memoria YARN en clúster** – naveguemos tooAmbari toofind espera que cada D4v2 tiene 25 GB de memoria YARN.  Dado que hay 8 nodos, la memoria disponible de hilo de Hola se multiplica por 8.

    Total YARN memory = nodes * YARN memory* per node
    Total YARN memory = 8 nodes * 25GB = 200GB
**Paso 5: Calcular num ejecutor** : parámetro de ejecutor num hello viene determinado por tomar Hola mínima de memoria hello y restricción de CPU de hello dividido por hello n.º de aplicaciones que se ejecutan en Spark.    

**Calcular la restricción de memoria** : restricción de memoria de Hola se calcula como Hola hilo de memoria total dividida por la memoria de Hola por ejecutor.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
    Memory constraint = (200GB / 6GB) / 2   
    Memory constraint = 16 (rounded)
**Calcular la restricción de CPU** -Hola restricción de CPU se calcula como Hola núcleos yarn total divididos por el número de núcleos por ejecutor Hola.
    
    YARN cores = nodes in cluster * # of cores per node * 2   
    YARN cores = 8 nodes * 8 cores per D14 * 2 = 128
    CPU constraint = (total YARN cores / # of cores per executor) / # of apps
    CPU constraint = (128 / 4) / 2
    CPU constraint = 16
**Establezca num-executors**

    num-executors = Min (memory constraint, CPU constraint)
    num-executors = Min (16, 16)
    num-executors = 16    

