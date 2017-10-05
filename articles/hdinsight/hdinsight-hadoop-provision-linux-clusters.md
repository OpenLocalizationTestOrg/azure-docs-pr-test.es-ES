---
title: "Configuración de clústeres de Hadoop, Spark, Kafka, HBase o R Server - Azure HDInsight | Microsoft Docs"
description: "Configure clústeres de Hadoop, Kafka, Spark, HBase, R Server o Storm para HDInsight desde un explorador, la CLI de Azure, Azure PowerShell, REST o el SDK."
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
ms.openlocfilehash: 473d71672cadb1d23f5942cb70294d213a8bbbca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-clusters-in-hdinsight-with-hadoop-spark-kafka-and-more"></a>Configuración de clústeres en HDInsight con Hadoop, Spark, Kafka, etc.

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Aprenda a instalar y configurar clústeres en HDInsight con Hadoop, Spark, Kafka, Hive interactivo, HBase, R Server o Storm. Además, aprenda a personalizar clústeres y a aumentar la seguridad al asociarlos a un dominio.

Un clúster de Hadoop se compone de varias máquinas virtuales (nodos) que se usan para el procesamiento distribuido de tareas. Azure HDInsight se ocupa de los detalles de implementación de la instalación y configuración de los nodos individuales, por lo que solo tiene que proporcionar información de configuración general. 

> [!IMPORTANT]
>La facturación del clúster de HDInsight se inicia una vez creado el clúster y solo se detiene cuando se elimina. Se facturan por minuto realizando una prorrata, por lo que siempre debe eliminar aquellos que ya no se estén utilizando. Aprenda a [eliminar un clúster](hdinsight-delete-cluster.md).
>

## <a name="cluster-setup-methods"></a>Métodos de configuración de clústeres
La tabla siguiente muestra los distintos métodos que se pueden usar para configurar un clúster de HDInsight.

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
Este artículo le guía a lo largo del proceso de configuración en [Azure Portal](https://portal.azure.com), donde puede crear un clúster de HDInsight con *Creación rápida* o *Personalizado*. 

Siga las instrucciones en pantalla para llevar a cabo una configuración básica de un clúster. A continuación se proporcionan detalles para:

* [Nombre del grupo de recursos](#resource-group-name)
* [Tipos y configuración de clústeres](#cluster-types) 
* [Inicio de sesión de clúster y nombre de usuario SSH](#cluster-login-and-ssh-username)
* [Ubicación](#location)

> [!IMPORTANT]
> Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores. Para más información, vea [Retirada de HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>

## <a name="resource-group-name"></a>Definición de un nombre de grupo de recursos 

[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) lo ayuda a trabajar con los recursos de la aplicación como grupo, al que se conoce como "grupo de recursos de Azure". Puede implementar, actualizar, supervisar o eliminar todos los recursos de la aplicación en una operación única y coordinada.

## <a name="cluster-types"></a> Tipos y configuración de clústeres
Actualmente, Azure HDInsight proporciona los siguientes tipos de clúster, cada uno de ellos con un conjunto de componentes que ofrecen determinadas funcionalidades.

> [!IMPORTANT]
> Los clústeres de HDInsight están disponibles en distintos tipos, cada uno de ellos para una carga de trabajo o una tecnología única. No hay ningún método admitido para crear un solo clúster que combine varios tipos, como Storm y HBase. Si la solución requiere tecnologías repartidas entre varios tipos de clústeres de HDInsight, una [red virtual de Azure](https://docs.microsoft.com/azure/virtual-network) puede conectar los tipos de clústeres necesarios. 
>
>

| Tipo de clúster | Funcionalidad |
| --- | --- |
| [Hadoop](hdinsight-hadoop-introduction.md) |Consulta por lotes y análisis de datos almacenados |
| [HBase](hdinsight-hbase-overview.md) |Procesamiento de grandes cantidades de datos no SQL sin esquema |
| [Storm](hdinsight-storm-overview.md) |Procesamiento de eventos en tiempo real |
| [Spark](hdinsight-apache-spark-overview.md) |Procesamiento en memoria, consultas interactivas, procesamiento de transmisión de microlotes |
| [Kafka (versión preliminar)](hdinsight-apache-kafka-introduction.md) | Una plataforma de streaming distribuida que se puede utilizar para compilar aplicaciones y canalizaciones de datos de streaming en tiempo real. |
| [R Server](hdinsight-hadoop-r-server-overview.md) |Distintas capacidades de estadísticas de macrodatos, modelado de predicción y aprendizaje automático |
| [Interactive Hive (versión preliminar)](hdinsight-hadoop-use-interactive-hive.md) |Almacenamiento en caché en memoria para realizar consultas de Hive interactivas y más rápidas |

### <a name="number-of-nodes-for-each-cluster-type"></a>Número de nodos de cada tipo de clúster
Cada tipo de clúster tiene su propio número de nodos, terminología para los nodos y tamaño de máquina virtual predeterminado. En la siguiente tabla, el número de nodos de cada tipo de nodo se muestra entre paréntesis.

| Tipo | Nodos | Diagrama |
| --- | --- | --- |
| Hadoop |Nodo principal (2), nodo de datos (más de 1) |![Nodos de clúster de Hadoop en HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hadoop-cluster-type-nodes.png) |
| HBase |Servidor principal (2), servidor de región (más de 1), nodo maestro/ZooKeeper (3) |![Nodos de clúster de HBase en HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hbase-cluster-type-setup.png) |
| Storm |Nodo Nimbus (2), servidor de supervisor (más de 1), nodo ZooKeeper (3) |![Nodos de clúster de Storm en HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-storm-cluster-type-setup.png) |
| Spark |Nodo principal (2), nodo de trabajo (más de 1), nodo ZooKeeper (3) (gratis para el tamaño de máquina virtual ZooKeeper A1) |![Nodos de clúster de Spark en HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-spark-cluster-type-setup.png) |

Para más información, vea [Configuración de nodo predeterminada y tamaños de máquina virtual para clústeres](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters) en "¿Cuáles son los componentes y versiones de Hadoop disponibles con HDInsight?"

### <a name="hdinsight-version"></a>Versión de HDInsight
Elija la versión de HDInsight para este clúster. Para más información, consulte [Versiones compatibles de HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="cluster-tiers"></a>Nivel de clúster: niveles de servicio de HDInsight

Azure HDInsight proporciona las ofertas de la nube de macrodatos en dos niveles de servicio: Standard y Premium.  Para más información, vea [HDInsight Standard y HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium).

La captura de pantalla siguiente muestra la información del Portal de Azure para elegir los tipos de clúster:

![Configuración de HDInsight Premium](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-type-configuration.png)


## <a name="cluster-login-and-ssh-user-name"></a>Inicio de sesión de clúster y nombre de usuario SSH
Con los clústeres de HDInsight, puede configurar dos cuentas de usuario durante la creación del clúster:

* Usuario HTTP: el nombre de usuario predeterminado es *admin*. Emplea la configuración básica en el portal de Azure. A veces, se denomina "Usuario de clúster".
* Usuario SSH (clústeres de Linux): se usa para conectarse al clúster mediante SSH. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="location"></a>Ubicación (regiones) para clústeres y almacenamiento

No es necesario especificar la ubicación del clúster de forma explícita: está en la misma ubicación que el almacenamiento predeterminado. Si desea obtener una lista de las regiones admitidas, haga clic en la lista desplegable **Región** en [Precios de HDInsight](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

## <a name="storage-endpoints-for-clusters"></a>Puntos de conexión de almacenamiento para clústeres

Aunque una instalación local de Hadoop usa el sistema de archivos distribuido de Hadoop (HDFS) para el almacenamiento en el clúster, en la nube se usan puntos de conexión de almacenamiento conectados al clúster. Los clústeres de HDInsight usan [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) o [blobs de Azure Storage](hdinsight-hadoop-use-blob-storage.md). El empleo de Azure Storage o Data Lake Store significa que puede eliminar con seguridad los clústeres de HDInsight usados para el cálculo y conservar los datos. 

> [!WARNING]
> No se admite el uso de una cuenta de almacenamiento adicional en una ubicación diferente a la del clúster de HDInsight.

Durante la configuración se especifica un contenedor de blobs de una cuenta de Azure Storage o de Data Lake Store para el punto de conexión de almacenamiento predeterminado. El almacenamiento predeterminado contiene los registros del sistema y de la aplicación. De manera opcional, puede especificar más cuentas vinculadas de Azure Storage y cuentas de Data Lake Store a las que el clúster pueda acceder. El clúster de HDInsight y las cuentas de almacenamiento dependientes deben estar en la misma ubicación de Azure.

![Configuración de almacenamiento de clústeres: puntos de conexión de almacenamiento compatibles con HDFS](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-creation-storage.png)

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


### <a name="optional-metastores"></a>Tiendas de metadatos opcionales
Puede crear tiendas de metadatos opcionales de Hive u Oozie. Pero no todos los tipos de clúster admiten las tiendas de metadatos; además, Azure SQL Data Warehouse no es compatible con ellas. 

> [!IMPORTANT]
> Cuando cree una tienda de metadatos personalizada, no use guiones ni espacios en el nombre de la base de datos. Podría provocar que el proceso de creación del clúster diera error.

### <a name="use-hiveoozie-metastore"></a>Hive Metastore

Si quiere conservar las tablas de Hive después de eliminar un clúster de HDInsight, use una tienda de metadatos personalizada. Luego puede adjuntar la tienda de metadatos a otro clúster de HDInsight.

Una instancia de Metastore de HDInsight creada para una versión del clúster de HDInsight no se puede compartir entre diferentes versiones del clúster de HDInsight. Para obtener una lista de versiones de HDInsight, consulte [Versiones compatibles de HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="oozie-metastore"></a>Oozie Metastore

Para aumentar el rendimiento al usar Oozie, utilice un Metastore personalizado. Una tienda de metadatos también puede proporcionar acceso a datos de trabajo de Oozie después de eliminar el clúster. 

> [!IMPORTANT]
> No puede volver a usar un Oozie Metastore personalizado. Para usar un Oozie Metastore personalizado, debe proporcionar una base de datos Azure SQL Database vacía al crear el clúster HDInsight.

## <a name="configure-cluster-size"></a>Configuración del tamaño del clúster

Mientras que exista el clúster se le facturará por el uso de nodos. La facturación se inicia una vez creado el clúster y se detiene cuando se elimina el clúster. Los clústeres no se puede desasignar ni ponerse en espera.

El costo de los clústeres de HDInsight viene determinado por el número de nodos y por los tamaños de las máquinas virtuales de los nodos. 

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
> El límite de tamaño del clúster varía entre las suscripciones a Azure. Póngase en contacto con el [servicio de soporte técnico de facturación de Azure](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) para aumentar el límite.
>

Al usar el portal de Azure para configurar el clúster, el tamaño del nodo está disponible en la hoja **Niveles de precios de nodo**. En el portal también puede ver el costo asociado a los diferentes tamaños de nodo. 

![Tamaños de nodo de máquina virtual de HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-node-sizes.png)

### <a name="virtual-machine-sizes"></a>Tamaños de máquina virtual 
Al implementar clústeres, elija los recursos de proceso en función de la solución que tenga previsto implementar. Las máquinas virtuales siguientes se usan para clústeres de HDInsight:
* Máquinas virtuales de las series A y D1-4: [tamaños de máquina virtual de Linux de uso general](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)
* Máquinas virtuales de la serie D11-14: [tamaños de máquina virtual de Linux optimizados para memoria](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)

Para averiguar el valor que debe usar para especificar un tamaño de máquina virtual durante la creación de un clúster mediante los distintos SDK o mientras usa Azure PowerShell, vea [Tamaños de máquina virtual para clústeres de HDInsight](../cloud-services/cloud-services-sizes-specs.md#size-tables). Use el valor de la columna **Tamaño** de las tablas de este artículo vinculado.

> [!IMPORTANT]
> Si necesita más de 32 nodos de trabajo en un clúster, tiene que seleccionar un tamaño de nodo principal con al menos 8 núcleos y 14 GB de RAM.
>
>

Para más información, consulte [Tamaños de las máquinas virtuales Linux en Azure](../virtual-machines/windows/sizes.md). Para más información sobre los precios de los diferentes tamaños, consulte [Precios de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight).   

## <a name="custom-cluster-setup"></a>Configuración personalizada de clústeres
La configuración personalizada de clústeres se basa en el valor Creación rápida y agrega las siguientes opciones:
- [Aplicaciones de HDInsight](#hdinsight-applications)
- [Tamaño del clúster](#cluster-size)
- Configuración avanzada
  - [Acciones de script](#customize-clusters-using-script-action)
  - [Red virtual](#use-virtual-network)

## <a name="install-hdinsight-applications-on-clusters"></a>Instalar aplicaciones de HDInsight en clústeres

Una aplicación de HDInsight es una aplicación que los usuarios pueden instalar en un clúster de HDInsight basado en Linux. Puede usar aplicaciones proporcionadas por Microsoft, de terceros o desarrolladas por sí mismo. Para más información, consulte [Instalación de aplicaciones de Hadoop de terceros en Azure HDInsight](hdinsight-apps-install-applications.md).

La mayoría de las aplicaciones de HDInsight se instalan en un nodo perimetral vacío.  Un nodo perimetral vacío es una máquina virtual Linux con las mismas herramientas cliente instaladas y configuradas que en el nodo principal. Se puede usar el nodo perimetral para acceder al clúster y para probar y hospedar las aplicaciones cliente. Para obtener más información, consulte [Uso de nodos perimetrales vacíos en HDInsight](hdinsight-apps-use-edge-node.md).

## <a name="advanced-settings-script-actions"></a>Configuración avanzada: acciones de script

Puede instalar componentes adicionales o personalizar la configuración del clúster mediante el uso de scripts durante la creación. Tales scripts se invocan mediante la opción de **Acción de script**, una opción de configuración que se puede usar a partir de los cmdlets de Windows PowerShell de HDInsight, en el Portal de Azure o el SDK de .NET para HDInsight. Para obtener más información, consulte [Personalización de un clúster de HDInsight mediante la acción de script](hdinsight-hadoop-customize-cluster-linux.md).

Algunos de los componentes nativos de Java, como Mahout y Cascading, se pueden ejecutar en el clúster como archivos Java Archive (JAR). Estos archivos JAR se pueden distribuir a Azure Storage y enviarse a clústeres de HDInsight con los mecanismos de envío de trabajos de Hadoop. Para obtener más información, consulte [Envío de trabajos de Hadoop mediante programación](hdinsight-submit-hadoop-jobs-programmatically.md).

> [!NOTE]
> Si tiene problemas con la implementación de archivos JAR en clústeres de HDInsight o con la llamada a archivos JAR en clústeres de HDInsight, póngase en contacto con el [soporte técnico de Microsoft](https://azure.microsoft.com/support/options/).
>
> Cascading no se admite en HDInsight, y no puede optar a recibir soporte técnico de Microsoft. Para ver las listas de los componentes compatibles, consulte [Novedades en las versiones de clústeres proporcionadas por HDInsight](hdinsight-component-versioning.md).
>
>

En ocasiones, querrá configurar los siguientes archivos de configuración durante el proceso de creación:

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
Si la solución requiere tecnologías repartidas entre varios tipos de clústeres de HDInsight, una [red virtual de Azure](https://docs.microsoft.com/azure/virtual-network) puede conectar los tipos de clústeres necesarios. Esta configuración permite que los clústeres, y cualquier otro código que se implemente en ellos, se comuniquen directamente entre sí.

Para más información sobre cómo usar una red virtual de Azure con HDInsight, consulte el artículo sobre cómo [Extensión de HDInsight con redes virtuales de Azure](hdinsight-extend-hadoop-virtual-network.md).

Para ver un ejemplo de cómo usar dos tipos de clúster en una red virtual de Azure, consulte [Análisis de datos de sensores con Storm y HBase](hdinsight-storm-sensor-data-analysis.md). Para más información sobre el uso de HDInsight con una red virtual, incluidos los requisitos de configuración específicos de la red virtual, consulte [Extensión de las funcionalidades de HDInsight con Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).

## <a name="troubleshoot-access-control-issues"></a>Solución de problemas de control de acceso

Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Pasos siguientes

- [¿Qué son HDInsight, el ecosistema Hadoop y los clústeres de Hadoop?](hdinsight-hadoop-introduction.md)
- [Introducción al uso de Hadoop en HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
- [Trabajo en Hadoop en HDInsight desde un equipo Windows](hdinsight-hadoop-windows-tools.md)
