---
title: aaaUse Phoenix Apache & ardilla con HBase - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Phoenix Apache en HDInsight y cómo tooinstall y configurar ardilla en el clúster de estación de trabajo tooconnect tooan HBase en HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a>Uso de Apache Phoenix con clústeres de HBase basados en Linux en HDInsight
Obtenga información acerca de cómo toouse [Apache Phoenix](http://phoenix.apache.org/) en HDInsight y cómo toouse SQLLine. Para obtener más información acerca de Phoenix, consulte [Phoenix en 15 minutos o menos](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Hola gramática de Phoenix, encontrará [gramática de Phoenix](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Para obtener información de versión de Phoenix en HDInsight de hello, consulte [cuáles son las novedades en las versiones de clúster de Hadoop Hola proporcionadas por HDInsight?](hdinsight-component-versioning.md).
>
>

## <a name="use-sqlline"></a>Uso de SQLLine
[SQLLine](http://sqlline.sourceforge.net/) es un tooexecute de utilidad de línea de comandos SQL.

### <a name="prerequisites"></a>Requisitos previos
Para poder usar SQLLine, debe tener el siguiente hello:

* **Un clúster de HBase en HDInsight**. Para obtener información sobre el aprovisionamiento del clúster de HBase, consulte [Introducción a HBase Apache en HDInsight][hdinsight-hbase-get-started].
* **Conectar el clúster de HBase toohello a través del protocolo de escritorio remoto de hello**. Para obtener instrucciones, consulte [Hadoop administrar clústeres de HDInsight mediante el uso de Hola portal de Azure][hdinsight-manage-portal].

Cuando se conecta el clúster de HBase tooan, deberá tooconnect tooone de hello Zookeepers. Cada clúster de HDInsight tiene tres Zookeepers.

**toofind el nombre de host de hello Zookeeper**

1. Abra Ambari examinando demasiado**https://<ClusterName>. azurehdinsight.net**.
2. Escriba hello toologin de nombre de usuario y contraseña HTTP (clúster).
3. Haga clic en **ZooKeeper** desde el menú de la izquierda Hola. Verá una lista con los tres **servidores de ZooKeeper**.
4. Haga clic en uno de hello **ZooKeeper Server** aparece. En el panel de resumen de hello, busque hello **Hostname**. Es similar demasiado*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.

**toouse SQLLine**

1. Conecte el clúster toohello mediante SSH. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. De SSH, ejecute hello después comandos toorun SQLLine:

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. Ejecute hello después comandos toocreate una tabla HBase e insertar algunos datos:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

Para más información, consulte el [manual de SQLLine](http://sqlline.sourceforge.net/#manual) y la [gramática de Phoenix](http://phoenix.apache.org/language/index.html).

## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido cómo toouse Phoenix Apache en HDInsight.  toolearn más información, vea:

* [Información general de HBase de HDInsight][hdinsight-hbase-overview]: HBase es una base de datos NoSQL de código abierto Apache basada en Hadoop que proporciona acceso aleatorio y una coherencia sólida para grandes cantidades de datos no estructurados y semiestructurados.
* [Aprovisionar clústeres de HBase en red Virtual de Azure][hdinsight-hbase-provision-vnet]: con la integración de red virtual, clústeres de HBase pueden ser implementado toohello mismo virtual de red así como las aplicaciones que las aplicaciones pueden comunicarse con HBase directamente.
* [Configurar la replicación de HBase en HDInsight](hdinsight-hbase-replication.md): Obtenga información acerca de cómo tooconfigure HBase replicación entre dos centros de datos de Azure.
* [Analizar la opinión de Twitter con HBase en HDInsight][hbase-twitter-sentiment]: Obtenga información acerca de cómo toodo en tiempo real [análisis de opiniones](http://en.wikipedia.org/wiki/Sentiment_analysis) de grandes cantidades de datos mediante el uso de HBase en un clúster de Hadoop en HDInsight.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
