---
title: "Solución de problemas de la Factoría de datos de Azure"
description: "Obtenga información acerca de la solución de problemas relacionados con la factoría de datos de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 953a2703db7c8991f580a7c963d6cbd94265c213
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="36ed5-103">Solución de problemas de la factoría de datos</span><span class="sxs-lookup"><span data-stu-id="36ed5-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="36ed5-104">En este artículo se proporcionan consejos para solución de problemas surgidos al usar Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="36ed5-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="36ed5-105">Este artículo no incluye todos los posibles problemas que pueden aparecer al usar el servicio, pero trata algunos de ellos, así como consejos para solución de problemas generales.</span><span class="sxs-lookup"><span data-stu-id="36ed5-105">This article does not list all the possible issues when using the service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="36ed5-106">Sugerencias de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="36ed5-106">Troubleshooting tips</span></span>
### <a name="error-the-subscription-is-not-registered-to-use-namespace-microsoftdatafactory"></a><span data-ttu-id="36ed5-107">Error: La suscripción no está registrada para usar el espacio de nombres 'Microsoft.DataFactory'</span><span class="sxs-lookup"><span data-stu-id="36ed5-107">Error: The subscription is not registered to use namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="36ed5-108">Si recibe este error, el proveedor de recursos de Data Factory de Azure no se ha registrado en su equipo.</span><span class="sxs-lookup"><span data-stu-id="36ed5-108">If you receive this error, the Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="36ed5-109">Haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="36ed5-109">Do the following:</span></span>

1. <span data-ttu-id="36ed5-110">Inicie Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36ed5-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="36ed5-111">Inicie sesión en la cuenta de Azure mediante el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="36ed5-111">Log in to your Azure account using the following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="36ed5-112">Ejecute el siguiente comando para registrar el proveedor de Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="36ed5-112">Run the following command to register the Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="36ed5-113">Problema: error no autorizado al ejecutar un cmdlet de Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="36ed5-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="36ed5-114">Probablemente no está usando la cuenta o suscripción de Azure correctas con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36ed5-114">You are probably not using the right Azure account or subscription with the Azure PowerShell.</span></span> <span data-ttu-id="36ed5-115">Use los cmdlets siguientes para seleccionar la cuenta y la suscripción de Azure correctas que se usarán con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36ed5-115">Use the following cmdlets to select the right Azure account and subscription to use with the Azure PowerShell.</span></span>

1. <span data-ttu-id="36ed5-116">Login-AzureRmAccount: use el id. de usuario y la contraseña correctos.</span><span class="sxs-lookup"><span data-stu-id="36ed5-116">Login-AzureRmAccount - Use the right user ID and password</span></span>
2. <span data-ttu-id="36ed5-117">Get-AzureRmSubscription: consulte todas las suscripciones de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="36ed5-117">Get-AzureRmSubscription - View all the subscriptions for the account.</span></span>
3. <span data-ttu-id="36ed5-118">Select-AzureRmSubscription &lt;nombre de la suscripción&gt;: seleccione la suscripción correcta.</span><span class="sxs-lookup"><span data-stu-id="36ed5-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select the right subscription.</span></span> <span data-ttu-id="36ed5-119">Use la misma que usó para crear una factoría de datos en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="36ed5-119">Use the same one you use to create a data factory on the Azure portal.</span></span>

### <a name="problem-fail-to-launch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="36ed5-120">Problema: no se pudo iniciar la configuración rápida de Data Management Gateway desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="36ed5-120">Problem: Fail to launch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="36ed5-121">La configuración rápida de Data Management Gateway requiere Internet Explorer o un explorador web compatible con Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="36ed5-121">The Express setup for the Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="36ed5-122">Si no se puede iniciar la configuración rápida, realice una de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="36ed5-122">If the Express Setup fails to start, do one of the following:</span></span>

* <span data-ttu-id="36ed5-123">Utilice Internet Explorer o un explorador web compatible con Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="36ed5-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="36ed5-124">Si usa Chrome, vaya a [Chrome Web Store](https://chrome.google.com/webstore/), busque la palabra clave "ClickOnce", elija una de las extensiones de ClickOnce e instálela.</span><span class="sxs-lookup"><span data-stu-id="36ed5-124">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="36ed5-125">Debe hacer lo mismo para Firefox (instale un complemento).</span><span class="sxs-lookup"><span data-stu-id="36ed5-125">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="36ed5-126">Haga clic en el botón Abrir menú de la barra de herramientas (tres líneas horizontales en la esquina superior derecha), haga clic en Complementos, busque la palabra clave "ClickOnce", elija una de las extensiones de ClickOnce e instálela.</span><span class="sxs-lookup"><span data-stu-id="36ed5-126">Click Open Menu button on the toolbar (three horizontal lines in the top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="36ed5-127">Haga clic en el vínculo **Instalación manual** que aparece en la misma hoja del portal.</span><span class="sxs-lookup"><span data-stu-id="36ed5-127">Use the **Manual Setup** link shown on the same blade in the portal.</span></span> <span data-ttu-id="36ed5-128">Utilice este enfoque para descargar el archivo de instalación y ejecutarlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="36ed5-128">You use this approach to download installation file and run it manually.</span></span> <span data-ttu-id="36ed5-129">Después de realizarse correctamente la instalación, verá el cuadro de diálogo Configuración de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="36ed5-129">After the installation is successful, you see the Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="36ed5-130">Copie la **clave** desde la pantalla del portal y úsela en el administrador de configuración para registrar manualmente la puerta de enlace con el servicio.</span><span class="sxs-lookup"><span data-stu-id="36ed5-130">Copy the **key** from the portal screen and use it in the configuration manager to manually register the gateway with the service.</span></span>  

### <a name="problem-fail-to-connect-to-on-premises-sql-server"></a><span data-ttu-id="36ed5-131">Problema: no se pudo conectar al servidor SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="36ed5-131">Problem: Fail to connect to on-premises SQL Server</span></span>
<span data-ttu-id="36ed5-132">Inicie **Administrador de configuración de Data Management Gateway** en el equipo de la puerta de enlace y use la pestaña **Solución de problemas** para probar la conexión a SQL Server desde el equipo de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="36ed5-132">Launch **Data Management Gateway Configuration Manager** on the gateway machine and use the **Troubleshooting** tab to test the connection to SQL Server from the gateway machine.</span></span> <span data-ttu-id="36ed5-133">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="36ed5-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="36ed5-134">Problema: Los segmentos de entrada están en el estado En espera de forma permanente.</span><span class="sxs-lookup"><span data-stu-id="36ed5-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="36ed5-135">Los intervalos pueden tener el estado **En espera** por diversos motivos.</span><span class="sxs-lookup"><span data-stu-id="36ed5-135">The slices could be in **Waiting** state due to various reasons.</span></span> <span data-ttu-id="36ed5-136">Uno de los motivos comunes es que la propiedad **external** no está establecida en **True**.</span><span class="sxs-lookup"><span data-stu-id="36ed5-136">One of the common reasons is that the **external** property is not set to **true**.</span></span> <span data-ttu-id="36ed5-137">Cualquier conjunto de datos que se produce fuera del ámbito de Data Factory de Azure debe marcarse con la propiedad **external** .</span><span class="sxs-lookup"><span data-stu-id="36ed5-137">Any dataset that is produced outside the scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="36ed5-138">Esto indica que los datos son externos y no están respaldados por ninguna canalización dentro de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="36ed5-138">This property indicates that the data is external and not backed by any pipelines within the data factory.</span></span> <span data-ttu-id="36ed5-139">Los segmentos de datos se marcan con el estado **Listo** una vez que están disponibles en el almacén correspondiente.</span><span class="sxs-lookup"><span data-stu-id="36ed5-139">The data slices are marked as **Ready** once the data is available in the respective store.</span></span>

<span data-ttu-id="36ed5-140">Consulte el ejemplo siguiente para el uso de la propiedad **external** .</span><span class="sxs-lookup"><span data-stu-id="36ed5-140">See the following example for the usage of the **external** property.</span></span> <span data-ttu-id="36ed5-141">Opcionalmente, puede especificar **externalData*** al establecer external en true.</span><span class="sxs-lookup"><span data-stu-id="36ed5-141">You can optionally specify **externalData*** when you set external to true.</span></span>

<span data-ttu-id="36ed5-142">Consulte el artículo [Conjuntos de datos](data-factory-create-datasets.md) para obtener más información sobre esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="36ed5-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

<span data-ttu-id="36ed5-143">Para resolver el error, agregue la propiedad **external** y la sección **externalData** opcional a la definición de JSON de la tabla de entrada y vuelva a crear la tabla.</span><span class="sxs-lookup"><span data-stu-id="36ed5-143">To resolve the error, add the **external** property and the optional **externalData** section to the JSON definition of the input table and recreate the table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="36ed5-144">Problema: la operación de copia híbrida produce un error.</span><span class="sxs-lookup"><span data-stu-id="36ed5-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="36ed5-145">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) si quiere ver los pasos para solucionar problemas con la copia en un almacén de datos local como origen o destino usando Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="36ed5-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps to troubleshoot issues with copying to/from an on-premises data store using the Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="36ed5-146">Problema: El aprovisionamiento de HDInsight a petición produce un error</span><span class="sxs-lookup"><span data-stu-id="36ed5-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="36ed5-147">Al usar un servicio vinculado de tipo HDInsightOnDemand, debe especificar linkedServiceName que apunte a Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="36ed5-147">When using a linked service of type HDInsightOnDemand, you need to specify a linkedServiceName that points to an Azure Blob Storage.</span></span> <span data-ttu-id="36ed5-148">El servicio Data Factory usa este almacenamiento para almacenar registros y archivos auxiliares para el clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="36ed5-148">Data Factory service uses this storage to store logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="36ed5-149">A veces, el aprovisionamiento de un clúster de HDInsight a petición produce el siguiente error:</span><span class="sxs-lookup"><span data-stu-id="36ed5-149">Sometimes provisioning of an on-demand HDInsight cluster fails with the following error:</span></span>

```
Failed to create cluster. Exception: Unable to complete the cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="36ed5-150">Este error suele indicar que la ubicación de la cuenta de almacenamiento especificada en linkedServiceName no está en la misma ubicación del centro de datos que donde se produce el aprovisionamiento de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="36ed5-150">This error usually indicates that the location of the storage account specified in the linkedServiceName is not in the same data center location where the HDInsight provisioning is happening.</span></span> <span data-ttu-id="36ed5-151">Ejemplo: si la factoría de datos está en el oeste de EE. UU. y el almacenamiento de Azure en el este de EE. UU., el aprovisionamiento a petición no se realizará correctamente en el oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="36ed5-151">Example: if your data factory is in West US and the Azure storage is in East US, the on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="36ed5-152">Además, hay una segunda propiedad de JSON additionalLinkedServiceNames, donde puede se especifiquen cuentas de almacenamiento adicionales en HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="36ed5-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="36ed5-153">Las cuentas de almacenamiento vinculado adicionales deben estar en la misma ubicación que el clúster de HDInsight; de lo contrario, se producirá el mismo error.</span><span class="sxs-lookup"><span data-stu-id="36ed5-153">Those additional linked storage accounts should be in the same location as the HDInsight cluster, or it fails with the same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="36ed5-154">Problema: La actividad de .NET personalizada produce un error</span><span class="sxs-lookup"><span data-stu-id="36ed5-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="36ed5-155">Consulte [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) (Depurar una canalización con una actividad personalizada) para obtener pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="36ed5-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-to-troubleshoot"></a><span data-ttu-id="36ed5-156">Uso del Portal de Azure para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="36ed5-156">Use Azure portal to troubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="36ed5-157">Uso de hojas del Portal</span><span class="sxs-lookup"><span data-stu-id="36ed5-157">Using portal blades</span></span>
<span data-ttu-id="36ed5-158">Consulte [Supervisión de la canalización](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) para ver los pasos.</span><span class="sxs-lookup"><span data-stu-id="36ed5-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="36ed5-159">Uso de la aplicación de supervisión y administración</span><span class="sxs-lookup"><span data-stu-id="36ed5-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="36ed5-160">Consulte [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) (Supervisar y administrar canalizaciones de Data Factory con una aplicación de supervisión y administración) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="36ed5-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-to-troubleshoot"></a><span data-ttu-id="36ed5-161">Usar Azure PowerShell para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="36ed5-161">Use Azure PowerShell to troubleshoot</span></span>
### <a name="use-azure-powershell-to-troubleshoot-an-error"></a><span data-ttu-id="36ed5-162">Usar Azure PowerShell para solucionar un error</span><span class="sxs-lookup"><span data-stu-id="36ed5-162">Use Azure PowerShell to troubleshoot an error</span></span>
<span data-ttu-id="36ed5-163">Consulte [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) (Supervisar canalizaciones de Data Factory con Azure PowerShell) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="36ed5-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
