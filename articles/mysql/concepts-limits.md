---
title: aaaLimitations en la base de datos de Azure para MySQL | Documentos de Microsoft
description: "Describe las limitaciones de la versión preliminar en Azure Database for MySQL."
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 9c877c592bf640f62182d8761c9c51363882d706
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a><span data-ttu-id="132af-103">Limitaciones en Azure Database for MySQL (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="132af-103">Limitations in Azure Database for MySQL (Preview)</span></span>
<span data-ttu-id="132af-104">Hola base de datos de Azure para el servicio MySQL está en vista previa pública.</span><span class="sxs-lookup"><span data-stu-id="132af-104">hello Azure Database for MySQL service is in public preview.</span></span> <span data-ttu-id="132af-105">Hello siguientes secciones describen los límites funcionales en el servicio de base de datos de Hola y capacidad.</span><span class="sxs-lookup"><span data-stu-id="132af-105">hello following sections describe capacity and functional limits in hello database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="132af-106">Máximos de nivel de servicio</span><span class="sxs-lookup"><span data-stu-id="132af-106">Service Tier Maximums</span></span>
<span data-ttu-id="132af-107">Azure Database for MySQL tiene varios niveles de servicio entre los que puede elegir al crear un servidor.</span><span class="sxs-lookup"><span data-stu-id="132af-107">Azure Database for MySQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="132af-108">Para obtener más información, consulte la [descripción sobre los elementos disponibles en cada nivel de servicio](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="132af-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="132af-109">Hay un número máximo de conexiones, unidades de proceso y almacenamiento en cada nivel de servicio durante la vista previa del servicio de hello, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="132af-109">There is a maximum number of connections, compute units, and storage in each service tier during hello service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="132af-110">**Conexiones máximas**</span><span class="sxs-lookup"><span data-stu-id="132af-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="132af-111">50 unidades de proceso básicas</span><span class="sxs-lookup"><span data-stu-id="132af-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="132af-112">50 conexiones</span><span class="sxs-lookup"><span data-stu-id="132af-112">50 connections</span></span>    |
| <span data-ttu-id="132af-113">100 unidades de proceso básicas</span><span class="sxs-lookup"><span data-stu-id="132af-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="132af-114">100 conexiones</span><span class="sxs-lookup"><span data-stu-id="132af-114">100 connections</span></span>   |
| <span data-ttu-id="132af-115">100 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="132af-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="132af-116">200 conexiones</span><span class="sxs-lookup"><span data-stu-id="132af-116">200 connections</span></span>   |
| <span data-ttu-id="132af-117">200 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="132af-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="132af-118">300 conexiones</span><span class="sxs-lookup"><span data-stu-id="132af-118">300 connections</span></span>   |
| <span data-ttu-id="132af-119">400 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="132af-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="132af-120">400 conexiones</span><span class="sxs-lookup"><span data-stu-id="132af-120">400 connections</span></span>   |
| <span data-ttu-id="132af-121">800 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="132af-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="132af-122">500 conexiones</span><span class="sxs-lookup"><span data-stu-id="132af-122">500 connections</span></span>   |
| <span data-ttu-id="132af-123">**Unidades de proceso máximas**</span><span class="sxs-lookup"><span data-stu-id="132af-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="132af-124">Nivel de servicio Básico</span><span class="sxs-lookup"><span data-stu-id="132af-124">Basic service tier</span></span>         | <span data-ttu-id="132af-125">100 unidades de proceso</span><span class="sxs-lookup"><span data-stu-id="132af-125">100 Compute Units</span></span> |
| <span data-ttu-id="132af-126">Nivel de servicio Estándar</span><span class="sxs-lookup"><span data-stu-id="132af-126">Standard service tier</span></span>      | <span data-ttu-id="132af-127">800 unidades de proceso</span><span class="sxs-lookup"><span data-stu-id="132af-127">800 Compute Units</span></span> |
| <span data-ttu-id="132af-128">**Almacenamiento máximo**</span><span class="sxs-lookup"><span data-stu-id="132af-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="132af-129">Nivel de servicio Básico</span><span class="sxs-lookup"><span data-stu-id="132af-129">Basic service tier</span></span>         | <span data-ttu-id="132af-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="132af-130">1 TB</span></span>              |
| <span data-ttu-id="132af-131">Nivel de servicio Estándar</span><span class="sxs-lookup"><span data-stu-id="132af-131">Standard service tier</span></span>      | <span data-ttu-id="132af-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="132af-132">1 TB</span></span>              |

<span data-ttu-id="132af-133">Cuando se alcanzan demasiadas conexiones, recibirá Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="132af-133">When too many connections are reached, you may receive hello following error:</span></span>
> <span data-ttu-id="132af-134">ERROR 1040 (08004): Too many connections</span><span class="sxs-lookup"><span data-stu-id="132af-134">ERROR 1040 (08004): Too many connections</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="132af-135">Limitaciones funcionales de versión preliminar:</span><span class="sxs-lookup"><span data-stu-id="132af-135">Preview functional limitations:</span></span>
### <a name="scale-operations"></a><span data-ttu-id="132af-136">Operaciones de escalado:</span><span class="sxs-lookup"><span data-stu-id="132af-136">Scale operations:</span></span>
1.  <span data-ttu-id="132af-137">El escalado dinámico de servidores entre niveles de servicio no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="132af-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="132af-138">Es decir, el cambio entre los niveles de servicio Básico y Estándar.</span><span class="sxs-lookup"><span data-stu-id="132af-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="132af-139">El aumento dinámico bajo demanda del almacenamiento en un servidor creado previamente no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="132af-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="132af-140">La reducción del tamaño de almacenamiento del servidor no se admite.</span><span class="sxs-lookup"><span data-stu-id="132af-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="132af-141">Actualizaciones de la versión de servidor:</span><span class="sxs-lookup"><span data-stu-id="132af-141">Server version upgrades:</span></span>
- <span data-ttu-id="132af-142">La migración automatizada entre las principales versiones del motor de base de datos no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="132af-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="132af-143">Administración de suscripciones:</span><span class="sxs-lookup"><span data-stu-id="132af-143">Subscription management:</span></span>
- <span data-ttu-id="132af-144">El movimiento dinámico de servidores creados previamente entre grupo de suscripciones y recursos no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="132af-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="132af-145">Restauración a un momento dado:</span><span class="sxs-lookup"><span data-stu-id="132af-145">Point-in-time-restore:</span></span>
1.  <span data-ttu-id="132af-146">No se admite la restauración de nivel de servicio de toodifferent o tamaño de unidades de proceso y almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="132af-146">Restoring toodifferent service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="132af-147">La restauración a un servidor que se ha quitado no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="132af-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="132af-148">Pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="132af-148">Next Steps:</span></span>
<span data-ttu-id="132af-149">[What’s available in each service tier](concepts-service-tiers.md)(Elementos disponibles en cada nivel de servicio)
[Supported MySQL Database Versions](concepts-supported-versions.md) (Versiones admitidas de Base de datos MySQL)</span><span class="sxs-lookup"><span data-stu-id="132af-149">[What’s available in each service tier](concepts-service-tiers.md)
[Supported MySQL Database Versions](concepts-supported-versions.md)</span></span>
