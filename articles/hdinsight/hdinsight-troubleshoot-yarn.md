---
title: aaaTroubleshoot YARN mediante el uso de HDInsight de Azure | Documentos de Microsoft
description: "Obtenga respuestas toocommon preguntas sobre cómo trabajar con Apache Hadoop YARN y HDInsight de Azure."
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
ms.openlocfilehash: 800d9738cb27e05a64db470ee58565af3b85aa99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a><span data-ttu-id="4694d-104">Solución de problemas de YARN mediante Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4694d-104">Troubleshoot YARN by using Azure HDInsight</span></span>

<span data-ttu-id="4694d-105">Obtenga información acerca de los principales problemas de Hola y sus soluciones cuando se trabaja con cargas de Apache Hadoop YARN en Ambari de Apache.</span><span class="sxs-lookup"><span data-stu-id="4694d-105">Learn about hello top issues and their resolutions when working with Apache Hadoop YARN payloads in Apache Ambari.</span></span>

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a><span data-ttu-id="4694d-106">Creación de una nueva cola de YARN en un clúster</span><span class="sxs-lookup"><span data-stu-id="4694d-106">How do I create a new YARN queue on a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="4694d-107">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="4694d-107">Resolution steps</span></span> 

<span data-ttu-id="4694d-108">A continuación Hola use los pasos de Ambari toocreate una nueva cola YARN y equilibrar, a continuación, la asignación de capacidad de hello entre todas las colas de Hola.</span><span class="sxs-lookup"><span data-stu-id="4694d-108">Use hello following steps in Ambari toocreate a new YARN queue, and then balance hello capacity allocation among all hello queues.</span></span> 

<span data-ttu-id="4694d-109">En este ejemplo, dos colas existentes (**predeterminado** y **thriftsvr**) ambos se cambian de 50% capacidad too25% de la capacidad, que proporciona la nueva capacidad de 50% de cola (spark) Hola.</span><span class="sxs-lookup"><span data-stu-id="4694d-109">In this example, two existing queues (**default** and **thriftsvr**) both are changed from 50% capacity too25% capacity, which gives hello new queue (spark) 50% capacity.</span></span>
| <span data-ttu-id="4694d-110">Cola</span><span class="sxs-lookup"><span data-stu-id="4694d-110">Queue</span></span> | <span data-ttu-id="4694d-111">Capacity</span><span class="sxs-lookup"><span data-stu-id="4694d-111">Capacity</span></span> | <span data-ttu-id="4694d-112">Capacidad máxima</span><span class="sxs-lookup"><span data-stu-id="4694d-112">Maximum capacity</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4694d-113">default</span><span class="sxs-lookup"><span data-stu-id="4694d-113">default</span></span> | <span data-ttu-id="4694d-114">25 %</span><span class="sxs-lookup"><span data-stu-id="4694d-114">25%</span></span> | <span data-ttu-id="4694d-115">50 %</span><span class="sxs-lookup"><span data-stu-id="4694d-115">50%</span></span> |
| <span data-ttu-id="4694d-116">thrftsvr</span><span class="sxs-lookup"><span data-stu-id="4694d-116">thrftsvr</span></span> | <span data-ttu-id="4694d-117">25 %</span><span class="sxs-lookup"><span data-stu-id="4694d-117">25%</span></span> | <span data-ttu-id="4694d-118">50 %</span><span class="sxs-lookup"><span data-stu-id="4694d-118">50%</span></span> |
| <span data-ttu-id="4694d-119">spark</span><span class="sxs-lookup"><span data-stu-id="4694d-119">spark</span></span> | <span data-ttu-id="4694d-120">50 %</span><span class="sxs-lookup"><span data-stu-id="4694d-120">50%</span></span> | <span data-ttu-id="4694d-121">50 %</span><span class="sxs-lookup"><span data-stu-id="4694d-121">50%</span></span> |

1. <span data-ttu-id="4694d-122">Seleccione hello **Ambari vistas** icono y el patrón de cuadrícula de hello, a continuación, seleccione.</span><span class="sxs-lookup"><span data-stu-id="4694d-122">Select hello **Ambari Views** icon, and then select hello grid pattern.</span></span> <span data-ttu-id="4694d-123">A continuación, seleccione **YARN Queue Manager** (Administrador de colas de YARN).</span><span class="sxs-lookup"><span data-stu-id="4694d-123">Next, select **YARN Queue Manager**.</span></span>

    ![Seleccione Hola vistas Ambari icono](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. <span data-ttu-id="4694d-125">Seleccione hello **predeterminado** cola.</span><span class="sxs-lookup"><span data-stu-id="4694d-125">Select hello **default** queue.</span></span>

    ![Seleccione Hola predeterminado cola](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. <span data-ttu-id="4694d-127">Para hello **predeterminado** de cola, cambie hello **capacidad** del 50% too25%.</span><span class="sxs-lookup"><span data-stu-id="4694d-127">For hello **default** queue, change hello **capacity** from 50% too25%.</span></span> <span data-ttu-id="4694d-128">Para hello **thriftsvr** de cola, cambie hello **capacidad** too25%.</span><span class="sxs-lookup"><span data-stu-id="4694d-128">For hello **thriftsvr** queue, change hello **capacity** too25%.</span></span>

    ![Cambiar la capacidad de hello too25% para las colas de forma predeterminada y thriftsvr de Hola](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. <span data-ttu-id="4694d-130">toocreate una nueva cola, seleccione **agregar cola**.</span><span class="sxs-lookup"><span data-stu-id="4694d-130">toocreate a new queue, select **Add Queue**.</span></span>

    ![Selección de Agregar cola](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. <span data-ttu-id="4694d-132">Nombre hello nueva cola.</span><span class="sxs-lookup"><span data-stu-id="4694d-132">Name hello new queue.</span></span>

    ![Nombre de cola de hello Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. <span data-ttu-id="4694d-134">Deje hello **capacidad** valores al 50% y, a continuación, seleccione hello **acciones** botón.</span><span class="sxs-lookup"><span data-stu-id="4694d-134">Leave hello **capacity** values at 50%, and then select hello **Actions** button.</span></span>

    ![Seleccione el botón de acciones de Hola](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. <span data-ttu-id="4694d-136">Seleccione **Save and Refresh Queues** (Guardar y actualizar colas).</span><span class="sxs-lookup"><span data-stu-id="4694d-136">Select **Save and Refresh Queues**.</span></span>

    ![Selección de Save and Refresh Queues (Guardar y actualizar colas)](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

<span data-ttu-id="4694d-138">Estos cambios son visibles inmediatamente en hello YARN programador UI.</span><span class="sxs-lookup"><span data-stu-id="4694d-138">These changes are visible immediately on hello YARN Scheduler UI.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="4694d-139">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="4694d-139">Additional reading</span></span>

- [<span data-ttu-id="4694d-140">YARN CapacityScheduler</span><span class="sxs-lookup"><span data-stu-id="4694d-140">YARN CapacityScheduler</span></span>](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a><span data-ttu-id="4694d-141">Descarga de los registros de YARN desde un clúster</span><span class="sxs-lookup"><span data-stu-id="4694d-141">How do I download YARN logs from a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="4694d-142">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="4694d-142">Resolution steps</span></span> 

1. <span data-ttu-id="4694d-143">Conecta el clúster de HDInsight de toohello con un cliente de Shell seguro (SSH).</span><span class="sxs-lookup"><span data-stu-id="4694d-143">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="4694d-144">Para más información, consulte [Lecturas adicionales](#additional-reading-2).</span><span class="sxs-lookup"><span data-stu-id="4694d-144">For more information, see [Additional reading](#additional-reading-2).</span></span>

2. <span data-ttu-id="4694d-145">toolist todos Hola Id. de aplicación de las aplicaciones de hilo de Hola que se están ejecutando, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4694d-145">toolist all hello application IDs of hello YARN applications that are currently running, run hello following command:</span></span>

    ```apache
    yarn top
    ```
    <span data-ttu-id="4694d-146">Hello identificadores aparecen en hello **APPLICATIONID** columna.</span><span class="sxs-lookup"><span data-stu-id="4694d-146">hello IDs are listed in hello **APPLICATIONID** column.</span></span> <span data-ttu-id="4694d-147">Puede descargar los registros de hello **APPLICATIONID** columna.</span><span class="sxs-lookup"><span data-stu-id="4694d-147">You can download logs from hello **APPLICATIONID** column.</span></span>

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

3. <span data-ttu-id="4694d-148">registros de contenedor YARN toodownload para todos los patrones de aplicación, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4694d-148">toodownload YARN container logs for all application masters, use hello following command:</span></span>
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    <span data-ttu-id="4694d-149">Este comando crea un archivo de registro denominado amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="4694d-149">This command creates a log file named amlogs.txt.</span></span> 

4. <span data-ttu-id="4694d-150">registros de contenedor YARN toodownload para solo Hola última aplicación maestra, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4694d-150">toodownload YARN container logs for only hello latest application master, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    <span data-ttu-id="4694d-151">Este comando crea un archivo de registro denominado latestamlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="4694d-151">This command creates a log file named latestamlogs.txt.</span></span> 

4. <span data-ttu-id="4694d-152">registros de contenedor YARN toodownload para patrones de aplicación dos primera hello, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4694d-152">toodownload YARN container logs for hello first two application masters, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    <span data-ttu-id="4694d-153">Este comando crea un archivo de registro denominado first2amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="4694d-153">This command creates a log file named first2amlogs.txt.</span></span> 

5. <span data-ttu-id="4694d-154">toodownload todos los registros de contenedor de hilo, utilice Hola comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="4694d-154">toodownload all YARN container logs, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    <span data-ttu-id="4694d-155">Este comando crea un archivo de registro denominado logs.txt.</span><span class="sxs-lookup"><span data-stu-id="4694d-155">This command creates a log file named logs.txt.</span></span> 

6. <span data-ttu-id="4694d-156">registro de contenedor de toodownload hello YARN para un contenedor específico, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4694d-156">toodownload hello YARN container log for a specific container, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    <span data-ttu-id="4694d-157">Este comando crea un archivo de registro denominado containerlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="4694d-157">This command creates a log file named containerlogs.txt.</span></span>

### <span data-ttu-id="4694d-158"><a name="additional-reading-2"></a>Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="4694d-158"><a name="additional-reading-2"></a>Additional reading</span></span>

- [<span data-ttu-id="4694d-159">Conectar tooHDInsight (Hadoop) a través de SSH</span><span class="sxs-lookup"><span data-stu-id="4694d-159">Connect tooHDInsight (Hadoop) by using SSH</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- <span data-ttu-id="4694d-160">[Apache Hadoop Yarn concepts and applications](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/) (Conceptos y aplicaciones de YARN en Apache Hadoop)</span><span class="sxs-lookup"><span data-stu-id="4694d-160">[Apache Hadoop YARN concepts and applications](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)</span></span>







