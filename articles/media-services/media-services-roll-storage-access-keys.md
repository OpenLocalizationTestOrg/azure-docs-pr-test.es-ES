---
title: "Servicios de multimedia de aaaUpdate después de revertir el almacenamiento de claves de acceso | Documentos de Microsoft"
description: "En este artículo se proporcionan instrucciones sobre cómo tooupdate los servicios multimedia después de revertir el almacenamiento de claves de acceso."
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
ms.openlocfilehash: 26fa7a75a73397842aaebda59516a00f68ab97f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="f6fef-103">Actualización de Media Services después de revertir las claves de acceso de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f6fef-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="f6fef-104">Cuando se crea una nueva cuenta de servicios de multimedia de Azure (AMS), también deberá tooselect un almacenamiento de Azure que es la cuenta utiliza toostore su contenido multimedia.</span><span class="sxs-lookup"><span data-stu-id="f6fef-104">When you create a new Azure Media Services (AMS) account, you are also asked tooselect an Azure Storage account that is used toostore your media content.</span></span> <span data-ttu-id="f6fef-105">Puede agregar tooyour de cuentas de almacenamiento más de una cuenta de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="f6fef-105">You can add more than one storage accounts tooyour Media Services account.</span></span> <span data-ttu-id="f6fef-106">Este tema se muestra cómo toorotate claves de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f6fef-106">This topic shows how toorotate storage keys.</span></span> <span data-ttu-id="f6fef-107">También muestra cómo las cuentas de almacenamiento de tooadd tooa cuenta de multimedia.</span><span class="sxs-lookup"><span data-stu-id="f6fef-107">It also shows how tooadd storage accounts tooa media account.</span></span> 

<span data-ttu-id="f6fef-108">acciones de hello tooperform descritas en este tema, debería utilizar [API ARM](https://docs.microsoft.com/rest/api/media/mediaservice) y [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span><span class="sxs-lookup"><span data-stu-id="f6fef-108">tooperform hello actions described in this topic, you should be using [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span></span>  <span data-ttu-id="f6fef-109">Para obtener más información, consulte [cómo toomanage Azure recursos con PowerShell y Administrador de recursos](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f6fef-109">For more information, see [How toomanage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

## <a name="overview"></a><span data-ttu-id="f6fef-110">Información general</span><span class="sxs-lookup"><span data-stu-id="f6fef-110">Overview</span></span>

<span data-ttu-id="f6fef-111">Cuando se crea una nueva cuenta de almacenamiento, Azure genera dos claves de acceso de almacenamiento de 512 bits, que son utilizado tooauthenticate acceso a la cuenta de almacenamiento de tooyour.</span><span class="sxs-lookup"><span data-stu-id="f6fef-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used tooauthenticate access tooyour storage account.</span></span> <span data-ttu-id="f6fef-112">tookeep las conexiones de almacenamiento más seguras, se recomienda tooperiodically volver a generar y rotación la clave de acceso de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f6fef-112">tookeep your storage connections more secure, it is recommended tooperiodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="f6fef-113">Dos claves de acceso (principales y secundarias) aparecen en orden tooenable se toomaintain conexiones toohello cuenta de almacenamiento mediante uno tener acceso a clave mientras regenera Hola otra clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="f6fef-113">Two access keys (primary and secondary) are provided in order tooenable you toomaintain connections toohello storage account using one access key while you regenerate hello other access key.</span></span> <span data-ttu-id="f6fef-114">Este procedimiento se conoce también como "rotación de claves de acceso".</span><span class="sxs-lookup"><span data-stu-id="f6fef-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="f6fef-115">Servicios multimedia depende de una clave de almacenamiento proporcionada tooit.</span><span class="sxs-lookup"><span data-stu-id="f6fef-115">Media Services depends on a storage key provided tooit.</span></span> <span data-ttu-id="f6fef-116">En concreto, localizadores hello toostream usado o descargan los activos dependen de tecla de acceso de almacenamiento especificada de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6fef-116">Specifically, hello locators that are used toostream or download your assets depend on hello specified storage access key.</span></span> <span data-ttu-id="f6fef-117">Cuando se crea una cuenta de AMS tome una dependencia en la clave de acceso de almacenamiento principal de Hola de forma predeterminada, pero como un usuario puede actualizar la clave de almacenamiento de hello AMS tiene.</span><span class="sxs-lookup"><span data-stu-id="f6fef-117">When an AMS account is created it takes a dependency on hello primary storage access key by default but as a user you can update hello storage key that AMS has.</span></span> <span data-ttu-id="f6fef-118">Debe asegurarse de que los servicios de multimedia toolet saber qué toouse clave siguiendo los pasos descritos en este tema.</span><span class="sxs-lookup"><span data-stu-id="f6fef-118">You must make sure toolet Media Services know which key toouse by following steps described in this topic.</span></span>  

>[!NOTE]
> <span data-ttu-id="f6fef-119">Si tiene varias cuentas de almacenamiento, realizaría este procedimiento con cada una.</span><span class="sxs-lookup"><span data-stu-id="f6fef-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="f6fef-120">orden de Hello en el que Rotar claves de almacenamiento no es fijo.</span><span class="sxs-lookup"><span data-stu-id="f6fef-120">hello order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="f6fef-121">Puede rotar la clave secundaria de hello en primer lugar y, a continuación, Hola principal clave o viceversa.</span><span class="sxs-lookup"><span data-stu-id="f6fef-121">You can rotate hello secondary key first and then hello primary key or vice versa.</span></span>
>
> <span data-ttu-id="f6fef-122">Antes de ejecutar los pasos descritos en este tema en una cuenta de producción, asegúrese de que tootest ellos en una cuenta de preproducción.</span><span class="sxs-lookup"><span data-stu-id="f6fef-122">Before executing steps described in this topic on a production account, make sure tootest them on a pre-production account.</span></span>
>

## <a name="steps-toorotate-storage-keys"></a><span data-ttu-id="f6fef-123">Claves de almacenamiento de toorotate de pasos</span><span class="sxs-lookup"><span data-stu-id="f6fef-123">Steps toorotate storage keys</span></span> 
 
 1. <span data-ttu-id="f6fef-124">Cambio Hola clave cuenta de almacenamiento principal a través del cmdlet de powershell de Hola o [Azure](https://portal.azure.com/) portal.</span><span class="sxs-lookup"><span data-stu-id="f6fef-124">Change hello storage account Primary key through hello powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="f6fef-125">Llame al cmdlet AzureRmMediaServiceStorageKeys de sincronización con los parámetros adecuados tooforce medios cuenta toopick las claves de cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f6fef-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params tooforce media account toopick up storage account keys</span></span>
 
    <span data-ttu-id="f6fef-126">Hola de ejemplo siguiente muestra cómo toosync claves toostorage cuentas.</span><span class="sxs-lookup"><span data-stu-id="f6fef-126">hello following example shows how toosync keys toostorage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="f6fef-127">Espere una hora más o menos.</span><span class="sxs-lookup"><span data-stu-id="f6fef-127">Wait an hour or so.</span></span> <span data-ttu-id="f6fef-128">Compruebe que están trabajando escenarios de transmisión por secuencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6fef-128">Verify hello streaming scenarios are working.</span></span>
 4. <span data-ttu-id="f6fef-129">Cambiar la clave secundaria de cuenta de almacenamiento mediante el cmdlet de powershell de Hola o portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6fef-129">Change storage account secondary key through hello powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="f6fef-130">Llame a powershell AzureRmMediaServiceStorageKeys de sincronización con los parámetros adecuados tooforce medios cuenta toopick seguridad nuevas claves de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f6fef-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params tooforce media account toopick up new storage account keys.</span></span> 
 6. <span data-ttu-id="f6fef-131">Espere una hora más o menos.</span><span class="sxs-lookup"><span data-stu-id="f6fef-131">Wait an hour or so.</span></span> <span data-ttu-id="f6fef-132">Compruebe que están trabajando escenarios de transmisión por secuencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6fef-132">Verify hello streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="f6fef-133">Un ejemplos de cmdlet de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6fef-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="f6fef-134">Hello en el ejemplo siguiente se muestra cómo tooget Hola cuenta de almacenamiento y sincronizarla con cuenta de hello AMS.</span><span class="sxs-lookup"><span data-stu-id="f6fef-134">hello following example demonstrates how tooget hello storage account and sync it with hello AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a><span data-ttu-id="f6fef-135">Cuentas de almacenamiento de información de pasos tooadd tooyour AMS cuenta</span><span class="sxs-lookup"><span data-stu-id="f6fef-135">Steps tooadd storage accounts tooyour AMS account</span></span>

<span data-ttu-id="f6fef-136">Hello siguiente tema muestra cómo las cuentas de almacenamiento de tooadd tooyour AMS cuenta: [adjuntar varios tooa de cuentas de almacenamiento cuenta de servicios multimedia](meda-services-managing-multiple-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="f6fef-136">hello following topic shows how tooadd storage accounts tooyour AMS account: [Attach multiple storage accounts tooa Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f6fef-137">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="f6fef-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f6fef-138">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="f6fef-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="f6fef-139">Agradecimientos</span><span class="sxs-lookup"><span data-stu-id="f6fef-139">Acknowledgments</span></span>
<span data-ttu-id="f6fef-140">Nos gustaría hello tooacknowledge siguientes personas que han contribuido a la creación de este documento: Cenk Dingiloglu, Gada Milán, Seva Titov.</span><span class="sxs-lookup"><span data-stu-id="f6fef-140">We would like tooacknowledge hello following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
