---
title: "Implementación de una aplicación web con MSDeploy con un nombre de host personalizado y un certificado SSL"
description: "Use una plantilla del Administrador de recursos de Azure para implementar una aplicación web mediante MSDeploy y configurar un nombre de host personalizado y un certificado SSL"
services: app-service\web
manager: erikre
documentationcenter: 
author: jodehavi
ms.assetid: 66366a72-cef7-4d75-8779-f4d32ed33cf7
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2016
ms.author: jodehavi
ms.openlocfilehash: a0e944d0d74ecb72a919538d54db330cbbdeef64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="4b981-103">Implementación de una aplicación web con MSDeploy, un nombre de host personalizado y un certificado SSL</span><span class="sxs-lookup"><span data-stu-id="4b981-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="4b981-104">En esta guía, se recorre el proceso de crear una implementación integral para una aplicación web de Azure, sacar provecho de MSDeploy, así como agregar un nombre de host personalizado y un certificado SSL a la plantilla de ARM.</span><span class="sxs-lookup"><span data-stu-id="4b981-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate to the ARM template.</span></span>

<span data-ttu-id="4b981-105">Para obtener más información sobre la creación de plantillas, consulte [Creación de plantillas de Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4b981-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="4b981-106">Creación de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4b981-106">Create Sample Application</span></span>
<span data-ttu-id="4b981-107">Va a implementar una aplicación web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4b981-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="4b981-108">El primer paso consiste en crear una aplicación web sencilla (o puede elegir usar una existente, en cuyo caso puede omitir este paso).</span><span class="sxs-lookup"><span data-stu-id="4b981-108">The first step is to create a simple web application (or you could choose to use an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="4b981-109">Abra Visual Studio 2015 y seleccione Archivo > Nuevo proyecto.</span><span class="sxs-lookup"><span data-stu-id="4b981-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="4b981-110">En el cuadro de diálogo que aparece, elija Web > Aplicación web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4b981-110">On the dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="4b981-111">En Plantillas, elija Web y después la plantilla MVC.</span><span class="sxs-lookup"><span data-stu-id="4b981-111">Under Templates choose Web and choose the MVC template.</span></span> <span data-ttu-id="4b981-112">En *Change authentication type* (Cambiar tipo de autenticación), seleccione *No Authentication* (Sin autenticación).</span><span class="sxs-lookup"><span data-stu-id="4b981-112">Select *Change authentication type* to *No Authentication*.</span></span> <span data-ttu-id="4b981-113">Esto es solo para hacer la aplicación de ejemplo tan sencilla como sea posible.</span><span class="sxs-lookup"><span data-stu-id="4b981-113">This is just to make the sample application as simple as possible.</span></span>

<span data-ttu-id="4b981-114">En este punto, tendrá una aplicación web ASP.NET básica lista para usarla como parte del proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="4b981-114">At this point you will have a basic ASP.Net web app ready to use as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="4b981-115">Creación del paquete MSDeploy</span><span class="sxs-lookup"><span data-stu-id="4b981-115">Create MSDeploy package</span></span>
<span data-ttu-id="4b981-116">El siguiente paso consiste en crear el paquete para implementar la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="4b981-116">Next step is to create the package to deploy the web app to Azure.</span></span> <span data-ttu-id="4b981-117">Para ello, guarde el proyecto y después ejecute lo siguiente en la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="4b981-117">To do this, save your project and then run the following from the command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="4b981-118">Esto creará un paquete comprimido en la carpeta PackageLocation.</span><span class="sxs-lookup"><span data-stu-id="4b981-118">This will create a zipped package under the PackageLocation folder.</span></span> <span data-ttu-id="4b981-119">La aplicación está lista para implementarse y ahora puede crear una plantilla del Administrador de recursos de Azure para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="4b981-119">The application is now ready to be deployed, which you can now build out an Azure Resource Manager template to do that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="4b981-120">Creación de la plantilla de ARM</span><span class="sxs-lookup"><span data-stu-id="4b981-120">Create ARM Template</span></span>
<span data-ttu-id="4b981-121">En primer lugar, vamos a comenzar con una plantilla de ARM básica que creará una aplicación web y un plan de hospedaje (tenga en cuenta que no se muestran los parámetros ni las variables por brevedad).</span><span class="sxs-lookup"><span data-stu-id="4b981-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

    {
        "name": "[parameters('appServicePlanName')]",
        "type": "Microsoft.Web/serverfarms",
        "location": "[resourceGroup().location]",
        "apiVersion": "2014-06-01",
        "dependsOn": [ ],
        "tags": {
            "displayName": "appServicePlan"
        },
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "sku": "[parameters('appServicePlanSKU')]",
            "workerSize": "[parameters('appServicePlanWorkerSize')]",
            "numberOfWorkers": 1
        }
    },
    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        }
    }

<span data-ttu-id="4b981-122">A continuación, debe modificar el recurso de la aplicación web para que admita un recurso de MSDeploy anidado.</span><span class="sxs-lookup"><span data-stu-id="4b981-122">Next, you will need to modify the web app resource to take a nested MSDeploy resource.</span></span> <span data-ttu-id="4b981-123">Esto le permitirá hacer referencia al paquete creado antes e indicar al Administrador de recursos de Azure que use MSDeploy para implementar el paquete en la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b981-123">This will allow you to reference the package created earlier and tell Azure Resource Manager to use MSDeploy to deploy the package to the Azure WebApp.</span></span> <span data-ttu-id="4b981-124">A continuación, se muestra el recurso Microsoft.Web/sites con el recurso de MSDeploy anidado:</span><span class="sxs-lookup"><span data-stu-id="4b981-124">The following shows the Microsoft.Web/sites resource with the nested MSDeploy resource:</span></span>

    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        },
        "resources": [
            {
                "name": "MSDeploy",
                "type": "extensions",
                "location": "[resourceGroup().location]",
                "apiVersion": "2015-08-01",
                "dependsOn": [
                    "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
                ],
                "tags": {
                    "displayName": "webDeploy"
                },
                "properties": {
                    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]",
                    "dbType": "None",
                    "connectionString": "",
                    "setParameters": {
                        "IIS Web Application Name": "[variables('webAppName')]"
                    }
                }
            }
        ]
    }

<span data-ttu-id="4b981-125">Ahora verá que el recurso de MSDeploy admite una propiedad **packageUri** que se define como sigue:</span><span class="sxs-lookup"><span data-stu-id="4b981-125">Now you will notice that the MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="4b981-126">Esta propiedad **packageUri** admite el identificador URI de la cuenta de almacenamiento que apunta a la cuenta de almacenamiento donde se cargará el archivo comprimido del paquete.</span><span class="sxs-lookup"><span data-stu-id="4b981-126">This **packageUri** takes the storage account uri which points to the storage account where you will upload your package zip to.</span></span> <span data-ttu-id="4b981-127">El Administrador de recursos de Azure aprovechará las [firmas de acceso compartido](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para descargar el paquete localmente desde la cuenta de almacenamiento cuando se implemente la plantilla.</span><span class="sxs-lookup"><span data-stu-id="4b981-127">The Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to pull the package down locally from the storage account when you deploy the template.</span></span> <span data-ttu-id="4b981-128">Este proceso se automatizará mediante un script de PowerShell que cargará el paquete y llamará a la API de administración de Azure para crear las claves requeridas y pasarlas a la plantilla como parámetros (*_artifactsLocation* y *_artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="4b981-128">This process will be automated via a PowerShell script that will upload the package and call the Azure Management API to create the keys required and pass those into the template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="4b981-129">Debe definir los parámetros de la carpeta y el nombre de archivo donde se carga el paquete en el contenedor de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4b981-129">You will need to define parameters for the folder and filename the package is uploaded to under the storage container.</span></span>

<span data-ttu-id="4b981-130">Después, debe agregar otro recurso anidado para configurar los enlaces de nombre de host para sacar provecho de un dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="4b981-130">Next you need to add in another nested resource to setup the hostname bindings to leverage a custom domain.</span></span> <span data-ttu-id="4b981-131">En primer lugar, deberá asegurarse de que posee el nombre de host y configurarlo para que Azure compruebe que en efecto lo posee; consulte [Configurar un nombre de dominio personalizado en el Servicio de aplicaciones de Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="4b981-131">You will first need to ensure that you own the hostname and set it up to be verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="4b981-132">Una vez hecho esto, puede agregar lo siguiente a la plantilla en la sección de recursos Microsoft.Web/sites:</span><span class="sxs-lookup"><span data-stu-id="4b981-132">Once that is done you can add the following to your template under the Microsoft.Web/sites resource section:</span></span>

    {
        "apiVersion": "2015-08-01",
        "type": "hostNameBindings",
        "name": "www.yourcustomdomain.com",
        "dependsOn": [
            "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
        ],
        "properties": {
            "domainId": null,
            "hostNameType": "Verified",
            "siteName": "variables('webAppName')"
        }
    }

<span data-ttu-id="4b981-133">Por último, debe agregar otro recurso de nivel superior, Microsoft.Web/certificates.</span><span class="sxs-lookup"><span data-stu-id="4b981-133">Finally you need to add another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="4b981-134">Este recurso contendrá su certificado SSL y se encontrará en el mismo nivel que la aplicación web y el plan de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="4b981-134">This resource will contain your SSL certificate and will exist at the same level as your web app and hosting plan.</span></span>

    {
        "name": "[parameters('certificateName')]",
        "apiVersion": "2014-04-01",
        "type": "Microsoft.Web/certificates",
        "location": "[resourceGroup().location]",
        "properties": {
            "pfxBlob": "pfx base64 blob",
            "password": "some pass"
        }
    }

<span data-ttu-id="4b981-135">Debe tener un certificado SSL válido para configurar este recurso.</span><span class="sxs-lookup"><span data-stu-id="4b981-135">You will need to have a valid SSL certificate in order to set up this resource.</span></span> <span data-ttu-id="4b981-136">Una vez que tenga ese certificado válido, debe extraer los bytes pfx como una cadena de base64.</span><span class="sxs-lookup"><span data-stu-id="4b981-136">Once you have that valid certificate then you need to extract the pfx bytes as a base64 string.</span></span> <span data-ttu-id="4b981-137">Una opción para extraerlos es usar el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4b981-137">One option to extract this is to use the following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="4b981-138">Después podría pasarlos como parámetro a la plantilla de implementación de ARM.</span><span class="sxs-lookup"><span data-stu-id="4b981-138">You could then pass this as a parameter to your ARM deployment template.</span></span>

<span data-ttu-id="4b981-139">En este punto, la plantilla de ARM está lista.</span><span class="sxs-lookup"><span data-stu-id="4b981-139">At this point the ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="4b981-140">Implementar plantilla</span><span class="sxs-lookup"><span data-stu-id="4b981-140">Deploy Template</span></span>
<span data-ttu-id="4b981-141">Los pasos finales sirven para juntar todo en una implementación integral completa.</span><span class="sxs-lookup"><span data-stu-id="4b981-141">The final steps are to piece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="4b981-142">Para facilitar la implementación, puede aprovechar el script de PowerShell **Deploy-AzureResourceGroup.ps1** que se agrega al crear un proyecto de grupo de recursos de Azure en Visual Studio para ayudar con la carga de los artefactos necesarios en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="4b981-142">To make deployment easier you can leverage the **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio to help with uploading of any artifacts required in the template.</span></span> <span data-ttu-id="4b981-143">Es necesario crear la cuenta de almacenamiento que desee usar con antelación.</span><span class="sxs-lookup"><span data-stu-id="4b981-143">It requires you to have created a storage account you want to use ahead of time.</span></span> <span data-ttu-id="4b981-144">En este ejemplo, he creado una cuenta de almacenamiento compartido en la que cargar el archivo package.zip.</span><span class="sxs-lookup"><span data-stu-id="4b981-144">For this example, I created a shared storage account for the package.zip to be uploaded.</span></span> <span data-ttu-id="4b981-145">El script hará uso de AzCopy para cargar el paquete en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4b981-145">The script will leverage AzCopy to upload the package to the storage account.</span></span> <span data-ttu-id="4b981-146">Se pasa la ubicación de la carpeta de artefactos y el script cargará automáticamente todos los archivos de ese directorio en el contenedor de almacenamiento con nombre.</span><span class="sxs-lookup"><span data-stu-id="4b981-146">You pass in your artifact folder location and the script will automatically upload all files within that directory to the named storage container.</span></span> <span data-ttu-id="4b981-147">Después de llamar a Deploy-AzureResourceGroup.ps1, tendrá que actualizar los enlaces SSL para asignar el nombre de host personalizado a su certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="4b981-147">After calling Deploy-AzureResourceGroup.ps1 you have to then update the SSL bindings to map the custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="4b981-148">El siguiente script de PowerShell muestra la implementación completa con una llamada a Deploy-AzureResourceGroup.ps1:</span><span class="sxs-lookup"><span data-stu-id="4b981-148">The following PowerShell shows the complete deployment calling the Deploy-AzureResourceGroup.ps1:</span></span>

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script to deploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app to bind ssl certificate to hostname. This has to be done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

<span data-ttu-id="4b981-149">En este momento, se debería haber implementado la aplicación y debería poder ir a ella mediante https://www.yourcustomdomain.com</span><span class="sxs-lookup"><span data-stu-id="4b981-149">At this point your application should have been deployed and you should be able to browse to it via https://www.yourcustomdomain.com</span></span>

