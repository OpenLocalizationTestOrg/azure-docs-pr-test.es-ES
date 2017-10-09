---
title: "notas de la versión de aaaArchived - componentes de Hadoop en HDInsight de Azure | Documentos de Microsoft"
description: "Notas de la versión archivadas de las versiones anteriores de los componentes de Hadoop para Azure HDInsight."
services: hdinsight
documentationcenter: 
editor: cgronlun
manager: jhubbard
author: nitinme
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 7a99c77f4557ca8c1dabe924cc67b2e0a134f8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-archive-for-hadoop-components-on-azure-hdinsight"></a>Notas de la versión (en archivo) de los componentes de Hadoop en Azure HDInsight

Este artículo proporciona información acerca de hello **anterior** actualizaciones de versión de HDInsight de Azure. Para obtener información sobre versiones más recientes, consulte las [notas de la versión de HDInsight](hdinsight-release-notes.md).

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Para obtener más información, consulte el [artículo de control de versiones de HDInsight](hdinsight-component-versioning.md).



## <a name="notes-for-08302016-release-of-hdinsight"></a>Notas de la versión del 30/08/2016 de HDInsight
números de versión completa de Hola para clústeres de HDInsight basados en Linux se implementan con esta versión:

| HDI | Versión del clúster de HDI | HDP | Compilación de HDP | Compilación de Ambari |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8268980 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8268980 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8269383 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

números de versión completa de Hola para clústeres de HDInsight basados en Windows se implementan con esta versión:

| HDI | Versión del clúster de HDI | HDP | Compilación de HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1033.2559206 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1033.2559206 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1033.2559206 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1033.2559206 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1033.2559206 |2.3 |2.3.3.1-25 |


## <a name="08172016---release-of-r-server-on-hdinsight"></a>Notas de la versión de 17/08/2016 para R Server en HDInsight
* R Server 8.0.5: básicamente, una versión con corrección de errores. Vea hello [R notas de la versión de servidor](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes) para obtener más información.
* Paquete de aprendizaje automático de Azure en el nodo del borde hello - [este paquete de R](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) habilita R modelos toobe publica y consume como un servicio web de aprendizaje automático de Azure.  Vea hello ["Poner un modelo"](hdinsight-hadoop-r-server-overview.md#operationalize-a-model) sección de nuestro ["Información general de R Server en HDInsight"](hdinsight-hadoop-r-server-overview.md) artículo para obtener más información.
* Dependencias de Linux de hello [top 100 paquetes de R más populares](https://github.com/metacran/cranlogs) -estas dependencias del paquete Linux ya están instaladas previamente.
* Repositorio CRAN de Hola de opción toouse al agregar R paquetes toohello los nodos de datos. Para más información, vea [Introducción al uso de R Server en HDInsight](hdinsight-hadoop-r-server-get-started.md).
* Confiabilidad de hello mejorada de aprovisionamiento del servidor de R cuando se crean los clústeres.

## <a name="notes-for-08012016-release-of-hdinsight"></a>Notas de la versión del 08/01/2016 de HDInsight
números de versión completa de Hola para clústeres de HDInsight basados en Linux se implementan con esta versión:

| HDI | Versión del clúster de HDI | HDP | Compilación de HDP | Compilación de Ambari |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8028416 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8028416 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8053402 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

números de versión completa de Hola para clústeres de HDInsight basados en Windows se implementan con esta versión:

| HDI | Versión del clúster de HDI | HDP | Compilación de HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1005.2488842 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1005.2488842 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1005.2488842 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1005.2488842 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1005.2488842 |2.3 |2.3.3.1-25 |

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Spark, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| Clústeres de tooHDInsight 3.4 de cambios |se cambian los valores predeterminados de Hola para las siguientes configuraciones de hive para mejorar el rendimiento <ul><li>`hive.vectorized.execution.reduce.enabled=true`</li><li>`hive.tez.min.partition.factor=1f`</li><li>`hive.tez.max.partition.factor=3f`</li><li>`tez.shuffle-vertex-manager.min-src-fraction=0.9`</li><li>`tez.shuffle-vertex-manager.max-src-fraction=0.95`</li><li>`tez.runtime.shuffle.connect.timeout= 30000`</li></ul> |Servicio |Todo |N/D |
| Las siguientes correcciones están incluidas en esta versión: |HIVE-13632, HIVE-12897,HIVE-12907,HIVE-12908,HIVE-12988,HIVE-13510,HIVE-13572,HIVE-13716,HIVE-13726,HIVE-12505,HIVE-13632,HIVE-13661,HIVE-13705,HIVE-13743,HIVE-13810,HIVE-13857,HIVE-13902,HIVE-13911,HIVE-13933 |Servicio |Todo |N/D |

## <a name="notes-for-07142016-release-of-hdinsight"></a>Notas de la versión del 14/07/2016 de HDInsight
números de versión completa de Hola para clústeres de HDInsight basados en Linux se implementan con esta versión:

| HDI | Versión del clúster de HDI | HDP | Compilación de HDP | Compilación de Ambari |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7932505 |2.2 |2.2.9.1-11 |2.2.1.12-2 |
| 3.3 |3.3.1000.0.7932505 |2.3 |2.3.3.1-18 |2.2.1.12-2 |
| 3.4 |3.4.1000.0.7933003 |2.4 |2.4.2.0 |2.2.1.12-2 |

números de versión completa de Hola para clústeres de HDInsight basados en Windows se implementan con esta versión:

| HDI | Versión del clúster de HDI | HDP | Compilación de HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.989.2441725 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.989.2441725 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.989.2441725 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.989.2441725 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.989.2441725 |2.3 |2.3.3.1-21 |

## <a name="notes-for-07072016-release-of-hdinsight"></a>Notas de la versión del 07/07/2016 de HDinsight
números de versión completa de Hola para clústeres de HDInsight basados en Linux se implementan con esta versión:

| HDI | Versión del clúster de HDI | HDP | Compilación de HDP |
| --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7864996 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.1000.0.7864996 |2.3 |2.3.3.1-18 |
| 3.4 |3.4.1000.0.7861906 |2.4 |2.4.2.0 |

números de versión completa de Hola para clústeres de HDInsight basados en Windows se implementan con esta versión:

| HDI | Versión del clúster de HDI | HDP | Compilación de HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.977.2413853 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.977.2413853 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.977.2413853 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.977.2413853 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.977.2413853 |2.3 |2.3.3.1-21 |

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Spark, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| [Herramientas de HDInsight para IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md) |El complemento de IntelliJ IDEA para clústeres de HDInsight Spark está integrado ahora con el Kit de herramientas de Azure para IntelliJ. Esta es compatible con Azure SDK v2.9.1, SDK de Java más reciente e incluye todas las características de Hola Hola Standalone HDInsight Plugin para IntelliJ. |Herramientas |Spark |N/D |
| [Herramientas de HDInsight para Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md) |El Kit de herramientas de Azure para Eclipse ahora es compatible con clústeres de HDInsight Spark. Permite Hola siguientes características: <ul><li>Crear y escribir una aplicación Spark fácilmente en Scala y Java con compatibilidad de creación de primer nivel con IntelliSense, formato automático, comprobación de errores, etc.</li><li>Probar la aplicación localmente de hello Spark.</li><li>Enviar grupo de trabajos tooHDInsight Spark y recuperar resultados de Hola.</li><li>Inicie sesión en tooAzure y tener acceso a todos los clústeres de Spark Hola asociados con las suscripciones de Azure.</li><li>Navegar por todos los recursos de almacenamiento de hello asociado de su clúster de HDInsight Spark.</li></ul> |Herramientas |Spark |N/D |

A partir de esta versión, hemos cambiado directiva de aplicación de revisión de SO de invitado y Hola para clústeres de HDInsight basados en Linux. objetivo de Hola de nueva directiva de hello es toosignificantly reducir el número de Hola de reinicios toopatching due. Hola nueva directiva revisiones máquinas virtuales (VM en Linux) agrupa todos los lunes o el jueves a partir de 12.00 UTC de forma escalonada en nodos cualquier clúster determinado. Sin embargo, cualquier máquina virtual determinada sólo se reinicia a lo sumo una vez cada 30 días debido a la aplicación de revisiones tooguest OS. Además, Hola reiniciar por primera vez para un clúster recién creado no se produce antes de 30 días a partir de la fecha de creación de clúster de Hola.

> [!NOTE]
> Estos cambios aplican solo toonewly creado clústeres igual o mayor que esta versión de lanzamiento.
>
>

## <a name="notes-for-06062016-release-of-hdinsight"></a>Notas de la versión del 06/06/2016 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

| HDP | Versión de HDI | Versión de Spark | Número de compilación de Ambari | Número de compilación de HDP |
| --- | --- | --- | --- | --- |
| 2.3 |3.3.1000.0.7702215 |1.5.2 |2.2.1.8-2 |2.3.3.1-18 |
| 2.4 |3.4.1000.0.7702224 |1.6.1 |2.2.1.8-2 |2.4.2.0 |

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Spark, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| Spark en HDInsight está disponible con carácter general |Esta versión ofrece mejoras de disponibilidad, escalabilidad y origen de la productividad tooopen Apache Spark en HDInsight. <ul><li>Un Acuerdo de Nivel de Servicio de disponibilidad líder del sector de un 99,9 %, adecuado para cargas de trabajo empresariales exigentes.</li><li>Capa de almacenamiento escalable mediante Azure Data Lake Store.</li><li>Herramientas de productividad en cada fase de la exploración y el desarrollo de los datos. Los cuadernos de Jupyter Notebook con el kernel Spark personalizado permiten la exploración interactiva de los datos, la integración con paneles de BI, como Power BI, Tableau y Qlik, resulta adecuada para compartir datos rápidamente y la creación continua de informes y el complemento IntelliJ es la opción en la que se puede confiar para el desarrollo y la depuración de artefactos de código a largo plazo.</li></ul> |Servicio |Spark |N/D |
| Herramientas de HDInsight para IntelliJ |Se trata de un complemento IntelliJ IDEA para clústeres HDInsight Spark, Permite Hola siguientes características:<ul><li>Crear y escribir una aplicación Spark fácilmente en Scala y Java con compatibilidad de creación de primer nivel con IntelliSense, formato automático, comprobación de errores, etc.</li><li>Probar la aplicación localmente de hello Spark.</li><li>Enviar grupo de trabajos tooHDInsight Spark y recuperar resultados de Hola.</li><li>Inicie sesión en tooAzure y tener acceso a todos los clústeres de Spark Hola asociados con las suscripciones de Azure.</li><li>Navegar por todos los recursos de almacenamiento de hello asociado de su clúster de HDInsight Spark.</li><li>Navegar por todos los Hola historial y trabajo de información de los trabajos para el clúster de HDInsight Spark.</li><li>Depurar los trabajos de Spark remotamente desde el equipo de escritorio.</li></ul> |Herramientas |Spark |N/D |

## <a name="notes-for-05132016-release-of-hdinsight"></a>Notas de la versión del 13/05/2016 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight (Windows) 2.1.10.875.2159884 (HDP 1.3.12.0-01795 - sin cambios)
* HDInsight (Windows) 3.0.6.875.2159884 (HDP 2.0.13.0-2117 - sin cambios)
* HDInsight (Windows)       3.1.4.922.2266903  (HDP 2.1.15.0-2374, sin cambios)
* HDInsight (Windows) 3.2.7.922.2266903  (HDP 2.2.9.1-11)
* HDInsight (Windows)        3.3.0.922.2266903  (HDP 2.3.3.1-18)
* HDInsight (Linux) 3.2.1000.0.7565644 (HDP 2.2.9.1-11)
* HDInsight (Linux) 3.3.1000.0.7565644 (HDP 2.3.3.1-18)
* HDInsight (Linux) 3.4.1000.0.7548380 (HDP 2.4.2.0)

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Spark, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| Actualización de la versión de Spark y otras correcciones de errores |Esta versión actualiza la versión de Hola Spark en HDInsight clúster too1.6.1 y corrige otros errores |Servicio |Spark |N/D |

## <a name="notes-for-04112016-release-of-hdinsight"></a>Notas de la versión del 11/04/2016 de HDInsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight (Windows) 2.1.10.889.2191206 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight (Windows) 3.0.6.889.2191206 (HDP 2.0.13.0-2117, sin cambios)
* HDInsight (Windows) 3.1.4.889.2191206 (HDP 2.1.15.0-2374, sin cambios)
* HDInsight (Windows) 3.2.7.889.2191206 (HDP 2.2.9.1-10)
* HDInsight (Windows) 3.3.0.889.2191206 (HDP 2.3.3.1-16, sin cambios)
* HDInsight (Linux) 3.2.1000.0.7339916 (HDP 2.2.9.1-10)
* HDInsight (Linux) 3.3.1000.0.7339916 (HDP 2.3.3.1-16)
* HDInsight (Linux) 3.4.1000.0.7338911 (HDP 2.4.1.1-3)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| Problemas de actualización de la tienda de metadatos personalizada de HDI 3.4 |Si utilizó una tienda de metadatos personalizada, que se utilizó antes en una versión anterior de otro clúster de HDInsight, se produciría un error en el proceso de creación del clúster. Esto fue debido a error del script de actualización tooan que ya se han corregido |Creación de clústeres |Todo |N/D |
| Recuperación tras bloqueo de Livy |Proporciona resistencia de estado de trabajos en todos los trabajos que se envíen a través de Livy. |Confiabilidad |Spark en Linux |N/D |
| Contenido de Jupyter (alta disponibilidad) |Proporciona Hola capacidad toosave y carga Jupyter notebook contenido tooand de hello cuenta de almacenamiento asociada con el clúster de Hola. Para obtener más información, consulte [Kernels disponibles para cuadernos de Jupyter con clústeres Spark en HDInsight basados en Linux en HDInsight (versión preliminar)](hdinsight-apache-spark-jupyter-notebook-kernels.md). |Cuadernos |Spark en Linux |N/D |
| Eliminación de hiveContext en cuadernos de Jupyter Notebook |Use la instrucción mágica `%%sql` en lugar de `%%hive`. SqlContext es toohiveContext equivalente. Para obtener más información, consulte [Kernels disponibles para cuadernos de Jupyter con clústeres Spark en HDInsight basados en Linux en HDInsight (versión preliminar)](hdinsight-apache-spark-jupyter-notebook-kernels.md) |Cuadernos |Clústeres de Spark en Linux |N/D |
| Degradación de las versiones anteriores de Spark |Versión anterior Spark 1.3.1 se quitó de servicio de hello en 31/5 |Servicio |Clústeres de Spark en Windows |N/D |

## <a name="notes-for-03292016-release-of-hdinsight"></a>Notas de la versión del 29/03/2016 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight (Windows) 2.1.10.875.2159884 (HDP 1.3.12.0-01795 - sin cambios)
* HDInsight (Windows) 3.0.6.875.2159884 (HDP 2.0.13.0-2117 - sin cambios)
* HDInsight (Windows) 3.1.4.875.2159884 (HDP 2.1.15.0-2374, sin cambios)
* HDInsight (Windows) 3.2.7.875.2159884 (HDP 2.2.9.1-7, sin cambios)
* HDInsight (Windows) 3.3.0.875.2159884 (HDP 2.3.3.1-16)
* HDInsight (Linux) 3.2.1000.0.7193255 (HDP 2.2.9.1-8, sin cambios)
* HDInsight (Linux) 3.3.1000.0.7193255 (HDP 2.3.3.1-7, sin cambios)
* HDInsight (Linux) 3.4.1000.0.7195842 (HDP 2.4.1.0-327)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| Se ha agregado la versión HDInsight 3.4 y se han actualizado las versiones HDP en todos los clústeres de HDInsight |En esta versión, se ha agregado HDInsight v3.4 (basado en HDP 2.4) y se han actualizado otras versiones de HDP. Las notas de la versión HDP 2.4 están disponibles [aquí ](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html)y se puede encontrar más información sobre las versiones de HDInsight [aquí](hdinsight-component-versioning.md). |Servicio |Todos los clústeres de Linux |N/D |
| HDInsight Premium |Ahora, HDInsight está disponible en dos categorías: Standard y Premium. Actualmente, HDInsight Premium se encuentra en versión preliminar y solo está disponible para los clústeres de Hadoop y Spark en Linux. Para más información, consulte [esta página](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium). |Servicio |Hadoop y Spark en Linux |N/D |
| Microsoft R Server |HDInsight Premium proporciona Microsoft R Server, que puede incluirse con los clústeres de Hadoop y Spark de Linux. Para más información, vea [Introducción a las funcionalidades de R de código abierto de R Server en HDInsight](hdinsight-hadoop-r-server-overview.md). |Servicio |Hadoop y Spark en Linux |N/D |
| Spark 1.6.0 |Ahora, los clústeres de HDInsight 3.4 incluyen Spark 1.6.0 |Servicio |Clústeres de Spark en Linux |N/D |
| Mejoras de Jupyter Notebook |Ahora, Jupyter Notebooks, disponible con los clústeres de Spark, proporciona kernels de Spark adicionales. También incluye mejoras como el uso de la visualización automática %%mágica y la integración con las bibliotecas de visualización de Python (como matplotlib). Para obtener más información, consulte [Kernels disponibles para cuadernos de Jupyter con clústeres Spark en HDInsight basados en Linux en HDInsight (versión preliminar)](hdinsight-apache-spark-jupyter-notebook-kernels.md). |Servicio |Clústeres de Spark en Linux |N/D |

## <a name="notes-for-03222016-release-of-hdinsight"></a>Notas de la versión del 22/03/2016 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight (Windows) 2.1.10.875.2159884 (HDP 1.3.12.0-01795 - sin cambios)
* HDInsight (Windows) 3.0.6.875.2159884 (HDP 2.0.13.0-2117 - sin cambios)
* HDInsight (Windows) 3.1.4.875.2159884 (HDP 2.1.15.0-2374, sin cambios)
* HDInsight (Windows) 3.2.7.875.2159884 (HDP 2.2.9.1-7, sin cambios)
* HDInsight (Windows) 3.3.0.875.2159884 (HDP 2.3.3.1-16)
* HDInsight (Linux) 3.2.1000.0.7193255 (HDP 2.2.9.1-8, sin cambios)
* HDInsight (Linux) 3.3.1000.0.7193255 (HDP 2.3.3.1-7, sin cambios)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| Versiones actualizadas de HDInsight para todos los clústeres de HDInsight |Con esta versión, hemos actualizado las versiones de HDInsight para todos los clústeres de HDInsight. |Servicio |Todo |N/D |

## <a name="notes-for-03102016-release-of-hdinsight"></a>Notas de la versión del 10/03/2016 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight (Windows) 2.1.10.859.2123216 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight (Windows) 3.0.6.859.2123216 (HDP 2.0.13.0-2117, sin cambios)
* HDInsight (Windows) 3.1.4.859.2123216 (HDP 2.1.15.0-2374, sin cambios)
* HDInsight (Windows) 3.2.7.859.2123216 (HDP 2.2.9.1-7)
* HDInsight (Windows) 3.3.0.859.2123216 (HDP 2.3.3.1-5, sin cambios)
* HDInsight (Linux) 3.2.1000.7076817 (HDP 2.2.9.1-8)
* HDInsight (Linux) 3.3.1000.7076817 (HDP 2.3.3.1-7)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| Versiones actualizadas de HDInsight para todos los clústeres de HDInsight |Con esta versión, hemos actualizado las versiones de HDInsight para todos los clústeres de HDInsight. |Servicio |Todo |N/D |

## <a name="notes-for-01272016-release-of-hdinsight"></a>Notas de la versión del 27/01/2016 de HDInsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight (Windows) 2.1.10.817.2028315 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight (Windows) 3.0.6.817.2028315 (HDP 2.0.13.0-2117, sin cambios)
* HDInsight (Windows) 3.1.4.817.2028315 (HDP 2.1.15.0-2374, sin cambios)
* HDInsight (Windows) 3.2.7.817.2028315 (HDP 2.2.9.1-1)
* HDInsight (Windows) 3.3.0.817.2028315 (HDP 2.3.3.1-5, sin cambios)
* HDInsight (Linux) 3.2.1000.4072335 (HDP 2.2.9.1-1)
* HDInsight (Linux) 3.3.1000.4072335 (HDP 2.3.3.1-1)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| Versiones actualizadas de HDInsight para todos los clústeres de HDInsight |Con esta versión, hemos actualizado las versiones de HDInsight para todos los clústeres de HDInsight. |Servicio |Todo |N/D |

## <a name="notes-for-12022015-release-of-hdinsight"></a>Notas de la versión del 02/12/2015 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight (Windows) 2.1.10.763.1931434 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight (Windows) 3.0.6.763.1931434 (HDP 2.0.13.0-2117, sin cambios)
* HDInsight (Windows) 3.1.4.763.1931434 (HDP 2.1.15.0-2374, sin cambios)
* HDInsight (Windows) 3.2.7.763.1931434 (HDP 2.2.7.1-34, sin cambios)
* HDInsight (Windows) 3.3.1000.0 (HDP 2.3.3.1-5)
* HDInsight (Linux) 3.2.1000.0.6392801 (HDP 2.2.7.1-34, sin cambios)
* HDInsight (Linux) 3.3.1000.0 (HDP 2.3.3.0-3039)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| Se ha agregado la versión HDInsight 3.3 y se han actualizado las versiones HDP en todos los clústeres de HDInsight |Con esta versión, se ha agregado HDInsight v3.3 (basada en HDP 2.3) y también se han actualizado otras versiones de HDP. Las notas de la versión HDP 2.3 están disponibles [aquí ](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html)y se puede encontrar más información sobre las versiones de HDInsight [aquí](hdinsight-component-versioning.md). |Servicio |Todo |N/D |

## <a name="notes-for-11302015-release-of-hdinsight"></a>Notas de la versión del 30/11/2015 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight (Windows) 2.1.10.757.1923908 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight (Windows) 3.0.6.757.1923908 (HDP 2.0.13.0-2117, sin cambios)
* HDInsight (Windows) 3.1.4.757.1923908 (HDP 2.1.15.0-2374, sin cambios)
* HDInsight (Windows) 3.2.7.757.1923908 (HDP 2.2.7.1-34)
* HDInsight (Linux) 3.2.1000.0.6392801 (HDP 2.2.7.1-34)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| Versiones de HDInsight actualizadas para todos los clústeres de HDInsight y versiones HDP para clústeres de HDInsight 3.2 (Windows y Linux) |Con esta versión, se han actualizado las versiones de HDInsight y HDP |Servicio |Todo |N/D |

## <a name="notes-for-10272015-release-of-hdinsight"></a>Notas de la versión del 27/10/2015 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight (Windows) 2.1.10.726.1866228 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight (Windows) 3.0.6.726.1866228 (HDP 2.0.13.0-2117, sin cambios)
* HDInsight (Windows) 3.1.4.726.1866228 (HDP 2.1.15.0-2374, sin cambios)
* HDInsight (Windows) 3.2.7.726.1866228 (HDP 2.2.7.1-33)
* HDInsight (Linux) 3.2.1000.0.6035701 (HDP 2.2.7.1-33)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| Versiones actualizadas de HDInsight para todos los clústeres de HDInsight (Windows y Linux) |Con esta versión, se han actualizado las versiones de HDInsight y HDP |Servicio |Todo |N/D |
| Se han corregido los clústeres de Jupyter para Windows Spark con clústeres escritos en letras mayúsculas |Clústeres que tenían los nombres DNS especificados en letras mayúsculas tenían problemas con equipos portátiles Jupyter debido tooan comprobación de solicitudes de origen. corrección de Hello era el nombre DNS de Hola de toochange en caso de toolower de configuración de Jupyter. |Servicio |HDInsight Spark (Windows) |N/D |

## <a name="notes-for-10202015-release-of-hdinsight"></a>Notas de la versión del 20/10/2015 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight     2.1.10.716.1846990 (Windows)    (HDP 1.3.12.0-01795, sin cambios)
* HDInsight 3.0.6.716.1846990 (Windows) (HDP 2.0.13.0-2117, sin cambios)
* HDInsight 3.1.4.716.1846990 (Windows) (HDP 2.1.16.0-2374)
* HDInsight 3.2.7.716.1846990 (Windows) (HDP 2.2.7.1-0004)
* HDInsight 3.2.1000.0.5930166 (Linux) (HDP 2.2.7.1-0004)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| De forma predeterminada HDP versión cambiado tooHDP 2.2 |versión de Hola predeterminada para los clústeres de HDInsight Windows es tooHDP modificado 2.2. HDInsight versión 3.2 (HDP 2.2) ha estado disponible con carácter general desde febrero de 2015. Este cambio solo voltea la versión de clúster de Hola de forma predeterminada, cuando una selección explícita no se ha realizado al aprovisionar el clúster de hello mediante Hola portal de Azure, cmdlets de PowerShell u Hola SDK. |Servicio |Todo |N/D |
| Cambios en el formato de nombre de máquina virtual para la implementación de múltiples clústeres de HDInsight en Linux en una red virtual única |En esta versión se agrega compatibilidad para implementar varios clústeres de Linux de HDInsight en una red virtual única. Como parte de la actualización, el formato de Hola de nombres de máquina virtual en clúster de hello ha cambiado desde el nodo principal\*, workernode\* y zookeepernode\* toohn\*, wn\*y zk\* respectivamente. No es un tootake de práctica recomendada una dependencia directa con formato de Hola de nombres de máquina virtual, ya que esto es toochange de asunto. Usar "nombre de host -f" en el equipo local de Hola o una lista de Hola de toodetermine Ambari APIs de hosts y asignación de Hola de componentes toohosts. Encontrará más información en [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md) y [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md). |Servicio |Clústeres de HDInsight en Linux |N/D |
| Cambios en la configuración |Para los clústeres de HDInsight 3.1, Hola siguiendo configuraciones está habilitado: <ul><li>tez.yarn.ats.enabled y yarn.log.server.url. Esto permite hello servidor de aplicaciones de escala de tiempo y Hola registro servidor toobe puede tooserve los registros.</li></ul>Para los clústeres de HDInsight 3.2, se han modificado Hola siguiendo configuraciones: <ul><li>se ha establecido MapReduce.fileoutputcommitter.Algorithm.Version too2. Esto habilita el uso de versión de V2 Hola de hello FileOutputCommitter.</li></ul> |Servicio |Todo |N/D |

## <a name="notes-for-09092015-release-of-hdinsight"></a>Notas de la versión del 09/09/2015 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight     2.1.10.675.1768697 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight     3.0.6.675.1768697  (HDP 2.0.13.0-2117, sin cambios)
* HDInsight     3.1.4.675.1768697  (HDP 2.1.15.0-2334, sin cambios)
* HDInsight 3.2.6.675.1768697 (HDP 2.2.6.1-0012, sin cambios)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| Versiones actualizadas de HDInsight para todos los clústeres de HDInsight |Con esta versión, se han actualizado las versiones de HDInsight |Servicio |Todo |N/D |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Notas de la versión del 31/07/2015 de HDInsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight     2.1.10.640.1695824 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight     3.0.6.640.1695824  (HDP 2.0.13.0-2117, sin cambios)
* HDInsight     3.1.4.640.1695824  (HDP 2.1.15.0-2334, sin cambios)
* HDInsight 3.2.6.640.1695824 (HDP 2.2.6.1-0012, sin cambios)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| Corregir flujo de trabajo de creación de imagen del nodo de clúster Spark |Se ha corregido un error que causaba Spark toonot recuperar después de restablecer la imagen inicial de nodos de clúster |Servicio |Spark |N/D |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Notas de la versión del 31/07/2015 de HDInsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight     2.1.10.635.1684502 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight     3.0.6.635.1684502  (HDP 2.0.13.0-2117, sin cambios)
* HDInsight     3.1.4.635.1684502  (HDP 2.1.15.0-2334, sin cambios)
* HDInsight 3.2.6.635.1684502 (HDP 2.2.6.1-0012, sin cambios)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| Versiones actualizadas de HDInsight para todos los clústeres de HDInsight |Con esta versión, se han actualizado las versiones de HDInsight |Servicio |Todo |N/D |

## <a name="notes-for-07072015-release-of-hdinsight"></a>Notas de la versión del 07/07/2015 de HDInsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 2.1.10.610.1630216 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight 3.0.6.610.1630216 (HDP 2.0.13.0-2117, sin cambios)
* HDInsight 3.1.4.610.1630216 (HDP 2.1.15.0-2334, sin cambios)
* HDInsight 3.2.4.610.1630216 (HDP 2.2.6.1-0012)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

| Título | Description | Área afectada (por ejemplo, servicio, componente o SDK) | Tipo de clúster (por ejemplo, Hadoop, HBase o Storm) | JIRA (si es aplicable) |
| --- | --- | --- | --- | --- |
| Versiones actualizadas de HDP para clústeres de HDInsight 3.2 |Con esta versión, HDInsight 3.2 implementa HDP 2.2.6.1-0012 |Servicio |Todo |N/D |

## <a name="notes-for-06262015-release-of-hdinsight"></a>Notas de la versión del 06/26/2015 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 2.1.10.601.1610731 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight 3.0.6.601.1610731 (HDP 2.0.13.0-2117, sin cambios)
* HDInsight 3.1.4.601.1610731 (HDP 2.1.15.0-2334, sin cambios)
* HDInsight 3.2.4.601.1610731 (HDP 2.2.6.1-0011)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Área afectada (por ejemplo, servicio, componente o SDK)</p></th>
<th>Tipo de clúster (por ejemplo, Hadoop, HBase o Storm)</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>Versiones actualizadas de HDP para clústeres de HDInsight 3.2</td>
<td>Con esta versión HDInsight 3.2 implementa HDP 2.2.6.1</td>
<td>Servicio</td>
<td>Todo</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-06182015-release-of-hdinsight"></a>Notas de la versión del 18/06/2015 de HDInsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 2.1.10.596.1601657 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight 3.0.6.596.1601657 (HDP 2.0.13.0-2117, sin cambios)
* HDInsight 3.1.4.596.1601657 (HDP 2.1.15.0-2334)
* HDInsight 3.2.4.596.1601657 (HDP 2.2.6.1-0002)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Área afectada (por ejemplo, servicio, componente o SDK)</p></th>
<th>Tipo de clúster (por ejemplo, Hadoop, HBase o Storm)</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>Puertos HTTPS adicionales abiertos</td>
<td>servicio de nube de Hello ahora abre 5 too8005 8001 puertos en el clúster de hello p. ej. en https://<clustername>.azurehdinsight.net:8001/. Las solicitudes de direcciones URL toothese se autentican utilizando Hola mismo mecanismo de contraseña de la autenticación básica como el puerto 443. Estos puertos enlazan toohello mismo número de puerto en el nodo principal activo de Hola. Las acciones de script pueden ser utilizados toomake cliente servicios escuchar en estos puertos en el clúster de Hola de toooutside de nodo principal y ruta Hola.</td>
<td>Servicio en la nube</td>
<td>Todo</td>
<td>N/D</td>
</tr>
<tr>
<td>Problema de orden aleatorio intermitente de MapReduce para HDInsight 3.2</td>
<td>Corrección de una condición de carrera poco frecuente e intermitente en orden aleatorio de MapReduce en clústeres grandes que provocaban errores de tareas ocasionales. Consulte <a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a> para más información.</td>
<td>Núcleo de Hadoop</td>
<td>Todo</td>
<td><a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a></td>
</tr>
<tr>
<td>Mover tooLatest 2.2 del SDK de Java de Azure para 3.2 de HDInsight</td>
<td>Mover toolatest versión de hello Azure SDK para Java utilizada hello WASB controlador. Hello SDK más reciente tiene algunas correcciones y notas de la versión de Hola para hello mismo están disponible en https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt.</td>
<td>Núcleo de Hadoop</td>
<td>Todo</td>
<td><a href="https://issues.apache.org/jira/browse/HADOOP-11959" target="_blank">HADOOP-11959</a></td>
</tr>
<tr>
<td>Mover tooHDP 2.1.15 para clústeres de HDInsight 3.1</td>
<td>Notas de la versión de Hortonworks versión Hola están disponibles <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.15-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.15.html" target="_blank">aquí</a>.</td>
<td>HDP</td>
<td>Todo</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-06042015-release-of-hdinsight"></a>Notas de la versión del 04/06/2015 de HDInsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 2.1.10.583.1575584 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight 3.0.6.583.1575584  (HDP 2.0.13.0-2117, sin cambios)
* HDInsight 3.1.3.583.1575584 (HDP 2.1.12.1-0003, sin cambios)
* HDInsight 3.2.4.583.1575584 (HDP 2.2.6.1-1)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Área afectada (por ejemplo, servicio, componente o SDK)</p></th>
<th>Tipo de clúster (por ejemplo, Hadoop, HBase o Storm)</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>Corrección para el error 502 de puerta de enlace incorrecta de los clústeres de Storm</td>
<td>Esta versión corrige un error que afecta a la API de envío de trabajo de Hola que produjo toobe del sitio Web de hello hacia abajo tras un reinicio.</td>
<td>Servicio</td>
<td>Storm</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-06012015-release-of-hdinsight"></a>Notas de la versión del 01/06/2015 de HDInsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 2.1.10.577.1563827 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight 3.0.6.577.1563827 (HDP 2.0.13.0-2117, sin cambios)
* HDInsight 3.1.3.577.1563827 (HDP 2.1.12.1-0003, sin cambios)
* HDInsight 3.2.4.577.1563827 (HDP 2.2.6.0-2800, sin cambios)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Área afectada (por ejemplo, servicio, componente o SDK)</p></th>
<th>Tipo de clúster (por ejemplo, Hadoop, HBase o Storm)</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>Varias correcciones de errores</td>
<td>Esta versión corrige los errores relacionados con el aprovisionamiento de toocluster.</td>
<td>Servicio</td>
<td>Todos los tipos de clúster</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-05272015-release-of-hdinsight"></a>Notas de la versión del 27/05/2015 de HDInsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 3.2.4.570.1554102 (HDP 2.2.6.0-2800)
* Las otras versiones de clúster y el SDK no se implementan como parte de esta versión.

Esta versión contiene Hola siguientes actualizaciones:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Área afectada (por ejemplo, servicio, componente o SDK)</p></th>
<th>Tipo de clúster (por ejemplo, Hadoop, HBase o Storm)</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>Actualización de HDP 2.2</td>
<td>Esta versión de HDInsight 3.2 contiene HDP 2.2.6 y aporta varias tooHDInsight de correcciones de errores importantes. Hello notas de la versión completa están disponibles en <a href="http://dev.hortonworks.com.s3.amazonaws.com/HDPDocuments/HDP2/HDP-2.2.6/HDP_RelNotes_v226/index.html">HDP 2.2.6 notas de la versión</a>.</td>
<td>HDP</td>
<td>Todos los tipos de clúster</td>
<td>N/D</td>
</tr>
<tr>
<td>Cambiar configuración de memoria del contenedor de Yarn tooDefault</td>
<td>En esta actualización, contenedores de tooYARN de memoria disponible de hello predeterminados (yarn.nodemanager.resource.memory mb y yarn.scheduler.maximum-asignación-mb), iniciado por el Administrador de nodo, es too5632MB mayor. Anteriormente, se trataba too4608MB reducida, pero basándose en varias ejecuciones de los trabajos, valor nuevo de hello debe ofrecer una mejor confiabilidad y rendimiento toomost trabajos, por lo que es el valor predeterminado es mejor. Como es habitual, si tiene una dependencia fundamental en esta configuración de memoria, establecer de forma explícita al crear el clúster de Hola.</td>
<td>HDP</td>
<td>Todos los tipos de clúster</td>
<td>N/D</td>
</tr>
<tr>
<td>Paridad de configuración predeterminada para los clústeres de HBase y Storm</td>
<td>Esta actualización restaura Hbase y aluvión de clústeres toouse Hola los mismos valores de configuración YARN como clústeres de Hadoop. Esto se hace por motivos de paridad en todos los tipos de clúster.</td>
<td>HDP</td>
<td>HBase, Storm</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-05202015-release-of-hdinsight"></a>Notas de la versión del 20/05/2015 de HDInsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 2.1.10.564.1542093 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight 3.0.6.564.1542093 (HDP 2.0.13.0-2117, sin cambios)
* HDInsight 3.1.3.564.1542093 (HDP 2.1.12.1-0003)
* HDInsight 3.2.4.564.1542093 (HDP 2.2.4.6-2)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Área afectada (por ejemplo, servicio, componente o SDK)</p></th>
<th>Tipo de clúster (por ejemplo, Hadoop, HBase o Storm)</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>Soporte de EventHub de SCP.NET</td>
<td>paquetes de clúster de Hello actualizado para HDInsight Storm ponga tooSCP.NET nuevas características. Ahora tienes acceso toonew API en el generador de topología que hacen que sea más fácil toouse EventHubSpout o Spouts de Java. Debe actualizar su toowork SDK de cliente SCP.NET con nuevos clústeres como contratos de Hola se han actualizado. Para obtener más información sobre Hola nuevas notas de API, el uso y la versión (incluidas correcciones de errores) consulte toohello archivo Léame incluido en el paquete NuGet SCP.NET Hola.</td>
<td>Herramientas de VS</td>
<td>Clústeres de Storm en HDInsight 3.2</td>
<td>N/D</td>
</tr>
<tr>
<td>Actualización de JDBC Driver</td>
<td>Hola actualizada controlador toohello SQL Server en sqljdbc_4.1.5605.100 una versión compatible.</td>
<td>Tienda de metadatos</td>
<td>Todo</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-04272015-release-of-hdinsight"></a>Notas de la versión del 27/04/2015 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 2.1.10.537.1486660 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight 3.0.6.537.1486660 (HDP 2.0.13.0-2117, sin cambios)
* HDInsight 3.1.3.537.1486660 (HDP 2.1.12.0-2329, sin cambios)
* HDInsight 3.2.3.537.1486660 (HDP 2.2.2.2-4)
* SDK 1.5.8

Esta versión contiene Hola siguientes actualizaciones:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Área afectada (por ejemplo, servicio, componente o SDK)</p></th>
<th>Tipo de clúster (por ejemplo, Hadoop, HBase o Storm)</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>Corregir la dependencia de DLL</td>
<td>Quita la dependencia de HDInsight en el marco de pruebas unitarias.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Corrección de errores para la condición de carrera</td>
<td>Un clúster crear solicitud ahora esperas de PUT solicitar toobe aceptado antes de sondeo de estado de Hola</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-04142015-release-of-hdinsight"></a>Notas de la versión del 14/04/2015 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 2.1.10.521.1453250 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight 3.0.6.521.1453250 (HDP 2.0.13.0-2117, sin cambios)
* HDInsight 3.1.3.521.1453250 (HDP 2.1.12.0-2329, sin cambios)
* HDInsight 3.2.3.525.1459730 (HDP 2.2.2.2-2)
* SDK 1.5.6

Esta versión contiene Hola siguientes actualizaciones:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Área afectada (por ejemplo, servicio, componente o SDK)</p></th>
<th>Tipo de clúster (por ejemplo, Hadoop, HBase o Storm)</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>Corrección de errores de Tez</td>
<td>Las correcciones de Apache TEZ 2214 y TEZ 1923 están incluidas en esta versión de HDI 3.2. Éstos son necesarios para algunas consultas de Hive en Tez que requieren tooshuffle una cantidad significativa de datos.
</td>
<td>HDP</td>
<td>Hadoop</td>
<td><a href="https://issues.apache.org/jira/browse/TEZ-2214">TEZ 2214</a></br><a href="https://issues.apache.org/jira/browse/TEZ-1923">TEZ 1923</a></td>
</tr>
</table>

## <a name="notes-for-04062015-release-of-hdinsight"></a>Notas de la versión del 06/04/2015 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 2.1.10.521.1453250 (HDP 1.3.12.0-01795, sin cambios)
* HDInsight 3.0.6.521.1453250 (HDP 2.0.13.0-2117, sin cambios)
* HDInsight 3.1.3.521.1453250 (HDP 2.1.12.0-2329, sin cambios)
* HDInsight 3.2.3.521.1453250 (HDP 2.2.2.2-1)
* SDK 1.5.6

Esta versión contiene Hola siguientes actualizaciones:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Área afectada (por ejemplo, servicio, componente o SDK)</p></th>
<th>Tipo de clúster (por ejemplo, Hadoop, HBase o Storm)</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>SDK .NET 1.5.6 de HDInsight</td>
<td>Actualiza tooremove algunas clases internas para HDInsight en Linux.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Biblioteca de Avro 1.5.6</td>
<td>Se ha agregado <b>KnownTypeAttribute</b> para el método <b>GetAllKnownTypes</b>. Se ha corregido una NullReferenceException fija cuando un tipo es null para el método GetAllKnownTypes.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Corrección de errores</td>
<td>Servicio de toohello de varias correcciones de errores</td>
<td>Servicio</td>
<td>Todo</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-04012015-release-of-hdinsight"></a>Notas de la versión del 01/04/2015 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 2.1.10.513.1431705 (HDP 1.3.12.0-01795)
* HDInsight 3.0.6.513.1431705 (HDP 2.0.13.0-2117)
* HDInsight 3.1.3.513.1431705 (HDP 2.1.12.0-2329)
* HDInsight 3.2.3.513.1431705 (HDP 2.2.2.1-2600)
* SDK 1.5.5

Esta versión contiene Hola siguientes actualizaciones:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Área afectada (por ejemplo, servicio, componente o SDK)</p></th>
<th>Tipo de clúster (por ejemplo, Hadoop, HBase o Storm)</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>Capacidad tooenable o deshabilitar Escritorio credenciales en clústeres de Windows a través del SDK de .NET</td>
<td>Compatibilidad mediante programación para habilitar o deshabilitar las credenciales de RDP en clústeres de Windows.</td>
<td>SDK</td>
<td>Todo</td>
<td>N/D</td>
</tr>
<tr>
<td>Capacidad tooenable escritorio credenciales en clústeres, mientras que se van a aprovisionar</td>
<td>Soporte de programación para habilitar las credenciales de escritorio remoto que se va a crear el clúster de Hola. Esto quita el proceso de dos pasos de hello para el primer clúster Hola aprovisionamiento y, a continuación, habilitar el escritorio remoto.</td>
<td>SDK</td>
<td>Todo</td>
<td>N/D</td>
</tr>
<tr>
<td>Too2.7.8 actualizada de Python</td>
<td>Python actualizado en clústeres de HDInsight tooPython 2.7.8, que contiene algunos seguridad importantes correcciones para las versiones 2.1, 3.0, 3.1 y 3.2 de HDInsight</td>
<td>Servicio</td>
<td>Todo</td>
<td>N/D</td>
</tr>
<tr>
<td>Cambio de configuración de YARN</td>
<td>Cambiados YARN configuración aplicaciones completado yarn.resourcemanager.max too1000 para todos los tipos de clúster para las versiones 3.1 y 3.2 de HDInsight. Este valor controla sólo lista de Hola de aplicaciones completadas en hello YARN interfaz de usuario. tooget información acerca de las aplicaciones que envía lista toohello anteriores de las aplicaciones que se muestra en hello interfaz de usuario, puede ir directamente toohello historial de servidor.</td>
<td>YARN</td>
<td>Todo</td>
<td>N/D</td>
</tr>
<tr>
<td>Cambio de tamaño de los nodos de un clúster de HBase</td>
<td>Los clústeres de HBase permiten ahora cambiar el tamaño de los nodos (hacia arriba y abajo) para las versiones 3.1 y 3.2 de HDInsight.</td>
<td>Servicio</td>
<td>hbase</td>
<td>N/D</td>
</tr>
<tr>
<td>Actualización de JDBC</td>
<td>Controlador JDBC de SQL es sqljdbc_4.0.2206.100 tooversion actualizada para la versión 3.2 de HDInsight. Esta versión contiene importantes mejoras de seguridad.</td>
<td>HDP</td>
<td>Todo</td>
<td>N/D</td>
</tr>
<tr>
<td>Actualización de la configuración de JVM</td>
<td>Actualizado JVM configuración networkaddress.cache.ttl too300 segundos del valor predeterminado de Hola de -1 para las versiones 3.1 y 3.2 de HDInsight. Este valor de configuración controla Hola directiva para las búsquedas de nombres correcta del servicio de nombres de Hola de caché. Esto corrige un error relacionado con toogrowing y disminuir el tamaño de los clústeres de HBase.</td>
<td>Servicio</td>
<td>hbase</td>
<td>N/D</td>
</tr>
<tr>
<td>Actualizar tooAzure Storage SDK para Java 2.0</td>
<td>Versión 3.2 de HDInsight toouse actualizado Hola versión es más reciente del programa Hola a almacenamiento de Azure SDK para Java. Contiene varias correcciones de errores importantes sobre la versión de Hola 0.6.0 actual.</td>
<td>HDP</td>
<td>Todo</td>
<td>N/D</td>
</tr>
<tr>
<td>Código de origen WASB tooApache actualizado</td>
<td>Versión 3.2 ahora usa Hola código más reciente para el controlador de hello WASB filesystem Apache Hadoop de HDInsight. Con este cambio, controlador de hello WASB ahora se empaqueta como un archivo jar independiente. Esto es simplemente un cambio de empaquetado y no contiene ningún toobehavior cambios del controlador WASB Hola. nombre de Hola de este archivo JAR es 2.6.0.jar de azure de hadoop.</td>
<td>HDP</td>
<td>Todo</td>
<td>N/D</td>
</tr>
<tr>
<td>Actualizaciones del nombre de archivo JAR en HDInsight 3.2</td>
<td>Esta versión de actualización tooHDInsight 3.2 contiene varias correcciones de errores y se han actualizado algunos archivos JAR interno empaquetada como parte de HDP. Estos paquetes HDP JAR archivosestán toohello interno y no para su uso directo por aplicaciones cliente. Las aplicaciones deben empaquetar su propia versión de Hola archivos JAR para que una actualización toohello archivos JAR de HDP interno no interrumpen las aplicaciones de cliente.</td>
<td>HDP</td>
<td>Todo</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-03032015-release-of-hdinsight"></a>Notas de la versión del 03/03/2015 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 2.1.10.488.1375841 (HDP 1.3.9.0-01351, sin cambios)
* HDInsight 3.0.6.488.1375841 (HDP 2.0.9.0-2097, sin cambios)
* HDInsight 3.1.3.488.1375841 (HDP 2.1.10.0-2290, sin cambios)
* HDInsight 3.2.3.488.1375841 (HDP 2.2.10.0-2340, sin cambios)
* SDK 1.5.0 (sin cambios)

Esta versión contiene Hola siguiente actualización:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Área afectada (por ejemplo, servicio, componente o SDK)</p></th>
<th>Tipo de clúster (por ejemplo, Hadoop, HBase o Storm)</th>
<th>JIRA</th>
</tr>
<tr>
<td>Mejoras de confiabilidad.</td>
<td>Hemos realizado correcciones que permiten Hola servicio tooscale mejor con una carga mayor Hola con sentido toocluster creación.</td>
<td>Servicio</td>
<td>Todo</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-02182015-release-of-hdinsight"></a>Notas de la versión del 18/02/2015 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 2.1.10.471.1342507 (HDP 1.3.9.0-01351, sin cambios)
* HDInsight 3.0.6.471.1342507 (HDP 2.0.9.0-2097, sin cambios)
* HDInsight 3.1.3.471.1342507 (HDP 2.1.10.0-2290, sin cambios)
* HDInsight 3.2.3.471.1342507 (HDP-2.2.10.0-2340)
* SDK 1.5.0

Esta versión contiene Hola siguientes actualizaciones:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Área afectada (por ejemplo, servicio, componente o SDK)</p></th>
<th>Tipo de clúster (por ejemplo, Hadoop, HBase o Storm)</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>Clústeres de HDInsight 3.2</td>
<td>Hadoop 2.6/HDP2.2 está disponible con los clústeres de HDInsight 3.2. Contiene actualizaciones principales tooall de componentes de código abierto de Hola. Para más información, vea las novedades de HDInsight y las <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html" target="_blank">notas de la versión de HDP 2.2.0.0</a>.</td>
<td>Software de código abierto</td>
<td>Todo</td>
<td>N/D</td>
</tr>
<tr>
<td>HDInsight en Linux (vista previa)</td>
<td>Los clústeres se pueden implementar ejecutándolos en Ubuntu Linux. Para más información, vea la introducción a HDInsight en Linux.</td>
<td>Servicio</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Disponibilidad general de Storm</td>
<td>Los clústeres de Apache Storm están generalmente disponibles. Para más información, vea la introducción al uso de Storm en HDInsight.</td>
<td>Servicio</td>
<td>Storm</td>
<td>N/D</td>
</tr>
<tr>
<td>Tamaños de máquina virtual</td>
<td>HDInsight de Azure está disponible en más tipos y tamaños de máquina virtual. HDInsight puede usar tamaños de tooA7 A2 compilados para fines generales; Nodos de la serie D que cuentan con unidades de estado sólido (SSD) y procesadores más rápidos de 60 por ciento; y los tamaños A8 y A9 con InfiniBand soporte técnico para una red rápida.</td>
<td>Servicio</td>
<td>Todo</td>
<td>N/D</td>
</tr>
<tr>
<td>Escalado de clústeres</td>
<td>Puede cambiar el número de Hola de nodos de datos de un clúster de HDInsight ejecutando sin necesidad de toodelete o volver a crearla. Actualmente, solo los tipos de clúster Hadoop consulta y Apache Storm tienen esta capacidad, pero la compatibilidad con el tipo de clúster de HBase Apache pronto es toofollow. Para más información, vea Administrar clústeres de HDInsight.</td>
<td>Servicio</td>
<td>Hadoop, Storm</td>
<td>N/D</td>
</tr>
<tr>
<td>Herramientas de Visual Studio</td>
<td>Además toocomplete conjunto de herramientas para Apache Storm, Hola conjunto de herramientas para Apache Hive en Visual Studio ha sido actualizada tooinclude la finalización de instrucciones y validación locales, compatibilidad mejorada con la depuración. Para más información, consulte Introducción a las herramientas de Hadoop de HDInsight para Visual Studio.</td>
<td>Herramientas</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<td>Conector de Hadoop de Azure Cosmos DB</td>
<td>Con el conector de Hadoop de Azure Cosmos DB, puede realizar agregaciones complejas, análisis y manipulaciones sobre los documentos JSON sin esquemas almacenados en todas las colecciones de Azure Cosmos DB o a través de las cuentas de base de datos. Para obtener información y un tutorial, vea el tema sobre cómo ejecutar trabajos de Hadoop con Azure Cosmos DB y HDInsight.</td>
<td>Servicio</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Corrección de errores</td>
<td>Hemos realizado varias correcciones de errores secundarias para servicios de HDInsight. No se espera que haya ningún cambio de comportamiento orientado al cliente.</td>
<td>Servicio</td>
<td>Todo</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-02062015-release-of-hdinsight"></a>Notas de la versión del 06/02/2015 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 2.1.10.463.1325367 (HDP 1.3.9.0-01351, sin cambios)
* HDInsight 3.0.6.463.1325367 (HDP 2.0.9.0-2097, sin cambios)
* HDInsight 3.1.2.463.1325367 (HDP 2.1.10.0-2290)
* SDK N/D

Esta versión contiene Hola siguientes actualizaciones:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Área afectada (por ejemplo, servicio, componente o SDK)</p></th>
<th>Tipo de clúster (por ejemplo, Hadoop, HBase o Storm)</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>Corrección de errores</td>
<td>Hemos realizado varias correcciones de errores secundarias para servicios de HDInsight. No se espera que haya ningún cambio de comportamiento orientado al cliente.</td>
<td>Servicio</td>
<td>Todo</td>
<td>N/D</td>
</tr>
<tr>
<td>Actualización de mantenimiento de HDP 2.1</td>
<td>3.1 HDInsight es toodeploy actualizada HDP 2.1.10.0. Para más información, consulte <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.10/bk_releasenotes_hdp_2.1/content/ch_relnotes-HDP-2.1.10.html" target="_blank">Notas de la versión de HDP-2.1.10</a>. </td>
<td>Software de código abierto</td>
<td>Todo</td>
<td>N/D</td>
</tr>
<tr>
<td>Actualizaciones binarias de HDP</td>
<td>Hay unos algunos archivos JAR en HBase para los que se han actualizado los nombres de archivo. Estos archivos JAR se utilizan internamente por HBase, por lo que no se espera que los clientes tienen una dependencia en nombres de Hola de estos archivos JAR. Entre ellos se incluyen los siguientes:
<ul>
<li>./lib/jetty-6.1.26.hwx.jar</li>
<li>./lib/jetty-sslengine-6.1.26.hwx.jar</li>
<li>./lib/jetty-util-6.1.26.hwx.jar</li>
</ul>
</td>
<td>Software de código abierto</td>
<td>HBase</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-1292015-release-of-hdinsight"></a>Notas de la versión del 29/1/2015 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 2.1.10.455.1309616 (HDP 1.3.9.0-01351, sin cambios)
* HDInsight 3.0.6.455.1309616 (HDP 2.0.9.0-2097, sin cambios)
* HDInsight 3.1.2.455.1309616 (HDP 2.1.9.0-2196, sin cambios)
* SDK N/D

Esta versión contiene Hola siguiente actualización:

<table border="1">

<tr>
<th>Título</th>
<th>Description</th>
<th>Área afectada (por ejemplo, servicio, componente o SDK)</p></th>
<th>Tipo de clúster (por ejemplo, Hadoop, HBase o Storm)</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>Corrección de errores</td>
<td>Hemos realizado algunas correcciones de errores importantes que mejoran la confiabilidad de Hola de clústeres de HDInsight de Hola durante las actualizaciones de Azure.</td>
<td>Servicio</td>
<td>Todo</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-152015-release-of-hdinsight"></a>Notas de la versión del 5/1/2015 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión:

* HDInsight 2.1.10.420.1246118 (HDP 1.3.9.0-01351, sin cambios)
* HDInsight 3.0.6.420.1246118 (HDP 2.0.9.0-2097, sin cambios)
* HDInsight 3.1.2.420.1246118 (HDP 2.1.9.0-2196, sin cambios)

Esta versión contiene Hola siguientes actualizaciones:

<table border="1">

<tr>
<th>Título</th>
<th>Description</th>
<th>Componente</th>
<th>Tipo de clúster</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>Muestras de análisis de tendencias de Twitter y recomendaciones de películas basadas en Mahout</td>
<td><p>En esta versión, Hola consola de consultas de HDInsight tiene dos muestras adicionales:</p>

<p><b>Análisis de tendencias de Twitter</b><br>
Las API públicas proporcionadas por sitios como Twitter constituyen un origen de datos muy útil para analizar y comprender las tendencias populares. En este tutorial, obtenga información acerca de cómo toouse Hive tooget una lista de usuarios de Twitter que envían Hola tweets mayoría que contienen una palabra determinada. </p>

<p><b>Recomendación de películas de Mahout</b><br>
Apache Mahout es una biblioteca de aprendizaje automático de Apache Hadoop. Mahout contiene algoritmos para el procesamiento de datos (como filtrado, clasificación y agrupación en clústeres). En este tutorial, usará un recomendaciones de película toogenerate de motor de recomendación basadas en las películas que han visto sus amigos.</p></td>
<td>Consola de consultas</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Cambiar valor toodefault para la configuración de Hive: hive.auto.convert.join.noconditionaltask.size</td>
<td><p>Esta configuración de tamaño aplica a las combinaciones de asignación de tooautomatically convertir. valor de Hello representa la suma de Hola de tamaños de Hola de tablas que se pueden convertir toohash mapas que caben en la memoria. En una versión anterior, este valor se aumentó desde el valor predeterminado de Hola de 10 MB de too128 MB. Sin embargo, el nuevo valor de Hola de 128 MB generaban toofail de trabajos due toolack de memoria. Esta versión revierte el valor predeterminado de hello realizar copia de too10 MB. Los clientes todavía pueden elegir toooverride este valor durante la creación del clúster, según sus consultas y tamaño de la tabla. Para obtener más información acerca de esta configuración y cómo toooverride, consulte <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.0.2/ds_Hive/optimize-joins.html#JoinOptimization-OptimizeAutoJoinConversion" target="_blank">optimizar automática unir conversión</a> en la documentación de Hortonworks. </p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-12232014-release-of-hdinsight"></a>Notas de la versión 23/12/2014 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión son:

* HDInsight 2.1.10.420.1246783 (versión de HDP sin cambios)
* HDInsight 3.0.6.420.1246783 (versión de HDP sin cambios)
* HDInsight 3.1.1.420.1246783 (versión de HDP sin cambios)

Esta versión contiene Hola siguiente actualización:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Componente</th>
<th>Tipo de clúster</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>Errores de creación de clúster intermitente debido tooexcessive carga</td>
<td><p>Algoritmo mejorado para la descarga de paquetes HDP durante la creación del clúster habilita el control más sólido de errores debido a carga tooexcessive.</p></td>
<td>Servicio</td>
<td>Hadoop, Hbase, Storm</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-12182014-release-of-hdinsight"></a>Notas de la versión del 18/12/2014 de HDinsight
Esta versión contiene Hola después de la actualización de componentes:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Componente</th>
<th>Tipo de clúster</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td><a href = "hdinsight-hadoop-customize-cluster.md" target="_blank">Disponibilidad general de la personalización de clústeres</a></td>
<td><p>Personalización proporciona la capacidad de hello automáticamente toocustomize clústeres de HDInsight de Azure con los proyectos que están disponibles en el ecosistema de Apache Hadoop Hola. Con esta nueva característica, puede experimentar e implementar proyectos de Hadoop tooAzure HDInsight. Esto se habilita a través de hello **acción de secuencia de comandos** característica, que puede modificar clústeres de Hadoop de maneras arbitrario mediante scripts personalizados. Esta personalización está disponible en todo tipo de clústeres de HDInsight, incluidos Hadoop, HBase y Storm. toodemonstrate potencia de Hola de esta capacidad, nos hemos documentados Hola Hola de tooinstall proceso popular <a href = "hdinsight-hadoop-spark-install.md" target="_blank">Spark</a>, <a href = "hdinsight-hadoop-r-scripts.md" target="_blank">R</a>, <a href = "hdinsight-hadoop-solr-install.md" target="_blank">Solr</a>, y <a href = "hdinsight-hadoop-giraph-install.md" target="_blank">Giraph</a> módulos. Esta versión también agrega la capacidad de Hola para los clientes toospecify su acción de secuencia de comandos personalizada a través del portal de Azure de hello, proporciona instrucciones y procedimientos recomendados acerca de cómo toobuild custom script acciones con métodos auxiliares y se proporcionan instrucciones acerca de cómo tootest acción de secuencia de comandos de Hola. </p></td>
<td>Disponibilidad general de características</td>
<td>Todo</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-12052014-release-of-hdinsight"></a>Notas de la versión del 05/12/2014 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión son:

* HDInsight 2.1.9.406.1221105 (HDP 1.3.9.0-01351)
* HDInsight 3.0.5.406.1221105 (HDP 2.0.9.0-2097)
* HDInsight 3.1.1.406.1221105 (HDP 2.1.9.0-2196)
* HDInsight SDK N/A

Esta versión contiene Hola después de las actualizaciones de componentes:

<table border="1">
<tr>
<th>Título</th>
<th>Description</th>
<th>Componente</th>
<th>Tipo de clúster</th>
<th>JIRA (si es aplicable)</th>
</tr>
<tr>
<td>Corrección de errores: error intermitente al agregar un gran número de tabla de particiones tooa en un archivo DDL de Hive </td>
<td><p>Si se produce un error de conexión intermitente con la base de datos de tienda de metadatos de Hive de hello cuando aumenta en gran medida de la tabla de particiones tooa Hive, Hola Hive DDL puede producir un error. Hola después isseen de instrucción en el registro de errores de Hive Hola si se produce este error: </p><p>"ERROR [main]: ql.Driver (SessionState.java:printError(547)) - FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask. MetaException(message:java.lang.RuntimeException: commitTransaction was called but openTransactionCalls = 0. Este error probablemente indica que no hay llamadas desequilibrada tooopenTransaction/commitTransaction)"</p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>HIVE-482 (This is an internal JIRA, so it cannot be quoted externally. Noted here for reference.)</td>
</tr>
<tr>
<td>Corrección de errores: falta de respuesta ocasional Hola consola de consultas de HDInsight</td>
<td>Cuando esto sucede, hello instrucción siguiente puede verse hello WebHCat para trabajo en registro hello WebHCat iniciador: <p>"org.apache.hive.hcatalog.templeton.CatchallExceptionMapper | org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.yarn.exceptions.YarnRuntimeException): no se pudo cargar el archivo de historial {archivo de historial de toohello de dirección url de wasb} "</p></td>
<td>WebHCat</td>
<td>Hadoop</td>
<td>HIVE-482 (This is an internal JIRA, so it cannot be quoted externally. Noted here for reference.)</td>
</tr>
<tr>
<td>Corrección de error: subida ocasional de latencia en consultas de Hbase</td>
<td>Si esto ocurre, los usuarios notarán un pico ocasional de 3 segundos de latencia de Hola de consultas de Hbase. </td>
<td>Puerta de enlace del clúster de HDInsight</td>
<td>HBase</td>
<td>N/D</td>
</tr>
<tr>
<td>Cambios en el nombre de archivo JAR de HDP</td>
<td>Versión 3.0, hay un par de cambios toohello interno JAR se instalaron por HDP clúster HDI. jetty 6.1.26.jar se ha reemplazado por jetty 6.1.26.hwx.jar. jetty-util-6.1.26.jar se ha reemplazado por jetty-util-6.1.26.hwx.jar. Estos cambios aplicarán tooHadoop, Mahout, WebHCat y Oozie proyectos.</td>
<td>Hadoop, Mahout, WebHCat, Oozie</td>
<td>Hadoop, HBase</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-11212014-release-of-hdinsight"></a>Notas de la versión del 21/11/2014 de HDinsight
números de versión completa de Hola para clústeres de HDInsight implementados con esta versión son:

* HDInsight 2.1.9.382.1169709 (sin cambios desde el 14/11/2014)
* HDInsight 3.0.5.382.1169709 (sin cambios desde el 11/14/2014)
* HDInsight 3.1.1.382.1169709 (sin cambios desde el 14/11/2014)
* HDInsight SDK 1.4.0

Esta versión contiene Hola después de las actualizaciones de componentes:

<table border="1">
<tr><th>Título</th><th>Description</th><th>Componente</th><th>Tipo de clúster</th><th>JIRA (si es aplicable)</th></tr>
<tr>
<td>Acceso a los registros de aplicación</td>
<td>Capacidad tooprogrammatically enumerar las aplicaciones que se han ejecutado en los clústeres y toodownload registros específicos de la aplicación o específicos de contenedores pertinentes toohelp problemático en aplicaciones de depuración.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Nombre de la región de capacidad toospecify en IHdInsightClient.DeleteCluster </td>
<td>Hola SDK de HDInsight de Azure proporciona Hola capacidad toospecify un nombre de región al usar **DeleteCluster**. Esto ayuda a los clientes que tenían dos recursos con el mismo nombre en diferentes regiones y si se hubiera toodelete no se puede desbloquear el alguno de ellos.</td>
<td>SDK</td>
<td>Todo</td>
<td>N/D</td>
</tr>
<tr>
<td>ClusterDetails.DeploymentId</td>
<td>Hola **ClusterDetails** objeto devuelve un **DeploymentID** campo que representa un identificador único para el clúster de Hola. Se garantiza toobe único a través de la creación del clúster intenta con hello mismo nombres.</td>
<td>SDK</td>
<td>Todo</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-11142014-release-of-hdinsight"></a>Notas de la versión del 14/11/2014 de HDinsight

números de versión completa de Hola para clústeres de HDInsight implementados con esta versión son:

* HDInsight 2.1.9.382.1169709
* HDInsight 3.0.5.382.1169709
* HDInsight 3.1.1.382.1169709

Esta versión contiene Hola siguientes características nuevas, actualizaciones de componentes y correcciones de errores.

<table border="1">
<tr><th>Título</th><th>Description</th><th>Componente</th><th>Tipo de clúster</th><th>JIRA (si es aplicable)</th></tr>
<tr>
<td>Acción de script (vista previa)</td>
<td>Vista previa de la característica de personalización de clúster de Hola que permite la modificación de Hadoop clústeres de maneras arbitrarios mediante el uso de secuencias de comandos personalizadas. Con esta característica, los usuarios pueden experimentar con e implementar proyectos que están disponibles en hello Apache Hadoop ecosistema tooAzure que clústeres de HDInsight. Esta característica de personalización está disponible en todo tipo de clústeres de HDInsight, como Hadoop, HBase y Storm.</td>
<td>Nueva característica</td>
<td>Todo</td>
<td>N/D</td>
</tr>
<tr>
<td>Trabajos precompilados para Azure Websites y análisis de los registros de almacenamiento</td>
<td>Hola HDInsight consulta consola tiene una galería de introducción que es compatible con soluciones que funcionan en los datos o en datos de ejemplo.
<p>**Soluciones que funcionan en sus datos**:<br>
Hemos creado trabajos para algunos de hello más comunes datos analysis escenarios tooprovide un punto de partida para crear sus propias soluciones. Puede usar los datos con hello trabajo toosee su funcionamiento. A continuación, cuando esté listo, utilice lo que ha aprendido toocreate una solución que se modela después de trabajo creada previamente Hola.</p>
<p>**Soluciones que funcionan en datos de ejemplo**:<br>
Obtenga información acerca de cómo toowork con HDInsight recorriendo algunos escenarios básicos (por ejemplo, análisis de registros web y los datos de sensor). Aprenderá cómo toouse de HDInsight tooanalyze este tipo de datos y cómo puede conectarse a otros datos de toothis aplicaciones y servicios. Visualizar datos mediante la conexión tooMicrosoft Excel proporciona un ejemplo de potencia de Hola de este enfoque.</p></td>
<td>Consola de consultas</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Corrección de pérdida de memoria en Templeton</td>
<td>Se ha solucionado un problema de pérdida de memoria en Templeton que afectaba a los clientes con clústeres de larga ejecución o que enviaban 100s de solicitudes de trabajos por segundo. Hello problema aparece como Templeton 5xx errores y solución de hello toorestart Hola servicio was. solución alternativa de Hello ya no es necesario.</td>
<td>Templeton</td>
<td>Todo</td>
<td>https://issues.apache.org/jira/browse/HADOOP-11248</td>
</tr>
</table>

> [!NOTE]
> se han documentado toodemonstrate Hola nuevas capacidades de facilitados por personalización en el clúster, procedimientos de hello mediante la acción de secuencia de comandos tooinstall Spark y módulos de R en un clúster. Para más información, consulte:

* [Instalación y uso de Spark 1.0 en clústeres de HDInsight](hdinsight-hadoop-spark-install.md)
* [Instalación y uso de R en clústeres de Hadoop para HDInsight](hdinsight-hadoop-r-scripts.md)

## <a name="notes-for-11072014-release-of-hdinsight"></a>Notas de la versión del 11/07/2014 de HDinsight

números de versión completa de Hola para los clústeres de HDInsight que se implementan con esta versión son:

* HDInsight 2.1 2.1.9.374.1153876
* HDInsight 3.0  3.0.5.374.1153876
* HDInsight 3.1 3.1.1.374.1153876

Esta versión contiene Hola después de las actualizaciones de componentes:

<table border="1">
<tr><th>Título</th><th>Description</th><th>Componente</th><th>Tipo de clúster</th><th>JIRA (si es aplicable)</th></tr>
<tr>
<td>HDP 2.1.7</td>
<td>Esta versión se basa en Hortonworks Data Platform (HDP) 2.1.7. Para más información, consulte <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html" target="_blank">Notas de la versión de HDP 2.1.7</a>.</td>
<td>HDP</td>
<td>Todo</td>
<td>N/D</td>
</tr>
<tr>
<td>Servidor de escala de tiempo de YARN</td>
<td>Hola Server de escala de tiempo YARN (también conocido como servidor genérico de historial de aplicación Hola) se habilitó de forma predeterminada. Hola Server de la escala de tiempo proporciona información genérica sobre aplicaciones completadas (por ejemplo, el identificador de la aplicación, nombre de la aplicación, estado de la aplicación, hora de envío de la aplicación y tiempo de finalización de la aplicación).

Esta información de la aplicación se puede recuperar desde el nodo principal de hello accediendo Hola URI http://headnodehost:8188 o ejecutando el comando YARN Hola: yarn aplicación - lista - appStates todos.

Esta información también puede recuperar remotamente mediante una API de REST en https://{ClusterDnsName}. azurehdinsight.net/ws/v1/applicationhistory/.

Para más información, consulte <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">Servidor de escala de tiempo de YARN</a>.</td>
<td>Servicio, YARN</td>
<td>Hadoop, HBase</td>
<td>N/D</td>
</tr>
<tr>
<td>Id. de implementación del clúster</td>
<td>A partir de la versión del SDK 1.3.3.1.5426.29232, los usuarios pueden acceder a un id. exclusivo emitido por HDInsight para cada clúster. Esta toofigure de clientes permite instancias únicas de clústeres cuando se vuelven a usar un nombre DNS a través de crear o quitar escenarios.</td>
<td>SDK</td>
<td>Todo</td>
<td>N/D</td>
</tr>
</table>

> [!NOTE]
> Hola que impidieron el número de versión completo de hello no se muestren en el portal de Hola o se devuelva mediante Hola SDK o mediante Windows PowerShell se ha corregido en esta versión.

## <a name="notes-for-10152014-release"></a>Notas de la versión del 15/10/2014

Esta versión de revisión ha corregido una fuga de memoria en Templeton que afectados usuarios frecuentes de Hola de Templeton. En algunos casos, los usuarios que había ejecutado Templeton muy verían errores aparece como 500 códigos de error, ya que las solicitudes de hello no tendría suficiente toorun de memoria. Hola para solucionar este problema era servicio de Templeton de toorestart Hola. Ahora se ha corregido.

## <a name="notes-for-1072014-release"></a>Notas de la versión del 7/10/2014

* Cuando se usa Ambari punto de conexión, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}" hello *host_name* campo devuelve Hola (FQDN) del nombre de dominio completo del nodo de hello en lugar de solo el nombre de host Hola. Por ejemplo, en lugar de devolver "**headnode0**", obtendrá Hola FQDN"**headnode0. {} ClusterDNS} .azurehdinsight .net**". Este cambio era escenarios toofacilitate requiere que se pueden implementar varios tipos de clúster (por ejemplo, HBase y Hadoop) en una red virtual. Esto ocurre, por ejemplo, cuando se usa HBase como plataforma de back-end para Hadoop.

* Se proporcionan nuevos valores de memoria para la implementación predeterminada de Hola Hola del clúster de HDInsight. Configuración de memoria predeterminada anterior no tuvo en cuenta adecuadamente para obtener instrucciones de hello para el número de Hola de núcleos de CPU que se va a implementar. Estos nuevos valores de memoria deberían proporcionar mejores resultados (según las recomendaciones de Hortonworks). toochange estos elementos, consulte la documentación de referencia SDK de toohello acerca de cómo cambiar la configuración del clúster. Hola nueva configuración de la memoria que se utiliza por clúster de HDInsight de hello predeterminado 4 CPU núcleos (8 contenedor) se detallan en hello en la tabla siguiente. (parenthetically también se proporcionan Hola valores utilizados toothis anterior versión.)

<table border="1">
<tr><th>Componente</th><th>Asignación de memoria</th></tr>
<tr><td> yarn.scheduler.minimum-allocation</td><td>768 MB (antes 512 MB)</td></tr>
<tr><td> yarn.scheduler.maximum-allocation</td><td>6144 MB (sin cambios)</td></tr>
<tr><td>yarn.nodemanager.resource.memory</td><td>6144 MB (sin cambios)</td></tr>
<tr><td>mapreduce.map.memory</td><td>768 MB (antes 512 MB)</td></tr>
<tr><td>mapreduce.map.java.opts</td><td>opts=-Xmx512m (antes -Xmx410m)</td></tr>
<tr><td>mapreduce.reduce.memory</td><td>1536 MB (antes 1024 MB)</td></tr>
<tr><td>mapreduce.reduce.java.opts</td><td>opts=-Xmx1024m (antes -Xmx819m)</td></tr>
<tr><td>yarn.app.mapreduce.am.resource</td><td>768 MB (antes 1024 MB)</td></tr>
<tr><td>yarn.app.mapreduce.am.command</td><td>opts=-Xmx512m (antes -Xmx819m)</td></tr>
<tr><td>mapreduce.task.io.sort</td><td>256 MB (antes 200 MB)</td></tr>
<tr><td>tez.am.resource.memory</td><td>1536 MB (sin cambios)</td></tr>
</table>

Para obtener más información sobre opciones de configuración de memoria de hello utilizado por hilo y MapReduce en hello Hortonworks Data Platform que usa HDInsight, vea [determinar valores de configuración de memoria HDP](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1-latest/bk_installing_manually_book/content/rpm-chap1-11.html). Hortonworks también proporciona una herramienta de configuración de la memoria adecuada de toocalculate.

Con respecto a Azure PowerShell de Hola y Hola mensaje de error de SDK de HDInsight: "*clúster no está configurado para el acceso de los servicios HTTP*":

* Este error es un conocido [problema de compatibilidad](https://social.msdn.microsoft.com/Forums/azure/a7de016d-8de1-4385-b89e-d2e7a1a9d927/hdinsight-powershellsdk-error-cluster-is-not-configured-for-http-services-access?forum=hdinsight) que se pueden producir debido a diferencia de tooa en la versión de Hola de SDK de HDInsight de Hola o hello y Azure PowerShell de clúster Hola. Los clústeres creados a partir del 15/8 cuentan con nueva funcionalidad de aprovisionamiento en redes virtuales. Pero esta capacidad no se interpreta correctamente las versiones anteriores del SDK de HDInsight de Hola o Azure PowerShell. resultado de Hello es un error en algunas operaciones de envío de trabajo. Si usa cmdlets de PowerShell de Azure o las API del SDK de HDInsight (**Use AzureRmHDInsightCluster** o **Invoke-AzureRmHDInsightHiveJob**) toosubmit, esas operaciones podrán errores en trabajos con el mensaje de error de hello " *Clúster <clustername> no está configurado para el acceso de los servicios HTTP*. " O (en función de operación de hello), puede obtener otros mensajes de error, como "*no se puede conectar toocluster*".
* Estos problemas de compatibilidad se resuelven en versiones más recientes de Hola de hello SDK de HDInsight y PowerShell de Azure. Se recomienda la actualización Hola SDK de HDInsight tooversion 1.3.1.6 o posterior y Azure PowerShell herramientas tooversion 0.8.8 o una versión posterior. Puede obtener acceso toohello SDK más reciente de HDInsight de [dato valioso](http://nuget.codeplex.com/wikipage?title=Getting%20Started) y Hola herramientas de PowerShell de Azure en [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

## <a name="notes-for-9122014-release-of-hdinsight-31"></a>Notas de la versión del 12/09/2014 de HDinsight 3.1
* Esta versión se basa en Hortonworks Data Platform (HDP) 2.1.5. Para obtener una lista de errores de hello corregidos en esta versión, vea hello [corregidos en esta versión](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.5/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.5-fixed.html) página en el sitio de Hortonworks Hola.
* En la carpeta de bibliotecas de hello Pig, Hola "avro-mapred-1.7.4.jar" archivo ha cambiado demasiado "avro-mapred-1.7.4-hadoop2.jar." contenido de Hola de este archivo contiene una corrección de errores menor que es indivisible. Se recomienda que los clientes no tome una dependencia directa con nombre Hola de hello JAR archivo tooavoid saltos cuando se cambia el nombre de archivos.

## <a name="notes-for-8212014-release"></a>Notas de la versión del 21/08/2014
* Estamos agregando Hola siguiente WebHCat configuración (HIVE-7155), que establece el límite de memoria de hello predeterminado para un controlador de Templeton trabajo too1 GB. (valor predeterminado de la anterior Hola era 512 MB).

     templeton.mapper.memory.mb (=1024)

  * Este cambio soluciona Hola tras error con determinadas consultas de Hive debido a límites de memoria de toolower: "Contenedor se está ejecutando más allá de los límites de memoria física".
  * toorevert toohello anterior los valores predeterminados, puede establecer esta too512 del valor de configuración a través de PowerShell de Azure en el momento de creación de clúster mediante Hola siguiente comando:

      Add-AzureRmHDInsightConfigValues -Core @{"templeton.mapper.memory.mb"="512";}
* nombre de host de Hello del rol de hello zookeeper cambió demasiado*zookeeper*. Esto afecta a la resolución de nombres en el clúster de hello, pero no afecta a las API de REST externo. Si tiene componentes que Hola uso *zookeepernode* nombre de host, deberá tooupdate les toouse nuevo nombre. Hola nuevos nombres de tres nodos de zookeeper Hola son:

  * zookeeper0
  * zookeeper1
  * zookeeper2
* Se actualiza la matriz de compatibilidad de versiones de HBase. Solo se admite la versión 3.1 de HDInsight (versión 0.98 de HBase) para las cargas de trabajo de HBase de producción. No se admite que la versión 3.0 que estaba disponible para vista previa siga avanzando.

## <a name="notes-about-clusters-created-prior-too8152014"></a>Notas acerca de los clústeres crean anterior too8/15/2014
Un mensaje de error de Azure PowerShell o el SDK de HDInsight, "clúster <clustername> no está configurado para el acceso de los servicios HTTP" (o según la operación hello, otro mensajes de error como: "No se puede conectar toocluster") se pueden producir debido a diferencia de la versión de tooa entre Azure PowerShell u Hola SDK de HDInsight y un clúster. Los clústeres creados a partir del 15/8 cuentan con nueva funcionalidad de aprovisionamiento en redes virtuales. Esta capacidad no interpreta correctamente en las versiones anteriores de hello Azure PowerShell o hello SDK de HDInsight, que da lugar a errores de las operaciones de envío de trabajo. Si usa las API del SDK de HDInsight o Azure PowerShell cmdlets (por ejemplo, utilice AzureRmHDInsightCluster o Invoke-AzureRmHDInsightHiveJob) toosubmit trabajos, esas operaciones pueden producir un error con uno de los mensajes de error de hello descritos.

Estos problemas de compatibilidad se resuelven en versiones más recientes de Hola de hello SDK de HDInsight y PowerShell de Azure. Se recomienda la actualización Hola SDK de HDInsight tooversion 1.3.1.6 o posterior y Azure PowerShell herramientas tooversion 0.8.8 o una versión posterior. Puede obtener acceso toohello SDK más reciente de HDInsight de [NuGet][nuget-link]. Puede tener acceso a herramientas de PowerShell de Azure de hello mediante [instalador de plataforma Web de Microsoft][webpi-link].

## <a name="notes-for-7282014-release"></a>Notas de la versión del 28/07/2014
* **HDInsight disponible en nuevas regiones**: se expanden las regiones toothree de presencia geográfica de HDInsight. Los clientes de HDInsight pueden crear clústeres en estas regiones:
  * Asia oriental
  * Centro-Norte de EE. UU
  * Centro-Sur de EE. UU
* HDInsight versión 1.6 (HDP 1.1 y Hadoop 1.0.3) y HDInsight versión 2.1 (HDP1.3 y 1.2 de Hadoop) que se quitan de hello portal de Azure. Para estas versiones mediante el uso de Hola cmdlet de PowerShell de Azure, puede seguir clústeres de Hadoop de toocreate [New-AzureRmHDInsightCluster](http://msdn.microsoft.com/library/dn593744.aspx) o mediante el uso de Hola [SDK de HDInsight](http://msdn.microsoft.com/library/azure/dn469975.aspx). Para obtener más información, consulte el artículo relativo al [control de versiones de componentes de HDInsight](hdinsight-component-versioning.md).
* Hortonworks Data Platform (HDP) cambia en esta versión:

<table border="1">
<tr><th>HDP</th><th>Cambios</th></tr>
<tr><td>HDP 1.3 / HDI 2.1</td><td>Sin cambios</td></tr>
<tr><td>HDP 2.0 / HDI 3.0</td><td>Sin cambios</td></tr>
<tr><td>HDP 2.1 / HDI 3.1</td><td>zookeeper: ['3.4.5.2.1.3.0-1948'] -> ['3.4.5.2.1.3.2-0002']</td></tr>
</table>

## <a name="notes-for-6242014-release"></a>Notas de la versión del 24/06/2014
Esta versión contiene el servicio de HDInsight de toohello de mejoras:

* **Disponibilidad de HDP 2.1**: 3.1 HDInsight (que contiene HDP 2.1) está generalmente disponible y es la versión de Hola predeterminada para nuevos clústeres.
* **HBase, mejoras de Azure Portal**: vamos a hacer que los clústeres de HBase estén disponibles en vista previa. Puede crear clústeres de HBase desde el portal de hello con unos pocos clics.

Con HBase, puede crear una variedad de cargas de trabajo en tiempo real en HDInsight, desde sitios Web interactivos que funcionan con tooservices de grandes conjuntos de datos almacena datos de sensor y telemetría de millones de dos puntos finales. Hola próximo paso sería tooanalyze datos de hello en estas cargas de trabajo con trabajos de Hadoop y esto es posible en HDInsight a través de PowerShell de Azure y panel de clúster de Hive Hola.

### <a name="apache-mahout-preinstalled-on-hdinsight-31"></a>Apache Mahout preinstalado en HDInsight 3.1
 [Mahout](http://hortonworks.com/hadoop/mahout/) viene preinstalado en los clústeres de Hadoop de HDInsight 3.1, por lo que puede ejecutar trabajos Mahout sin necesidad de hello para la configuración de clúster adicionales. Por ejemplo, puede remoto en un clúster de Hadoop mediante el protocolo de escritorio remoto (RDP) y sin realizar pasos adicionales, puede ejecutar el siguiente comando de Hello World Mahout de hello:

        mahout org.apache.mahout.classifier.df.tools.Describe -p /user/hdp/glass.data -f /user/hdp/glass.info -d I 9 N L

        mahout org.apache.mahout.classifier.df.BreimanExample -d /user/hdp/glass.data -ds /user/hdp/glass.info -i 10 -t 100

Para obtener una explicación más completa de este procedimiento, consulte documentación de Hola de hello [Breiman ejemplo](https://mahout.apache.org/users/classification/breiman-example.html) en el sitio Web de Apache Mahout Hola.

### <a name="hive-queries-can-use-tez-in-hdinsight-31"></a>Las consultas de Hive pueden usar Tez en HDInsight 3.1
Hive 0.13 se encuentra disponible en HDInsight 3.1 y es capaz de ejecutar consultas mediante Tez, que se pueden aprovechar para conseguir mejoras sustanciales del rendimiento.
Tez no está habilitado de forma predeterminada en las consultas de Hive. toouse, debe elegir. Puede habilitar Tez ejecutando Hola siguiente fragmento de código:

        set hive.execution.engine=tez;
        select sc_status, count(*), histogram_numeric(sc_bytes,5) from website_logs_orc_local group by sc_status;

Hortonworks ha publicado un desglose detallado de las mejoras en el rendimiento de las consultas de Hive con Tez proporcionadas en comparativas estándar. Para obtener detalles, consulte [Comparativa de Apache Hive 13 para Enterprise Hadoop](http://hortonworks.com/blog/benchmarking-apache-hive-13-enterprise-hadoop/).

Para más información, vea [Hive en Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez).

### <a name="global-availability"></a>Disponibilidad global
Con la versión de Hola de HDInsight en Hadoop 2.2, Microsoft ha realizado HDInsight disponible en todas las regiones geográficas principales donde Azure está disponible. En concreto, Hola oeste Europa y Asia Sureste los centros de datos se introdujeron en línea. Esto permite que los clústeres de toolocate de clientes en un centro de datos que esté cerca y potencialmente en una zona de requisitos de cumplimiento de normas similares.

### <a name="dos--donts-between-cluster-versions"></a>Qué se debe hacer y qué no se debe hacer entre versiones de clúster
**Las tiendas de metadatos Oozie que se usan con un clúster de HDInsight 3.1 no son compatibles con clústeres de HDInsight 2.1 y no se pueden usar con esta versión anterior**.

Una base de datos personalizada de la tienda de metadatos Oozie implementada con un clúster de HDInsight 3.1 no se puede reutilizar con un clúster de HDInsight 2.1. Este es el caso de hello aunque tienda de metadatos de hello tiene su origen en un clúster de HDInsight 2.1. Este escenario no se admite porque el esquema de la tienda de metadatos de Hola obtiene actualiza cuando se usa con un clúster de HDInsight 3.1, por lo que ya no es compatible con la tienda de metadatos de hello requerido por clústeres hello HDInsight 2.1. Cualquier tooreuse de intento de una tienda de metadatos de Oozie que se ha utilizado con un clúster de HDInsight 3.1 inutilizar el clúster de HDInsight 2.1 Hola.

**Las tiendas de metadatos Oozie no se pueden compartir entre clústeres.**

Las tiendas de metadatos de Oozie son los clústeres de toospecific adjunto, y no se puede compartir a través de clústeres.

### <a name="breaking-changes"></a>Cambios drásticos
**Sintaxis de los prefijos**: Hola solo "wasb: / /" se admiten la sintaxis de 3.0 clústeres y 3.1 de HDInsight. Hola anterior "asv: / /" se admiten la sintaxis de 1.6 clústeres y 2.1 de HDInsight, pero no se admite en HDInsight 3.1 o 3.0 clústeres. Esto significa que todos los trabajos enviaron tooan HDInsight 3.1 o 3.0 de clúster que explícitamente utiliza Hola "asv: / /" se producirá un error de sintaxis. Hola "wasb: / /" sintaxis se debe utilizar en su lugar. Además, trabajos envían tooany HDInsight 3.1 o 3.0 clústeres que se crean con una tienda de metadatos existente que contiene explícitos hace referencia a tooresources mediante Hola "asv: / /" se producirá un error de sintaxis. Estos las tiendas de metadatos necesitan toobe vuelve a crear con hello "wasb: / /" recursos de tooaddress de sintaxis.

**Puertos**: Hola los puertos utilizados por el servicio HDInsight de hello han cambiado. Hola números de puerto que se estaban utilizando estaban dentro del intervalo de puertos efímeros Hola Hola operativo del sistema de Windows. Los puertos se asignan automáticamente desde un intervalo transitorio predefinido en comunicaciones basadas en protocolo de Internet de corta duración. nuevo conjunto de números de puerto de servicio de Hortonworks Data Platform (HDP) permitidos de Hello están fuera de este tooavoid de intervalo que se produzcan conflictos que podrían surgir con puertos de hello utilizados por los servicios que se ejecutan en el nodo principal de Hola. números de puerto nuevos Hello no deberían causar los cambios importantes. números de Hello utilizados son los siguientes:

 **HDInsight 1.6 (HDP 1.1)**

<table border="1">
<tr><th>Nombre</th><th>Valor</th></tr>
<tr><td>dfs.http.address</td><td>namenodehost:30070</td></tr>
<tr><td>dfs.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>dfs.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>dfs.datanode.ipc.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>dfs.secondary.http.address</td><td>0.0.0.0:30090</td></tr>
<tr><td>mapred.job.tracker.http.address</td><td>jobtrackerhost:30030</td></tr>
<tr><td>mapred.task.tracker.http.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>mapreduce.history.server.http.address</td><td>0.0.0.0:31111</td></tr>
<tr><td>templeton.port</td><td>30111</td></tr>
</table>

 **HDInsight 3.1 y 3.0 (HDP 2.1 y 2.0)**

<table border="1">
<tr><th>Nombre</th><th>Valor</th></tr>
<tr><td>dfs.namenode.http-address</td><td>namenodehost:30070</td></tr>
<tr><td>dfs.namenode.https-address</td><td>headnodehost:30470</td></tr>
<tr><td>dfs.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>dfs.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>dfs.datanode.ipc.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>dfs.namenode.secondary.http-address</td><td>0.0.0.0:30090</td></tr>
<tr><td>yarn.nodemanager.webapp.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>templeton.port</td><td>30111</td></tr>
</table>

### <a name="dependencies"></a>Dependencias
Hello las dependencias siguientes agregadas en HDInsight 3.x (HDP2.x):

* guice-servlet
* optiq-core
* javax.inject
* activation
* jsr305
* geronimo-jaspic_1.0_spec
* jul-to-slf4j
* java-xmlbuilder
* ant
* commons-compiler
* jdo-api
* commons-math3
* paranamer
* jaxb-impl
* stringtemplate
* eigenbase-xom
* jersey-servlet
* commons-exec
* jaxb-api
* jetty-all-server
* janino
* xercesImpl
* optiq-avatica
* jta
* eigenbase-properties
* groovy-all
* hamcrest-core
* mail
* linq4j
* jpam
* jersey-client
* aopalliance
* geronimo-annotation_1.0_spec
* ant-launcher
* jersey-guice
* xml-apis
* stax-api
* asm-commons
* asm-tree
* wadl
* geronimo-jta_1.1_spec
* guice
* leveldbjni-all
* velocity
* jettison
* snappy-java
* jetty-all
* commons-dbcp

Hello las dependencias siguientes ya no existen en HDInsight 3.x (HDP2.x):

* jdeb
* kfs
* sqlline
* ivy
* aspectjrt
* json
* core
* jdo2-api
* avro-mapred
* datanucleus-enhancer
* jsp
* commons-logging-api
* commons-math
* JavaEWAH
* aspectjtools
* javolution
* hdfsproxy
* hbase
* snappy

### <a name="version-changes"></a>Cambios de versión
Hola después de los cambios de versión se realizaron entre HDInsight 2.x (HDP1.x) y HDInsight 3.x (HDP2.x):

* metrics-core: ['2.1.2'] -> ['3.0.0']
* derbynet: ['10.4.2.0'] -> ['10.10.1.1']
* datanucleus: ['rdbms-3.0.8'] -> ['rdbms-3.2.9']
* jasper-compiler: ['5.5.12'] -> ['5.5.23']
* log4j: ['1.2.15', '1.2.16'] -> ['1.2.16', '1.2.17']
* derbyclient: ['10.4.2.0'] -> ['10.10.1.1']
* httpcore: ['4.2.4'] -> ['4.2.5']
* hsqldb: ['1.8.0.10'] -> ['2.0.0']
* jets3t: ['0.6.1'] -> ['0.9.0']
* protobuf-java: ['2.4.1'] -> ['2.5.0']
* derby: ['10.4.2.0'] -> ['10.10.1.1']
* jasper: ['runtime-5.5.12'] -> ['runtime-5.5.23']
* commons-daemon: ['1.0.1'] -> ['1.0.13']
* datanucleus-core: ['3.0.9'] -> ['3.2.10']
* datanucleus-api-jdo: ['3.0.7'] -> ['3.2.6']
* zookeeper: ['3.4.5.1.3.9.0-01320'] -> ['3.4.5.2.1.3.0-1948']
* bonecp: ['0.7.1.RELEASE'] -> ['
* 0.8.0.RELEASE']

### <a name="drivers"></a>Controladores
controlador de Hello Java Database Connectivity (JDBC) para SQL Server se usa internamente en HDInsight y no se utiliza para las operaciones externas. Si desea tooconnect tooHDInsight mediante el uso de Open Database Connectivity (ODBC), use Hola Hive controlador ODBC de Microsoft. Para obtener más información, consulte [tooHDInsight Excel conectarse con hello Microsoft Hive ODBC Driver](hdinsight-connect-excel-hive-odbc-driver.md).

### <a name="bug-fixes"></a>Corrección de errores
Con esta versión, nos hemos actualizar Hola después de las versiones de HDInsight con varias correcciones de errores:

* HDInsight 2.1 (HDP 1.3)
* HDInsight 3.0 (HDP 2.0)
* HDInsight 3.1 (HDP 2.1)

## <a name="hortonworks-release-notes"></a>Notas de la versión de Hortonworks
Notas de la versión de Hola plataformas de datos de Hortonworks (HDPs) que se usan los clústeres de la versión de HDInsight están disponibles en hello ubicaciones siguientes:

* La versión 3.1 de HDInsight utiliza una distribución de Hadoop que se basa en hello [Hortonworks Data Platform 2.1.7][hdp-2-1-7]. Se trata de un clúster de Hadoop de hello predeterminado creado cuando se usa Hola portal de Azure después de 7/11/2014. Clústeres de HDInsight 3.1 creados antes de 7/11/2014 se basaban en hello [Hortonworks Data Platform 2.1.1][hdp-2-1-1]
* HDInsight versión 3.0 usa una distribución de Hadoop que se basa en hello [Hortonworks Data Platform 2.0][hdp-2-0-8].
* HDInsight versión 2.1 utiliza una distribución de Hadoop que se basa en hello [1.3 de plataforma de datos de Hortonworks][hdp-1-3-0].
* HDInsight versión 1.6 utiliza una distribución de Hadoop que se basa en hello [1.1 de plataforma de datos de Hortonworks][hdp-1-1-0].

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[nuget-link]: https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.HDInsight/

[webpi-link]: http://go.microsoft.com/?linkid=9811175&clcid=0x409

[hdinsight-install-spark]: ../hdinsight-hadoop-spark-install/
[hdinsight-r-scripts]: ../hdinsight-hadoop-r-scripts/
