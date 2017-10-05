---
title: Implementar la plantilla de Azure con el token de SAS y PowerShell | Microsoft Docs
description: "Use Azure Resource Manager y Azure PowerShell para implementar recursos en Azure desde una plantilla que está protegida con el token de SAS."
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
ms.openlocfilehash: 1e3cea027b599e2b1af1ced0fdf14e2cc8a0db82
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a><span data-ttu-id="fcd5a-103">Implementar la plantilla de Resource Manager privada con el token de SAS y Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fcd5a-103">Deploy private Resource Manager template with SAS token and Azure PowerShell</span></span>

<span data-ttu-id="fcd5a-104">Cuando la plantilla se encuentra en una cuenta de almacenamiento, puede restringir el acceso a la plantilla y proporcionar un token de firma de acceso compartido (SAS) durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="fcd5a-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="fcd5a-105">En este tema se explica cómo usar Azure PowerShell con plantillas de Resource Manager para proporcionar un token de SAS durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="fcd5a-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span></span> 

## <a name="add-private-template-to-storage-account"></a><span data-ttu-id="fcd5a-106">Adición de plantilla privada a la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="fcd5a-106">Add private template to storage account</span></span>

<span data-ttu-id="fcd5a-107">Puede agregar las plantillas a una cuenta de almacenamiento y establecer vínculos a ellas durante la implementación con un token de SAS.</span><span class="sxs-lookup"><span data-stu-id="fcd5a-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcd5a-108">Siguiendo estos pasos, el blob que contiene la plantilla solo es accesible para el propietario de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="fcd5a-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span></span> <span data-ttu-id="fcd5a-109">Sin embargo, cuando se crea un token de SAS para el blob, el blob es accesible para cualquier persona con ese URI.</span><span class="sxs-lookup"><span data-stu-id="fcd5a-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span></span> <span data-ttu-id="fcd5a-110">Si otro usuario intercepta el URI, ese usuario podrá tener acceso a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="fcd5a-110">If another user intercepts the URI, that user is able to access the template.</span></span> <span data-ttu-id="fcd5a-111">El uso de un token de SAS supone un buen método para limitar el acceso a las plantillas, pero no debe incluir información confidencial como contraseñas directamente en estas.</span><span class="sxs-lookup"><span data-stu-id="fcd5a-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span></span>
> 
> 

<span data-ttu-id="fcd5a-112">El siguiente ejemplo configura un contenedor de una cuenta de almacenamiento privado y carga una plantilla:</span><span class="sxs-lookup"><span data-stu-id="fcd5a-112">The following example sets up a private storage account container and uploads a template:</span></span>
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="fcd5a-113">Provisión del token de SAS durante la implementación</span><span class="sxs-lookup"><span data-stu-id="fcd5a-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="fcd5a-114">Para implementar una plantilla privada en una cuenta de almacenamiento, genere un token de SAS e inclúyalo en el identificador URI de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="fcd5a-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="fcd5a-115">Establezca el tiempo de expiración con un margen suficiente para completar la implementación.</span><span class="sxs-lookup"><span data-stu-id="fcd5a-115">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get the URI with the SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

<span data-ttu-id="fcd5a-116">Para obtener un ejemplo del uso de un token de SAS con plantillas vinculadas, consulte [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fcd5a-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="fcd5a-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fcd5a-117">Next steps</span></span>
* <span data-ttu-id="fcd5a-118">Para obtener una introducción a la implementación de plantillas, vea [Implementación de recursos con plantillas de Resource Manager y Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="fcd5a-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="fcd5a-119">Para obtener un script de ejemplo completo que implementa una plantilla, vea [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md) (Implementar script de plantilla de Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="fcd5a-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md)</span></span>
* <span data-ttu-id="fcd5a-120">Para definir parámetros de plantilla, consulte [Creación de plantillas](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="fcd5a-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="fcd5a-121">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="fcd5a-121">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

