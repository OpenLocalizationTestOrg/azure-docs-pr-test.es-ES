---
title: "Actualización de Media Services después de revertir las claves de acceso de almacenamiento | Microsoft Docs"
description: "En este artículo se proporcionan instrucciones sobre cómo actualizar Servicios multimedia tras rotar las claves de acceso de almacenamiento."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: 304e72e0d2d4a7e95df513e6d5481def9eae3f68
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="60169-103">Actualización de Media Services después de revertir las claves de acceso de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="60169-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="60169-104">Cuando crea una nueva cuenta de Azure Media Services (AMS), también se le pide que seleccione una cuenta de Azure Storage que se usa para almacenar el contenido multimedia.</span><span class="sxs-lookup"><span data-stu-id="60169-104">When you create a new Azure Media Services (AMS) account, you are also asked to select an Azure Storage account that is used to store your media content.</span></span> <span data-ttu-id="60169-105">Puede agregar más de una cuenta de almacenamiento a su cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="60169-105">You can add more than one storage accounts to your Media Services account.</span></span> <span data-ttu-id="60169-106">En este tema se explica cómo rotar las claves de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="60169-106">This topic shows how to rotate storage keys.</span></span> <span data-ttu-id="60169-107">También se explica cómo agregar cuentas de almacenamiento a una cuenta multimedia.</span><span class="sxs-lookup"><span data-stu-id="60169-107">It also shows how to add storage accounts to a media account.</span></span> 

<span data-ttu-id="60169-108">Para realizar las acciones descritas en este tema, debe usar las [API de ARM](https://docs.microsoft.com/rest/api/media/mediaservice) y [PowerShell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span><span class="sxs-lookup"><span data-stu-id="60169-108">To perform the actions described in this topic, you should be using [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span></span>  <span data-ttu-id="60169-109">Para más información, vea [How to manage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md) (Administración de recursos de Azure con PowerShell y Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="60169-109">For more information, see [How to manage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

## <a name="overview"></a><span data-ttu-id="60169-110">Información general</span><span class="sxs-lookup"><span data-stu-id="60169-110">Overview</span></span>

<span data-ttu-id="60169-111">Cuando se crea una nueva cuenta de almacenamiento, Azure genera dos claves de acceso de almacenamiento de 512 bits, que se usan para autenticar el acceso a su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="60169-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used to authenticate access to your storage account.</span></span> <span data-ttu-id="60169-112">Para aumentar la seguridad de sus conexiones de almacenamiento, se recomienda regenerar y rotar periódicamente su claves de acceso de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="60169-112">To keep your storage connections more secure, it is recommended to periodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="60169-113">Se proporcionan dos claves de acceso (principal y secundaria) con el fin de permitirle mantener conexiones con la cuenta de almacenamiento mediante el uso de una clave de acceso mientras regenera la otra.</span><span class="sxs-lookup"><span data-stu-id="60169-113">Two access keys (primary and secondary) are provided in order to enable you to maintain connections to the storage account using one access key while you regenerate the other access key.</span></span> <span data-ttu-id="60169-114">Este procedimiento se conoce también como "rotación de claves de acceso".</span><span class="sxs-lookup"><span data-stu-id="60169-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="60169-115">Servicios multimedia depende de una clave de almacenamiento que se le ofrece.</span><span class="sxs-lookup"><span data-stu-id="60169-115">Media Services depends on a storage key provided to it.</span></span> <span data-ttu-id="60169-116">En concreto, los localizadores que se usan para transmitir o descargar sus activos dependen de la clave de acceso de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="60169-116">Specifically, the locators that are used to stream or download your assets depend on the specified storage access key.</span></span> <span data-ttu-id="60169-117">Cuando se crea una cuenta de AMS toma una dependencia en la clave de acceso de almacenamiento principal de forma predeterminada, pero como usuario puede actualizar la clave de almacenamiento que AMS tiene.</span><span class="sxs-lookup"><span data-stu-id="60169-117">When an AMS account is created it takes a dependency on the primary storage access key by default but as a user you can update the storage key that AMS has.</span></span> <span data-ttu-id="60169-118">Debe asegurarse de que Media Services conocen qué clave usar siguiendo los pasos descritos en este tema.</span><span class="sxs-lookup"><span data-stu-id="60169-118">You must make sure to let Media Services know which key to use by following steps described in this topic.</span></span>  

>[!NOTE]
> <span data-ttu-id="60169-119">Si tiene varias cuentas de almacenamiento, realizaría este procedimiento con cada una.</span><span class="sxs-lookup"><span data-stu-id="60169-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="60169-120">El orden en que se rotan las claves de almacenamiento no es fijo.</span><span class="sxs-lookup"><span data-stu-id="60169-120">The order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="60169-121">Puede rotar primero la clave secundaria y después la primaria, o viceversa.</span><span class="sxs-lookup"><span data-stu-id="60169-121">You can rotate the secondary key first and then the primary key or vice versa.</span></span>
>
> <span data-ttu-id="60169-122">Antes de ejecutar los pasos que se describen en este tema en una cuenta de producción, asegúrese de probarlos en una cuenta de ensayo.</span><span class="sxs-lookup"><span data-stu-id="60169-122">Before executing steps described in this topic on a production account, make sure to test them on a pre-production account.</span></span>
>

## <a name="steps-to-rotate-storage-keys"></a><span data-ttu-id="60169-123">Pasos para rotar claves de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="60169-123">Steps to rotate storage keys</span></span> 
 
 1. <span data-ttu-id="60169-124">Cambie la clave principal de la cuenta de almacenamiento mediante el cmdlet de PowerShell o en [Azure](https://portal.azure.com/) Portal.</span><span class="sxs-lookup"><span data-stu-id="60169-124">Change the storage account Primary key through the powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="60169-125">Llame al cmdlet Sync-AzureRmMediaServiceStorageKeys con los parámetros adecuados para forzar a la cuenta multimedia a seleccionar las claves de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="60169-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params to force media account to pick up storage account keys</span></span>
 
    <span data-ttu-id="60169-126">En el ejemplo siguiente se muestra cómo sincronizar las claves para las cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="60169-126">The following example shows how to sync keys to storage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="60169-127">Espere una hora más o menos.</span><span class="sxs-lookup"><span data-stu-id="60169-127">Wait an hour or so.</span></span> <span data-ttu-id="60169-128">Verifique que los escenarios de streaming estén funcionando.</span><span class="sxs-lookup"><span data-stu-id="60169-128">Verify the streaming scenarios are working.</span></span>
 4. <span data-ttu-id="60169-129">Cambie la clave secundaria de la cuenta de almacenamiento con el cmdlet de PowerShell o en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="60169-129">Change storage account secondary key through the powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="60169-130">Llame al cmdlet Sync-AzureRmMediaServiceStorageKeys de PowerShell con los parámetros adecuados para forzar a la cuenta multimedia a seleccionar las nuevas claves de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="60169-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params to force media account to pick up new storage account keys.</span></span> 
 6. <span data-ttu-id="60169-131">Espere una hora más o menos.</span><span class="sxs-lookup"><span data-stu-id="60169-131">Wait an hour or so.</span></span> <span data-ttu-id="60169-132">Verifique que los escenarios de streaming estén funcionando.</span><span class="sxs-lookup"><span data-stu-id="60169-132">Verify the streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="60169-133">Un ejemplos de cmdlet de PowerShell</span><span class="sxs-lookup"><span data-stu-id="60169-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="60169-134">En el ejemplo siguiente se muestra cómo obtener la cuenta de almacenamiento y sincronizarla con la cuenta de AMS.</span><span class="sxs-lookup"><span data-stu-id="60169-134">The following example demonstrates how to get the storage account and sync it with the AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-to-add-storage-accounts-to-your-ams-account"></a><span data-ttu-id="60169-135">Pasos para agregar cuentas de almacenamiento a la cuenta de AMS</span><span class="sxs-lookup"><span data-stu-id="60169-135">Steps to add storage accounts to your AMS account</span></span>

<span data-ttu-id="60169-136">En el tema siguiente se explica cómo agregar cuentas de almacenamiento a la cuenta de AMS: [Agregar varias cuentas de almacenamiento a una cuenta de Media Services](meda-services-managing-multiple-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="60169-136">The following topic shows how to add storage accounts to your AMS account: [Attach multiple storage accounts to a Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="60169-137">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="60169-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="60169-138">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="60169-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="60169-139">Agradecimientos</span><span class="sxs-lookup"><span data-stu-id="60169-139">Acknowledgments</span></span>
<span data-ttu-id="60169-140">Nos gustaría mencionar a las siguientes personas que han contribuido a crear este documento: Cenk Dingiloglu, Gada Milán y Seva Titov.</span><span class="sxs-lookup"><span data-stu-id="60169-140">We would like to acknowledge the following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
