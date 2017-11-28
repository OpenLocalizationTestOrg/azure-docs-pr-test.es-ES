---
title: Limitaciones en Azure Database for MySQL | Microsoft Docs
description: "Describe las limitaciones de la versión preliminar en Azure Database for MySQL."
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c61d70897b66c2ffee819ac98c38ab75000db907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a><span data-ttu-id="00502-103">Limitaciones en Azure Database for MySQL (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="00502-103">Limitations in Azure Database for MySQL (Preview)</span></span>
<span data-ttu-id="00502-104">El servicio Azure Database for MySQL se encuentra en versión preliminar pública.</span><span class="sxs-lookup"><span data-stu-id="00502-104">The Azure Database for MySQL service is in public preview.</span></span> <span data-ttu-id="00502-105">En las secciones siguientes se describen los límites de capacidad y funcionales en el servicio de base de datos.</span><span class="sxs-lookup"><span data-stu-id="00502-105">The following sections describe capacity and functional limits in the database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="00502-106">Máximos de nivel de servicio</span><span class="sxs-lookup"><span data-stu-id="00502-106">Service Tier Maximums</span></span>
<span data-ttu-id="00502-107">Azure Database for MySQL tiene varios niveles de servicio entre los que puede elegir al crear un servidor.</span><span class="sxs-lookup"><span data-stu-id="00502-107">Azure Database for MySQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="00502-108">Para obtener más información, consulte la [descripción sobre los elementos disponibles en cada nivel de servicio](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="00502-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="00502-109">Hay un número máximo de conexiones, unidades de proceso y almacenamiento en cada nivel de servicio mientras el servicio esté en versión preliminar, y son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="00502-109">There is a maximum number of connections, compute units, and storage in each service tier during the service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="00502-110">**Conexiones máximas**</span><span class="sxs-lookup"><span data-stu-id="00502-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="00502-111">50 unidades de proceso básicas</span><span class="sxs-lookup"><span data-stu-id="00502-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="00502-112">50 conexiones</span><span class="sxs-lookup"><span data-stu-id="00502-112">50 connections</span></span>    |
| <span data-ttu-id="00502-113">100 unidades de proceso básicas</span><span class="sxs-lookup"><span data-stu-id="00502-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="00502-114">100 conexiones</span><span class="sxs-lookup"><span data-stu-id="00502-114">100 connections</span></span>   |
| <span data-ttu-id="00502-115">100 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="00502-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="00502-116">200 conexiones</span><span class="sxs-lookup"><span data-stu-id="00502-116">200 connections</span></span>   |
| <span data-ttu-id="00502-117">200 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="00502-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="00502-118">300 conexiones</span><span class="sxs-lookup"><span data-stu-id="00502-118">300 connections</span></span>   |
| <span data-ttu-id="00502-119">400 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="00502-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="00502-120">400 conexiones</span><span class="sxs-lookup"><span data-stu-id="00502-120">400 connections</span></span>   |
| <span data-ttu-id="00502-121">800 unidades de proceso estándar</span><span class="sxs-lookup"><span data-stu-id="00502-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="00502-122">500 conexiones</span><span class="sxs-lookup"><span data-stu-id="00502-122">500 connections</span></span>   |
| <span data-ttu-id="00502-123">**Unidades de proceso máximas**</span><span class="sxs-lookup"><span data-stu-id="00502-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="00502-124">Nivel de servicio Básico</span><span class="sxs-lookup"><span data-stu-id="00502-124">Basic service tier</span></span>         | <span data-ttu-id="00502-125">100 unidades de proceso</span><span class="sxs-lookup"><span data-stu-id="00502-125">100 Compute Units</span></span> |
| <span data-ttu-id="00502-126">Nivel de servicio Estándar</span><span class="sxs-lookup"><span data-stu-id="00502-126">Standard service tier</span></span>      | <span data-ttu-id="00502-127">800 unidades de proceso</span><span class="sxs-lookup"><span data-stu-id="00502-127">800 Compute Units</span></span> |
| <span data-ttu-id="00502-128">**Almacenamiento máximo**</span><span class="sxs-lookup"><span data-stu-id="00502-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="00502-129">Nivel de servicio Básico</span><span class="sxs-lookup"><span data-stu-id="00502-129">Basic service tier</span></span>         | <span data-ttu-id="00502-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="00502-130">1 TB</span></span>              |
| <span data-ttu-id="00502-131">Nivel de servicio Estándar</span><span class="sxs-lookup"><span data-stu-id="00502-131">Standard service tier</span></span>      | <span data-ttu-id="00502-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="00502-132">1 TB</span></span>              |

<span data-ttu-id="00502-133">Cuando se alcanzan demasiadas conexiones, puede recibir el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="00502-133">When too many connections are reached, you may receive the following error:</span></span>
> <span data-ttu-id="00502-134">ERROR 1040 (08004): Too many connections</span><span class="sxs-lookup"><span data-stu-id="00502-134">ERROR 1040 (08004): Too many connections</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="00502-135">Limitaciones funcionales de versión preliminar:</span><span class="sxs-lookup"><span data-stu-id="00502-135">Preview functional limitations:</span></span>
### <a name="scale-operations"></a><span data-ttu-id="00502-136">Operaciones de escalado:</span><span class="sxs-lookup"><span data-stu-id="00502-136">Scale operations:</span></span>
1.  <span data-ttu-id="00502-137">El escalado dinámico de servidores entre niveles de servicio no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="00502-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="00502-138">Es decir, el cambio entre los niveles de servicio Básico y Estándar.</span><span class="sxs-lookup"><span data-stu-id="00502-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="00502-139">El aumento dinámico bajo demanda del almacenamiento en un servidor creado previamente no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="00502-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="00502-140">La reducción del tamaño de almacenamiento del servidor no se admite.</span><span class="sxs-lookup"><span data-stu-id="00502-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="00502-141">Actualizaciones de la versión de servidor:</span><span class="sxs-lookup"><span data-stu-id="00502-141">Server version upgrades:</span></span>
- <span data-ttu-id="00502-142">La migración automatizada entre las principales versiones del motor de base de datos no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="00502-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="00502-143">Administración de suscripciones:</span><span class="sxs-lookup"><span data-stu-id="00502-143">Subscription management:</span></span>
- <span data-ttu-id="00502-144">El movimiento dinámico de servidores creados previamente entre grupo de suscripciones y recursos no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="00502-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="00502-145">Restauración a un momento dado:</span><span class="sxs-lookup"><span data-stu-id="00502-145">Point-in-time-restore:</span></span>
1.  <span data-ttu-id="00502-146">La restauración a un nivel de servicio o unidades de proceso y tamaño de almacenamiento diferente no se admite.</span><span class="sxs-lookup"><span data-stu-id="00502-146">Restoring to different service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="00502-147">La restauración a un servidor que se ha quitado no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="00502-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00502-148">Pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="00502-148">Next Steps:</span></span>
<span data-ttu-id="00502-149">[What’s available in each service tier](concepts-service-tiers.md)(Elementos disponibles en cada nivel de servicio)
[Supported MySQL Database Versions](concepts-supported-versions.md) (Versiones admitidas de Base de datos MySQL)</span><span class="sxs-lookup"><span data-stu-id="00502-149">[What’s available in each service tier](concepts-service-tiers.md)
[Supported MySQL Database Versions](concepts-supported-versions.md)</span></span>
