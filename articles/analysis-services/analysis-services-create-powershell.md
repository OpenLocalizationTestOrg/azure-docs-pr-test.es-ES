---
title: aaaCreate un servidor de Analysis Services de Azure mediante PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una Azure Analysis Services server usando PowerShell"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="2ca17-103">Creación de un servidor de Azure Analysis Services mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ca17-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="2ca17-104">Este tutorial rápido describe el uso de PowerShell de hello toocreate de línea de comandos un servidor de Analysis Services de Azure en un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2ca17-104">This quickstart describes using PowerShell from hello command line toocreate an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="2ca17-105">Esta tarea requiere la versión 4.0 del módulo de Azure PowerShell, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="2ca17-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="2ca17-106">versión de hello toofind, ejecute ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="2ca17-106">toofind hello version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="2ca17-107">tooinstall o actualización, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="2ca17-107">tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="2ca17-108">La creación de un servidor puede dar lugar a un nuevo servicio facturable.</span><span class="sxs-lookup"><span data-stu-id="2ca17-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="2ca17-109">más información, consulte toolearn [precios de Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="2ca17-109">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ca17-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2ca17-110">Prerequisites</span></span>
<span data-ttu-id="2ca17-111">toocomplete este tutorial rápido, necesita:</span><span class="sxs-lookup"><span data-stu-id="2ca17-111">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="2ca17-112">**Suscripción de Azure**: visite [evaluación gratuita de Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate una cuenta.</span><span class="sxs-lookup"><span data-stu-id="2ca17-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="2ca17-113">**Azure Active Directory**: la suscripción debe estar asociada a un inquilino de Azure Active Directory y debe tener una cuenta en ese directorio.</span><span class="sxs-lookup"><span data-stu-id="2ca17-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="2ca17-114">más información, consulte toolearn [permisos de usuario y la autenticación](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="2ca17-114">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="2ca17-115">Importación del módulo AzureRm.AnalysisServices</span><span class="sxs-lookup"><span data-stu-id="2ca17-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="2ca17-116">toocreate un servidor en su suscripción, usas hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) módulo del componente.</span><span class="sxs-lookup"><span data-stu-id="2ca17-116">toocreate a server in your subscription, you use hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="2ca17-117">Cargar el módulo de AzureRm.AnalysisServices de hello en la sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2ca17-117">Load hello AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a><span data-ttu-id="2ca17-118">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="2ca17-118">Sign in tooAzure</span></span>

<span data-ttu-id="2ca17-119">Inicie sesión en tooyour suscripción de Azure mediante hello [AzureRmAccount agregar](/powershell/module/azurerm.profile/add-azurermaccount) comando.</span><span class="sxs-lookup"><span data-stu-id="2ca17-119">Sign in tooyour Azure subscription by using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="2ca17-120">Siga hello en pantalla de instrucciones.</span><span class="sxs-lookup"><span data-stu-id="2ca17-120">Follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="2ca17-121">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2ca17-121">Create a resource group</span></span>
 
<span data-ttu-id="2ca17-122">Un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) es un contenedor lógico en el que se implementan y se administran los recursos de Azure como grupo.</span><span class="sxs-lookup"><span data-stu-id="2ca17-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="2ca17-123">Cuando cree el servidor, deberá especificar un grupo de recursos de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="2ca17-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="2ca17-124">Si no dispone de un grupo de recursos, puede crear uno nuevo mediante el uso de hello [AzureRmResourceGroup New](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando.</span><span class="sxs-lookup"><span data-stu-id="2ca17-124">If you do not already have a resource group, you can create a new one by using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="2ca17-125">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en la región del oeste de Estados Unidos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ca17-125">hello following example creates a resource group named `myResourceGroup` in hello West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="2ca17-126">Creación de un servidor</span><span class="sxs-lookup"><span data-stu-id="2ca17-126">Create a server</span></span>

<span data-ttu-id="2ca17-127">Crear un nuevo servidor mediante el uso de hello [AzureRmAnalysisServicesServer New](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) comando.</span><span class="sxs-lookup"><span data-stu-id="2ca17-127">Create a new server by using hello [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="2ca17-128">Hello siguiente ejemplo crea un servidor denominado myServer en myResourceGroup de región del oeste de EE. Hola, en el nivel de hello D1 y especifica philipc@adventureworks.com como un administrador del servidor.</span><span class="sxs-lookup"><span data-stu-id="2ca17-128">hello following example creates a server named myServer in myResourceGroup, in hello West US region, at hello D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="2ca17-129">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="2ca17-129">Clean up resources</span></span>

<span data-ttu-id="2ca17-130">Puede quitar servidor hello de su suscripción mediante el uso de hello [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) comando.</span><span class="sxs-lookup"><span data-stu-id="2ca17-130">You can remove hello server from your subscription by using hello [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="2ca17-131">Si va a seguir con otros inicios rápidos y tutoriales de esta colección, no quite el servidor.</span><span class="sxs-lookup"><span data-stu-id="2ca17-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="2ca17-132">Hello en el ejemplo siguiente se quita servidor hello creado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ca17-132">hello following example removes hello server created in hello previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="2ca17-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2ca17-133">Next steps</span></span>
<span data-ttu-id="2ca17-134">[Administración de Azure Analysis Services con PowerShell](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="2ca17-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="2ca17-135">[Implementación de un modelo desde SSDT](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="2ca17-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="2ca17-136">Creación de un modelo en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2ca17-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)