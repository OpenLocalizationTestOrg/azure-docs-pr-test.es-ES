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
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a>Habilitación de los volcados de montón de los servicios de Hadoop en HDInsight basado en Linux

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Los volcados del montón contienen una instantánea de memoria de la aplicación hello, incluidos los valores de hello de variables en tiempo de Hola se creó el volcado de Hola. Por ello, estos volcados resultan útiles a la hora de diagnosticar cualquier problema que ocurra en tiempo de ejecución.

> [!IMPORTANT]
> Hello pasos descritos en este documento solo funcionan con clústeres de HDInsight que utilizan Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="whichServices"></a>Servicios

Puede habilitar los volcados del montón para hello siguientes servicios:

* **hcatalog** - tempelton
* **hive** - hiveserver2, metastore, derbyserver
* **mapreduce** - jobhistoryserver
* **yarn** - resourcemanager, nodemanager, timelineserver
* **hdfs** - datanode, secondarynamenode, namenode

También puede habilitar los volcados del montón para asignación de Hola y reducir los procesos que se ejecutaban por HDInsight.

## <a name="configuration"></a>Información sobre cómo configurar el volcado de montón

Se habilitan los volcados del montón pasando opciones (a veces conocido como opts, o parámetros) toohello JVM cuando se inicia un servicio. La mayoría de los servicios Hadoop, puede modificar estas opciones de hello shell script utilizado toostart Hola servicio toopass.

En cada secuencia de comandos, hay una exportación para  **\* \_OPTS**, que contiene opciones de hello pasa toohello JVM. Por ejemplo, en hello **hadoop env.sh** en un script, línea hello que comienza con `export HADOOP_NAMENODE_OPTS=` contiene las opciones de Hola para hello NameNode servicio.

Asignación y reducción procesos son ligeramente diferentes, ya que estas operaciones son un proceso secundario de hello MapReduce servicio. Cada uno de ellos se asignan o reducir el proceso se ejecuta en un contenedor secundario, y hay dos entradas que contienen opciones de JVM Hola. Ambos están en **mapred-site.xml**:

* **mapreduce.admin.map.child.java.opts**
* **mapreduce.admin.reduce.child.java.opts**

> [!NOTE]
> Se recomienda con Ambari toomodify ambos Hola scripts y configuración mapred-site.xml, como Ambari controlar replicar cambios en nodos de clúster de Hola. Vea hello [Ambari utilizando](#using-ambari) sección para obtener pasos específicos.

### <a name="enable-heap-dumps"></a>Habilitar los volcados de montón

Hello siguiente opción permite que los volcados del montón cuando se produce un OutOfMemoryError:

    -XX:+HeapDumpOnOutOfMemoryError

Hola  **+**  indica que esta opción está habilitada. Hola predeterminado está deshabilitado.

> [!WARNING]
> Los volcados del montón no están habilitados para los servicios de Hadoop en HDInsight de forma predeterminada, como archivos de volcado de hello pueden ser grandes. Si habilitarlas para solucionar el problema, recuerde toodisable ellos una vez que ha reproducido Hola problema y archivos de volcado de hello recopilada.

### <a name="dump-location"></a>Ubicación de volcado

ubicación predeterminada de Hello para el archivo de volcado de memoria de hello es el directorio de trabajo actual de Hola. Puede controlar dónde hello archivo se almacena utilizando Hola después de opción:

    -XX:HeapDumpPath=/path

Por ejemplo, si se usa `-XX:HeapDumpPath=/tmp` hace Hola volcados toobe almacenado en el directorio de Hola/tmp.

### <a name="scripts"></a>Scripts

También puede desencadenar un script cuando se produzca un error **OutOfMemoryError** . Por ejemplo, se ha producido desencadenar una notificación para que sepa que error Hola. Siguiente de hello utilice opción tootrigger una secuencia de comandos en un __OutOfMemoryError__:

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> Puesto que Hadoop es un sistema distribuido, se debe colocar cualquier secuencia de comandos utilizada en todos los nodos de clúster de Hola que se ejecuta el servicio de hello en.
> 
> script de Hola debe también ser en una ubicación que sea accesible para hello cuenta Hola se ejecuta el servicio como y debe proporcionar permisos de ejecución. Por ejemplo, podría desear toostore scripts en `/usr/local/bin` y usar `chmod go+rx /usr/local/bin/filename.sh` toogrant permisos read y execute.

## <a name="using-ambari"></a>Uso de Ambari

configuración de hello toomodify para un servicio, Hola uso pasos:

1. Abra hello Ambari web interfaz de usuario para el clúster. dirección URL de Hello es https://YOURCLUSTERNAME.azurehdinsight.net.

    Cuando se le solicite, autenticar sitio toohello con el nombre de la cuenta de hello HTTP (valor predeterminado: administrador) y la contraseña para el clúster.

   > [!NOTE]
   > Se le pedirá una segunda vez por Ambari por nombre de usuario de Hola y la contraseña. Si es así, escriba Hola el mismo nombre de cuenta y contraseña

2. En lista de Hola de hello izquierda, seleccione el área de servicio de hello desea toomodify. Por ejemplo, **HDFS**. En el área central de hello, seleccione hello **configuraciones** ficha.

    ![Imagen de la web de Ambari web con la ficha de configuración HDFS seleccionada](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. Con hello **filtro...**  entrada, escriba **opts**. Solo se muestran los elementos que contienen este texto.

    ![Lista filtrada](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. Buscar hello  **\* \_OPTS** entrada de servicio de Hola que desee tooenable los volcados del montón para y agrega Hola opciones que desea tooenable. Hola después de la imagen, he agregado `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** entrada:

    ![HADOOP_NAMENODE_OPTS con -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > Al habilitar los volcados del montón para hello asignarán o reducen el proceso secundario, busque campos Hola denominados **mapreduce.admin.map.child.java.opts** y **mapreduce.admin.reduce.child.java.opts**.

    Hola de uso **guardar** botón toosave Hola cambiará. Puede escribir una nota breve que describe los cambios de Hola.

5. Una vez que se han aplicado los cambios de hello, Hola **debe reiniciarse** icono aparece junto a uno o varios servicios.

    ![icono «Es necesario reiniciar» y botón de reinicio](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. Seleccione cada servicio que requiere un reinicio y usar hello **acciones de servicio** botón demasiado**en modo de mantenimiento**. Modo de mantenimiento evita que las alertas se generan desde el servicio de Hola durante el reinicio.

    ![Activar el menú del modo de mantenimiento](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. Una vez que se ha habilitado el modo de mantenimiento, usar hello **reiniciar** botón para servicio de hello demasiado**reiniciar realiza todas las**

    ![Reiniciar todas las entradas afectadas](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > Hola entradas para hello **reiniciar** botón puede ser diferente para otros servicios.

8. Una vez que se hayan reiniciado los servicios de hello, usar hello **acciones de servicio** botón demasiado**activar el modo de mantenimiento**. Este tooresume Ambari supervisión de alertas de servicio de Hola.

