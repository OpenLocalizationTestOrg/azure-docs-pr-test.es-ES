---
title: aaaInstall o actualizar Mono en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse una versión específica de Mono con clúster de HDInsight. Mono es toorun usa .NET applications en clústeres de HDInsight basados en Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.openlocfilehash: 1e8a8aaeff231c93a9e232379448517b326da965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a>Instalación o actualización de Mono en HDInsight

Obtenga información acerca de cómo tooinstall una versión específica de [Mono](https://www.mono-project.com) en HDInsight 3.4 o superior.

Mono se instala en HDInsight 3.4 y versiones posteriores y es toorun usa .NET applications. Para obtener información sobre la versión de Hola de Mono que se incluyen con cada versión de HDInsight, vea [versiones de componentes de HDInsight](hdinsight-component-versioning.md). tooinstall una versión diferente en el clúster, la acción de secuencia de comandos de uso hello en este documento. 

## <a name="how-it-works"></a>Cómo funciona

Esta secuencia de comandos acepta Hola después de parámetro:

* __Número de versión mono__: versión de Hola de tooinstall Mono. versión de Hola debe estar disponible desde [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).

script de Hola instala Hola siguientes Mono paquetes:

* __mono-complete__

* __ca-certificates-mono__

## <a name="hello-script"></a>script de Hola

__Ubicación de script__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)

__Requisitos__:

* se debe aplicar el script de Hola en hello __head nodos__ y __nodos de trabajador__.

## <a name="toouse-hello-script"></a>script de Hola toouse

Para obtener información sobre cómo toouse esta secuencia de comandos con HDInsight, vea hello [mediante la acción de secuencia de comandos de clústeres de HDInsight basados en Linux personalizar](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) documento. Puede usar el script de Hola Hola portal de Azure, Azure PowerShell, u Hola CLI de Azure.

Mientras siguiente hello documento de la acción de secuencia de comandos, utilice Hola siguiente URI:

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> Al configurar HDInsight con este script, marque el script de Hola como __Persisted__. Esta configuración permite HDInsight tooapply nodos de hello script tooworker agregados a través de las operaciones de ajuste de escala.


## <a name="next-steps"></a>Pasos siguientes

Ha aprendido cómo tooupgrade o instale una versión específica de Mono en HDInsight. Para obtener más información sobre el uso de aplicaciones .NET con Mono en HDInsight, vea Hola siguientes documentos:

* [Uso de .NET con el streaming de MapReduce en Hadoop en HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [Uso de .NET con Hive y Pig en HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [Desarrollo de topologías de C# para Apache Storm en HDInsight con herramientas de Hadoop para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Migrar soluciones de .NET basada en tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)

Para más información sobre el uso de las acciones de script, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md).