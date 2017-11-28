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
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a><span data-ttu-id="ba66a-104">Solución de problemas de Spark mediante Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ba66a-104">Troubleshoot Spark by using Azure HDInsight</span></span>

<span data-ttu-id="ba66a-105">Obtenga información acerca de los principales problemas de Hola y sus soluciones cuando se trabaja con cargas de Apache Spark en Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="ba66a-105">Learn about hello top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span></span>

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a><span data-ttu-id="ba66a-106">Cómo se configura una aplicación Spark mediante Ambari en clústeres</span><span class="sxs-lookup"><span data-stu-id="ba66a-106">How do I configure a Spark application by using Ambari on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="ba66a-107">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="ba66a-107">Resolution steps</span></span>

<span data-ttu-id="ba66a-108">valores de configuración de Hola para este procedimiento se haya establecido anteriormente en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ba66a-108">hello configuration values for this procedure were previously set in HDInsight.</span></span> <span data-ttu-id="ba66a-109">vea toodetermine qué configuraciones de Spark necesitan valores de conjunto y toowhat toobe, [¿qué hace que un Spark excepción de aplicación OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="ba66a-109">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

1. <span data-ttu-id="ba66a-110">En la lista Hola de clústeres, seleccione **Spark2**.</span><span class="sxs-lookup"><span data-stu-id="ba66a-110">In hello list of clusters, select **Spark2**.</span></span>

    ![Selección del clúster de la lista](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. <span data-ttu-id="ba66a-112">Seleccione hello **configuraciones** ficha.</span><span class="sxs-lookup"><span data-stu-id="ba66a-112">Select hello **Configs** tab.</span></span>

    ![Seleccione la pestaña de configuraciones de Hola](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. <span data-ttu-id="ba66a-114">En la lista Hola de configuraciones, seleccione **valores predeterminados personalizados-spark2**.</span><span class="sxs-lookup"><span data-stu-id="ba66a-114">In hello list of configurations, select **Custom-spark2-defaults**.</span></span>

    ![Selección de custom-spark-defaults](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. <span data-ttu-id="ba66a-116">Buscar valor Hola configuración que necesita como tooadjust, **spark.executor.memory**.</span><span class="sxs-lookup"><span data-stu-id="ba66a-116">Look for hello value setting that you need tooadjust, such as **spark.executor.memory**.</span></span> <span data-ttu-id="ba66a-117">En este caso, Hola valo **4608m** es demasiado alto.</span><span class="sxs-lookup"><span data-stu-id="ba66a-117">In this case, hello value of **4608m** is too high.</span></span>

    ![Seleccione el campo de hello spark.executor.memory](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. <span data-ttu-id="ba66a-119">Conjunto Hola valor toohello configuración recomendada.</span><span class="sxs-lookup"><span data-stu-id="ba66a-119">Set hello value toohello recommended setting.</span></span> <span data-ttu-id="ba66a-120">Hola valor **2048m** se recomienda para esta configuración.</span><span class="sxs-lookup"><span data-stu-id="ba66a-120">hello value **2048m** is recommended for this setting.</span></span>

    ![Cambiar valor too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. <span data-ttu-id="ba66a-122">Guardar el valor de hello y, a continuación, Guardar configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba66a-122">Save hello value, and then save hello configuration.</span></span> <span data-ttu-id="ba66a-123">En la barra de herramientas de hello, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="ba66a-123">On hello toolbar, select **Save**.</span></span>

    ![Guardar la configuración y la configuración de Hola](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    <span data-ttu-id="ba66a-125">Se le notificará si hay configuraciones que necesiten atención.</span><span class="sxs-lookup"><span data-stu-id="ba66a-125">You are notified if any configurations need attention.</span></span> <span data-ttu-id="ba66a-126">Tenga en cuenta los elementos de hello y, a continuación, seleccione **continuar de todos modos**.</span><span class="sxs-lookup"><span data-stu-id="ba66a-126">Note hello items, and then select **Proceed Anyway**.</span></span> 

    ![Selección de Proceed Anyway (Continuar de todos modos)](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    <span data-ttu-id="ba66a-128">Escribir una nota sobre los cambios de configuración de hello y, a continuación, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="ba66a-128">Write a note about hello configuration changes, and then select **Save**.</span></span>

    ![Escriba una nota sobre los cambios de hello realizados](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. <span data-ttu-id="ba66a-130">Cada vez que se guarda una configuración, le preguntarán si servicio de hello toorestart.</span><span class="sxs-lookup"><span data-stu-id="ba66a-130">Whenever a configuration is saved, you are prompted toorestart hello service.</span></span> <span data-ttu-id="ba66a-131">Seleccione **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="ba66a-131">Select **Restart**.</span></span>

    ![Selección de Reiniciar](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    <span data-ttu-id="ba66a-133">Confirme el reinicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba66a-133">Confirm hello restart.</span></span>

    ![Selección de Confirm Restart All (Confirmar reinicio de todo)](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    <span data-ttu-id="ba66a-135">Puede revisar los procesos de Hola que se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="ba66a-135">You can review hello processes that are running.</span></span>

    ![Revisar los procesos en ejecución](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. <span data-ttu-id="ba66a-137">Puede agregar configuraciones.</span><span class="sxs-lookup"><span data-stu-id="ba66a-137">You can add configurations.</span></span> <span data-ttu-id="ba66a-138">En la lista Hola de configuraciones, seleccione **valores predeterminados personalizados-spark2**y, a continuación, seleccione **Agregar propiedad**.</span><span class="sxs-lookup"><span data-stu-id="ba66a-138">In hello list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span></span>

    ![Selección de Agregar propiedad](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. <span data-ttu-id="ba66a-140">Defina una nueva propiedad.</span><span class="sxs-lookup"><span data-stu-id="ba66a-140">Define a new property.</span></span> <span data-ttu-id="ba66a-141">Puede definir una propiedad única mediante un cuadro de diálogo para una configuración específica, como tipo de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba66a-141">You can define a single property by using a dialog box for specific settings such as hello data type.</span></span> <span data-ttu-id="ba66a-142">O bien, puede definir varias propiedades mediante una definición por línea.</span><span class="sxs-lookup"><span data-stu-id="ba66a-142">Or, you can define multiple properties by using one definition per line.</span></span> 

    <span data-ttu-id="ba66a-143">En este ejemplo, Hola **spark.driver.memory** propiedad se define con un valor de **4g**.</span><span class="sxs-lookup"><span data-stu-id="ba66a-143">In this example, hello **spark.driver.memory** property is defined with a value of **4g**.</span></span>

    ![Definir la nueva propiedad](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. <span data-ttu-id="ba66a-145">Guardar configuración de hello y, a continuación, reinicie el servicio de hello tal como se describe en los pasos 6 y 7.</span><span class="sxs-lookup"><span data-stu-id="ba66a-145">Save hello configuration, and then restart hello service as described in steps 6 and 7.</span></span>

<span data-ttu-id="ba66a-146">Estos cambios para todo el clúster, pero pueden reemplazarse cuando se envía el trabajo de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="ba66a-146">These changes are cluster-wide but can be overridden when you submit hello Spark job.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="ba66a-147">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="ba66a-147">Additional reading</span></span>

[<span data-ttu-id="ba66a-148">Envío de trabajos de Spark en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="ba66a-148">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a><span data-ttu-id="ba66a-149">Cómo se configura una aplicación Spark mediante un cuaderno de Jupyter Notebook en clústeres</span><span class="sxs-lookup"><span data-stu-id="ba66a-149">How do I configure a Spark application by using a Jupyter notebook on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="ba66a-150">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="ba66a-150">Resolution steps</span></span>

1. <span data-ttu-id="ba66a-151">vea toodetermine qué configuraciones de Spark necesitan valores de conjunto y toowhat toobe, [¿qué hace que un Spark excepción de aplicación OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="ba66a-151">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="ba66a-152">En la celda primera Hola de hello Jupyter Bloc de notas, después de hello **%% configurar** directiva, especificar configuraciones de Spark hello en formato JSON válido.</span><span class="sxs-lookup"><span data-stu-id="ba66a-152">In hello first cell of hello Jupyter notebook, after hello **%%configure** directive, specify hello Spark configurations in valid JSON format.</span></span> <span data-ttu-id="ba66a-153">Cambiar los valores reales de hello según sea necesario:</span><span class="sxs-lookup"><span data-stu-id="ba66a-153">Change hello actual values as necessary:</span></span>

    ![Agregar una configuración](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a><span data-ttu-id="ba66a-155">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="ba66a-155">Additional reading</span></span>

[<span data-ttu-id="ba66a-156">Envío de trabajos de Spark en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="ba66a-156">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a><span data-ttu-id="ba66a-157">Cómo se configura una aplicación Spark mediante Livy en clústeres</span><span class="sxs-lookup"><span data-stu-id="ba66a-157">How do I configure a Spark application by using Livy on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="ba66a-158">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="ba66a-158">Resolution steps</span></span>

1. <span data-ttu-id="ba66a-159">vea toodetermine qué configuraciones de Spark necesitan valores de conjunto y toowhat toobe, [¿qué hace que un Spark excepción de aplicación OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="ba66a-159">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

2. <span data-ttu-id="ba66a-160">Enviar Hola Spark aplicación tooLivy mediante un cliente REST como cURL.</span><span class="sxs-lookup"><span data-stu-id="ba66a-160">Submit hello Spark application tooLivy by using a REST client like cURL.</span></span> <span data-ttu-id="ba66a-161">Use un comando información similar toohello siguiente.</span><span class="sxs-lookup"><span data-stu-id="ba66a-161">Use a command similar toohello following.</span></span> <span data-ttu-id="ba66a-162">Cambiar los valores reales de hello según sea necesario:</span><span class="sxs-lookup"><span data-stu-id="ba66a-162">Change hello actual values as necessary:</span></span>

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a><span data-ttu-id="ba66a-163">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="ba66a-163">Additional reading</span></span>

[<span data-ttu-id="ba66a-164">Envío de trabajos de Spark en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="ba66a-164">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a><span data-ttu-id="ba66a-165">Cómo se configura una aplicación Spark mediante spark-submit en clústeres</span><span class="sxs-lookup"><span data-stu-id="ba66a-165">How do I configure a Spark application by using spark-submit on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="ba66a-166">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="ba66a-166">Resolution steps</span></span>

1. <span data-ttu-id="ba66a-167">vea toodetermine qué configuraciones de Spark necesitan valores de conjunto y toowhat toobe, [¿qué hace que un Spark excepción de aplicación OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="ba66a-167">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="ba66a-168">Inicie el shell de spark mediante un siguiente toohello similar de comando.</span><span class="sxs-lookup"><span data-stu-id="ba66a-168">Launch spark-shell by using a command similar toohello following.</span></span> <span data-ttu-id="ba66a-169">Cambie el valor real de Hola de configuraciones de Hola según sea necesario:</span><span class="sxs-lookup"><span data-stu-id="ba66a-169">Change hello actual value of hello configurations as necessary:</span></span> 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a><span data-ttu-id="ba66a-170">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="ba66a-170">Additional reading</span></span>

[<span data-ttu-id="ba66a-171">Envío de trabajos de Spark en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="ba66a-171">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a><span data-ttu-id="ba66a-172">Qué produce una excepción OutOfMemoryError en una aplicación Spark</span><span class="sxs-lookup"><span data-stu-id="ba66a-172">What causes a Spark application OutofMemoryError exception</span></span>

### <a name="detailed-description"></a><span data-ttu-id="ba66a-173">Descripción detallada</span><span class="sxs-lookup"><span data-stu-id="ba66a-173">Detailed description</span></span>

<span data-ttu-id="ba66a-174">Hola aplicación Spark produce un error, con los siguientes tipos de excepciones no detectadas de hello:</span><span class="sxs-lookup"><span data-stu-id="ba66a-174">hello Spark application fails, with hello following types of uncaught exceptions:</span></span>

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

### <a name="probable-cause"></a><span data-ttu-id="ba66a-175">Causa probable</span><span class="sxs-lookup"><span data-stu-id="ba66a-175">Probable cause</span></span>

<span data-ttu-id="ba66a-176">Hola más probable de esta excepción es que no hay suficiente memoria en montón se asigna máquinas virtuales de Java toohello (JVMs).</span><span class="sxs-lookup"><span data-stu-id="ba66a-176">hello most likely cause of this exception is that not enough heap memory is allocated toohello Java virtual machines (JVMs).</span></span> <span data-ttu-id="ba66a-177">Estas JVMs se inician como elementos de ejecución o los controladores como parte de la aplicación de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="ba66a-177">These JVMs are launched as executors or drivers as part of hello Spark application.</span></span> 

### <a name="resolution-steps"></a><span data-ttu-id="ba66a-178">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="ba66a-178">Resolution steps</span></span>

1. <span data-ttu-id="ba66a-179">Determinar el tamaño máximo de Hola de identificadores de aplicación de hello datos Hola Spark.</span><span class="sxs-lookup"><span data-stu-id="ba66a-179">Determine hello maximum size of hello data hello Spark application handles.</span></span> <span data-ttu-id="ba66a-180">Puede realizar una estimación basada en tamaño máximo de Hola Hola de datos de entrada, los datos de hello intermedios que se generan al transformar los datos de entrada de Hola y datos de salida de hello que se producen cuando la aplicación hello más está transformando los datos intermedios Hola.</span><span class="sxs-lookup"><span data-stu-id="ba66a-180">You can make a guess based on hello maximum size of hello input data, hello intermediate data that's produced by transforming hello input data, and hello output data that's produced when hello application is further transforming hello intermediate data.</span></span> <span data-ttu-id="ba66a-181">Este proceso puede ser iterativo si no puede realizar una estimación formal inicial.</span><span class="sxs-lookup"><span data-stu-id="ba66a-181">This process can be an iterative if you can't make an initial formal guess.</span></span> 

2. <span data-ttu-id="ba66a-182">Asegúrese de que ese clúster de HDInsight de Hola que se vayan toouse tiene suficientes recursos de memoria y núcleos tooaccommodate Hola Spark una aplicación.</span><span class="sxs-lookup"><span data-stu-id="ba66a-182">Make sure that hello HDInsight cluster that you're going toouse has enough resources in terms of memory and cores tooaccommodate hello Spark application.</span></span> <span data-ttu-id="ba66a-183">Se puede determinar mediante la visualización de la sección de las métricas de clúster Hola de hello YARN UI para los valores de hello de **usa memoria** vs. **Memory Total** (Total de memoria ) y **VCores Used** (VCores usados) frente a **VCores Total** (Total de VCores).</span><span class="sxs-lookup"><span data-stu-id="ba66a-183">You can determine this by viewing hello cluster metrics section of hello YARN UI for hello values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span></span>

3. <span data-ttu-id="ba66a-184">Establecer los valores de tooappropriate de configuraciones, que no deben superar el 90% de memoria disponible de Hola y núcleos de hello después Spark.</span><span class="sxs-lookup"><span data-stu-id="ba66a-184">Set hello following Spark configurations tooappropriate values, which should not exceed 90% of hello available memory and cores.</span></span> <span data-ttu-id="ba66a-185">Hola valores deberían estar bien dentro de los requisitos de memoria de Hola de hello aplicación Spark:</span><span class="sxs-lookup"><span data-stu-id="ba66a-185">hello values should be well within hello memory requirements of hello Spark application:</span></span> 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    <span data-ttu-id="ba66a-186">tooget Hola memoria total utilizada por todos los elementos de ejecución, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="ba66a-186">tooget hello total memory used by all executors, run hello following command:</span></span> 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    <span data-ttu-id="ba66a-187">tooget Hola memoria total utilizada por el controlador de hello, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="ba66a-187">tooget hello total memory used by hello driver, run hello following command:</span></span>
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a><span data-ttu-id="ba66a-188">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="ba66a-188">Additional reading</span></span>

- [<span data-ttu-id="ba66a-189">Información general de la administración de memoria en Spark</span><span class="sxs-lookup"><span data-stu-id="ba66a-189">Spark memory management overview</span></span>](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- <span data-ttu-id="ba66a-190">[Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/) (Depuración de una aplicación Spark en un clúster de HDInsight)</span><span class="sxs-lookup"><span data-stu-id="ba66a-190">[Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)</span></span>

