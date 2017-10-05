---
title: "Solución de problemas de YARN mediante Azure HDInsight | Microsoft Docs"
description: "Obtenga respuestas a las preguntas más comunes sobre cómo trabajar con Apache Hadoop YARN y Azure HDInsight."
keywords: "Azure HDInsight, YARN, preguntas más frecuentes, guía de solución de problemas, preguntas comunes"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: F76786A9-99AB-4B85-9B15-CA03528FC4CD
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: 63f2d88ad59661b7fbcffd0aaeb94c58d40bdb73
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a><span data-ttu-id="2fc38-104">Solución de problemas de YARN mediante Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2fc38-104">Troubleshoot YARN by using Azure HDInsight</span></span>

<span data-ttu-id="2fc38-105">Obtenga información sobre los principales problemas y sus soluciones al trabajar con cargas útiles de Apache Hadoop YARN en Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="2fc38-105">Learn about the top issues and their resolutions when working with Apache Hadoop YARN payloads in Apache Ambari.</span></span>

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a><span data-ttu-id="2fc38-106">Creación de una nueva cola de YARN en un clúster</span><span class="sxs-lookup"><span data-stu-id="2fc38-106">How do I create a new YARN queue on a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="2fc38-107">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="2fc38-107">Resolution steps</span></span> 

<span data-ttu-id="2fc38-108">Para crear una nueva cola de YARN y equilibrar la asignación de capacidad en todas las colas, siga estos pasos en Ambari.</span><span class="sxs-lookup"><span data-stu-id="2fc38-108">Use the following steps in Ambari to create a new YARN queue, and then balance the capacity allocation among all the queues.</span></span> 

<span data-ttu-id="2fc38-109">En este ejemplo, se cambia la capacidad de las dos colas existentes (**default** (predeterminado) y **thriftsvr**) del 50% al 25%, lo que proporciona una capacidad del 50% a la nueva cola (spark).</span><span class="sxs-lookup"><span data-stu-id="2fc38-109">In this example, two existing queues (**default** and **thriftsvr**) both are changed from 50% capacity to 25% capacity, which gives the new queue (spark) 50% capacity.</span></span>
| <span data-ttu-id="2fc38-110">Cola</span><span class="sxs-lookup"><span data-stu-id="2fc38-110">Queue</span></span> | <span data-ttu-id="2fc38-111">Capacity</span><span class="sxs-lookup"><span data-stu-id="2fc38-111">Capacity</span></span> | <span data-ttu-id="2fc38-112">Capacidad máxima</span><span class="sxs-lookup"><span data-stu-id="2fc38-112">Maximum capacity</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2fc38-113">default</span><span class="sxs-lookup"><span data-stu-id="2fc38-113">default</span></span> | <span data-ttu-id="2fc38-114">25 %</span><span class="sxs-lookup"><span data-stu-id="2fc38-114">25%</span></span> | <span data-ttu-id="2fc38-115">50 %</span><span class="sxs-lookup"><span data-stu-id="2fc38-115">50%</span></span> |
| <span data-ttu-id="2fc38-116">thrftsvr</span><span class="sxs-lookup"><span data-stu-id="2fc38-116">thrftsvr</span></span> | <span data-ttu-id="2fc38-117">25 %</span><span class="sxs-lookup"><span data-stu-id="2fc38-117">25%</span></span> | <span data-ttu-id="2fc38-118">50 %</span><span class="sxs-lookup"><span data-stu-id="2fc38-118">50%</span></span> |
| <span data-ttu-id="2fc38-119">spark</span><span class="sxs-lookup"><span data-stu-id="2fc38-119">spark</span></span> | <span data-ttu-id="2fc38-120">50 %</span><span class="sxs-lookup"><span data-stu-id="2fc38-120">50%</span></span> | <span data-ttu-id="2fc38-121">50 %</span><span class="sxs-lookup"><span data-stu-id="2fc38-121">50%</span></span> |

1. <span data-ttu-id="2fc38-122">Seleccione el icono **Ambari Views** (Vistas de Ambari) y, a continuación, seleccione el patrón de cuadrícula.</span><span class="sxs-lookup"><span data-stu-id="2fc38-122">Select the **Ambari Views** icon, and then select the grid pattern.</span></span> <span data-ttu-id="2fc38-123">A continuación, seleccione **YARN Queue Manager** (Administrador de colas de YARN).</span><span class="sxs-lookup"><span data-stu-id="2fc38-123">Next, select **YARN Queue Manager**.</span></span>

    ![Selección del icono Vistas de Ambari](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. <span data-ttu-id="2fc38-125">Seleccione la cola **default**.</span><span class="sxs-lookup"><span data-stu-id="2fc38-125">Select the **default** queue.</span></span>

    ![Selección de la cola default (predeterminada)](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. <span data-ttu-id="2fc38-127">Para la cola **default**, cambie la **capacidad** del 50% al 25%.</span><span class="sxs-lookup"><span data-stu-id="2fc38-127">For the **default** queue, change the **capacity** from 50% to 25%.</span></span> <span data-ttu-id="2fc38-128">Para la cola **thriftsvr**, cambie la **capacidad** al 25%.</span><span class="sxs-lookup"><span data-stu-id="2fc38-128">For the **thriftsvr** queue, change the **capacity** to 25%.</span></span>

    ![Cambio de la capacidad al 25 % para las colas default y thriftsvr](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. <span data-ttu-id="2fc38-130">Seleccione **Add Queue** (Agregar cola) para crear una nueva cola.</span><span class="sxs-lookup"><span data-stu-id="2fc38-130">To create a new queue, select **Add Queue**.</span></span>

    ![Selección de Agregar cola](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. <span data-ttu-id="2fc38-132">Asigne un nombre a la cola nueva.</span><span class="sxs-lookup"><span data-stu-id="2fc38-132">Name the new queue.</span></span>

    ![Asignación del nombre Spark a la cola](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. <span data-ttu-id="2fc38-134">Deje los valores de **Capacity** (Capacidad) en el 50 % y seleccione el botón **Actions** (Acciones).</span><span class="sxs-lookup"><span data-stu-id="2fc38-134">Leave the **capacity** values at 50%, and then select the **Actions** button.</span></span>

    ![Selección del botón Actions (Acciones)](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. <span data-ttu-id="2fc38-136">Seleccione **Save and Refresh Queues** (Guardar y actualizar colas).</span><span class="sxs-lookup"><span data-stu-id="2fc38-136">Select **Save and Refresh Queues**.</span></span>

    ![Selección de Save and Refresh Queues (Guardar y actualizar colas)](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

<span data-ttu-id="2fc38-138">Estos cambios están visibles inmediatamente en la interfaz de usuario de YARN Scheduler.</span><span class="sxs-lookup"><span data-stu-id="2fc38-138">These changes are visible immediately on the YARN Scheduler UI.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="2fc38-139">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="2fc38-139">Additional reading</span></span>

- [<span data-ttu-id="2fc38-140">YARN CapacityScheduler</span><span class="sxs-lookup"><span data-stu-id="2fc38-140">YARN CapacityScheduler</span></span>](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a><span data-ttu-id="2fc38-141">Descarga de los registros de YARN desde un clúster</span><span class="sxs-lookup"><span data-stu-id="2fc38-141">How do I download YARN logs from a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="2fc38-142">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="2fc38-142">Resolution steps</span></span> 

1. <span data-ttu-id="2fc38-143">Conéctese al clúster de HDInsight con un cliente Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="2fc38-143">Connect to the HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="2fc38-144">Para más información, consulte [Lecturas adicionales](#additional-reading-2).</span><span class="sxs-lookup"><span data-stu-id="2fc38-144">For more information, see [Additional reading](#additional-reading-2).</span></span>

2. <span data-ttu-id="2fc38-145">Enumere todos los identificadores de aplicación de las aplicaciones Yarn que se están ejecutando con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2fc38-145">To list all the application IDs of the YARN applications that are currently running, run the following command:</span></span>

    ```apache
    yarn top
    ```
    <span data-ttu-id="2fc38-146">Los identificadores aparecen en la columna **APPLICATIONID**.</span><span class="sxs-lookup"><span data-stu-id="2fc38-146">The IDs are listed in the **APPLICATIONID** column.</span></span> <span data-ttu-id="2fc38-147">Puede descargar los registros desde la columna **APPLICATIONID**.</span><span class="sxs-lookup"><span data-stu-id="2fc38-147">You can download logs from the **APPLICATIONID** column.</span></span>

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. <span data-ttu-id="2fc38-148">Descargue los registros de contenedor de YARN para todos los maestros de aplicación con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2fc38-148">To download YARN container logs for all application masters, use the following command:</span></span>
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    <span data-ttu-id="2fc38-149">Este comando crea un archivo de registro denominado amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="2fc38-149">This command creates a log file named amlogs.txt.</span></span> 

4. <span data-ttu-id="2fc38-150">Descargue los registros de contenedor de YARN solo para el maestro de aplicación más reciente con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2fc38-150">To download YARN container logs for only the latest application master, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    <span data-ttu-id="2fc38-151">Este comando crea un archivo de registro denominado latestamlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="2fc38-151">This command creates a log file named latestamlogs.txt.</span></span> 

4. <span data-ttu-id="2fc38-152">Descargue los registros de contenedor de YARN para los dos primeros maestros de aplicación con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2fc38-152">To download YARN container logs for the first two application masters, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    <span data-ttu-id="2fc38-153">Este comando crea un archivo de registro denominado first2amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="2fc38-153">This command creates a log file named first2amlogs.txt.</span></span> 

5. <span data-ttu-id="2fc38-154">Descargue todos los registros de contenedor de YARN con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2fc38-154">To download all YARN container logs, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    <span data-ttu-id="2fc38-155">Este comando crea un archivo de registro denominado logs.txt.</span><span class="sxs-lookup"><span data-stu-id="2fc38-155">This command creates a log file named logs.txt.</span></span> 

6. <span data-ttu-id="2fc38-156">Descargue el registro de YARN de un contenedor determinado con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2fc38-156">To download the YARN container log for a specific container, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    <span data-ttu-id="2fc38-157">Este comando crea un archivo de registro denominado containerlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="2fc38-157">This command creates a log file named containerlogs.txt.</span></span>

### <span data-ttu-id="2fc38-158"><a name="additional-reading-2"></a>Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="2fc38-158"><a name="additional-reading-2"></a>Additional reading</span></span>

- [<span data-ttu-id="2fc38-159">Conexión a HDInsight (Hadoop) a través de SSH</span><span class="sxs-lookup"><span data-stu-id="2fc38-159">Connect to HDInsight (Hadoop) by using SSH</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- <span data-ttu-id="2fc38-160">[Apache Hadoop Yarn concepts and applications](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/) (Conceptos y aplicaciones de YARN en Apache Hadoop)</span><span class="sxs-lookup"><span data-stu-id="2fc38-160">[Apache Hadoop YARN concepts and applications](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)</span></span>







