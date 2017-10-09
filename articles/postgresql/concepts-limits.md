---
title: aaaLimitations en la base de datos de Azure para PostgreSQL | Documentos de Microsoft
description: Describe las limitaciones en Azure Database for PostgreSQL.
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: article
ms.date: 06/01/2017
ms.openlocfilehash: f53dd240e55e0633bc1dfb8ad25e1818fa8ae18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-postgresql"></a><span data-ttu-id="0dec3-103">Limitaciones en Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="0dec3-103">Limitations in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="0dec3-104">Hola base de datos de Azure para servicio PostgreSQL está en vista previa pública.</span><span class="sxs-lookup"><span data-stu-id="0dec3-104">hello Azure Database for PostgreSQL service is in public preview.</span></span> <span data-ttu-id="0dec3-105">Hello siguientes secciones describen los límites funcionales en el servicio de base de datos de Hola y capacidad.</span><span class="sxs-lookup"><span data-stu-id="0dec3-105">hello following sections describe capacity and functional limits in hello database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="0dec3-106">Máximos de nivel de servicio</span><span class="sxs-lookup"><span data-stu-id="0dec3-106">Service Tier Maximums</span></span>
<span data-ttu-id="0dec3-107">Azure Database for PostgreSQL tiene varios niveles de servicio entre los que puede elegir al crear un servidor.</span><span class="sxs-lookup"><span data-stu-id="0dec3-107">Azure Database for PostgreSQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="0dec3-108">Para obtener más información, consulte la [descripción sobre los elementos disponibles en cada nivel de servicio](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="0dec3-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="0dec3-109">Hay un número máximo de conexiones, unidades de proceso y almacenamiento en cada nivel de servicio durante la vista previa del servicio de hello, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="0dec3-109">There is a maximum number of connections, compute units, and storage in each service tier during hello service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="0dec3-110">**Conexiones máximas**</span><span class="sxs-lookup"><span data-stu-id="0dec3-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="0dec3-111">50 unidades de proceso básicas</span><span class="sxs-lookup"><span data-stu-id="0dec3-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="0dec3-112">50 conexiones</span><span class="sxs-lookup"><span data-stu-id="0dec3-112">50 connections</span></span>    |
| <span data-ttu-id="0dec3-113">100 unidades de proceso básicas</span><span class="sxs-lookup"><span data-stu-id="0dec3-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="0dec3-114">100 conexiones</span><span class="sxs-lookup"><span data-stu-id="0dec3-114">100 connections</span></span>   |
| <span data-ttu-id="0dec3-115">100 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="0dec3-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="0dec3-116">200 conexiones</span><span class="sxs-lookup"><span data-stu-id="0dec3-116">200 connections</span></span>   |
| <span data-ttu-id="0dec3-117">200 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="0dec3-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="0dec3-118">300 conexiones</span><span class="sxs-lookup"><span data-stu-id="0dec3-118">300 connections</span></span>   |
| <span data-ttu-id="0dec3-119">400 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="0dec3-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="0dec3-120">400 conexiones</span><span class="sxs-lookup"><span data-stu-id="0dec3-120">400 connections</span></span>   |
| <span data-ttu-id="0dec3-121">800 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="0dec3-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="0dec3-122">500 conexiones</span><span class="sxs-lookup"><span data-stu-id="0dec3-122">500 connections</span></span>   |
| <span data-ttu-id="0dec3-123">**Unidades de proceso máximas**</span><span class="sxs-lookup"><span data-stu-id="0dec3-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="0dec3-124">Nivel de servicio Básico</span><span class="sxs-lookup"><span data-stu-id="0dec3-124">Basic service tier</span></span>         | <span data-ttu-id="0dec3-125">100 unidades de proceso</span><span class="sxs-lookup"><span data-stu-id="0dec3-125">100 Compute Units</span></span> |
| <span data-ttu-id="0dec3-126">Nivel de servicio Estándar</span><span class="sxs-lookup"><span data-stu-id="0dec3-126">Standard service tier</span></span>      | <span data-ttu-id="0dec3-127">800 unidades de proceso</span><span class="sxs-lookup"><span data-stu-id="0dec3-127">800 Compute Units</span></span> |
| <span data-ttu-id="0dec3-128">**Almacenamiento máximo**</span><span class="sxs-lookup"><span data-stu-id="0dec3-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="0dec3-129">Nivel de servicio Básico</span><span class="sxs-lookup"><span data-stu-id="0dec3-129">Basic service tier</span></span>         | <span data-ttu-id="0dec3-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="0dec3-130">1 TB</span></span>              |
| <span data-ttu-id="0dec3-131">Nivel de servicio Estándar</span><span class="sxs-lookup"><span data-stu-id="0dec3-131">Standard service tier</span></span>      | <span data-ttu-id="0dec3-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="0dec3-132">1 TB</span></span>              |

<span data-ttu-id="0dec3-133">Cuando se alcanzan demasiadas conexiones, recibirá Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="0dec3-133">When too many connections are reached, you may receive hello following error:</span></span>
> <span data-ttu-id="0dec3-134">FATAL:  sorry, too many clients already</span><span class="sxs-lookup"><span data-stu-id="0dec3-134">FATAL:  sorry, too many clients already</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="0dec3-135">Limitaciones funcionales de la versión preliminar</span><span class="sxs-lookup"><span data-stu-id="0dec3-135">Preview functional limitations</span></span>
### <a name="scale-operations"></a><span data-ttu-id="0dec3-136">Operaciones de escalado</span><span class="sxs-lookup"><span data-stu-id="0dec3-136">Scale operations</span></span>
1.  <span data-ttu-id="0dec3-137">El escalado dinámico de servidores entre niveles de servicio no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="0dec3-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="0dec3-138">Es decir, el cambio entre los niveles de servicio Básico y Estándar.</span><span class="sxs-lookup"><span data-stu-id="0dec3-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="0dec3-139">El aumento dinámico bajo demanda del almacenamiento en un servidor creado previamente no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="0dec3-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="0dec3-140">La reducción del tamaño de almacenamiento del servidor no se admite.</span><span class="sxs-lookup"><span data-stu-id="0dec3-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="0dec3-141">Actualizaciones de la versión de servidor</span><span class="sxs-lookup"><span data-stu-id="0dec3-141">Server version upgrades</span></span>
- <span data-ttu-id="0dec3-142">La migración automatizada entre las principales versiones del motor de base de datos no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="0dec3-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="0dec3-143">Administración de suscripciones</span><span class="sxs-lookup"><span data-stu-id="0dec3-143">Subscription management</span></span>
- <span data-ttu-id="0dec3-144">El movimiento dinámico de servidores creados previamente entre grupo de suscripciones y recursos no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="0dec3-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="0dec3-145">Restauración a un momento dado</span><span class="sxs-lookup"><span data-stu-id="0dec3-145">Point-in-time-restore</span></span>
1.  <span data-ttu-id="0dec3-146">No se admite la restauración de nivel de servicio de toodifferent o tamaño de unidades de proceso y almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0dec3-146">Restoring toodifferent service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="0dec3-147">La restauración a un servidor que se ha quitado no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="0dec3-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0dec3-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0dec3-148">Next steps</span></span>
- <span data-ttu-id="0dec3-149">Comprenda lo que [hay disponible en cada plan de tarifa](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="0dec3-149">Understand [What’s available in each pricing tier](concepts-service-tiers.md)</span></span>
- <span data-ttu-id="0dec3-150">Conozca las [versiones de base de datos de PostgreSQL admitidas](concepts-supported-versions.md).</span><span class="sxs-lookup"><span data-stu-id="0dec3-150">Understand [Supported PostgreSQL Database Versions](concepts-supported-versions.md)</span></span>
- <span data-ttu-id="0dec3-151">Revisión [cómo tooBack seguridad y restauración de un servidor de base de datos de Azure para usar PostgreSQL Hola portal de Azure](howto-restore-server-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0dec3-151">Review [How tooBack up and Restore a server in Azure Database for PostgreSQL using hello Azure portal](howto-restore-server-portal.md)</span></span>
