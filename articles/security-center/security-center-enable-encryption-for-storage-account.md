---
title: aaaEnable cifrado para la cuenta de almacenamiento en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendaciones de Azure Security Center ** habilitar el cifrado para Azure almacenamiento cuenta **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="73836-103">Habilitación del cifrado para la cuenta de Azure Storage en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="73836-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="73836-104">Azure Security Center puede recomendar que habilite el cifrado del servicio de Azure Storage para datos en reposo.</span><span class="sxs-lookup"><span data-stu-id="73836-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="73836-105">Cifrado de servicio de almacenamiento (SSE) funciona al cifrar los datos de hello cuando se escribe tooAzure almacenamiento y descifrar datos Hola antes de la recuperación.</span><span class="sxs-lookup"><span data-stu-id="73836-105">Storage Service Encryption (SSE) works by encrypting hello data when it is written tooAzure storage and decrypting hello data before retrieval.</span></span>  <span data-ttu-id="73836-106">SSE actualmente solo está disponible para hello servicio Blob de Azure y puede usarse para blobs en bloques, blobs de página y blobs en anexos.</span><span class="sxs-lookup"><span data-stu-id="73836-106">SSE is currently available only for hello Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="73836-107">más información, consulte toolearn [cifrado del servicio de almacenamiento de datos en reposo](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="73836-107">toolearn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="73836-108">Después de habilitar el cifrado, se cifran únicamente los datos nuevos.</span><span class="sxs-lookup"><span data-stu-id="73836-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="73836-109">Los blobs existentes en la cuenta de almacenamiento permanecen sin cifrar.</span><span class="sxs-lookup"><span data-stu-id="73836-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="73836-110">tooencrypt blobs existentes, vea hello [preguntas más frecuentes sobre el cifrado del servicio de almacenamiento](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="73836-110">tooencrypt existing blobs, see hello [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="73836-111">El Cifrado del servicio de almacenamiento solo se admite en las cuentas de almacenamiento de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="73836-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="73836-112">Las cuentas de almacenamiento clásico no se admiten en este momento.</span><span class="sxs-lookup"><span data-stu-id="73836-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="73836-113">Hola toounderstand clásico y modelos de implementación del Administrador de recursos, consulte [modelos de implementación de Azure](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="73836-113">toounderstand hello classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="73836-114">Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="73836-114">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="73836-115">Este documento no es una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="73836-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="73836-116">Implementar la recomendación de Hola</span><span class="sxs-lookup"><span data-stu-id="73836-116">Implement hello recommendation</span></span>
1. <span data-ttu-id="73836-117">Hola **recomendaciones** hoja, seleccione **habilitar el cifrado para la cuenta de almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="73836-117">In hello **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="73836-118">![Habilitar el cifrado para la cuenta de almacenamiento][1]</span><span class="sxs-lookup"><span data-stu-id="73836-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="73836-119">Hola **Habilitar cifrado de almacenamiento** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="73836-119">hello **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="73836-120">Esta hoja enumera las cuentas de almacenamiento de Azure Hola donde se deshabilita el cifrado de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="73836-120">This blade lists hello Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="73836-121">En este ejemplo, vamos a seleccionar **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="73836-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="73836-122">![Habilitar el cifrado de almacenamiento][2]</span><span class="sxs-lookup"><span data-stu-id="73836-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="73836-123">Hola **cifrado** hoja para **storageacct1** se abre.</span><span class="sxs-lookup"><span data-stu-id="73836-123">hello **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="73836-124">Seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="73836-124">Select **Enabled**.</span></span>
   <span data-ttu-id="73836-125">![Hoja de cifrado][3]</span><span class="sxs-lookup"><span data-stu-id="73836-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="73836-126">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="73836-126">Select **Save**.</span></span>

<span data-ttu-id="73836-127">Ahora ha habilitado el cifrado de almacenamiento para **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="73836-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="73836-128">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="73836-128">See also</span></span>
<span data-ttu-id="73836-129">Este documento se ha explicado cómo tooimplement Hola centro de seguridad recomendación "Habilitar el cifrado para la cuenta de almacenamiento de Azure."</span><span class="sxs-lookup"><span data-stu-id="73836-129">This document showed you how tooimplement hello Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="73836-130">toolearn más información acerca del cifrado del servicio de almacenamiento de Azure, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="73836-130">toolearn more about Azure Storage Service Encryption, see hello following:</span></span>

* [<span data-ttu-id="73836-131">Cifrado del servicio Azure Storage para datos en reposo (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="73836-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="73836-132">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="73836-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="73836-133">[Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) -Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="73836-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="73836-134">[Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) -Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="73836-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="73836-135">[Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md) -Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.</span><span class="sxs-lookup"><span data-stu-id="73836-135">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="73836-136">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="73836-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="73836-137">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md) -buscar preguntas más frecuentes sobre el uso de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="73836-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="73836-138">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): encuentre publicaciones de blog sobre el cumplimiento y la seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="73836-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
