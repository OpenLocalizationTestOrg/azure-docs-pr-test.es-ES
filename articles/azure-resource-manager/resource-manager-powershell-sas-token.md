---
title: plantilla de Azure con PowerShell y el token de SAS aaaDeploy | Documentos de Microsoft
description: "Use el Administrador de recursos de Azure y Azure PowerShell toodeploy tooAzure de recursos de una plantilla que esté protegida con token de SAS."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: b95e096591d6213f8ef79235c8cd85705c4b79ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a><span data-ttu-id="275ae-103">Implementar la plantilla de Resource Manager privada con el token de SAS y Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="275ae-103">Deploy private Resource Manager template with SAS token and Azure PowerShell</span></span>

<span data-ttu-id="275ae-104">Cuando la plantilla reside en una cuenta de almacenamiento, puede restringir la plantilla de toohello de acceso y proporcionar un token de firma (SAS) de acceso compartido durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="275ae-104">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="275ae-105">Este tema se explica cómo toouse PowerShell de Azure con el Administrador de recursos plantillas tooprovide un token SAS durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="275ae-105">This topic explains how toouse Azure PowerShell with Resource Manager templates tooprovide a SAS token during deployment.</span></span> 

## <a name="add-private-template-toostorage-account"></a><span data-ttu-id="275ae-106">Agregar plantilla privada toostorage cuenta</span><span class="sxs-lookup"><span data-stu-id="275ae-106">Add private template toostorage account</span></span>

<span data-ttu-id="275ae-107">Puede agregar la cuenta de almacenamiento de tooa de plantillas y vincular toothem durante la implementación con un token de SAS.</span><span class="sxs-lookup"><span data-stu-id="275ae-107">You can add your templates tooa storage account and link toothem during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="275ae-108">Siguiendo estos pasos hello, blob de Hola que contiene la plantilla de hello es propietario de la cuenta de acceso tooonly Hola.</span><span class="sxs-lookup"><span data-stu-id="275ae-108">By following hello steps below, hello blob containing hello template is accessible tooonly hello account owner.</span></span> <span data-ttu-id="275ae-109">Sin embargo, cuando se crea un token SAS para blob hello, blob hello es accesible tooanyone con ese URI.</span><span class="sxs-lookup"><span data-stu-id="275ae-109">However, when you create a SAS token for hello blob, hello blob is accessible tooanyone with that URI.</span></span> <span data-ttu-id="275ae-110">Si otro usuario intercepta Hola URI, ese usuario es tooaccess capaz de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="275ae-110">If another user intercepts hello URI, that user is able tooaccess hello template.</span></span> <span data-ttu-id="275ae-111">Con un token SAS es una buena forma de limitar el acceso tooyour plantillas, pero no debe incluir datos confidenciales tales como contraseñas directamente en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="275ae-111">Using a SAS token is a good way of limiting access tooyour templates, but you should not include sensitive data like passwords directly in hello template.</span></span>
> 
> 

<span data-ttu-id="275ae-112">Hello en el ejemplo siguiente se configura un contenedor de la cuenta de almacenamiento privado y carga una plantilla:</span><span class="sxs-lookup"><span data-stu-id="275ae-112">hello following example sets up a private storage account container and uploads a template:</span></span>
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="275ae-113">Provisión del token de SAS durante la implementación</span><span class="sxs-lookup"><span data-stu-id="275ae-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="275ae-114">toodeploy una plantilla privada en una cuenta de almacenamiento, generar un token SAS e incluirla en hello URI para la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="275ae-114">toodeploy a private template in a storage account, generate a SAS token and include it in hello URI for hello template.</span></span> <span data-ttu-id="275ae-115">Establecer tooallow de tiempo de expiración de hello suficiente implementación en tiempo de toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="275ae-115">Set hello expiry time tooallow enough time toocomplete hello deployment.</span></span>
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get hello URI with hello SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

<span data-ttu-id="275ae-116">Para obtener un ejemplo del uso de un token de SAS con plantillas vinculadas, consulte [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="275ae-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="275ae-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="275ae-117">Next steps</span></span>
* <span data-ttu-id="275ae-118">Para una plantilla de toodeploying introducción, consulte [implementar los recursos con plantillas de administrador de recursos y Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="275ae-118">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="275ae-119">Para obtener un script de ejemplo completo que implementa una plantilla, vea [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md) (Implementar script de plantilla de Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="275ae-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md)</span></span>
* <span data-ttu-id="275ae-120">toodefine parámetros de plantilla, vea [crear plantillas](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="275ae-120">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="275ae-121">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="275ae-121">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

