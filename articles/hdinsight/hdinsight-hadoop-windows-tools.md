---
title: aaaUse un PC Windows con Hadoop en HDInsight - Azure | Documentos de Microsoft
description: "Trabaje desde un equipo Windows en Hadoop en HDInsight. Administre y consulte clústeres con PowerShell, Visual Studio y herramientas de Linux. Desarrolle soluciones de macrodatos con .NET."
services: hdinsight
keywords: hadoop en windows,hadoop para windows
author: cjgronlund
manager: jhubbard
ms.author: cgronlun
ms.date: 05/17/2017
ms.topic: article
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 7c93f16e93349c0b8fb1abd55320c2c172b93aa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="work-in-hello-hadoop-ecosystem-on-hdinsight-from-a-windows-pc"></a>Trabajar en hello ecosistema de Hadoop en HDInsight de un equipo con Windows

Obtenga información acerca del desarrollo y opciones de administración de PC de Windows hello para trabajar en el ecosistema de hello Hadoop en HDInsight. 

HDInsight se basa en Apache Hadoop y componentes de Hadoop, tecnologías de código abierto desarrolladas en Linux. HDInsight versión 3.4 y versiones posterior utiliza Hola distribución Ubuntu Linux como Hola subyacente OS para clúster Hola. Sin embargo, puede trabajar con HDInsight desde un cliente Windows o un entorno de desarrollo de Windows.

## <a name="use-powershell-for-deployment-and-management-tasks"></a>Uso de PowerShell para tareas de implementación y administración
Azure PowerShell es un entorno de scripting que puede usar toocontrol y automatizar las tareas de implementación y administración en HDInsight de Windows.

Ejemplos de tareas que puede realizar con PowerShell:

* [Creación de clústeres con PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [Ejecución de consultas de Hive con PowerShell](hdinsight-hadoop-use-hive-powershell.md)
* [Administración de clústeres con PowerShell](hdinsight-administer-use-powershell.md)

Siga los pasos demasiado[instalar y configurar Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) versión más reciente de tooget Hola. Si tiene secuencias de comandos que necesitan toobe modificar toouse Hola nuevos cmdlets para el Administrador de recursos de Azure, consulte [migrar tooAzure herramientas de desarrollo basado en el Administrador de recursos para clústeres de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="utilities-you-can-run-in-a-browser"></a>Utilidades que puede ejecutar en un explorador
Hello utilidades siguientes tienen una interfaz de usuario que se ejecuta en un explorador web:
* **[Shell de nube de Azure (vista previa)](https://docs.microsoft.com/azure/cloud-shell/quickstart)**  es un shell interactivo, línea de comandos que se ejecuta en el explorador y desde Hola portal de Azure.
* **[Interfaz de usuario de Ambari Web](hdinsight-hadoop-manage-ambari.md)**  es una administración y supervisión de la utilidad está disponible en hello portal de Azure que puede ser utilizados toomanage diferentes tipos de trabajos, como:
    * [Usar Ambari con hello API de REST](hdinsight-hadoop-manage-ambari-rest-api.md)
    * [Vista de Hive en Ambari](hdinsight-hadoop-use-hive-ambari-view.md)
    * [Vista de Tez en Ambari](hdinsight-debug-ambari-tez-view.md)

## <a name="data-lake-hadoop-tools-for-visual-studio"></a>Herramientas de Data Lake (Hadoop) para Visual Studio
Utilice Data Lake Tools para Visual Studio toodeploy y administrar topologías de Storm. Herramientas de datos Lake también instala hello SCP.NET SDK, que permite las topologías de C# aluvión de toodevelop con Visual Studio.

Antes de ir toohello, en los ejemplos siguientes [instalar y probar Data Lake Tools para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md). 

Ejemplos de tareas que puede hacer con Visual Studio y Herramientas de Data Lake para Visual Studio:
* [Implementación y administración de topologías de Storm desde Visual Studio](hdinsight-storm-deploy-monitor-topology-linux.md)
* [Desarrollo de las topologías de C# para Storm con Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md) bits de Hello incluyen plantillas de ejemplo para las topologías de Storm puede conectarse toodatabases, como la base de datos de Azure Cosmos y base de datos SQL.

## <a name="visual-studio-and-hello-net-sdk"></a>Visual Studio y .NET SDK Hola 

Puede usar Visual Studio con clústeres de toomanage SDK de .NET de Hola y desarrollar aplicaciones de grandes cantidades de datos. Puede usar otros IDE para hello siguiente las tareas, pero se muestran ejemplos de Visual Studio.

Ejemplos de tareas que puede realizar con hello SDK de .NET en Visual Studio:
* [Creación de clústeres y trabajo en HDInsight desde una aplicación de .NET Framework](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* [Ejecutar consultas de Hive con hello SDK para .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [Uso de funciones definidas por el usuario de C# con el streaming de Hive y Pig en Hadoop](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

> Sugerencia Si ejecutas soluciones .NET con clústeres de HDInsight basados en Windows, es un tooplan buen momento una migración de clústeres basados en tooLinux. Para obtener más información, consulte [solución .NET migrar de HDInsight basados en Windows-based tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="intellij-idea-and-eclipse-ide-for-spark-clusters"></a>Intellij IDEA y Eclipse IDE para clústeres de Spark
Ambos [Intellij IDEA](https://www.jetbrains.com/idea/download) hello y [Eclipse IDE](https://www.eclipse.org/downloads/) se puede usar para:
* Desarrollar y enviar una aplicación Spark en Scala en un clúster de Spark en HDInsight.
* Acceder a recursos de clúster de Spark.
* Desarrollar y ejecutar localmente una aplicación Spark en Scala.

En estos artículos se muestra cómo hacerlo: 
* Intellij IDEA: [aplicaciones de Spark crear mediante Azure Toolkit for Intellij complemento Hola y Hola Scala SDK.](hdinsight-apache-spark-intellij-tool-plugin.md)
* Eclipse IDE o Scala IDE para Eclipse: [hello Azure Toolkit for Eclipse y aplicaciones crear Spark](hdinsight-apache-spark-eclipse-tool-plugin.md) 


## <a name="notebooks-on-spark-for-data-scientists"></a>Notebooks en Spark para científicos de datos 
Los clústeres de Apache Spark en HDInsight incluyen notebooks y kernels de Zeppelin que se pueden usar con notebooks de Jupyter. 

* [Obtenga información acerca de cómo los kernels de toouse en Spark clústeres con aplicaciones de Jupyter blocs de notas tootest Spark](hdinsight-apache-spark-zeppelin-notebook.md)
* [Obtenga información acerca de cómo los blocs de notas de toouse Zeppeling en Spark clústeres trabajos de Spark toorun](hdinsight-apache-spark-jupyter-notebook-kernels.md) 


## <a name="run-linux-based-tools-and-technologies-on-windows"></a>Ejecución en Windows de tecnologías y herramientas basadas en Linux

Si se produce una situación donde debe usar una herramienta o la tecnología que solo está disponible en Linux, considere la posibilidad de hello siguientes opciones:

* **Bash (beta) en Windows 10** proporciona un subsistema de Linux en Windows. Intensiva de errores permite toodirectly ejecute Linux utilidades sin necesidad de toomaintain una instalación de Linux dedicada. [Instalar y ejecutar la versión beta de Bash hello en Windows 10](https://msdn.microsoft.com/commandline/wsl/install_guide)
* **Docker para Windows** proporciona acceso toomany basado en Linux, herramientas y se puede ejecutar directamente desde Windows. Por ejemplo, puede usar el cliente Beeline hello toorun para Hive directamente desde Windows. Puede usar Docker toorun Jupyter notebook local y conectarse de forma remota tooSpark en HDInsight. [Introducción a Docker para Windows](https://docs.docker.com/docker-for-windows/)
* **[MobaXTerm](http://mobaxterm.mobatek.net/)**  permite el sistema de archivos del clúster de toographically examinar Hola a través de una conexión SSH.

## <a name="next-steps"></a>Pasos siguientes
Si está tooworking nueva en clústeres basados en Linux, vea Hola siga artículos:
* [Configuración de Hadoop, Kafka, Spark u otros clústeres](hdinsight-hadoop-provision-linux-clusters.md)
* [Sugerencias para clústeres de HDInsight en Linux](hdinsight-hadoop-linux-information.md)