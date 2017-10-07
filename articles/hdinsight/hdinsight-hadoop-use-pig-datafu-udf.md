---
title: aaaUse DataFu con Pig en HDInsight - Azure | Documentos de Microsoft
description: "DataFu es un conjunto de bibliotecas para su uso con Hadoop. Aprenda cómo usar DataFu con Pig en su clúster de HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 0016721a-82be-4773-88ad-91e6b2c21cbb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 357ad8f9694cc590115289877e752bdd242bdadc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-datafu-with-pig-on-hdinsight"></a>Uso de DataFu con Pig en HDInsight

Obtenga información acerca de cómo toouse DataFu con HDInsight. DataFu es un conjunto de bibliotecas de código abierto que se usan con Pig en Hadoop.

## <a name="prerequisites"></a>Requisitos previos

* Una suscripción de Azure.

* Clúster de HDInsight de Azure (basado en Linux o Windows)

  > [!IMPORTANT]
  > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Cierta familiaridad básica con el [uso de Pig en HDInsight](hdinsight-use-pig.md)

## <a name="install-datafu-on-linux-based-hdinsight"></a>Instalación de DataFu en HDInsight basado en Linux

> [!IMPORTANT]
> DataFu se instala en clústeres basados en Linux 3.3 y versiones posteriores, así como en clústeres basados en Windows. No se instala en clústeres basados en Linux anteriores a la versión 3.3.
>
> Si usa un clúster basado en Windows o un clúster basado en Linux con una versión superior a la versión 3.3, omita esta sección.

DataFu puede descargarse e instalarse desde el repositorio de Maven Hola. Usar hello después de clúster de HDInsight de pasos tooadd DataFu tooyour:

1. Conecte el clúster de HDInsight basados en Linux de tooyour mediante SSH. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Usar hello siguiente comando toodownload hello DataFu jar archivo mediante la utilidad de wget hello, o copie y pegue Hola vínculo en la descarga de hello toobegin de explorador.

    ```
    wget http://central.maven.org/maven2/com/linkedin/datafu/datafu/1.2.0/datafu-1.2.0.jar
    ```

3. A continuación, cargue toodefault almacenamiento de archivos de hello para el clúster de HDInsight. Colocar el archivo hello en default almacenamiento lo convierte en disponible tooall nodos en clúster Hola.

    ```
    hdfs dfs -put datafu-1.2.0.jar /example/jars
    ```

    > [!NOTE]
    > comando anterior Hola almacena jar de hello en `/example/jars` porque este directorio ya existe en el almacenamiento de clúster de Hola. Puede usar la ubicación que desee en el almacenamiento del clúster de HDInsight.

## <a name="use-datafu-with-pig"></a>Uso de DataFu con Pig

pasos de Hello en esta sección se supone que está familiarizado con el uso de Pig en HDInsight. Para obtener más información acerca del uso de Pig con HDInsight, consulte [Uso de Pig con HDInsight](hdinsight-use-pig.md).

> [!IMPORTANT]
> Si instaló manualmente DataFu siguiendo los pasos de hello en la sección anterior de hello, debe registrar antes de usarlo.
>
> * Si el clúster usa Azure Storage, utilice una ruta `wasb://`. Por ejemplo: `register wasb:///example/jars/datafu-1.2.0.jar`.
>
> * Si el clúster usa Azure Data Lake Store, utilice una ruta `adl://`. Por ejemplo: `register adl://home/example/jars/datafu-1.2.0.jar`.

Normalmente, definirá un alias para las funciones de DataFu.Normalmente, definirá un alias para las funciones de DataFu. Hello en el ejemplo siguiente se define un alias de `SHA`:

```piglatin
DEFINE SHA datafu.pig.hash.SHA();
```

A continuación, puede usar este alias en un toogenerate de script de Pig latino un hash de los datos de entrada de Hola. Por ejemplo, hello código siguiente reemplaza ubicación hello en los datos de entrada de hello con un valor de hash:

```piglatin
raw = LOAD '/HdiSamples/HdiSamples/SensorSampleData/building/building.csv' USING
    org.apache.pig.piggybank.storage.CSVExcelStorage(',', 'NO_MULTILINE', 'UNIX', 'SKIP_INPUT_HEADER') AS
    (int1:int,
     id1:chararray,
     int2:int,
     id2:chararray,
     location:chararray);
mask = FOREACH raw GENERATE int1, id1, int2, id2, SHA(location);
DUMP mask;
```

Genera Hola después de salida:

    (1,M1,25,AC1000,aa5ab35a9174c2062b7f7697b33fafe5ce404cf5fecf6bfbbf0dc96ba0d90046)
    (2,M2,27,FN39TG,7a1ca4ef7515f7276bae7230545829c27810c9d9e98ab2c06066bee6270d5153)
    (3,M3,28,JDNS77,07f62b021771d3cf67e2e1faf18769cc5e5c119ad7d4d1847a11e11d6d5a7ecb)
    (4,M4,17,GG1919,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (5,M5,3,ACMAX22,1ed8c7e56c947bebc0cfcf88c4ea0f02c944568f71df893a99970e4f0c78cddc)
    (6,M6,9,AC1000,c96dd81db196cca5f57bd4270bbb9d9e9d1b242d67f9364005ee1dfdc2632523)
    (7,M7,13,FN39TG,3e049d78d958038ac6bd5dcf038075cc73362b4956aaf7308c3a69c8eca76297)
    (8,M8,25,JDNS77,c1ef40ce0484c698eb4bd27fe56c1e7b68d74f9780ed674210d0e5013dae45e9)
    (9,M9,11,GG1919,a7d355b26bda6bf1196ccffead0b2cf2b81f0a9de5b4876b44407f1dc07e51e6)
    (10,M10,23,ACMAX22,10436829032f361a3de50048de41755140e581467bc1895e6c1a17f423e42d10)
    (11,M11,14,AC1000,348841ef53dbd5a64008a86be432973db790774fb28b59b0d99702a3188b3705)
    (12,M12,26,FN39TG,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (13,M13,25,JDNS77,ed9ad13611d7164839dd3feaf9a7f6a75a4138f389e0d45f8e07fa38da1116a2)
    (14,M14,17,GG1919,80db4ccdca106d37b920206331fcfe3e9e50a9e763d89b54ce3ad5ac8cf30f03)
    (15,M15,19,ACMAX22,3552ac0c032467fbf592cb4d10c5c9267800c01e343ad8ca557256d882ae9327)
    (16,M16,23,AC1000,07c67d76ef92ac9853588e098983fefba4ba5965f8fec95f42ab0d04c27865ba)
    (17,M17,11,FN39TG,557c1599d9a04895d3817d293e0806a4419a14de31958386182798d0d2ed3a56)
    (18,M18,25,JDNS77,dbc74a36d8e7439c45c64d856388506cc9b1218619cef979c3d605115a7a4546)
    (19,M19,14,GG1919,be55ef3f4c4e6c2d9c2afe2a33ac90ad0f50d4de7f9163999877e2a9ca5a54f8)
    (20,M20,19,ACMAX22,ea0b937ea317101ee2c26b03a4843a19ceced8a2b9673c3cf409a726ca2b0fd8)

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre DataFu o Pig, consulte Hola siguientes documentos:

* [Guía de Pig de Apache DataFu](http://datafu.incubator.apache.org/docs/datafu/guide.html).
* [Uso de Pig con HDInsight](hdinsight-use-pig.md)
