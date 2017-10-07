---
title: "creación - Azure de clústeres de bibliotecas de Hive aaaAdd durante HDInsight | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd Hive bibliotecas (archivos jar), tooan HDInsight clúster durante la creación del clúster."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a>Incorporación de bibliotecas personalizadas de Hive al crear el clúster de HDInsight

Si dispone de las bibliotecas que utilizan con frecuencia con Hive en HDInsight, este documento contiene información sobre el uso de una biblioteca de acción de secuencia de comandos toopre carga Hola durante la creación del clúster. Las bibliotecas que se agregan mediante los pasos de hello en este documento están disponibles globalmente en el subárbol: no hay ninguna necesidad de toouse [agregar JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload ellos.

## <a name="how-it-works"></a>Cómo funciona

Al crear un clúster, también puede especificar una acción de secuencia de comandos que se ejecuta una secuencia de comandos en nodos de clúster de hello mientras se crea. script de Hola en este documento acepta un único parámetro, que es una ubicación de WASB que contenga Hola bibliotecas (almacenadas como archivos jar) toobe previamente cargado.

Durante la creación del clúster, script de Hola enumera los archivos de hello, copiarlos en toohello `/usr/lib/customhivelibs/` directorio en los nodos principal y de trabajo, a continuación, agrega toohello `hive.aux.jars.path` propiedad Hola `core-site.xml` archivo. En los clústeres basados en Linux, también actualiza hello `hive-env.sh` archivo con la ubicación Hola archivos Hola.

> [!NOTE]
> Con las acciones de script de Hola en este artículo incluye bibliotecas de hello en hello los escenarios siguientes:
>
> * **HDInsight basados en Linux** : al usar Hola un cliente de Hive, **WebHCat**, y **HiveServer2**.
> * **HDInsight basados en Windows** : cuando se usa el cliente de Hive de Hola y **WebHCat**.

## <a name="hello-script"></a>script de Hola

**Ubicación del script**

En los **clústeres basados en Linux**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)

En los **clústeres basados en Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

**Requisitos**

* scripts de Hello deben ser aplicado tooboth Hola **Head nodos** y **nodos de trabajador**.

* Hola JAR desea tooinstall deben estar almacenados en almacenamiento de blobs de Azure en un **único contenedor**.

* cuenta de almacenamiento de Hola que contiene la biblioteca de Hola de archivos jar **debe** ser toohello vinculado HDInsight clúster durante la creación. Debe ser cuenta de almacenamiento predeterminada de Hola o agrega una cuenta a través de __configuración opcional__.

* contenedor de toohello de ruta de acceso de Hello WASB debe especificarse como una acción de secuencia de comandos de toohello de parámetro. Por ejemplo, si hello archivos JAR se almacena en un contenedor denominado **bibliotecas** en una cuenta de almacenamiento denominada **mystorage**, sería el parámetro hello  **wasb://libs@mystorage.blob.core.windows.net/** .

  > [!NOTE]
  > Este documento se supone que ya ha crear una cuenta de almacenamiento, contenedor de blobs y tooit de archivos cargados Hola.
  >
  > Si no ha creado una cuenta de almacenamiento, puede hacerlo a través de hello [portal de Azure](https://portal.azure.com). A continuación, puede usar una utilidad como [Azure Storage Explorer](http://storageexplorer.com/) toocreate un contenedor en la cuenta de hello y carga archivos tooit.

## <a name="create-a-cluster-using-hello-script"></a>Crear un clúster mediante el script de Hola

> [!NOTE]
> Hola pasos crea un clúster de HDInsight basados en Linux. Seleccione un clúster basado en Windows, toocreate **Windows** como Hola clúster SO al crear el clúster de Hola y utilizar secuencias de comandos de Windows (PowerShell) de hello en lugar de la secuencia de comandos de hello intensiva de errores.
>
> También puede usar PowerShell de Azure o hello HDInsight .NET SDK toocreate un clúster mediante esta secuencia de comandos. Para obtener más información sobre el uso de estos métodos, consulte [Personalización de clústeres de HDInsight mediante acciones de script](hdinsight-hadoop-customize-cluster-linux.md).

1. Iniciar el aprovisionamiento de un clúster mediante el uso de pasos de hello en [clústeres de HDInsight de aprovisionar en Linux](hdinsight-hadoop-provision-linux-clusters.md), pero no complete el aprovisionamiento.

2. En hello **configuración opcional** hoja, seleccione **acciones de Script**y proporcionar Hola siguiente información:

   * **NOMBRE**: escriba un nombre descriptivo para la acción de secuencia de comandos de Hola.

   * **URI DEL SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh

   * **PRINCIPAL**: active esta opción.

   * **TRABAJADOR**: active esta opción.

   * **ZOOKEEPER**: déjelo en blanco.

   * **PARÁMETROS**: escriba hello WASB toohello contenedor y el almacenamiento cuenta de dirección que contiene archivos JAR Hola. Por ejemplo, **wasb://libs@mystorage.blob.core.windows.net/**.

3. Final de Hola de hello **acciones de Script**, usar hello **seleccione** configuración del botón toosave Hola.

4. En hello **configuración opcional** hoja, seleccione **cuentas de almacenamiento vinculadas** y seleccione hello **agregar una clave de almacenamiento** vínculo. Seleccionar cuenta de almacenamiento de Hola que contiene archivos JAR hello y, a continuación, usar hello **seleccione** devuelto hello y configuración de botones toosave **configuración opcional** hoja.

5. Hola de uso **seleccione** situado en la parte inferior de Hola de hello **configuración opcional** información de configuración opcional de hoja toosave Hola.

6. Continuar aprovisionamiento clúster Hola tal y como se describe en [clústeres de HDInsight de aprovisionar en Linux](hdinsight-hadoop-provision-linux-clusters.md).

Una vez finalizada la creación del clúster, es capaz de toouse archivos JAR Hola agregada a través de este script de Hive sin necesidad de hello toouse `ADD JAR` instrucción.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca del trabajo con Hive, consulte [Use Hive with HDInsight](hdinsight-use-hive.md)
