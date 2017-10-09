---
title: Hola a aaaCreate un concentrador de IoT de Azure mediante API de REST de proveedor de recursos | Documentos de Microsoft
description: "¿Cómo toouse Hola toocreate de API de REST de proveedor de recursos de un centro de IoT."
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
ms.openlocfilehash: 98d240ccce47dec13a255bce28943b40f5354ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a><span data-ttu-id="b7e7b-103">Crear un centro de IoT mediante el proveedor de recursos de hello API de REST (. NET)</span><span class="sxs-lookup"><span data-stu-id="b7e7b-103">Create an IoT hub using hello resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="b7e7b-104">Puede usar hello [API de REST de proveedor de recursos de centro de IoT] [ lnk-rest-api] toocreate y administrar centros de IoT de Azure mediante programación.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-104">You can use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="b7e7b-105">Este tutorial muestra cómo toouse Hola toocreate de API de REST de proveedor de recursos de centro de IoT un centro de IoT desde un programa de C#.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-105">This tutorial shows you how toouse hello IoT Hub resource provider REST API toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="b7e7b-106">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b7e7b-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="b7e7b-107">Este artículo tratan con modelo de implementación de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="b7e7b-108">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b7e7b-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b7e7b-109">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="b7e7b-110">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-110">An active Azure account.</span></span> <br/><span data-ttu-id="b7e7b-111">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="b7e7b-112">[Azure PowerShell 1.0][lnk-powershell-install] o posterior.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="b7e7b-113">Preparar su proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b7e7b-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="b7e7b-114">En Visual Studio, cree un proyecto de Visual C# escritorio clásico de Windows mediante hello **aplicación de consola (.NET Framework)** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="b7e7b-115">Proyecto de hello Name **CreateIoTHubREST**.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-115">Name hello project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="b7e7b-116">En el Explorador de soluciones, haga clic con el botón secundario en su proyecto y luego haga clic en **Administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="b7e7b-117">Compruebe en el Administrador de paquetes de NuGet, **versión preliminar de inclusión**y en hello **examinar** Buscar página **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-117">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="b7e7b-118">Seleccionar paquete de hello, haga clic en **instalar**, en **revisar cambios** haga clic en **Aceptar**, a continuación, haga clic en **acepto** licencias de hello tooaccept.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-118">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="b7e7b-119">En el Administrador de paquetes NuGet, busque **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="b7e7b-120">Haga clic en **instalar**, en **revisar cambios** haga clic en **Aceptar**, a continuación, haga clic en **acepto** licencia de hello tooaccept.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="b7e7b-121">En Program.cs, reemplace Hola existente **con** instrucciones con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="b7e7b-121">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

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

6. <span data-ttu-id="b7e7b-122">En Program.cs, agregue Hola siguiendo las variables estáticas reemplazando los valores de marcador de posición de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-122">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="b7e7b-123">Ha tomado nota de **ApplicationId**, **SubscriptionId**, **TenantId** y **Password** anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="b7e7b-124">**Nombre del grupo de recursos** es nombre Hola Hola del grupo de recursos se usa cuando crea el centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-124">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="b7e7b-125">Puede ser un grupo de recursos ya existente u otro nuevo.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="b7e7b-126">**El nombre del centro de IoT** es nombre Hola de Hola que cree, como el centro de IoT **MyIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-126">**IoT Hub name** is hello name of hello IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="b7e7b-127">nombre de Hola de su centro de IoT debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-127">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="b7e7b-128">**Nombre de la implementación** es un nombre para la implementación de hello, como **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

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

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a><span data-ttu-id="b7e7b-129">Usar toocreate de API de REST de proveedor de recursos de hello un centro de IoT</span><span class="sxs-lookup"><span data-stu-id="b7e7b-129">Use hello resource provider REST API toocreate an IoT hub</span></span>

<span data-ttu-id="b7e7b-130">Hola de uso [API de REST de proveedor de recursos de centro de IoT] [ lnk-rest-api] toocreate un centro de IoT en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-130">Use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="b7e7b-131">También puede utilizar Hola recursos proveedor API de REST toomake cambios tooan existente centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-131">You can also use hello resource provider REST API toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="b7e7b-132">Agregue Hola siguiendo el método tooProgram.cs:</span><span class="sxs-lookup"><span data-stu-id="b7e7b-132">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="b7e7b-133">Agregar Hola después código toohello **CreateIoTHub** método.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-133">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="b7e7b-134">Este código crea un **HttpClient** objeto con el token de autenticación de hello en encabezados de hello:</span><span class="sxs-lookup"><span data-stu-id="b7e7b-134">This code creates an **HttpClient** object with hello authentication token in hello headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="b7e7b-135">Agregar Hola después código toohello **CreateIoTHub** método.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-135">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="b7e7b-136">Este código describe Hola IoT hub toocreate y genera una representación de JSON.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-136">This code describes hello IoT hub toocreate and generates a JSON representation.</span></span> <span data-ttu-id="b7e7b-137">Consulte lista actual de Hola de ubicaciones que admiten el centro de IoT [estado de Azure][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="b7e7b-137">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

4. <span data-ttu-id="b7e7b-138">Agregar Hola después código toohello **CreateIoTHub** método.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-138">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="b7e7b-139">Este código envía Hola REST solicitud tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-139">This code submits hello REST request tooAzure.</span></span> <span data-ttu-id="b7e7b-140">código de Hello, a continuación, comprueba la respuesta de Hola y recupera la dirección URL de hello puede utilizar el estado de hello toomonitor de tarea de implementación de hello:</span><span class="sxs-lookup"><span data-stu-id="b7e7b-140">hello code then checks hello response and retrieves hello URL you can use toomonitor hello state of hello deployment task:</span></span>

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

5. <span data-ttu-id="b7e7b-141">Agregar Hola siguiente código toohello final de hello **CreateIoTHub** método.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-141">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="b7e7b-142">Este código usa hello **asyncStatusUri** dirección recupera en hello anterior paso toowait para hello toocomplete de implementación:</span><span class="sxs-lookup"><span data-stu-id="b7e7b-142">This code uses hello **asyncStatusUri** address retrieved in hello previous step toowait for hello deployment toocomplete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="b7e7b-143">Agregar Hola siguiente código toohello final de hello **CreateIoTHub** método.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-143">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="b7e7b-144">Este código recupera las claves de Hola de hello centro de IoT se crean y se imprime toohello consola:</span><span class="sxs-lookup"><span data-stu-id="b7e7b-144">This code retrieves hello keys of hello IoT hub you created and prints them toohello console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="b7e7b-145">Aplicación hello completo y ejecución</span><span class="sxs-lookup"><span data-stu-id="b7e7b-145">Complete and run hello application</span></span>

<span data-ttu-id="b7e7b-146">Ahora puede completar aplicación hello mediante la llamada hello **CreateIoTHub** método antes de compilarla y ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-146">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="b7e7b-147">Agregar Hola siguiente código toohello final de hello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="b7e7b-147">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="b7e7b-148">Haga clic en **Compilar** y luego en **Compilar solución**.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="b7e7b-149">Corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-149">Correct any errors.</span></span>

3. <span data-ttu-id="b7e7b-150">Haga clic en **depurar** y, a continuación, **Iniciar depuración** aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-150">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="b7e7b-151">Puede tardar varios minutos para hello toorun de implementación.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-151">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="b7e7b-152">tooverify que agrega la aplicación Hola nuevo centro de IoT, visite hello [portal de Azure] [ lnk-azure-portal] y ver la lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-152">tooverify that your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="b7e7b-153">O bien, usar hello **Get-AzureRmResource** cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-153">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="b7e7b-154">Esta aplicación de ejemplo agrega un centro de IoT estándar S1 por el que se le cobrará.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="b7e7b-155">Cuando haya terminado, puede eliminar el centro de IoT de Hola a través de hello [portal de Azure] [ lnk-azure-portal] o mediante el uso de hello **Remove-AzureRmResource** cmdlet de PowerShell cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-155">When you are finished, you can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7e7b-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b7e7b-156">Next steps</span></span>
<span data-ttu-id="b7e7b-157">Ahora que ha implementado un centro de IoT mediante el proveedor de recursos de hello API de REST, puede que desee tooexplore adicional:</span><span class="sxs-lookup"><span data-stu-id="b7e7b-157">Now you have deployed an IoT hub using hello resource provider REST API, you may want tooexplore further:</span></span>

* <span data-ttu-id="b7e7b-158">Obtenga información sobre las capacidades de Hola de hello [API de REST de proveedor de recursos de centro de IoT][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="b7e7b-158">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="b7e7b-159">Lectura [Introducción al administrador de recursos de Azure] [ lnk-azure-rm-overview] toolearn más información acerca de las capacidades de hello del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7e7b-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="b7e7b-160">toolearn más sobre el desarrollo de centro de IoT, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="b7e7b-160">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="b7e7b-161">[Introducción tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="b7e7b-161">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="b7e7b-162">[SDK de IoT de Azure][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="b7e7b-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="b7e7b-163">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="b7e7b-163">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b7e7b-164">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="b7e7b-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
