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
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a><span data-ttu-id="e788f-103">Implementación de una máquina virtual de Azure con C# y una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e788f-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span></span>
<span data-ttu-id="e788f-104">Este artículo muestra cómo toodeploy una plantilla de Azure Resource Manager utilizando C#.</span><span class="sxs-lookup"><span data-stu-id="e788f-104">This article shows you how toodeploy an Azure Resource Manager template using C#.</span></span> <span data-ttu-id="e788f-105">plantilla de Hola que cree implementa una sola máquina virtual que ejecute Windows Server en una nueva red virtual con una sola subred.</span><span class="sxs-lookup"><span data-stu-id="e788f-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="e788f-106">Para obtener una descripción detallada del recurso de la máquina virtual de hello, consulte [máquinas virtuales en una plantilla de Azure Resource Manager](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="e788f-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="e788f-107">Para obtener más información acerca de todos los recursos de hello en una plantilla, consulte [tutorial de plantilla de Azure Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="e788f-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="e788f-108">Tarda aproximadamente 10 minutos toodo estos pasos.</span><span class="sxs-lookup"><span data-stu-id="e788f-108">It takes about 10 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="e788f-109">Creación de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e788f-109">Create a Visual Studio project</span></span>

<span data-ttu-id="e788f-110">En este paso, asegúrese de que está instalado Visual Studio y crear una plantilla de hello consola toodeploy de aplicación que se usa.</span><span class="sxs-lookup"><span data-stu-id="e788f-110">In this step, you make sure that Visual Studio is installed and you create a console application used toodeploy hello template.</span></span>

1. <span data-ttu-id="e788f-111">Si aún no lo ha hecho, instale [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="e788f-111">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="e788f-112">Seleccione **desarrollo de escritorio de .NET** en Hola página cargas de trabajo y, a continuación, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="e788f-112">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="e788f-113">En resumen de hello, puede ver que **herramientas de desarrollo de .NET Framework 4-4.6** se selecciona automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e788f-113">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="e788f-114">Si ya ha instalado Visual Studio, puede agregar carga de trabajo de .NET de hello mediante Hola selector de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e788f-114">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="e788f-115">En Visual Studio, haga clic en **Archivo** > **Nuevo** > **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="e788f-115">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="e788f-116">En **plantillas** > **Visual C#**, seleccione **aplicación de consola (.NET Framework)**, escriba *myDotnetProject* nombre Hola de Hola proyecto, ubicación de hello seleccione del proyecto de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e788f-116">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-packages"></a><span data-ttu-id="e788f-117">Instalar paquetes de saludo</span><span class="sxs-lookup"><span data-stu-id="e788f-117">Install hello packages</span></span>

<span data-ttu-id="e788f-118">Paquetes de NuGet son hello más fácil manera tooinstall Hola bibliotecas que necesita toofinish estos pasos.</span><span class="sxs-lookup"><span data-stu-id="e788f-118">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="e788f-119">bibliotecas de hello tooget que necesite en Visual Studio, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e788f-119">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="e788f-120">Haga clic en **Herramientas** > **Administrador de paquetes Nuget** y, después, haga clic en **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="e788f-120">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="e788f-121">En la consola de hello, escriba estos comandos:</span><span class="sxs-lookup"><span data-stu-id="e788f-121">Type these commands in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a><span data-ttu-id="e788f-122">Crear archivos de Hola</span><span class="sxs-lookup"><span data-stu-id="e788f-122">Create hello files</span></span>

<span data-ttu-id="e788f-123">En este paso, creará un archivo de plantilla que implementa los recursos de Hola y un archivo de parámetros que proporciona la plantilla de toohello de valores de parámetro.</span><span class="sxs-lookup"><span data-stu-id="e788f-123">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="e788f-124">También creará un archivo de autorización es decir, operaciones de Azure Resource Manager tooperform usado.</span><span class="sxs-lookup"><span data-stu-id="e788f-124">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

### <a name="create-hello-template-file"></a><span data-ttu-id="e788f-125">Crea un archivo de plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="e788f-125">Create hello template file</span></span>

1. <span data-ttu-id="e788f-126">En el Explorador de soluciones, haga clic en *myDotnetProject* > **Agregar** > **Nuevo elemento** y, después, seleccione **Archivo de texto** en *Elementos de Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="e788f-126">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="e788f-127">Archivo de nombre hello *CreateVMTemplate.json*y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="e788f-127">Name hello file *CreateVMTemplate.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="e788f-128">Agregue este archivo de toohello de código JSON que ha creado:</span><span class="sxs-lookup"><span data-stu-id="e788f-128">Add this JSON code toohello file that you created:</span></span>

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

3. <span data-ttu-id="e788f-129">Guarde el archivo de hello CreateVMTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="e788f-129">Save hello CreateVMTemplate.json file.</span></span>

### <a name="create-hello-parameters-file"></a><span data-ttu-id="e788f-130">Crear archivo de parámetros de hello</span><span class="sxs-lookup"><span data-stu-id="e788f-130">Create hello parameters file</span></span>

<span data-ttu-id="e788f-131">toospecify valores para parámetros de recursos de Hola que se definen en la plantilla de hello, cree un archivo de parámetros que contiene los valores de hello.</span><span class="sxs-lookup"><span data-stu-id="e788f-131">toospecify values for hello resource parameters that are defined in hello template, you create a parameters file that contains hello values.</span></span>

1. <span data-ttu-id="e788f-132">En el Explorador de soluciones, haga clic en *myDotnetProject* > **Agregar** > **Nuevo elemento** y, después, seleccione **Archivo de texto** en *Elementos de Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="e788f-132">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="e788f-133">Archivo de nombre hello *Parameters.json*y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="e788f-133">Name hello file *Parameters.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="e788f-134">Agregue este archivo de toohello de código JSON que ha creado:</span><span class="sxs-lookup"><span data-stu-id="e788f-134">Add this JSON code toohello file that you created:</span></span>

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

4. <span data-ttu-id="e788f-135">Guarde el archivo de hello Parameters.json.</span><span class="sxs-lookup"><span data-stu-id="e788f-135">Save hello Parameters.json file.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="e788f-136">Crear archivo de autorización de hello</span><span class="sxs-lookup"><span data-stu-id="e788f-136">Create hello authorization file</span></span>

<span data-ttu-id="e788f-137">Antes de poder implementar una plantilla, asegúrese de que tiene acceso tooan [entidad de servicio de Active Directory](../../resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="e788f-137">Before you can deploy a template, make sure that you have access tooan [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="e788f-138">Servidor principal de servicio de hello, adquirir un token para autenticar las solicitudes tooAzure el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="e788f-138">From hello service principal, you acquire a token for authenticating requests tooAzure Resource Manager.</span></span> <span data-ttu-id="e788f-139">También debe registrar el identificador de la aplicación hello y clave de autenticación de hello, Id. de inquilino de Hola que necesite en el archivo de autorización de hello.</span><span class="sxs-lookup"><span data-stu-id="e788f-139">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in hello authorization file.</span></span>

1. <span data-ttu-id="e788f-140">En el Explorador de soluciones, haga clic en *myDotnetProject* > **Agregar** > **Nuevo elemento** y, después, seleccione **Archivo de texto** en *Elementos de Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="e788f-140">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="e788f-141">Archivo de nombre hello *azureauth.properties*y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="e788f-141">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="e788f-142">Agregue estas propiedades de autorización:</span><span class="sxs-lookup"><span data-stu-id="e788f-142">Add these authorization properties:</span></span>

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

    <span data-ttu-id="e788f-143">Reemplace  **&lt;Id. de suscripción&gt;**  con su identificador de suscripción,  **&lt;identificador de la aplicación&gt;**  con hello aplicación de Active Directory identificador,  **&lt;clave de autenticación&gt;**  con clave de la aplicación hello, y  **&lt;Id. de inquilino&gt;**  con inquilinos de Hola identificador.</span><span class="sxs-lookup"><span data-stu-id="e788f-143">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="e788f-144">Guarde el archivo de hello azureauth.properties.</span><span class="sxs-lookup"><span data-stu-id="e788f-144">Save hello azureauth.properties file.</span></span>
4. <span data-ttu-id="e788f-145">Establecer una variable de entorno de Windows denominado AZURE_AUTH_LOCATION con el archivo de tooauthorization de ruta de acceso completa de hello que ha creado, por ejemplo Hola después puede utilizarse el comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e788f-145">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created, for example hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a><span data-ttu-id="e788f-146">Crear el cliente de administración de Hola</span><span class="sxs-lookup"><span data-stu-id="e788f-146">Create hello management client</span></span>

1. <span data-ttu-id="e788f-147">Abrir archivo Program.cs de Hola para proyecto de Hola que creó y, a continuación, agregarlas mediante instrucciones toohello existente en la parte superior del archivo hello:</span><span class="sxs-lookup"><span data-stu-id="e788f-147">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. <span data-ttu-id="e788f-148">cliente de administración de toocreate hello, agregue este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="e788f-148">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="e788f-149">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e788f-149">Create a resource group</span></span>

<span data-ttu-id="e788f-150">toospecify valores para la aplicación hello, agregue el método Main de toohello de código:</span><span class="sxs-lookup"><span data-stu-id="e788f-150">toospecify values for hello application, add code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a><span data-ttu-id="e788f-151">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e788f-151">Create a storage account</span></span>

<span data-ttu-id="e788f-152">plantilla de Hola y parámetros se implementan desde una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e788f-152">hello template and parameters are deployed from a storage account in Azure.</span></span> <span data-ttu-id="e788f-153">En este paso, cree la cuenta de hello y cargar archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e788f-153">In this step, you create hello account and upload hello files.</span></span> 

<span data-ttu-id="e788f-154">toocreate Hola cuenta, agregue este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="e788f-154">toocreate hello account, add this code toohello Main method:</span></span>

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

## <a name="deploy-hello-template"></a><span data-ttu-id="e788f-155">Implementar la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="e788f-155">Deploy hello template</span></span>

<span data-ttu-id="e788f-156">Implementar la plantilla de Hola y los parámetros de cuenta de almacenamiento de Hola que se creó.</span><span class="sxs-lookup"><span data-stu-id="e788f-156">Deploy hello template and parameters from hello storage account that was created.</span></span> 

<span data-ttu-id="e788f-157">plantilla de hello toodeploy, agregue este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="e788f-157">toodeploy hello template, add this code toohello Main method:</span></span>

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

## <a name="delete-hello-resources"></a><span data-ttu-id="e788f-158">Eliminar recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="e788f-158">Delete hello resources</span></span>

<span data-ttu-id="e788f-159">Dado que se le cobra por recursos que usa en Azure, siempre es recursos toodelete de buena práctica que ya no son necesarios.</span><span class="sxs-lookup"><span data-stu-id="e788f-159">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="e788f-160">No es necesario toodelete cada recurso por separado de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e788f-160">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="e788f-161">Eliminar el grupo de recursos de Hola y todos sus recursos se eliminarán automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e788f-161">Delete hello resource group and all its resources are automatically deleted.</span></span> 

<span data-ttu-id="e788f-162">recursos de hello toodelete grupo, agregue este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="e788f-162">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="e788f-163">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="e788f-163">Run hello application</span></span>

<span data-ttu-id="e788f-164">Tardará aproximadamente cinco minutos para este toorun de aplicación de consola completamente de toofinish de inicio.</span><span class="sxs-lookup"><span data-stu-id="e788f-164">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="e788f-165">aplicación de consola de hello toorun, haga clic en **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="e788f-165">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="e788f-166">Antes de presionar **ENTRAR** toostart eliminar recursos, podría tardar unos minutos creación de hello tooverify de recursos de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e788f-166">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="e788f-167">Haga clic en información de toosee de estado de implementación de hello acerca de la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e788f-167">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e788f-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e788f-168">Next steps</span></span>
* <span data-ttu-id="e788f-169">Si había problemas con la implementación de hello, el siguiente paso sería toolook en [solucionar errores comunes de implementación de Azure con el Administrador de recursos de Azure](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="e788f-169">If there were issues with hello deployment, a next step would be toolook at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="e788f-170">Obtenga información acerca de cómo toodeploy una máquina virtual y sus recursos de soporte revisando [implementar un Azure Máquina Virtual usando C#](csharp.md).</span><span class="sxs-lookup"><span data-stu-id="e788f-170">Learn how toodeploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
