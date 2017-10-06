---
title: problemas de aaaTroubleshoot Data Factory de Azure
description: "Obtenga información acerca de cómo tootroubleshoot problemas con el uso de Data Factory de Azure."
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
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="f1cd6-103">Solución de problemas de la factoría de datos</span><span class="sxs-lookup"><span data-stu-id="f1cd6-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="f1cd6-104">En este artículo se proporcionan consejos para solución de problemas surgidos al usar Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="f1cd6-105">En este artículo no enumera todos los posibles problemas de hello cuando se usa el servicio de hello, pero se tratan algunos problemas y sugerencias de solución de problemas generales.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-105">This article does not list all hello possible issues when using hello service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="f1cd6-106">Sugerencias de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="f1cd6-106">Troubleshooting tips</span></span>
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a><span data-ttu-id="f1cd6-107">Error: suscripción de hello no está registrado toouse de espacio de nombres 'Microsoft.DataFactory'</span><span class="sxs-lookup"><span data-stu-id="f1cd6-107">Error: hello subscription is not registered toouse namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="f1cd6-108">Si recibe este error, no se registró el proveedor de recursos de hello Data Factory de Azure en su equipo.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-108">If you receive this error, hello Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="f1cd6-109">Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="f1cd6-109">Do hello following:</span></span>

1. <span data-ttu-id="f1cd6-110">Inicie Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="f1cd6-111">Inicie sesión en tooyour cuenta de Azure mediante el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-111">Log in tooyour Azure account using hello following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="f1cd6-112">Ejecute hello después de proveedor del comando tooregister Hola Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-112">Run hello following command tooregister hello Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="f1cd6-113">Problema: error no autorizado al ejecutar un cmdlet de Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="f1cd6-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="f1cd6-114">Probablemente no utilizas Hola derecha cuenta de Azure o suscripción con hello Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-114">You are probably not using hello right Azure account or subscription with hello Azure PowerShell.</span></span> <span data-ttu-id="f1cd6-115">Usar hello después cmdlets tooselect Hola derecha toouse de cuenta y suscripción de Azure con hello Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-115">Use hello following cmdlets tooselect hello right Azure account and subscription toouse with hello Azure PowerShell.</span></span>

1. <span data-ttu-id="f1cd6-116">Inicio de sesión-AzureRmAccount - Id. de usuario de uso hello y una contraseña</span><span class="sxs-lookup"><span data-stu-id="f1cd6-116">Login-AzureRmAccount - Use hello right user ID and password</span></span>
2. <span data-ttu-id="f1cd6-117">Get-AzureRmSubscription - vista todos Hola suscripciones de cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-117">Get-AzureRmSubscription - View all hello subscriptions for hello account.</span></span>
3. <span data-ttu-id="f1cd6-118">Seleccione AzureRmSubscription &lt;nombre de la suscripción&gt; -seleccione Hola derecho suscripción.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select hello right subscription.</span></span> <span data-ttu-id="f1cd6-119">Use Hola mismo que usar toocreate una factoría de datos en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-119">Use hello same one you use toocreate a data factory on hello Azure portal.</span></span>

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="f1cd6-120">Problema: No toolaunch instalación de Express de puerta de enlace de datos de administración del portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f1cd6-120">Problem: Fail toolaunch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="f1cd6-121">el programa de instalación rápida de Hola para hello Data Management Gateway requiere Internet Explorer o un explorador de web compatible con Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-121">hello Express setup for hello Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="f1cd6-122">Si el programa de instalación de Express de Hola no toostart, siga uno de los procedimientos de hello:</span><span class="sxs-lookup"><span data-stu-id="f1cd6-122">If hello Express Setup fails toostart, do one of hello following:</span></span>

* <span data-ttu-id="f1cd6-123">Utilice Internet Explorer o un explorador web compatible con Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="f1cd6-124">Si usas Chrome, vaya toohello [almacén web de Chrome](https://chrome.google.com/webstore/), buscar con la palabra clave "ClickOnce", elija una de las extensiones de ClickOnce hello e instalarlo.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-124">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="f1cd6-125">Hola mismo para Firefox (complemento de instalación).</span><span class="sxs-lookup"><span data-stu-id="f1cd6-125">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="f1cd6-126">Haga clic en el botón de menú Abrir en la barra de herramientas de hello (tres líneas horizontales en la esquina superior derecha de hello), haga clic en los complementos, buscar con la palabra clave "ClickOnce", elija una de las extensiones de ClickOnce hello e instalarlo.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-126">Click Open Menu button on hello toolbar (three horizontal lines in hello top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="f1cd6-127">Hola de uso **el programa de instalación Manual** vínculo se muestra en hello misma hoja en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-127">Use hello **Manual Setup** link shown on hello same blade in hello portal.</span></span> <span data-ttu-id="f1cd6-128">Use este archivo de instalación de toodownload de enfoque y ejecutarlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-128">You use this approach toodownload installation file and run it manually.</span></span> <span data-ttu-id="f1cd6-129">Tras instalación hello es correcta, se mostrará el cuadro de diálogo de configuración de puerta de enlace de administración de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-129">After hello installation is successful, you see hello Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="f1cd6-130">Hola copia **clave** de pantalla de portal de bienvenida y utilizar en hello configuration manager toomanually registrar puerta de enlace de hello con servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-130">Copy hello **key** from hello portal screen and use it in hello configuration manager toomanually register hello gateway with hello service.</span></span>  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a><span data-ttu-id="f1cd6-131">Problema: No tooconnect tooon local SQL Server</span><span class="sxs-lookup"><span data-stu-id="f1cd6-131">Problem: Fail tooconnect tooon-premises SQL Server</span></span>
<span data-ttu-id="f1cd6-132">Iniciar **Administrador de configuración de Data Management Gateway** Hola máquina de puerta de enlace y usar hello **solución de problemas** ficha tootest Hola conexión tooSQL Server de la máquina de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-132">Launch **Data Management Gateway Configuration Manager** on hello gateway machine and use hello **Troubleshooting** tab tootest hello connection tooSQL Server from hello gateway machine.</span></span> <span data-ttu-id="f1cd6-133">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="f1cd6-134">Problema: Los segmentos de entrada están en el estado En espera de forma permanente.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="f1cd6-135">segmentos de Hello pudieron estar en **espera** estado debido a motivos de toovarious.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-135">hello slices could be in **Waiting** state due toovarious reasons.</span></span> <span data-ttu-id="f1cd6-136">Uno de los motivos comunes de hello es ese hello **externo** propiedad no se establece demasiado**true**.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-136">One of hello common reasons is that hello **external** property is not set too**true**.</span></span> <span data-ttu-id="f1cd6-137">Cualquier conjunto de datos que es ámbito producidos Hola fuera de Data Factory de Azure debe marcarse con **externo** propiedad.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-137">Any dataset that is produced outside hello scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="f1cd6-138">Esta propiedad indica que Hola datos externos y no con el respaldo de las canalizaciones de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-138">This property indicates that hello data is external and not backed by any pipelines within hello data factory.</span></span> <span data-ttu-id="f1cd6-139">segmentos de datos de Hola se marcan como **listo** una vez Hola datos están disponibles en tienda respectiva Hola.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-139">hello data slices are marked as **Ready** once hello data is available in hello respective store.</span></span>

<span data-ttu-id="f1cd6-140">Vea Hola siguiente ejemplo para el uso de Hola de hello **externo** propiedad.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-140">See hello following example for hello usage of hello **external** property.</span></span> <span data-ttu-id="f1cd6-141">Opcionalmente, puede especificar **externalData*** al establecer tootrue externo.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-141">You can optionally specify **externalData*** when you set external tootrue.</span></span>

<span data-ttu-id="f1cd6-142">Consulte el artículo [Conjuntos de datos](data-factory-create-datasets.md) para obtener más información sobre esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

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

<span data-ttu-id="f1cd6-143">tooresolve Hola error, agregue hello **externo** hello opcional y la propiedad **externalData** sección toohello definición de JSON de tabla de entrada de Hola y vuelva a crear tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-143">tooresolve hello error, add hello **external** property and hello optional **externalData** section toohello JSON definition of hello input table and recreate hello table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="f1cd6-144">Problema: la operación de copia híbrida produce un error.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="f1cd6-145">Vea [solucionar problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para pasos tootroubleshoot problemas con la copia de un dato local almacenan utilizando Hola Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps tootroubleshoot issues with copying to/from an on-premises data store using hello Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="f1cd6-146">Problema: El aprovisionamiento de HDInsight a petición produce un error</span><span class="sxs-lookup"><span data-stu-id="f1cd6-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="f1cd6-147">Cuando se utiliza un servicio vinculado de tipo HDInsightOnDemand, deberá toospecify un linkedServiceName que señala tooan almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-147">When using a linked service of type HDInsightOnDemand, you need toospecify a linkedServiceName that points tooan Azure Blob Storage.</span></span> <span data-ttu-id="f1cd6-148">Servicio de factoría de datos usa este almacenamiento toostore registros y archivos auxiliares para el clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-148">Data Factory service uses this storage toostore logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="f1cd6-149">Se produce un error en ocasiones, el aprovisionamiento de un clúster de HDInsight a petición con hello siguiente error:</span><span class="sxs-lookup"><span data-stu-id="f1cd6-149">Sometimes provisioning of an on-demand HDInsight cluster fails with hello following error:</span></span>

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="f1cd6-150">Este error suele indicar que no es ubicación Hola de cuenta de almacenamiento de hello especificada en hello linkedServiceName Hola ubicación donde sucede el aprovisionamiento de hello HDInsight del centro de datos mismas.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-150">This error usually indicates that hello location of hello storage account specified in hello linkedServiceName is not in hello same data center location where hello HDInsight provisioning is happening.</span></span> <span data-ttu-id="f1cd6-151">Ejemplo: si su factoría de datos es zona horaria del Pacífico occidental y Hola almacenamiento de Azure está en UU, Hola a petición se produce un error aprovisionamiento zona horaria del Pacífico occidental.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-151">Example: if your data factory is in West US and hello Azure storage is in East US, hello on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="f1cd6-152">Además, hay una segunda propiedad de JSON additionalLinkedServiceNames, donde puede se especifiquen cuentas de almacenamiento adicionales en HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="f1cd6-153">Las cuentas de almacenamiento vinculado adicional deben ser Hola se produce un error en la misma ubicación que el clúster de HDInsight de hello, o bien con hello mismo error.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-153">Those additional linked storage accounts should be in hello same location as hello HDInsight cluster, or it fails with hello same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="f1cd6-154">Problema: La actividad de .NET personalizada produce un error</span><span class="sxs-lookup"><span data-stu-id="f1cd6-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="f1cd6-155">Consulte [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) (Depurar una canalización con una actividad personalizada) para obtener pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-tootroubleshoot"></a><span data-ttu-id="f1cd6-156">Usar tootroubleshoot de portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f1cd6-156">Use Azure portal tootroubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="f1cd6-157">Uso de hojas del Portal</span><span class="sxs-lookup"><span data-stu-id="f1cd6-157">Using portal blades</span></span>
<span data-ttu-id="f1cd6-158">Consulte [Supervisión de la canalización](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) para ver los pasos.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="f1cd6-159">Uso de la aplicación de supervisión y administración</span><span class="sxs-lookup"><span data-stu-id="f1cd6-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="f1cd6-160">Consulte [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) (Supervisar y administrar canalizaciones de Data Factory con una aplicación de supervisión y administración) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-tootroubleshoot"></a><span data-ttu-id="f1cd6-161">Usar tootroubleshoot de PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="f1cd6-161">Use Azure PowerShell tootroubleshoot</span></span>
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a><span data-ttu-id="f1cd6-162">Usar PowerShell de Azure tootroubleshoot un error</span><span class="sxs-lookup"><span data-stu-id="f1cd6-162">Use Azure PowerShell tootroubleshoot an error</span></span>
<span data-ttu-id="f1cd6-163">Consulte [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) (Supervisar canalizaciones de Data Factory con Azure PowerShell) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="f1cd6-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

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
