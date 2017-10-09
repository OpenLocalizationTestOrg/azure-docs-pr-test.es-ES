---
title: "aaaDeploy una aplicación web con MSDeploy con certificado ssl y el nombre de host"
description: "Usar un toodeploy de plantilla de Azure Resource Manager en una aplicación web usando MSDeploy y configurar un certificado SSL y un nombre de host personalizado"
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
ms.openlocfilehash: ac13f4a7d14ae182e8e7ced5adff30491422d1e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="a0ae5-103">Implementación de una aplicación web con MSDeploy, un nombre de host personalizado y un certificado SSL</span><span class="sxs-lookup"><span data-stu-id="a0ae5-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="a0ae5-104">Esta guía se describen la creación de una implementación de extremo a extremo de una aplicación Web de Azure, aprovechar MSDeploy, así como agregar un nombre de host personalizado y una plantilla de ARM de toohello de certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate toohello ARM template.</span></span>

<span data-ttu-id="a0ae5-105">Para obtener más información sobre la creación de plantillas, consulte [Creación de plantillas de Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a0ae5-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="a0ae5-106">Creación de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a0ae5-106">Create Sample Application</span></span>
<span data-ttu-id="a0ae5-107">Va a implementar una aplicación web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="a0ae5-108">Hola primer paso es toocreate una aplicación web simple (o puede elegir toouse uno ya existente; en cuyo caso, puede omitir este paso).</span><span class="sxs-lookup"><span data-stu-id="a0ae5-108">hello first step is toocreate a simple web application (or you could choose toouse an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="a0ae5-109">Abra Visual Studio 2015 y seleccione Archivo > Nuevo proyecto.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="a0ae5-110">En el cuadro de diálogo de Hola que aparece, elija Web > aplicación Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-110">On hello dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="a0ae5-111">En plantillas elija Web y elija la plantilla MVC Hola.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-111">Under Templates choose Web and choose hello MVC template.</span></span> <span data-ttu-id="a0ae5-112">Seleccione *cambiar el tipo de autenticación* demasiado*sin autenticación*.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-112">Select *Change authentication type* too*No Authentication*.</span></span> <span data-ttu-id="a0ae5-113">Esto es simplemente toomake Hola aplicación de ejemplo tan simple como sea posible.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-113">This is just toomake hello sample application as simple as possible.</span></span>

<span data-ttu-id="a0ae5-114">En este momento tendrá un toouse listo de ASP.Net web app básica como parte del proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-114">At this point you will have a basic ASP.Net web app ready toouse as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="a0ae5-115">Creación del paquete MSDeploy</span><span class="sxs-lookup"><span data-stu-id="a0ae5-115">Create MSDeploy package</span></span>
<span data-ttu-id="a0ae5-116">Siguiente paso es toocreate Hola paquete toodeploy hello web app tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-116">Next step is toocreate hello package toodeploy hello web app tooAzure.</span></span> <span data-ttu-id="a0ae5-117">toodo, guarde el proyecto y, a continuación, ejecute el siguiente de Hola desde línea de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="a0ae5-117">toodo this, save your project and then run hello following from hello command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="a0ae5-118">Esto creará un paquete comprimido en la carpeta de PackageLocation Hola.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-118">This will create a zipped package under hello PackageLocation folder.</span></span> <span data-ttu-id="a0ae5-119">Hello aplicación está ahora listo toobe implementado, que ahora puede crear un toodo de plantilla de Azure Resource Manager que.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-119">hello application is now ready toobe deployed, which you can now build out an Azure Resource Manager template toodo that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="a0ae5-120">Creación de la plantilla de ARM</span><span class="sxs-lookup"><span data-stu-id="a0ae5-120">Create ARM Template</span></span>
<span data-ttu-id="a0ae5-121">En primer lugar, vamos a comenzar con una plantilla de ARM básica que creará una aplicación web y un plan de hospedaje (tenga en cuenta que no se muestran los parámetros ni las variables por brevedad).</span><span class="sxs-lookup"><span data-stu-id="a0ae5-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

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

<span data-ttu-id="a0ae5-122">A continuación, deberá toomodify hello web app recursos tootake un recurso anidado de MSDeploy.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-122">Next, you will need toomodify hello web app resource tootake a nested MSDeploy resource.</span></span> <span data-ttu-id="a0ae5-123">Esto permitirá tooreference Hola paquete creado anteriormente y saber Azure Resource Manager toouse MSDeploy toodeploy Hola paquete toohello WebApp de Azure.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-123">This will allow you tooreference hello package created earlier and tell Azure Resource Manager toouse MSDeploy toodeploy hello package toohello Azure WebApp.</span></span> <span data-ttu-id="a0ae5-124">siguiente Hola muestra Hola de recursos de Microsoft.Web/sites con recursos de MSDeploy Hola anidado:</span><span class="sxs-lookup"><span data-stu-id="a0ae5-124">hello following shows hello Microsoft.Web/sites resource with hello nested MSDeploy resource:</span></span>

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

<span data-ttu-id="a0ae5-125">Ahora observará ese Hola MSDeploy recurso toma una **packageUri** propiedad que se define como sigue:</span><span class="sxs-lookup"><span data-stu-id="a0ae5-125">Now you will notice that hello MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="a0ae5-126">Esto **packageUri** toma Hola uri de la cuenta de almacenamiento que señala toohello cuenta de almacenamiento donde se cargará el zip de paquete a.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-126">This **packageUri** takes hello storage account uri which points toohello storage account where you will upload your package zip to.</span></span> <span data-ttu-id="a0ae5-127">Hello Azure Resource Manager aprovecharán [firmas de acceso compartido](../storage/common/storage-dotnet-shared-access-signature-part-1.md) paquete de hello toopull hacia abajo localmente desde la cuenta de almacenamiento de hello al implementar la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-127">hello Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull hello package down locally from hello storage account when you deploy hello template.</span></span> <span data-ttu-id="a0ae5-128">Este proceso se automatiza a través de una secuencia de comandos de PowerShell que cargar paquete de Hola y llamar a Hola API de administración de Azure toocreate hello las claves se requieren y en la plantilla de hello pasar como parámetros (*_artifactsLocation* y *_artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="a0ae5-128">This process will be automated via a PowerShell script that will upload hello package and call hello Azure Management API toocreate hello keys required and pass those into hello template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="a0ae5-129">Necesitará toodefine parámetros para la carpeta de Hola y nombre de archivo paquete de hello es el contenedor de almacenamiento de Hola de toounder cargado.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-129">You will need toodefine parameters for hello folder and filename hello package is uploaded toounder hello storage container.</span></span>

<span data-ttu-id="a0ae5-130">A continuación debe tooadd en otro recurso anidado toosetup Hola hostname enlaces tooleverage un dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-130">Next you need tooadd in another nested resource toosetup hello hostname bindings tooleverage a custom domain.</span></span> <span data-ttu-id="a0ae5-131">Que se van a primera tooensure de necesidad que posee el nombre de host de Hola y configurarla toobe Azure comprobado que usted es el propietario: vea [configurar un nombre de dominio personalizado en el servicio de aplicación de Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="a0ae5-131">You will first need tooensure that you own hello hostname and set it up toobe verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="a0ae5-132">Una vez que se hace puede agregar Hola sigue tooyour template en la sección de recursos de Hola Microsoft.Web/sites:</span><span class="sxs-lookup"><span data-stu-id="a0ae5-132">Once that is done you can add hello following tooyour template under hello Microsoft.Web/sites resource section:</span></span>

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

<span data-ttu-id="a0ae5-133">Por último, debe tooadd otro recurso de nivel superior, Microsoft.Web/certificates.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-133">Finally you need tooadd another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="a0ae5-134">Este recurso contendrá su certificado SSL y seguirán existiendo en el plan de mismo nivel que la aplicación web y el hospedaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-134">This resource will contain your SSL certificate and will exist at hello same level as your web app and hosting plan.</span></span>

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

<span data-ttu-id="a0ae5-135">Deberá toohave un certificado SSL válido en orden tooset este recurso.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-135">You will need toohave a valid SSL certificate in order tooset up this resource.</span></span> <span data-ttu-id="a0ae5-136">Una vez que tenga ese certificado válido debe bytes de pfx hello tooextract como una cadena de base64.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-136">Once you have that valid certificate then you need tooextract hello pfx bytes as a base64 string.</span></span> <span data-ttu-id="a0ae5-137">Una opción tooextract es hello toouse siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a0ae5-137">One option tooextract this is toouse hello following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="a0ae5-138">A continuación, se podría pasar como una plantilla de implementación de parámetro tooyour ARM.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-138">You could then pass this as a parameter tooyour ARM deployment template.</span></span>

<span data-ttu-id="a0ae5-139">En este momento la plantilla de ARM de hello está listo.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-139">At this point hello ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="a0ae5-140">Implementar plantilla</span><span class="sxs-lookup"><span data-stu-id="a0ae5-140">Deploy Template</span></span>
<span data-ttu-id="a0ae5-141">Hola pasos finales son toopiece esto todo junto en una implementación end-to-end.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-141">hello final steps are toopiece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="a0ae5-142">toomake implementación más fácil, puede aprovechar hello **Deploy-AzureResourceGroup.ps1** secuencia de comandos de PowerShell que se agrega al crear un proyecto del grupo de recursos de Azure en Visual Studio toohelp con la carga de los artefactos necesarios en plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-142">toomake deployment easier you can leverage hello **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio toohelp with uploading of any artifacts required in hello template.</span></span> <span data-ttu-id="a0ae5-143">Requiere toohave creado una cuenta de almacenamiento que desee toouse antelación.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-143">It requires you toohave created a storage account you want toouse ahead of time.</span></span> <span data-ttu-id="a0ae5-144">En este ejemplo, crea una cuenta de almacenamiento compartido para hello package.zip toobe cargado.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-144">For this example, I created a shared storage account for hello package.zip toobe uploaded.</span></span> <span data-ttu-id="a0ae5-145">script de Hola aprovecharán la cuenta de almacenamiento de AzCopy tooupload Hola paquete toohello.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-145">hello script will leverage AzCopy tooupload hello package toohello storage account.</span></span> <span data-ttu-id="a0ae5-146">Se pasa en la ubicación de carpeta artefacto y script de Hola cargará automáticamente todos los archivos de ese toohello de directorio con el nombre de contenedor de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-146">You pass in your artifact folder location and hello script will automatically upload all files within that directory toohello named storage container.</span></span> <span data-ttu-id="a0ae5-147">Después de llamar a Deploy-AzureResourceGroup.ps1 tiene toothen actualización Hola SSL enlaces toomap Hola nombre de host personalizado con su certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="a0ae5-147">After calling Deploy-AzureResourceGroup.ps1 you have toothen update hello SSL bindings toomap hello custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="a0ae5-148">Hola siguientes se muestra en PowerShell Hola Hola que realiza la llamada de implementación completa Deploy-AzureResourceGroup.ps1:</span><span class="sxs-lookup"><span data-stu-id="a0ae5-148">hello following PowerShell shows hello complete deployment calling hello Deploy-AzureResourceGroup.ps1:</span></span>

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script toodeploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app toobind ssl certificate toohostname. This has toobe done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

<span data-ttu-id="a0ae5-149">En este momento la aplicación debe se han implementado y debe ser capaz de toobrowse tooit a través de https://www.yourcustomdomain.com</span><span class="sxs-lookup"><span data-stu-id="a0ae5-149">At this point your application should have been deployed and you should be able toobrowse tooit via https://www.yourcustomdomain.com</span></span>

