---
title: aaaMigrate de HDInsight basados en Windows-based tooLinux HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomigrate desde un HDInsight basados en Windows cluster tooa clúster de HDInsight basados en Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: ff35be59-bae3-42fd-9edc-77f0041bab93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 7e5e536e8672d7e7c3086c6860cec062d05eda65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-a-windows-based-hdinsight-cluster-tooa-linux-based-cluster"></a>Migrar desde un clúster de basados en Linux de tooa de clúster de HDInsight basados en Windows

Este documento proporciona información sobre las diferencias de hello entre HDInsight en Windows y Linux e instrucciones sobre cómo toomigrate las cargas de trabajo tooa basados en Linux clúster existente.

Aunque HDInsight basados en Windows proporciona una toouse fácilmente Hadoop en la nube de hello, puede ser necesario toomigrate tooa basados en Linux clúster. Por ejemplo, tootake las herramientas basadas en Linux y las tecnologías que son necesarias para la solución. Muchas cosas en el ecosistema de Hadoop de Hola se desarrollan en sistemas basados en Linux y no estén disponibles para su uso con HDInsight basados en Windows. Además, en muchos libros, vídeos y otros materiales de aprendizaje se da por sentado que cuando se trabaja con Hadoop se usa un sistema Linux.

> [!NOTE]
> Clústeres de HDInsight usar compatibilidad a largo plazo de Ubuntu (LTS) como sistema operativo de Hola para los nodos de hello en clúster de Hola. Para obtener información sobre la versión de Hola de Ubuntu disponible con HDInsight, junto con otra información de control de versiones del componente, vea [versiones de componentes de HDInsight](hdinsight-component-versioning.md).

## <a name="migration-tasks"></a>Tareas de migración

flujo de trabajo general de Hello para la migración es como sigue.

![Diagrama de flujo de trabajo de migración](./media/hdinsight-migrate-from-windows-to-linux/workflow.png)

1. Leer cada sección de este documento toounderstand cambios que podrían ser necesarios cuando se migra el flujo de trabajo existente, los trabajos y clúster de etc. tooa basados en Linux.

2. Cree un clúster basado en Linux como entorno de control de calidad o de pruebas. Para obtener más información sobre cómo crear un clúster basado en Linux, consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

3. Copia receptores toohello nuevo entorno, orígenes de datos y trabajos existentes.

4. Realizar pruebas toomake seguro de que los trabajos funcionan según lo previsto en el nuevo clúster de Hola de validación.

Una vez haya comprobado que todo funciona según lo esperado, programe el tiempo de inactividad para la migración de Hola. Durante este tiempo de inactividad, lleve a cabo Hola siguientes acciones:

1. Realizar una copia de los datos transitorios almacenados localmente en nodos de clúster de Hola. Por ejemplo, si tiene datos que se almacenan directamente en un nodo principal.

2. Eliminar el clúster de hello basados en Windows.

3. Cree un clúster basados en Linux con hello mismo almacén de datos que Hola clúster basado en Windows que utiliza predeterminado. clúster de Hello basados en Linux puede seguir trabajando con sus datos de producción existente.

4. Importe los datos transitorios cuya copia de seguridad realizó.

5. Iniciar trabajos/continuar procesando usando Hola nuevo clúster.

### <a name="copy-data-toohello-test-environment"></a>Entorno de prueba de toohello de datos de copia

Hay muchos datos de métodos toocopy hello y trabajos, sin embargo Hola dos se trata en esta sección son hello más sencillo métodos toodirectly mover archivos tooa clúster de prueba.

#### <a name="hdfs-copy"></a>Copia de HDFS

Usar hello siguientes datos toocopy de pasos de clúster de prueba de toohello de clúster de producción de hello. Estos pasos utiliza hello `hdfs dfs` utilidad que se incluye con HDInsight.

1. Buscar Hola almacenamiento predeterminado contenedor información de cuenta y para el clúster existente. Hola de ejemplo siguiente usa PowerShell tooretrieve esta información:

    ```powershell
    $clusterName="Your existing HDInsight cluster name"
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    write-host "Storage account name: $clusterInfo.DefaultStorageAccount.split('.')[0]"
    write-host "Default container: $clusterInfo.DefaultStorageContainer"
    ```

2. toocreate un entorno de prueba, siga los pasos de hello en clústeres de hello basados en Linux crear documento de HDInsight. Detenga antes de crear el clúster de hello y, en su lugar Active **configuración opcional**.

3. En la hoja de configuración opcional de hello, seleccione **cuentas de almacenamiento vinculadas**.

4. Seleccione **agregar una clave de almacenamiento**y cuando se le solicite, seleccione la cuenta de almacenamiento de Hola que devolvió hello secuencia de comandos de PowerShell en el paso 1. Haga clic en la opción **Seleccionar** de cada hoja. Finalmente, cree el clúster de Hola.

5. Una vez que se haya creado el clúster de hello, conectarse utilizando tooit **SSH.** Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

6. Desde la sesión de SSH de hello, utilice Hola siguientes archivos de comandos toocopy de cuenta de almacenamiento de hello vinculado almacenamiento cuenta toohello nuevo de forma predeterminada. Reemplace el contenedor con información de contenedor de hello devuelta por PowerShell. Reemplace __cuenta__ con el nombre de la cuenta de hello. Reemplace hello toodata de ruta de acceso con el archivo de datos de tooa de ruta de acceso de Hola.

    ```bash
    hdfs dfs -cp wasb://CONTAINER@ACCOUNT.blob.core.windows.net/path/to/old/data /path/to/new/location
    ```

    > [!NOTE]
    > Si la estructura de directorios de Hola que contiene datos de hello no existe en el entorno de prueba de hello, puede crearlo mediante Hola siguiente comando:

    ```bash
    hdfs dfs -mkdir -p /new/path/to/create
    ```

    Hola `-p` conmutador permite la creación de hello de todos los directorios de la ruta de acceso de Hola.

#### <a name="direct-copy-between-blobs-in-azure-storage"></a>Copia directa entre blobs de Azure Storage

Como alternativa, puede que desee toouse hello `Start-AzureStorageBlobCopy` toocopy blobs de cmdlet de PowerShell de Azure entre cuentas de almacenamiento fuera de HDInsight. Para obtener más información, vea cómo hello toomanage sección de Blobs de Azure de uso de PowerShell de Azure con el almacenamiento de Azure.

## <a name="client-side-technologies"></a>Tecnologías de cliente

Tecnologías de cliente como [cmdlets de PowerShell de Azure](/powershell/azureps-cmdlets-docs), [CLI de Azure](../cli-install-nodejs.md), o hello [.NET SDK para Hadoop](https://hadoopsdk.codeplex.com/) continuar toowork los clústeres basados en Linux. Estas tecnologías se basan en REST API que Hola igual en los dos tipos de clúster SO.

## <a name="server-side-technologies"></a>Tecnologías de servidor

Hello en la tabla siguiente proporciona directrices para migrar componentes del lado servidor que son específicos de Windows.

| Si utiliza esta tecnología... | Realice esta acción... |
| --- | --- |
| **PowerShell** (scripts de servidor, incluidas las acciones de script que se usan durante la creación del clúster) |Vuelva a escribirlos como scripts de Bash. Para acciones de script, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md) y [Desarrollo de la acción de script con HDInsight](hdinsight-hadoop-script-actions-linux.md). |
| **CLI de Azure** (scripts de servidor) |Mientras Hola CLI de Azure está disponible en Linux, no lo vienen preinstalada en nodos principales del clúster de HDInsight Hola. Para obtener más información acerca de cómo instalar Hola CLI de Azure, consulte [empezar a trabajar con Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli). |
| **Componentes de .NET** |.NET no es compatible con HDInsight basado en Linux a través de [Mono](https://mono-project.com). Para obtener más información, consulte [soluciones migrar .NET basada en tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md). |
| **Componentes de Win32 o de otras tecnologías de Windows** |Instrucciones depende del componente de Hola o tecnología. Es posible que pueda toofind una versión que sea compatible con Linux, o pueda necesitar toofind una solución alternativa o vuelva a escribir este componente. |

> [!IMPORTANT]
> administración de HDInsight de Hello SDK no es totalmente compatible con Mono. No debe usarse como parte de las soluciones implementadas clúster de HDInsight de toohello en este momento.

## <a name="cluster-creation"></a>Creación de clústeres

Esta sección ofrece información sobre las diferencias en la creación de clústeres.

### <a name="ssh-user"></a>Usuario de SSH

Clústeres de HDInsight basados en Linux usar hello **Shell seguro (SSH)** nodos de clúster de tooprovide acceso remoto toohello del protocolo. A diferencia de Escritorio remoto para clústeres basados en Windows, la mayoría de clientes de SSH no ofrece experiencia de usuario gráfica. En su lugar, los clientes SSH proporcionan una línea de comandos que permita los comandos de toorun en clúster de Hola. Algunos clientes (como [MobaXterm](http://mobaxterm.mobatek.net/)) proporcionan un explorador de sistema de archivos gráfica en línea de comandos de adición tooa remoto.

Durante la creación del clúster, debe especificar un usuario SSH y una **contraseña**, o bien un **certificado de clave pública** para la autenticación.

Se recomienda usar el certificado de clave pública, ya que es más seguro que usar una contraseña. Autenticación de certificado funciona generando un par de claves pública/privada con signo, a continuación, proporcionar la clave pública de hello al crear el clúster de Hola. Al conectar el servidor de toohello mediante SSH, clave privada de hello en el cliente de hello proporciona autenticación para la conexión de Hola.

Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="cluster-customization"></a>Personalización del clúster

**acciones de script** se utilizan con clústeres basados en Linux y deben escribirse en script de Bash. Aunque se puede utilizar acciones de Script durante la creación de clústeres, para clústeres basados en Linux también pueden ser utilizados tooperform personalización después de un clúster está activo y en ejecución. Para más información, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md) y [Desarrollo de la acción de script con HDInsight](hdinsight-hadoop-script-actions-linux.md).

Otra característica de personalización es **arranque**. Para los clústeres de Windows, esta característica permite toospecify ubicación de Hola de bibliotecas adicionales para su uso con Hive. Después de la creación del clúster, estas bibliotecas están automáticamente disponibles para su uso con consultas de Hive sin Hola necesidad toouse `ADD JAR`.

característica de arranque de Hola para clústeres basados en Linux no proporciona esta funcionalidad. En su lugar, use la acción de script que se documenta en [Incorporación de bibliotecas de Hive durante la creación del clúster](hdinsight-hadoop-add-hive-libraries.md).

### <a name="virtual-networks"></a>Redes virtuales

Los clústeres de HDInsight basados en Windows solo funcionan con redes virtuales clásicas, mientras que los clústeres HDInsight basados en Linux requieren redes virtuales del Administrador de recursos. Si tiene los recursos una red Virtual clásico que Hola clúster de HDInsight de Linux debe conectarse a, consulte [conectar una red Virtual de administrador de recursos de red Virtual clásica tooa](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

Para obtener más información sobre los requisitos de configuración para usar redes virtuales de Azure con HDInsight, consulte [Extensión de las funcionalidades de HDInsight con una red virtual](hdinsight-extend-hadoop-virtual-network.md).

## <a name="management-and-monitoring"></a>Administración y supervisión

Muchas de web Hola interfaces de usuario que se ha utilizado con HDInsight basados en Windows, por ejemplo, historial de trabajos o la interfaz de usuario de hilo, están disponibles a través de Ambari. Además, hello Ambari Hive vista proporciona un toorun manera consultas de Hive mediante el explorador web. Hola interfaz de usuario de Ambari Web está disponible en clústeres basados en Linux en https://CLUSTERNAME.azurehdinsight.net.

Para obtener más información sobre cómo trabajar con Ambari, vea Hola siguientes documentos:

* [Web de Ambari](hdinsight-hadoop-manage-ambari.md)
* [API de REST de Ambari](hdinsight-hadoop-manage-ambari-rest-api.md)

### <a name="ambari-alerts"></a>Alertas de Ambari

Ambari tiene un sistema de alertas que puede avisarle de problemas potenciales con el clúster de Hola. Las alertas aparecen como entradas de color rojo o amarillas en hello Ambari la interfaz de usuario Web, sin embargo, también se puede recuperar a través de la API de REST de Hola.

> [!IMPORTANT]
> Las alertas de Ambari indican que *puede* que haya un problema, no que *exista* realmente. Por ejemplo, puede recibir una alerta que indica que no se puede tener acceso a HiveServer2, aunque pueda tener acceso a él normalmente.
>
> Las alertas se implementan como consultas basadas en intervalos en un servicio y esperan una respuesta en un plazo de tiempo específico. Por lo que alerta hello no significa necesariamente que el servicio de hello está funcionando, solo que no devolver resultados en el período de tiempo de espera de Hola.

Debería evaluar si una alerta se ha venido produciendo durante un período prolongado o si refleja problemas de los usuarios que se han registrado antes de realizar ninguna acción en el servicio.

## <a name="file-system-locations"></a>Ubicaciones del sistema de archivos

Hola sistema de archivos del clúster de Linux se distribuyen de manera diferente que en los clústeres de HDInsight basados en Windows. Usar hello siguientes archivos de tabla toofind de uso frecuente.

| Necesito toofind... | Se encuentra... |
| --- | --- |
| Configuración |`/etc`. Por ejemplo, `/etc/hadoop/conf/core-site.xml` |
| Archivos de registro |`/var/logs` |
| HortonWorks Data Platform (HDP) |`/usr/hdp`. Hay dos directorios en este caso, encuentran uno que sea la versión actual de HDP de Hola y `current`. Hola `current` directorio contiene vínculos simbólicos toofiles y directorios ubicados en el directorio de número de versión de Hola. Hola `current` directorio es siempre como una manera cómoda de obtener acceso a archivos HDP desde Hola número de versión cambia como Hola HDP versión está actualizada. |
| hadoop-streaming.jar |`/usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar` |

En general, si conoce Hola nombre de archivo hello, puede usar Hola siguiente comando desde una ruta de acceso de archivo SSH sesión toofind hello:

    find / -name FILENAME 2>/dev/null

También puede usar caracteres comodín con nombre de archivo de Hola. Por ejemplo, `find / -name *streaming*.jar 2>/dev/null` devuelve tooany de ruta de acceso de hello archivos jar que contienen la palabra Hola streaming como parte del nombre de archivo de Hola.

## <a name="hive-pig-and-mapreduce"></a>Hive, Pig y MapReduce

Las cargas de trabajo de Pig y MapReduce son similares en clústeres basados en Linux. Sin embargo, los clústeres de HDInsight basados en Linux se pueden crear usando versiones más recientes de Hadoop, Hive y Pig. Estas diferencias de versión pueden provocar cambios en el funcionamiento de las soluciones existentes. Para obtener más información sobre las versiones de Hola de componentes que se incluyen con HDInsight, vea [versiones de componentes de HDInsight](hdinsight-component-versioning.md).

HDInsight basado en Linux no proporciona funcionalidad de escritorio remoto. En su lugar, puede utilizar SSH tooremotely conectar toohello nodos principales del clúster. Para obtener más información, vea Hola siguientes documentos:

* [Uso de Hive con SSH](hdinsight-hadoop-use-hive-ssh.md)
* [Uso de Pig con SSH](hdinsight-hadoop-use-pig-ssh.md)
* [Uso de MapReduce con SSH](hdinsight-hadoop-use-mapreduce-ssh.md)

### <a name="hive"></a>Hive

> [!IMPORTANT]
> Si utiliza una tienda de metadatos externo de Hive, debería hacer una tienda de metadatos de hello antes de usarlo con HDInsight basados en Linux. HDInsight basado en Linux está disponible con las versiones más recientes de Hive, lo que puede provocar incompatibilidades con las tiendas de metadatos creadas con versiones anteriores.

Hola tabla siguiente proporciona instrucciones sobre cómo migrar las cargas de trabajo de Hive.

| En basado en Windows, se usa... | En basado en Linux... |
| --- | --- |
| **Editor de Hive** |[Vista de Hive en Ambari](hdinsight-hadoop-use-hive-ambari-view.md) |
| `set hive.execution.engine=tez;`tooenable Tez |Tez es Hola motor de ejecución predeterminado para los clústeres basados en Linux, por lo que Hola set (instrucción) ya no es necesario. |
| Funciones definidas por el usuario de C# | Para obtener información sobre cómo validar los componentes de C# con HDInsight basados en Linux, consulte [soluciones migrar .NET basada en tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD, archivos o secuencias de comandos en servidor hello invocado como parte de un trabajo de Hive |se usan scripts de Bash |
| `hive` desde Escritorio remoto |Uso de [Beeline](hdinsight-hadoop-use-hive-beeline.md) o [Hive en una sesión de SSH](hdinsight-hadoop-use-hive-ssh.md) |

### <a name="pig"></a>Pig

| En basado en Windows, se usa... | En basado en Linux... |
| --- | --- |
| Funciones definidas por el usuario de C# | Para obtener información sobre cómo validar los componentes de C# con HDInsight basados en Linux, consulte [soluciones migrar .NET basada en tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD, archivos o secuencias de comandos en servidor hello invocado como parte de un trabajo de Pig |se usan scripts de Bash |

### <a name="mapreduce"></a>MapReduce

| En basado en Windows, se usa... | En basado en Linux... |
| --- | --- |
| Componentes asignadores y reductores de C# | Para obtener información sobre cómo validar los componentes de C# con HDInsight basados en Linux, consulte [soluciones migrar .NET basada en tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD, archivos o secuencias de comandos en servidor hello invocado como parte de un trabajo de Hive |se usan scripts de Bash |

## <a name="oozie"></a>Oozie

> [!IMPORTANT]
> Si utiliza una tienda de metadatos externo de Oozie, debería hacer una tienda de metadatos de hello antes de usarlo con HDInsight basados en Linux. HDInsight basado en Linux está disponible con las versiones más recientes de Oozie, lo que puede provocar incompatibilidades con las tiendas de metadatos creadas con versiones anteriores.

Los flujos de trabajo de Oozie permiten acciones de shell. Acciones de shell utilizar el comando de shell de hello predeterminado para los comandos de línea de comandos de toorun del sistema operativo de Hola. Si dispone de los flujos de trabajo de Oozie que se basan en el shell de Windows hello, debe volver a escribir hello toorely de flujos de trabajo en el entorno de shell de Linux de hello (intensiva de errores). Para obtener más información sobre el uso de acciones de shell con Oozie, consulte [Oozie shell action extension](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html) (Extensión de la acción del shell de Oozie).

Si tiene flujos de trabajo de Oozie que se basan en las aplicaciones de C# invocadas a través de acciones de shell, debe validar estas aplicaciones en un entorno de Linux. Para obtener más información, consulte [soluciones migrar .NET basada en tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="storm"></a>Storm

| En basado en Windows, se usa... | En basado en Linux... |
| --- | --- |
| panel de Storm |Hola aluvión de panel no está disponible. Vea [topologías implementar y administrar aluvión de HDInsight basados en Linux](hdinsight-storm-deploy-monitor-topology-linux.md) para las topologías de toosubmit de formas |
| UI de Storm |Hola aluvión de interfaz de usuario está disponible en https://CLUSTERNAME.azurehdinsight.net/stormui |
| Toocreate Visual Studio, implementar y administrar topologías de C# o híbrida |Visual Studio puede ser toocreate usado, implementar y administrar C# (SCP.NET) ni con topologías híbridas en Linux-based Storm en clústeres de HDInsight que se crean después de 10/28/2016. |

## <a name="hbase"></a>HBase

En los clústeres basados en Linux, es primario de hello znode para HBase `/hbase-unsecure`. Establezca este valor en la configuración de Hola para las aplicaciones de cliente de Java que usan la API nativa de Java de HBase.

Consulte [Compilación de una aplicación HBase basada en Java](hdinsight-hbase-build-java-maven.md) para ver un cliente de ejemplo que establece este valor.

## <a name="spark"></a>Spark

Los clústeres de Spark estaban disponibles en los clústeres de Windows durante la vista previa. Spark GA solo está disponible con clústeres basados en Linux. No hay ninguna ruta de acceso de migración de un clúster Spark basados en Windows Vista previa clúster tooa versión Spark basados en Linux.

## <a name="known-issues"></a>Problemas conocidos

### <a name="azure-data-factory-custom-net-activities"></a>Actividades de .NET personalizadas de Data Factory de Azure

Las actividades de .NET personalizadas de Data Factory de Azure no son compatibles actualmente con clústeres de HDInsight basado en Linux. En su lugar, debe usar uno de hello siguiendo las actividades personalizadas de métodos tooimplement como parte de la canalización ADF.

* Ejecute actividades de .NET en grupo de Lote de Azure. Consulte la sección de servicio vinculado Azure Batch de uso de Hola de [utilizar actividades personalizadas en una canalización del generador de datos de Azure](../data-factory/data-factory-use-custom-activities.md)
* Implementar la actividad de hello como una actividad de MapReduce. Para obtener más información, consulte [Invocación de programas MapReduce desde Data Factory](../data-factory/data-factory-map-reduce.md).

### <a name="line-endings"></a>Fin de línea

Por lo general, los fines de línea en sistemas basados en Windows usan CRLF, mientras que los sistemas basados en Linux usan LF. Si produce o esperar datos con el fin de línea CRLF, deberá toomodify hello toowork productores o los consumidores con el fin de línea de hello LF.

Por ejemplo, con tooquery de PowerShell de Azure HDInsight en un clúster basado en Windows, devuelve datos con CRLF. Hello misma consulta con un clúster basado en Linux devuelve LF. Debe probar toosee si el final de la línea de hello causa un problema con su solutuion antes de migrar clústeres de tooa basados en Linux.

Si tiene secuencias de comandos que se ejecutan directamente en nodos de clústeres de Linux de hello, debe utilizar siempre LF como final de la línea de saludo. Si usas CRLF, verá errores al ejecutar scripts de hello en un clúster basado en Linux.

Si sabe que las secuencias de comandos de hello no contienen cadenas de caracteres CR incrustados, es posible hacer masiva finales de línea de cambio hello mediante uno de los siguientes métodos de hello:

* **Antes de cargar clúster toohello**: Hola de uso siguientes finales de línea de PowerShell instrucciones toochange Hola de CRLF tooLF antes de cargar el clúster de toohello de script de Hola.

    ```powershell
    $original_file ='c:\path\to\script.py'
    $text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
    [IO.File]::WriteAllText($original_file, $text)
    ```

* **Después de cargar clúster toohello**: comando siguiente de Hola de uso de un toohello de sesión SSH secuencias de comandos de clúster basado en Linux toomodify Hola.

    ```bash
    hdfs dfs -get wasb:///path/to/script.py oldscript.py
    tr -d '\r' < oldscript.py > script.py
    hdfs dfs -put -f script.py wasb:///path/to/script.py
    ```

## <a name="next-steps"></a>Pasos siguientes

* [Obtenga información acerca de cómo toocreate HDInsight basados en Linux clústeres](hdinsight-hadoop-provision-linux-clusters.md)
* [Utilizar SSH tooconnect tooHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Administración de un clúster basado en Linux mediante Ambari](hdinsight-hadoop-manage-ambari.md)
