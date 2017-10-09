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
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a>Solución de problemas de HBase mediante Azure HDInsight

Obtener información sobre problemas principales de Hola y sus soluciones cuando se trabaja con cargas de Apache HBase en Ambari de Apache.

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a>Cómo se ejecutan informes de comando hbck con varias regiones sin asignar

Un mensaje de error comunes que podría ver al ejecutar hello `hbase hbck` comando es "varias regiones está sin asignar o agujeros en cadena Hola de regiones."

Hola HBase Master UI, puede ver número Hola de regiones que no están equilibrados en todos los servidores de la región. A continuación, puede ejecutar `hbase hbck` comando toosee vulnerabilidades de cadena de la región de Hola.

Vulnerabilidades pueden deberse regiones de hello sin conexión, por lo que las asignaciones de Hola de corrección en primer lugar. 

toobring Hola sin asignar regiones tooa espera el estado normal, completar Hola pasos:

1. Inicie sesión en toohello clúster de HBase para HDInsight a través de SSH.
2. tooconnect con shell de ZooKeeper hello, ejecute hello `hbase zkcli` comando.
3. Ejecute hello `rmr /hbase/regions-in-transition` comando o hello `rmr /hbase-unsecure/regions-in-transition` comando.
4. tooexit de hello `hbase zkcli` de shell, use hello `exit` comando.
5. Abra Hola Apache Ambari UI y, a continuación, reinicie el servicio de Active HBase Master de Hola.
6. Ejecute hello `hbase hbck` comando nuevo (sin ninguna opción). Compruebe la salida de hello de este tooensure de comando que se está asignando todas las regiones.


## <a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Cómo se solucionan los problemas de tiempo de espera cuando se usan comandos hbck para las asignaciones de regiones

### <a name="issue"></a>Problema

Una posible causa de problemas de tiempo de espera al usar hello `hbck` comando podría ser que varias regiones son Hola "en"transición de estado durante mucho tiempo. Puede ver esas regiones como sin conexión en hello UI Master de HBase. Dado que un gran número de regiones estás intentando tootransition, Master HBase podría tiempo de espera y toobring no se puede esas regiones en línea.

### <a name="resolution-steps"></a>Pasos de la solución

1. Inicie sesión en toohello clúster de HBase para HDInsight a través de SSH.
2. tooconnect con shell de ZooKeeper hello, ejecute hello `hbase zkcli` comando.
3. Ejecute hello `rmr /hbase/regions-in-transition` o hello `rmr /hbase-unsecure/regions-in-transition` comando.
4. Hola tooexit `hbase zkcli` de shell, use hello `exit` comando.
5. Hola Ambari UI, reinicie el servicio de Active HBase Master de Hola.
6. Ejecute hello `hbase hbck -fixAssignments` comando nuevo.

## <a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Cómo forzar la deshabilitación del modo seguro de HDFS en un clúster

### <a name="issue"></a>Problema

Hola local Hadoop distribuidas archivo sistema (HDFS) está atascada en el modo seguro en clúster de HDInsight Hola.

### <a name="detailed-description"></a>Descripción detallada

Este error podría deberse a un error al ejecutar Hola siguiente HDFS comando:

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

error de Hello que vean cuando intente el comando de hello toorun tiene el siguiente aspecto:

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

### <a name="probable-cause"></a>Causa probable

Hello clúster de HDInsight ha sido reducida tooa muy pocos nodos. Hola o número de nodos está por debajo de cerrar el factor de replicación de toohello HDFS.

### <a name="resolution-steps"></a>Pasos de la solución 

1. Obtener estado de Hola de hello que HDFS en hello HDInsight de clúster mediante la ejecución de hello siguientes comandos:

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
2. También puede comprobar integridad de Hola de hello que HDFS en hello HDInsight clúster mediante Hola siguientes comandos:

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

3. Si determina que no hay ningún bloques que falta, está dañados o under-replicados, o que pueden hacer caso omiso de los bloques, ejecute hello después de nodo de nombre de comando tootake Hola fuera del modo seguro:

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a>Cómo se solucionan los problemas de conectividad de JDBC o SQLLine con Apache Phoenix

### <a name="resolution-steps"></a>Pasos de la solución

tooconnect con Phoenix, debe proporcionar la dirección IP de Hola de un nodo activo de ZooKeeper. Asegúrese de que hello ZooKeeper está tratando de servicio toowhich sqlline.py tooconnect está en funcionamiento.
1. Inicie sesión en toohello clúster de HDInsight a través de SSH.
2. Escriba el siguiente comando de hello:
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > Puede obtener la dirección IP de Hola de nodo de hello activo ZooKeeper de hello Ambari UI. Vaya demasiado**HBase** > **vínculos rápidos** > **ZK\* (Active)** > **Zookeeper información**. 

3. Si sqlline.py Hola se conecta tooPhoenix y tiempo de espera no lo hace, siguiente ejecución Hola comando toovalidate disponibilidad de Hola y el estado de Phoenix:

   ```apache
           !tables
           !quit
   ```      
4. Si el comando funciona, no hay ningún problema. dirección IP de Hello proporcionada por usuario de hello podría ser incorrecta. Sin embargo, si el comando hello pone en pausa durante un período prolongado y, a continuación, muestra hello tras error, continuar toostep 5.

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. Ejecute hello siguientes comandos de condición de hello nodo principal (hn0) toodiagnose Hola de hello Phoenix sistema. Tabla del catálogo:

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   comando de Hello debe devolver una continuación toohello similar de error: 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. Hola Ambari UI, realizar Hola después de servicio de HMaster de Hola de toorestart de pasos en todos los nodos de ZooKeeper:

    1. Hola **resumen** sección de HBase, vaya demasiado**HBase** > **Active HBase Master**. 
    2. Hola **componentes** sección, reinicie el servicio de HBase Master Hola.
    3. Repita estos para todos los servicios **Standby HBase Master** restantes. 

Puede tardar minutos toofive Hola Master HBase servicio toostabilize y finalizar el proceso de recuperación de Hola. Después de unos minutos, repita hello sqlline.py comandos tooconfirm ese sistema Hola. Tabla del catálogo está activo y que TI puede consultarse. 

Hola al sistema. Tabla del catálogo es toonormal atrás, tooPhoenix de problema de conectividad de hello debería resolverse automáticamente.


## <a name="what-causes-a-master-server-toofail-toostart"></a>¿Qué hace que un servidor maestro toofail toostart

### <a name="error"></a>Error 

Se produce un error de cambio de nombre atómico.

### <a name="detailed-description"></a>Descripción detallada

Durante el proceso de inicio de hello, HMaster completa muchos pasos de inicialización. Puede tratarse de mover datos desde el principio de hello (.tmp) carpeta toohello la carpeta de datos. HMaster también busca en la carpeta toosee de hello registros de escritura anticipada (WALs) si no hay ningún servidor de la región que no responde, y así sucesivamente. 

Durante el inicio, HMaster realiza un comando `list` básico en estas carpetas. Si en algún momento HMaster ve un archivo inesperado en cualquiera de estas carpetas, genera una excepción y no se inicia.  

### <a name="probable-cause"></a>Causa probable

En los registros de servidor de región de hello, realice escala de tiempo de tooidentify Hola Hola de creación del archivo y, a continuación, compruebe si se ha producido que un bloqueo del proceso alrededor de hello hora Hola archivo se creó. (Póngase en contacto con tooassist de soporte técnico de HBase en hacerlo.) Esto nos ayuda a proporcionar mecanismos más robustos para que pueda evitar toparse con este error y asegurarse apagados de procesos correctos.

### <a name="resolution-steps"></a>Pasos de la solución

Compruebe la pila de llamadas de hello e inténtelo toodetermine qué carpeta podría estar causando el problema de hello (por ejemplo, podría ser carpeta de WALs de Hola u Hola .tmp). A continuación, en el Explorador de la nube o mediante comandos HDFS, pruebe con toolocate Hola problema. Normalmente, es un archivo \*-renamePending.json. (hello \*-renamePending.json archivo es un archivo de diario que ha utilizado la operación atómica de cambio de nombre de tooimplement hello en el controlador WASB Hola. Mucha toobugs en esta implementación, estos archivos pueden ser restantes después de bloqueos de procesos y así sucesivamente.) Fuerce la eliminación de este archivo en Cloud Explorer o mediante los comandos de HDFS. 

En ocasiones, en esta ubicación también puede haber un archivo temporal denominado algo así como *$$$. $$$*. Tiene toouse HDFS `ls` comando toosee este archivo; no puede ver el archivo hello en el explorador en la nube. toodelete este archivo, use Hola HDFS comando `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.  

Una vez que haya ejecutado estos comandos, HMaster debería iniciarse de inmediato. 

### <a name="error"></a>Error

No se enumera ninguna dirección de servidor en *hbase: meta* para la región xxx.

### <a name="detailed-description"></a>Descripción detallada

Puede aparecer un mensaje en el clúster de Linux que indica que hello *hbase: meta* tabla no está en línea. La ejecución de `hbck` puede notificar que "No se encuentra la tabla hbase: meta replicaId 0 en ninguna región". posible problema de Hola que HMaster no se pudo inicializar una vez reiniciado HBase. En los registros de HMaster hello, podría ver mensajes de bienvenida: "ninguna dirección de servidor enumerados en hbase: meta para región hbase: copia de seguridad \<nombre de la región\>".  

### <a name="resolution-steps"></a>Pasos de la solución

1. Hola shell de HBase, escriba Hola después de comandos (valores reales de cambio según corresponda):  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. Eliminar hello *hbase: espacio de nombres* entrada. Esta entrada podría ser Hola mismo error que se va a notificar cuando hello *hbase: espacio de nombres* se examina la tabla.

3. toobring de HBase en un estado de ejecución, en hello Ambari UI, reinicie el servicio de Active HMaster de Hola.  

4. Hola shell de HBase, toobring todas las tablas sin conexión, ejecute hello siguiente comando:

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a>Lecturas adicionales

[Tabla de HBase de hello tooprocess no se puede](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a>Error

Agota el tiempo de espera del HMaster con un too"java.io.IOException similar de excepción grave: 300000ms de tiempo de espera agotado esperando toobe de la tabla de espacio de nombres asignado."

### <a name="detailed-description"></a>Descripción detallada

Este problema puede aparecer si hay muchas tablas y regiones que no se han vaciado al reiniciar los servicios de HMaster. Podría producirse un error de reinicio y verá Hola precede el mensaje de error.  

### <a name="probable-cause"></a>Causa probable

Se trata de un problema conocido con hello HMaster servicio. Las tareas de inicio de los clústeres generales pueden tardar mucho tiempo. HMaster se cierra porque todavía no se ha asignado la tabla de espacio de nombres de Hola. Esto sucede solo en aquellos escenarios en los que existe una gran cantidad de datos no vaciados y no es suficiente un tiempo de expiración de cinco minutos.
  
### <a name="resolution-steps"></a>Pasos de la solución

1. Hola Ambari UI, vaya demasiado**HBase** > **configuraciones**. En archivo de hbase-site.xml personalizado de hello, agregue Hola después de configuración: 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. Reinicie los servicios de hello necesario (HMaster y posiblemente otros servicios de HBase).  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a>Qué provoca un error de reinicio en un servidor de regiones

### <a name="issue"></a>Problema

Si se siguen los procedimientos recomendados, se puede evitar un error de reinicio en un servidor de regiones. Se recomienda pausar la actividad de gran carga de trabajo para planear servidores de región de HBase toorestart. Si una aplicación continúa tooconnect con servidores de región cuando cierre esté en curso, operación de reinicio del servidor de región de hello será más lento por varios minutos. Además, es un vaciado de que todas las tablas de Hola toofirst de buena idea. Para obtener una referencia sobre cómo tooflush tablas, vea [HBase para HDInsight: cómo clúster de HBase tooimprove Hola reiniciar tiempo vaciando tablas](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).

Si inicia la operación de reinicio de hello en los servidores de la región de HBase de hello Ambari UI, verá inmediatamente que los servidores de región de hello ha fallado, pero no reinicien inmediatamente. 

Aquí es lo que ocurre entre bastidores de hello: 

1. agente de Ambari Hola envía a un servidor de región de toohello de solicitud de detención.
2. Hola Ambari agente espera 30 segundos para hello región server tooshut hacia abajo a correctamente. 
3. Si su aplicación continúa tooconnect con el servidor de la región de hello, servidor de hello no apagará inmediatamente. tiempo de espera de 30 segundos de Hello expira antes de que el apagado se produce. 
4. Después de 30 segundos, el agente de Ambari de hello envía una interrupción force (`kill -9`) servidor de región de comandos toohello. Puede verlo en hello ambari agente registro (Hola/var/log/directorio de nodo de trabajo respectiva hello):

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
Por cierre del abrupto hello, puerto Hola asociado con el proceso de hello podría no puede liberarse, aunque se haya detenido el proceso de servidor de región de Hola. Esta situación puede provocar tooan AddressBindException cuando se inicia el servidor de la región de hello, como se muestra en hello después de registros. Puede comprobarlo en hello región-server.log en directorio de /var/log/hbase hello en nodos de trabajador de Hola que servidor de la región de hello no toostart. 

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

### <a name="resolution-steps"></a>Pasos de la solución

1. Intente tooreduce Hola carga en los servidores de región de hello HBase antes de iniciar un reinicio. 
2. Como alternativa (si no ayuda paso 1), comandos try toomanually reinicio región servidores en los nodos de trabajador de hello mediante el uso de Hola siguientes:

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

