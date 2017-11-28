---
title: "Creación de un servidor de Azure Analysis Services mediante PowerShell | Microsoft Docs"
description: Aprenda a crear un servidor de Azure Analysis Services mediante PowerShell.
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
ms.openlocfilehash: cb42fd3ed51364cf478848cc51ebbb2f175e96d2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="030d2-103">Creación de un servidor de Azure Analysis Services mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="030d2-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="030d2-104">Este inicio rápido describe el uso de PowerShell desde la línea de comandos para crear un servidor de Azure Analysis Services en un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="030d2-104">This quickstart describes using PowerShell from the command line to create an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="030d2-105">Esta tarea requiere la versión 4.0 del módulo de Azure PowerShell, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="030d2-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="030d2-106">Para encontrar la versión, ejecute ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="030d2-106">To find the version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="030d2-107">Si necesita instalarla o actualizarla, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="030d2-107">To install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="030d2-108">La creación de un servidor puede dar lugar a un nuevo servicio facturable.</span><span class="sxs-lookup"><span data-stu-id="030d2-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="030d2-109">Para obtener más información, consulte los [precios de Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="030d2-109">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="030d2-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="030d2-110">Prerequisites</span></span>
<span data-ttu-id="030d2-111">Para completar este inicio rápido necesita instalar:</span><span class="sxs-lookup"><span data-stu-id="030d2-111">To complete this quickstart, you need:</span></span>

* <span data-ttu-id="030d2-112">**Suscripción de Azure**: visite [Evaluación gratuita de Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) para crear una cuenta.</span><span class="sxs-lookup"><span data-stu-id="030d2-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
* <span data-ttu-id="030d2-113">**Azure Active Directory**: la suscripción debe estar asociada a un inquilino de Azure Active Directory y debe tener una cuenta en ese directorio.</span><span class="sxs-lookup"><span data-stu-id="030d2-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="030d2-114">Para más información, consulte [Permisos de usuario y autenticación](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="030d2-114">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="030d2-115">Importación del módulo AzureRm.AnalysisServices</span><span class="sxs-lookup"><span data-stu-id="030d2-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="030d2-116">Para crear un servidor en su suscripción, utilice el módulo del componente [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices).</span><span class="sxs-lookup"><span data-stu-id="030d2-116">To create a server in your subscription, you use the [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="030d2-117">Cargue el módulo AzureRm.AnalysisServices en la sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="030d2-117">Load the AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-to-azure"></a><span data-ttu-id="030d2-118">Inicio de sesión en Azure</span><span class="sxs-lookup"><span data-stu-id="030d2-118">Sign in to Azure</span></span>

<span data-ttu-id="030d2-119">Inicie sesión en su suscripción de Azure mediante el comando [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount).</span><span class="sxs-lookup"><span data-stu-id="030d2-119">Sign in to your Azure subscription by using the [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="030d2-120">Siga las instrucciones que aparecen en pantalla.</span><span class="sxs-lookup"><span data-stu-id="030d2-120">Follow the on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="030d2-121">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="030d2-121">Create a resource group</span></span>
 
<span data-ttu-id="030d2-122">Un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) es un contenedor lógico en el que se implementan y se administran los recursos de Azure como grupo.</span><span class="sxs-lookup"><span data-stu-id="030d2-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="030d2-123">Cuando cree el servidor, deberá especificar un grupo de recursos de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="030d2-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="030d2-124">Si aún no dispone de un grupo de recursos, puede crearlo mediante el comando [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="030d2-124">If you do not already have a resource group, you can create a new one by using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="030d2-125">En el siguiente ejemplo, se crea un grupo de recursos denominado `myResourceGroup` en la región del oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="030d2-125">The following example creates a resource group named `myResourceGroup` in the West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="030d2-126">Creación de un servidor</span><span class="sxs-lookup"><span data-stu-id="030d2-126">Create a server</span></span>

<span data-ttu-id="030d2-127">Cree un nuevo servidor mediante el comando [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver).</span><span class="sxs-lookup"><span data-stu-id="030d2-127">Create a new server by using the [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="030d2-128">En el ejemplo siguiente se crea un servidor denominado myServer en myResourceGroup, en la región oeste de Estados Unidos, en el nivel de D1, y se especifica philipc@adventureworks.com como administrador del servidor.</span><span class="sxs-lookup"><span data-stu-id="030d2-128">The following example creates a server named myServer in myResourceGroup, in the West US region, at the D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="030d2-129">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="030d2-129">Clean up resources</span></span>

<span data-ttu-id="030d2-130">Puede quitar el servidor de la suscripción mediante el comando [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver).</span><span class="sxs-lookup"><span data-stu-id="030d2-130">You can remove the server from your subscription by using the [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="030d2-131">Si va a seguir con otros inicios rápidos y tutoriales de esta colección, no quite el servidor.</span><span class="sxs-lookup"><span data-stu-id="030d2-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="030d2-132">En el ejemplo siguiente se quita el servidor creado en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="030d2-132">The following example removes the server created in the previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="030d2-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="030d2-133">Next steps</span></span>
<span data-ttu-id="030d2-134">[Administración de Azure Analysis Services con PowerShell](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="030d2-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="030d2-135">[Implementación de un modelo desde SSDT](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="030d2-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="030d2-136">Creación de un modelo en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="030d2-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)