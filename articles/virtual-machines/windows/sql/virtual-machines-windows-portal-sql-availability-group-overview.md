---
title: "información general de grupos de disponibilidad de servidor - máquinas virtuales de Azure - aaaSQL | Documentos de Microsoft"
description: "En este artículo se describen los grupos de disponibilidad de SQL Server en Azure Virtual Machines."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="c4682-103">Introducción a grupos de disponibilidad de SQL Server AlwaysOn en Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="c4682-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="c4682-104">En este artículo se describen los grupos de disponibilidad de SQL Server en Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="c4682-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="c4682-105">Grupos de disponibilidad AlwaysOn en máquinas virtuales de Azure son tooAlways similar en grupos de disponibilidad local.</span><span class="sxs-lookup"><span data-stu-id="c4682-105">Always On availability groups on Azure Virtual Machines are similar tooAlways On availability groups on premises.</span></span> <span data-ttu-id="c4682-106">Para obtener más información, consulte [Grupos de disponibilidad AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4682-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="c4682-107">diagrama de Hello muestra partes de Hola de un grupo de disponibilidad de servidor completa de SQL en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="c4682-107">hello diagram illustrates hello parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![Grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="c4682-109">Hello diferencia clave para un grupo de disponibilidad en máquinas virtuales de Azure es que Hola máquinas virtuales de Azure, requieren una [equilibrador de carga](../../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4682-109">hello key difference for an Availability Group in Azure Virtual Machines is that hello Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="c4682-110">equilibrador de carga de Hello contiene direcciones IP de hello para el agente de escucha del grupo de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4682-110">hello load balancer holds hello IP addresses for hello availability group listener.</span></span> <span data-ttu-id="c4682-111">Si tiene más de un grupo de disponibilidad, se necesita un agente de escucha por grupo.</span><span class="sxs-lookup"><span data-stu-id="c4682-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="c4682-112">Un equilibrador de carga puede admitir varios agentes de escucha.</span><span class="sxs-lookup"><span data-stu-id="c4682-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="c4682-113">Cuando esté listo toobuild un aroup de disponibilidad de SQL Server en máquinas virtuales de Azure, consulte los tutoriales de toothese.</span><span class="sxs-lookup"><span data-stu-id="c4682-113">When you are ready toobuild a SQL Server availability aroup on Azure Virtual Machines, refer toothese tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="c4682-114">Creación automática de grupos de disponibilidad desde una plantilla</span><span class="sxs-lookup"><span data-stu-id="c4682-114">Automatically create an availability group from a template</span></span>

<span data-ttu-id="c4682-115">[Configure Always On availability group in Azure VM automatically - Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) (Configuración automática de grupos de disponibilidad Always On de máquinas virtuales de Azure - Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="c4682-115">[Configure Always On availability group in Azure VM automatically - Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)</span></span>

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="c4682-116">Creación manual de grupos de disponibilidad en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c4682-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="c4682-117">También puede crear los hello las máquinas virtuales sin plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="c4682-117">You can also create hello virtual machines yourself without hello template.</span></span> <span data-ttu-id="c4682-118">En primer lugar, complete los requisitos previos de hello, a continuación, crear grupo de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4682-118">First, complete hello prerequisites, then create hello availability group.</span></span> <span data-ttu-id="c4682-119">Vea Hola temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="c4682-119">See hello following topics:</span></span> 

- <span data-ttu-id="c4682-120">[Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md) (Configuración de requisitos previos para grupos de disponibilidad de SQL Server AlwaysOn en Azure Virtual Machines)///</span><span class="sxs-lookup"><span data-stu-id="c4682-120">[Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md)</span></span>

- [<span data-ttu-id="c4682-121">Crear grupo de disponibilidad AlwaysOn tooimprove disponibilidad y recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="c4682-121">Create Always On Availability Group tooimprove availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="c4682-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c4682-122">Next steps</span></span>

<span data-ttu-id="c4682-123">[Configuración de un grupo de disponibilidad de SQL Server AlwaysOn en Azure Virtual Machines en regiones distintas](virtual-machines-windows-portal-sql-availability-group-dr.md)</span><span class="sxs-lookup"><span data-stu-id="c4682-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
