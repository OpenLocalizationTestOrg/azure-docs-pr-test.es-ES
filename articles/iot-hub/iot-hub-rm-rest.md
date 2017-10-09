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
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a>Crear un centro de IoT mediante el proveedor de recursos de hello API de REST (. NET)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Puede usar hello [API de REST de proveedor de recursos de centro de IoT] [ lnk-rest-api] toocreate y administrar centros de IoT de Azure mediante programación. Este tutorial muestra cómo toouse Hola toocreate de API de REST de proveedor de recursos de centro de IoT un centro de IoT desde un programa de C#.

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y clásico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artículo tratan con modelo de implementación de hello Azure Resource Manager.

toocomplete este tutorial, necesita Hola siguientes:

* Visual Studio 2015 o Visual Studio 2017.
* Una cuenta de Azure activa. <br/>Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.
* [Azure PowerShell 1.0][lnk-powershell-install] o posterior.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Preparar su proyecto de Visual Studio

1. En Visual Studio, cree un proyecto de Visual C# escritorio clásico de Windows mediante hello **aplicación de consola (.NET Framework)** plantilla de proyecto. Proyecto de hello Name **CreateIoTHubREST**.

2. En el Explorador de soluciones, haga clic con el botón secundario en su proyecto y luego haga clic en **Administrar paquetes de NuGet**.

3. Compruebe en el Administrador de paquetes de NuGet, **versión preliminar de inclusión**y en hello **examinar** Buscar página **Microsoft.Azure.Management.ResourceManager**. Seleccionar paquete de hello, haga clic en **instalar**, en **revisar cambios** haga clic en **Aceptar**, a continuación, haga clic en **acepto** licencias de hello tooaccept.

4. En el Administrador de paquetes NuGet, busque **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Haga clic en **instalar**, en **revisar cambios** haga clic en **Aceptar**, a continuación, haga clic en **acepto** licencia de hello tooaccept.

5. En Program.cs, reemplace Hola existente **con** instrucciones con hello siguiente código:

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

6. En Program.cs, agregue Hola siguiendo las variables estáticas reemplazando los valores de marcador de posición de Hola. Ha tomado nota de **ApplicationId**, **SubscriptionId**, **TenantId** y **Password** anteriormente en este tutorial. **Nombre del grupo de recursos** es nombre Hola Hola del grupo de recursos se usa cuando crea el centro de IoT Hola. Puede ser un grupo de recursos ya existente u otro nuevo. **El nombre del centro de IoT** es nombre Hola de Hola que cree, como el centro de IoT **MyIoTHub**. nombre de Hola de su centro de IoT debe ser único globalmente. **Nombre de la implementación** es un nombre para la implementación de hello, como **Deployment_01**.

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

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a>Usar toocreate de API de REST de proveedor de recursos de hello un centro de IoT

Hola de uso [API de REST de proveedor de recursos de centro de IoT] [ lnk-rest-api] toocreate un centro de IoT en el grupo de recursos. También puede utilizar Hola recursos proveedor API de REST toomake cambios tooan existente centro de IoT.

1. Agregue Hola siguiendo el método tooProgram.cs:

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. Agregar Hola después código toohello **CreateIoTHub** método. Este código crea un **HttpClient** objeto con el token de autenticación de hello en encabezados de hello:

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. Agregar Hola después código toohello **CreateIoTHub** método. Este código describe Hola IoT hub toocreate y genera una representación de JSON. Consulte lista actual de Hola de ubicaciones que admiten el centro de IoT [estado de Azure][lnk-status]:

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

4. Agregar Hola después código toohello **CreateIoTHub** método. Este código envía Hola REST solicitud tooAzure. código de Hello, a continuación, comprueba la respuesta de Hola y recupera la dirección URL de hello puede utilizar el estado de hello toomonitor de tarea de implementación de hello:

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

5. Agregar Hola siguiente código toohello final de hello **CreateIoTHub** método. Este código usa hello **asyncStatusUri** dirección recupera en hello anterior paso toowait para hello toocomplete de implementación:

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. Agregar Hola siguiente código toohello final de hello **CreateIoTHub** método. Este código recupera las claves de Hola de hello centro de IoT se crean y se imprime toohello consola:

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a>Aplicación hello completo y ejecución

Ahora puede completar aplicación hello mediante la llamada hello **CreateIoTHub** método antes de compilarla y ejecutarla.

1. Agregar Hola siguiente código toohello final de hello **Main** método:

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. Haga clic en **Compilar** y luego en **Compilar solución**. Corrija los errores.

3. Haga clic en **depurar** y, a continuación, **Iniciar depuración** aplicación de hello toorun. Puede tardar varios minutos para hello toorun de implementación.

4. tooverify que agrega la aplicación Hola nuevo centro de IoT, visite hello [portal de Azure] [ lnk-azure-portal] y ver la lista de recursos. O bien, usar hello **Get-AzureRmResource** cmdlet de PowerShell.

> [!NOTE]
> Esta aplicación de ejemplo agrega un centro de IoT estándar S1 por el que se le cobrará. Cuando haya terminado, puede eliminar el centro de IoT de Hola a través de hello [portal de Azure] [ lnk-azure-portal] o mediante el uso de hello **Remove-AzureRmResource** cmdlet de PowerShell cuando haya terminado.

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha implementado un centro de IoT mediante el proveedor de recursos de hello API de REST, puede que desee tooexplore adicional:

* Obtenga información sobre las capacidades de Hola de hello [API de REST de proveedor de recursos de centro de IoT][lnk-rest-api].
* Lectura [Introducción al administrador de recursos de Azure] [ lnk-azure-rm-overview] toolearn más información acerca de las capacidades de hello del Administrador de recursos de Azure.

toolearn más sobre el desarrollo de centro de IoT, vea Hola siguientes artículos:

* [Introducción tooC SDK][lnk-c-sdk]
* [SDK de IoT de Azure][lnk-sdks]

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Simular un dispositivo con Azure IoT Edge][lnk-iotedge]

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
