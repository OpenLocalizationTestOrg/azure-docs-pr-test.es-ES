---
title: "Creación de un centro de IoT de Azure mediante la API de REST del proveedor de recursos | Microsoft Docs"
description: "Describe cómo usar la API de REST del proveedor de recursos para crear un centro de IoT."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 52814ee5-bc10-4abe-9eb2-f8973096c2d8
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e443259507aacbefca141be4c9c1688ab19bf6ec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-resource-provider-rest-api-net"></a><span data-ttu-id="97d99-103">Creación de un centro de IoT mediante la API de REST del proveedor de recursos (.NET)</span><span class="sxs-lookup"><span data-stu-id="97d99-103">Create an IoT hub using the resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="97d99-104">Puede usar la [API de REST del proveedor de recursos de IoT Hub][lnk-rest-api] para crear y administrar los centros de IoT de Azure mediante programación.</span><span class="sxs-lookup"><span data-stu-id="97d99-104">You can use the [IoT Hub resource provider REST API][lnk-rest-api] to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="97d99-105">En este tutorial se muestra cómo usar la API de REST del proveedor de recursos de IoT Hub para crear un IoT Hub desde un programa de C#.</span><span class="sxs-lookup"><span data-stu-id="97d99-105">This tutorial shows you how to use the IoT Hub resource provider REST API to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="97d99-106">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="97d99-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="97d99-107">Este artículo trata sobre el uso del modelo de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="97d99-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="97d99-108">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="97d99-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="97d99-109">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="97d99-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="97d99-110">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="97d99-110">An active Azure account.</span></span> <br/><span data-ttu-id="97d99-111">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="97d99-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="97d99-112">[Azure PowerShell 1.0][lnk-powershell-install] o posterior.</span><span class="sxs-lookup"><span data-stu-id="97d99-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="97d99-113">Preparar su proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="97d99-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="97d99-114">En Visual Studio, cree un proyecto de escritorio clásico de Windows de Visual C# usando la plantilla de proyecto **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="97d99-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="97d99-115">Asigne al proyecto el nombre **CreateIoTHubREST**.</span><span class="sxs-lookup"><span data-stu-id="97d99-115">Name the project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="97d99-116">En el Explorador de soluciones, haga clic con el botón secundario en su proyecto y luego haga clic en **Administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="97d99-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="97d99-117">En el Administrador de paquetes NuGet, active **Incluir versión preliminar** y en la página **Examinar** busque **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="97d99-117">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="97d99-118">Seleccione el paquete, haga clic en **Instalar**, en **Revisar cambios**, haga clic en **Aceptar** y, luego, en **Acepto** para aceptar las licencias.</span><span class="sxs-lookup"><span data-stu-id="97d99-118">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>

4. <span data-ttu-id="97d99-119">En el Administrador de paquetes NuGet, busque **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="97d99-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="97d99-120">Haga clic en **Instalar**, en **Revisar cambios**, haga clic en **Aceptar** y, luego, en **Acepto** para aceptar la licencia.</span><span class="sxs-lookup"><span data-stu-id="97d99-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>

5. <span data-ttu-id="97d99-121">En Program.cs, reemplace las instrucciones **using** existentes por el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="97d99-121">In Program.cs, replace the existing **using** statements with the following code:</span></span>

    ```csharp
    using System;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Text;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    using Microsoft.Rest;
    using System.Linq;
    using System.Threading;
    ```

6. <span data-ttu-id="97d99-122">En Program.cs, agregue las siguientes variables estáticas reemplazando los valores de marcador de posición.</span><span class="sxs-lookup"><span data-stu-id="97d99-122">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="97d99-123">Ha tomado nota de **ApplicationId**, **SubscriptionId**, **TenantId** y **Password** anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="97d99-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="97d99-124">El **nombre de grupo de recursos** es el nombre del grupo de recursos que usará al crear IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="97d99-124">**Resource group name** is the name of the resource group you use when you create the IoT hub.</span></span> <span data-ttu-id="97d99-125">Puede ser un grupo de recursos ya existente u otro nuevo.</span><span class="sxs-lookup"><span data-stu-id="97d99-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="97d99-126">**Nombre de IoT Hub** es el nombre de la instancia de IoT Hub que creó como, por ejemplo, **MyIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="97d99-126">**IoT Hub name** is the name of the IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="97d99-127">El nombre de su instancia de IoT Hub debe única globalmente.</span><span class="sxs-lookup"><span data-stu-id="97d99-127">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="97d99-128">El **Nombre de la implementación** es un nombre para la implementación, como **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="97d99-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";

    static string rgName = "{Resource group name}";
    static string iotHubName = "{IoT Hub name including your initials}";
    ```
[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="use-the-resource-provider-rest-api-to-create-an-iot-hub"></a><span data-ttu-id="97d99-129">Uso de la API de REST del proveedor de recursos para crear un centro de IoT</span><span class="sxs-lookup"><span data-stu-id="97d99-129">Use the resource provider REST API to create an IoT hub</span></span>

<span data-ttu-id="97d99-130">Utilice la [API de REST del proveedor de recursos de IoT Hub][lnk-rest-api] para crear un centro de IoT en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="97d99-130">Use the [IoT Hub resource provider REST API][lnk-rest-api] to create an IoT hub in your resource group.</span></span> <span data-ttu-id="97d99-131">También puede utilizar la API de REST del proveedor de recursos para efectuar cambios en un centro de IoT existente.</span><span class="sxs-lookup"><span data-stu-id="97d99-131">You can also use the resource provider REST API to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="97d99-132">Agregue el método siguiente a Program.cs:</span><span class="sxs-lookup"><span data-stu-id="97d99-132">Add the following method to Program.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="97d99-133">Agregue el código siguiente al método **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="97d99-133">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="97d99-134">Este código crea un objeto **HttpClient** con el token de autenticación de los encabezados:</span><span class="sxs-lookup"><span data-stu-id="97d99-134">This code creates an **HttpClient** object with the authentication token in the headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="97d99-135">Agregue el código siguiente al método **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="97d99-135">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="97d99-136">Este código describe el centro de IoT que se creará y genera una representación JSON.</span><span class="sxs-lookup"><span data-stu-id="97d99-136">This code describes the IoT hub to create and generates a JSON representation.</span></span> <span data-ttu-id="97d99-137">Para ver la lista actualizada de las ubicaciones admitidas por IoT Hub, consulte [Estado de Azure][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="97d99-137">For the current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

    ```csharp
    var description = new
    {
      name = iotHubName,
      location = "East US",
      sku = new
      {
        name = "S1",
        tier = "Standard",
        capacity = 1
      }
    };

    var json = JsonConvert.SerializeObject(description, Formatting.Indented);
    ```

4. <span data-ttu-id="97d99-138">Agregue el código siguiente al método **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="97d99-138">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="97d99-139">Este código envía la solicitud REST a Azure.</span><span class="sxs-lookup"><span data-stu-id="97d99-139">This code submits the REST request to Azure.</span></span> <span data-ttu-id="97d99-140">El código comprueba la respuesta y recupera la URL con la que se puede supervisar el estado de la tarea de implementación:</span><span class="sxs-lookup"><span data-stu-id="97d99-140">The code then checks the response and retrieves the URL you can use to monitor the state of the deployment task:</span></span>

    ```csharp
    var content = new StringContent(JsonConvert.SerializeObject(description), Encoding.UTF8, "application/json");
    var requestUri = string.Format("https://management.azure.com/subscriptions/{0}/resourcegroups/{1}/providers/Microsoft.devices/IotHubs/{2}?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var result = client.PutAsync(requestUri, content).Result;

    if (!result.IsSuccessStatusCode)
    {
      Console.WriteLine("Failed {0}", result.Content.ReadAsStringAsync().Result);
      return;
    }

    var asyncStatusUri = result.Headers.GetValues("Azure-AsyncOperation").First();
    ```

5. <span data-ttu-id="97d99-141">Agregue el siguiente código al final del método **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="97d99-141">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="97d99-142">Este código usa la dirección **asyncStatusUri** recuperada del paso anterior para esperar a que finalice la implementación:</span><span class="sxs-lookup"><span data-stu-id="97d99-142">This code uses the **asyncStatusUri** address retrieved in the previous step to wait for the deployment to complete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="97d99-143">Agregue el siguiente código al final del método **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="97d99-143">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="97d99-144">Este código recupera las claves del centro de IoT que se crea y las imprime en la consola:</span><span class="sxs-lookup"><span data-stu-id="97d99-144">This code retrieves the keys of the IoT hub you created and prints them to the console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="97d99-145">Completar y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="97d99-145">Complete and run the application</span></span>

<span data-ttu-id="97d99-146">Ahora puede completar la aplicación llamando al método **CreateIoTHub** antes de compilarla y ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="97d99-146">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="97d99-147">Agregue el siguiente código al final del método **Main** :</span><span class="sxs-lookup"><span data-stu-id="97d99-147">Add the following code to the end of the **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="97d99-148">Haga clic en **Compilar** y luego en **Compilar solución**.</span><span class="sxs-lookup"><span data-stu-id="97d99-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="97d99-149">Corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="97d99-149">Correct any errors.</span></span>

3. <span data-ttu-id="97d99-150">Haga clic en **Depurar** y luego en **Iniciar depuración** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="97d99-150">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="97d99-151">La ejecución de la implementación puede tardar varios minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="97d99-151">It may take several minutes for the deployment to run.</span></span>

4. <span data-ttu-id="97d99-152">Para comprobar que la aplicación ha agregado la nueva instancia de IoT Hub, visite [Azure Portal][lnk-azure-portal] y vea la lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="97d99-152">To verify that your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="97d99-153">Como alternativa, use el cmdlet de PowerShell **Get-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="97d99-153">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="97d99-154">Esta aplicación de ejemplo agrega un centro de IoT estándar S1 por el que se le cobrará.</span><span class="sxs-lookup"><span data-stu-id="97d99-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="97d99-155">Cuando haya terminado, podrá eliminar el centro de IoT a través de [Azure Portal][lnk-azure-portal] o con el cmdlet **Remove-AzureRmResource** de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97d99-155">When you are finished, you can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97d99-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97d99-156">Next steps</span></span>
<span data-ttu-id="97d99-157">Ahora que ha implementado un centro de IoT con la API de REST del proveedor de recursos, es posible que quiera profundizar más en este tema:</span><span class="sxs-lookup"><span data-stu-id="97d99-157">Now you have deployed an IoT hub using the resource provider REST API, you may want to explore further:</span></span>

* <span data-ttu-id="97d99-158">Consulte las funcionalidades de la [API de REST del proveedor de recursos de IoT Hub][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="97d99-158">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="97d99-159">Para más información sobre las funcionalidades de Azure Resource Manager, consulte [Información general de Azure Resource Manager][lnk-azure-rm-overview].</span><span class="sxs-lookup"><span data-stu-id="97d99-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="97d99-160">Para obtener más información sobre cómo desarrollar para IoT Hub, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="97d99-160">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="97d99-161">[Introducción al SDK de C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="97d99-161">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="97d99-162">[SDK de IoT de Azure][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="97d99-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="97d99-163">Para explorar aún más las funcionalidades de IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="97d99-163">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="97d99-164">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="97d99-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
