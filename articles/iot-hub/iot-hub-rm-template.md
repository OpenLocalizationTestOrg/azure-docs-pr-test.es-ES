---
title: "Creación de un centro de IoT de Azure mediante una plantilla (.NET) | Microsoft Docs"
description: "Describe cómo usar una plantilla de Azure Resource Manager para crear un centro de IoT con el programa C#."
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
ms.openlocfilehash: 0f197a28e0c51b06d0b47a03c29fe1fde0c6b78d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="9ab22-103">Creación de un centro de IoT con una plantilla de Azure Resource Manager (.NET)</span><span class="sxs-lookup"><span data-stu-id="9ab22-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="9ab22-104">Puede usar Azure Resource Manager para crear y administrar los centros de IoT de Azure mediante programación.</span><span class="sxs-lookup"><span data-stu-id="9ab22-104">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="9ab22-105">En este tutorial se muestra cómo usar una plantilla de Azure Resource Manager para crear un IoT Hub desde un programa de C#.</span><span class="sxs-lookup"><span data-stu-id="9ab22-105">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="9ab22-106">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9ab22-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="9ab22-107">Este artículo trata sobre el uso del modelo de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9ab22-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="9ab22-108">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9ab22-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="9ab22-109">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9ab22-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="9ab22-110">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="9ab22-110">An active Azure account.</span></span> <br/><span data-ttu-id="9ab22-111">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="9ab22-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="9ab22-112">Una [cuenta de Azure Storage][lnk-storage-account] en la que pueda guardar los archivos de plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9ab22-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="9ab22-113">[Azure PowerShell 1.0][lnk-powershell-install] o posterior.</span><span class="sxs-lookup"><span data-stu-id="9ab22-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="9ab22-114">Preparar su proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9ab22-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="9ab22-115">En Visual Studio, cree un proyecto de escritorio clásico de Windows de Visual C# usando la plantilla de proyecto **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="9ab22-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="9ab22-116">Asigne al proyecto el nombre **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="9ab22-116">Name the project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="9ab22-117">En el Explorador de soluciones, haga clic con el botón secundario en su proyecto y luego haga clic en **Administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9ab22-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="9ab22-118">En el Administrador de paquetes NuGet, active **Incluir versión preliminar** y en la página **Examinar** busque **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="9ab22-118">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="9ab22-119">Seleccione el paquete, haga clic en **Instalar**, en **Revisar cambios**, haga clic en **Aceptar** y, luego, en **Acepto** para aceptar las licencias.</span><span class="sxs-lookup"><span data-stu-id="9ab22-119">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>

4. <span data-ttu-id="9ab22-120">En el Administrador de paquetes NuGet, busque **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="9ab22-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="9ab22-121">Haga clic en **Instalar**, en **Revisar cambios**, haga clic en **Aceptar** y, luego, en **Acepto** para aceptar la licencia.</span><span class="sxs-lookup"><span data-stu-id="9ab22-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>

5. <span data-ttu-id="9ab22-122">En Program.cs, reemplace las instrucciones **using** existentes por el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="9ab22-122">In Program.cs, replace the existing **using** statements with the following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="9ab22-123">En Program.cs, agregue las siguientes variables estáticas reemplazando los valores de marcador de posición.</span><span class="sxs-lookup"><span data-stu-id="9ab22-123">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="9ab22-124">Ha tomado nota de **ApplicationId**, **SubscriptionId**, **TenantId** y **Password** anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9ab22-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="9ab22-125">El **nombre de la cuenta de Azure Storage** es el nombre de la cuenta de Azure Storage en donde almacenará los archivos de la plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9ab22-125">**Your Azure Storage account name** is the name of the Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="9ab22-126">El **nombre de grupo de recursos** es el nombre del grupo de recursos que usará al crear IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9ab22-126">**Resource group name** is the name of the resource group you use when you create the IoT hub.</span></span> <span data-ttu-id="9ab22-127">El nombre puede ser un grupo de recursos ya existente u otro nuevo.</span><span class="sxs-lookup"><span data-stu-id="9ab22-127">The name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="9ab22-128">El **Nombre de la implementación** es un nombre para la implementación, como **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="9ab22-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>

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

## <a name="submit-a-template-to-create-an-iot-hub"></a><span data-ttu-id="9ab22-129">Enviar una plantilla para crear un centro de IoT</span><span class="sxs-lookup"><span data-stu-id="9ab22-129">Submit a template to create an IoT hub</span></span>

<span data-ttu-id="9ab22-130">Use una plantilla de JSON y un archivo de parámetro para crear un centro de IoT en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9ab22-130">Use a JSON template and parameter file to create an IoT hub in your resource group.</span></span> <span data-ttu-id="9ab22-131">También puede usar una plantilla de Azure Resource Manager para realizar cambios en un IoT Hub existente.</span><span class="sxs-lookup"><span data-stu-id="9ab22-131">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="9ab22-132">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto, haga clic en **Agregar** y luego en **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="9ab22-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="9ab22-133">Agregue un archivo JSON denominado **template.json** a su proyecto.</span><span class="sxs-lookup"><span data-stu-id="9ab22-133">Add a JSON file called **template.json** to your project.</span></span>

2. <span data-ttu-id="9ab22-134">Reemplace el contenido de **template.json** por la siguiente definición de recursos para agregar un centro de IoT estándar a la región **este de EE. UU.**</span><span class="sxs-lookup"><span data-stu-id="9ab22-134">To add a standard IoT hub to the **East US** region, replace the contents of **template.json** with the following resource definition.</span></span> <span data-ttu-id="9ab22-135">Para ver una lista actualizada de las ubicaciones admitidas en IoT Hub, consulte [Estado de Azure][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="9ab22-135">For the current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

3. <span data-ttu-id="9ab22-136">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto, haga clic en **Agregar** y luego en **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="9ab22-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="9ab22-137">Agregue un archivo JSON denominado **parameters.json** a su proyecto.</span><span class="sxs-lookup"><span data-stu-id="9ab22-137">Add a JSON file called **parameters.json** to your project.</span></span>

4. <span data-ttu-id="9ab22-138">Reemplace el contenido de **parameters.json** por la siguiente información de parámetro que establece el nombre del nuevo IoT Hub, como **{sus iniciales}miNuevoCentroDeIoT**.</span><span class="sxs-lookup"><span data-stu-id="9ab22-138">Replace the contents of **parameters.json** with the following parameter information that sets a name for the new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="9ab22-139">El nombre del centro de IoT debe ser único en todo el mundo, por lo que debe incluir su nombre o sus iniciales:</span><span class="sxs-lookup"><span data-stu-id="9ab22-139">The IoT hub name must be globally unique so it should include your name or initials:</span></span>

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

5. <span data-ttu-id="9ab22-140">En el **Explorador de servidores**, conéctese a su suscripción de Azure y, en su cuenta de Azure Storage, cree un contenedor denominado **plantillas**.</span><span class="sxs-lookup"><span data-stu-id="9ab22-140">In **Server Explorer**, connect to your Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="9ab22-141">En el panel **Propiedades**, establezca los permisos de **Acceso de lectura público** para el contenedor de **plantillas** en **Blob**.</span><span class="sxs-lookup"><span data-stu-id="9ab22-141">In the **Properties** panel, set the **Public Read Access** permissions for the **templates** container to **Blob**.</span></span>

6. <span data-ttu-id="9ab22-142">En el **Explorador de servidores**, haga clic con el botón derecho en el contenedor **plantillas** y luego haga clic en **Ver contenedor de blob**.</span><span class="sxs-lookup"><span data-stu-id="9ab22-142">In **Server Explorer**, right-click on the **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="9ab22-143">Haga clic en el botón **Cargar blob**, seleccione los dos archivos, **parameters.json** y **templates.json**, y luego haga clic en **Abrir** para cargar los archivos JSON en el contenedor de **plantillas**.</span><span class="sxs-lookup"><span data-stu-id="9ab22-143">Click the **Upload Blob** button, select the two files, **parameters.json** and **templates.json**, and then click **Open** to upload the JSON files to the **templates** container.</span></span> <span data-ttu-id="9ab22-144">Las direcciones URL de los blobs que contienen los datos de JSON son:</span><span class="sxs-lookup"><span data-stu-id="9ab22-144">The URLs of the blobs containing the JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="9ab22-145">Agregue el método siguiente a Program.cs:</span><span class="sxs-lookup"><span data-stu-id="9ab22-145">Add the following method to Program.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="9ab22-146">Agregue el código siguiente al método **CreateIoTHub** para enviar los archivos de plantilla y parámetro a Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="9ab22-146">Add the following code to the **CreateIoTHub** method to submit the template and parameter files to the Azure Resource Manager:</span></span>

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

9. <span data-ttu-id="9ab22-147">Agregue el código siguiente al método **CreateIoTHub** que muestra el estado y las claves del nuevo centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="9ab22-147">Add the following code to the **CreateIoTHub** method that displays the status and the keys for the new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed to create iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="9ab22-148">Completar y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="9ab22-148">Complete and run the application</span></span>

<span data-ttu-id="9ab22-149">Ahora puede completar la aplicación llamando al método **CreateIoTHub** antes de compilarla y ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="9ab22-149">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="9ab22-150">Agregue el siguiente código al final del método **Main** :</span><span class="sxs-lookup"><span data-stu-id="9ab22-150">Add the following code to the end of the **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="9ab22-151">Haga clic en **Compilar** y luego en **Compilar solución**.</span><span class="sxs-lookup"><span data-stu-id="9ab22-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="9ab22-152">Corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="9ab22-152">Correct any errors.</span></span>

3. <span data-ttu-id="9ab22-153">Haga clic en **Depurar** y luego en **Iniciar depuración** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9ab22-153">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="9ab22-154">La ejecución de la implementación puede tardar varios minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="9ab22-154">It may take several minutes for the deployment to run.</span></span>

4. <span data-ttu-id="9ab22-155">Para comprobar que la aplicación ha agregado el nuevo centro de IoT, visite [Azure Portal][lnk-azure-portal] y vea la lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="9ab22-155">To verify your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="9ab22-156">Como alternativa, use el cmdlet de PowerShell **Get-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="9ab22-156">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="9ab22-157">Esta aplicación de ejemplo agrega un centro de IoT estándar S1 por el que se le cobrará.</span><span class="sxs-lookup"><span data-stu-id="9ab22-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="9ab22-158">Cuando haya terminado, podrá eliminar el centro de IoT Hub a través de [Azure Portal][lnk-azure-portal] o mediante el cmdlet **Remove-AzureRmResource** de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ab22-158">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ab22-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9ab22-159">Next steps</span></span>
<span data-ttu-id="9ab22-160">Ahora que ha implementado un centro de IoT mediante una plantilla de Azure Resource Manager con un programa de C#, quizá desee seguir explorando:</span><span class="sxs-lookup"><span data-stu-id="9ab22-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want to explore further:</span></span>

* <span data-ttu-id="9ab22-161">Consulte las funcionalidades de la [API de REST del proveedor de recursos de IoT Hub][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="9ab22-161">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="9ab22-162">Para más información sobre las funcionalidades de Azure Resource Manager, consulte [Información general de Azure Resource Manager][lnk-azure-rm-overview].</span><span class="sxs-lookup"><span data-stu-id="9ab22-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="9ab22-163">Para obtener más información sobre cómo desarrollar para IoT Hub, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="9ab22-163">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="9ab22-164">[Introducción al SDK de C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="9ab22-164">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="9ab22-165">[SDK de IoT de Azure][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="9ab22-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="9ab22-166">Para explorar aún más las funcionalidades de IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="9ab22-166">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="9ab22-167">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="9ab22-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
