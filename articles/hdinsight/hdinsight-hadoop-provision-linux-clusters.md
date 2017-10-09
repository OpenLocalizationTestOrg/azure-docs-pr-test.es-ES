---
title: "el programa de instalación de aaaCluster para Hadoop, Spark, Kafka, HBase o R Server - HDInsight de Azure | Documentos de Microsoft"
description: "Configurar clústeres de Hadoop, Kafka, Spark, HBase, R Server o aluvión de HDInsight desde un explorador, Hola CLI de Azure, Azure PowerShell, REST o SDK."
keywords: "configuración de clústeres de hadoop, configuración de clústeres de kafka, configuración de clústeres de spark, qué es un clúster en hadoop"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 23a01938-3fe5-4e2e-8e8b-3368e1bbe2ca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: jgao
ms.openlocfilehash: 80ec59d8a39f7fccb940503fd2dc3ae5afee6bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-clusters-in-hdinsight-with-hadoop-spark-kafka-and-more"></a>Configuración de clústeres en HDInsight con Hadoop, Spark, Kafka, etc.

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Obtenga información acerca de cómo tooset una copia de seguridad y configurar clústeres de HDInsight con Hadoop, Spark, Kafka, Hive interactivo, HBase, R Server o Storm. Además, obtenga información acerca de cómo toocustomize clústeres y aumenta la seguridad mediante la combinación de dominio de tooa.

Un clúster de Hadoop se compone de varias máquinas virtuales (nodos) que se usan para el procesamiento distribuido de tareas. HDInsight de Azure controla los detalles de implementación de instalación y configuración de los nodos individuales, por lo que solo tiene información de configuración general de tooprovide. 

> [!IMPORTANT]
>La facturación de clúster de HDInsight empieza cuando un clúster se crea y se detiene cuando se elimina el clúster de Hola. Se facturan por minuto realizando una prorrata, por lo que siempre debe eliminar aquellos que ya no se estén utilizando. Obtenga información acerca de cómo demasiado[eliminar un clúster.](hdinsight-delete-cluster.md)
>

## <a name="cluster-setup-methods"></a>Métodos de configuración de clústeres
Hello tabla siguiente se muestran diferentes métodos de hello que puede utilizar tooset de un clúster de HDInsight.

| Clústeres creados con | Explorador web | Línea de comandos | API de REST | SDK | 
| --- |:---:|:---:|:---:|:---:|
| [Portal de Azure](hdinsight-hadoop-create-linux-clusters-portal.md) |✔ |&nbsp; |&nbsp; |&nbsp; |
| [Factoría de datos de Azure](hdinsight-hadoop-create-linux-clusters-adf.md) |✔ |✔ |✔ |✔ |
| [CLI de Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [cURL](hdinsight-hadoop-create-linux-clusters-curl-rest.md) |&nbsp; |✔ |✔ |&nbsp; |
| [.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |&nbsp; |&nbsp; |&nbsp; |✔ |
| [Plantillas del Administrador de recursos de Azure](hdinsight-hadoop-create-linux-clusters-arm-templates.md) |&nbsp; |✔ |&nbsp; |&nbsp; |

## <a name="quick-create-basic-cluster-setup"></a>Creación rápida: configuración básica de clústeres
Este artículo le guiará por el programa de instalación en hello [portal de Azure](https://portal.azure.com), donde puede crear un clúster de HDInsight con *creación rápida* o *personalizado*. 

Siga las instrucciones de Hola pantalla toodo una configuración de clúster básico. A continuación se proporcionan detalles para:

* [Nombre del grupo de recursos](#resource-group-name)
* [Tipos y configuración de clústeres](#cluster-types) 
* [Inicio de sesión de clúster y nombre de usuario SSH](#cluster-login-and-ssh-username)
* [Ubicación](#location)

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Para más información, vea la sección [Retirada de HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>

## <a name="resource-group-name"></a>Definición de un nombre de grupo de recursos 

[El Administrador de recursos Azure](../azure-resource-manager/resource-group-overview.md) podrá trabajar con recursos de hello en la aplicación como un grupo, denominado tooas un grupo de recursos de Azure. Puede implementar, actualizar, supervisar o eliminar todos los recursos de hello para la aplicación en una sola operación coordinada.

## <a name="cluster-types"></a> Tipos y configuración de clústeres
HDInsight de Azure proporciona actualmente siguiente Hola clúster tipos, cada uno con un conjunto de componentes tooprovide determinadas funciones.

> [!IMPORTANT]
> Los clústeres de HDInsight están disponibles en distintos tipos, cada uno de ellos para una carga de trabajo o una tecnología única. No hay ningún toocreate método admitido para un clúster que combina varios tipos, como Storm y HBase en un clúster. Si su solución requiere tecnologías que están repartidas entre varios tipos de clúster de HDInsight, un [red virtual de Azure](https://docs.microsoft.com/azure/virtual-network) puede conectarse a tipos de clúster de hello necesario. 
>
>

| Tipo de clúster | Funcionalidad |
| --- | --- |
| [Hadoop](hdinsight-hadoop-introduction.md) |Consulta por lotes y análisis de datos almacenados |
| [HBase](hdinsight-hbase-overview.md) |Procesamiento de grandes cantidades de datos no SQL sin esquema |
| [Storm](hdinsight-storm-overview.md) |Procesamiento de eventos en tiempo real |
| [Spark](hdinsight-apache-spark-overview.md) |Procesamiento en memoria, consultas interactivas, procesamiento de transmisión de microlotes |
| [Kafka (versión preliminar)](hdinsight-apache-kafka-introduction.md) | Una plataforma de transmisión por secuencias distribuida que puede ser canalizaciones de datos de transmisión por secuencias en tiempo real de toobuild usado y aplicaciones |
| [R Server](hdinsight-hadoop-r-server-overview.md) |Distintas capacidades de estadísticas de macrodatos, modelado de predicción y aprendizaje automático |
| [Interactive Hive (versión preliminar)](hdinsight-hadoop-use-interactive-hive.md) |Almacenamiento en caché en memoria para realizar consultas de Hive interactivas y más rápidas |

### <a name="number-of-nodes-for-each-cluster-type"></a>Número de nodos de cada tipo de clúster
Cada tipo de clúster tiene su propio número de nodos, terminología para los nodos y tamaño de máquina virtual predeterminado. Hola en la tabla siguiente, número de Hola de nodos para cada tipo de nodo es entre paréntesis.

| Tipo | Nodos | Diagrama |
| --- | --- | --- |
| Hadoop |Nodo principal (2), nodo de datos (más de 1) |![Nodos de clúster de Hadoop en HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hadoop-cluster-type-nodes.png) |
| HBase |Servidor principal (2), servidor de región (más de 1), nodo maestro/ZooKeeper (3) |![Nodos de clúster de HBase en HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hbase-cluster-type-setup.png) |
| Storm |Nodo Nimbus (2), servidor de supervisor (más de 1), nodo ZooKeeper (3) |![Nodos de clúster de Storm en HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-storm-cluster-type-setup.png) |
| Spark |Nodo principal (2), nodo de trabajo (más de 1), nodo ZooKeeper (3) (gratis para el tamaño de máquina virtual ZooKeeper A1) |![Nodos de clúster de Spark en HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-spark-cluster-type-setup.png) |

Para obtener más información, consulte [predeterminado tamaños de máquinas virtuales y la configuración de nodo para los clústeres de](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters) en "¿Cuáles son los componentes de Hadoop de Hola y versiones de HDInsight?"

### <a name="hdinsight-version"></a>Versión de HDInsight
Elegir versión de Hola de HDInsight para este clúster. Para más información, consulte [Versiones compatibles de HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="cluster-tiers"></a>Nivel de clúster: niveles de servicio de HDInsight

HDInsight de Azure proporciona las ofertas de nube de hello grandes cantidades de datos en dos niveles de servicio: Standard y Premium.  Para más información, vea [HDInsight Standard y HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium).

Hello captura de pantalla siguiente muestra hello información del portal de Azure para elegir los tipos de clúster.

![Configuración de HDInsight Premium](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-type-configuration.png)


## <a name="cluster-login-and-ssh-user-name"></a>Inicio de sesión de clúster y nombre de usuario SSH
Con los clústeres de HDInsight, puede configurar dos cuentas de usuario durante la creación del clúster:

* Usuario HTTP: nombre de usuario predeterminado de hello es *administración*. Usa la configuración básica de hello en hello portal de Azure. A veces, se denomina "Usuario de clúster".
* Usuario SSH (clústeres de Linux): tooconnect usado toohello clúster a través de SSH. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="location"></a>Ubicación (regiones) para clústeres y almacenamiento

No es necesario ubicación del clúster toospecify Hola explícitamente: Hola clúster sea Hola misma ubicación que el almacenamiento de hello predeterminado. Para obtener una lista de regiones admitidas, haga clic en hello **región** lista de desplegable en [precios HDInsight](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

## <a name="storage-endpoints-for-clusters"></a>Puntos de conexión de almacenamiento para clústeres

Aunque una instalación local de Hadoop usa Hola sistema de archivos distribuido de Hadoop (HDFS) para el almacenamiento en clúster de hello, en hello en la nube usar los puntos de conexión de almacenamiento conectado toocluster. Los clústeres de HDInsight usan [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) o [blobs de Azure Storage](hdinsight-hadoop-use-blob-storage.md). Uso de almacenamiento de Azure o almacén de Data Lake significa que puede eliminar con seguridad los clústeres de HDInsight de hello utilizados para el cálculo mientras se conservan los datos. 

> [!WARNING]
> No se admite con una cuenta de almacenamiento adicional en una ubicación diferente del clúster de HDInsight Hola.

Durante la configuración, para punto de conexión de almacenamiento de hello predeterminado se especifica un contenedor de blobs de una cuenta de almacenamiento de Azure o un almacén de Data Lake. Hello almacenamiento predeterminado contiene aplicación y sistema de registros. Si lo desea, puede especificar cuentas de almacenamiento de Azure vinculadas adicionales y las cuentas de almacén de Data Lake que Hola clúster pueden tener acceso. clúster de HDInsight de Hola y almacenamiento dependientes Hola cuentas deben estar en Hola misma ubicación de Azure.

![Configuración de almacenamiento de clústeres: puntos de conexión de almacenamiento compatibles con HDFS](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-creation-storage.png)

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


### <a name="optional-metastores"></a>Tiendas de metadatos opcionales
Puede crear tiendas de metadatos opcionales de Hive u Oozie. Pero no todos los tipos de clúster admiten las tiendas de metadatos; además, Azure SQL Data Warehouse no es compatible con ellas. 

> [!IMPORTANT]
> Cuando se crea una tienda de metadatos personalizado, no use guiones, guiones ni espacios en el nombre de la base de datos de Hola. Esto puede causar toofail de proceso de creación de clúster de Hola.

### <a name="use-hiveoozie-metastore"></a>Hive Metastore

Si desea tooretain las tablas de Hive después de eliminar un clúster de HDInsight, use una tienda de metadatos personalizado. A continuación, puede adjuntar clúster de HDInsight de tooanother de hello tienda de metadatos.

Una instancia de Metastore de HDInsight creada para una versión del clúster de HDInsight no se puede compartir entre diferentes versiones del clúster de HDInsight. Para obtener una lista de versiones de HDInsight, consulte [Versiones compatibles de HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="oozie-metastore"></a>Oozie Metastore

tooincrease rendimiento al utilizar Oozie, use una tienda de metadatos personalizado. Una tienda de metadatos también puede proporcionar acceso tooOozie trabajo datos después de eliminar el clúster. 

> [!IMPORTANT]
> No puede volver a usar un Oozie Metastore personalizado. toouse una tienda de metadatos de Oozie personalizado, debe proporcionar una base de datos de SQL Azure vacía al crear el clúster de HDInsight Hola.

## <a name="configure-cluster-size"></a>Configuración del tamaño del clúster

Se le facturará para el uso de nodo para siempre y cuando exista clúster Hola. La facturación se inicia cuando se crea un clúster y se detiene cuando se elimina el clúster de Hola. Los clústeres no se puede desasignar ni ponerse en espera.

costo de Hola de clústeres de HDInsight viene determinado por número de Hola de nodos y tamaños de máquinas virtuales de Hola para los nodos de Hola. 

Los distintos tipos de clúster tienen distintos tipos, número y tamaños de nodos:
* Tipo de clúster predeterminado de Hadoop: 
    * Dos *nodos principales*  
    * Cuatro *nodos de datos*
* Tipo de clúster predeterminado de Storm: 
    * Dos *nodos Nimbus*
    * Tres *nodos ZooKeeper*
    * Cuatro *nodos de supervisor* 

Si simplemente se está probando HDInsight, se recomienda usar un nodo de datos. Para más información sobre los precios de HDInsight, vea [HDInsight Precios](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

> [!NOTE]
> límite de tamaño de clúster de Hello varía para las suscripciones de Azure. Póngase en contacto con [soporte de facturación de Azure](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) límite de hello tooincrease.
>

Cuando se usa el clúster de Hola de tooconfigure portal Azure de hello, tamaño de nodo de hello está disponible a través de hello **los niveles de precios de nodo** hoja. En el portal de hello, también puede ver Hola costo asociado con tamaños de otro nodo de Hola. 

![Tamaños de nodo de máquina virtual de HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-node-sizes.png)

### <a name="virtual-machine-sizes"></a>Tamaños de máquina virtual 
Cuando se implementan clústeres, elija recursos de proceso basados en la solución de hello piensa toodeploy. Hola que máquinas virtuales siguientes sirven para clústeres de HDInsight:
* Máquinas virtuales de las series A y D1-4: [tamaños de máquina virtual de Linux de uso general](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)
* Máquinas virtuales de la serie D11-14: [tamaños de máquina virtual de Linux optimizados para memoria](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)

toofind espera el valor que debe usar toospecify un tamaño de memoria virtual durante la creación de un clúster con Hola diferentes SDK o durante el uso de PowerShell de Azure, consulte [toouse para clústeres de HDInsight de tamaños de máquina virtual](../cloud-services/cloud-services-sizes-specs.md#size-tables). De este artículo vinculado, utilice el valor de Hola Hola **tamaño** columnas de tablas de Hola.

> [!IMPORTANT]
> Si necesita más de 32 nodos de trabajo en un clúster, tiene que seleccionar un tamaño de nodo principal con al menos 8 núcleos y 14 GB de RAM.
>
>

Para más información, consulte [Tamaños de las máquinas virtuales Linux en Azure](../virtual-machines/windows/sizes.md). Para obtener información sobre los precios de saludo diversos tamaños, vea [precios HDInsight](https://azure.microsoft.com/pricing/details/hdinsight).   

## <a name="custom-cluster-setup"></a>Configuración personalizada de clústeres
El programa de instalación de clúster personalizado se basa en hello rápido crear una configuración y agrega Hola siguientes opciones:
- [Aplicaciones de HDInsight](#hdinsight-applications)
- [Tamaño del clúster](#cluster-size)
- Configuración avanzada
  - [Acciones de script](#customize-clusters-using-script-action)
  - [Red virtual](#use-virtual-network)

## <a name="install-hdinsight-applications-on-clusters"></a>Instalar aplicaciones de HDInsight en clústeres

Una aplicación de HDInsight es una aplicación que los usuarios pueden instalar en un clúster de HDInsight basado en Linux. Puede usar aplicaciones proporcionadas por Microsoft, de terceros o desarrolladas por sí mismo. Para más información, consulte [Instalación de aplicaciones de Hadoop de terceros en Azure HDInsight](hdinsight-apps-install-applications.md).

La mayoría de las aplicaciones de HDInsight de Hola se instala en un nodo del borde vacío.  Un nodo del borde vacío es una máquina virtual de Linux con hello mismas herramientas de cliente instalado y configurado como en el nodo principal de Hola. Puede usar el nodo del borde de hello para tener acceso clúster hello, probar las aplicaciones cliente y las aplicaciones cliente de hospedaje. Para obtener más información, consulte [Uso de nodos perimetrales vacíos en HDInsight](hdinsight-apps-use-edge-node.md).

## <a name="advanced-settings-script-actions"></a>Configuración avanzada: acciones de script

Puede instalar componentes adicionales o personalizar la configuración del clúster mediante el uso de scripts durante la creación. Estos scripts se invocan a través de **acción de secuencia de comandos**, que es una opción de configuración que se puedan usar desde Hola portal de Azure, cmdlets de Windows PowerShell de HDInsight o hello HDInsight .NET SDK. Para obtener más información, consulte [Personalización de un clúster de HDInsight mediante la acción de script](hdinsight-hadoop-customize-cluster-linux.md).

Algunos componentes de Java nativo, como Mahout y en cascada, se pueden ejecutar en el clúster de hello como archivos de almacenamiento de Java (JAR). Estos archivos JAR pueden ser distribuida tooAzure almacenamiento y envían tooHDInsight clústeres con los mecanismos de envío de trabajos de Hadoop. Para obtener más información, consulte [Envío de trabajos de Hadoop mediante programación](hdinsight-submit-hadoop-jobs-programmatically.md).

> [!NOTE]
> Si tiene problemas de implementación de clústeres de tooHDInsight archivos JAR, o llamar a archivos JAR en clústeres de HDInsight, póngase en contacto con [Microsoft Support](https://azure.microsoft.com/support/options/).
>
> Cascading no se admite en HDInsight, y no puede optar a recibir soporte técnico de Microsoft. Para obtener listas de componentes compatibles, vea [cuáles son las novedades en las versiones de clúster Hola proporcionadas por HDInsight](hdinsight-component-versioning.md).
>
>

A veces, desea hello tooconfigure siguientes archivos de configuración durante el proceso de creación de hello:

* clusterIdentity.xml
* core-site.xml
* gateway.xml
* hbase-env.xml
* hbase-site.xml
* hdfs-site.xml
* hive-env.xml
* hive-site.xml
* mapred-site
* oozie-site.xml
* oozie-env.xml
* storm-site.xml
* tez-site.xml
* webhcat-site.xml
* yarn-site.xml

Para más información, consulte [Personalización de los clústeres de HDInsight con Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).

## <a name="advanced-settings-extend-clusters-with-a-virtual-network"></a>Configuración avanzada: extensión de clústeres con una red virtual
Si su solución requiere tecnologías que están repartidas entre varios tipos de clúster de HDInsight, un [red virtual de Azure](https://docs.microsoft.com/azure/virtual-network) puede conectarse a tipos de clúster de hello necesario. Esta configuración permite clústeres hello y cualquier código que implementa toothem, toodirectly se comunican entre sí.

Para más información sobre cómo usar una red virtual de Azure con HDInsight, consulte el artículo sobre cómo [Extensión de HDInsight con redes virtuales de Azure](hdinsight-extend-hadoop-virtual-network.md).

Para ver un ejemplo de cómo usar dos tipos de clúster en una red virtual de Azure, consulte [Análisis de datos de sensores con Storm y HBase](hdinsight-storm-sensor-data-analysis.md). Para obtener más información sobre el uso de HDInsight con una red virtual, incluidos los requisitos específicos de configuración de red virtual de hello, consulte [capacidades de HDInsight extender mediante el uso de red Virtual de Azure](hdinsight-extend-hadoop-virtual-network.md).

## <a name="troubleshoot-access-control-issues"></a>Solución de problemas de control de acceso

Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Pasos siguientes

- [¿Cuáles son HDInsight, ecosistema de Hadoop de Hola y clústeres de Hadoop?](hdinsight-hadoop-introduction.md)
- [Introducción al uso de Hadoop en HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
- [Trabajo en Hadoop en HDInsight desde un equipo Windows](hdinsight-hadoop-windows-tools.md)
