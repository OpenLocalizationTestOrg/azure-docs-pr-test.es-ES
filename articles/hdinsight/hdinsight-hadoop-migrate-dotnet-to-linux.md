---
title: aaaUse .NET con Hadoop MapReduce en HDInsight basados en Linux - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo las aplicaciones de .NET toouse de transmisión por secuencias MapReduce en HDInsight basados en Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a>Migrar soluciones de .NET para HDInsight basados en Windows-based tooLinux HDInsight

Uso de clústeres de HDInsight basados en Linux [Mono (https://mono-project.com)](https://mono-project.com) toorun aplicaciones. NET. Mono permite toouse componentes de .NET como las aplicaciones de MapReduce con HDInsight basados en Linux. En este documento, obtenga información acerca de cómo se crean soluciones de .NET toomigrate para toowork de clústeres de HDInsight basados en Windows con Mono en HDInsight basados en Linux.

## <a name="mono-compatibility-with-net"></a>Compatibilidad de Mono con .NET

La versión 4.2.1 de Mono está incluida en la versión 3.5 de HDInsight. Para obtener más información sobre la versión de Hola de Mono incluido con HDInsight, vea [versiones de componentes de HDInsight](hdinsight-component-versioning.md). tooinstall una versión específica de Mono, vea hello [instalación o una actualización Mono](hdinsight-hadoop-install-mono.md) documento.

Para obtener información detallada sobre la compatibilidad entre Mono y. NET, vea hello [compatibilidad Mono (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) documento.

> [!IMPORTANT]
> el marco de trabajo de Hello SCP.NET es compatible con Mono. Para obtener más información sobre el uso de SCP.NET con Mono, consulte [topologías de toodevelop C# utilice Visual Studio para Apache Storm en HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="automated-portability-analysis"></a>Análisis de portabilidad automatizado

Hola [analizador de portabilidad de .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) puede ser usado toogenerate un informe de las incompatibilidades entre la aplicación y Mono. Usar hello siguiendo los pasos tooconfigure Hola analizador toocheck la aplicación para la portabilidad Mono:

1. Instalar hello [analizador de portabilidad de .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer). Durante la instalación, seleccione la versión de Hola de toouse de Visual Studio.

2. En Visual Studio 2015, seleccione __analizar__ > __configuración de analizador de portabilidad__y asegúrese de que __4.5__ está activada en hello __Mono__  sección.

    ![4.5 activadas en la sección Mono para la configuración del analizador de Hola](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    Seleccione __Aceptar__ configuración de toosave Hola.

3. Seleccione __Analyze__ > __Analyze Assembly Portability__ (Analizar > Analizar portabilidad de ensamblado). Seleccionar ensamblado de Hola que contiene la solución y, a continuación, seleccione __abiertos__ toobegin analysis.

4. Una vez completado el análisis, seleccione __Analyze__ > __View analysis reports__ (Analizar > Ver informes de análisis). En __resultados del análisis de portabilidad__, seleccione __abrir informe__ tooopen un informe.

    ![Cuadro de diálogo de resultados del analizador de portabilidad](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> Analizador de Hello no puede detectar todos los problemas con la solución. Por ejemplo, una ruta de archivo de `c:\temp\file.txt` se considera correcto porque Mono se ejecuta en Windows y la ruta de acceso de hello es válido en ese contexto. Sin embargo, la ruta de acceso de hello no es válido en una plataforma de Linux.

## <a name="manual-portability-analysis"></a>Análisis de portabilidad manual

Realizar una auditoría manual del código utilizando información de Hola Hola [portabilidad de aplicación (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) documento.

## <a name="modify-and-build"></a>Modificación y compilación

Puede continuar toouse Visual Studio toobuild sus soluciones de .NET para HDInsight. Sin embargo, debe asegurarse de que ese proyecto Hola está configurado toouse .NET Framework 4.5.

## <a name="deploy-and-test"></a>Implementación y prueba

Una vez que haya modificado la solución con las recomendaciones de Hola de hello analizador de portabilidad de .NET o de un análisis manual, debe probarla con HDInsight. Probar la solución de hello en un clúster de HDInsight basados en Linux puede revelar problemas sutiles que requieren toobe que se ha corregido. Se recomienda que habilite el registro adicional en la aplicación durante la prueba.

Para obtener más información sobre cómo acceder a los registros, vea Hola siguientes documentos:

* [Acceso a registros de aplicación de YARN en HDInsight basado en Linux](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a>Pasos siguientes

* [Uso de MapReduce en C# en HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [Uso de funciones definidas por el usuario de C# con Hive y Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [Desarrollo de topologías de C# para Storm en HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md)