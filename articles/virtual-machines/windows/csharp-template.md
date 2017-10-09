---
title: "aaaDeploy una máquina virtual con C# y una plantilla de administrador de recursos | Documentos de Microsoft"
description: "Obtenga información acerca de toohow toouse C# y un toodeploy de plantilla de administrador de recursos una VM de Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: bfba66e8-c923-4df2-900a-0c2643b81240
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: davidmu
ms.openlocfilehash: 91d470228cfeed72336b488ffef4dfbb25bc3a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a>Implementación de una máquina virtual de Azure con C# y una plantilla de Resource Manager
Este artículo muestra cómo toodeploy una plantilla de Azure Resource Manager utilizando C#. plantilla de Hola que cree implementa una sola máquina virtual que ejecute Windows Server en una nueva red virtual con una sola subred.

Para obtener una descripción detallada del recurso de la máquina virtual de hello, consulte [máquinas virtuales en una plantilla de Azure Resource Manager](template-description.md). Para obtener más información acerca de todos los recursos de hello en una plantilla, consulte [tutorial de plantilla de Azure Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Tarda aproximadamente 10 minutos toodo estos pasos.

## <a name="create-a-visual-studio-project"></a>Creación de un proyecto de Visual Studio

En este paso, asegúrese de que está instalado Visual Studio y crear una plantilla de hello consola toodeploy de aplicación que se usa.

1. Si aún no lo ha hecho, instale [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Seleccione **desarrollo de escritorio de .NET** en Hola página cargas de trabajo y, a continuación, haga clic en **instalar**. En resumen de hello, puede ver que **herramientas de desarrollo de .NET Framework 4-4.6** se selecciona automáticamente. Si ya ha instalado Visual Studio, puede agregar carga de trabajo de .NET de hello mediante Hola selector de Visual Studio.
2. En Visual Studio, haga clic en **Archivo** > **Nuevo** > **proyecto**.
3. En **plantillas** > **Visual C#**, seleccione **aplicación de consola (.NET Framework)**, escriba *myDotnetProject* nombre Hola de Hola proyecto, ubicación de hello seleccione del proyecto de hello y, a continuación, haga clic en **Aceptar**.

## <a name="install-hello-packages"></a>Instalar paquetes de saludo

Paquetes de NuGet son hello más fácil manera tooinstall Hola bibliotecas que necesita toofinish estos pasos. bibliotecas de hello tooget que necesite en Visual Studio, siga estos pasos:

1. Haga clic en **Herramientas** > **Administrador de paquetes Nuget** y, después, haga clic en **Consola del Administrador de paquetes**.
2. En la consola de hello, escriba estos comandos:

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a>Crear archivos de Hola

En este paso, creará un archivo de plantilla que implementa los recursos de Hola y un archivo de parámetros que proporciona la plantilla de toohello de valores de parámetro. También creará un archivo de autorización es decir, operaciones de Azure Resource Manager tooperform usado.

### <a name="create-hello-template-file"></a>Crea un archivo de plantilla de Hola

1. En el Explorador de soluciones, haga clic en *myDotnetProject* > **Agregar** > **Nuevo elemento** y, después, seleccione **Archivo de texto** en *Elementos de Visual C#*. Archivo de nombre hello *CreateVMTemplate.json*y, a continuación, haga clic en **agregar**.
2. Agregue este archivo de toohello de código JSON que ha creado:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

3. Guarde el archivo de hello CreateVMTemplate.json.

### <a name="create-hello-parameters-file"></a>Crear archivo de parámetros de hello

toospecify valores para parámetros de recursos de Hola que se definen en la plantilla de hello, cree un archivo de parámetros que contiene los valores de hello.

1. En el Explorador de soluciones, haga clic en *myDotnetProject* > **Agregar** > **Nuevo elemento** y, después, seleccione **Archivo de texto** en *Elementos de Visual C#*. Archivo de nombre hello *Parameters.json*y, a continuación, haga clic en **agregar**.
2. Agregue este archivo de toohello de código JSON que ha creado:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

4. Guarde el archivo de hello Parameters.json.

### <a name="create-hello-authorization-file"></a>Crear archivo de autorización de hello

Antes de poder implementar una plantilla, asegúrese de que tiene acceso tooan [entidad de servicio de Active Directory](../../resource-group-authenticate-service-principal.md). Servidor principal de servicio de hello, adquirir un token para autenticar las solicitudes tooAzure el Administrador de recursos. También debe registrar el identificador de la aplicación hello y clave de autenticación de hello, Id. de inquilino de Hola que necesite en el archivo de autorización de hello.

1. En el Explorador de soluciones, haga clic en *myDotnetProject* > **Agregar** > **Nuevo elemento** y, después, seleccione **Archivo de texto** en *Elementos de Visual C#*. Archivo de nombre hello *azureauth.properties*y, a continuación, haga clic en **agregar**.
2. Agregue estas propiedades de autorización:

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    Reemplace  **&lt;Id. de suscripción&gt;**  con su identificador de suscripción,  **&lt;identificador de la aplicación&gt;**  con hello aplicación de Active Directory identificador,  **&lt;clave de autenticación&gt;**  con clave de la aplicación hello, y  **&lt;Id. de inquilino&gt;**  con inquilinos de Hola identificador.

3. Guarde el archivo de hello azureauth.properties.
4. Establecer una variable de entorno de Windows denominado AZURE_AUTH_LOCATION con el archivo de tooauthorization de ruta de acceso completa de hello que ha creado, por ejemplo Hola después puede utilizarse el comando de PowerShell:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a>Crear el cliente de administración de Hola

1. Abrir archivo Program.cs de Hola para proyecto de Hola que creó y, a continuación, agregarlas mediante instrucciones toohello existente en la parte superior del archivo hello:

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. cliente de administración de toocreate hello, agregue este toohello código del método Main:

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

toospecify valores para la aplicación hello, agregue el método Main de toohello de código:

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento

plantilla de Hola y parámetros se implementan desde una cuenta de almacenamiento de Azure. En este paso, cree la cuenta de hello y cargar archivos de Hola. 

toocreate Hola cuenta, agregue este toohello código del método Main:

```
string storageAccountName = SdkContext.RandomResourceName("st", 10);

Console.WriteLine("Creating storage account...");
var storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USWest)
    .WithExistingResourceGroup(resourceGroup)
    .Create();

var storageKeys = storage.GetKeys();
string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=" + storage.Name
    + ";AccountKey=" + storageKeys[0].Value
    + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
var serviceClient = account.CreateCloudBlobClient();

Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("templates");
container.CreateIfNotExistsAsync().Wait();
var containerPermissions = new BlobContainerPermissions()
    { PublicAccess = BlobContainerPublicAccessType.Container };
container.SetPermissionsAsync(containerPermissions).Wait();

Console.WriteLine("Uploading template file...");
var templateblob = container.GetBlockBlobReference("CreateVMTemplate.json");
templateblob.UploadFromFile("..\\..\\CreateVMTemplate.json");

Console.WriteLine("Uploading parameters file...");
var paramblob = container.GetBlockBlobReference("Parameters.json");
paramblob.UploadFromFile("..\\..\\Parameters.json");
```

## <a name="deploy-hello-template"></a>Implementar la plantilla de Hola

Implementar la plantilla de Hola y los parámetros de cuenta de almacenamiento de Hola que se creó. 

plantilla de hello toodeploy, agregue este toohello código del método Main:

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter toodelete hello resource group...");
Console.ReadLine();
```

## <a name="delete-hello-resources"></a>Eliminar recursos de Hola

Dado que se le cobra por recursos que usa en Azure, siempre es recursos toodelete de buena práctica que ya no son necesarios. No es necesario toodelete cada recurso por separado de un grupo de recursos. Eliminar el grupo de recursos de Hola y todos sus recursos se eliminarán automáticamente. 

recursos de hello toodelete grupo, agregue este toohello código del método Main:

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Ejecutar la aplicación hello

Tardará aproximadamente cinco minutos para este toorun de aplicación de consola completamente de toofinish de inicio. 

1. aplicación de consola de hello toorun, haga clic en **iniciar**.

2. Antes de presionar **ENTRAR** toostart eliminar recursos, podría tardar unos minutos creación de hello tooverify de recursos de Hola Hola portal de Azure. Haga clic en información de toosee de estado de implementación de hello acerca de la implementación de Hola.

## <a name="next-steps"></a>Pasos siguientes
* Si había problemas con la implementación de hello, el siguiente paso sería toolook en [solucionar errores comunes de implementación de Azure con el Administrador de recursos de Azure](../../resource-manager-common-deployment-errors.md).
* Obtenga información acerca de cómo toodeploy una máquina virtual y sus recursos de soporte revisando [implementar un Azure Máquina Virtual usando C#](csharp.md).
