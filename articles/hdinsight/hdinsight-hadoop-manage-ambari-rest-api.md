---
title: aaaMonitor y administrar Hadoop con la API de REST de Ambari - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Ambari toomonitor y administrar clústeres de Hadoop en HDInsight de Azure. En este documento, obtendrá información sobre cómo clústeres toouse Hola API de REST de Ambari incluido con HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 1866a77c8e402231bccbcfba7174253aca41339b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a>Administrar clústeres de HDInsight con Ambari API de REST de Hola

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Obtenga información acerca de cómo toouse Hola API de REST de Ambari toomanage y supervisar clústeres de Hadoop en HDInsight de Azure.

Apache Ambari simplifica la administración de Hola y supervisión de un clúster de Hadoop proporcionando fácil toouse web API de REST y de interfaz de usuario. Ambari se incluye en los clústeres de HDInsight que usan el sistema operativo de Linux de Hola. Puede usar Ambari toomonitor Hola clúster y realizar cambios de configuración.

## <a id="whatis"></a>¿Qué es Ambari?

[Apache Ambari](http://ambari.apache.org) proporciona la interfaz de usuario que puede ser usado tooprovision, administrar y supervisar clústeres de Hadoop web. Los desarrolladores pueden integrar estas capacidades en sus aplicaciones mediante el uso de hello [API de REST de Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

De manera predeterminada, Ambari viene con los clústeres de HDInsight basado en Linux.

## <a name="how-toouse-hello-ambari-rest-api"></a>¿Cómo toouse Hola Ambari API de REST

> [!IMPORTANT]
> Hola información y ejemplos de este documento requieren un clúster de HDInsight que usa el sistema operativo Linux. Para más información, vea la [introducción a HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

ejemplos de Hello en este documento se proporcionan para que el shell de Bourne hello (intensiva de errores) y PowerShell. bash Hola ejemplos se han probado con GNU bash 4.3.11, pero deben funcionar con otros shells de Unix. ejemplos de PowerShell de Hola se han probado con PowerShell 5.0, pero deberían funcionar con PowerShell 3.0 o superior.

Si usa hello __shell Bourne__ (intensiva de errores), debe tener instalado el siguiente hello:

* [cURL](http://curl.haxx.se/): cURL es una utilidad que puede ser toowork utilizado con las API de REST de línea de comandos de Hola. En este documento, es toocommunicate usado con hello API de REST de Ambari.

Tanto si usa Bash como PowerShell, también debe tener [jq](https://stedolan.github.io/jq/) instalado. Jq es una utilidad para trabajar con documentos JSON. Se utiliza en **todos los** Hola ejemplos intensiva de errores, y **una** de ejemplos de PowerShell de Hola.

### <a name="base-uri-for-ambari-rest-api"></a>URI base para la API de REST de Ambari

URI base para hello API de REST de Ambari en HDInsight Hello es https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, donde **CLUSTERNAME** es Hola nombre del clúster.

> [!IMPORTANT]
> Mientras el nombre de clúster de Hola Hola completo parte del dominio (FQDN) del nombre del programa Hola URI (CLUSTERNAME.azurehdinsight.net) distingue mayúsculas de minúsculas, otras apariciones en hello URI distinguen mayúsculas de minúsculas. Por ejemplo, si el clúster se denomina `MyCluster`, siguiente Hola es URI válidos:
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> siguiente Hola URI devuelve un error porque no es Hola Hola segunda aparición del nombre de hello corregir caso.
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a>Autenticación

Conexión tooAmbari en HDInsight requiere HTTPS. Nombre de la cuenta de administrador de uso hello (valor predeterminado de hello es **administración**) y la contraseña proporcionados durante la creación del clúster.

## <a name="examples-authentication-and-parsing-json"></a>Ejemplos: Autenticación y análisis JSON

Hello en los ejemplos siguientes muestra cómo toomake una solicitud GET en hello base Ambari API de REST:

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> en los ejemplos de este documento Hola intensiva de errores que Hola siguientes supuestos:
>
> * nombre de inicio de sesión de Hello para el clúster de hello es Hola valor predeterminado `admin`.
> * `$PASSWORD`contiene la contraseña de Hola para hello comando de inicio de sesión de HDInsight. Puede establecer este valor mediante `PASSWORD='mypassword'`.
> * `$CLUSTERNAME`contiene el nombre de Hola de clúster de Hola. Puede establecer este valor mediante `set CLUSTERNAME='clustername'`.

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> ejemplos de PowerShell de Hello en este documento que Hola siguientes supuestos:
>
> * `$creds`es un objeto de credencial que contiene el inicio de sesión de administrador de hello y una contraseña para el clúster de Hola. Puede establecer este valor mediante `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` y proporcionar las credenciales de hello cuando se le solicite.
> * `$clusterName`es una cadena que contiene el nombre de hello del clúster de Hola. Puede establecer este valor mediante `$clusterName="clustername"`.

Ambos ejemplos devuelven un documento JSON que comienza con información toohello similar siguiente ejemplo:

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a>Análisis de datos JSON

Hello siguiente ejemplo se utiliza `jq` tooparse Hola documento de respuesta JSON y mostrar solo hello `health_report` información de resultados de Hola.

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

PowerShell 3.0 y versiones posterior proporciona hello `ConvertFrom-Json` cmdlet, que convierte el documento JSON de hello en un objeto que es más fácil toowork con de PowerShell. Hello siguiente ejemplo se utiliza `ConvertFrom-Json` toodisplay solo hello `health_report` información de resultados de Hola.

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> Aunque la mayoría de los ejemplos de este documento se usa `ConvertFrom-Json` toodisplay elementos de documento de respuesta de Hola Hola [configuración de actualización Ambari](#example-update-ambari-configuration) en el ejemplo se utiliza jq. Jq se utiliza en este ejemplo tooconstruct una nueva plantilla de documento de respuesta JSON de Hola.

Para obtener una referencia completa de hello API de REST, consulte [V1 de referencia de API de Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a>Ejemplo: Obtener Hola FQDN de nodos de clúster

Cuando se trabaja con HDInsight, necesita el nombre de dominio completo de Hola de tooknow (FQDN) de un nodo de clúster. Puede recuperar con facilidad hello FQDN para saludo diversos nodos de clúster de hello mediante hello en los ejemplos siguientes:

* **Todos los nodos**

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* **Nodos principales**

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **Nodos de trabajo**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **Nodos de Zookeeper**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a>Ejemplo: Obtener la dirección IP interna de Hola de nodos de clúster

> [!IMPORTANT]
> direcciones IP de Hello devueltas en los ejemplos de hello en esta sección están no directamente accesible over Hola internet. Solo están accesibles desde la red Virtual de Azure que contiene el clúster de HDInsight de Hola Hola.
>
> Para obtener más información sobre el uso de HDInsight y de las redes virtuales, vea [Extensión de las funcionalidades de HDInsight con una red virtual de Azure personalizada](hdinsight-extend-hadoop-virtual-network.md).

dirección IP de toofind hello, debe conocer el nombre de dominio completo interno de hello (FQDN) del programa Hola a los nodos del clúster. Una vez que tenga Hola FQDN, a continuación, puede obtener dirección IP de Hola de host de Hola. Hello en los ejemplos siguientes primero consultan Ambari Hola FQDN de todos los nodos de host de Hola y consultan Ambari para la dirección IP de Hola de cada host.

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-hello-default-storage"></a>Ejemplo: Obtener almacenamiento predeterminado de Hola

Cuando se crea un clúster de HDInsight, debe usar una cuenta de almacenamiento de Azure o un almacén de Data Lake como almacenamiento predeterminado de hello para el clúster de Hola. Puede usar Ambari tooretrieve esta información una vez creado el clúster de Hola. Por ejemplo, si desea que el contenedor de toohello tooread/escritura datos fuera de HDInsight.

Hello en los ejemplos siguientes recuperan configuración de almacenamiento predeterminada de Hola Hola clúster de:

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> Estos ejemplos devuelven Hola primer servidor de toohello de configuración que se aplica (`service_config_version=1`) que contiene esta información. Si recupera un valor que se ha modificado después de la creación del clúster, puede necesita toolist Hola configuración versiones y recuperar hello más reciente.

valor devuelto de Hello es tooone similar de hello en los ejemplos siguientes:

* `wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Este valor indica que ese clúster Hola está usando una cuenta de almacenamiento de Azure para el almacenamiento de forma predeterminada. Hola `ACCOUNTNAME` valor es Hola nombre de cuenta de almacenamiento de Hola. Hola `CONTAINER` parte es el nombre de Hola Hola del contenedor de blobs en la cuenta de almacenamiento de Hola. contenedor de Hello es la raíz de Hola de almacenamiento compatible HDFS del clúster Hola Hola.

* `adl://home`-Este valor indica que ese clúster Hola está usando un almacén de Data Lake de Azure para el almacenamiento de forma predeterminada.

    nombre de cuenta de almacén de Data Lake de toofind hello, Hola de uso en los ejemplos siguientes:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    Hello valor devuelto es similar demasiado`ACCOUNTNAME.azuredatalakestore.net`, donde `ACCOUNTNAME` es Hola nombre de cuenta de almacén de Data Lake Hola.

    directorio de hello toofind dentro de almacén de Data Lake que contiene almacenamiento Hola Hola del clúster, Hola de uso en los ejemplos siguientes:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    Hello valor devuelto es similar demasiado`/clusters/CLUSTERNAME/`. Este valor es una ruta de acceso dentro de la cuenta de almacén de Data Lake Hola. Esta ruta de acceso es la raíz de Hola de hello HDFS compatible filesystem para clúster Hola. 

> [!NOTE]
> Hola `Get-AzureRmHDInsightCluster` cmdlet proporcionado por [Azure PowerShell](/powershell/azure/overview) también devuelve Hola información de almacenamiento de clúster en Hola.


## <a name="example-get-configuration"></a>Ejemplo: Obtener configuración

1. Obtener las configuraciones de Hola que están disponibles para el clúster.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    Este ejemplo devuelve un documento JSON que contiene la configuración actual de hello (identificada por hello *etiqueta* valor) para los componentes de hello instalados en el clúster de Hola. Hello ejemplo siguiente es un extracto de datos de hello devueltos desde un tipo de clúster de Spark.
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. Obtiene la configuración de hello para el componente de Hola que le interesa. Hola siguiente ejemplo, reemplace `INITIAL` con el valor de etiqueta de hello procedente de la solicitud anterior de Hola.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    Este ejemplo devuelve un documento JSON que contiene la configuración actual de Hola Hola `core-site` componente.

## <a name="example-update-configuration"></a>Ejemplo: Actualizar la configuración

1. Obtener la configuración actual de hello, que Ambari se almacena como Hola "configuración deseada":

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    Este ejemplo devuelve un documento JSON que contiene la configuración actual de hello (identificada por hello *etiqueta* valor) para los componentes de hello instalados en el clúster de Hola. Hello ejemplo siguiente es un extracto de datos de hello devueltos desde un tipo de clúster de Spark.
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    En esta lista, necesita toocopy Hola nombre del componente de hello (por ejemplo, **spark\_thrift\_sparkconf** hello y **etiqueta** valor.

2. Recuperar configuración hello para el componente de Hola y etiqueta mediante Hola siguientes comandos:
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    > [!NOTE]
    > Reemplace **sparkconf de thrift de spark** y **inicial** en el componente de Hola y etiquetas que desee que la configuración de hello tooretrieve para.
   
    Jq son los datos de hello tooturn usado recuperados desde HDInsight en una nueva plantilla de configuración. En concreto, estos ejemplos realiza Hola siguientes acciones:
   
    * Crea un valor único que contiene la cadena de Hola "versión" y la fecha de hello, que se almacena en `newtag`.

    * Crea un documento de raíz para la nueva configuración deseada de Hola.

    * Obtiene Hola contenido de hello `.items[]` de matriz y lo agrega a hello **desired_config** elemento.

    * Hola eliminaciones `href`, `version`, y `Config` elementos, como estos elementos no están necesario toosubmit una nueva configuración.

    * Agrega un nuevo elemento `tag` con un valor de `version#################`. parte numérica de Hola se basa en hello fecha actual. Cada configuración debe tener una etiqueta única.
     
    Por último, se guardan los datos de hello toohello `newconfig.json` documento. estructura del documento Hola debe aparecer similar toohello siguiente ejemplo:
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. Abra hello `newconfig.json` documento y agregar o modificar valores de hello `properties` objeto. ejemplo siguiente se cambia Hola Hola valo `"spark.yarn.am.memory"` de `"1g"` demasiado`"3g"`. También agrega `"spark.kryoserializer.buffer.max"` con un valor de `"256m"`.
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    Guardar archivo hello cuando haya terminado de realizar modificaciones.

4. Usar hello después comandos toosubmit Hola actualizar configuración tooAmbari.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    Estos comandos enviar contenido Hola de hello **newconfig.json** archivo toohello clúster Hola configuración deseado de nuevo. solicitud de Hello devuelve un documento JSON. Hola **versionTag** elemento en este documento debe coincidir con la versión de Hola envía y Hola **configuraciones** objeto contiene los cambios de configuración de hello solicitado.

### <a name="example-restart-a-service-component"></a>Ejemplo: Reiniciar un componente de servicio

En este momento, si mira en la interfaz de usuario de web de Ambari hello, Hola servicio de Spark indica que requiere toobe reiniciarse para que apliquen la nueva configuración de Hola. Usar hello después pasos toorestart Hola servicio.

1. Usar hello después tooenable de modo de mantenimiento para el servicio de Spark hello:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    Estos comandos de envío de un servidor de toohello de documento JSON que activa el modo de mantenimiento. Puede comprobar que servicio Hola ahora está en modo de mantenimiento usando Hola después de solicitud:
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    Hello valor devuelto es `ON`.

2. A continuación, usar hello después tooturn desactivar servicio hello:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    respuesta de Hello es similar toohello siguiente ejemplo:
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > Hola `href` valor devuelto por este identificador URI está usando la dirección IP interna de Hola Hola del nodo de clúster. toouse desde el clúster fuera de hello, reemplazar parte de hello '10.0.0.18:8080' con el FQDN del clúster de Hola Hola. 
    
    Hola, siga los comandos recuperar el estado de Hola de solicitud de hello:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    Una respuesta de `COMPLETED` indica que la solicitud Hola ha finalizado.

3. Cuando se completa la solicitud anterior de hello, utilice Hola después toostart Hola servicio.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    servicio de Hello ahora está usando la nueva configuración de Hola.

4. Por último, utilice Hola después tooturn desactiva el modo de mantenimiento.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a>Pasos siguientes

Para obtener una referencia completa de hello API de REST, consulte [V1 de referencia de API de Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

