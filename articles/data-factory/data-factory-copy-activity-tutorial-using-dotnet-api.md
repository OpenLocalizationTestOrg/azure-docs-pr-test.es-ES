---
title: "Tutorial: Crear una canalización con la actividad de copia mediante la API de NET | Microsoft Docs"
description: "En este tutorial, se crea una canalización de Data Factory de Azure con una actividad de copia mediante la API de .NET."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="11e00-103">Tutorial: crear una canalización con la actividad de copia mediante la API de NET</span><span class="sxs-lookup"><span data-stu-id="11e00-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11e00-104">Introducción y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="11e00-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="11e00-105">Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="11e00-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="11e00-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="11e00-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="11e00-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="11e00-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="11e00-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="11e00-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="11e00-109">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="11e00-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="11e00-110">API DE REST</span><span class="sxs-lookup"><span data-stu-id="11e00-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="11e00-111">API de .NET</span><span class="sxs-lookup"><span data-stu-id="11e00-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="11e00-112">En este artículo, aprenderá cómo toouse [API de .NET](https://portal.azure.com) toocreate una factoría de datos con una canalización que copia datos de una base de datos de SQL Azure del tooan de almacenamiento blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="11e00-112">In this article, you learn how toouse [.NET API](https://portal.azure.com) toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="11e00-113">Si es nuevo tooAzure factoría de datos, lea hello [tooAzure Introducción factoría de datos](data-factory-introduction.md) artículo antes de realizar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="11e00-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="11e00-114">En este tutorial, creará una canalización con una actividad en ella: la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="11e00-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="11e00-115">actividad de copia de Hello copia datos de un almacén de datos de datos admitidos almacén tooa receptor admitidos.</span><span class="sxs-lookup"><span data-stu-id="11e00-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="11e00-116">Para obtener una lista de almacenes de datos que se admiten como orígenes y receptores, consulte los [almacenes de datos admitidos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="11e00-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="11e00-117">actividad Hello funciona con un servicio disponible globalmente que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable.</span><span class="sxs-lookup"><span data-stu-id="11e00-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="11e00-118">Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="11e00-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="11e00-119">pero cualquier canalización puede tener más de una actividad.</span><span class="sxs-lookup"><span data-stu-id="11e00-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="11e00-120">Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad.</span><span class="sxs-lookup"><span data-stu-id="11e00-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="11e00-121">Para más información, consulte [Varias actividades en una canalización](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="11e00-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="11e00-122">Para obtener documentación completa sobre la API de .NET para Data Factory, consulte la [referencia de API de .NET de Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="11e00-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="11e00-123">canalización de datos de Hello en este tutorial copia datos de un almacén de datos de destino de origen datos almacén tooa.</span><span class="sxs-lookup"><span data-stu-id="11e00-123">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="11e00-124">Para obtener un tutorial sobre cómo tootransform los datos mediante Data Factory de Azure, consulte [Tutorial: generar una canalización de datos tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="11e00-124">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11e00-125">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="11e00-125">Prerequisites</span></span>
* <span data-ttu-id="11e00-126">Vaya a través de [Tutorial de introducción y los requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget una visión general de tutorial de Hola y Hola completa **prerequisite** pasos.</span><span class="sxs-lookup"><span data-stu-id="11e00-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget an overview of hello tutorial and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="11e00-127">Visual Studio 2012, 2013 o 2015</span><span class="sxs-lookup"><span data-stu-id="11e00-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="11e00-128">Descargue e instale el [SDK de .NET de Azure](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="11e00-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="11e00-129">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="11e00-129">Azure PowerShell.</span></span> <span data-ttu-id="11e00-130">Siga las instrucciones de [cómo tooinstall y configurar Azure PowerShell](../powershell-install-configure.md) artículo tooinstall Azure PowerShell en el equipo.</span><span class="sxs-lookup"><span data-stu-id="11e00-130">Follow instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="11e00-131">Usar PowerShell de Azure toocreate una aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="11e00-131">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="11e00-132">Creación de una aplicación en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11e00-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="11e00-133">Crear una aplicación de Azure Active Directory, cree una entidad de servicio para la aplicación hello y asignar toohello **colaborador de la factoría de datos** rol.</span><span class="sxs-lookup"><span data-stu-id="11e00-133">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="11e00-134">Inicie **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="11e00-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="11e00-135">Ejecute el siguiente comando de Hola y escriba el nombre de usuario de Hola y la contraseña que usa toosign en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="11e00-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="11e00-136">Ejecute hello después comando tooview todas las suscripciones de Hola para esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="11e00-136">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="11e00-137">Ejecute hello después de suscripción de hello tooselect de comando que desee toowork con.</span><span class="sxs-lookup"><span data-stu-id="11e00-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="11e00-138">Reemplace  **&lt;NameOfAzureSubscription** &gt; con el nombre de Hola de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="11e00-138">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="11e00-139">Tenga en cuenta hacia abajo **SubscriptionId** y **TenantId** de salida de hello de este comando.</span><span class="sxs-lookup"><span data-stu-id="11e00-139">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="11e00-140">Crear un grupo de recursos de Azure denominado **ADFTutorialResourceGroup** ejecutando Hola siguiente comando en hello PowerShell.</span><span class="sxs-lookup"><span data-stu-id="11e00-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="11e00-141">Si ya existe el grupo de recursos de hello, especifique si tooupdate se (Y) o mantener un nivel tan (N).</span><span class="sxs-lookup"><span data-stu-id="11e00-141">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="11e00-142">Si utiliza un grupo de recursos diferente, necesita toouse Hola nombre de su grupo de recursos en lugar de ADFTutorialResourceGroup en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="11e00-142">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="11e00-143">Cree una aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="11e00-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="11e00-144">Si se producen Hola tras error, especifique una URL distinta y vuelva a ejecutar el comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="11e00-144">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="11e00-145">Crear Hola la entidad de servicio de AD.</span><span class="sxs-lookup"><span data-stu-id="11e00-145">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="11e00-146">Agregar servicio principal toohello **colaborador de la factoría de datos** rol.</span><span class="sxs-lookup"><span data-stu-id="11e00-146">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="11e00-147">Obtener el identificador de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="11e00-147">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="11e00-148">Anote el identificador de la aplicación de hello (applicationID) de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="11e00-148">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="11e00-149">Debe tener los cuatro valores siguientes de estos pasos:</span><span class="sxs-lookup"><span data-stu-id="11e00-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="11e00-150">Id. de inquilino</span><span class="sxs-lookup"><span data-stu-id="11e00-150">Tenant ID</span></span>
* <span data-ttu-id="11e00-151">Id. de suscripción</span><span class="sxs-lookup"><span data-stu-id="11e00-151">Subscription ID</span></span>
* <span data-ttu-id="11e00-152">Identificador de aplicación</span><span class="sxs-lookup"><span data-stu-id="11e00-152">Application ID</span></span>
* <span data-ttu-id="11e00-153">Contraseña (especificada en el primer comando de hello)</span><span class="sxs-lookup"><span data-stu-id="11e00-153">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="11e00-154">Tutorial</span><span class="sxs-lookup"><span data-stu-id="11e00-154">Walkthrough</span></span>
1. <span data-ttu-id="11e00-155">Con Visual Studio 2012, 2013 o 2015, cree una aplicación de consola .NET de C#.</span><span class="sxs-lookup"><span data-stu-id="11e00-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="11e00-156">Inicie **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="11e00-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="11e00-157">Haga clic en **archivo**, seleccione demasiado**New**y haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="11e00-157">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="11e00-158">Expanda **Plantillas** y seleccione **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="11e00-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="11e00-159">En este tutorial, se usa C# pero puede usar cualquier lenguaje .NET.</span><span class="sxs-lookup"><span data-stu-id="11e00-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="11e00-160">Seleccione **aplicación de consola** de lista de Hola de tipos de proyecto en hello derecho.</span><span class="sxs-lookup"><span data-stu-id="11e00-160">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="11e00-161">Escriba **DataFactoryAPITestApp** para hello nombre.</span><span class="sxs-lookup"><span data-stu-id="11e00-161">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="11e00-162">Seleccione **C:\ADFGetStarted** para hello ubicación.</span><span class="sxs-lookup"><span data-stu-id="11e00-162">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="11e00-163">Haga clic en **Aceptar** proyecto de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="11e00-163">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="11e00-164">Haga clic en **herramientas**, seleccione demasiado**Administrador de paquetes de NuGet**y haga clic en **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="11e00-164">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="11e00-165">Hola **Package Manager Console**, Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="11e00-165">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="11e00-166">Ejecute hello después el paquete de comando tooinstall factoría de datos:`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="11e00-166">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="11e00-167">Ejecute hello después el paquete de Azure Active Directory tooinstall command (usar API de Active Directory en el código de hello):`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="11e00-167">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="11e00-168">Agregue los siguiente hello **appSetttings** sección toohello **App.config** archivo.</span><span class="sxs-lookup"><span data-stu-id="11e00-168">Add hello following **appSetttings** section toohello **App.config** file.</span></span> <span data-ttu-id="11e00-169">Esta configuración se usa por el método de aplicación auxiliar de hello: **GetAuthorizationHeader**.</span><span class="sxs-lookup"><span data-stu-id="11e00-169">These settings are used by hello helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="11e00-170">Reemplace los valores de **&lt;Id. de aplicación&gt;**, **&lt;Contraseña&gt;**, **&lt;Id. de suscripción&gt;** e **&lt;Id. de inquilino&gt;** por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="11e00-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

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

5. <span data-ttu-id="11e00-171">Agregue los siguiente hello **con** el archivo de código fuente de toohello de instrucciones (Program.cs) en el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="11e00-171">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

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

6. <span data-ttu-id="11e00-172">Agregar Hola después el código que crea una instancia de **DataPipelineManagementClient** clase toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="11e00-172">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="11e00-173">Utilice este objeto toocreate una factoría de datos, un servicio vinculado, los conjuntos de datos de entrada y salida y una canalización.</span><span class="sxs-lookup"><span data-stu-id="11e00-173">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="11e00-174">También se pueden utilizar este sectores de toomonitor de objeto de un conjunto de datos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="11e00-174">You also use this object toomonitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="11e00-175">Reemplazar el valor de Hola de **resourceGroupName** con el nombre de Hola de su grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="11e00-175">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="11e00-176">Actualizar nombre de hello toobe de fábrica (dataFactoryName) de datos único.</span><span class="sxs-lookup"><span data-stu-id="11e00-176">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="11e00-177">Nombre de la factoría de datos de hello debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="11e00-177">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="11e00-178">Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="11e00-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="11e00-179">Agregar Hola después el código que crea un **factoría de datos** toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="11e00-179">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

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

    <span data-ttu-id="11e00-180">Una factoría de datos puede tener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="11e00-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="11e00-181">Una canalización puede tener una o más actividades.</span><span class="sxs-lookup"><span data-stu-id="11e00-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="11e00-182">Por ejemplo, una toocopy de datos de actividad de copia de un almacén de datos de origen tooa destino y un toorun de actividad de Hive de HDInsight un tootransform de script de Hive datos de salida de tooproduct de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="11e00-182">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="11e00-183">Puede empezar con la creación de factoría de datos de hello en este paso.</span><span class="sxs-lookup"><span data-stu-id="11e00-183">Let's start with creating hello data factory in this step.</span></span>
8. <span data-ttu-id="11e00-184">Agregar Hola después el código que crea una **servicio vinculado de almacenamiento de Azure** toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="11e00-184">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="11e00-185">Reemplace **storageaccountname** y **accountkey** por el nombre y la clave de su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="11e00-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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

    <span data-ttu-id="11e00-186">Crear servicios vinculados en un toolink de factoría de datos almacenan sus datos y se factoría de datos de toohello de servicios de proceso.</span><span class="sxs-lookup"><span data-stu-id="11e00-186">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="11e00-187">En este tutorial, no se usa ningún servicio de proceso, como Azure HDInsight o Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="11e00-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="11e00-188">Se usan dos almacenes de datos del tipo Azure Storage (origen) y Azure SQL Database (destino).</span><span class="sxs-lookup"><span data-stu-id="11e00-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="11e00-189">Por lo tanto, se crean dos servicios vinculados llamados AzureStorageLinkedService y AzureSqlLinkedService del tipo AzureStorage y AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="11e00-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="11e00-190">Hola AzureStorageLinkedService vincula su factoría de datos de toohello de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="11e00-190">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="11e00-191">Esta cuenta de almacenamiento es hello uno en el que se creó un contenedor y cargar datos de hello como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="11e00-191">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="11e00-192">Agregar Hola después el código que crea una **servicio vinculado de SQL Azure** toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="11e00-192">Add hello following code that creates an **Azure SQL linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="11e00-193">Reemplace **servername**, **databasename**, **username** y **password** por los nombres del servidor de Azure SQL, de la base de datos, del usuario y de la contraseña.</span><span class="sxs-lookup"><span data-stu-id="11e00-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    <span data-ttu-id="11e00-194">AzureSqlLinkedService vincula su factoría de datos de toohello de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="11e00-194">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="11e00-195">datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="11e00-195">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="11e00-196">Crear tabla emp de hello en esta base de datos como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="11e00-196">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="11e00-197">Agregar Hola después el código que crea **conjuntos de datos de entrada y salida** toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="11e00-197">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
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

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
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
    
    <span data-ttu-id="11e00-198">En el paso anterior de hello, crear servicios vinculados toolink su cuenta de almacenamiento de Azure y la factoría de datos de tooyour de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="11e00-198">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="11e00-199">En este paso, definirá dos conjuntos de datos con el nombre InputDataset y OutputDataset que representan la entrada y los datos de salida que se almacenan en almacenes de datos de Hola que hace referencia AzureStorageLinkedService y AzureSqlLinkedService respectivamente.</span><span class="sxs-lookup"><span data-stu-id="11e00-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="11e00-200">servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="11e00-200">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="11e00-201">Y conjunto de datos de blob de entrada de hello (InputDataset) especifica contenedor de Hola y la carpeta de Hola que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="11e00-201">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="11e00-202">De forma similar, Hola servicio de base de datos de Azure SQL vinculado especifica cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="11e00-202">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="11e00-203">Y conjunto de datos de tabla SQL (OututDataset) especifica la tabla de Hola Hola Hola de toowhich de base de datos se copian datos desde almacenamiento de blobs de Hola de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="11e00-203">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

    <span data-ttu-id="11e00-204">En este paso, creará un conjunto de datos denominado InputDataset que apunta a un archivo blob tooa (emp.txt) en la carpeta raíz de Hola de un contenedor de blobs (adftutorial) en hello representado por hello AzureStorageLinkedService vinculado servicio de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="11e00-204">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="11e00-205">Si no especifica un valor para el nombre de archivo de hello (o puede omitirla), datos de todos los blobs en la carpeta de entrada de hello son destino toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="11e00-205">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="11e00-206">En este tutorial, especifique un valor para el nombre de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="11e00-206">In this tutorial, you specify a value for hello fileName.</span></span>    

    <span data-ttu-id="11e00-207">En este paso se crea un conjunto de datos de salida denominado **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="11e00-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="11e00-208">Este conjunto de datos señala tooa table de SQL de base de datos de SQL Azure de hello representado por **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="11e00-208">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="11e00-209">Agregue los siguiente Hola código que **creará y activará una canalización** toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="11e00-209">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="11e00-210">En este paso, creará una canalización con una **actividad de copia** que utiliza **InputDataset** como entrada y **OutputDataset** como salida.</span><span class="sxs-lookup"><span data-stu-id="11e00-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

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
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
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
                    }
                }
            }
        });
    ```

    <span data-ttu-id="11e00-211">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="11e00-211">Note hello following points:</span></span>
   
    - <span data-ttu-id="11e00-212">En la sección de actividades de hello, hay sólo una actividad cuyo **tipo** se establece demasiado**copia**.</span><span class="sxs-lookup"><span data-stu-id="11e00-212">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="11e00-213">Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="11e00-213">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="11e00-214">En las soluciones de Data Factory, también puede usar [actividades de transformación de datos](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="11e00-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="11e00-215">Entrada de actividad hello se establece demasiado**InputDataset** y salida de actividad hello se establece demasiado**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="11e00-215">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="11e00-216">Hola **typeProperties** sección, **BlobSource** se especifica como tipo de origen de Hola y **SqlSink** se especifica como el tipo de receptor de Hola.</span><span class="sxs-lookup"><span data-stu-id="11e00-216">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="11e00-217">Para obtener una lista completa de los almacenes de datos compatibles con la actividad de copia de hello como orígenes y receptores, vea [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="11e00-217">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="11e00-218">toolearn cómo almacenar toouse datos compatibles especificados como un origen/receptor, haga clic en el vínculo hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="11e00-218">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
   
    <span data-ttu-id="11e00-219">Actualmente, el conjunto de datos de salida es qué unidades Hola programación.</span><span class="sxs-lookup"><span data-stu-id="11e00-219">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="11e00-220">En este tutorial, el conjunto de datos de salida es tooproduce configurado un segmento una vez cada hora.</span><span class="sxs-lookup"><span data-stu-id="11e00-220">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="11e00-221">canalización de Hello tiene una hora de inicio y la hora de finalización que son un día separado, lo que es de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="11e00-221">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="11e00-222">Por lo tanto, 24 segmentos del conjunto de datos de salida generados por la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="11e00-222">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span>
12. <span data-ttu-id="11e00-223">Agregar Hola después código toohello **Main** conjunto de datos de salida de estado de hello tooget la forma de un segmento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11e00-223">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="11e00-224">Solo se espera un segmento en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="11e00-224">There is only slice expected in this sample.</span></span>

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

13. <span data-ttu-id="11e00-225">Agregar código tooget ejecutar detalles para un toohello de segmento de datos siguientes de Hola **Main** método.</span><span class="sxs-lookup"><span data-stu-id="11e00-225">Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

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
            }
        );

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

14. <span data-ttu-id="11e00-226">Agregar Hola siguiendo el método auxiliar utilizado por hello **Main** método toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="11e00-226">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="11e00-227">Cuando copie y pegue el siguiente código de hello, asegúrese de que ese Hola copiado el código está en hello como Hola método Main de mismo nivel.</span><span class="sxs-lookup"><span data-stu-id="11e00-227">When you copy and paste hello following code, make sure that hello copied code is at hello same level as hello Main method.</span></span>

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

15. <span data-ttu-id="11e00-228">En hello en el Explorador de soluciones, expanda el proyecto de hello (DataFactoryAPITestApp), haga clic en **referencias**y haga clic en **Agregar referencia**.</span><span class="sxs-lookup"><span data-stu-id="11e00-228">In hello Solution Explorer, expand hello project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="11e00-229">Active la casilla del ensamblado **System.Configuration**.</span><span class="sxs-lookup"><span data-stu-id="11e00-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="11e00-230">Después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="11e00-230">and click **OK**.</span></span>
16. <span data-ttu-id="11e00-231">Compile la aplicación de consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="11e00-231">Build hello console application.</span></span> <span data-ttu-id="11e00-232">Haga clic en **generar** en el menú de Hola y haga clic en **generar solución**.</span><span class="sxs-lookup"><span data-stu-id="11e00-232">Click **Build** on hello menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="11e00-233">Confirme que hay al menos un archivo en hello **adftutorial** contenedor en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="11e00-233">Confirm that there is at least one file in hello **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="11e00-234">Si no es así, cree **Emp.txt** de archivos en el Bloc de notas con hello siguen contenido y cargarlo toohello adftutorial contenedor.</span><span class="sxs-lookup"><span data-stu-id="11e00-234">If not, create **Emp.txt** file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="11e00-235">Ejecutar el ejemplo hello haciendo clic en **depurar** -> **Iniciar depuración** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="11e00-235">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="11e00-236">Cuando vea hello **obtención de detalles de un segmento de datos de la serie**, espere unos minutos y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="11e00-236">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="11e00-237">Use Hola tooverify portal Azure ese factoría de datos de hello **APITutorialFactory** se crea con hello siguientes artefactos:</span><span class="sxs-lookup"><span data-stu-id="11e00-237">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
   * <span data-ttu-id="11e00-238">Servicio vinculado: **LinkedService_AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="11e00-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="11e00-239">Conjunto de datos: **InputDataset** y **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="11e00-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="11e00-240">Canalización: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="11e00-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="11e00-241">Compruebe que se crean los registros de empleados Hola dos en hello **emp** tabla Hola especifica la base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="11e00-241">Verify that hello two employee records are created in hello **emp** table in hello specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11e00-242">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="11e00-242">Next steps</span></span>
<span data-ttu-id="11e00-243">Para obtener documentación completa sobre la API de .NET para Data Factory, consulte la [referencia de API de .NET de Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="11e00-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="11e00-244">En este tutorial, ha usado Azure Blob Storage como almacén de datos de origen y una base de datos SQL de Azure como almacén de datos de destino en una operación de copia.</span><span class="sxs-lookup"><span data-stu-id="11e00-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="11e00-245">Hello tabla siguiente proporciona una lista de almacenes de datos que se admiten como orígenes y destinos por actividad de copia de hello:</span><span class="sxs-lookup"><span data-stu-id="11e00-245">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="11e00-246">toolearn acerca de cómo almacenan datos toocopy de datos, haga clic en vínculo Hola Hola de almacén de datos en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="11e00-246">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>

