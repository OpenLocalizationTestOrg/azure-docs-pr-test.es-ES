---
title: "clúster de recursos de aaaManage de Apache Spark en HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse administrar recursos para clústeres de Spark en HDInsight de Azure para mejorar el rendimiento."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9da7d4e3-458e-4296-a628-77b14643f7e4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: e18682a24f77494db884105f9db03c0a350ddad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a>Administración de recursos de un clúster Apache Spark en Azure HDInsight 

En este artículo, aprenderá cómo interfaces de hello tooaccess como Ambari UI, interfaz de usuario de YARN y Hola Spark historial Server asociada a su clúster Spark. También obtendrá información acerca de cómo tootune Hola configuración de clúster para un rendimiento óptimo.

**Requisitos previos:**

Debe disponer de hello siguiente:

* Una suscripción de Azure. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un clúster de Apache Spark en HDInsight. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-do-i-launch-hello-ambari-web-ui"></a>¿Cómo se puede iniciar hello Ambari Web UI?
1. De hello [Portal de Azure](https://portal.azure.com/), desde el panel de inicio de hello, haga clic en icono de hello para el clúster de Spark (si anclarlo toohello panel de inicio). También puede navegar clúster tooyour en **examinar todos los** > **clústeres de HDInsight**.
2. En la hoja de clúster de Spark hello, haga clic en **panel**. Cuando se le solicite, escriba las credenciales de administrador de Hola para clúster de Spark Hola.

    ![Inicio de Ambari](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "Inicio de Resource Manager")
3. Esto debería iniciar hello Ambari la interfaz de usuario Web, tal y como se muestra a continuación.

    ![Interfaz de usuario web de Ambari](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Interfaz de usuario web de Ambari")   

## <a name="how-do-i-launch-hello-spark-history-server"></a>¿Cómo se puede iniciar Hola Spark historial Server?
1. De hello [Portal de Azure](https://portal.azure.com/), desde el panel de inicio de hello, haga clic en icono de hello para el clúster de Spark (si anclarlo toohello panel de inicio).
2. De hello clúster hoja, en **vínculos rápidos**, haga clic en **panel clúster**. Hola **panel clúster** hoja, haga clic en **Spark historial Server**.

    ![Servidor de historial de Spark](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Servidor de historial de Spark")

    Cuando se le solicite, escriba las credenciales de administrador de Hola para clúster de Spark Hola.

## <a name="how-do-i-launch-hello-yarn-ui"></a>¿Cómo se puede iniciar hello Yarn UI?
Puede usar las aplicaciones de toomonitor de interfaz de usuario de YARN Hola que se están ejecutando en el clúster de Spark Hola.

1. En la hoja de clúster de hello, haga clic en **panel clúster**y, a continuación, haga clic en **YARN**.

    ![Iniciar interfaz de usuario de YARN](./media/hdinsight-apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > Como alternativa, también puede iniciar hello YARN UI de hello Ambari UI. Hola toolaunch Ambari UI, desde la hoja de clúster de hello, haga clic en **panel clúster**y, a continuación, haga clic en **panel de clúster de HDInsight**. En hello Ambari UI, haga clic en **YARN**, haga clic en **vínculos rápidos**, haga clic en Administrador de recursos activos de hello y, a continuación, haga clic en **ResourceManager UI**.
   >
   >

## <a name="what-is-hello-optimum-cluster-configuration-toorun-spark-applications"></a>¿Qué es aplicaciones de Spark de toorun de configuración de clúster óptima de hello?
Hola tres parámetros clave que pueden usar para la configuración de Spark según los requisitos de la aplicación son `spark.executor.instances`, `spark.executor.cores`, y `spark.executor.memory`. Un ejecutor es un proceso que se inicia para una aplicación Spark. Se ejecuta en el nodo de trabajo hello y es responsable toocarry tareas de hello para la aplicación hello. número predeterminado de Hola de ejecutor y tamaños de ejecutor de Hola para cada clúster se calcula según en número de Hola de nodos de trabajador y el tamaño de nodo de trabajo de Hola. Estos se almacenan en `spark-defaults.conf` en nodos principales del clúster Hola.

tres parámetros de configuración de Hello pueden configurarse en el nivel de clúster de hello (para todas las aplicaciones que se ejecutan en el clúster de hello) o se pueden especificar para cada aplicación así.

### <a name="change-hello-parameters-using-ambari-ui"></a>Cambiar los parámetros de hello usando Ambari UI
1. En hello Ambari UI haga clic en **Spark**, haga clic en **configuraciones**y, a continuación, expanda **valores predeterminados personalizados spark**.

    ![Establecer los parámetros mediante Ambari](./media/hdinsight-apache-spark-resource-manager/set-parameters-using-ambari.png)
2. valores predeterminados de Hello son aplicaciones de Spark de buena toohave 4 ejecutarse simultáneamente en el clúster de Hola. Puede cambios estos valores de la interfaz de usuario de hello, tal y como se muestra a continuación.

    ![Establecer los parámetros mediante Ambari](./media/hdinsight-apache-spark-resource-manager/set-executor-parameters.png)
3. Haga clic en **guardar** cambios de configuración de toosave Hola. Hola parte superior de la página de hello, se le pedirá toorestart Hola a todos los servicios afectados. Haga clic en **Restart**(Reiniciar).

    ![Reiniciar los servicios](./media/hdinsight-apache-spark-resource-manager/restart-services.png)

### <a name="change-hello-parameters-for-an-application-running-in-jupyter-notebook"></a>Cambiar los parámetros de Hola de una aplicación que se ejecuta en el Bloc de notas de Jupyter
Para aplicaciones que se ejecutan en el Bloc de notas de hello Jupyter, puede usar hello `%%configure` mágico cambios de configuración de toomake Hola. Idealmente, debe realizar dichos cambios al principio de hello de la aplicación hello, antes de ejecutar la primera celda de código. Esto garantiza que la configuración de hello esté aplicado toohello Livio sesión, cuando se crea. Si desea que la configuración de Hola de toochange en una fase posterior en la aplicación hello, debe usar hello `-f` parámetro. Sin embargo, por lo que todos transcurrir en hello aplicación se perderá.

fragmento de Hola a continuación muestra cómo toochange Hola configuración para una aplicación que se ejecuta en Jupyter.

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, "numExecutors":10}

Parámetros de configuración deben pasar como una cadena JSON y deben estar en línea siguiente de hello después magia hello, como se muestra en la columna de ejemplo de Hola.

### <a name="change-hello-parameters-for-an-application-submitted-using-spark-submit"></a>Cambiar los parámetros de Hola para una aplicación que se envía mediante spark-submit
Siguiente comando es un ejemplo de cómo toochange Hola parámetros de configuración para una aplicación de lote que se envía mediante `spark-submit`.

    spark-submit --class <hello application class tooexecute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-hello-parameters-for-an-application-submitted-using-curl"></a>Cambiar los parámetros de Hola de una aplicación que se envía mediante cURL
Siguiente comando es un ejemplo de cómo toochange Hola parámetros de configuración para una aplicación de lote que se envía utilizando cURL.

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<hello application class tooexecute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="how-do-i-change-these-parameters-on-a-spark-thrift-server"></a>¿Cómo se pueden cambiar estos parámetros en un servidor Thrift de Spark?
Servidor Thrift de Spark proporciona clúster de Spark JDBC/ODBC acceso tooa y es utilizado tooservice consultas Spark SQL. Herramientas como Power BI, Tableau, etc. utilizar ODBC protocolo toocommunicate con consultas de servidor Thrift de Spark tooexecute Spark SQL como una aplicación de Spark. Cuando se crea un clúster de Spark, dos instancias de hello servidor Thrift de Spark se inician, uno en cada nodo principal. Cada servidor Thrift de Spark está visible como una aplicación de Spark en hello YARN interfaz de usuario.

Servidor Thrift de Spark usa inspirará asignación dinámica ejecutor y Hola, por tanto, `spark.executor.instances` no se utiliza. En su lugar, utiliza el servidor Thrift de Spark `spark.dynamicAllocation.minExecutors` y `spark.dynamicAllocation.maxExecutors` recuento de ejecutor de toospecify Hola. parámetros de configuración de Hola `spark.executor.cores` y `spark.executor.memory` es toomodify Hola ejecutor tamaño usado. Puede cambiar estos parámetros como se muestra a continuación.

* Expanda hello **avanzada spark-thrift-sparkconf** parámetros de categoría tooupdate hello `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, y `spark.executor.memory`.

    ![Configurar el servidor Thrift de Spark](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-1.png)    
* Expanda hello **personalizado spark-thrift-sparkconf** parámetro de categoría tooupdate hello `spark.executor.cores`.

    ![Configurar el servidor Thrift de Spark](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="how-do-i-change-hello-driver-memory-of-hello-spark-thrift-server"></a>¿Cómo se cambia la memoria del controlador de Hola de hello servidor Thrift de Spark?
Memoria de servidor Thrift de Spark controlador es too25 configurado % del tamaño de RAM del nodo principal de hello, proporcionado por el tamaño de RAM total de Hola de nodo principal de hello es mayor que 14GB. Puede usar hello Ambari UI toochange Hola controlador configuración de la memoria, tal y como se muestra a continuación.

* En hello Ambari UI haga clic en **Spark**, haga clic en **configuraciones**, expanda **avanzada spark env**y, a continuación, proporcionar valor de Hola para **spark_thrift_cmd_opts**.

    ![Configurar la RAM del servidor Thrift de Spark](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="i-do-not-use-bi-with-spark-cluster-how-do-i-take-hello-resources-back"></a>No uso BI con el clúster Spark. ¿Cómo realizo recursos Hola nuevo?
Dado que se usa la asignación dinámica de Spark, hello únicamente los recursos consumidos por servidor thrift son Hola recursos para dos patrones de aplicación Hola. tooreclaim servicios de servidor Thrift que se ejecutan en el clúster de Hola Hola a estos recursos que debe detener.

1. De Hola Ambari UI, desde el panel izquierdo de hello, haga clic en **Spark**.
2. En la página siguiente de hello, haga clic en **servidores Thrift de Spark**.

    ![Reiniciar el servidor Thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-1.png)
3. Debería ver Hola dos headnodes en qué Hola se está ejecutando servidor Thrift de Spark. Haga clic en uno de hello headnodes.

    ![Reiniciar el servidor Thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-2.png)
4. página siguiente de Hello enumera todos los servicios de hello ejecutando en ese nodo principal. En lista de hello haga clic en hello botón desplegable siguiente tooSpark servidor Thrift y, a continuación, haga clic en **detener**.

    ![Reiniciar el servidor Thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-3.png)
5. Repita estos pasos en hello también otro nodo principal.

## <a name="my-jupyter-notebooks-are-not-running-as-expected-how-can-i-restart-hello-service"></a>Mis cuadernos de Jupyter no se ejecutan según lo previsto. ¿Cómo puedo reiniciar servicio Hola?
Inicie hello Ambari Web UI como se indicó anteriormente. En el panel de navegación izquierdo de hello, haga clic en **Jupyter**, haga clic en **acciones de servicio**y, a continuación, haga clic en **reiniciar todos los**. Esto iniciará el servicio de Jupyter de hello en todos los headnodes Hola.

    ![Restart Jupyter](./media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")

## <a name="how-do-i-know-if-i-am-running-out-of-resources"></a>¿Cómo sé si me estoy quedando sin recursos?
Inicie hello Yarn interfaz de usuario como se indicó anteriormente. En la tabla de métricas de clúster sobre la pantalla de bienvenida, compruebe los valores de **usa memoria** y **Total de memoria** columnas. Si los valores de hello 2 son muy similares, podría no ser suficiente siguiente aplicación de recursos toostart Hola. Hello Esto mismo aplica toohello **VCores utiliza** y **VCores Total** columnas. Además, en la vista principal de hello, si hay una aplicación permanecido en **aceptado** estado y no pasar al **EJECUTANDO** ni **error** estado, esto también podría ser una indicación que no está obteniendo suficiente toostart de recursos.

    ![Resource Limit](./media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")

## <a name="how-do-i-kill-a-running-application-toofree-up-resource"></a>¿Cómo se puede terminar un ejecución toofree aplicación recurso?
1. Hola Yarn de interfaz de usuario, desde el panel izquierdo de hello, haga clic en **ejecutando**. En la lista hello las aplicaciones en ejecución, determinar Hola aplicación toobe eliminar y haga clic en hello **identificador**.

    ![Eliminación de App1](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "Eliminación de App1")

2. Haga clic en **aplicación Kill** en hello esquina superior derecha, a continuación, haga clic en **Aceptar**.

    ![Eliminación de App2](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "Eliminación de App2")

## <a name="see-also"></a>Otras referencias
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)

### <a name="for-data-analysts"></a>Para analistas de datos

* [Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Análisis del registro del sitio web con Spark en HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Análisis de datos de telemetría de Application Insights con Spark en HDInsight](hdinsight-spark-analyze-application-insight-logs.md)
* [Uso de Caffe en Azure HDInsight Spark para el aprendizaje profundo distribuido](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Para desarrolladores de Spark

* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar solicitudes de Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Uso de paquetes externos con cuadernos de Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)
