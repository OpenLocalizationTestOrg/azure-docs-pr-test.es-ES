---
title: "aaaUse toocreate de plantillas de Azure HDInsight y almacén de Data Lake | Documentos de Microsoft"
description: "Utilice toocreate de plantillas de administrador de recursos de Azure y clústeres de HDInsight con el almacén de Azure Data Lake"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a>Creación de un clúster de HDInsight con Data Lake Store mediante las plantillas de Azure Resource Manager
> [!div class="op_single_selector"]
> * [Uso del Portal](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Uso de PowerShell (para el almacenamiento predeterminado)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Uso de PowerShell (para el almacenamiento adicional)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Uso de Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Obtenga información acerca de cómo toouse Azure PowerShell tooconfigure un HDInsight de clúster con el almacén de Azure Data Lake **como almacenamiento adicional**.

Para los tipos de clúster compatibles, Data Lake Store se puede usar como un almacenamiento predeterminado o una cuenta de almacenamiento adicional. Cuando se utiliza el almacén de Data Lake como almacenamiento adicional, cuenta de almacenamiento predeterminada de Hola para clústeres de hello seguirán estando Blobs de almacenamiento de Azure (WASB) y archivos relacionados con el clúster de hello (por ejemplo, registros, etc.) se escriben todavía almacenamiento predeterminado de toohello, mientras que los datos de Hola que desea tooprocess pueden almacenarse en una cuenta de almacén de Data Lake. Usar almacén de Data Lake como una cuenta de almacenamiento adicional no afecta a rendimiento u Hola capacidad tooread/escritura toohello almacenamiento Hola clúster.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>Uso de Data Lake Store para el almacenamiento de clústeres de HDInsight

Estas son algunas consideraciones importantes que deben tenerse en cuenta al usar HDInsight con Data Lake Store:

* Clústeres de HDInsight de toocreate opción con acceso tooData Lake almacén como almacenamiento predeterminado está disponible para HDInsight versión 3.5 y 3.6.

* Clústeres de HDInsight de toocreate opción con acceso tooData Lake almacén como almacenamiento adicional está disponible para las versiones 3.2, 3.4, 3.5 y 3.6 de HDInsight.

En este artículo, aprovisionamos un clúster de Hadoop con el Almacén de Data Lake como almacenamiento adicional. Para obtener instrucciones sobre cómo toocreate un Hadoop de clúster con el almacén de Data Lake como almacenamiento predeterminado, consulte [crear un clúster de HDInsight con el almacén de Data Lake mediante el Portal de Azure](data-lake-store-hdinsight-hadoop-use-portal.md).

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 o versiones posteriores**. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).
* **Entidad de servicio de Azure Active Directory** Pasos de este tutorial proporcionan instrucciones sobre cómo toocreate una entidad de servicio en Azure AD. Sin embargo, debe ser un toocreate capaz de Azure AD administrador toobe una entidad de servicio. Si eres un administrador de Azure AD, puede omitir este requisito previo y continuar con tutorial Hola.

    **Si no es un administrador de Azure AD**, no será capaz de tooperform Hola pasos necesarios toocreate una entidad de servicio. En este caso, su administrador de Azure AD debe generar primero una entidad de servicio antes de crear un clúster de HDInsight con Data Lake Store. Además, entidad de servicio de hello debe crearse con un certificado, como se describe en [crear una entidad de servicio con el certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a>Creación de un clúster de HDInsight con Azure Data Lake Store
plantilla de administrador de recursos de Hola y requisitos previos de Hola para usar la plantilla hello, están disponibles en GitHub en [implementar un clúster de HDInsight Linux con el nuevo almacén de Data Lake](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage). Siga las instrucciones de hello proporcionadas en este vínculo toocreate un clúster de HDInsight con el almacén de Data Lake de Azure como almacenamiento adicional de Hola.

instrucciones de Hello en el vínculo de hello mencionadas anteriormente requieren PowerShell. Antes de empezar con estas instrucciones, asegúrese de que inicie sesión en tooyour cuenta de Azure. Desde el escritorio, abra una nueva ventana de PowerShell de Azure y escriba Hola siguientes fragmentos de código. Cuando toolog solicitada, asegúrese de que inicie sesión como una suscripción de hello admininistrators/propietario:

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a>Cargar el almacén de datos toohello Azure Data Lake de ejemplo
plantilla de administrador de recursos de Hello crea una nueva cuenta de almacén de Data Lake y lo asocia con clúster de HDInsight Hola. Ahora debe cargar algunos toohello de datos de ejemplo almacén de Data Lake. Necesitará estos datos más adelante en trabajos de toorun tutorial Hola desde un clúster de HDInsight que tienen acceso a datos en el almacén de Data Lake Hola. Para obtener instrucciones sobre cómo ver datos tooupload, [cargar un almacén de Data Lake de archivo tooyour](data-lake-store-get-started-portal.md#uploaddata). Si desea obtener algunos tooupload de datos de ejemplo, puede obtener hello **ambulancia datos** carpeta de hello [repositorio de Git de Azure datos Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).

## <a name="set-relevant-acls-on-hello-sample-data"></a>Establecer las ACL relevantes en los datos de ejemplo de Hola
toomake seguro de datos de ejemplo de Hola que cargue están accesibles desde el clúster de HDInsight de hello, debe asegurarse de que la aplicación hello Azure AD identidad tooestablish utilizado entre el clúster de HDInsight de Hola y almacén de Data Lake tiene acceso toohello archivo o carpeta que está intentar tooaccess. toodo, realizar Hola pasos.

1. Encontrar Hola nombre de aplicación de Azure AD que está asociado con el clúster de HDInsight de Hola y Hola almacén de Data Lake. Toolook unidireccional para nombre de hello hoja de clúster de HDInsight tooopen Hola que haya creado mediante la plantilla de administrador de recursos de hello, haga clic en hello **identidad de AAD de clúster** y a buscar valor hello **entidad de servicio Nombre para mostrar**.
2. Ahora, proporcionar acceso toothis aplicación de Azure AD en hello, archivo o carpeta que desea tooaccess de clúster de HDInsight de Hola. vea tooset Hola ACL de derechos en hello archivo o carpeta en el almacén de Data Lake [proteger los datos en el almacén de Data Lake](data-lake-store-secure-data.md#filepermissions).

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Ejecutar trabajos de prueba en Hola de toouse de clúster de HDInsight de hello almacén de Data Lake
Después de haber configurado un clúster de HDInsight, se puede ejecutar trabajos de prueba en hello clúster tootest ese hello HDInsight clúster puede tener acceso a almacén de Data Lake. toodo por lo tanto, se ejecutará un trabajo de Hive de ejemplo que crea una tabla con datos de ejemplo de Hola que cargan almacén de Data Lake de tooyour anteriores.

En esta sección le SSH en un clúster de HDInsight Linux y ejecución Hola una consulta de Hive de ejemplo. Si usa un cliente Windows, se recomienda usar **PuTTY**, que se puede descargar en [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Para obtener más información sobre el uso de PuTTY, consulte [Uso de SSH con Hadoop basado en Linux en HDInsight desde Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

1. Una vez conectado, inicie Hola Hive CLI mediante Hola siguiente comando:

   ```
   hive
   ```
2. Hola CLI, escriba Hola siguiendo las instrucciones toocreate una nueva tabla denominada **vehículos** mediante el uso de datos de ejemplo de Hola Hola almacén de Data Lake:

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   Debería ver un siguiente toohello similar de salida:

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a>Acceso al Almacén de Data Lake mediante comandos de HDFS
Una vez haya configurado el almacén de hello HDInsight clúster toouse Data Lake, puede usar comandos de shell de hello HDFS tooaccess Hola almacén.

En esta sección le SSH en un clúster de HDInsight Linux y ejecución Hola comandos HDFS. Si usa un cliente Windows, se recomienda usar **PuTTY**, que se puede descargar en [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Para obtener más información sobre el uso de PuTTY, consulte [Uso de SSH con Hadoop basado en Linux en HDInsight desde Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

Una vez conectado, use Hola siguientes archivos HDFS filesystem comando toolist Hola Hola almacén de Data Lake.

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

Esto debería incluir archivo hello que cargan almacén de Data Lake de toohello anteriores.

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

También puede usar hello `hdfs dfs -put` comando tooupload algunos toohello archivos del almacén de Data Lake y, a continuación, usar `hdfs dfs -ls` tooverify si los archivos de saludo se cargaron correctamente.


## <a name="next-steps"></a>Pasos siguientes
* [Copiar los datos de almacén de Blobs de Azure almacenamiento Lake tooData](data-lake-store-copy-data-wasb-distcp.md)
