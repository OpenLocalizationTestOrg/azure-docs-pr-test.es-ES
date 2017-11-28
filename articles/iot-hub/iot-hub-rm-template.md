---
title: un centro de IoT de Azure mediante una plantilla (. NET) aaaCreate | Documentos de Microsoft
description: "¿Cómo toouse un toocreate de plantilla de Azure Resource Manager un centro de IoT con un programa de C#."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a447b40c-c728-487e-875d-db554db5adc3
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 6140deff3553701f994502fd4a60178f874e27cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="d88ce-103">Creación de un centro de IoT con una plantilla de Azure Resource Manager (.NET)</span><span class="sxs-lookup"><span data-stu-id="d88ce-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="d88ce-104">Puede usar el Administrador de recursos de Azure toocreate y administrar centros de IoT de Azure mediante programación.</span><span class="sxs-lookup"><span data-stu-id="d88ce-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="d88ce-105">Este tutorial muestra cómo toouse una toocreate de plantilla de Azure Resource Manager un centro de IoT desde un programa de C#.</span><span class="sxs-lookup"><span data-stu-id="d88ce-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="d88ce-106">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d88ce-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="d88ce-107">Este artículo tratan con modelo de implementación de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d88ce-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="d88ce-108">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="d88ce-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d88ce-109">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d88ce-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="d88ce-110">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="d88ce-110">An active Azure account.</span></span> <br/><span data-ttu-id="d88ce-111">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="d88ce-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="d88ce-112">Una [cuenta de Azure Storage][lnk-storage-account] en la que pueda guardar los archivos de plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d88ce-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="d88ce-113">[Azure PowerShell 1.0][lnk-powershell-install] o posterior.</span><span class="sxs-lookup"><span data-stu-id="d88ce-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="d88ce-114">Preparar su proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d88ce-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="d88ce-115">En Visual Studio, cree un proyecto de Visual C# escritorio clásico de Windows mediante hello **aplicación de consola (.NET Framework)** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="d88ce-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="d88ce-116">Proyecto de hello Name **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="d88ce-116">Name hello project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="d88ce-117">En el Explorador de soluciones, haga clic con el botón secundario en su proyecto y luego haga clic en **Administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d88ce-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="d88ce-118">Compruebe en el Administrador de paquetes de NuGet, **versión preliminar de inclusión**y en hello **examinar** Buscar página **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="d88ce-118">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="d88ce-119">Seleccionar paquete de hello, haga clic en **instalar**, en **revisar cambios** haga clic en **Aceptar**, a continuación, haga clic en **acepto** licencias de hello tooaccept.</span><span class="sxs-lookup"><span data-stu-id="d88ce-119">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="d88ce-120">En el Administrador de paquetes NuGet, busque **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="d88ce-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="d88ce-121">Haga clic en **instalar**, en **revisar cambios** haga clic en **Aceptar**, a continuación, haga clic en **acepto** licencia de hello tooaccept.</span><span class="sxs-lookup"><span data-stu-id="d88ce-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="d88ce-122">En Program.cs, reemplace Hola existente **con** instrucciones con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="d88ce-122">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="d88ce-123">En Program.cs, agregue Hola siguiendo las variables estáticas reemplazando los valores de marcador de posición de Hola.</span><span class="sxs-lookup"><span data-stu-id="d88ce-123">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="d88ce-124">Ha tomado nota de **ApplicationId**, **SubscriptionId**, **TenantId** y **Password** anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d88ce-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="d88ce-125">**El nombre de cuenta de almacenamiento de Azure** es nombre de Hola de hello cuenta de almacenamiento de Azure donde se almacenan los archivos de plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d88ce-125">**Your Azure Storage account name** is hello name of hello Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="d88ce-126">**Nombre del grupo de recursos** es nombre Hola Hola del grupo de recursos se usa cuando crea el centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="d88ce-126">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="d88ce-127">nombre de Hello puede ser un grupo de recursos existente o nuevo.</span><span class="sxs-lookup"><span data-stu-id="d88ce-127">hello name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="d88ce-128">**Nombre de la implementación** es un nombre para la implementación de hello, como **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="d88ce-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";
    static string storageAddress = "https://{Your storage account name}.blob.core.windows.net";
    static string rgName = "{Resource group name}";
    static string deploymentName = "{Deployment name}";
    ```

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="d88ce-129">Enviar una toocreate de plantilla un centro de IoT</span><span class="sxs-lookup"><span data-stu-id="d88ce-129">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="d88ce-130">Use un toocreate archivo plantilla y los parámetros JSON un centro de IoT en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d88ce-130">Use a JSON template and parameter file toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="d88ce-131">También puede utilizar un centro de IoT Azure Resource Manager plantilla toomake cambios tooan existente.</span><span class="sxs-lookup"><span data-stu-id="d88ce-131">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="d88ce-132">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto, haga clic en **Agregar** y luego en **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="d88ce-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="d88ce-133">Agregue un archivo JSON denominado **template.json** tooyour proyecto.</span><span class="sxs-lookup"><span data-stu-id="d88ce-133">Add a JSON file called **template.json** tooyour project.</span></span>

2. <span data-ttu-id="d88ce-134">tooadd un estándar toohello centro de IoT **UU** región, replace Hola contenido de **template.json** con hello después de la definición de recursos.</span><span class="sxs-lookup"><span data-stu-id="d88ce-134">tooadd a standard IoT hub toohello **East US** region, replace hello contents of **template.json** with hello following resource definition.</span></span> <span data-ttu-id="d88ce-135">Consulte lista actual de Hola de las regiones que admiten el centro de IoT [estado de Azure][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="d88ce-135">For hello current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

3. <span data-ttu-id="d88ce-136">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto, haga clic en **Agregar** y luego en **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="d88ce-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="d88ce-137">Agregue un archivo JSON denominado **parameters.json** tooyour proyecto.</span><span class="sxs-lookup"><span data-stu-id="d88ce-137">Add a JSON file called **parameters.json** tooyour project.</span></span>

4. <span data-ttu-id="d88ce-138">Reemplace el contenido de Hola de **parameters.json** con hello siguiendo la información de parámetros que se establece como un nombre para el nuevo centro de IoT hello **{sus iniciales} mynewiothub**.</span><span class="sxs-lookup"><span data-stu-id="d88ce-138">Replace hello contents of **parameters.json** with hello following parameter information that sets a name for hello new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="d88ce-139">nombre del centro de IoT Hola debe ser único globalmente, por lo que debe incluir su nombre o iniciales:</span><span class="sxs-lookup"><span data-stu-id="d88ce-139">hello IoT hub name must be globally unique so it should include your name or initials:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": { "value": "mynewiothub" }
      }
    }
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

5. <span data-ttu-id="d88ce-140">En **Explorador de servidores**, conectar tooyour suscripción de Azure, y en el almacenamiento de Azure cuenta crear un contenedor denominado **plantillas**.</span><span class="sxs-lookup"><span data-stu-id="d88ce-140">In **Server Explorer**, connect tooyour Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="d88ce-141">Hola **propiedades** panel, conjunto hello **acceso de lectura público** permisos para hello **plantillas** contenedor demasiado**Blob**.</span><span class="sxs-lookup"><span data-stu-id="d88ce-141">In hello **Properties** panel, set hello **Public Read Access** permissions for hello **templates** container too**Blob**.</span></span>

6. <span data-ttu-id="d88ce-142">En **Explorador de servidores**, haga doble clic en hello **plantillas** contenedor y, a continuación, haga clic en **ver contenedor de Blob**.</span><span class="sxs-lookup"><span data-stu-id="d88ce-142">In **Server Explorer**, right-click on hello **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="d88ce-143">Haga clic en hello **cargar Blob** botón, seleccione dos archivos de hello, **parameters.json** y **templates.json**y, a continuación, haga clic en **abiertos** Hola tooupload JSON archivos toohello **plantillas** contenedor.</span><span class="sxs-lookup"><span data-stu-id="d88ce-143">Click hello **Upload Blob** button, select hello two files, **parameters.json** and **templates.json**, and then click **Open** tooupload hello JSON files toohello **templates** container.</span></span> <span data-ttu-id="d88ce-144">direcciones URL de Hola de blobs de Hola que contienen datos JSON Hola son:</span><span class="sxs-lookup"><span data-stu-id="d88ce-144">hello URLs of hello blobs containing hello JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="d88ce-145">Agregue Hola siguiendo el método tooProgram.cs:</span><span class="sxs-lookup"><span data-stu-id="d88ce-145">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="d88ce-146">Agregar Hola después código toohello **CreateIoTHub** método toosubmit Hola plantilla y parámetros archivos toohello Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="d88ce-146">Add hello following code toohello **CreateIoTHub** method toosubmit hello template and parameter files toohello Azure Resource Manager:</span></span>

    ```csharp
    var createResponse = client.Deployments.CreateOrUpdate(
        rgName,
        deploymentName,
        new Deployment()
        {
          Properties = new DeploymentProperties
          {
            Mode = DeploymentMode.Incremental,
            TemplateLink = new TemplateLink
            {
              Uri = storageAddress + "/templates/template.json"
            },
            ParametersLink = new ParametersLink
            {
              Uri = storageAddress + "/templates/parameters.json"
            }
          }
        });
    ```

9. <span data-ttu-id="d88ce-147">Agregar Hola después código toohello **CreateIoTHub** método que muestra el estado de Hola y claves de hello para el nuevo centro de IoT hello:</span><span class="sxs-lookup"><span data-stu-id="d88ce-147">Add hello following code toohello **CreateIoTHub** method that displays hello status and hello keys for hello new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="d88ce-148">Aplicación hello completo y ejecución</span><span class="sxs-lookup"><span data-stu-id="d88ce-148">Complete and run hello application</span></span>

<span data-ttu-id="d88ce-149">Ahora puede completar aplicación hello mediante la llamada hello **CreateIoTHub** método antes de compilarla y ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="d88ce-149">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="d88ce-150">Agregar Hola siguiente código toohello final de hello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="d88ce-150">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="d88ce-151">Haga clic en **Compilar** y luego en **Compilar solución**.</span><span class="sxs-lookup"><span data-stu-id="d88ce-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="d88ce-152">Corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="d88ce-152">Correct any errors.</span></span>

3. <span data-ttu-id="d88ce-153">Haga clic en **depurar** y, a continuación, **Iniciar depuración** aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="d88ce-153">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="d88ce-154">Puede tardar varios minutos para hello toorun de implementación.</span><span class="sxs-lookup"><span data-stu-id="d88ce-154">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="d88ce-155">tooverify agregado la aplicación Hola nuevo centro de IoT, visite hello [portal de Azure] [ lnk-azure-portal] y ver la lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="d88ce-155">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="d88ce-156">O bien, usar hello **Get-AzureRmResource** cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d88ce-156">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="d88ce-157">Esta aplicación de ejemplo agrega un centro de IoT estándar S1 por el que se le cobrará.</span><span class="sxs-lookup"><span data-stu-id="d88ce-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="d88ce-158">Puede eliminar el centro de IoT de Hola a través de hello [portal de Azure] [ lnk-azure-portal] o mediante el uso de hello **Remove-AzureRmResource** cmdlet de PowerShell cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="d88ce-158">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d88ce-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d88ce-159">Next steps</span></span>
<span data-ttu-id="d88ce-160">Ahora que ha implementado un centro de IoT utilizando una plantilla de Azure Resource Manager con un programa de C#, puede que desee tooexplore adicional:</span><span class="sxs-lookup"><span data-stu-id="d88ce-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want tooexplore further:</span></span>

* <span data-ttu-id="d88ce-161">Obtenga información sobre las capacidades de Hola de hello [API de REST de proveedor de recursos de centro de IoT][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="d88ce-161">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="d88ce-162">Lectura [Introducción al administrador de recursos de Azure] [ lnk-azure-rm-overview] toolearn más información acerca de las capacidades de hello del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d88ce-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="d88ce-163">toolearn más sobre el desarrollo de centro de IoT, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="d88ce-163">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="d88ce-164">[Introducción tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="d88ce-164">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="d88ce-165">[SDK de IoT de Azure][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="d88ce-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="d88ce-166">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="d88ce-166">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d88ce-167">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="d88ce-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-storage-account]:../storage/common/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
