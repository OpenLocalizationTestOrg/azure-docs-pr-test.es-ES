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
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a>Implementación de una aplicación web con MSDeploy, un nombre de host personalizado y un certificado SSL
Esta guía se describen la creación de una implementación de extremo a extremo de una aplicación Web de Azure, aprovechar MSDeploy, así como agregar un nombre de host personalizado y una plantilla de ARM de toohello de certificado SSL.

Para obtener más información sobre la creación de plantillas, consulte [Creación de plantillas de Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).

### <a name="create-sample-application"></a>Creación de la aplicación de ejemplo
Va a implementar una aplicación web ASP.NET. Hola primer paso es toocreate una aplicación web simple (o puede elegir toouse uno ya existente; en cuyo caso, puede omitir este paso).

Abra Visual Studio 2015 y seleccione Archivo > Nuevo proyecto. En el cuadro de diálogo de Hola que aparece, elija Web > aplicación Web ASP.NET. En plantillas elija Web y elija la plantilla MVC Hola. Seleccione *cambiar el tipo de autenticación* demasiado*sin autenticación*. Esto es simplemente toomake Hola aplicación de ejemplo tan simple como sea posible.

En este momento tendrá un toouse listo de ASP.Net web app básica como parte del proceso de implementación.

### <a name="create-msdeploy-package"></a>Creación del paquete MSDeploy
Siguiente paso es toocreate Hola paquete toodeploy hello web app tooAzure. toodo, guarde el proyecto y, a continuación, ejecute el siguiente de Hola desde línea de comandos de hello:

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

Esto creará un paquete comprimido en la carpeta de PackageLocation Hola. Hello aplicación está ahora listo toobe implementado, que ahora puede crear un toodo de plantilla de Azure Resource Manager que.

### <a name="create-arm-template"></a>Creación de la plantilla de ARM
En primer lugar, vamos a comenzar con una plantilla de ARM básica que creará una aplicación web y un plan de hospedaje (tenga en cuenta que no se muestran los parámetros ni las variables por brevedad).

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

A continuación, deberá toomodify hello web app recursos tootake un recurso anidado de MSDeploy. Esto permitirá tooreference Hola paquete creado anteriormente y saber Azure Resource Manager toouse MSDeploy toodeploy Hola paquete toohello WebApp de Azure. siguiente Hola muestra Hola de recursos de Microsoft.Web/sites con recursos de MSDeploy Hola anidado:

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

Ahora observará ese Hola MSDeploy recurso toma una **packageUri** propiedad que se define como sigue:

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

Esto **packageUri** toma Hola uri de la cuenta de almacenamiento que señala toohello cuenta de almacenamiento donde se cargará el zip de paquete a. Hello Azure Resource Manager aprovecharán [firmas de acceso compartido](../storage/common/storage-dotnet-shared-access-signature-part-1.md) paquete de hello toopull hacia abajo localmente desde la cuenta de almacenamiento de hello al implementar la plantilla de Hola. Este proceso se automatiza a través de una secuencia de comandos de PowerShell que cargar paquete de Hola y llamar a Hola API de administración de Azure toocreate hello las claves se requieren y en la plantilla de hello pasar como parámetros (*_artifactsLocation* y *_artifactsLocationSasToken*). Necesitará toodefine parámetros para la carpeta de Hola y nombre de archivo paquete de hello es el contenedor de almacenamiento de Hola de toounder cargado.

A continuación debe tooadd en otro recurso anidado toosetup Hola hostname enlaces tooleverage un dominio personalizado. Que se van a primera tooensure de necesidad que posee el nombre de host de Hola y configurarla toobe Azure comprobado que usted es el propietario: vea [configurar un nombre de dominio personalizado en el servicio de aplicación de Azure](app-service-web-tutorial-custom-domain.md). Una vez que se hace puede agregar Hola sigue tooyour template en la sección de recursos de Hola Microsoft.Web/sites:

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

Por último, debe tooadd otro recurso de nivel superior, Microsoft.Web/certificates. Este recurso contendrá su certificado SSL y seguirán existiendo en el plan de mismo nivel que la aplicación web y el hospedaje de Hola.

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

Deberá toohave un certificado SSL válido en orden tooset este recurso. Una vez que tenga ese certificado válido debe bytes de pfx hello tooextract como una cadena de base64. Una opción tooextract es hello toouse siguiente comando de PowerShell:

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

A continuación, se podría pasar como una plantilla de implementación de parámetro tooyour ARM.

En este momento la plantilla de ARM de hello está listo.

### <a name="deploy-template"></a>Implementar plantilla
Hola pasos finales son toopiece esto todo junto en una implementación end-to-end. toomake implementación más fácil, puede aprovechar hello **Deploy-AzureResourceGroup.ps1** secuencia de comandos de PowerShell que se agrega al crear un proyecto del grupo de recursos de Azure en Visual Studio toohelp con la carga de los artefactos necesarios en plantilla de Hola. Requiere toohave creado una cuenta de almacenamiento que desee toouse antelación. En este ejemplo, crea una cuenta de almacenamiento compartido para hello package.zip toobe cargado. script de Hola aprovecharán la cuenta de almacenamiento de AzCopy tooupload Hola paquete toohello. Se pasa en la ubicación de carpeta artefacto y script de Hola cargará automáticamente todos los archivos de ese toohello de directorio con el nombre de contenedor de almacenamiento. Después de llamar a Deploy-AzureResourceGroup.ps1 tiene toothen actualización Hola SSL enlaces toomap Hola nombre de host personalizado con su certificado SSL.

Hola siguientes se muestra en PowerShell Hola Hola que realiza la llamada de implementación completa Deploy-AzureResourceGroup.ps1:

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

En este momento la aplicación debe se han implementado y debe ser capaz de toobrowse tooit a través de https://www.yourcustomdomain.com

