---
title: aaaDeploy plantilla de Azure con el token de SAS y la CLI de Azure | Documentos de Microsoft
description: "Use el Administrador de recursos de Azure y Azure CLI toodeploy tooAzure de recursos de una plantilla que esté protegida con token de SAS."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 59c64616d6e1f5e456d88a72854d0ed99e1bdc0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a><span data-ttu-id="2f2b5-103">Implementar la plantilla de Resource Manager privada con el token de SAS y la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="2f2b5-103">Deploy private Resource Manager template with SAS token and Azure CLI</span></span>

<span data-ttu-id="2f2b5-104">Cuando la plantilla reside en una cuenta de almacenamiento, puede restringir la plantilla de toohello de acceso y proporcionar un token de firma (SAS) de acceso compartido durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="2f2b5-104">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="2f2b5-105">Este tema se explica cómo toouse PowerShell de Azure con el Administrador de recursos plantillas tooprovide un token SAS durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="2f2b5-105">This topic explains how toouse Azure PowerShell with Resource Manager templates tooprovide a SAS token during deployment.</span></span> 

## <a name="add-private-template-toostorage-account"></a><span data-ttu-id="2f2b5-106">Agregar plantilla privada toostorage cuenta</span><span class="sxs-lookup"><span data-stu-id="2f2b5-106">Add private template toostorage account</span></span>

<span data-ttu-id="2f2b5-107">Puede agregar la cuenta de almacenamiento de tooa de plantillas y vincular toothem durante la implementación con un token de SAS.</span><span class="sxs-lookup"><span data-stu-id="2f2b5-107">You can add your templates tooa storage account and link toothem during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f2b5-108">Siguiendo estos pasos hello, blob de Hola que contiene la plantilla de hello es propietario de la cuenta de acceso tooonly Hola.</span><span class="sxs-lookup"><span data-stu-id="2f2b5-108">By following hello steps below, hello blob containing hello template is accessible tooonly hello account owner.</span></span> <span data-ttu-id="2f2b5-109">Sin embargo, cuando se crea un token SAS para blob hello, blob hello es accesible tooanyone con ese URI.</span><span class="sxs-lookup"><span data-stu-id="2f2b5-109">However, when you create a SAS token for hello blob, hello blob is accessible tooanyone with that URI.</span></span> <span data-ttu-id="2f2b5-110">Si otro usuario intercepta Hola URI, ese usuario es tooaccess capaz de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f2b5-110">If another user intercepts hello URI, that user is able tooaccess hello template.</span></span> <span data-ttu-id="2f2b5-111">Con un token SAS es una buena forma de limitar el acceso tooyour plantillas, pero no debe incluir datos confidenciales tales como contraseñas directamente en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f2b5-111">Using a SAS token is a good way of limiting access tooyour templates, but you should not include sensitive data like passwords directly in hello template.</span></span>
> 
> 

<span data-ttu-id="2f2b5-112">Hello en el ejemplo siguiente se configura un contenedor de la cuenta de almacenamiento privado y carga una plantilla:</span><span class="sxs-lookup"><span data-stu-id="2f2b5-112">hello following example sets up a private storage account container and uploads a template:</span></span>
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="2f2b5-113">Provisión del token de SAS durante la implementación</span><span class="sxs-lookup"><span data-stu-id="2f2b5-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="2f2b5-114">toodeploy una plantilla privada en una cuenta de almacenamiento, generar un token SAS e incluirla en hello URI para la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f2b5-114">toodeploy a private template in a storage account, generate a SAS token and include it in hello URI for hello template.</span></span> <span data-ttu-id="2f2b5-115">Establecer tooallow de tiempo de expiración de hello suficiente implementación en tiempo de toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="2f2b5-115">Set hello expiry time tooallow enough time toocomplete hello deployment.</span></span>
   
```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

<span data-ttu-id="2f2b5-116">Para obtener un ejemplo del uso de un token de SAS con plantillas vinculadas, consulte [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2f2b5-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f2b5-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f2b5-117">Next steps</span></span>
* <span data-ttu-id="2f2b5-118">Para una plantilla de toodeploying introducción, consulte [implementar los recursos con plantillas de administrador de recursos y Azure PowerShell](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2f2b5-118">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="2f2b5-119">Para obtener un script de ejemplo completo que implementa una plantilla, vea [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md) (Implementar script de plantilla de Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="2f2b5-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md)</span></span>
* <span data-ttu-id="2f2b5-120">toodefine parámetros de plantilla, vea [crear plantillas](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="2f2b5-120">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="2f2b5-121">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="2f2b5-121">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
