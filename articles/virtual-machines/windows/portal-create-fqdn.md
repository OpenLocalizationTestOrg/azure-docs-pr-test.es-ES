---
title: "Creación de FQDN para una VM de Windows en Azure Portal | Microsoft Docs"
description: "Aprenda a crear un nombre de dominio completo, o FQDN, para una máquina virtual basada en Resource Manager en Azure Portal."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2d5a555cd873222efcdb29e8eb3aaf128a24414b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-windows-vm"></a><span data-ttu-id="6a00b-103">Creación de un nombre de dominio completo en Azure Portal para una máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="6a00b-103">Create a fully qualified domain name in the Azure portal for a Windows VM</span></span>

<span data-ttu-id="6a00b-104">Cuando crea una máquina virtual (VM) en [Azure Portal](https://portal.azure.com), se crea automáticamente un recurso de IP pública para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6a00b-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com), a public IP resource for the virtual machine is automatically created.</span></span> <span data-ttu-id="6a00b-105">Use esta dirección IP para acceder de forma remota a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6a00b-105">You use this IP address to remotely access the VM.</span></span> <span data-ttu-id="6a00b-106">Aunque el portal no crea [un nombre de dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), o FQDN, puede crear uno cuando se crea la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6a00b-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can create one once the VM is created.</span></span> <span data-ttu-id="6a00b-107">Este artículo muestra los pasos para crear un nombre DNS o FQDN.</span><span class="sxs-lookup"><span data-stu-id="6a00b-107">This article demonstrates the steps to create a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="6a00b-108">Creación de un FQDN</span><span class="sxs-lookup"><span data-stu-id="6a00b-108">Create a FQDN</span></span>
<span data-ttu-id="6a00b-109">En este artículo se supone que ya ha creado una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6a00b-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="6a00b-110">Si es necesario, puede [crear una máquina virtual en el portal](quick-create-portal.md) o [con Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6a00b-110">If needed, you can [create a VM in the portal](quick-create-portal.md) or [with Azure PowerShell](quick-create-powershell.md).</span></span> <span data-ttu-id="6a00b-111">Una vez que la máquina virtual está en funcionamiento, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="6a00b-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="6a00b-112">Ahora puede conectarse de forma remota a la máquina virtual con este nombre DNS, por ejemplo, para el protocolo de escritorio remoto (RDP).</span><span class="sxs-lookup"><span data-stu-id="6a00b-112">You can now connect remotely to the VM using this DNS name such as for Remote Desktop Protocol (RDP).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a00b-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6a00b-113">Next steps</span></span>
<span data-ttu-id="6a00b-114">Ahora que la máquina virtual tiene un nombre DNS y una IP pública, puede implementar marcos o servicios de aplicaciones comunes, como IIS, SQL o SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6a00b-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span></span>

<span data-ttu-id="6a00b-115">En [Información general sobre Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) encontrará sugerencias sobre la creación de implementaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="6a00b-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

