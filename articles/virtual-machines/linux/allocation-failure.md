---
title: "VM de Linux aaaTroubleshooting errores de asignación | Documentos de Microsoft"
description: "Solución de problemas de errores de asignación al crear, reiniciar o cambiar el tamaño de una máquina virtual de Linux en Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resourece-manager,azure-service-management
ms.assetid: 1ef41144-6dd6-4a56-b180-9d8b3d05eae7
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cjiang
ms.openlocfilehash: 502fbb406b0b4acf086c2586795f69a44cc1a004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-linux-vms-in-azure"></a><span data-ttu-id="fa1b0-103">Solución de problemas de errores de asignación al crear, reiniciar o cambiar el tamaño de una máquina virtual de Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="fa1b0-103">Troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure</span></span>
<span data-ttu-id="fa1b0-104">Al crear una máquina virtual, reiniciar máquinas virtuales (desasignadas) detenidas o cambiar el tamaño de una máquina virtual, Microsoft Azure asigna recursos de proceso tooyour suscripción.</span><span class="sxs-lookup"><span data-stu-id="fa1b0-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources tooyour subscription.</span></span> <span data-ttu-id="fa1b0-105">En ocasiones, puede recibir errores al realizar estas operaciones, incluso antes de llegar a los límites de suscripción de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="fa1b0-105">You may occasionally receive errors when performing these operations -- even before you reach hello Azure subscription limits.</span></span> <span data-ttu-id="fa1b0-106">Este artículo explica causas Hola de algunos de los errores de asignación comunes de Hola y sugiere posibles correcciones.</span><span class="sxs-lookup"><span data-stu-id="fa1b0-106">This article explains hello causes of some of hello common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="fa1b0-107">información de Hello también puede resultarle útil cuando planee la implementación de Hola de sus servicios.</span><span class="sxs-lookup"><span data-stu-id="fa1b0-107">hello information may also be useful when you plan hello deployment of your services.</span></span> <span data-ttu-id="fa1b0-108">También puede [solucionar los errores de asignación al crear, reiniciar o cambiar de tamaño máquinas virtuales Windows en Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fa1b0-108">You can also [troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

