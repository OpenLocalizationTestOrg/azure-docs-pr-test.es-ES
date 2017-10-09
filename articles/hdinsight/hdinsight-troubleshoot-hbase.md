---
title: aaaTroubleshoot HBase mediante el uso de HDInsight de Azure | Documentos de Microsoft
description: "Obtenga respuestas toocommon preguntas sobre cómo trabajar con HBase y HDInsight de Azure."
services: hdinsight
documentationcenter: 
author: nitinver
manager: ashitg
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 7/7/2017
ms.author: nitinver
ms.openlocfilehash: 5210184f8ea95628952a95df8c98f5b98e37c53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a><span data-ttu-id="4cbd9-103">Solución de problemas de HBase mediante Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4cbd9-103">Troubleshoot HBase by using Azure HDInsight</span></span>

<span data-ttu-id="4cbd9-104">Obtener información sobre problemas principales de Hola y sus soluciones cuando se trabaja con cargas de Apache HBase en Ambari de Apache.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-104">Learn about hello top issues and their resolutions when working with Apache HBase payloads in Apache Ambari.</span></span>

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a><span data-ttu-id="4cbd9-105">Cómo se ejecutan informes de comando hbck con varias regiones sin asignar</span><span class="sxs-lookup"><span data-stu-id="4cbd9-105">How do I run hbck command reports with multiple unassigned regions</span></span>

<span data-ttu-id="4cbd9-106">Un mensaje de error comunes que podría ver al ejecutar hello `hbase hbck` comando es "varias regiones está sin asignar o agujeros en cadena Hola de regiones."</span><span class="sxs-lookup"><span data-stu-id="4cbd9-106">A common error message that you might see when you run hello `hbase hbck` command is "multiple regions being unassigned or holes in hello chain of regions."</span></span>

<span data-ttu-id="4cbd9-107">Hola HBase Master UI, puede ver número Hola de regiones que no están equilibrados en todos los servidores de la región.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-107">In hello HBase Master UI, you can see hello number of regions that are unbalanced across all region servers.</span></span> <span data-ttu-id="4cbd9-108">A continuación, puede ejecutar `hbase hbck` comando toosee vulnerabilidades de cadena de la región de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-108">Then, you can run `hbase hbck` command toosee holes in hello region chain.</span></span>

<span data-ttu-id="4cbd9-109">Vulnerabilidades pueden deberse regiones de hello sin conexión, por lo que las asignaciones de Hola de corrección en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-109">Holes might be caused by hello offline regions, so fix hello assignments first.</span></span> 

<span data-ttu-id="4cbd9-110">toobring Hola sin asignar regiones tooa espera el estado normal, completar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4cbd9-110">toobring hello unassigned regions back tooa normal state, complete hello following steps:</span></span>

1. <span data-ttu-id="4cbd9-111">Inicie sesión en toohello clúster de HBase para HDInsight a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-111">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="4cbd9-112">tooconnect con shell de ZooKeeper hello, ejecute hello `hbase zkcli` comando.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-112">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="4cbd9-113">Ejecute hello `rmr /hbase/regions-in-transition` comando o hello `rmr /hbase-unsecure/regions-in-transition` comando.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-113">Run hello `rmr /hbase/regions-in-transition` command or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="4cbd9-114">tooexit de hello `hbase zkcli` de shell, use hello `exit` comando.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-114">tooexit from hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="4cbd9-115">Abra Hola Apache Ambari UI y, a continuación, reinicie el servicio de Active HBase Master de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-115">Open hello Apache Ambari UI, and then restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="4cbd9-116">Ejecute hello `hbase hbck` comando nuevo (sin ninguna opción).</span><span class="sxs-lookup"><span data-stu-id="4cbd9-116">Run hello `hbase hbck` command again (without any options).</span></span> <span data-ttu-id="4cbd9-117">Compruebe la salida de hello de este tooensure de comando que se está asignando todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-117">Check hello output of this command tooensure that all regions are being assigned.</span></span>


## <span data-ttu-id="4cbd9-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Cómo se solucionan los problemas de tiempo de espera cuando se usan comandos hbck para las asignaciones de regiones</span><span class="sxs-lookup"><span data-stu-id="4cbd9-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>How do I fix timeout issues when using hbck commands for region assignments</span></span>

### <a name="issue"></a><span data-ttu-id="4cbd9-119">Problema</span><span class="sxs-lookup"><span data-stu-id="4cbd9-119">Issue</span></span>

<span data-ttu-id="4cbd9-120">Una posible causa de problemas de tiempo de espera al usar hello `hbck` comando podría ser que varias regiones son Hola "en"transición de estado durante mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-120">A potential cause for timeout issues when you use hello `hbck` command might be that several regions are in hello "in transition" state for a long time.</span></span> <span data-ttu-id="4cbd9-121">Puede ver esas regiones como sin conexión en hello UI Master de HBase.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-121">You can see those regions as offline in hello HBase Master UI.</span></span> <span data-ttu-id="4cbd9-122">Dado que un gran número de regiones estás intentando tootransition, Master HBase podría tiempo de espera y toobring no se puede esas regiones en línea.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-122">Because a high number of regions are attempting tootransition, HBase Master might timeout and be unable toobring those regions back online.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="4cbd9-123">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="4cbd9-123">Resolution steps</span></span>

1. <span data-ttu-id="4cbd9-124">Inicie sesión en toohello clúster de HBase para HDInsight a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-124">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="4cbd9-125">tooconnect con shell de ZooKeeper hello, ejecute hello `hbase zkcli` comando.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-125">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="4cbd9-126">Ejecute hello `rmr /hbase/regions-in-transition` o hello `rmr /hbase-unsecure/regions-in-transition` comando.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-126">Run hello `rmr /hbase/regions-in-transition` or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="4cbd9-127">Hola tooexit `hbase zkcli` de shell, use hello `exit` comando.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-127">tooexit hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="4cbd9-128">Hola Ambari UI, reinicie el servicio de Active HBase Master de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-128">In hello Ambari UI, restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="4cbd9-129">Ejecute hello `hbase hbck -fixAssignments` comando nuevo.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-129">Run hello `hbase hbck -fixAssignments` command again.</span></span>

## <span data-ttu-id="4cbd9-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Cómo forzar la deshabilitación del modo seguro de HDFS en un clúster</span><span class="sxs-lookup"><span data-stu-id="4cbd9-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>How do I force-disable HDFS safe mode in a cluster</span></span>

### <a name="issue"></a><span data-ttu-id="4cbd9-131">Problema</span><span class="sxs-lookup"><span data-stu-id="4cbd9-131">Issue</span></span>

<span data-ttu-id="4cbd9-132">Hola local Hadoop distribuidas archivo sistema (HDFS) está atascada en el modo seguro en clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-132">hello local Hadoop Distributed File System (HDFS) is stuck in safe mode on hello HDInsight cluster.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="4cbd9-133">Descripción detallada</span><span class="sxs-lookup"><span data-stu-id="4cbd9-133">Detailed description</span></span>

<span data-ttu-id="4cbd9-134">Este error podría deberse a un error al ejecutar Hola siguiente HDFS comando:</span><span class="sxs-lookup"><span data-stu-id="4cbd9-134">This error might be caused by a failure when you run hello following HDFS command:</span></span>

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

<span data-ttu-id="4cbd9-135">error de Hello que vean cuando intente el comando de hello toorun tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="4cbd9-135">hello error you might see when you try toorun hello command looks like this:</span></span>

```apache
hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" tooturn safe mode off.
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkNameNodeSafeMode(FSNamesystem.java:1359)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.mkdirs(FSNamesystem.java:4010)
        at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.mkdirs(NameNodeRpcServer.java:1102)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.mkdirs(ClientNamenodeProtocolServerSideTranslatorPB.java:630)
        at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:640)
        at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:982)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2313)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2309)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:422)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1724)
        at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2307)
        at org.apache.hadoop.ipc.Client.getRpcResponse(Client.java:1552)
        at org.apache.hadoop.ipc.Client.call(Client.java:1496)
        at org.apache.hadoop.ipc.Client.call(Client.java:1396)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:233)
        at com.sun.proxy.$Proxy10.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolTranslatorPB.mkdirs(ClientNamenodeProtocolTranslatorPB.java:603)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:278)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:194)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:176)
        at com.sun.proxy.$Proxy11.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.DFSClient.primitiveMkdir(DFSClient.java:3061)
        at org.apache.hadoop.hdfs.DFSClient.mkdirs(DFSClient.java:3031)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1162)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1158)
        at org.apache.hadoop.fs.FileSystemLinkResolver.resolve(FileSystemLinkResolver.java:81)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirsInternal(DistributedFileSystem.java:1158)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirs(DistributedFileSystem.java:1150)
        at org.apache.hadoop.fs.FileSystem.mkdirs(FileSystem.java:1898)
        at org.apache.hadoop.fs.shell.Mkdir.processNonexistentPath(Mkdir.java:76)
        at org.apache.hadoop.fs.shell.Command.processArgument(Command.java:273)
        at org.apache.hadoop.fs.shell.Command.processArguments(Command.java:255)
        at org.apache.hadoop.fs.shell.FsCommand.processRawArguments(FsCommand.java:119)
        at org.apache.hadoop.fs.shell.Command.run(Command.java:165)
        at org.apache.hadoop.fs.FsShell.run(FsShell.java:297)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:90)
        at org.apache.hadoop.fs.FsShell.main(FsShell.java:350)
mkdir: Cannot create directory /temp. Name node is in safe mode.
```

### <a name="probable-cause"></a><span data-ttu-id="4cbd9-136">Causa probable</span><span class="sxs-lookup"><span data-stu-id="4cbd9-136">Probable cause</span></span>

<span data-ttu-id="4cbd9-137">Hello clúster de HDInsight ha sido reducida tooa muy pocos nodos.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-137">hello HDInsight cluster has been scaled down tooa very few nodes.</span></span> <span data-ttu-id="4cbd9-138">Hola o número de nodos está por debajo de cerrar el factor de replicación de toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-138">hello number of nodes is below or close toohello HDFS replication factor.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="4cbd9-139">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="4cbd9-139">Resolution steps</span></span> 

1. <span data-ttu-id="4cbd9-140">Obtener estado de Hola de hello que HDFS en hello HDInsight de clúster mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="4cbd9-140">Get hello status of hello HDFS on hello HDInsight cluster by running hello following commands:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   ```

   ```apache
   hdiuser@hn0-spark2:~$ hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   Safe mode is ON
   Configured Capacity: 3372381241344 (3.07 TB)
   Present Capacity: 3138625077248 (2.85 TB)
   DFS Remaining: 3102710317056 (2.82 TB)
   DFS Used: 35914760192 (33.45 GB)
   DFS Used%: 1.14%
   Under replicated blocks: 0
   Blocks with corrupt replicas: 0
   Missing blocks: 0
   Missing blocks (with replication factor 1): 0

   -------------------------------------------------
   Live datanodes (8):

   Name: 10.0.0.17:30010 (10.0.0.17)
   Hostname: 10.0.0.17
   Decommission Status : Normal
   Configured Capacity: 421547655168 (392.60 GB)
   DFS Used: 5288128512 (4.92 GB)
   Non DFS Used: 29087272960 (27.09 GB)
   DFS Remaining: 387172253696 (360.58 GB)
   DFS Used%: 1.25%
   DFS Remaining%: 91.85%
   Configured Cache Capacity: 0 (0 B)
   Cache Used: 0 (0 B)
   Cache Remaining: 0 (0 B)
   Cache Used%: 100.00%
   Cache Remaining%: 0.00%
   Xceivers: 2
   Last contact: Wed Apr 05 16:22:00 UTC 2017
   ...

   ```
2. <span data-ttu-id="4cbd9-141">También puede comprobar integridad de Hola de hello que HDFS en hello HDInsight clúster mediante Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="4cbd9-141">You also can check hello integrity of hello HDFS on hello HDInsight cluster by using hello following commands:</span></span>

   ```apache
   hdiuser@hn0-spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
   ```

   ```apache
   Connecting toonamenode via http://hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net:30070/fsck?ugi=hdiuser&path=%2F
   FSCK started by hdiuser (auth:SIMPLE) from /10.0.0.22 for path / at Wed Apr 05 16:40:28 UTC 2017
   ....................................................................................................

   ....................................................................................................
   ..................Status: HEALTHY
   Total size:    9330539472 B
   Total dirs:    37
   Total files:   2618
   Total symlinks:                0 (Files currently being written: 2)
   Total blocks (validated):      2535 (avg. block size 3680686 B)
   Minimally replicated blocks:   2535 (100.0 %)
   Over-replicated blocks:        0 (0.0 %)
   Under-replicated blocks:       0 (0.0 %)
   Mis-replicated blocks:         0 (0.0 %)
   Default replication factor:    3
   Average block replication:     3.0
   Corrupt blocks:                0
   Missing replicas:              0 (0.0 %)
   Number of data-nodes:          8
   Number of racks:               1
   FSCK ended at Wed Apr 05 16:40:28 UTC 2017 in 187 milliseconds

   hello filesystem under path '/' is HEALTHY
   ```

3. <span data-ttu-id="4cbd9-142">Si determina que no hay ningún bloques que falta, está dañados o under-replicados, o que pueden hacer caso omiso de los bloques, ejecute hello después de nodo de nombre de comando tootake Hola fuera del modo seguro:</span><span class="sxs-lookup"><span data-stu-id="4cbd9-142">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run hello following command tootake hello name node out of safe mode:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a><span data-ttu-id="4cbd9-143">Cómo se solucionan los problemas de conectividad de JDBC o SQLLine con Apache Phoenix</span><span class="sxs-lookup"><span data-stu-id="4cbd9-143">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="4cbd9-144">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="4cbd9-144">Resolution steps</span></span>

<span data-ttu-id="4cbd9-145">tooconnect con Phoenix, debe proporcionar la dirección IP de Hola de un nodo activo de ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-145">tooconnect with Phoenix, you must provide hello IP address of an active ZooKeeper node.</span></span> <span data-ttu-id="4cbd9-146">Asegúrese de que hello ZooKeeper está tratando de servicio toowhich sqlline.py tooconnect está en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-146">Ensure that hello ZooKeeper service toowhich sqlline.py is trying tooconnect is up and running.</span></span>
1. <span data-ttu-id="4cbd9-147">Inicie sesión en toohello clúster de HDInsight a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-147">Sign in toohello HDInsight cluster by using SSH.</span></span>
2. <span data-ttu-id="4cbd9-148">Escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="4cbd9-148">Enter hello following command:</span></span>
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > <span data-ttu-id="4cbd9-149">Puede obtener la dirección IP de Hola de nodo de hello activo ZooKeeper de hello Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-149">You can get hello IP address of hello active ZooKeeper node from hello Ambari UI.</span></span> <span data-ttu-id="4cbd9-150">Vaya demasiado**HBase** > **vínculos rápidos** > **ZK\* (Active)** > **Zookeeper información**.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-150">Go too**HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info**.</span></span> 

3. <span data-ttu-id="4cbd9-151">Si sqlline.py Hola se conecta tooPhoenix y tiempo de espera no lo hace, siguiente ejecución Hola comando toovalidate disponibilidad de Hola y el estado de Phoenix:</span><span class="sxs-lookup"><span data-stu-id="4cbd9-151">If hello sqlline.py connects tooPhoenix and does not timeout, run hello following command toovalidate hello availability and health of Phoenix:</span></span>

   ```apache
           !tables
           !quit
   ```      
4. <span data-ttu-id="4cbd9-152">Si el comando funciona, no hay ningún problema.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-152">If this command works, there is no issue.</span></span> <span data-ttu-id="4cbd9-153">dirección IP de Hello proporcionada por usuario de hello podría ser incorrecta.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-153">hello IP address provided by hello user might be incorrect.</span></span> <span data-ttu-id="4cbd9-154">Sin embargo, si el comando hello pone en pausa durante un período prolongado y, a continuación, muestra hello tras error, continuar toostep 5.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-154">However, if hello command pauses for an extended time and then displays hello following error, continue toostep 5.</span></span>

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. <span data-ttu-id="4cbd9-155">Ejecute hello siguientes comandos de condición de hello nodo principal (hn0) toodiagnose Hola de hello Phoenix sistema. Tabla del catálogo:</span><span class="sxs-lookup"><span data-stu-id="4cbd9-155">Run hello following commands from hello head node (hn0) toodiagnose hello condition of hello Phoenix SYSTEM.CATALOG table:</span></span>

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   <span data-ttu-id="4cbd9-156">comando de Hello debe devolver una continuación toohello similar de error:</span><span class="sxs-lookup"><span data-stu-id="4cbd9-156">hello command should return an error similar toohello following:</span></span> 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. <span data-ttu-id="4cbd9-157">Hola Ambari UI, realizar Hola después de servicio de HMaster de Hola de toorestart de pasos en todos los nodos de ZooKeeper:</span><span class="sxs-lookup"><span data-stu-id="4cbd9-157">In hello Ambari UI, complete hello following steps toorestart hello HMaster service on all ZooKeeper nodes:</span></span>

    1. <span data-ttu-id="4cbd9-158">Hola **resumen** sección de HBase, vaya demasiado**HBase** > **Active HBase Master**.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-158">In hello **Summary** section of HBase, go too**HBase** > **Active HBase Master**.</span></span> 
    2. <span data-ttu-id="4cbd9-159">Hola **componentes** sección, reinicie el servicio de HBase Master Hola.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-159">In hello **Components** section, restart hello HBase Master service.</span></span>
    3. <span data-ttu-id="4cbd9-160">Repita estos para todos los servicios **Standby HBase Master** restantes.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-160">Repeat these steps for all remaining **Standby HBase Master** services.</span></span> 

<span data-ttu-id="4cbd9-161">Puede tardar minutos toofive Hola Master HBase servicio toostabilize y finalizar el proceso de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-161">It can take up toofive minutes for hello HBase Master service toostabilize and finish hello recovery process.</span></span> <span data-ttu-id="4cbd9-162">Después de unos minutos, repita hello sqlline.py comandos tooconfirm ese sistema Hola. Tabla del catálogo está activo y que TI puede consultarse.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-162">After a few minutes, repeat hello sqlline.py commands tooconfirm that hello SYSTEM.CATALOG table is up, and that it can be queried.</span></span> 

<span data-ttu-id="4cbd9-163">Hola al sistema. Tabla del catálogo es toonormal atrás, tooPhoenix de problema de conectividad de hello debería resolverse automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-163">When hello SYSTEM.CATALOG table is back toonormal, hello connectivity issue tooPhoenix should be automatically resolved.</span></span>


## <a name="what-causes-a-master-server-toofail-toostart"></a><span data-ttu-id="4cbd9-164">¿Qué hace que un servidor maestro toofail toostart</span><span class="sxs-lookup"><span data-stu-id="4cbd9-164">What causes a master server toofail toostart</span></span>

### <a name="error"></a><span data-ttu-id="4cbd9-165">Error</span><span class="sxs-lookup"><span data-stu-id="4cbd9-165">Error</span></span> 

<span data-ttu-id="4cbd9-166">Se produce un error de cambio de nombre atómico.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-166">An atomic renaming failure occurs.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="4cbd9-167">Descripción detallada</span><span class="sxs-lookup"><span data-stu-id="4cbd9-167">Detailed description</span></span>

<span data-ttu-id="4cbd9-168">Durante el proceso de inicio de hello, HMaster completa muchos pasos de inicialización.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-168">During hello startup process, HMaster completes many initialization steps.</span></span> <span data-ttu-id="4cbd9-169">Puede tratarse de mover datos desde el principio de hello (.tmp) carpeta toohello la carpeta de datos.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-169">These include moving data from hello scratch (.tmp) folder toohello data folder.</span></span> <span data-ttu-id="4cbd9-170">HMaster también busca en la carpeta toosee de hello registros de escritura anticipada (WALs) si no hay ningún servidor de la región que no responde, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-170">HMaster also looks at hello write-ahead logs (WALs) folder toosee if there are any unresponsive region servers, and so on.</span></span> 

<span data-ttu-id="4cbd9-171">Durante el inicio, HMaster realiza un comando `list` básico en estas carpetas.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-171">During startup, HMaster does a basic `list` command on these folders.</span></span> <span data-ttu-id="4cbd9-172">Si en algún momento HMaster ve un archivo inesperado en cualquiera de estas carpetas, genera una excepción y no se inicia.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-172">If at any time, HMaster sees an unexpected file in any of these folders, it throws an exception and doesn't start.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="4cbd9-173">Causa probable</span><span class="sxs-lookup"><span data-stu-id="4cbd9-173">Probable cause</span></span>

<span data-ttu-id="4cbd9-174">En los registros de servidor de región de hello, realice escala de tiempo de tooidentify Hola Hola de creación del archivo y, a continuación, compruebe si se ha producido que un bloqueo del proceso alrededor de hello hora Hola archivo se creó.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-174">In hello region server logs, try tooidentify hello timeline of hello file creation, and then see if there was a process crash around hello time hello file was created.</span></span> <span data-ttu-id="4cbd9-175">(Póngase en contacto con tooassist de soporte técnico de HBase en hacerlo.) Esto nos ayuda a proporcionar mecanismos más robustos para que pueda evitar toparse con este error y asegurarse apagados de procesos correctos.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-175">(Contact HBase support tooassist you in doing this.) This helps us provide more robust mechanisms, so that you can avoid hitting this bug, and ensure graceful process shutdowns.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="4cbd9-176">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="4cbd9-176">Resolution steps</span></span>

<span data-ttu-id="4cbd9-177">Compruebe la pila de llamadas de hello e inténtelo toodetermine qué carpeta podría estar causando el problema de hello (por ejemplo, podría ser carpeta de WALs de Hola u Hola .tmp).</span><span class="sxs-lookup"><span data-stu-id="4cbd9-177">Check hello call stack and try toodetermine which folder might be causing hello problem (for instance, it might be hello WALs folder or hello .tmp folder).</span></span> <span data-ttu-id="4cbd9-178">A continuación, en el Explorador de la nube o mediante comandos HDFS, pruebe con toolocate Hola problema.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-178">Then, in Cloud Explorer or by using HDFS commands, try toolocate hello problem file.</span></span> <span data-ttu-id="4cbd9-179">Normalmente, es un archivo \*-renamePending.json.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-179">Usually, this is a \*-renamePending.json file.</span></span> <span data-ttu-id="4cbd9-180">(hello \*-renamePending.json archivo es un archivo de diario que ha utilizado la operación atómica de cambio de nombre de tooimplement hello en el controlador WASB Hola.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-180">(hello \*-renamePending.json file is a journal file that's used tooimplement hello atomic rename operation in hello WASB driver.</span></span> <span data-ttu-id="4cbd9-181">Mucha toobugs en esta implementación, estos archivos pueden ser restantes después de bloqueos de procesos y así sucesivamente.) Fuerce la eliminación de este archivo en Cloud Explorer o mediante los comandos de HDFS.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-181">Due toobugs in this implementation, these files can be left over after process crashes, and so on.) Force-delete this file either in Cloud Explorer or by using HDFS commands.</span></span> 

<span data-ttu-id="4cbd9-182">En ocasiones, en esta ubicación también puede haber un archivo temporal denominado algo así como *$$$. $$$*.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-182">Sometimes, there might also be a temporary file named something like *$$$.$$$* at this location.</span></span> <span data-ttu-id="4cbd9-183">Tiene toouse HDFS `ls` comando toosee este archivo; no puede ver el archivo hello en el explorador en la nube.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-183">You have toouse HDFS `ls` command toosee this file; you cannot see hello file in Cloud Explorer.</span></span> <span data-ttu-id="4cbd9-184">toodelete este archivo, use Hola HDFS comando `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-184">toodelete this file, use hello HDFS command `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span></span>  

<span data-ttu-id="4cbd9-185">Una vez que haya ejecutado estos comandos, HMaster debería iniciarse de inmediato.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-185">After you've run these commands, HMaster should start immediately.</span></span> 

### <a name="error"></a><span data-ttu-id="4cbd9-186">Error</span><span class="sxs-lookup"><span data-stu-id="4cbd9-186">Error</span></span>

<span data-ttu-id="4cbd9-187">No se enumera ninguna dirección de servidor en *hbase: meta* para la región xxx.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-187">No server address is listed in *hbase: meta* for region xxx.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="4cbd9-188">Descripción detallada</span><span class="sxs-lookup"><span data-stu-id="4cbd9-188">Detailed description</span></span>

<span data-ttu-id="4cbd9-189">Puede aparecer un mensaje en el clúster de Linux que indica que hello *hbase: meta* tabla no está en línea.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-189">You might see a message on your Linux cluster that indicates that hello *hbase: meta* table is not online.</span></span> <span data-ttu-id="4cbd9-190">La ejecución de `hbck` puede notificar que "No se encuentra la tabla hbase: meta replicaId 0 en ninguna región".</span><span class="sxs-lookup"><span data-stu-id="4cbd9-190">Running `hbck` might report that "hbase: meta table replicaId 0 is not found on any region."</span></span> <span data-ttu-id="4cbd9-191">posible problema de Hola que HMaster no se pudo inicializar una vez reiniciado HBase.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-191">hello problem might be that HMaster could not initialize after you restarted HBase.</span></span> <span data-ttu-id="4cbd9-192">En los registros de HMaster hello, podría ver mensajes de bienvenida: "ninguna dirección de servidor enumerados en hbase: meta para región hbase: copia de seguridad \<nombre de la región\>".</span><span class="sxs-lookup"><span data-stu-id="4cbd9-192">In hello HMaster logs, you might see hello message: "No server address listed in hbase: meta for region hbase: backup \<region name\>".</span></span>  

### <a name="resolution-steps"></a><span data-ttu-id="4cbd9-193">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="4cbd9-193">Resolution steps</span></span>

1. <span data-ttu-id="4cbd9-194">Hola shell de HBase, escriba Hola después de comandos (valores reales de cambio según corresponda):</span><span class="sxs-lookup"><span data-stu-id="4cbd9-194">In hello HBase shell, enter hello following commands (change actual values as applicable):</span></span>  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. <span data-ttu-id="4cbd9-195">Eliminar hello *hbase: espacio de nombres* entrada.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-195">Delete hello *hbase: namespace* entry.</span></span> <span data-ttu-id="4cbd9-196">Esta entrada podría ser Hola mismo error que se va a notificar cuando hello *hbase: espacio de nombres* se examina la tabla.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-196">This entry might be hello same error that's being reported when hello *hbase: namespace* table is scanned.</span></span>

3. <span data-ttu-id="4cbd9-197">toobring de HBase en un estado de ejecución, en hello Ambari UI, reinicie el servicio de Active HMaster de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-197">toobring up HBase in a running state, in hello Ambari UI, restart hello Active HMaster service.</span></span>  

4. <span data-ttu-id="4cbd9-198">Hola shell de HBase, toobring todas las tablas sin conexión, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4cbd9-198">In hello HBase shell, toobring up all offline tables, run hello following command:</span></span>

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a><span data-ttu-id="4cbd9-199">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="4cbd9-199">Additional reading</span></span>

[<span data-ttu-id="4cbd9-200">Tabla de HBase de hello tooprocess no se puede</span><span class="sxs-lookup"><span data-stu-id="4cbd9-200">Unable tooprocess hello HBase table</span></span>](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a><span data-ttu-id="4cbd9-201">Error</span><span class="sxs-lookup"><span data-stu-id="4cbd9-201">Error</span></span>

<span data-ttu-id="4cbd9-202">Agota el tiempo de espera del HMaster con un too"java.io.IOException similar de excepción grave: 300000ms de tiempo de espera agotado esperando toobe de la tabla de espacio de nombres asignado."</span><span class="sxs-lookup"><span data-stu-id="4cbd9-202">HMaster times out with a fatal exception similar too"java.io.IOException: Timedout 300000ms waiting for namespace table toobe assigned."</span></span>

### <a name="detailed-description"></a><span data-ttu-id="4cbd9-203">Descripción detallada</span><span class="sxs-lookup"><span data-stu-id="4cbd9-203">Detailed description</span></span>

<span data-ttu-id="4cbd9-204">Este problema puede aparecer si hay muchas tablas y regiones que no se han vaciado al reiniciar los servicios de HMaster.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-204">You might experience this issue if you have many tables and regions that have not been flushed when you restart your HMaster services.</span></span> <span data-ttu-id="4cbd9-205">Podría producirse un error de reinicio y verá Hola precede el mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-205">Restart might fail, and you'll see hello preceding error message.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="4cbd9-206">Causa probable</span><span class="sxs-lookup"><span data-stu-id="4cbd9-206">Probable cause</span></span>

<span data-ttu-id="4cbd9-207">Se trata de un problema conocido con hello HMaster servicio.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-207">This is a known issue with hello HMaster service.</span></span> <span data-ttu-id="4cbd9-208">Las tareas de inicio de los clústeres generales pueden tardar mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-208">General cluster startup tasks can take a long time.</span></span> <span data-ttu-id="4cbd9-209">HMaster se cierra porque todavía no se ha asignado la tabla de espacio de nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-209">HMaster shuts down because hello namespace table isn’t yet assigned.</span></span> <span data-ttu-id="4cbd9-210">Esto sucede solo en aquellos escenarios en los que existe una gran cantidad de datos no vaciados y no es suficiente un tiempo de expiración de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-210">This occurs only in scenarios in which large amount of unflushed data exists, and a timeout of five minutes is not sufficient.</span></span>
  
### <a name="resolution-steps"></a><span data-ttu-id="4cbd9-211">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="4cbd9-211">Resolution steps</span></span>

1. <span data-ttu-id="4cbd9-212">Hola Ambari UI, vaya demasiado**HBase** > **configuraciones**.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-212">In hello Ambari UI, go too**HBase** > **Configs**.</span></span> <span data-ttu-id="4cbd9-213">En archivo de hbase-site.xml personalizado de hello, agregue Hola después de configuración:</span><span class="sxs-lookup"><span data-stu-id="4cbd9-213">In hello custom hbase-site.xml file, add hello following setting:</span></span> 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. <span data-ttu-id="4cbd9-214">Reinicie los servicios de hello necesario (HMaster y posiblemente otros servicios de HBase).</span><span class="sxs-lookup"><span data-stu-id="4cbd9-214">Restart hello required services (HMaster, and possibly other HBase services).</span></span>  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a><span data-ttu-id="4cbd9-215">Qué provoca un error de reinicio en un servidor de regiones</span><span class="sxs-lookup"><span data-stu-id="4cbd9-215">What causes a restart failure on a region server</span></span>

### <a name="issue"></a><span data-ttu-id="4cbd9-216">Problema</span><span class="sxs-lookup"><span data-stu-id="4cbd9-216">Issue</span></span>

<span data-ttu-id="4cbd9-217">Si se siguen los procedimientos recomendados, se puede evitar un error de reinicio en un servidor de regiones.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-217">A restart failure on a region server might be prevented by following best practices.</span></span> <span data-ttu-id="4cbd9-218">Se recomienda pausar la actividad de gran carga de trabajo para planear servidores de región de HBase toorestart.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-218">We recommend that you pause heavy workload activity when you are planning toorestart HBase region servers.</span></span> <span data-ttu-id="4cbd9-219">Si una aplicación continúa tooconnect con servidores de región cuando cierre esté en curso, operación de reinicio del servidor de región de hello será más lento por varios minutos.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-219">If an application continues tooconnect with region servers when shutdown is in progress, hello region server restart operation will be slower by several minutes.</span></span> <span data-ttu-id="4cbd9-220">Además, es un vaciado de que todas las tablas de Hola toofirst de buena idea.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-220">Also, it's a good idea toofirst flush all hello tables.</span></span> <span data-ttu-id="4cbd9-221">Para obtener una referencia sobre cómo tooflush tablas, vea [HBase para HDInsight: cómo clúster de HBase tooimprove Hola reiniciar tiempo vaciando tablas](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span><span class="sxs-lookup"><span data-stu-id="4cbd9-221">For a reference on how tooflush tables, see [HDInsight HBase: How tooimprove hello HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span></span>

<span data-ttu-id="4cbd9-222">Si inicia la operación de reinicio de hello en los servidores de la región de HBase de hello Ambari UI, verá inmediatamente que los servidores de región de hello ha fallado, pero no reinicien inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-222">If you initiate hello restart operation on HBase region servers from hello Ambari UI, you immediately see that hello region servers went down, but they don't restart right away.</span></span> 

<span data-ttu-id="4cbd9-223">Aquí es lo que ocurre entre bastidores de hello:</span><span class="sxs-lookup"><span data-stu-id="4cbd9-223">Here's what's happening behind hello scenes:</span></span> 

1. <span data-ttu-id="4cbd9-224">agente de Ambari Hola envía a un servidor de región de toohello de solicitud de detención.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-224">hello Ambari agent sends a stop request toohello region server.</span></span>
2. <span data-ttu-id="4cbd9-225">Hola Ambari agente espera 30 segundos para hello región server tooshut hacia abajo a correctamente.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-225">hello Ambari agent waits for 30 seconds for hello region server tooshut down gracefully.</span></span> 
3. <span data-ttu-id="4cbd9-226">Si su aplicación continúa tooconnect con el servidor de la región de hello, servidor de hello no apagará inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-226">If your application continues tooconnect with hello region server, hello server won't shut down immediately.</span></span> <span data-ttu-id="4cbd9-227">tiempo de espera de 30 segundos de Hello expira antes de que el apagado se produce.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-227">hello 30-second timeout expires before shutdown occurs.</span></span> 
4. <span data-ttu-id="4cbd9-228">Después de 30 segundos, el agente de Ambari de hello envía una interrupción force (`kill -9`) servidor de región de comandos toohello.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-228">After 30 seconds, hello Ambari agent sends a force-kill (`kill -9`) command toohello region server.</span></span> <span data-ttu-id="4cbd9-229">Puede verlo en hello ambari agente registro (Hola/var/log/directorio de nodo de trabajo respectiva hello):</span><span class="sxs-lookup"><span data-stu-id="4cbd9-229">You can see this in hello ambari-agent log (in hello /var/log/ directory of hello respective worker node):</span></span>

   ```apache
           2017-03-21 13:22:09,171 - Execute['/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/current/hbase-regionserver/conf stop regionserver'] {'only_if': 'ambari-sudo.sh  -H -E t
           est -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1', 'on_timeout': '! ( ambari-sudo.sh  -H -E test -
           f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H 
           -E cat /var/run/hbase/hbase-hbase-regionserver.pid`', 'timeout': 30, 'user': 'hbase'}
           2017-03-21 13:22:40,268 - Executing '! ( ambari-sudo.sh  -H -E test -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >
           /dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid`'. Reason: Execution of 'ambari-sudo.sh su hbase -l -s /bin/bash -c 'export  
           PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/var/lib/ambari-agent ; /usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/curre
           nt/hbase-regionserver/conf stop regionserver was killed due timeout after 30 seconds
           2017-03-21 13:22:40,285 - File['/var/run/hbase/hbase-hbase-regionserver.pid'] {'action': ['delete']}
           2017-03-21 13:22:40,285 - Deleting File['/var/run/hbase/hbase-hbase-regionserver.pid']
   ```
<span data-ttu-id="4cbd9-230">Por cierre del abrupto hello, puerto Hola asociado con el proceso de hello podría no puede liberarse, aunque se haya detenido el proceso de servidor de región de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-230">Because of hello abrupt shutdown, hello port associated with hello process might not be released, even though hello region server process is stopped.</span></span> <span data-ttu-id="4cbd9-231">Esta situación puede provocar tooan AddressBindException cuando se inicia el servidor de la región de hello, como se muestra en hello después de registros.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-231">This situation can lead tooan AddressBindException when hello region server is starting, as shown in hello following logs.</span></span> <span data-ttu-id="4cbd9-232">Puede comprobarlo en hello región-server.log en directorio de /var/log/hbase hello en nodos de trabajador de Hola que servidor de la región de hello no toostart.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-232">You can verify this in hello region-server.log in hello /var/log/hbase directory on hello worker nodes where hello region server fails toostart.</span></span> 

   ```apache

   2017-03-21 13:25:47,061 ERROR [main] regionserver.HRegionServerCommandLine: Region server exiting
   java.lang.RuntimeException: Failed construction of Regionserver: class org.apache.hadoop.hbase.regionserver.HRegionServer
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2636)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.start(HRegionServerCommandLine.java:64)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.run(HRegionServerCommandLine.java:87)
   at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
   at org.apache.hadoop.hbase.util.ServerCommandLine.doMain(ServerCommandLine.java:126)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.main(HRegionServer.java:2651)
        
   Caused by: java.lang.reflect.InvocationTargetException
   at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
   at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:57)
   at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
   at java.lang.reflect.Constructor.newInstance(Constructor.java:526)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2634)
   ... 5 more
        
   Caused by: java.net.BindException: Problem binding too/10.2.0.4:16020 : Address already in use
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2497)
   at org.apache.hadoop.hbase.ipc.RpcServer$Listener.<init>(RpcServer.java:580)
   at org.apache.hadoop.hbase.ipc.RpcServer.<init>(RpcServer.java:1982)
   at org.apache.hadoop.hbase.regionserver.RSRpcServices.<init>(RSRpcServices.java:863)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.createRpcServices(HRegionServer.java:632)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.<init>(HRegionServer.java:532)
   ... 10 more
        
   Caused by: java.net.BindException: Address already in use
   at sun.nio.ch.Net.bind0(Native Method)
   at sun.nio.ch.Net.bind(Net.java:463)
   at sun.nio.ch.Net.bind(Net.java:455)
   at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:223)
   at sun.nio.ch.ServerSocketAdaptor.bind(ServerSocketAdaptor.java:74)
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2495)
   ... 15 more
   ```

### <a name="resolution-steps"></a><span data-ttu-id="4cbd9-233">Pasos de la solución</span><span class="sxs-lookup"><span data-stu-id="4cbd9-233">Resolution steps</span></span>

1. <span data-ttu-id="4cbd9-234">Intente tooreduce Hola carga en los servidores de región de hello HBase antes de iniciar un reinicio.</span><span class="sxs-lookup"><span data-stu-id="4cbd9-234">Try tooreduce hello load on hello HBase region servers before you initiate a restart.</span></span> 
2. <span data-ttu-id="4cbd9-235">Como alternativa (si no ayuda paso 1), comandos try toomanually reinicio región servidores en los nodos de trabajador de hello mediante el uso de Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="4cbd9-235">Alternatively (if step 1 doesn't help), try toomanually restart region servers on hello worker nodes by using hello following commands:</span></span>

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

