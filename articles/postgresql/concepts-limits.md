---
title: Limitaciones en Azure Database for PostgreSQL | Microsoft Docs
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
ms.openlocfilehash: 38988fc5c0dc05331ea078534cd1a05e9eca2493
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="limitations-in-azure-database-for-postgresql"></a><span data-ttu-id="15dc0-103">Limitaciones en Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="15dc0-103">Limitations in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="15dc0-104">El servicio Azure Database for PostgreSQL se encuentra en versión preliminar pública.</span><span class="sxs-lookup"><span data-stu-id="15dc0-104">The Azure Database for PostgreSQL service is in public preview.</span></span> <span data-ttu-id="15dc0-105">En las secciones siguientes se describen los límites de capacidad y funcionales en el servicio de base de datos.</span><span class="sxs-lookup"><span data-stu-id="15dc0-105">The following sections describe capacity and functional limits in the database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="15dc0-106">Máximos de nivel de servicio</span><span class="sxs-lookup"><span data-stu-id="15dc0-106">Service Tier Maximums</span></span>
<span data-ttu-id="15dc0-107">Azure Database for PostgreSQL tiene varios niveles de servicio entre los que puede elegir al crear un servidor.</span><span class="sxs-lookup"><span data-stu-id="15dc0-107">Azure Database for PostgreSQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="15dc0-108">Para obtener más información, consulte la [descripción sobre los elementos disponibles en cada nivel de servicio](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="15dc0-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="15dc0-109">Hay un número máximo de conexiones, unidades de proceso y almacenamiento en cada nivel de servicio mientras el servicio esté en versión preliminar, y son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="15dc0-109">There is a maximum number of connections, compute units, and storage in each service tier during the service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="15dc0-110">**Conexiones máximas**</span><span class="sxs-lookup"><span data-stu-id="15dc0-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="15dc0-111">50 unidades de proceso básicas</span><span class="sxs-lookup"><span data-stu-id="15dc0-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="15dc0-112">50 conexiones</span><span class="sxs-lookup"><span data-stu-id="15dc0-112">50 connections</span></span>    |
| <span data-ttu-id="15dc0-113">100 unidades de proceso básicas</span><span class="sxs-lookup"><span data-stu-id="15dc0-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="15dc0-114">100 conexiones</span><span class="sxs-lookup"><span data-stu-id="15dc0-114">100 connections</span></span>   |
| <span data-ttu-id="15dc0-115">100 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="15dc0-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="15dc0-116">200 conexiones</span><span class="sxs-lookup"><span data-stu-id="15dc0-116">200 connections</span></span>   |
| <span data-ttu-id="15dc0-117">200 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="15dc0-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="15dc0-118">300 conexiones</span><span class="sxs-lookup"><span data-stu-id="15dc0-118">300 connections</span></span>   |
| <span data-ttu-id="15dc0-119">400 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="15dc0-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="15dc0-120">400 conexiones</span><span class="sxs-lookup"><span data-stu-id="15dc0-120">400 connections</span></span>   |
| <span data-ttu-id="15dc0-121">800 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="15dc0-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="15dc0-122">500 conexiones</span><span class="sxs-lookup"><span data-stu-id="15dc0-122">500 connections</span></span>   |
| <span data-ttu-id="15dc0-123">**Unidades de proceso máximas**</span><span class="sxs-lookup"><span data-stu-id="15dc0-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="15dc0-124">Nivel de servicio Básico</span><span class="sxs-lookup"><span data-stu-id="15dc0-124">Basic service tier</span></span>         | <span data-ttu-id="15dc0-125">100 unidades de proceso</span><span class="sxs-lookup"><span data-stu-id="15dc0-125">100 Compute Units</span></span> |
| <span data-ttu-id="15dc0-126">Nivel de servicio Estándar</span><span class="sxs-lookup"><span data-stu-id="15dc0-126">Standard service tier</span></span>      | <span data-ttu-id="15dc0-127">800 unidades de proceso</span><span class="sxs-lookup"><span data-stu-id="15dc0-127">800 Compute Units</span></span> |
| <span data-ttu-id="15dc0-128">**Almacenamiento máximo**</span><span class="sxs-lookup"><span data-stu-id="15dc0-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="15dc0-129">Nivel de servicio Básico</span><span class="sxs-lookup"><span data-stu-id="15dc0-129">Basic service tier</span></span>         | <span data-ttu-id="15dc0-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="15dc0-130">1 TB</span></span>              |
| <span data-ttu-id="15dc0-131">Nivel de servicio Estándar</span><span class="sxs-lookup"><span data-stu-id="15dc0-131">Standard service tier</span></span>      | <span data-ttu-id="15dc0-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="15dc0-132">1 TB</span></span>              |

<span data-ttu-id="15dc0-133">Cuando se alcanzan demasiadas conexiones, puede recibir el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="15dc0-133">When too many connections are reached, you may receive the following error:</span></span>
> <span data-ttu-id="15dc0-134">FATAL:  sorry, too many clients already</span><span class="sxs-lookup"><span data-stu-id="15dc0-134">FATAL:  sorry, too many clients already</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="15dc0-135">Limitaciones funcionales de la versión preliminar</span><span class="sxs-lookup"><span data-stu-id="15dc0-135">Preview functional limitations</span></span>
### <a name="scale-operations"></a><span data-ttu-id="15dc0-136">Operaciones de escalado</span><span class="sxs-lookup"><span data-stu-id="15dc0-136">Scale operations</span></span>
1.  <span data-ttu-id="15dc0-137">El escalado dinámico de servidores entre niveles de servicio no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="15dc0-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="15dc0-138">Es decir, el cambio entre los niveles de servicio Básico y Estándar.</span><span class="sxs-lookup"><span data-stu-id="15dc0-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="15dc0-139">El aumento dinámico bajo demanda del almacenamiento en un servidor creado previamente no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="15dc0-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="15dc0-140">La reducción del tamaño de almacenamiento del servidor no se admite.</span><span class="sxs-lookup"><span data-stu-id="15dc0-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="15dc0-141">Actualizaciones de la versión de servidor</span><span class="sxs-lookup"><span data-stu-id="15dc0-141">Server version upgrades</span></span>
- <span data-ttu-id="15dc0-142">La migración automatizada entre las principales versiones del motor de base de datos no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="15dc0-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="15dc0-143">Administración de suscripciones</span><span class="sxs-lookup"><span data-stu-id="15dc0-143">Subscription management</span></span>
- <span data-ttu-id="15dc0-144">El movimiento dinámico de servidores creados previamente entre grupo de suscripciones y recursos no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="15dc0-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="15dc0-145">Restauración a un momento dado</span><span class="sxs-lookup"><span data-stu-id="15dc0-145">Point-in-time-restore</span></span>
1.  <span data-ttu-id="15dc0-146">La restauración a un nivel de servicio o unidades de proceso y tamaño de almacenamiento diferente no se admite.</span><span class="sxs-lookup"><span data-stu-id="15dc0-146">Restoring to different service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="15dc0-147">La restauración a un servidor que se ha quitado no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="15dc0-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15dc0-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="15dc0-148">Next steps</span></span>
- <span data-ttu-id="15dc0-149">Comprenda lo que [hay disponible en cada plan de tarifa](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="15dc0-149">Understand [What’s available in each pricing tier](concepts-service-tiers.md)</span></span>
- <span data-ttu-id="15dc0-150">Conozca las [versiones de base de datos de PostgreSQL admitidas](concepts-supported-versions.md).</span><span class="sxs-lookup"><span data-stu-id="15dc0-150">Understand [Supported PostgreSQL Database Versions](concepts-supported-versions.md)</span></span>
- <span data-ttu-id="15dc0-151">Revise [cómo hacer una copia de seguridad de un servidor y restaurarlo en Azure Database for PostgreSQL mediante Azure Portal](howto-restore-server-portal.md)</span><span class="sxs-lookup"><span data-stu-id="15dc0-151">Review [How To Back up and Restore a server in Azure Database for PostgreSQL using the Azure portal](howto-restore-server-portal.md)</span></span>
