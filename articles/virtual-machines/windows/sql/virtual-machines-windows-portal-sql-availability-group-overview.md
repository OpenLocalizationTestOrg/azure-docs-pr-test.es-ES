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
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a>Introducción a grupos de disponibilidad de SQL Server AlwaysOn en Azure Virtual Machines #

En este artículo se describen los grupos de disponibilidad de SQL Server en Azure Virtual Machines. 

Grupos de disponibilidad AlwaysOn en máquinas virtuales de Azure son tooAlways similar en grupos de disponibilidad local. Para obtener más información, consulte [Grupos de disponibilidad AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx). 

diagrama de Hello muestra partes de Hola de un grupo de disponibilidad de servidor completa de SQL en máquinas virtuales de Azure.

![Grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

Hello diferencia clave para un grupo de disponibilidad en máquinas virtuales de Azure es que Hola máquinas virtuales de Azure, requieren una [equilibrador de carga](../../../load-balancer/load-balancer-overview.md). equilibrador de carga de Hello contiene direcciones IP de hello para el agente de escucha del grupo de disponibilidad de Hola. Si tiene más de un grupo de disponibilidad, se necesita un agente de escucha por grupo. Un equilibrador de carga puede admitir varios agentes de escucha.

Cuando esté listo toobuild un aroup de disponibilidad de SQL Server en máquinas virtuales de Azure, consulte los tutoriales de toothese.

## <a name="automatically-create-an-availability-group-from-a-template"></a>Creación automática de grupos de disponibilidad desde una plantilla

[Configure Always On availability group in Azure VM automatically - Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) (Configuración automática de grupos de disponibilidad Always On de máquinas virtuales de Azure - Resource Manager)

## <a name="manually-create-an-availability-group-in-azure-portal"></a>Creación manual de grupos de disponibilidad en Azure Portal

También puede crear los hello las máquinas virtuales sin plantilla Hola. En primer lugar, complete los requisitos previos de hello, a continuación, crear grupo de disponibilidad de Hola. Vea Hola temas siguientes: 

- [Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md) (Configuración de requisitos previos para grupos de disponibilidad de SQL Server AlwaysOn en Azure Virtual Machines)///

- [Crear grupo de disponibilidad AlwaysOn tooimprove disponibilidad y recuperación ante desastres](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a>Pasos siguientes

[Configuración de un grupo de disponibilidad de SQL Server AlwaysOn en Azure Virtual Machines en regiones distintas](virtual-machines-windows-portal-sql-availability-group-dr.md)
