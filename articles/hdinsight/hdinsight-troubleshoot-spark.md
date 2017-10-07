---
title: aaaTroubleshoot Spark mediante el uso de HDInsight de Azure | Documentos de Microsoft
description: "Obtenga respuestas toocommon preguntas sobre cómo trabajar con Apache Spark y HDInsight de Azure."
keywords: "Azure HDInsight, preguntas más frecuentes de Spark, guía de solución de problemas, problemas comunes, configuración de la aplicación, Ambari"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: 25D89586-DE5B-4268-B5D5-CC2CE12207ED
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: c9f910daf295462238a3143ae2589db6d383097f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a>Solución de problemas de Spark mediante Azure HDInsight

Obtenga información acerca de los principales problemas de Hola y sus soluciones cuando se trabaja con cargas de Apache Spark en Apache Ambari.

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a>Cómo se configura una aplicación Spark mediante Ambari en clústeres

### <a name="resolution-steps"></a>Pasos de la solución

valores de configuración de Hola para este procedimiento se haya establecido anteriormente en HDInsight. vea toodetermine qué configuraciones de Spark necesitan valores de conjunto y toowhat toobe, [¿qué hace que un Spark excepción de aplicación OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception). 

1. En la lista Hola de clústeres, seleccione **Spark2**.

    ![Selección del clúster de la lista](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. Seleccione hello **configuraciones** ficha.

    ![Seleccione la pestaña de configuraciones de Hola](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. En la lista Hola de configuraciones, seleccione **valores predeterminados personalizados-spark2**.

    ![Selección de custom-spark-defaults](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. Buscar valor Hola configuración que necesita como tooadjust, **spark.executor.memory**. En este caso, Hola valo **4608m** es demasiado alto.

    ![Seleccione el campo de hello spark.executor.memory](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. Conjunto Hola valor toohello configuración recomendada. Hola valor **2048m** se recomienda para esta configuración.

    ![Cambiar valor too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. Guardar el valor de hello y, a continuación, Guardar configuración de Hola. En la barra de herramientas de hello, seleccione **guardar**.

    ![Guardar la configuración y la configuración de Hola](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    Se le notificará si hay configuraciones que necesiten atención. Tenga en cuenta los elementos de hello y, a continuación, seleccione **continuar de todos modos**. 

    ![Selección de Proceed Anyway (Continuar de todos modos)](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    Escribir una nota sobre los cambios de configuración de hello y, a continuación, seleccione **guardar**.

    ![Escriba una nota sobre los cambios de hello realizados](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. Cada vez que se guarda una configuración, le preguntarán si servicio de hello toorestart. Seleccione **Reiniciar**.

    ![Selección de Reiniciar](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    Confirme el reinicio de Hola.

    ![Selección de Confirm Restart All (Confirmar reinicio de todo)](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    Puede revisar los procesos de Hola que se ejecutan.

    ![Revisar los procesos en ejecución](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. Puede agregar configuraciones. En la lista Hola de configuraciones, seleccione **valores predeterminados personalizados-spark2**y, a continuación, seleccione **Agregar propiedad**.

    ![Selección de Agregar propiedad](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. Defina una nueva propiedad. Puede definir una propiedad única mediante un cuadro de diálogo para una configuración específica, como tipo de datos de Hola. O bien, puede definir varias propiedades mediante una definición por línea. 

    En este ejemplo, Hola **spark.driver.memory** propiedad se define con un valor de **4g**.

    ![Definir la nueva propiedad](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. Guardar configuración de hello y, a continuación, reinicie el servicio de hello tal como se describe en los pasos 6 y 7.

Estos cambios para todo el clúster, pero pueden reemplazarse cuando se envía el trabajo de Spark Hola.

### <a name="additional-reading"></a>Lecturas adicionales

[Envío de trabajos de Spark en clústeres de HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a>Cómo se configura una aplicación Spark mediante un cuaderno de Jupyter Notebook en clústeres

### <a name="resolution-steps"></a>Pasos de la solución

1. vea toodetermine qué configuraciones de Spark necesitan valores de conjunto y toowhat toobe, [¿qué hace que un Spark excepción de aplicación OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).

2. En la celda primera Hola de hello Jupyter Bloc de notas, después de hello **%% configurar** directiva, especificar configuraciones de Spark hello en formato JSON válido. Cambiar los valores reales de hello según sea necesario:

    ![Agregar una configuración](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a>Lecturas adicionales

[Envío de trabajos de Spark en clústeres de HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a>Cómo se configura una aplicación Spark mediante Livy en clústeres

### <a name="resolution-steps"></a>Pasos de la solución

1. vea toodetermine qué configuraciones de Spark necesitan valores de conjunto y toowhat toobe, [¿qué hace que un Spark excepción de aplicación OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception). 

2. Enviar Hola Spark aplicación tooLivy mediante un cliente REST como cURL. Use un comando información similar toohello siguiente. Cambiar los valores reales de hello según sea necesario:

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a>Lecturas adicionales

[Envío de trabajos de Spark en clústeres de HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a>Cómo se configura una aplicación Spark mediante spark-submit en clústeres

### <a name="resolution-steps"></a>Pasos de la solución

1. vea toodetermine qué configuraciones de Spark necesitan valores de conjunto y toowhat toobe, [¿qué hace que un Spark excepción de aplicación OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).

2. Inicie el shell de spark mediante un siguiente toohello similar de comando. Cambie el valor real de Hola de configuraciones de Hola según sea necesario: 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a>Lecturas adicionales

[Envío de trabajos de Spark en clústeres de HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a>Qué produce una excepción OutOfMemoryError en una aplicación Spark

### <a name="detailed-description"></a>Descripción detallada

Hola aplicación Spark produce un error, con los siguientes tipos de excepciones no detectadas de hello:

```apache
ERROR Executor: Exception in task 7.0 in stage 6.0 (TID 439) 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

```apache
ERROR SparkUncaughtExceptionHandler: Uncaught exception in thread Thread[Executor task launch worker-0,5,main] 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

### <a name="probable-cause"></a>Causa probable

Hola más probable de esta excepción es que no hay suficiente memoria en montón se asigna máquinas virtuales de Java toohello (JVMs). Estas JVMs se inician como elementos de ejecución o los controladores como parte de la aplicación de Spark Hola. 

### <a name="resolution-steps"></a>Pasos de la solución

1. Determinar el tamaño máximo de Hola de identificadores de aplicación de hello datos Hola Spark. Puede realizar una estimación basada en tamaño máximo de Hola Hola de datos de entrada, los datos de hello intermedios que se generan al transformar los datos de entrada de Hola y datos de salida de hello que se producen cuando la aplicación hello más está transformando los datos intermedios Hola. Este proceso puede ser iterativo si no puede realizar una estimación formal inicial. 

2. Asegúrese de que ese clúster de HDInsight de Hola que se vayan toouse tiene suficientes recursos de memoria y núcleos tooaccommodate Hola Spark una aplicación. Se puede determinar mediante la visualización de la sección de las métricas de clúster Hola de hello YARN UI para los valores de hello de **usa memoria** vs. **Memory Total** (Total de memoria ) y **VCores Used** (VCores usados) frente a **VCores Total** (Total de VCores).

3. Establecer los valores de tooappropriate de configuraciones, que no deben superar el 90% de memoria disponible de Hola y núcleos de hello después Spark. Hola valores deberían estar bien dentro de los requisitos de memoria de Hola de hello aplicación Spark: 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    tooget Hola memoria total utilizada por todos los elementos de ejecución, ejecute el siguiente comando de hello: 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    tooget Hola memoria total utilizada por el controlador de hello, ejecute el siguiente comando de hello:
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a>Lecturas adicionales

- [Información general de la administración de memoria en Spark](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/) (Depuración de una aplicación Spark en un clúster de HDInsight)

