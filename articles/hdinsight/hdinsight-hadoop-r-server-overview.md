---
title: Visita aaaIntroduction Server en HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse R Server en las aplicaciones de toocreate de HDInsight para el análisis de grandes cantidades de datos."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6dc21bf5-4429-435f-a0fb-eea856e0ea96
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: daf7b70a15748d66510a04da370f39c5f26eb4ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#<a name="introduction-toor-server-and-open-source-r-capabilities-on-hdinsight"></a>Introducción visita Server y las capacidades de R de código abierto en HDInsight

Microsoft R Server está disponible como opción de implementación al crear clústeres de HDInsight en Azure. Esta nueva capacidad proporciona científicos de datos, estadísticos y los programadores de R con acceso a petición tooscalable, distribuidas métodos de análisis en HDInsight.

Clústeres pueden ser el tamaño adecuado toohello proyectos y tareas en cuestión y, a continuación, se cierra cuando ya no se necesitan. Puesto que formen parte de HDInsight de Azure, estos clústeres vienen con el soporte técnico 24/7 de nivel empresarial, un SLA del 99,9% del tiempo y Hola capacidad toointegrate con otros componentes de hello ecosistema de Azure.

R Server en HDInsight proporciona capacidades más recientes de hello para el análisis basado en R en conjuntos de datos de prácticamente cualquier tamaño, cargar tooeither almacenamiento de blobs de Azure o Data Lake. Puesto que el servidor de R se basa en código abierto R, pueden aprovechar Hola R aplicaciones que compilar cualquiera de los paquetes de código abierto R de hello 8000 +. rutinas de Hello en ScaleR, paquete de análisis de grandes cantidades de datos de Microsoft incluido con R Server, también están disponibles.

nodo de Hello borde de un clúster proporciona un lugar cómodo tooconnect toohello clúster y toorun los scripts de R. Con un nodo del borde, tienen funciones de opción de ejecución hello en paralelo distribuida Hola de ScaleR entre núcleos de Hola de servidores de nodos de hello borde. También puede ejecutar ellos en todos los nodos de Hola de clúster de hello mediante el uso del ScaleR Hadoop MapReduce o Spark contextos de proceso.

modelos de Hola o predicciones que se puede descargar el resultado del análisis para usan en local. También pueden emplearse en otro lugar de Azure, en concreto a través del [servicio web](../machine-learning/machine-learning-publish-a-machine-learning-web-service.md) [Azure Machine Learning Studio](http://studio.azureml.net).

## <a name="get-started-with-r-on-hdinsight"></a>Introducción a R en HDInsight
tooinclude R Server en un clúster de HDInsight, debe seleccionar tipo de clúster de servidor de R Hola al crear un clúster de HDInsight con hello portal de Azure. Hola tipo de clúster de servidor de R incluye R Server Hola nodos de datos de clúster de Hola y en un nodo del borde, que actúa como una zona de aterrizaje para el análisis basado en servidor de R. Vea [Getting Started with R Server en HDInsight](hdinsight-hadoop-r-server-get-started.md) para ver un tutorial sobre cómo toocreate Hola clúster.

## <a name="learn-about-data-storage-options"></a>Información sobre las opciones de almacenamiento de datos
Almacenamiento predeterminado para el sistema de archivos HDFS Hola de clústeres de HDInsight puede asociarse con una cuenta de almacenamiento de Azure o un almacén de Azure Data Lake. Esta asociación se asegura de que se cargan los datos toohello de almacenamiento de clúster durante el análisis se hace persistente. Existen diversas herramientas para controlar Hola datos transferencia toohello opción de almacenamiento que seleccione, incluidas las instalaciones de carga basado en el portal de Hola de cuenta de almacenamiento de Hola y Hola [AzCopy](../storage/common/storage-use-azcopy.md) utilidad.

Tiene la opción de Hola de agregar acceso tooadditional Blob y lake almacenes de datos durante el proceso independientemente de la opción de almacenamiento principal de hello en uso de aprovisionamiento de clúster de Hola. Vea [Introducción a servidor de R en HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-get-started) para obtener información sobre cómo agregar cuentas de acceso de tooadditional. Vea Hola complementario [opciones de almacenamiento de Azure para R Server en HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-storage) toolearn artículo más acerca del uso de varias cuentas de almacenamiento.

También puede usar [archivos de Azure](../storage/files/storage-how-to-use-files-linux.md) como una opción de almacenamiento para su uso en el nodo del borde de Hola. Archivos de Azure permite toomount un recurso compartido de archivos que se creó en el almacenamiento de Azure toohello sistema de archivos de Linux. Para más información sobre estas opciones de almacenamiento de datos de R Server en un clúster de HDInsight, consulte [Opciones de Azure Storage para R Server en HDInsight](hdinsight-hadoop-r-server-storage.md).

## <a name="access-r-server-on-hello-cluster"></a>Acceso R Server en clúster de Hola
Puede conectar visita servidor en el nodo del borde hello mediante un explorador, siempre que ha elegido tooinclude RStudio Server durante el proceso de aprovisionamiento de Hola. Si no ha instalado al aprovisionar el clúster de hello, puede agregarlo más adelante. Para información sobre cómo instalar RStudio Server una vez que se haya creado un clúster, consulte [Instalación de RStudio con R Server en HDInsight](hdinsight-hadoop-r-server-install-r-studio.md). También puede conectar toohello R Server mediante SSH/PuTTY tooaccess Hola R consola. 

## <a name="develop-and-run-r-scripts"></a>Desarrollo y ejecución de scripts de R
las secuencias de comandos de Hello R creará y ejecutará pueden usar cualquiera de hello 8000 + paquetes de código abierto R en suma toohello en paralelo y distribuyen rutinas disponibles en la biblioteca de ScaleR Hola. En general, una secuencia de comandos que se ejecuta con el servidor de R en el nodo del borde de Hola se ejecuta dentro de intérprete de R de hello en ese nodo. excepciones de Hello son los pasos que necesitan toocall una función ScaleR con un contexto de proceso que se establece tooHadoop MapReduce (RxHadoopMR) o Spark (RxSpark). En este caso, la función de Hola se ejecuta en modo distribuido a través de los nodos de datos (tarea) del clúster de Hola que están asociados a los datos de saludo al que hace referencia. Para obtener más información acerca de las opciones de contexto de proceso distinto de hello, consulte [proceso opciones de contexto de servidor de R en HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).

## <a name="operationalize-a-model"></a>Uso de modelos
Una vez completado el modelado de datos, puede poner las predicciones de hello modelo toomake para datos nuevos de Azure y local. Este proceso se conoce como "puntuación". La puntuación puede realizarse en HDInsight, Azure Machine Learning o de forma local.

### <a name="score-in-hdinsight"></a>Puntuación en HDInsight
tooscore en HDInsight, escribir una función de R que llama a las predicciones de toomake de modelo para un nuevo archivo de datos que ha cargado tooyour cuenta de almacenamiento. A continuación, guardar predicciones hello toohello back-cuenta de almacenamiento. Puede ejecutar Hola rutinarias a petición en el nodo del borde Hola del clúster o mediante un trabajo programado.  

### <a name="score-in-azure-machine-learning-aml"></a>Puntuación en Azure Machine Learning (AML)
tooscore con un servicio web AML, use Hola abre paquete de R de aprendizaje de Azure máquina de origen conocido como [AzureML](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) toopublish el modelo como un servicio web de Azure. Para mayor comodidad, este paquete es previamente instalado en el nodo del borde de Hola. A continuación, utilizar servicios de hello en aprendizaje automático toocreate una interfaz de usuario para el servicio web de hello y, a continuación, llame al servicio web de hello según sea necesario para la puntuación.

Si elige esta opción, deberá tooconvert los objetos de modelo de código abierto ScaleR tooequivalent de objetos de modelo para usan con el servicio web de Hola. Para esta conversión, utilice las funciones de coerción de ScaleR, como `as.randomForest()`, para los modelos basados en conjuntos.

### <a name="score-on-premises"></a>Puntuación en un entorno local
tooscore local después de crear el modelo, puede serializar el modelo de hello en R, descarga, deserializar y, a continuación, usarlo para puntuar nuevos datos. Puede puntuar nuevos datos con enfoque Hola se describió anteriormente en [de puntuación en HDInsight](#scoring-in-hdinsight) o mediante [DeployR](https://deployr.revolutionanalytics.com/).

## <a name="maintain-hello-cluster"></a>Mantener el clúster de Hola
### <a name="install-and-maintain-r-packages"></a>Instalación y mantenimiento de paquetes de R
La mayoría de los paquetes de hello R que utilizan es obligatorios en el nodo del borde de Hola desde la mayoría de los pasos de los scripts de R que se ejecuten allí. tooinstall paquetes de R adicionales en el nodo del borde de hello, puede usar Hola habitual `install.packages()` método en R.

Si simplemente está utilizando rutinas de biblioteca de ScaleR hello en el clúster de hello, no es necesario normalmente tooinstall paquetes de R adicionales en los nodos de datos Hola. Sin embargo, tendrá que usar de hello toosupport de paquetes adicionales de **rxExec** o **RxDataStep** ejecución Hola nodos de datos.

En estos casos, los paquetes adicionales de hello pueden instalarse con una acción de secuencia de comandos después de crear el clúster de Hola. Para más información, consulte [Creación de un clúster de HDInsight con R Server](hdinsight-hadoop-r-server-get-started.md).   

### <a name="change-hadoop-map-reduce-memory-settings"></a>Cambio de la configuración de memoria de Hadoop MapReduce
Un clúster puede ser modificado toochange Hola cantidad de memoria que está disponible visita Server cuando se ejecuta un trabajo de MapReduce. toomodify un clúster, use Hola Apache Ambari UI que está disponible a través de Hola de Azure, hoja portal para el clúster. Para obtener instrucciones acerca de cómo tooaccess Hola Ambari UI para el clúster, consulte [administrar clústeres de HDInsight con hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).

También es posible toochange Hola cantidad de memoria que está disponible visita Server mediante conmutadores de Hadoop en llamada de hello demasiado**RxHadoopMR** como se indica a continuación:

    hadoopSwitches = "-libjars /etc/hadoop/conf -Dmapred.job.map.memory.mb=6656"  

### <a name="scale-your-cluster"></a>Escalado del clúster
Un clúster existente se puede escalar hacia arriba o hacia abajo a través del portal de Hola. Mediante el escalado, puede tener una capacidad adicional Hola que podría necesitar para tareas de procesamiento más grandes o se puede reducir un clúster cuando está inactivo. Para obtener instrucciones acerca de cómo tooscale un clúster, consulte [HDInsight administrar clústeres](hdinsight-administer-use-portal-linux.md).

### <a name="maintain-hello-system"></a>Mantener el sistema de Hola
Revisiones del sistema operativo de tooapply de mantenimiento y otras actualizaciones se realiza en hello subyacente máquinas virtuales de Linux en un clúster de HDInsight durante horas de poca actividad. Normalmente, se realiza mantenimiento a las 3:30 A.M. (basado en hora local Hola Hola VM) todos los lunes y el jueves. Las actualizaciones se realizan de forma que no afecten a más de un cuarto del clúster de Hola a la vez.  

Puesto que los nodos principales de hello son redundantes y no todos los nodos de datos que se ven afectados, pueden ralentizar los trabajos que se ejecutan durante este tiempo. Todavía debe ejecutarse toocompletion, sin embargo. Cualquier software personalizado o dato local que haya instalado se conserva a través de estos eventos de mantenimiento, salvo que se produzca un error irrecuperable que requiera recompilar el clúster.

## <a name="learn-about-ide-options-for-r-server-on-an-hdinsight-cluster"></a>Más información sobre las opciones del IDE de R Server en el clúster de HDInsight
nodo del borde de Linux Hola de un clúster de HDInsight es hello aterrizaje zona para el análisis basado en R. Las versiones recientes de HDInsight proporcionan una opción predeterminada para instalar la versión de la Comunidad de Hola de [RStudio Server](https://www.rstudio.com/products/rstudio-server/) en el nodo de hello borde como un IDE basada en explorador. Uso de servidor de RStudio como un IDE para el desarrollo de Hola y ejecutar scripts de R pueden ser considerablemente más productivos que simplemente utilizando la consola de hello R. Si eligió no tooadd RStudio servidor al crear Hola clúster pero desea ponerlos tooadd una versión posterior, a continuación, consulte [instalar R Studio Server en clústeres de HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-install-r-studio). +

Otra opción IDE completa es tooinstall un IDE, escritorio y usar clúster de hello tooaccess mediante el uso de un contexto de proceso remoto MapReduce o Spark. Las opciones incluyen [Herramientas de R para Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx) (RTVS) de Microsoft, RStudio y [StatET](http://www.walware.de/goto/statet) basado en Eclipse de Walware.

Por último, se puede tener acceso a consola de R Server hello en el nodo del borde de hello escribiendo **R** en línea de comandos de Linux Hola después de conectarse a través de SSH o PuTY. Cuando se usa la interfaz de la consola de hello, es conveniente toorun un editor de texto para el desarrollo de script de R en otra ventana y corte y pegue las secciones de la secuencia de comandos en consola Hola R según sea necesario.

## <a name="learn-about-pricing"></a>Más información sobre los precios
Hello las cuotas que están asociadas a un clúster de servidor de R de HDInsight estructuran similar toohello cuotas para los clústeres de HDInsight estándar de Hola. Se basan en el tamaño de Hola de hello subyacentes de las máquinas virtuales en nombre de Hola, datos y nodos de borde, con adición de Hola de un aumento de horas de núcleo. Para obtener más información sobre precios HDInsight y la disponibilidad de Hola de una prueba gratuita de 30 días, vea [precios HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de cómo toouse R Server con HDInsight clústeres, vea Hola temas siguientes:

* [Introducción al uso de R Server en HDInsight (versión preliminar)](hdinsight-hadoop-r-server-get-started.md)
* [Agregar servidor RStudio tooHDInsight (si no se instala durante la creación del clúster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opciones de contexto de proceso para R Server en HDInsight (versión preliminar)](hdinsight-hadoop-r-server-compute-contexts.md)
* [Opciones de Azure Storage para R Server en HDInsight](hdinsight-hadoop-r-server-storage.md)
