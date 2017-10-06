---
title: cuentas de almacenamiento de Azure adicional aaaAdd tooHDInsight | Documentos de Microsoft
description: "Obtenga información acerca de cómo las cuentas de almacenamiento de Azure adicionales de tooadd tooan clúster de HDInsight existente."
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
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a>Agregar tooHDInsight de cuentas de almacenamiento adicional

Obtenga información acerca de cómo las cuentas de tooHDInsight toouse script acciones tooadd adicionales almacenamiento de Azure. Hello pasos de este documento agregan un clúster de HDInsight basados en Linux existente de almacenamiento cuenta tooan.

> [!IMPORTANT]
> información de Hello en este documento es sobre la adición de clúster de almacenamiento adicional tooa después de que se ha creado. Para más información sobre cómo agregar cuentas de almacenamiento durante la creación del clúster, consulte [Configuración de clústeres de HDInsight con Hadoop, Spark, Kafka y mucho más](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="how-it-works"></a>Cómo funciona

Este script toma Hola parámetros siguientes:

* __Nombre de la cuenta de almacenamiento de Azure__: nombre de Hola Hola almacenamiento cuenta tooadd toohello del clúster de HDInsight. Después de ejecutar el script de Hola, HDInsight puede leer y escribir datos almacenados en esta cuenta de almacenamiento.

* __Clave de cuenta de almacenamiento de Azure__: una clave que conceda acceso a cuenta de almacenamiento de toohello.

* __-p__ (opcional): si se especifica, clave hello no se cifra y se almacena en el archivo de core-site.xml de hello como texto sin formato.

Durante el procesamiento, el script de Hola realiza Hola siguientes acciones:

* Si hello cuenta de almacenamiento ya existe en la configuración de core-site.xml hello para el clúster de hello, Hola script se cerrará y no se llevan a cabo ninguna acción adicional.

* Comprueba que la cuenta de almacenamiento de hello existe y puede tener acceso mediante la clave de Hola.

* Cifra la clave de hello mediante credenciales de clúster de Hola.

* Agrega el archivo core-site.xml toohello de hello almacenamiento cuenta.

* Detiene y reinicia los servicios de Oozie, YARN, MapReduce2 y HDFS Hola. Detener e iniciar estos servicios les permite nueva cuenta de almacenamiento de toouse Hola.

> [!WARNING]
> No se admite el uso de una cuenta de almacenamiento en una ubicación diferente que el clúster de HDInsight de Hola.

## <a name="hello-script"></a>script de Hola

__Ubicación del script__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)

__Requisitos__:

* se debe aplicar el script de Hola en hello __Head nodos__.

## <a name="toouse-hello-script"></a>script de Hola toouse

Este script puede utilizarse desde Hola portal de Azure, Azure PowerShell, u Hola 1.0 de CLI de Azure. Para obtener más información, vea hello [mediante la acción de secuencia de comandos de clústeres de HDInsight basados en Linux personalizar](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) documento.

> [!IMPORTANT]
> Al usar pasos de hello indicados en documento de personalización de hello, use Hola después información tooapply esta secuencia de comandos:
>
> * Reemplace cualquier URI de acción de secuencia de comandos de ejemplo con hello URI para esta secuencia de comandos (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).
> * Reemplace los parámetros de ejemplo por nombre de cuenta de almacenamiento de Azure de Hola y la clave de clúster agregado toohello toobe cuenta de almacenamiento de Hola. Si utiliza hello portal de Azure, estos parámetros deben estar separados por un espacio.
> * No es necesario toomark esta secuencia de comandos como __Persisted__, tal y como actualiza directamente configuración de Ambari de hello para el clúster de Hola.

## <a name="known-issues"></a>Problemas conocidos

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a>Cuentas de almacenamiento que no se muestran en Azure Portal o las herramientas

Cuando visualización hello HDInsight clúster Hola portal de Azure, seleccionar hello __cuentas de almacenamiento__ entrada bajo __propiedades__ no muestra las cuentas de almacenamiento agregadas a través de esta acción de secuencia de comandos. Azure PowerShell y la CLI de Azure no muestran cuenta de almacenamiento adicional de Hola o.

no se muestra información de almacenamiento de Hello porque el script de Hola sólo modifica la configuración de core-site.xml de hello para el clúster de Hola. Esta información no se utiliza al recuperar la información de clúster de hello mediante las API de administración de Azure.

información de cuenta de almacenamiento tooview agrega clúster toohello mediante este script, utilice Hola API de REST de Ambari. Usar hello después comandos tooretrieve esta información para el clúster:

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> Establecer `$clusterName` toohello nombre hello del clúster de HDInsight. Establecer `$storageAccountName` toohello nombre de cuenta de almacenamiento de Hola. Cuando se le solicite, escriba el inicio de sesión de clúster de hello (admin) y una contraseña.

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> Establecer `$PASSWORD` toohello contraseña de la cuenta de inicio de sesión (admin) de clúster. Establecer `$CLUSTERNAME` toohello nombre hello del clúster de HDInsight. Establecer `$STORAGEACCOUNTNAME` toohello nombre de cuenta de almacenamiento de Hola.
>
> Este ejemplo se utiliza [curl (http://curl.haxx.se/)](http://curl.haxx.se/) y [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve y analizar datos JSON.

Si utiliza este comando, reemplace __CLUSTERNAME__ con el nombre de Hola Hola del clúster de HDInsight. Reemplace __contraseña__ con la contraseña de inicio de sesión de hello HTTP para el clúster de Hola. Reemplace __STORAGEACCOUNT__ con el nombre de Hola de cuenta de almacenamiento de hello agregada mediante la acción de secuencia de comandos. Información devuelta por este comando aparece toohello similar siguiente texto:

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

Este texto es un ejemplo de una clave cifrada, que se usa tooaccess Hola cuenta de almacenamiento.

### <a name="unable-tooaccess-storage-after-changing-key"></a>No se puede tooaccess almacenamiento después de cambiar la clave

Si cambia la clave de Hola para una cuenta de almacenamiento, HDInsight ya no puede acceder a la cuenta de almacenamiento de Hola. HDInsight utiliza una copia en caché de clave en hello core-site.xml para clúster Hola. Esta copia en caché debe ser clave nueva de hello toomatch actualizada.

Ejecuta la acción de secuencia de comandos de hello nuevo __no__ actualizar la clave de hello, tal y como toosee el script de Hola comprueba si ya existe una entrada para la cuenta de almacenamiento de Hola. Si ya existe una entrada, no realice ningún cambio.

toowork solucionar este problema, debe quitar la entrada existente de Hola Hola cuenta de almacenamiento. Usar hello siguientes pasos tooremove Hola existente entrada:

1. En un explorador web, abra hello Ambari Web UI para el clúster de HDInsight. Hola URI es https://CLUSTERNAME.azurehdinsight.net. Reemplace __CLUSTERNAME__ con nombre hello del clúster.

    Cuando se le solicite, escriba Hola HTTP inicio de sesión y la contraseña para el clúster.

2. En la lista hello de servicios en la izquierda de Hola de página de hello, seleccione __HDFS__. A continuación, seleccione hello __configuraciones__ ficha en el centro de Hola de página Hola.

3. Hola __filtro...__  , introduzca un valor de __fs.azure.account__. Esto devuelve las entradas para las cuentas de almacenamiento adicional que se han agregado toohello clúster. Hay dos tipos de entradas; __keyprovider__ y __key__. Ambos contienen el nombre hello de cuenta de almacenamiento de hello como parte del nombre de clave de Hola.

    Hello siguientes son las entradas de ejemplo para una cuenta de almacenamiento denominada __mystorage__:

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. Después de haber identificado las claves de Hola Hola cuenta de almacenamiento necesita tooremove, usar hello rojo '-' toohello icono derecha de hello entrada toodelete lo. A continuación, usar hello __guardar__ botón toosave los cambios.

5. Una vez que se guardaron los cambios, utilice cuenta de almacenamiento de hello script acción tooadd hello y toohello valor de clave nuevo.

### <a name="poor-performance"></a>Rendimiento deficiente

Si la cuenta de almacenamiento de hello está en una región diferente de clúster de HDInsight de hello, puede experimentar un rendimiento deficiente. Acceso a datos de un región diferente envía tráfico de red fuera de centro de datos de Azure regional de Hola y a través Hola internet pública, que puede presentar latencia.

> [!WARNING]
> No se admite el uso de una cuenta de almacenamiento en una región diferente de clúster de HDInsight de Hola.

### <a name="additional-charges"></a>Cargos adicionales

Si cuenta de almacenamiento de hello es en una región distinta de Hola clúster de HDInsight, puede que experimente cargos de salida adicionales en la facturación de Azure. Se aplica un cargo de salida cuando los datos salen de un centro de datos regional. Este cargo se aplica incluso si el tráfico de hello está destinado a otro centro de datos de Azure en una región distinta.

> [!WARNING]
> No se admite el uso de una cuenta de almacenamiento en una región diferente de clúster de HDInsight de Hola.

## <a name="next-steps"></a>Pasos siguientes

Ha aprendido cómo las cuentas de almacenamiento adicional de tooadd tooan clúster de HDInsight existente. Para más información sobre las acciones de script, consulte [Personalización de clústeres de HDInsight basados en Linux mediante la acción de script](hdinsight-hadoop-customize-cluster-linux.md).
