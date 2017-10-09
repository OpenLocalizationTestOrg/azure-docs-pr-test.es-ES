---
title: aaaCreate las canalizaciones de datos mediante el uso de Azure SDK para .NET | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooprogrammatically crear, supervisar y administrar factorías de datos de Azure mediante el SDK de generador de datos."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="2827b-103">Creación, supervisión y administración de factorías de datos de Azure mediante el SDK de .NET de Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2827b-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="2827b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="2827b-104">Overview</span></span>
<span data-ttu-id="2827b-105">Puede crear, supervisar y administrar factorías de datos de Azure mediante programación con el SDK de .NET de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="2827b-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="2827b-106">Este artículo contiene un tutorial que puede seguir toocreate una aplicación de consola .NET de ejemplo que crea y supervisa una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="2827b-106">This article contains a walkthrough that you can follow toocreate a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="2827b-107">Este artículo no cubre Hola todas las API de .NET del generador de datos.</span><span class="sxs-lookup"><span data-stu-id="2827b-107">This article does not cover all hello Data Factory .NET API.</span></span> <span data-ttu-id="2827b-108">Para obtener documentación completa sobre la API de .NET para Data Factory, consulte la [referencia de API de .NET de Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="2827b-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2827b-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2827b-109">Prerequisites</span></span>
* <span data-ttu-id="2827b-110">Visual Studio 2012, 2013 o 2015</span><span class="sxs-lookup"><span data-stu-id="2827b-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="2827b-111">Descargue e instale el [SDK de .NET de Azure](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2827b-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="2827b-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2827b-112">Azure PowerShell.</span></span> <span data-ttu-id="2827b-113">Siga las instrucciones de [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo tooinstall Azure PowerShell en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2827b-113">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="2827b-114">Usar PowerShell de Azure toocreate una aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2827b-114">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="2827b-115">Creación de una aplicación en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2827b-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="2827b-116">Crear una aplicación de Azure Active Directory, cree una entidad de servicio para la aplicación hello y asignar toohello **colaborador de la factoría de datos** rol.</span><span class="sxs-lookup"><span data-stu-id="2827b-116">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="2827b-117">Inicie **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="2827b-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="2827b-118">Ejecute el siguiente comando de Hola y escriba el nombre de usuario de Hola y la contraseña que usa toosign en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2827b-118">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="2827b-119">Ejecute hello después comando tooview todas las suscripciones de Hola para esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="2827b-119">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="2827b-120">Ejecute hello después de suscripción de hello tooselect de comando que desee toowork con.</span><span class="sxs-lookup"><span data-stu-id="2827b-120">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="2827b-121">Reemplace  **&lt;NameOfAzureSubscription** &gt; con el nombre de Hola de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2827b-121">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="2827b-122">Tenga en cuenta hacia abajo **SubscriptionId** y **TenantId** de salida de hello de este comando.</span><span class="sxs-lookup"><span data-stu-id="2827b-122">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="2827b-123">Crear un grupo de recursos de Azure denominado **ADFTutorialResourceGroup** ejecutando Hola siguiente comando en hello PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2827b-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="2827b-124">Si ya existe el grupo de recursos de hello, especifique si tooupdate se (Y) o mantener un nivel tan (N).</span><span class="sxs-lookup"><span data-stu-id="2827b-124">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="2827b-125">Si utiliza un grupo de recursos diferente, necesita toouse Hola nombre de su grupo de recursos en lugar de ADFTutorialResourceGroup en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="2827b-125">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="2827b-126">Cree una aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2827b-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="2827b-127">Si se producen Hola tras error, especifique una URL distinta y vuelva a ejecutar el comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="2827b-127">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="2827b-128">Crear Hola la entidad de servicio de AD.</span><span class="sxs-lookup"><span data-stu-id="2827b-128">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="2827b-129">Agregar servicio principal toohello **colaborador de la factoría de datos** rol.</span><span class="sxs-lookup"><span data-stu-id="2827b-129">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="2827b-130">Obtener el identificador de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="2827b-130">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="2827b-131">Anote el identificador de la aplicación de hello (applicationID) de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="2827b-131">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="2827b-132">Debe tener los cuatro valores siguientes de estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2827b-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="2827b-133">Id. de inquilino</span><span class="sxs-lookup"><span data-stu-id="2827b-133">Tenant ID</span></span>
* <span data-ttu-id="2827b-134">Id. de suscripción</span><span class="sxs-lookup"><span data-stu-id="2827b-134">Subscription ID</span></span>
* <span data-ttu-id="2827b-135">Identificador de aplicación</span><span class="sxs-lookup"><span data-stu-id="2827b-135">Application ID</span></span>
* <span data-ttu-id="2827b-136">Contraseña (especificada en el primer comando de hello)</span><span class="sxs-lookup"><span data-stu-id="2827b-136">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="2827b-137">Tutorial</span><span class="sxs-lookup"><span data-stu-id="2827b-137">Walkthrough</span></span>
<span data-ttu-id="2827b-138">En el tutorial de hello, se crea una factoría de datos con una canalización que contiene una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="2827b-138">In hello walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="2827b-139">Hello actividad de copia copia los datos desde una carpeta en su carpeta de tooanother de almacenamiento de blobs de Azure en hello mismo almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="2827b-139">hello copy activity copies data from a folder in your Azure blob storage tooanother folder in hello same blob storage.</span></span> 

<span data-ttu-id="2827b-140">Hola actividad de copia realiza el movimiento de datos de hello en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="2827b-140">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="2827b-141">actividad Hello funciona con un servicio disponible globalmente que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable.</span><span class="sxs-lookup"><span data-stu-id="2827b-141">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="2827b-142">Vea [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo para obtener más información acerca de la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="2827b-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

1. <span data-ttu-id="2827b-143">Con Visual Studio 2012, 2013 o 2015, cree una aplicación de consola .NET de C#.</span><span class="sxs-lookup"><span data-stu-id="2827b-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="2827b-144">Inicie **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="2827b-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="2827b-145">Haga clic en **archivo**, seleccione demasiado**New**y haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="2827b-145">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="2827b-146">Expanda **Plantillas** y seleccione **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="2827b-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="2827b-147">En este tutorial, se usa C# pero puede usar cualquier lenguaje .NET.</span><span class="sxs-lookup"><span data-stu-id="2827b-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="2827b-148">Seleccione **aplicación de consola** de lista de Hola de tipos de proyecto en hello derecho.</span><span class="sxs-lookup"><span data-stu-id="2827b-148">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="2827b-149">Escriba **DataFactoryAPITestApp** para hello nombre.</span><span class="sxs-lookup"><span data-stu-id="2827b-149">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="2827b-150">Seleccione **C:\ADFGetStarted** para hello ubicación.</span><span class="sxs-lookup"><span data-stu-id="2827b-150">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="2827b-151">Haga clic en **Aceptar** proyecto de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2827b-151">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="2827b-152">Haga clic en **herramientas**, seleccione demasiado**Administrador de paquetes de NuGet**y haga clic en **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="2827b-152">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="2827b-153">Hola **Package Manager Console**, Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2827b-153">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="2827b-154">Ejecute hello después el paquete de comando tooinstall factoría de datos:`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="2827b-154">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="2827b-155">Ejecute hello después el paquete de Azure Active Directory tooinstall command (usar API de Active Directory en el código de hello):`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="2827b-155">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="2827b-156">Reemplace el contenido de Hola de **App.config** archivo de proyecto de hello con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="2827b-156">Replace hello contents of **App.config** file in hello project with hello following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="2827b-157">En el archivo App.Config de hello, actualice los valores de  **&lt;Id. de aplicación&gt;**,  **&lt;contraseña&gt;**,  **&lt; Id. de suscripción&gt;**, y  **&lt;identificador de inquilino&gt;**  con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="2827b-157">In hello App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="2827b-158">Agregue Hola siguiente **con** instrucciones toohello **Program.cs** archivo de proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="2827b-158">Add hello following **using** statements toohello **Program.cs** file in hello project.</span></span>

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. <span data-ttu-id="2827b-159">Agregar Hola después el código que crea una instancia de **DataPipelineManagementClient** clase toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="2827b-159">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="2827b-160">Utilice este objeto toocreate una factoría de datos, un servicio vinculado, los conjuntos de datos de entrada y salida y una canalización.</span><span class="sxs-lookup"><span data-stu-id="2827b-160">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="2827b-161">También se pueden utilizar este sectores de toomonitor de objeto de un conjunto de datos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="2827b-161">You also use this object toomonitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="2827b-162">Reemplazar el valor de Hola de **resourceGroupName** con el nombre de Hola de su grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2827b-162">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span> <span data-ttu-id="2827b-163">Puede crear un grupo de recursos con hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2827b-163">You can create a resource group using hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="2827b-164">Actualizar nombre de hello toobe de fábrica (dataFactoryName) de datos único.</span><span class="sxs-lookup"><span data-stu-id="2827b-164">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="2827b-165">Nombre de la factoría de datos de hello debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="2827b-165">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="2827b-166">Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="2827b-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="2827b-167">Agregar Hola después el código que crea un **factoría de datos** toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="2827b-167">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. <span data-ttu-id="2827b-168">Agregar Hola después el código que crea una **servicio vinculado de almacenamiento de Azure** toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="2827b-168">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="2827b-169">Reemplace **storageaccountname** y **accountkey** por el nombre y la clave de su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2827b-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. <span data-ttu-id="2827b-170">Agregar Hola después el código que crea **conjuntos de datos de entrada y salida** toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="2827b-170">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    <span data-ttu-id="2827b-171">Hola **FolderPath** de blob de entrada de Hola se establece demasiado**adftutorial /** donde **adftutorial** es Hola nombre del contenedor de hello en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="2827b-171">hello **FolderPath** for hello input blob is set too**adftutorial/** where **adftutorial** is hello name of hello container in your blob storage.</span></span> <span data-ttu-id="2827b-172">Si este contenedor no existe en el almacenamiento de blobs de Azure, crear un contenedor con este nombre: **adftutorial** y cargar un contenedor de toohello del archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="2827b-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file toohello container.</span></span>

    <span data-ttu-id="2827b-173">Hola FolderPath para hello de salida blob se establece en: **adftutorial/apifactoryoutput / {Slice}** donde **segmento** es calculada dinámicamente hello en función de valor de **SliceStart**(fecha y hora de cada sector de inicio).</span><span class="sxs-lookup"><span data-stu-id="2827b-173">hello FolderPath for hello output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on hello value of **SliceStart** (start date-time of each slice.)</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. <span data-ttu-id="2827b-174">Agregue los siguiente Hola código que **creará y activará una canalización** toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="2827b-174">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="2827b-175">Esta canalización tiene un elemento **CopyActivity** que toma **BlobSource** como origen y **BlobSink** como receptor.</span><span class="sxs-lookup"><span data-stu-id="2827b-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="2827b-176">Hola actividad de copia realiza el movimiento de datos de hello en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="2827b-176">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="2827b-177">actividad Hello funciona con un servicio disponible globalmente que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable.</span><span class="sxs-lookup"><span data-stu-id="2827b-177">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="2827b-178">Vea [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo para obtener más información acerca de la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="2827b-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need tooset slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. <span data-ttu-id="2827b-179">Agregar Hola después código toohello **Main** conjunto de datos de salida de estado de hello tooget la forma de un segmento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2827b-179">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="2827b-180">Solo se espera un segmento en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2827b-180">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");
        // wait before hello next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. <span data-ttu-id="2827b-181">**(opcional)**  Siguiente de Hola de agregar código tooget ejecutar detalles para un toohello de segmento de datos **Main** método.</span><span class="sxs-lookup"><span data-stu-id="2827b-181">**(optional)** Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="2827b-182">Agregar Hola siguiendo el método auxiliar utilizado por hello **Main** método toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="2827b-182">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span> <span data-ttu-id="2827b-183">Este método abre un cuadro de diálogo que le permite ofrecer **nombre de usuario** y **contraseña** que usar toolog en tooAzure portal.</span><span class="sxs-lookup"><span data-stu-id="2827b-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use toolog in tooAzure portal.</span></span>

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. <span data-ttu-id="2827b-184">Hola el Explorador de soluciones, expanda el proyecto de hello: **DataFactoryAPITestApp**, haga clic en **referencias**y haga clic en **Agregar referencia**.</span><span class="sxs-lookup"><span data-stu-id="2827b-184">In hello Solution Explorer, expand hello project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="2827b-185">Seleccione la casilla del ensamblado de `System.Configuration` y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2827b-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="2827b-186">Compile la aplicación de consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="2827b-186">Build hello console application.</span></span> <span data-ttu-id="2827b-187">Haga clic en **generar** en el menú de Hola y haga clic en **generar solución**.</span><span class="sxs-lookup"><span data-stu-id="2827b-187">Click **Build** on hello menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="2827b-188">Confirme que hay al menos un archivo en el contenedor de adftutorial hello en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="2827b-188">Confirm that there is at least one file in hello adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="2827b-189">Si no es así, crear archivo Emp.txt en el Bloc de notas con hello después de contenido y cargarlo toohello adftutorial contenedor.</span><span class="sxs-lookup"><span data-stu-id="2827b-189">If not, create Emp.txt file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="2827b-190">Ejecutar el ejemplo hello haciendo clic en **depurar** -> **Iniciar depuración** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="2827b-190">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="2827b-191">Cuando vea hello **obtención de detalles de un segmento de datos de la serie**, espere unos minutos y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="2827b-191">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="2827b-192">Use Hola tooverify portal Azure ese factoría de datos de hello **APITutorialFactory** se crea con hello siguientes artefactos:</span><span class="sxs-lookup"><span data-stu-id="2827b-192">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
    * <span data-ttu-id="2827b-193">Servicio vinculado: **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="2827b-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="2827b-194">Conjunto de datos: **DatasetBlobSource** y **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="2827b-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="2827b-195">Canalización: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="2827b-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="2827b-196">Compruebe que se crea un archivo de salida en hello **apifactoryoutput** carpeta Hola **adftutorial** contenedor.</span><span class="sxs-lookup"><span data-stu-id="2827b-196">Verify that an output file is created in hello **apifactoryoutput** folder in hello **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="2827b-197">Obtener una lista de segmentos de datos con errores</span><span class="sxs-lookup"><span data-stu-id="2827b-197">Get a list of failed data slices</span></span> 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a><span data-ttu-id="2827b-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2827b-198">Next steps</span></span>
<span data-ttu-id="2827b-199">Vea Hola siguiente ejemplo para crear una canalización mediante el SDK de .NET que copia datos de una base de datos de SQL Azure del tooan de almacenamiento blob de Azure:</span><span class="sxs-lookup"><span data-stu-id="2827b-199">See hello following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage tooan Azure SQL database:</span></span> 

- [<span data-ttu-id="2827b-200">Crear una canalización de datos de toocopy de almacenamiento de blobs tooSQL base de datos</span><span class="sxs-lookup"><span data-stu-id="2827b-200">Create a pipeline toocopy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
