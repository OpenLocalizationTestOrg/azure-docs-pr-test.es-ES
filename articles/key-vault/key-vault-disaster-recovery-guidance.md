---
title: "aaaWhat toodo en caso de hello de una interrupción del servicio de Azure que afecta al almacén de claves de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de qué toodo en caso de hello de una interrupción del servicio de Azure que afecta al almacén de claves de Azure."
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="8e8f8-103">Redundancia y disponibilidad del Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="8e8f8-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="8e8f8-104">Almacén de claves de Azure ofrece varios niveles de redundancia toomake seguro de que sus claves y secretos seguirán siendo aplicación tooyour disponible incluso si los componentes individuales de hello producirá un error de servicio.</span><span class="sxs-lookup"><span data-stu-id="8e8f8-104">Azure Key Vault features multiple layers of redundancy toomake sure that your keys and secrets remain available tooyour application even if individual components of hello service fail.</span></span>

<span data-ttu-id="8e8f8-105">Hello contenido de su almacén de claves se replica dentro de la región de Hola y región secundaria tooa al menos 150 millas inmediatamente, pero dentro de hello mismo geography.</span><span class="sxs-lookup"><span data-stu-id="8e8f8-105">hello contents of your key vault are replicated within hello region and tooa secondary region at least 150 miles away but within hello same geography.</span></span> <span data-ttu-id="8e8f8-106">Así se mantiene la durabilidad de las claves y los secretos.</span><span class="sxs-lookup"><span data-stu-id="8e8f8-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="8e8f8-107">Vea hello [Azure emparejado regiones](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) documento para obtener más información sobre los pares de región específica.</span><span class="sxs-lookup"><span data-stu-id="8e8f8-107">See hello [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="8e8f8-108">Si se produce un error en componentes individuales de servicio de almacén de claves de hello, componentes alternativos dentro de la región de hello paso en tooserve su toomake solicitud seguro de que no hay ninguna degradación de la funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="8e8f8-108">If individual components within hello key vault service fail, alternate components within hello region step in tooserve your request toomake sure that there is no degradation of functionality.</span></span> <span data-ttu-id="8e8f8-109">No es necesario tootake cualquier acción tootrigger esto.</span><span class="sxs-lookup"><span data-stu-id="8e8f8-109">You do not need tootake any action tootrigger this.</span></span> <span data-ttu-id="8e8f8-110">Se produce automáticamente y será tooyou transparente.</span><span class="sxs-lookup"><span data-stu-id="8e8f8-110">It happens automatically and will be transparent tooyou.</span></span>

<span data-ttu-id="8e8f8-111">En el caso poco frecuente de Hola que toda una región de Azure no está disponible, automáticamente se enrutan las solicitudes de hello realizados de almacén de claves de Azure en dicha región (*conmutarán por error*) tooa de región secundaria.</span><span class="sxs-lookup"><span data-stu-id="8e8f8-111">In hello rare event that an entire Azure region is unavailable, hello requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) tooa secondary region.</span></span> <span data-ttu-id="8e8f8-112">Cuando la región principal de hello esté disponible de nuevo, las solicitudes se enrutan volver (*no se pudo volver*) toohello de región principal.</span><span class="sxs-lookup"><span data-stu-id="8e8f8-112">When hello primary region is available again, requests are routed back (*failed back*) toohello primary region.</span></span> <span data-ttu-id="8e8f8-113">Una vez más, no es necesario tootake ninguna acción porque esto sucede automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8e8f8-113">Again, you do not need tootake any action because this happens automatically.</span></span>

<span data-ttu-id="8e8f8-114">Hay unos toobe advertencias en cuenta:</span><span class="sxs-lookup"><span data-stu-id="8e8f8-114">There are a few caveats toobe aware of:</span></span>

* <span data-ttu-id="8e8f8-115">En caso de hello de una región de conmutación por error, puede tardar unos minutos para hello servicio toofail.</span><span class="sxs-lookup"><span data-stu-id="8e8f8-115">In hello event of a region failover, it may take a few minutes for hello service toofail over.</span></span> <span data-ttu-id="8e8f8-116">Las solicitudes realizadas durante este período, pueden producir un error hasta que se complete la conmutación por error de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e8f8-116">Requests that are made during this time may fail until hello failover completes.</span></span>
* <span data-ttu-id="8e8f8-117">Una vez finalizada una conmutación por error, el almacén de claves se encontrará en modo de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="8e8f8-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="8e8f8-118">Las solicitudes compatibles con este modo son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="8e8f8-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="8e8f8-119">Enumeración de almacenes de claves</span><span class="sxs-lookup"><span data-stu-id="8e8f8-119">List key vaults</span></span>
  * <span data-ttu-id="8e8f8-120">Obtención de propiedades de los almacenes de claves</span><span class="sxs-lookup"><span data-stu-id="8e8f8-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="8e8f8-121">Enumeración de secretos</span><span class="sxs-lookup"><span data-stu-id="8e8f8-121">List secrets</span></span>
  * <span data-ttu-id="8e8f8-122">Obtención de secretos</span><span class="sxs-lookup"><span data-stu-id="8e8f8-122">Get secrets</span></span>
  * <span data-ttu-id="8e8f8-123">Enumeración de claves</span><span class="sxs-lookup"><span data-stu-id="8e8f8-123">List keys</span></span>
  * <span data-ttu-id="8e8f8-124">Obtención de (propiedades de) claves</span><span class="sxs-lookup"><span data-stu-id="8e8f8-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="8e8f8-125">Cifrar</span><span class="sxs-lookup"><span data-stu-id="8e8f8-125">Encrypt</span></span>
  * <span data-ttu-id="8e8f8-126">Descifrado</span><span class="sxs-lookup"><span data-stu-id="8e8f8-126">Decrypt</span></span>
  * <span data-ttu-id="8e8f8-127">Encapsulado</span><span class="sxs-lookup"><span data-stu-id="8e8f8-127">Wrap</span></span>
  * <span data-ttu-id="8e8f8-128">Desencapsulado</span><span class="sxs-lookup"><span data-stu-id="8e8f8-128">Unwrap</span></span>
  * <span data-ttu-id="8e8f8-129">Verify</span><span class="sxs-lookup"><span data-stu-id="8e8f8-129">Verify</span></span>
  * <span data-ttu-id="8e8f8-130">Firma</span><span class="sxs-lookup"><span data-stu-id="8e8f8-130">Sign</span></span>
  * <span data-ttu-id="8e8f8-131">Copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="8e8f8-131">Backup</span></span>
* <span data-ttu-id="8e8f8-132">Cuando tenga lugar la conmutación por error, todos los tipos de solicitudes (incluidas de lectura *y* escritura) pasarán a estar disponibles.</span><span class="sxs-lookup"><span data-stu-id="8e8f8-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

