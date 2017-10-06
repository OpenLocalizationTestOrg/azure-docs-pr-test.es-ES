---
title: aaaTips para el uso de Hadoop en HDInsight basados en Linux - Azure | Documentos de Microsoft
description: "Obtengan sugerencias de implementación para el uso de clústeres de HDInsight basados en Linux (Hadoop) en un entorno familiar de Linux que se ejecuta en hello nube de Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c41c611c-5798-4c14-81cc-bed1e26b5609
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: a555622605079c9beae88ece872042e36d540c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="information-about-using-hdinsight-on-linux"></a>Información sobre el uso de HDInsight en Linux

Clústeres de HDInsight de Azure proporcionan Hadoop en un entorno familiar de Linux, ejecutando Hola nube de Azure. En la mayoría de los casos, debiera funcionar exactamente como cualquier otra instalación de Hadoop en Linux. Este documento detalla las diferencias específicas que debe tener en cuenta.

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Requisitos previos

Muchos de los pasos de hello en este documento usan hello siguientes utilidades, que necesitan toobe instalada en el sistema.

* [cURL](https://curl.haxx.se/) -usa toocommunicate con servicios basados en web
* [jq](https://stedolan.github.io/jq/) -tooparse JSON documentos utilizados
* [Azure 2.0 CLI](https://docs.microsoft.com/cli/azure/install-az-cli2) (versión preliminar) - tooremotely usado administrar servicios de Azure

## <a name="users"></a>Usuarios

A menos que esté [unido a un dominio](hdinsight-domain-joined-introduction.md), HDInsight debe considerarse un sistema de **un solo usuario**. Se crea una sola cuenta de usuario SSH con clúster de hello, con permisos de nivel de administrador. Se pueden crear cuentas adicionales de SSH, pero tienen también clúster de toohello de acceso de administrador.

HDInsight unido a un dominio admite varios usuarios y una configuración más granular de los permisos y roles. Para más información, consulte [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Administración de clústeres de HDInsight unidos a dominio).

## <a name="domain-names"></a>Nombres de dominio

Hola completo toouse (FQDN) del nombre de dominio cuando se conecta el clúster toohello desde Hola internet es  **&lt;clustername >. azurehdinsight.net** o (para SSH solo)  **&lt;clustername-ssh >. azurehdinsight.net**.

Internamente, cada nodo de clúster de hello tiene un nombre que se asigna durante la configuración de clúster. los nombres de clúster de toofind hello, vea hello **Hosts** página en hello Ambari Web UI. También puede usar Hola después tooreturn una lista de hosts de hello Ambari API de REST:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts" | jq '.items[].Hosts.host_name'

Reemplace **contraseña** con contraseña Hola de cuenta de administrador de Hola y **CLUSTERNAME** con nombre hello del clúster. Este comando devuelve un documento JSON que contiene una lista de hosts de hello en clúster de Hola. Jq es tooextract usado hello `host_name` valor del elemento para cada host.

Si necesita toofind Hola nombre del nodo de Hola para un servicio concreto, puede consultar Ambari de ese componente. Por ejemplo, hosts de hello toofind para el nodo de nombre de hello HDFS, utilice Hola siguiente comando:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/NAMENODE" | jq '.host_components[].HostRoles.host_name'

Este comando devuelve un documento JSON que describe el servicio de hello y, a continuación, extrae jq solo hello `host_name` valor para los hosts de Hola.

## <a name="remote-access-tooservices"></a>Tooservices de acceso remoto

* **Ambari (web)** - https://&lt;clustername&gt;.azurehdinsight.net

    Autenticar mediante contraseña y usuario del Administrador de clúster de hello y, a continuación, inicie sesión en tooAmbari.

    La autenticación es texto simple; siempre use HTTPS toohelp Asegúrese de que Hola conexión es segura.

    > [!IMPORTANT]
    > Algunos de web Hola interfaces de usuario disponibles a través de los nodos de acceso Ambari usando un nombre de dominio interno. No son públicamente accesible a través de nombres de dominio interno Hola internet. Puede recibir errores de "no se encontró el servidor" al intentar tooaccess algunas características sobre Hola Internet.
    >
    > toouse Hola toda la funcionalidad de interfaz de usuario, de la web de Ambari Hola utilice un SSH túnel tooproxy web tráfico toohello nodo principal del clúster. Vea [uso de SSH túnel tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie y otras interfaces de usuario web](hdinsight-linux-ambari-ssh-tunnel.md)

* **Ambari (REST)** - https://&lt;nombreDeClúster&gt;.azurehdinsight.net/ambari

    > [!NOTE]
    > Autenticar mediante contraseña y usuario del Administrador de clúster de Hola.
    >
    > La autenticación es texto simple; siempre use HTTPS toohelp Asegúrese de que Hola conexión es segura.

* **WebHCat (Templeton)** - https://&lt;nombreDeClúster&gt;.azurehdinsight.net/templeton

    > [!NOTE]
    > Autenticar mediante contraseña y usuario del Administrador de clúster de Hola.
    >
    > La autenticación es texto simple; siempre use HTTPS toohelp Asegúrese de que Hola conexión es segura.

* **SSH** - &lt;nombreDeClúster&gt;-ssh.azurehdinsight.net en los puertos 22 o 23. Puerto 22 es nodo principal en el principal de toohello tooconnect utilizados, mientras que 23 es tooconnect usado toohello secundaria. Para obtener más información sobre los nodos principales de hello, consulte [clústeres de disponibilidad y confiabilidad de Hadoop en HDInsight](hdinsight-high-availability-linux.md).

    > [!NOTE]
    > Solo puede acceder a los nodos principales del clúster de Hola a través de SSH desde un equipo cliente. Una vez conectado, a continuación, puede tener acceso a nodos de trabajador de Hola a través de SSH desde un nodo principal.

## <a name="file-locations"></a>Ubicaciones de archivo

Archivos de Hadoop pueden encontrarse en los nodos de clúster de Hola de `/usr/hdp`. Este directorio contiene Hola siguientes subdirectorios:

* **2.2.4.9-1**: nombre del directorio hello es la versión de Hola de hello Hortonworks Data Platform utilizando HDInsight. número de Hello en el clúster puede ser diferente de hello uno indicados a continuación.
* **actual**: este directorio contiene vínculos toosubdirectories en hello **2.2.4.9-1** directory. Este directorio existe para que no tiene número de versión de hello tooremember.

Se pueden encontrar datos de ejemplo y archivos JAR en el sistema de archivos distribuido de Hadoop en `/example` y `/HdiSamples`.

## <a name="hdfs-azure-storage-and-data-lake-store"></a>HDFS, Azure Storage y Data Lake Store

En la mayoría de las distribuciones de Hadoop, HDFS está respaldado por almacenamiento local en máquinas de hello en clúster de Hola. El uso de almacenamiento local puede ser costoso para una solución basada en la nube en la que se le cobra por hora o por minuto por los recursos de proceso.

HDInsight utiliza blobs en almacenamiento de Azure o almacén de Azure Data Lake como almacén predeterminado de Hola. Estos servicios proporcionan Hola siguientes ventajas:

* Almacenamiento económico a largo plazo
* Accesible desde servicios externos, como sitios web, utilidades para carga/descarga de archivos, SDK en varios idiomas y exploradores web.

> [!WARNING]
> HDInsight solo admite cuentas de Azure Storage de __uso general__. No es compatible actualmente con hello __almacenamiento de blobs__ tipo de cuenta.

Una cuenta de almacenamiento de Azure puede contener una too4.75 TB, aunque los blobs individuales (o archivos desde una perspectiva de HDInsight) sólo pueden crecer hasta too195 GB. Almacén de Azure Data Lake puede crecer dinámicamente toohold trillones de archivos, con mayores que un petabyte de archivos individuales. Para más información, consulte [Introducción a los blobs](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) y [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).

Cuando se utiliza el almacenamiento de Azure o almacén de Data Lake, no tiene nada especial de datos de saludo de HDInsight tooaccess toodo. Por ejemplo, hello siguiente comando enumera archivos hello `/example/data` carpeta independientemente de si se almacena en el almacenamiento de Azure o almacén de Data Lake:

    hdfs dfs -ls /example/data

### <a name="uri-and-scheme"></a>Identificador URI y esquema

Algunos comandos pueden requerir que esquema de hello toospecify como parte del programa Hola URI al tener acceso a un archivo. Por ejemplo, hello componente HDFS Storm requiere esquema de hello toospecify. Cuando se usa almacenamiento no predeterminados (almacenamiento agregado como clúster de toohello de almacenamiento "adicionales"), siempre debe utilizar el esquema de hello como parte del programa Hola URI.

Cuando se usa __el almacenamiento de Azure__, utilice uno de los siguientes esquemas de URI de Hola:

* `wasb:///`: accede al almacenamiento predeterminado mediante una comunicación sin cifrar.

* `wasbs:///`: accede al almacenamiento predeterminado mediante una comunicación cifrada.  esquema de Hello wasbs sólo es compatible desde HDInsight versión 3.6 y versiones posteriores.

* `wasb://<container-name>@<account-name>.blob.core.windows.net/`: se usa al comunicarse con una cuenta de almacenamiento no predeterminada. Por ejemplo, cuando tiene una cuenta de almacenamiento adicional o accede a los datos almacenados en una cuenta de almacenamiento que es accesible públicamente.

Cuando se usa __almacén de Data Lake__, utilice uno de los siguientes esquemas de URI de Hola:

* `adl:///`: Obtener acceso a almacén de Data Lake Hola predeterminado para el clúster de Hola.

* `adl://<storage-name>.azuredatalakestore.net/`: se usa al comunicarse con un almacén Data Lake Store no predeterminado. También utiliza datos tooaccess fuera del directorio raíz de Hola de su clúster de HDInsight.

> [!IMPORTANT]
> Cuando se usa el almacén de Data Lake como almacén predeterminado de Hola para HDInsight, debe especificar una ruta dentro de hello almacén toouse como raíz de Hola de almacenamiento de HDInsight. ruta de acceso de Hello predeterminada es `/clusters/<cluster-name>/`.
>
> Cuando se usa `/` o `adl:///` tooaccess datos, solo puede acceder a los datos almacenados en la raíz de hello (por ejemplo, `/clusters/<cluster-name>/`) del clúster de Hola. tooaccess datos en cualquier lugar en el almacén de hello, usar hello `adl://<storage-name>.azuredatalakestore.net/` formato.

### <a name="what-storage-is-hello-cluster-using"></a>El almacenamiento de clúster hello usa

Puede utilizar configuración de almacenamiento predeterminada de Ambari tooretrieve hello para el clúster de Hola. Comando información de configuración de HDFS tooretrieve mediante curl siguiente de Hola de uso y filtrar mediante [jq](https://stedolan.github.io/jq/):

```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'```

> [!NOTE]
> Esto devuelve Hola primer servidor de toohello de configuración que se aplica (`service_config_version=1`), que contiene esta información. Puede que tenga a toolist todas las versiones de configuración toofind Hola más reciente.

Este comando devuelve un toohello similar valor después de URI:

* `wasb://<container-name>@<account-name>.blob.core.windows.net` si usa una cuenta de Azure Storage.

    Hello nombre de cuenta nombre Hola de cuenta de almacenamiento de Azure de hello, mientras que el nombre del contenedor de hello es el contenedor de blobs de Hola que es raíz Hola Hola de almacenamiento de clúster.

* `adl://home` si usa Azure Data Lake Store. nombre de almacén de Data Lake de hello tooget, Hola de uso después de la llamada de REST:

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'```

    Este comando devuelve Hola después de nombre de host: `<data-lake-store-account-name>.azuredatalakestore.net`.

    directorio de hello tooget dentro de almacén de hello raíz Hola de HDInsight, Hola de uso después de la llamada de REST:

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'```

    Este comando devuelve un toohello similar de ruta de acceso después de la ruta de acceso: `/clusters/<hdinsight-cluster-name>/`.

También puede encontrar información de almacenamiento de hello usando Hola portal de Azure mediante Hola pasos:

1. Hola [portal de Azure](https://portal.azure.com/), seleccione el clúster de HDInsight.

2. De hello **propiedades** sección, seleccione **cuentas de almacenamiento**. se muestra la información de almacenamiento de Hello para el clúster de Hola.

### <a name="how-do-i-access-files-from-outside-hdinsight"></a>¿Cómo accedo a los archivos desde fuera de HDInsight?

Hay una varias maneras tooaccess datos de clúster de HDInsight de hello exterior. siguiente Hola es unos vínculos tooutilities y SDK que puede ser utilizado toowork con los datos:

Si usa __el almacenamiento de Azure__, vea los siguientes vínculos para ver las formas que puede tener acceso a los datos de Hola:

* [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): comandos de la interfaz de la línea de comandos para trabajar con Azure. Después de instalar, usar hello `az storage` comando para obtener ayuda sobre el uso de almacenamiento, o `az storage blob` para comandos específicos del blob.
* [blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): un script de Python para trabajar con blobs en almacenamiento de Azure.
* Diversos SDK:

    * [Java](https://github.com/Azure/azure-sdk-for-java)
    * [Node.js](https://github.com/Azure/azure-sdk-for-node)
    * [PHP](https://github.com/Azure/azure-sdk-for-php)
    * [Python](https://github.com/Azure/azure-sdk-for-python)
    * [Ruby](https://github.com/Azure/azure-sdk-for-ruby)
    * [.NET](https://github.com/Azure/azure-sdk-for-net)
    * [API de REST de almacenamiento](https://msdn.microsoft.com/library/azure/dd135733.aspx)

Si usa __almacén de Azure Data Lake__, vea los siguientes vínculos para ver las formas que puede tener acceso a los datos de Hola:

* [Explorador web](../data-lake-store/data-lake-store-get-started-portal.md)
* [PowerShell](../data-lake-store/data-lake-store-get-started-powershell.md)
* [CLI de Azure 2.0](../data-lake-store/data-lake-store-get-started-cli-2.0.md)
* [API de REST de WebHDFS](../data-lake-store/data-lake-store-get-started-rest-api.md)
* [Data Lake Tools para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)
* [.NET](../data-lake-store/data-lake-store-get-started-net-sdk.md)
* [Java](../data-lake-store/data-lake-store-get-started-java-sdk.md)
* [Python](../data-lake-store/data-lake-store-get-started-python.md)

## <a name="scaling"></a>Escalar el clúster

característica de ajuste de escala de clúster de Hello permite a toodynamically cambiar el número de Hola de nodos de datos usado por un clúster. Puedes realizar operaciones de escala mientras se están ejecutando otros trabajos o procesos en un clúster.

tipos de otro clúster de Hola se ven afectados mediante el escalado como sigue:

* **Hadoop**: cuando se reduzca el número de Hola de nodos de un clúster, algunos de los servicios de hello en clúster de Hola se reinician. Las operaciones de ajuste de escala puede provocar los trabajos en ejecución o pendientes toofail al término de Hola Hola la operación de escalado. Puede volver a enviar trabajos de hello una vez completada la operación de Hola.
* **HBase**: servidores regionales se equilibran automáticamente dentro de unos minutos después de finalizar la operación de escalado de Hola. servidores regionales de saldo de toomanually, usar hello pasos:

    1. Conecte el clúster de HDInsight de toohello mediante SSH. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

    2. Usar hello después de shell de HBase Hola toostart:

            hbase shell

    3. Una vez que ha cargado el shell de HBase hello, utilice Hola después servidores regionales de toomanually saldo hello:

            balancer

* **Storm**: debe reequilibrar todas las topologías Storm en ejecución después de realizar una operación de escalado. Reequilibrio permite que la configuración de paralelismo de tooreadjust Hola topología depende Hola nuevo número de nodos de clúster de Hola. toorebalance ejecuta estas topologías, use uno de hello siguientes opciones:

    * **SSH**: Conectar servidor toohello y comando de uso Hola siguiente toorebalance una topología:

            storm rebalance TOPOLOGYNAME

        También puede especificar sugerencias de paralelismo parámetros toooverride Hola proporcionadas originalmente mediante la topología de Hola. Por ejemplo, `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` reconfigura Hola procesos de trabajo de topología too5, 3 ejecutor para componente de azul pitorro hello y 10 ejecutor para componente de amarillo rayo de Hola.

    * **Interfaz de usuario de Storm**: pasos siguientes de Hola de uso toorebalance una topología con hello aluvión de interfaz de usuario.

        1. Abra **https://CLUSTERNAME.azurehdinsight.net/stormui** en el explorador web, donde CLUSTERNAME es nombre de Hola de su clúster de Storm. Si se le pide, escriba el nombre de administrador (admin) del clúster de HDInsight de Hola y la contraseña que especificó al crear el clúster de Hola.
        2. Seleccione la topología de Hola que desea toorebalance y luego seleccione hello **reequilibrar** botón. Especificar un intervalo de hello antes de realiza la operación de equilibra Hola.

Para obtener información específica sobre cómo ampliar tu clúster de HDInsight, consulta:

* [Administrar clústeres de Hadoop en HDInsight con hello portal de Azure](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [Administración de clústeres de Hadoop en HDInsight con Azure PowerShell](hdinsight-administer-use-command-line.md#scale-clusters)

## <a name="how-do-i-install-hue-or-other-hadoop-component"></a>¿Cómo puedo instalar Hue (u otro componente de Hadoop)?

HDInsight es un servicio administrado. Si Azure detecta un problema con el clúster de hello, pueden eliminar Hola errores de nodo y crear un nodo tooreplace lo. Si instala manualmente cosas en clúster de hello, no se conservan cuando se produce esta operación. En su lugar, use [acciones de script de HDInsight](hdinsight-hadoop-customize-cluster.md). Una acción de secuencia de comandos puede ser hello toomake usado siguientes cambios:

* Instalar y configurar un servicio o un sitio web, como Spark o Hue.
* Instale y configure un componente que requiere cambios de configuración en varios nodos de clúster de Hola. Por ejemplo, una variable de entorno requerida o la creación de un directorio de registro o de un archivo de configuración.

Las acciones de script son scripts de Bash. las secuencias de comandos de Hello ejecutar durante el aprovisionamiento de clústeres, pueden tooinstall usado y configurar componentes adicionales en el clúster de Hola. Secuencias de comandos de ejemplo se proporcionan para la instalación de Hola de los componentes siguientes:

* [Hue](hdinsight-hadoop-hue-linux.md)
* [Giraph.](hdinsight-hadoop-giraph-install-linux.md)
* [Solr](hdinsight-hadoop-solr-install-linux.md)

Para obtener información sobre el desarrollo de sus propias acciones de script, consulte [Desarrollo de la acción de script con HDInsight](hdinsight-hadoop-script-actions-linux.md).

### <a name="jar-files"></a>Archivos JAR

Algunas tecnologías de Hadoop se proporcionan en archivos jar independientes con funciones que se usan como parte de un trabajo de MapReduce o desde dentro de Pig o Hive. Mientras estos se pueden instalar mediante acciones de Script, a menudo no requiere ninguna configuración y pueden ser toohello cargado clúster después de aprovisionar y utilizar directamente. Si desea toomake seguro de componente de hello sobrevive restableciendo imagen inicial del clúster de Hola, puede almacenar archivos jar de hello en almacenamiento predeterminado de hello para el clúster (WASB o ADL).

Por ejemplo, si desea que la versión más reciente de hello toouse de [DataFu](http://datafu.incubator.apache.org/), puede descargar un archivo jar que contiene el proyecto de Hola y cargarlo en clúster de HDInsight toohello. A continuación, siga documentación de hello DataFu acerca de cómo toouse de Pig o Hive.

> [!IMPORTANT]
> Algunos componentes que son archivos jar de independiente se proporcionan con HDInsight, pero no están en la ruta de acceso de Hola. Si desea obtener un componente específico, puede usar Hola seguimiento toosearch para él en el clúster:
>
> ```find / -name *componentname*.jar 2>/dev/null```
>
> Este comando devuelve la ruta de acceso de Hola de los archivos jar coincidente.

toouse una versión diferente de un componente, la versión de Hola de carga que necesita y usarlo en los trabajos.

> [!WARNING]
> Componentes suministrados con clúster de HDInsight de hello son totalmente compatibles y Microsoft Support le ayuda a tooisolate y resolver los problemas relacionados toothese componentes.
>
> Componentes personalizados reciben soporte comercialmente razonable toohelp toofurther solucionar el problema de Hola. Esto podría producir en resolver el problema de hello ni pedir que tooengage canales disponibles para hello abrir tecnologías de origen donde se encuentra la amplia experiencia para que la tecnología. Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Además, los proyectos de Apache tienen sitios del proyecto en [http://apache.org](http://apache.org), por ejemplo, [Hadoop](http://hadoop.apache.org/) y [Spark](http://spark.apache.org/).

## <a name="next-steps"></a>Pasos siguientes

* [Migrar de HDInsight basados en Windows en función de tooLinux](hdinsight-migrate-from-windows-to-linux.md)
* [Uso de Hive con HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con HDInsight](hdinsight-use-pig.md)
* [Uso de trabajos de MapReduce con HDInsight](hdinsight-use-mapreduce.md)
