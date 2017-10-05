---
title: "Habilitación de volcados de montón de los servicios de Hadoop en HDInsight - Azure | Microsoft Docs"
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
ms.openlocfilehash: 59942e989d622c2486edf181d76e13344c71e6f9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="9f46c-103">Habilitación de los volcados de montón de los servicios de Hadoop en HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="9f46c-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="9f46c-104">Los volcados de montón contienen una instantánea de la memoria de la aplicación, incluidos los valores de variables en el momento en el que se creó el volcado de memoria.</span><span class="sxs-lookup"><span data-stu-id="9f46c-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="9f46c-105">Por ello, estos volcados resultan útiles a la hora de diagnosticar cualquier problema que ocurra en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9f46c-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f46c-106">Los pasos de este documento solo funcionan con clústeres de HDInsight que usan Linux.</span><span class="sxs-lookup"><span data-stu-id="9f46c-106">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="9f46c-107">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="9f46c-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9f46c-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9f46c-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="9f46c-109"><a name="whichServices"></a>Servicios</span><span class="sxs-lookup"><span data-stu-id="9f46c-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="9f46c-110">Puede habilitar los volcados de montón en los siguientes servicios:</span><span class="sxs-lookup"><span data-stu-id="9f46c-110">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="9f46c-111">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="9f46c-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="9f46c-112">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="9f46c-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="9f46c-113">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="9f46c-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="9f46c-114">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="9f46c-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="9f46c-115">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="9f46c-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="9f46c-116">También puede habilitar los volcados de montón para los procesos de asignación y ejecución que ejecuta HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f46c-116">You can also enable heap dumps for the map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="9f46c-117"><a name="configuration"></a>Información sobre cómo configurar el volcado de montón</span><span class="sxs-lookup"><span data-stu-id="9f46c-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="9f46c-118">Son las opciones de paso (también conocidas como opciones o parámetros) las que habilitan los volcados de montón en JVM cuando se inicia un servicio.</span><span class="sxs-lookup"><span data-stu-id="9f46c-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) to the JVM when a service is started.</span></span> <span data-ttu-id="9f46c-119">En la mayoría de los servicios de Hadoop, puede modificar el script de shell empleado para iniciar el servicio para pasar estas opciones.</span><span class="sxs-lookup"><span data-stu-id="9f46c-119">For most Hadoop services, you can modify the shell script used to start the service to pass these options.</span></span>

<span data-ttu-id="9f46c-120">En cada script hay una exportación de **\*\_OPTS** que contiene las opciones que se pasan a JVM.</span><span class="sxs-lookup"><span data-stu-id="9f46c-120">In each script, there is an export for **\*\_OPTS**, which contains the options passed to the JVM.</span></span> <span data-ttu-id="9f46c-121">Por ejemplo, en el script **hadoop env.sh**, la línea que comienza con `export HADOOP_NAMENODE_OPTS=` contiene las opciones del servicio NameNode.</span><span class="sxs-lookup"><span data-stu-id="9f46c-121">For example, in the **hadoop-env.sh** script, the line that begins with `export HADOOP_NAMENODE_OPTS=` contains the options for the NameNode service.</span></span>

<span data-ttu-id="9f46c-122">La asignación y reducción de procesos son tareas ligeramente diferentes, ya que se tratan de procesos secundarios del servicio MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9f46c-122">Map and reduce processes are slightly different, as these operations are a child process of the MapReduce service.</span></span> <span data-ttu-id="9f46c-123">Cada proceso de asignación o reducción se ejecuta en un contenedor secundario y existen dos entradas que contienen las opciones de JVM.</span><span class="sxs-lookup"><span data-stu-id="9f46c-123">Each map or reduce process runs in a child container, and there are two entries that contain the JVM options.</span></span> <span data-ttu-id="9f46c-124">Ambos están en **mapred-site.xml**:</span><span class="sxs-lookup"><span data-stu-id="9f46c-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="9f46c-125">**mapreduce.admin.map.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="9f46c-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="9f46c-126">**mapreduce.admin.reduce.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="9f46c-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="9f46c-127">Se recomienda usar Ambari para modificar los scripts y la configuración de mapred-site.xml, puesto que Ambari controla la replicación de los cambios en los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="9f46c-127">We recommend using Ambari to modify both the scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in the cluster.</span></span> <span data-ttu-id="9f46c-128">Consulte la sección [Uso de Ambari](#using-ambari) para obtener los pasos específicos que debe dar.</span><span class="sxs-lookup"><span data-stu-id="9f46c-128">See the [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="9f46c-129">Habilitar los volcados de montón</span><span class="sxs-lookup"><span data-stu-id="9f46c-129">Enable heap dumps</span></span>

<span data-ttu-id="9f46c-130">La siguiente opción habilita los volcados del montón cuando se produce un OutOfMemoryError:</span><span class="sxs-lookup"><span data-stu-id="9f46c-130">The following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="9f46c-131">El símbolo **+** indica que esta opción está habilitada,</span><span class="sxs-lookup"><span data-stu-id="9f46c-131">The **+** indicates that this option is enabled.</span></span> <span data-ttu-id="9f46c-132">ya que está deshabilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9f46c-132">The default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="9f46c-133">Los volcados de montón no están habilitados para los servicios Hadoop en HDInsight, ya que el tamaño de los archivos de volcado puede ser grande.</span><span class="sxs-lookup"><span data-stu-id="9f46c-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as the dump files can be large.</span></span> <span data-ttu-id="9f46c-134">Si los habilita para solucionar problemas, no olvide deshabilitarlos una vez haya reproducido el problema y recopilado los archivos de volcado.</span><span class="sxs-lookup"><span data-stu-id="9f46c-134">If you do enable them for troubleshooting, remember to disable them once you have reproduced the problem and gathered the dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="9f46c-135">Ubicación de volcado</span><span class="sxs-lookup"><span data-stu-id="9f46c-135">Dump location</span></span>

<span data-ttu-id="9f46c-136">La ubicación predeterminada del archivo de volcado es el directorio en el cual está trabajando.</span><span class="sxs-lookup"><span data-stu-id="9f46c-136">The default location for the dump file is the current working directory.</span></span> <span data-ttu-id="9f46c-137">Puede decidir dónde guardar el archivo con la siguiente opción:</span><span class="sxs-lookup"><span data-stu-id="9f46c-137">You can control where the file is stored using the following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="9f46c-138">Por ejemplo, al usar `-XX:HeapDumpPath=/tmp`, los volcados se almacenarán en el directorio /tmp.</span><span class="sxs-lookup"><span data-stu-id="9f46c-138">For example, using `-XX:HeapDumpPath=/tmp` causes the dumps to be stored in the /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="9f46c-139">Scripts</span><span class="sxs-lookup"><span data-stu-id="9f46c-139">Scripts</span></span>

<span data-ttu-id="9f46c-140">También puede desencadenar un script cuando se produzca un error **OutOfMemoryError** .</span><span class="sxs-lookup"><span data-stu-id="9f46c-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="9f46c-141">Por ejemplo, puede desencadenar una notificación que le avise de que el error se ha producido.</span><span class="sxs-lookup"><span data-stu-id="9f46c-141">For example, triggering a notification so you know that the error has occurred.</span></span> <span data-ttu-id="9f46c-142">Utilice la siguiente opción para desencadenar un script en un error __OutOfMemoryError__:</span><span class="sxs-lookup"><span data-stu-id="9f46c-142">Use the following option to trigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="9f46c-143">Puesto que Hadoop es un sistema distribuido, debe colocar cualquier script que use en todos los nodos del clúster que ejecute el servicio.</span><span class="sxs-lookup"><span data-stu-id="9f46c-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in the cluster that the service runs on.</span></span>
> 
> <span data-ttu-id="9f46c-144">Asimismo, el script debe estar en una ubicación que sea accesible para la cuenta con la cual se ejecuta el servicio y deberá proporcionar permisos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9f46c-144">The script must also be in a location that is accessible by the account the service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="9f46c-145">A modo de ejemplo, es posible que desee almacenar los scripts en `/usr/local/bin` y usar `chmod go+rx /usr/local/bin/filename.sh` para conceder permisos de ejecución y lectura.</span><span class="sxs-lookup"><span data-stu-id="9f46c-145">For example, you may wish to store scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` to grant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="9f46c-146">Uso de Ambari</span><span class="sxs-lookup"><span data-stu-id="9f46c-146">Using Ambari</span></span>

<span data-ttu-id="9f46c-147">Para modificar la configuración de un servicio, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9f46c-147">To modify the configuration for a service, use the following steps:</span></span>

1. <span data-ttu-id="9f46c-148">Abra la interfaz de usuario web Ambari del clúster.</span><span class="sxs-lookup"><span data-stu-id="9f46c-148">Open the Ambari web UI for your cluster.</span></span> <span data-ttu-id="9f46c-149">La dirección URL es https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="9f46c-149">The URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="9f46c-150">Cuando se le solicite, deberá autenticarse en el sitio mediante el nombre de cuenta HTTP (nombre predeterminado: admin) y la contraseña del clúster.</span><span class="sxs-lookup"><span data-stu-id="9f46c-150">When prompted, authenticate to the site using the HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9f46c-151">Es posible que Ambari le pida de nuevo que escriba el nombre de usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="9f46c-151">You may be prompted a second time by Ambari for the user name and password.</span></span> <span data-ttu-id="9f46c-152">Si es así, escriba el mismo nombre de cuenta y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="9f46c-152">If so, enter the same account name and password</span></span>

2. <span data-ttu-id="9f46c-153">En la lista de la izquierda, seleccione el área de servicio que desea modificar.</span><span class="sxs-lookup"><span data-stu-id="9f46c-153">Using the list of on the left, select the service area you want to modify.</span></span> <span data-ttu-id="9f46c-154">Por ejemplo, **HDFS**.</span><span class="sxs-lookup"><span data-stu-id="9f46c-154">For example, **HDFS**.</span></span> <span data-ttu-id="9f46c-155">En el área central, seleccione la ficha **Configuraciones** .</span><span class="sxs-lookup"><span data-stu-id="9f46c-155">In the center area, select the **Configs** tab.</span></span>

    ![Imagen de la web de Ambari web con la ficha de configuración HDFS seleccionada](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="9f46c-157">Mediante la entrada **Filtrar...**, escriba **opciones**.</span><span class="sxs-lookup"><span data-stu-id="9f46c-157">Using the **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="9f46c-158">Solo se muestran los elementos que contienen este texto.</span><span class="sxs-lookup"><span data-stu-id="9f46c-158">Only items containing this text are displayed.</span></span>

    ![Lista filtrada](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="9f46c-160">Busque la entrada **\*\_OPTS** del servicio en el cual desea habilitar los volcados de montón y agregue las opciones que desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="9f46c-160">Find the **\*\_OPTS** entry for the service you want to enable heap dumps for, and add the options you wish to enable.</span></span> <span data-ttu-id="9f46c-161">En la siguiente imagen, he agregado `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` a la entrada **HADOOP\_NAMENODE\_OPTS**:</span><span class="sxs-lookup"><span data-stu-id="9f46c-161">In the following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` to the **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![HADOOP_NAMENODE_OPTS con -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="9f46c-163">Al habilitar los volcados de montón para el proceso secundario de asignación o reducción, busque los campos con los nombres **mapreduce.admin.map.child.java.opts** y **mapreduce.admin.reduce.child.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="9f46c-163">When enabling heap dumps for the map or reduce child process, look for the fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="9f46c-164">Presione el botón **Guardar** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="9f46c-164">Use the **Save** button to save the changes.</span></span> <span data-ttu-id="9f46c-165">Puede elaborar una nota breve en la que se describan los cambios.</span><span class="sxs-lookup"><span data-stu-id="9f46c-165">You can enter a short note describing the changes.</span></span>

5. <span data-ttu-id="9f46c-166">Una vez que se hayan aplicado los cambios, aparecerá el icono **Es necesario reiniciar** junto a uno o más servicios.</span><span class="sxs-lookup"><span data-stu-id="9f46c-166">Once the changes have been applied, the **Restart required** icon appears beside one or more services.</span></span>

    ![icono «Es necesario reiniciar» y botón de reinicio](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="9f46c-168">Seleccione cada uno de los servicios que necesite reiniciar y pulse el botón **Acciones de servicio** para seleccionar la opción **Activar modo de mantenimiento**.</span><span class="sxs-lookup"><span data-stu-id="9f46c-168">Select each service that needs a restart, and use the **Service Actions** button to **Turn On Maintenance Mode**.</span></span> <span data-ttu-id="9f46c-169">El modo de mantenimiento evita que se generen alertas desde el servicio al reiniciarlo.</span><span class="sxs-lookup"><span data-stu-id="9f46c-169">Maintenance mode prevents alerts from being generated from the service when you restart it.</span></span>

    ![Activar el menú del modo de mantenimiento](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="9f46c-171">Una vez habilitado el modo de mantenimiento, pulse el botón **Reiniciar** para que el servicio pueda **Reiniciar todos los afectados**</span><span class="sxs-lookup"><span data-stu-id="9f46c-171">Once you have enabled maintenance mode, use the **Restart** button for the service to **Restart All Effected**</span></span>

    ![Reiniciar todas las entradas afectadas](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="9f46c-173">es posible que las entradas del botón **Reiniciar** botón sean diferentes en otros servicios.</span><span class="sxs-lookup"><span data-stu-id="9f46c-173">the entries for the **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="9f46c-174">Una vez haya reiniciado los servicios, pulse el botón **Acciones de servicio** para **Desactivar el modo de mantenimiento**.</span><span class="sxs-lookup"><span data-stu-id="9f46c-174">Once the services have been restarted, use the **Service Actions** button to **Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="9f46c-175">Esto hará que Ambari reanude la supervisión de alertas para el servicio.</span><span class="sxs-lookup"><span data-stu-id="9f46c-175">This Ambari to resume monitoring for alerts for the service.</span></span>

