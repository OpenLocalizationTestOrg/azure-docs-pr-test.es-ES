---
title: "volcados de memoria de montón aaaEnable para los servicios de Hadoop en HDInsight - Azure | Documentos de Microsoft"
description: "Habilitar los volcados de montón de los servicios de Hadoop en los clústeres de HDInsight basado en Linux para la depuración y el análisis."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8f151adb-f687-41e4-aca0-82b551953725
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 49e30f26e1a83f19e068e9da253b5548caec70d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="42efb-103">Habilitación de los volcados de montón de los servicios de Hadoop en HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="42efb-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="42efb-104">Los volcados del montón contienen una instantánea de memoria de la aplicación hello, incluidos los valores de hello de variables en tiempo de Hola se creó el volcado de Hola.</span><span class="sxs-lookup"><span data-stu-id="42efb-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="42efb-105">Por ello, estos volcados resultan útiles a la hora de diagnosticar cualquier problema que ocurra en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="42efb-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42efb-106">Hello pasos descritos en este documento solo funcionan con clústeres de HDInsight que utilizan Linux.</span><span class="sxs-lookup"><span data-stu-id="42efb-106">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="42efb-107">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="42efb-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="42efb-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="42efb-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="42efb-109"><a name="whichServices"></a>Servicios</span><span class="sxs-lookup"><span data-stu-id="42efb-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="42efb-110">Puede habilitar los volcados del montón para hello siguientes servicios:</span><span class="sxs-lookup"><span data-stu-id="42efb-110">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="42efb-111">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="42efb-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="42efb-112">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="42efb-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="42efb-113">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="42efb-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="42efb-114">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="42efb-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="42efb-115">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="42efb-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="42efb-116">También puede habilitar los volcados del montón para asignación de Hola y reducir los procesos que se ejecutaban por HDInsight.</span><span class="sxs-lookup"><span data-stu-id="42efb-116">You can also enable heap dumps for hello map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="42efb-117"><a name="configuration"></a>Información sobre cómo configurar el volcado de montón</span><span class="sxs-lookup"><span data-stu-id="42efb-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="42efb-118">Se habilitan los volcados del montón pasando opciones (a veces conocido como opts, o parámetros) toohello JVM cuando se inicia un servicio.</span><span class="sxs-lookup"><span data-stu-id="42efb-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) toohello JVM when a service is started.</span></span> <span data-ttu-id="42efb-119">La mayoría de los servicios Hadoop, puede modificar estas opciones de hello shell script utilizado toostart Hola servicio toopass.</span><span class="sxs-lookup"><span data-stu-id="42efb-119">For most Hadoop services, you can modify hello shell script used toostart hello service toopass these options.</span></span>

<span data-ttu-id="42efb-120">En cada secuencia de comandos, hay una exportación para  **\* \_OPTS**, que contiene opciones de hello pasa toohello JVM.</span><span class="sxs-lookup"><span data-stu-id="42efb-120">In each script, there is an export for **\*\_OPTS**, which contains hello options passed toohello JVM.</span></span> <span data-ttu-id="42efb-121">Por ejemplo, en hello **hadoop env.sh** en un script, línea hello que comienza con `export HADOOP_NAMENODE_OPTS=` contiene las opciones de Hola para hello NameNode servicio.</span><span class="sxs-lookup"><span data-stu-id="42efb-121">For example, in hello **hadoop-env.sh** script, hello line that begins with `export HADOOP_NAMENODE_OPTS=` contains hello options for hello NameNode service.</span></span>

<span data-ttu-id="42efb-122">Asignación y reducción procesos son ligeramente diferentes, ya que estas operaciones son un proceso secundario de hello MapReduce servicio.</span><span class="sxs-lookup"><span data-stu-id="42efb-122">Map and reduce processes are slightly different, as these operations are a child process of hello MapReduce service.</span></span> <span data-ttu-id="42efb-123">Cada uno de ellos se asignan o reducir el proceso se ejecuta en un contenedor secundario, y hay dos entradas que contienen opciones de JVM Hola.</span><span class="sxs-lookup"><span data-stu-id="42efb-123">Each map or reduce process runs in a child container, and there are two entries that contain hello JVM options.</span></span> <span data-ttu-id="42efb-124">Ambos están en **mapred-site.xml**:</span><span class="sxs-lookup"><span data-stu-id="42efb-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="42efb-125">**mapreduce.admin.map.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="42efb-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="42efb-126">**mapreduce.admin.reduce.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="42efb-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="42efb-127">Se recomienda con Ambari toomodify ambos Hola scripts y configuración mapred-site.xml, como Ambari controlar replicar cambios en nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="42efb-127">We recommend using Ambari toomodify both hello scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in hello cluster.</span></span> <span data-ttu-id="42efb-128">Vea hello [Ambari utilizando](#using-ambari) sección para obtener pasos específicos.</span><span class="sxs-lookup"><span data-stu-id="42efb-128">See hello [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="42efb-129">Habilitar los volcados de montón</span><span class="sxs-lookup"><span data-stu-id="42efb-129">Enable heap dumps</span></span>

<span data-ttu-id="42efb-130">Hello siguiente opción permite que los volcados del montón cuando se produce un OutOfMemoryError:</span><span class="sxs-lookup"><span data-stu-id="42efb-130">hello following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="42efb-131">Hola  **+**  indica que esta opción está habilitada.</span><span class="sxs-lookup"><span data-stu-id="42efb-131">hello **+** indicates that this option is enabled.</span></span> <span data-ttu-id="42efb-132">Hola predeterminado está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="42efb-132">hello default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="42efb-133">Los volcados del montón no están habilitados para los servicios de Hadoop en HDInsight de forma predeterminada, como archivos de volcado de hello pueden ser grandes.</span><span class="sxs-lookup"><span data-stu-id="42efb-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as hello dump files can be large.</span></span> <span data-ttu-id="42efb-134">Si habilitarlas para solucionar el problema, recuerde toodisable ellos una vez que ha reproducido Hola problema y archivos de volcado de hello recopilada.</span><span class="sxs-lookup"><span data-stu-id="42efb-134">If you do enable them for troubleshooting, remember toodisable them once you have reproduced hello problem and gathered hello dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="42efb-135">Ubicación de volcado</span><span class="sxs-lookup"><span data-stu-id="42efb-135">Dump location</span></span>

<span data-ttu-id="42efb-136">ubicación predeterminada de Hello para el archivo de volcado de memoria de hello es el directorio de trabajo actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="42efb-136">hello default location for hello dump file is hello current working directory.</span></span> <span data-ttu-id="42efb-137">Puede controlar dónde hello archivo se almacena utilizando Hola después de opción:</span><span class="sxs-lookup"><span data-stu-id="42efb-137">You can control where hello file is stored using hello following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="42efb-138">Por ejemplo, si se usa `-XX:HeapDumpPath=/tmp` hace Hola volcados toobe almacenado en el directorio de Hola/tmp.</span><span class="sxs-lookup"><span data-stu-id="42efb-138">For example, using `-XX:HeapDumpPath=/tmp` causes hello dumps toobe stored in hello /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="42efb-139">Scripts</span><span class="sxs-lookup"><span data-stu-id="42efb-139">Scripts</span></span>

<span data-ttu-id="42efb-140">También puede desencadenar un script cuando se produzca un error **OutOfMemoryError** .</span><span class="sxs-lookup"><span data-stu-id="42efb-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="42efb-141">Por ejemplo, se ha producido desencadenar una notificación para que sepa que error Hola.</span><span class="sxs-lookup"><span data-stu-id="42efb-141">For example, triggering a notification so you know that hello error has occurred.</span></span> <span data-ttu-id="42efb-142">Siguiente de hello utilice opción tootrigger una secuencia de comandos en un __OutOfMemoryError__:</span><span class="sxs-lookup"><span data-stu-id="42efb-142">Use hello following option tootrigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="42efb-143">Puesto que Hadoop es un sistema distribuido, se debe colocar cualquier secuencia de comandos utilizada en todos los nodos de clúster de Hola que se ejecuta el servicio de hello en.</span><span class="sxs-lookup"><span data-stu-id="42efb-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in hello cluster that hello service runs on.</span></span>
> 
> <span data-ttu-id="42efb-144">script de Hola debe también ser en una ubicación que sea accesible para hello cuenta Hola se ejecuta el servicio como y debe proporcionar permisos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="42efb-144">hello script must also be in a location that is accessible by hello account hello service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="42efb-145">Por ejemplo, podría desear toostore scripts en `/usr/local/bin` y usar `chmod go+rx /usr/local/bin/filename.sh` toogrant permisos read y execute.</span><span class="sxs-lookup"><span data-stu-id="42efb-145">For example, you may wish toostore scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` toogrant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="42efb-146">Uso de Ambari</span><span class="sxs-lookup"><span data-stu-id="42efb-146">Using Ambari</span></span>

<span data-ttu-id="42efb-147">configuración de hello toomodify para un servicio, Hola uso pasos:</span><span class="sxs-lookup"><span data-stu-id="42efb-147">toomodify hello configuration for a service, use hello following steps:</span></span>

1. <span data-ttu-id="42efb-148">Abra hello Ambari web interfaz de usuario para el clúster.</span><span class="sxs-lookup"><span data-stu-id="42efb-148">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="42efb-149">dirección URL de Hello es https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="42efb-149">hello URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="42efb-150">Cuando se le solicite, autenticar sitio toohello con el nombre de la cuenta de hello HTTP (valor predeterminado: administrador) y la contraseña para el clúster.</span><span class="sxs-lookup"><span data-stu-id="42efb-150">When prompted, authenticate toohello site using hello HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="42efb-151">Se le pedirá una segunda vez por Ambari por nombre de usuario de Hola y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="42efb-151">You may be prompted a second time by Ambari for hello user name and password.</span></span> <span data-ttu-id="42efb-152">Si es así, escriba Hola el mismo nombre de cuenta y contraseña</span><span class="sxs-lookup"><span data-stu-id="42efb-152">If so, enter hello same account name and password</span></span>

2. <span data-ttu-id="42efb-153">En lista de Hola de hello izquierda, seleccione el área de servicio de hello desea toomodify.</span><span class="sxs-lookup"><span data-stu-id="42efb-153">Using hello list of on hello left, select hello service area you want toomodify.</span></span> <span data-ttu-id="42efb-154">Por ejemplo, **HDFS**.</span><span class="sxs-lookup"><span data-stu-id="42efb-154">For example, **HDFS**.</span></span> <span data-ttu-id="42efb-155">En el área central de hello, seleccione hello **configuraciones** ficha.</span><span class="sxs-lookup"><span data-stu-id="42efb-155">In hello center area, select hello **Configs** tab.</span></span>

    ![Imagen de la web de Ambari web con la ficha de configuración HDFS seleccionada](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="42efb-157">Con hello **filtro...**  entrada, escriba **opts**.</span><span class="sxs-lookup"><span data-stu-id="42efb-157">Using hello **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="42efb-158">Solo se muestran los elementos que contienen este texto.</span><span class="sxs-lookup"><span data-stu-id="42efb-158">Only items containing this text are displayed.</span></span>

    ![Lista filtrada](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="42efb-160">Buscar hello  **\* \_OPTS** entrada de servicio de Hola que desee tooenable los volcados del montón para y agrega Hola opciones que desea tooenable.</span><span class="sxs-lookup"><span data-stu-id="42efb-160">Find hello **\*\_OPTS** entry for hello service you want tooenable heap dumps for, and add hello options you wish tooenable.</span></span> <span data-ttu-id="42efb-161">Hola después de la imagen, he agregado `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** entrada:</span><span class="sxs-lookup"><span data-stu-id="42efb-161">In hello following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![HADOOP_NAMENODE_OPTS con -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="42efb-163">Al habilitar los volcados del montón para hello asignarán o reducen el proceso secundario, busque campos Hola denominados **mapreduce.admin.map.child.java.opts** y **mapreduce.admin.reduce.child.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="42efb-163">When enabling heap dumps for hello map or reduce child process, look for hello fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="42efb-164">Hola de uso **guardar** botón toosave Hola cambiará.</span><span class="sxs-lookup"><span data-stu-id="42efb-164">Use hello **Save** button toosave hello changes.</span></span> <span data-ttu-id="42efb-165">Puede escribir una nota breve que describe los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="42efb-165">You can enter a short note describing hello changes.</span></span>

5. <span data-ttu-id="42efb-166">Una vez que se han aplicado los cambios de hello, Hola **debe reiniciarse** icono aparece junto a uno o varios servicios.</span><span class="sxs-lookup"><span data-stu-id="42efb-166">Once hello changes have been applied, hello **Restart required** icon appears beside one or more services.</span></span>

    ![icono «Es necesario reiniciar» y botón de reinicio](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="42efb-168">Seleccione cada servicio que requiere un reinicio y usar hello **acciones de servicio** botón demasiado**en modo de mantenimiento**.</span><span class="sxs-lookup"><span data-stu-id="42efb-168">Select each service that needs a restart, and use hello **Service Actions** button too**Turn On Maintenance Mode**.</span></span> <span data-ttu-id="42efb-169">Modo de mantenimiento evita que las alertas se generan desde el servicio de Hola durante el reinicio.</span><span class="sxs-lookup"><span data-stu-id="42efb-169">Maintenance mode prevents alerts from being generated from hello service when you restart it.</span></span>

    ![Activar el menú del modo de mantenimiento](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="42efb-171">Una vez que se ha habilitado el modo de mantenimiento, usar hello **reiniciar** botón para servicio de hello demasiado**reiniciar realiza todas las**</span><span class="sxs-lookup"><span data-stu-id="42efb-171">Once you have enabled maintenance mode, use hello **Restart** button for hello service too**Restart All Effected**</span></span>

    ![Reiniciar todas las entradas afectadas](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="42efb-173">Hola entradas para hello **reiniciar** botón puede ser diferente para otros servicios.</span><span class="sxs-lookup"><span data-stu-id="42efb-173">hello entries for hello **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="42efb-174">Una vez que se hayan reiniciado los servicios de hello, usar hello **acciones de servicio** botón demasiado**activar el modo de mantenimiento**.</span><span class="sxs-lookup"><span data-stu-id="42efb-174">Once hello services have been restarted, use hello **Service Actions** button too**Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="42efb-175">Este tooresume Ambari supervisión de alertas de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="42efb-175">This Ambari tooresume monitoring for alerts for hello service.</span></span>

