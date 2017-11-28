---
title: Alta disponibilidad de Azure Analysis Services | Microsoft Docs
description: Garantizar una alta disponibilidad de Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 84b4c59bac1feeb8611b3a8d783d093ba073e532
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="analysis-services-high-availability"></a><span data-ttu-id="e4d9d-103">Alta disponibilidad de Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="e4d9d-103">Analysis Services high availability</span></span>
<span data-ttu-id="e4d9d-104">En este artículo se describe cómo garantizar la alta disponibilidad de los servidores de Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="e4d9d-104">This article describes assuring high availability for Azure Analysis Services servers.</span></span> 


## <a name="assuring-high-availability-during-a-service-disruption"></a><span data-ttu-id="e4d9d-105">Garantizar la alta disponibilidad durante una interrupción del servicio</span><span class="sxs-lookup"><span data-stu-id="e4d9d-105">Assuring high availability during a service disruption</span></span>
<span data-ttu-id="e4d9d-106">Aunque es poco habitual, en los centros de datos de Azure pueden producirse interrupciones.</span><span class="sxs-lookup"><span data-stu-id="e4d9d-106">While rare, an Azure data center can have an outage.</span></span> <span data-ttu-id="e4d9d-107">Cuando esto ocurre, provoca también una interrupción en el negocio que podría extenderse unos pocos minutos o incluso horas.</span><span class="sxs-lookup"><span data-stu-id="e4d9d-107">When an outage occurs, it causes a business disruption that might last a few minutes or might last for hours.</span></span> <span data-ttu-id="e4d9d-108">La alta disponibilidad se suele lograr con la redundancia de servidores.</span><span class="sxs-lookup"><span data-stu-id="e4d9d-108">High availability is most often achieved with server redundancy.</span></span> <span data-ttu-id="e4d9d-109">Con Azure Analysis Services, la redundancia se obtiene gracias a la creación de servidores secundarios adicionales en una o varias regiones.</span><span class="sxs-lookup"><span data-stu-id="e4d9d-109">With Azure Analysis Services, you can achieve redundancy by creating additional, secondary servers in one or more regions.</span></span> <span data-ttu-id="e4d9d-110">Para garantizar que los datos y metadatos de esos servidores redundantes que cree estén sincronizados con el servidor en una región que se ha desconectado, puede:</span><span class="sxs-lookup"><span data-stu-id="e4d9d-110">When creating redundant servers, to assure the data and metadata on those servers is in-sync with the server in a region that has gone offline, you can:</span></span>

* <span data-ttu-id="e4d9d-111">Implementar modelos en servidores redundantes en otras regiones.</span><span class="sxs-lookup"><span data-stu-id="e4d9d-111">Deploy models to redundant servers in other regions.</span></span> <span data-ttu-id="e4d9d-112">Este método requiere el procesamiento en paralelo de los datos en el servidor principal y en los servidores redundantes, lo que asegura que todos los servidores están sincronizados.</span><span class="sxs-lookup"><span data-stu-id="e4d9d-112">This method requires processing data on both your primary server and redundant servers in-parallel, assuring all servers are in-sync.</span></span>

* <span data-ttu-id="e4d9d-113">Realizar copias de seguridad de las bases de datos del servidor principal y restaurarlas en los servidores redundantes.</span><span class="sxs-lookup"><span data-stu-id="e4d9d-113">Back up databases from your primary server and restore on redundant servers.</span></span> <span data-ttu-id="e4d9d-114">Por ejemplo, se puede automatizar la creación de copias de seguridad en Azure Storage durante la noche y hacer una restauración en los servidores redundantes de otras regiones.</span><span class="sxs-lookup"><span data-stu-id="e4d9d-114">For example, you can automate nightly backups to Azure storage, and restore to other redundant servers in other regions.</span></span> 

<span data-ttu-id="e4d9d-115">En cualquier caso, si se produce una interrupción en el servidor principal, se deben cambiar las cadenas de conexión en los clientes de informes para conectarse al servidor en otro centro de datos regional.</span><span class="sxs-lookup"><span data-stu-id="e4d9d-115">In either case, if your primary server experiences an outage, you must change the connection strings in reporting clients to connect to the server in a different regional datacenter.</span></span> <span data-ttu-id="e4d9d-116">Este cambio debe considerarse un último recurso y solo si se produce una interrupción catastrófica del centro de datos regional.</span><span class="sxs-lookup"><span data-stu-id="e4d9d-116">This change should be considered a last resort and only if a catastrophic regional data center outage occurs.</span></span> <span data-ttu-id="e4d9d-117">Es más probable que una interrupción en el centro de datos que hospeda el servidor principal se recupere antes de que se puedan actualizar las conexiones en todos los clientes.</span><span class="sxs-lookup"><span data-stu-id="e4d9d-117">It's more likely a data center outage hosting your primary server would come back online before you could update connections on all clients.</span></span> 



## <a name="related-information"></a><span data-ttu-id="e4d9d-118">Información relacionada</span><span class="sxs-lookup"><span data-stu-id="e4d9d-118">Related information</span></span>
<span data-ttu-id="e4d9d-119">[Copia de seguridad y restauración](analysis-services-backup.md) </span><span class="sxs-lookup"><span data-stu-id="e4d9d-119">[Backup and restore](analysis-services-backup.md) </span></span>  
[<span data-ttu-id="e4d9d-120">Administración de Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="e4d9d-120">Manage Azure Analysis Services</span></span>](analysis-services-manage.md) 

