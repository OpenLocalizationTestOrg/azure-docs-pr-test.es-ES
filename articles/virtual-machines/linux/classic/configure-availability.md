---
title: "Conjuntos de disponibilidad para máquinas virtuales Linux (modelo clásico)| Microsoft Docs"
description: "Configure un conjunto de disponibilidad para una máquina virtual Linux nueva o existente en el modelo de implementación clásica con el Portal de Azure y Azure PowerShell."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b8624315-beca-4ec7-8441-2e98b166b548
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: cynthn
ms.openlocfilehash: 41d427862150d17e1ad726afc51114d6f62f5a8e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-an-availability-set-for-linux-virtual-machines-in-the-classic-deployment-model"></a><span data-ttu-id="3dacd-103">Configuración de un conjunto de disponibilidad para máquinas virtuales Linux en el modelo de implementación clásica</span><span class="sxs-lookup"><span data-stu-id="3dacd-103">How to configure an availability set for Linux virtual machines in the classic deployment model</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="3dacd-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3dacd-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3dacd-105">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="3dacd-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="3dacd-106">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="3dacd-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="3dacd-107">También puede [configurar conjuntos de disponibilidad](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) en las implementaciones de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3dacd-107">You can also [configure availability sets](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) in Resource Manager deployments.</span></span>

[!INCLUDE [virtual-machines-common-classic-configure-availability](../../../../includes/virtual-machines-common-classic-configure-availability.md)]