---
title: "Qué hacer si se produce una interrupción del servicio de Azure que afecte a Azure Key Vault | Microsoft Docs"
description: "Descubra qué hacer en caso de que se produzca una interrupción del servicio de Azure que afecte a Azure Key Vault."
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
ms.openlocfilehash: 6419d54c54e7d19103419262b79e7a5268b2268c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="6f7ad-103">Redundancia y disponibilidad del Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="6f7ad-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="6f7ad-104">El Almacén de claves de Azure tiene varias capas de redundancia para garantizar la disponibilidad de las claves y los secretos para su aplicación, aunque se produzcan errores de componentes individuales del servicio.</span><span class="sxs-lookup"><span data-stu-id="6f7ad-104">Azure Key Vault features multiple layers of redundancy to make sure that your keys and secrets remain available to your application even if individual components of the service fail.</span></span>

<span data-ttu-id="6f7ad-105">El contenido del almacén de claves se replica dentro de la región y en una región secundaria que se encuentre a una distancia mínima de 241 km pero dentro de la misma ubicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="6f7ad-105">The contents of your key vault are replicated within the region and to a secondary region at least 150 miles away but within the same geography.</span></span> <span data-ttu-id="6f7ad-106">Así se mantiene la durabilidad de las claves y los secretos.</span><span class="sxs-lookup"><span data-stu-id="6f7ad-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="6f7ad-107">Consulte el artículo sobre las [regiones emparejadas de Azure](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) para obtener más información sobre pares de regiones específicas.</span><span class="sxs-lookup"><span data-stu-id="6f7ad-107">See the [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="6f7ad-108">Si se produce un error en algún componente individual dentro del servicio del almacén de claves, los componentes alternativos de la región se encargan de atender la solicitud para garantizar que no se pierde funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="6f7ad-108">If individual components within the key vault service fail, alternate components within the region step in to serve your request to make sure that there is no degradation of functionality.</span></span> <span data-ttu-id="6f7ad-109">No es necesario realizar ninguna acción para ello.</span><span class="sxs-lookup"><span data-stu-id="6f7ad-109">You do not need to take any action to trigger this.</span></span> <span data-ttu-id="6f7ad-110">Se lleva a cabo automáticamente y es transparente para el programador.</span><span class="sxs-lookup"><span data-stu-id="6f7ad-110">It happens automatically and will be transparent to you.</span></span>

<span data-ttu-id="6f7ad-111">En el caso excepcional de que toda una región de Azure pase a estar no disponible, las solicitudes efectuadas a Azure Key Vault de esa región se enrutarán automáticamente (un proceso conocido como *conmutación por error*) a una región secundaria.</span><span class="sxs-lookup"><span data-stu-id="6f7ad-111">In the rare event that an entire Azure region is unavailable, the requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) to a secondary region.</span></span> <span data-ttu-id="6f7ad-112">Cuando la región primaria vuelva a estar disponible, las solicitudes se enrutarán a ella nuevamente (*conmutación por recuperación*).</span><span class="sxs-lookup"><span data-stu-id="6f7ad-112">When the primary region is available again, requests are routed back (*failed back*) to the primary region.</span></span> <span data-ttu-id="6f7ad-113">Conviene insistir en que no es necesaria ninguna acción, ya que este proceso se realiza automáticamente.</span><span class="sxs-lookup"><span data-stu-id="6f7ad-113">Again, you do not need to take any action because this happens automatically.</span></span>

<span data-ttu-id="6f7ad-114">Hay algunas advertencias que deben tenerse en cuenta:</span><span class="sxs-lookup"><span data-stu-id="6f7ad-114">There are a few caveats to be aware of:</span></span>

* <span data-ttu-id="6f7ad-115">La conmutación por error de región, en caso de producirse, puede tardar varios minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="6f7ad-115">In the event of a region failover, it may take a few minutes for the service to fail over.</span></span> <span data-ttu-id="6f7ad-116">Las solicitudes realizadas durante este intervalo podrían no efectuarse correctamente mientras no se complete la conmutación.</span><span class="sxs-lookup"><span data-stu-id="6f7ad-116">Requests that are made during this time may fail until the failover completes.</span></span>
* <span data-ttu-id="6f7ad-117">Una vez finalizada una conmutación por error, el almacén de claves se encontrará en modo de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="6f7ad-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="6f7ad-118">Las solicitudes compatibles con este modo son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="6f7ad-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="6f7ad-119">Enumeración de almacenes de claves</span><span class="sxs-lookup"><span data-stu-id="6f7ad-119">List key vaults</span></span>
  * <span data-ttu-id="6f7ad-120">Obtención de propiedades de los almacenes de claves</span><span class="sxs-lookup"><span data-stu-id="6f7ad-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="6f7ad-121">Enumeración de secretos</span><span class="sxs-lookup"><span data-stu-id="6f7ad-121">List secrets</span></span>
  * <span data-ttu-id="6f7ad-122">Obtención de secretos</span><span class="sxs-lookup"><span data-stu-id="6f7ad-122">Get secrets</span></span>
  * <span data-ttu-id="6f7ad-123">Enumeración de claves</span><span class="sxs-lookup"><span data-stu-id="6f7ad-123">List keys</span></span>
  * <span data-ttu-id="6f7ad-124">Obtención de (propiedades de) claves</span><span class="sxs-lookup"><span data-stu-id="6f7ad-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="6f7ad-125">Cifrar</span><span class="sxs-lookup"><span data-stu-id="6f7ad-125">Encrypt</span></span>
  * <span data-ttu-id="6f7ad-126">Descifrado</span><span class="sxs-lookup"><span data-stu-id="6f7ad-126">Decrypt</span></span>
  * <span data-ttu-id="6f7ad-127">Encapsulado</span><span class="sxs-lookup"><span data-stu-id="6f7ad-127">Wrap</span></span>
  * <span data-ttu-id="6f7ad-128">Desencapsulado</span><span class="sxs-lookup"><span data-stu-id="6f7ad-128">Unwrap</span></span>
  * <span data-ttu-id="6f7ad-129">Verify</span><span class="sxs-lookup"><span data-stu-id="6f7ad-129">Verify</span></span>
  * <span data-ttu-id="6f7ad-130">Firma</span><span class="sxs-lookup"><span data-stu-id="6f7ad-130">Sign</span></span>
  * <span data-ttu-id="6f7ad-131">Copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="6f7ad-131">Backup</span></span>
* <span data-ttu-id="6f7ad-132">Cuando tenga lugar la conmutación por error, todos los tipos de solicitudes (incluidas de lectura *y* escritura) pasarán a estar disponibles.</span><span class="sxs-lookup"><span data-stu-id="6f7ad-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

