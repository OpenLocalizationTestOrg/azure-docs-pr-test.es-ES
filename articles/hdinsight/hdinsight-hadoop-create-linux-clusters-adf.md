---
title: "aaaCreate clústeres de Hadoop de petición con factoría de datos: HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate clústeres de petición Hadoop en HDInsight con Data Factory de Azure."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a>Creación de clústeres de Hadoop en HDInsight mediante Azure Data Factory
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

[Factoría de datos de Azure](../data-factory/data-factory-introduction.md) es un servicio de integración de datos en la nube que organiza y automatiza el movimiento de Hola y la transformación de datos. Puede crear un tooprocess de just-in-time de clúster de Hadoop de HDInsight un segmento de datos de entrada y eliminar el clúster de hello cuando se completa el procesamiento de Hola. Algunas de las ventajas de hello del uso de un clúster de Hadoop de HDInsight a petición son:

- Pago solo para el trabajo de temporizador de Hola se está ejecutando en hello Hadoop de HDInsight de clúster (más un breve tiempo de inactividad configurable). facturación de Hola para clústeres de HDInsight es proporcional por minuto, independientemente de si se usa o no. Cuando se usa un servicio vinculado de HDInsight de petición de factoría de datos, clústeres de Hola se crean a petición. Y clústeres de Hola se eliminan automáticamente cuando se completan los trabajos de Hola. Por lo tanto, solo se paga por trabajo Hola duración y el tiempo de inactividad breve de hello (opción de período de vida).
- Puede crear un flujo de trabajo mediante una canalización de Data Factory. Por ejemplo, puede tener datos de toocopy de canalización de saludo de un tooan de SQL Server local almacenamiento de blobs de Azure, proceso Hola datos ejecutando un script de Hive y un script de Pig en un clúster de Hadoop de HDInsight a petición. A continuación, copie el resultado de hello datos tooan almacenamiento de datos de SQL Azure para tooconsume de aplicaciones de BI.
- Puede programar Hola flujo de trabajo toorun periódicamente (cada hora, diariamente, semanalmente, mensualmente, etcetera).

En Azure Data Factory, una factoría de datos puede tener una o varias canalizaciones de datos. Una canalización de datos consta de una o varias actividades. Hay dos tipos de actividades: [actividades de movimiento de datos](../data-factory/data-factory-data-movement-activities.md) y [actividades de transformación de datos](../data-factory/data-factory-data-transformation-activities.md). Utiliza los datos de toomove de actividades (en la actualidad, solo copia) de movimiento de datos de un almacén de datos de destino de origen datos almacén tooa. Usar datos de tootransform o proceso de las actividades de transformación de datos. Actividad de Hive de HDInsight es una de las actividades de transformación de hello admitidas factoría de datos. Usar la actividad de transformación de Hive de hello en este tutorial.

Puede configurar una toouse de actividad de hive su propio clúster de Hadoop de HDInsight o un clúster de Hadoop de HDInsight a petición. En este tutorial, actividad de Hive en la canalización de factoría de datos de Hola Hola es toouse configurado un clúster de HDInsight a petición. Por lo tanto, cuando la actividad hello ejecuta tooprocess un segmento de datos, sucede lo siguiente:

1. Automáticamente se crea un clúster de Hadoop de HDInsight de sector hello tooprocess just-in-time.  
2. datos de entrada de Hola se procesan mediante la ejecución de un script de HiveQL en clúster de Hola.
3. Hola clúster de Hadoop de HDInsight se elimina cuando ha finalizado el procesamiento de Hola y clúster Hola está inactivo durante la cantidad de hello configurado de tiempo (valor timeToLive). Si el segmento de datos de hello siguiente está disponible para su procesamiento con en este tiempo de inactividad timeToLive, hello mismo clúster es tooprocess usado Hola sector.  

En este tutorial, Hola script de HiveQL asociado a la actividad de hive hello realiza Hola siguientes acciones:

1. Crea una tabla externa que Hola de referencias de datos de registro de web sin formato almacenados en un almacenamiento de blobs de Azure.
2. Datos sin procesar de saludo de particiones por año y mes.
3. Hola a almacenes de datos particionados en hello almacenamiento de blobs de Azure.

En este tutorial, Hola script de HiveQL asociado a la actividad de hive hello crea una tabla externa que Hola de referencias de datos de registro de web sin formato almacenados en hello almacenamiento de blobs de Azure. Aquí son filas de ejemplo de Hola para cada mes en el archivo de entrada de Hola.

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

particiones de script de HiveQL Hola Hola datos sin procesar por año y mes. Crea tres carpetas de salida basadas en la entrada anterior Hola. Cada carpeta contiene un archivo con las entradas de cada mes.

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

Para obtener una lista de actividades de transformación de datos de factoría de datos en la actividad de tooHive de adición, vea [transformar y analizar con Data Factory de Azure](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> Actualmente, solo se puede crear un clúster de HDInsight versión 3.2 desde Azure Data Factory.

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar con instrucciones de hello en este artículo, debe tener Hola siguientes elementos:

* [Suscripción de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Azure PowerShell.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a>Preparación de la cuenta de almacenamiento
Puede usar las cuentas de almacenamiento de toothree en este escenario:

- cuenta de almacenamiento predeterminada para el clúster de HDInsight de Hola
- cuenta de almacenamiento de datos de entrada de Hola
- cuenta de almacenamiento de datos de salida de hello

tutorial de hello toosimplify, use una cuenta tooserve Hola tres propósitos de almacenamiento. script de ejemplo de Hola PowerShell de Azure en esta sección incluyen realiza Hola siguientes tareas:

1. Inicie sesión en tooAzure.
2. Cree un grupo de recursos de Azure.
3. Cree una cuenta de almacenamiento de Azure.
4. Crear un contenedor de Blob en la cuenta de almacenamiento de Hola
5. Copie Hola después de contenedor de blobs de toohello de dos archivos:

   * Archivo de datos de entrada: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)
   * Script de HiveQL: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)

     Ambos archivos se almacenan en un contenedor de blobs público.


**tooprepare Hola almacenamiento y copiar Hola archivos mediante Azure PowerShell:**
> [!IMPORTANT]
> Especifique nombres de cuenta de almacenamiento de Azure de Hola que va a crear script de Hola y el grupo de recursos de Azure de Hola.
> Anote **nombre del grupo de recursos**, **nombre de la cuenta de almacenamiento**, y **clave de la cuenta de almacenamiento** arroja script de Hola. Se necesita en la sección siguiente Hola.

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

Si necesita ayuda con la secuencia de comandos de PowerShell de hello, consulte [hello mediante PowerShell de Azure con el almacenamiento de Azure](../storage/common/storage-powershell-guide-full.md). Si le gustaría toouse CLI de Azure en su lugar, vea hello [apéndice](#appendix) sección para hello secuencia de comandos de CLI de Azure.

**tooexamine Hola almacenamiento cuenta Hola tipos de contenido y**

1. Inicio de sesión toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **grupos de recursos** en el panel izquierdo de Hola.
3. Haga doble clic en el nombre del grupo de recursos de Hola que creó en el script de PowerShell. Utilice el filtro de hello si tiene demasiados grupos de recursos que se muestran.
4. En hello **recursos** mosaico, debe tener un recurso, a menos que el grupo de recursos de Hola se comparte con otros proyectos. Ese recurso es la cuenta de almacenamiento de hello con nombre hello especificado anteriormente. Haga clic en el nombre de cuenta de almacenamiento de Hola.
5. Haga clic en hello **Blobs** iconos.
6. Haga clic en hello **adfgetstarted** contenedor. Verá dos carpetas: **inputdata** y **script**.
7. Abra la carpeta de Hola y compruebe Hola archivos en carpetas de Hola. Hola inputdata contiene archivos de hello input.log con datos de entrada y la carpeta de script de Hola contiene el archivo de script de HiveQL Hola.

## <a name="create-a-data-factory-using-resource-manager-template"></a>Creación de una factoría de datos mediante una plantilla de Resource Manager
Con la cuenta de almacenamiento de hello, datos de entrada de Hola y Hola script de HiveQL preparado, está listo toocreate un generador de datos de Azure. Existen varios métodos para crear Data Factory. En este tutorial, creará una factoría de datos mediante la implementación de una plantilla de Azure Resource Manager con hello portal de Azure. También puede implementar una plantilla de Resource Manager mediante la [CLI de Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) y [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template). Para otros métodos de creación de Data Factory, vea [Tutorial: creación de la  primera Data Factory](../data-factory/data-factory-build-your-first-pipeline.md).

1. Haga clic en hello siguientes toosign de imagen en tooAzure y plantilla de administrador de recursos abiertos Hola Hola portal de Azure. plantilla de Hola se encuentra en https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json. Vea hello [las entidades de la factoría de datos de plantilla de hello](#data-factory-entities-in-the-template) sección para obtener información detallada sobre las entidades definidas en la plantilla de Hola. 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Seleccione **usar existente** opción para hello **grupo de recursos** configuración y el nombre de select Hola Hola del grupo de recursos creado en el paso anterior hello (mediante el script de PowerShell).
3. Escriba un nombre para la factoría de datos de hello (**nombre de la factoría de datos**). Este nombre debe ser único globalmente.
4. Escriba hello **nombre de la cuenta de almacenamiento** y **clave de la cuenta de almacenamiento** anotó en el paso anterior de Hola.
5. Seleccione **muestro mi conformidad toohello términos y condiciones** indicados anteriormente después de leer **términos y condiciones**.
6. Seleccione **toodashboard Pin** opción.
6. Haga clic en **Comprar o crear**. Verá un icono en hello panel denominado **implementación de plantilla de implementación de**. Espere hasta que hello **grupo de recursos** abre el módulo para el grupo de recursos. También puede hacer clic en icono Hola titulada como su hoja de grupo de recursos grupo nombre tooopen Hola recursos.
6. Si la hoja de grupo de recursos de hello ya no está abierto, haga clic en grupo de recursos de hello mosaico tooopen Hola. Ahora verá un recurso de factoría de datos más aparece además toohello recurso de cuenta de almacenamiento.
7. Haga clic en nombre de saludo de la factoría de datos (valor especificado para hello **nombre de la factoría de datos** parámetro).
8. En la hoja de la factoría de datos de hello, haga clic en hello **diagrama** icono. diagrama de Hello muestra una actividad con un conjunto de datos de entrada y un conjunto de datos de salida:

    ![Diagrama de la canalización de la actividad de Hive bajo demanda de HDInsight para Data Factory de Azure](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    Hola nombres se definen en la plantilla de administrador de recursos de Hola.
9. Haga doble clic en **AzureBlobOutput**.
10. En hello **recientes actualizan sectores**, verá un sector. Si el estado de hello es **en curso**, espere hasta que se cambie demasiado**listo**. Proceso suele tardar aproximadamente **20 minutos** toocreate un clúster de HDInsight.

### <a name="check-hello-data-factory-output"></a>Compruebe la salida de factoría de datos de hello

1. Use Hola mismo procedimiento descrito en hello última sesión toocheck Hola contenedores hello adfgetstarted del contenedor de. Hay dos nuevos contenedores además demasiado**adfgetsarted**:

   * Un contenedor con nombre que sigue el patrón de hello: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`. Este contenedor es el contenedor predeterminado de hello para el clúster de HDInsight de Hola.
   * adfjobs: este contenedor es el contenedor de Hola Hola ADF registros de trabajos.

     resultado de factoría de datos de Hola se almacena en **afgetstarted** que haya configurado en la plantilla de administrador de recursos de Hola.
2. Haga clic en **adfgetstarted**.
3. Haga doble clic en **partitioneddata**. Verá un **año = 2014** carpeta porque todos los registros de hello web con una fecha en el año 2014.

    ![Salida de la canalización de la actividad de Hive bajo demanda de HDInsight para Data Factory de Azure](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    Si se profundiza lista hello, verá tres carpetas de enero, febrero y marzo. Además, hay un registro para cada mes.

    ![Salida de la canalización de la actividad de Hive bajo demanda de HDInsight para Data Factory de Azure](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a>Entidades de generador de datos en la plantilla de Hola
Aquí es cómo Hola plantilla nivel superior de administrador de recursos de una factoría de datos tiene un aspecto como:

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a>Definición de factoría de datos
Defina una factoría de datos en la plantilla de administrador de recursos de hello tal y como se muestra en el siguiente ejemplo de Hola:  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
Hola dataFactoryName es nombre Hola Hola factoría de datos que especifique al implementar la plantilla de Hola. Factoría de datos está actualmente solo se admite en regiones del este de EE., oeste de Estados Unidos y Europa del Norte Hola.

### <a name="defining-entities-within-hello-data-factory"></a>Definir las entidades de la factoría de datos de Hola
Hello siguientes entidades de la factoría de datos definidas en hello JSON plantilla:

* [Servicio vinculado de Almacenamiento de Azure](#azure-storage-linked-service)
* [Servicio vinculado a petición de HDInsight](#hdinsight-on-demand-linked-service)
* [Conjunto de datos de entrada de blob de Azure:](#azure-blob-input-dataset)
* [Conjunto de datos de salida de blob de Azure](#azure-blob-output-dataset)
* [Canalización de datos con una actividad de copia](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Servicio vinculado de Azure Storage
Hola almacenamiento de Azure vinculados a los vínculos de servicio su factoría de datos de almacenamiento de Azure cuenta toohello. En este tutorial, hello misma cuenta de almacenamiento se usa como cuenta de almacenamiento de HDInsight de hello predeterminada, el almacenamiento de datos de entrada y almacenamiento de datos de salida. Por consiguiente, se define solo un servicio vinculado Azure Storage. En definición de servicio vinculado de hello, especificar nombre de Hola y clave de la cuenta de almacenamiento de Azure. Vea [servicio vinculado de almacenamiento de Azure](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) para obtener más información sobre JSON toodefine de propiedades que se usan un almacenamiento de Azure servicio vinculado.

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
Hola **connectionString** usa Hola parámetros storageAccountName y storageAccountKey. Especifique valores para estos parámetros durante la implementación de plantilla de Hola.  

#### <a name="hdinsight-on-demand-linked-service"></a>Servicio vinculado a petición de HDInsight
Hola HDInsight a petición había vinculada definición de servicio, especifique valores para parámetros de configuración que se utilizan por toocreate de servicio de factoría de datos de hello clúster de Hadoop de HDInsight en tiempo de ejecución. Vea [servicios vinculados de proceso](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) un servicio vinculado de HDInsight a petición del artículo para obtener más información acerca de toodefine de propiedades que se usan JSON.  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
Tenga en cuenta Hola siguientes puntos:

* Hello factoría de datos se crea un **basados en Linux** clúster de HDInsight para usted.
* Hello clúster de Hadoop de HDInsight se crea en Hola misma región que la cuenta de almacenamiento de Hola.
* Hola aviso *timeToLive* configuración. factoría de datos de Hello elimina clúster Hola automáticamente después de clúster de saludo se está inactivo durante 30 minutos.
* clúster de HDInsight de Hello crea un **contenedor predeterminado** en almacenamiento de blobs de Hola que especificó en hello JSON (**linkedServiceName**). HDInsight no elimine este contenedor cuando se elimina el clúster de Hola. Este comportamiento es así por diseño. Con el servicio de vinculado de HDInsight a petición, se crea un clúster de HDInsight cada vez que un segmento necesario toobe procesado a menos que haya un clúster existente en vivo (**timeToLive**) y se elimina cuando se realiza un procesamiento Hola.

Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .

> [!IMPORTANT]
> A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure. Si no se necesita para solucionar problemas de trabajos de hello, quizá le interese toodelete ellos el costo de almacenamiento de tooreduce Hola. nombres de Hola de estos contenedores siguen un patrón: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Usar herramientas como [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) almacenamiento de blobs de contenedores de toodelete en Azure.

#### <a name="azure-blob-input-dataset"></a>Conjunto de datos de entrada de blob de Azure
En la definición de conjunto de datos de entrada de hello, especifique nombres Hola de contenedor de blobs, carpeta y archivo que contiene los datos de entrada de Hola. Vea [propiedades de conjunto de datos de Blob de Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) para obtener más información sobre JSON toodefine de propiedades que se usan un conjunto de datos de Blob de Azure.

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}

```

Tenga en cuenta Hola después de una configuración específica en la definición de JSON de hello:

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a>Conjunto de datos de salida de blob de Azure
En la definición de conjunto de datos de salida de hello, especificar nombres de Hola de contenedor de blob y la carpeta que contiene los datos de salida de hello. Vea [propiedades de conjunto de datos de Blob de Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) para obtener más información sobre JSON toodefine de propiedades que se usan un conjunto de datos de Blob de Azure.  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

Hola folderPath especifica hello toohello ruta de acceso que contiene los datos de salida de hello:

```json
"folderPath": "adfgetstarted/partitioneddata",
```

Hola [disponibilidad del conjunto de datos](../data-factory/data-factory-create-datasets.md#dataset-availability) configuración es la siguiente:

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

En la factoría de datos de Azure, canalización de salida de conjunto de datos disponibilidad unidades Hola. En este ejemplo, hello segmento se genera mensualmente Hola último día del mes (EndOfInterval). Para obtener más información, vea [Programación y ejecución de Data Factory](../data-factory/data-factory-scheduling-and-execution.md).

#### <a name="data-pipeline"></a>Canalización de datos
Defina una canalización que transforme los datos mediante la ejecución de un script de Hive en un clúster de Azure HDInsight a petición. Vea [JSON de canalización](../data-factory/data-factory-create-pipelines.md#pipeline-json) para obtener descripciones de elementos que se usan de JSON toodefine una canalización en este ejemplo.

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

canalización de Hello contiene una actividad, actividad de HDInsightHive. Como las fechas de inicio y finalización están en enero de 2016, se procesan los datos de un solo mes (un segmento). Ambos *iniciar* y *final* de actividad hello tienen una fecha pasada, por lo que Hola factoría de datos procesa los datos de mes de hello inmediatamente. Si el final de hello es una fecha futura, factoría de datos de hello crea otro segmento cuando llega la hora de Hola. Para obtener más información, vea [Programación y ejecución de Data Factory](../data-factory/data-factory-scheduling-and-execution.md).

## <a name="clean-up-hello-tutorial"></a>Limpiar el tutorial Hola

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a>Eliminar contenedores de blobs de hello creados por clúster de HDInsight a petición
Con el servicio de vinculado de HDInsight a petición, se crea un clúster de HDInsight cada vez que un segmento necesario toobe procesado a menos que haya un clúster existente en vivo (timeToLive); y clúster Hola se elimina cuando se realiza un procesamiento Hola. Para cada clúster, Data Factory de Azure crea un contenedor de blobs en almacenamiento de blobs de Azure que se usará como cuenta de almacenamiento (SAN) de hello predeterminada para el clúster de Hola Hola. Incluso si se elimina el clúster de HDInsight, contenedor de almacenamiento de blobs predeterminado de Hola y cuenta de almacenamiento de hello asociada no se eliminan. Este comportamiento es así por diseño. A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure. Si no se necesita para solucionar problemas de trabajos de hello, quizá le interese toodelete ellos el costo de almacenamiento de tooreduce Hola. nombres de Hola de estos contenedores siguen un patrón: `adfyourdatafactoryname-linkedservicename-datetimestamp`.

Eliminar hello **adfjobs** y **adfyourdatafactoryname-linkedservicename-datetimestamp** carpetas. contenedor de Hello adfjobs contiene registros de trabajos de Data Factory de Azure.

### <a name="delete-hello-resource-group"></a>Eliminar grupo de recursos de Hola
[El Administrador de recursos Azure](../azure-resource-manager/resource-group-overview.md) es toodeploy usado, administrar y supervisar la solución como un grupo.  Eliminar un grupo de recursos, elimina todos los componentes de hello dentro de grupo de Hola.  

1. Inicio de sesión toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **grupos de recursos** en el panel izquierdo de Hola.
3. Haga clic en el nombre del grupo de recursos de Hola que creó en el script de PowerShell. Utilice el filtro de hello si tiene demasiados grupos de recursos que se muestran. Grupo de recursos de Hola se abre en una nueva hoja.
4. En hello **recursos** mosaico, debe tener cuenta de almacenamiento predeterminada de Hola y el generador de datos de hello, a menos que el grupo de recursos de Hola se comparte con otros proyectos.
5. Haga clic en **eliminar** en la parte superior de Hola de hoja de Hola. Si lo hace, elimina la cuenta de almacenamiento de Hola y datos de hello almacenados en la cuenta de almacenamiento de Hola.
6. Escriba la eliminación de tooconfirm del nombre del grupo de recursos de hello y, a continuación, haga clic en **eliminar**.

En caso de que no desea cuenta de almacenamiento de hello toodelete cuando se elimina el grupo de recursos de hello, considere la posibilidad de hello después arquitectura mediante la separación de datos de negocio de saludo de cuenta de almacenamiento predeterminada de Hola. En este caso, tiene un grupo de recursos Hola cuenta de almacenamiento con datos de negocio de Hola y Hola a otro grupo de recursos de cuenta de almacenamiento predeterminada de Hola para HDInsight vinculado hello y servicio de factoría de datos. Cuando se elimina el segundo grupo de recursos de hello, que no afecte a cuenta de almacenamiento de datos de negocio de Hola. toodo para:

* Agregar Hola después el grupo de recursos de nivel superior de toohello junto con hello Microsoft.DataFactory/datafactories recursos en la plantilla de administrador de recursos. Crea una cuenta de almacenamiento:

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* Agregar una nueva toohello de punto de servicio vinculado nueva cuenta de almacenamiento:

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* Configurar el servicio de ondemand vinculado de HDInsight de hello con un dependsOn adicional y un additionalLinkedServiceNames:

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido cómo tooprocess de clúster de HDInsight de toouse toocreate Data Factory de Azure a petición trabajos de Hive. tooread más:

* [Tutorial de Hadoop: Introducción al uso de Hadoop en HDInsight basado en Linux](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Documentación de HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Documentación de Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a>Anexo

### <a name="azure-cli-script"></a>Script de la CLI de Azure
Puede utilizar la CLI de Azure en lugar de utilizar el tutorial de Azure PowerShell toodo Hola. toouse CLI de Azure, instale primero la CLI de Azure según Hola siguiendo las instrucciones:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a>Usar el almacenamiento de Azure CLI tooprepare hello y copie los archivos de Hola

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

es el nombre del contenedor de Hello *adfgetstarted*. Déjelo como está. En caso contrario es necesaria una plantilla de administrador de recursos de tooupdate Hola. Si necesita ayuda para esta secuencia de comandos CLI, consulte [Using Hola CLI de Azure con el almacenamiento de Azure](../storage/common/storage-azure-cli.md).
