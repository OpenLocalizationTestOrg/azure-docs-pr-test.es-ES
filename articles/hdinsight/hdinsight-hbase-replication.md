---
title: "replicación de clúster de HBase aaaConfigure dentro de redes virtuales - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure HBase replicación equilibrio de carga, alta disponibilidad, sin tiempos de inactividad migración o actualización de una tooanother de versión de HDInsight y recuperación ante desastres."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a>Configuración de la replicación de clúster de HBase en redes virtuales

Obtenga información acerca de cómo tooconfigure HBase replicación en una red virtual (VNet) o entre dos redes virtuales.

La replicación de clúster usa una metodología de inserción de origen. Un clúster de HBase puede ser un origen, un destino o cumplir ambos roles a la vez. La replicación es asincrónica y objetivo de Hola de replicación es coherencia definitiva. Cuando el origen de Hola recibe una familia de columna de tooa de edición con la replicación habilitada, editar es tooall propagado clústeres de destino. Cuando se replican datos desde un tooanother de clúster, clúster de origen de Hola y todos los clústeres que ya se han utilizado datos Hola son sometidos a seguimiento tooprevent replicación bucles.

En este tutorial, configurará una replicación de origen y de destino. Para otras topologías de clúster, consulte [Guía de referencia de HBase Apache](http://hbase.apache.org/book.html#_cluster_replication).

Casos de uso de replicación de HBase para una única red virtual:

* Equilibrio de carga, por ejemplo, ejecutando exámenes o trabajos MapReduce en clúster de destino de hello e introducción de datos en clúster de origen Hola
* Alta disponibilidad
* Migrar datos desde un tooanother de clúster de HBase
* Actualizar un clúster de HDInsight de Azure desde una tooanother de versión

Casos de uso de replicación de HBase para dos redes virtuales:

* Recuperación ante desastres
* Creación de particiones de aplicación hello y equilibrio de carga
* Alta disponibilidad

Puede replicar clústeres mediante scripts de [acción de script](hdinsight-hadoop-customize-cluster-linux.md) que se encuentran en [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener una suscripción a Azure. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="configure-hello-environments"></a>Configurar entornos de Hola

Hay tres opciones de configuración posibles:

- Dos clústeres de HBase en una única red virtual de Azure
- Dos clústeres de HBase en dos redes virtuales diferentes en Hola misma región
- Dos clústeres de HBase en dos redes virtuales diferentes de dos regiones distintas (replicación geográfica)

toomake lo más fácil de entornos de hello tooconfigure, hemos creado algunos [plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md). Si prefiere entornos de hello tooconfigure mediante otros métodos, consulte:

- [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
- [Create HBase clusters in Azure Virtual Network](hdinsight-hbase-provision-vnet.md) (Creación de clústeres de HBase en Azure Virtual Network)

### <a name="configure-one-virtual-network"></a>Configuración de una única red virtual

Haga clic en hello después imagen toocreate dos HBase clústeres Hola misma red virtual. Hola plantilla se almacena en [plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a>Configurar dos redes virtuales en hello misma región

Haga clic en hello después imagen toocreate dos redes virtuales con intercambio de tráfico de red virtual y dos clústeres de HBase en hello misma región. Hola plantilla se almacena en [plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



Este escenario requiere [emparejamiento de VNet](../virtual-network/virtual-network-peering-overview.md). plantilla de Hello permite el intercambio de tráfico de red virtual.   

Replicación de HBase utiliza direcciones IP de hello ZooKeeper las máquinas virtuales. Debe configurar las direcciones IP estáticas para los nodos de HBase ZooKeeper de destino de Hola.

**direcciones IP estáticas tooconfigure**

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Hola menú izquierdo, haga clic en **grupos de recursos**.
3. Haga clic en el grupo de recursos que contiene el clúster de HBase de destino de Hola. Se trata de un grupo de recursos de Hola que especificó cuando se usa el entorno hello toocreate plantillas de administrador de recursos de Hola. Puede usar Hola filtro toonarrow hacia abajo de la lista de Hola. Puede ver una lista de recursos que contiene las dos redes virtuales de Hola.
4. Haga clic en la red virtual de Hola que contiene el clúster de HBase de destino de Hola. Por ejemplo, haga clic en **xxxx-vnet2**. Puede ver tres dispositivos con nombres que empiezan por **nic-zookeepermode-**. Los dispositivos están las máquinas virtuales de hello tres ZooKeeper.
5. Haga clic en uno de hello ZooKeeper las máquinas virtuales.
6. Haga clic en **IP configurations** (Configuraciones IP).
7. Haga clic en **ipConfig1** de lista de Hola.
8. Haga clic en **estático**y anote la dirección IP real de Hola. Necesitará la dirección IP de hello cuando ejecuta la replicación de tooenable de acción de secuencia de comandos de Hola.

  ![Dirección IP estática ZooKeeper de replicación de HBase para HDInsight](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. Repita el paso 6 tooset Hola IP estática para hello otros dos nodos ZooKeeper.

Para el escenario de red virtual entre hello, debe usar hello **- ip** cambiar al llamar a hello **hdi_enable_replication.sh** acción de secuencia de comandos.

### <a name="configure-two-virtual-networks-in-two-different-regions"></a>Configuración de dos redes virtuales en dos regiones distintas

Haga clic en hello después imagen toocreate dos redes virtuales en dos regiones diferentes. plantilla de Hola se almacena en un contenedor de blobs de Azure público.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

Crear una puerta de enlace VPN entre las dos redes virtuales de Hola. Para obtener instrucciones, consulte [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) (Creación de una red virtual con una conexión de sitio a sitio).

Replicación de HBase utiliza direcciones IP de hello ZooKeeper las máquinas virtuales. Debe configurar las direcciones IP estáticas para los nodos de HBase ZooKeeper de destino de Hola. tooconfigure dirección IP estática, consulte la sección "configurar dos redes virtuales en Hola misma región" de hello en este artículo.

Para el escenario de red virtual entre hello, debe usar hello **- ip** cambiar al llamar a hello **hdi_enable_replication.sh** acción de secuencia de comandos.

## <a name="load-test-data"></a>Carga de datos de prueba

Cuando se replica un clúster, debe especificar Hola tablas tooreplicate. En esta sección, se cargará algunos datos en clúster de origen Hola. En la siguiente sección hello, permitirá que la replicación entre dos clústeres de Hola.

Siga las instrucciones de hello en [HBase tutorial: Introducción al uso de HBase de Apache con basado en Linux, Hadoop en HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate un **contactos** tabla e insertar algunos datos en la tabla Hola.

## <a name="enable-replication"></a>Habilitar replicación

Hola siguientes pasos muestra cómo toocall Hola acción de script de Hola portal de Azure. Para ejecutar una acción de secuencia de comandos mediante el uso de hello interfaz de línea de comandos (CLI) de Azure y Azure PowerShell, consulte [clústeres de HDInsight basados en Linux personalizar mediante la acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md).

**replicación de HBase tooenable de hello portal de Azure**

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Abra el clúster de HBase de origen de Hola.
3. En el menú de clúster de hello, haga clic en **acciones de Script**.
4. Haga clic en **Enviar nueva** de arriba Hola de hoja de Hola.
5. Seleccione o escriba Hola siguiente información:

  - **Nombre** especifique **Enable replication** (Habilitar replicación).
  - **URL de script de Bash**: escriba **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.
  - **Principal**: seleccionado. Desactive Hola otros tipos de nodos.
  - **Parámetros**: siguiente Hola parámetros Habilitar replicación para todas las tablas existentes de Hola de ejemplo y copiar todos los datos de Hola Hola origen clúster toohello destino clúster:

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. Haga clic en **Crear**. script de Hola puede tardar algún tiempo, especialmente cuando se usa el argumento - copydata de Hola.

Argumentos necesarios:

|Nombre|Descripción|
|----|-----------|
|-s, --src-cluster | Especifique el nombre DNS de hello del clúster de HBase de origen de Hola. Por ejemplo: -s hbsrccluster, --src-cluster=hbsrccluster |
|-d, --dst-cluster | Especifique el nombre DNS de hello del destino de hello (réplica) de clúster de HBase. Por ejemplo: -s dsthbcluster, --src-cluster=dsthbcluster |
|-sp, --src-ambari-password | Especifique la contraseña de administrador de Hola para Ambari en clúster de HBase de origen de Hola. |
|-dp, --dst-ambari-password | Especifique la contraseña de administrador de Hola para Ambari en clúster de HBase de destino de Hola.|

Argumentos opcionales:

|Nombre|Descripción|
|----|-----------|
|-su, --src-ambari-user | Especificar nombre de usuario de administrador de Hola para Ambari en clúster de HBase de origen de Hola. es el valor predeterminado de Hello **administración**. |
|-du, --dst-ambari-user | Especificar nombre de usuario de administrador de Hola para Ambari en clúster de HBase de destino de Hola. es el valor predeterminado de Hello **administración**. |
|-t, --table-list | Especifique hello toobe de tablas replicada. Por ejemplo: --table-list="table1;table2;table3". Si no se especifica unas tablas determinadas, se replican todas las tablas de HBase existentes.|
|-m, --machine | Especificar el nodo principal de Hola donde se ejecutará la acción de secuencia de comandos de Hola. valor de Hello es hn1 o hn0. Dado que hn0 suele estar más ocupado, se recomienda utilizar hn1. Utilice esta opción si estás ejecutando script de Hola $0 como una acción de secuencia de comandos desde el portal de HDInsight de Hola o Azure PowerShell.|
|-ip | Este argumento es necesario cuando se habilita la replicación entre dos redes virtuales. Este argumento actúa como un conmutador toouse Hola estático direcciones IP de ZooKeeper los nodos de clústeres de réplica en lugar de nombres FQDN. Hola toobe de direcciones IP estática necesidad preconfigurado antes de habilitar la replicación. |
|-cp, -copydata | Habilite la migración de Hola de los datos existentes en las tablas de Hola donde está habilitada la replicación. |
|-rpm, -replicate-phoenix-meta | Habilita la replicación en las tablas del sistema Phoenix. <br><br>*Esta opción se debe utilizar con precaución.* Se recomienda volver a crear tablas de Phoenix en clústeres de réplica antes de utilizar este script. |
|-h, --help | Muestra información de uso. |

Hola print_usage() sección de hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) proporciona una explicación detallada de parámetros.

Después de acción de secuencia de comandos de hello correctamente implementado, puede usar clúster de HBase SSH tooconnect toohello destino y comprobar datos Hola se han replicado.

### <a name="replication-scenarios"></a>Escenarios de replicación

Hello lista siguiente muestra algunos casos de uso general y sus valores de parámetro:

- **Habilitar la replicación en todas las tablas entre clústeres de hello dos**. Este escenario no requiere Hola copia/migración de datos existentes en las tablas de hello y no utiliza tablas de Phoenix. Usar hello parámetros siguientes:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- **Habilitar la replicación en tablas específicas**. Usar hello después de la replicación de tooenable parámetros en table1, table2 y table3:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- **Habilitar la replicación en tablas específicas y copie los datos existentes de hello**. Usar hello después de la replicación de tooenable parámetros en table1, table2 y table3:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- **Habilitar la replicación en todas las tablas con replicar phoenix metadatos de origen toodestination**. La replicación de metadatos de Phoenix no es perfecta, así que debe habilitarse con precaución.

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a>Copia y migración de datos

Hay dos scripts de acción de script independientes para copiar o migrar datos después de habilitar la replicación:

- [Secuencia de comandos para tablas pequeñas](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (unos pocos gigabytes de tamaño y general copia es toofinish esperado en menos de una hora)

- [Secuencia de comandos para tablas grandes](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (se esperaba tootake más de una hora toocopy)

Puede seguir Hola mismo procedimiento en [habilitar la replicación](#enable-replication) toocall Hola Generar script de acción con hello parámetros siguientes:

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

Hola print_usage() sección de hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) ofrece una descripción detallada de los parámetros.

### <a name="scenarios"></a>Escenarios

- **Copiar tablas específicas (test1, test2 y test3) para todas las filas editadas hasta ahora (marca de tiempo actual)**:

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  o

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- **Copiar tablas específicas con el intervalo de tiempo especificado**:

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a>Deshabilitar replicación

replicación de toodisable, usa otro script de acción de secuencia de comandos situada [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh). Puede seguir Hola mismo procedimiento en [habilitar la replicación](#enable-replication) toocall Hola Generar script de acción con hello parámetros siguientes:

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

Hola print_usage() sección de hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) proporciona una explicación detallada de parámetros.

### <a name="scenarios"></a>Escenarios

- **Deshabilitar la replicación en todas las tablas**:

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  o

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- **Deshabilitar la replicación en las tablas especificadas (table1, table2 y table3)**:

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, se habrá aprendido cómo tooconfigure HBase replicación entre dos centros de datos. toolearn más información acerca de HDInsight y HBase, consulte:

* [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started] (Introducción a HBase Apache en HDInsight)
* [HDInsight HBase overview][hdinsight-hbase-overview] (Información general de HBase de HDInsight)
* [Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet] (Creación de clústeres de HBase en Azure Virtual Network)
* [Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment] (Análisis de opinión en Twitter en tiempo real con HBase)
* [Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data] [Análisis de los datos de sensor con Storm y HBase en HDInsight (Hadoop)]

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
