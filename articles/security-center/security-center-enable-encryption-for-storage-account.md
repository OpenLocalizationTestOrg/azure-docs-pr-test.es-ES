---
title: "Habilitación del cifrado para la cuenta de almacenamiento en Azure Security Center | Microsoft Docs"
description: "En este documento se muestra cómo implementar las recomendaciones de Azure Security Center de //Habilitar el cifrado para la cuenta de Azure Storage**."
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
ms.openlocfilehash: b7b2e8a12cbab68da9c8fcc348e8e3c543607007
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="e87c3-103">Habilitación del cifrado para la cuenta de Azure Storage en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="e87c3-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="e87c3-104">Azure Security Center puede recomendar que habilite el cifrado del servicio de Azure Storage para datos en reposo.</span><span class="sxs-lookup"><span data-stu-id="e87c3-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="e87c3-105">El Cifrado de servicio de almacenamiento (SSE) funciona mediante el cifrado de los datos cuando se escriben en Azure Storage y el descifrado de los datos antes de la recuperación.</span><span class="sxs-lookup"><span data-stu-id="e87c3-105">Storage Service Encryption (SSE) works by encrypting the data when it is written to Azure storage and decrypting the data before retrieval.</span></span>  <span data-ttu-id="e87c3-106">SSE actualmente solo está disponible para Azure Blob service y puede usarse para blobs en bloques, blobs de página y blobs en anexos.</span><span class="sxs-lookup"><span data-stu-id="e87c3-106">SSE is currently available only for the Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="e87c3-107">Para obtener más información, consulte [Cifrado del servicio Almacenamiento de Azure para datos en reposo (versión preliminar)](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="e87c3-107">To learn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="e87c3-108">Después de habilitar el cifrado, se cifran únicamente los datos nuevos.</span><span class="sxs-lookup"><span data-stu-id="e87c3-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="e87c3-109">Los blobs existentes en la cuenta de almacenamiento permanecen sin cifrar.</span><span class="sxs-lookup"><span data-stu-id="e87c3-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="e87c3-110">Para cifrar los blobs existentes, consulte [Preguntas más frecuentes acerca de Cifrado del servicio de Almacenamiento para datos en reposo](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="e87c3-110">To encrypt existing blobs, see the [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="e87c3-111">El Cifrado del servicio de almacenamiento solo se admite en las cuentas de almacenamiento de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e87c3-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="e87c3-112">Las cuentas de almacenamiento clásico no se admiten en este momento.</span><span class="sxs-lookup"><span data-stu-id="e87c3-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="e87c3-113">Para entender los modelos de implementación clásico y de Resource Manager, consulte [Modelos de implementación de Azure](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="e87c3-113">To understand the classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e87c3-114">En este documento se presenta el servicio mediante una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e87c3-114">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="e87c3-115">Este documento no es una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="e87c3-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="e87c3-116">Implementación de la recomendación</span><span class="sxs-lookup"><span data-stu-id="e87c3-116">Implement the recommendation</span></span>
1. <span data-ttu-id="e87c3-117">En la hoja **Recomendaciones**, seleccione **Enable encryption for Azure Storage Account** (Habilitar el cifrado para la cuenta de Azure Storage).</span><span class="sxs-lookup"><span data-stu-id="e87c3-117">In the **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="e87c3-118">![Habilitar el cifrado para la cuenta de almacenamiento][1]</span><span class="sxs-lookup"><span data-stu-id="e87c3-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="e87c3-119">Se abre la hoja **Habilitar el cifrado de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="e87c3-119">The **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="e87c3-120">En esta hoja se enumera las cuentas de Azure Storage donde el cifrado de almacenamiento está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="e87c3-120">This blade lists the Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="e87c3-121">En este ejemplo, vamos a seleccionar **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="e87c3-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="e87c3-122">![Habilitar el cifrado de almacenamiento][2]</span><span class="sxs-lookup"><span data-stu-id="e87c3-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="e87c3-123">Se abre la hoja **Cifrado** para **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="e87c3-123">The **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="e87c3-124">Seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="e87c3-124">Select **Enabled**.</span></span>
   <span data-ttu-id="e87c3-125">![Hoja de cifrado][3]</span><span class="sxs-lookup"><span data-stu-id="e87c3-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="e87c3-126">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e87c3-126">Select **Save**.</span></span>

<span data-ttu-id="e87c3-127">Ahora ha habilitado el cifrado de almacenamiento para **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="e87c3-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="e87c3-128">Consulte también</span><span class="sxs-lookup"><span data-stu-id="e87c3-128">See also</span></span>
<span data-ttu-id="e87c3-129">En este documento se muestra cómo implementar la recomendación de Azure Security Center "Habilitar el cifrado para la cuenta de Azure Storage".</span><span class="sxs-lookup"><span data-stu-id="e87c3-129">This document showed you how to implement the Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="e87c3-130">Para obtener más información acerca del cifrado de servicio de Azure Storage, vea lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e87c3-130">To learn more about Azure Storage Service Encryption, see the following:</span></span>

* [<span data-ttu-id="e87c3-131">Cifrado del servicio Almacenamiento de Azure para datos en reposo (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="e87c3-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="e87c3-132">Para más información sobre el Centro de seguridad, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="e87c3-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="e87c3-133">[Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md): aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e87c3-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="e87c3-134">[Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md): obtenga información sobre cómo supervisar el mantenimiento de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e87c3-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="e87c3-135">[Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md): obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e87c3-135">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="e87c3-136">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e87c3-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="e87c3-137">[Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md): encuentre las preguntas más frecuentes sobre el uso del servicio.</span><span class="sxs-lookup"><span data-stu-id="e87c3-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="e87c3-138">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): encuentre publicaciones de blog sobre el cumplimiento y la seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="e87c3-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
