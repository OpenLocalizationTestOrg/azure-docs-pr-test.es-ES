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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a>Creación de un centro de IoT con una plantilla de Azure Resource Manager (.NET)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Puede usar el Administrador de recursos de Azure toocreate y administrar centros de IoT de Azure mediante programación. Este tutorial muestra cómo toouse una toocreate de plantilla de Azure Resource Manager un centro de IoT desde un programa de C#.

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y clásico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artículo tratan con modelo de implementación de hello Azure Resource Manager.

toocomplete este tutorial, necesita Hola siguientes:

* Visual Studio 2015 o Visual Studio 2017.
* Una cuenta de Azure activa. <br/>Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.
* Una [cuenta de Azure Storage][lnk-storage-account] en la que pueda guardar los archivos de plantilla de Azure Resource Manager.
* [Azure PowerShell 1.0][lnk-powershell-install] o posterior.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Preparar su proyecto de Visual Studio

1. En Visual Studio, cree un proyecto de Visual C# escritorio clásico de Windows mediante hello **aplicación de consola (.NET Framework)** plantilla de proyecto. Proyecto de hello Name **CreateIoTHub**.

2. En el Explorador de soluciones, haga clic con el botón secundario en su proyecto y luego haga clic en **Administrar paquetes de NuGet**.

3. Compruebe en el Administrador de paquetes de NuGet, **versión preliminar de inclusión**y en hello **examinar** Buscar página **Microsoft.Azure.Management.ResourceManager**. Seleccionar paquete de hello, haga clic en **instalar**, en **revisar cambios** haga clic en **Aceptar**, a continuación, haga clic en **acepto** licencias de hello tooaccept.

4. En el Administrador de paquetes NuGet, busque **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Haga clic en **instalar**, en **revisar cambios** haga clic en **Aceptar**, a continuación, haga clic en **acepto** licencia de hello tooaccept.

5. En Program.cs, reemplace Hola existente **con** instrucciones con hello siguiente código:

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. En Program.cs, agregue Hola siguiendo las variables estáticas reemplazando los valores de marcador de posición de Hola. Ha tomado nota de **ApplicationId**, **SubscriptionId**, **TenantId** y **Password** anteriormente en este tutorial. **El nombre de cuenta de almacenamiento de Azure** es nombre de Hola de hello cuenta de almacenamiento de Azure donde se almacenan los archivos de plantilla de Azure Resource Manager. **Nombre del grupo de recursos** es nombre Hola Hola del grupo de recursos se usa cuando crea el centro de IoT Hola. nombre de Hello puede ser un grupo de recursos existente o nuevo. **Nombre de la implementación** es un nombre para la implementación de hello, como **Deployment_01**.

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

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Enviar una toocreate de plantilla un centro de IoT

Use un toocreate archivo plantilla y los parámetros JSON un centro de IoT en el grupo de recursos. También puede utilizar un centro de IoT Azure Resource Manager plantilla toomake cambios tooan existente.

1. En el Explorador de soluciones, haga clic con el botón derecho en el proyecto, haga clic en **Agregar** y luego en **Nuevo elemento**. Agregue un archivo JSON denominado **template.json** tooyour proyecto.

2. tooadd un estándar toohello centro de IoT **UU** región, replace Hola contenido de **template.json** con hello después de la definición de recursos. Consulte lista actual de Hola de las regiones que admiten el centro de IoT [estado de Azure][lnk-status]:

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

3. En el Explorador de soluciones, haga clic con el botón derecho en el proyecto, haga clic en **Agregar** y luego en **Nuevo elemento**. Agregue un archivo JSON denominado **parameters.json** tooyour proyecto.

4. Reemplace el contenido de Hola de **parameters.json** con hello siguiendo la información de parámetros que se establece como un nombre para el nuevo centro de IoT hello **{sus iniciales} mynewiothub**. nombre del centro de IoT Hola debe ser único globalmente, por lo que debe incluir su nombre o iniciales:

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

5. En **Explorador de servidores**, conectar tooyour suscripción de Azure, y en el almacenamiento de Azure cuenta crear un contenedor denominado **plantillas**. Hola **propiedades** panel, conjunto hello **acceso de lectura público** permisos para hello **plantillas** contenedor demasiado**Blob**.

6. En **Explorador de servidores**, haga doble clic en hello **plantillas** contenedor y, a continuación, haga clic en **ver contenedor de Blob**. Haga clic en hello **cargar Blob** botón, seleccione dos archivos de hello, **parameters.json** y **templates.json**y, a continuación, haga clic en **abiertos** Hola tooupload JSON archivos toohello **plantillas** contenedor. direcciones URL de Hola de blobs de Hola que contienen datos JSON Hola son:

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. Agregue Hola siguiendo el método tooProgram.cs:

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. Agregar Hola después código toohello **CreateIoTHub** método toosubmit Hola plantilla y parámetros archivos toohello Azure Resource Manager:

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

9. Agregar Hola después código toohello **CreateIoTHub** método que muestra el estado de Hola y claves de hello para el nuevo centro de IoT hello:

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a>Aplicación hello completo y ejecución

Ahora puede completar aplicación hello mediante la llamada hello **CreateIoTHub** método antes de compilarla y ejecutarla.

1. Agregar Hola siguiente código toohello final de hello **Main** método:

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. Haga clic en **Compilar** y luego en **Compilar solución**. Corrija los errores.

3. Haga clic en **depurar** y, a continuación, **Iniciar depuración** aplicación de hello toorun. Puede tardar varios minutos para hello toorun de implementación.

4. tooverify agregado la aplicación Hola nuevo centro de IoT, visite hello [portal de Azure] [ lnk-azure-portal] y ver la lista de recursos. O bien, usar hello **Get-AzureRmResource** cmdlet de PowerShell.

> [!NOTE]
> Esta aplicación de ejemplo agrega un centro de IoT estándar S1 por el que se le cobrará. Puede eliminar el centro de IoT de Hola a través de hello [portal de Azure] [ lnk-azure-portal] o mediante el uso de hello **Remove-AzureRmResource** cmdlet de PowerShell cuando haya terminado.

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha implementado un centro de IoT utilizando una plantilla de Azure Resource Manager con un programa de C#, puede que desee tooexplore adicional:

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
[lnk-storage-account]:../storage/common/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
