---
title: "aaaCreate FQDN para una máquina virtual de Windows en hello portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un nombre de dominio completo o FQDN, para un administrador de recursos según la máquina virtual en hello portal de Azure."
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
ms.openlocfilehash: 67c817ec97073803e513bc41ebde67b75ced565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-windows-vm"></a><span data-ttu-id="562be-103">Crear un nombre de dominio completo de hello portal de Azure para una VM de Windows</span><span class="sxs-lookup"><span data-stu-id="562be-103">Create a fully qualified domain name in hello Azure portal for a Windows VM</span></span>

<span data-ttu-id="562be-104">Cuando crea una máquina virtual (VM) en hello [portal de Azure](https://portal.azure.com), automáticamente se crea un recurso IP público para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="562be-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="562be-105">Utilice este Hola acceso de tooremotely de dirección IP virtual.</span><span class="sxs-lookup"><span data-stu-id="562be-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="562be-106">Aunque el portal de hello no crea un [nombre de dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), o FQDN, puede crear uno una vez hello máquina virtual creada.</span><span class="sxs-lookup"><span data-stu-id="562be-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can create one once hello VM is created.</span></span> <span data-ttu-id="562be-107">En este artículo se muestra hello pasos toocreate un nombre DNS o el FQDN.</span><span class="sxs-lookup"><span data-stu-id="562be-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="562be-108">Creación de un FQDN</span><span class="sxs-lookup"><span data-stu-id="562be-108">Create a FQDN</span></span>
<span data-ttu-id="562be-109">En este artículo se supone que ya ha creado una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="562be-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="562be-110">Si es necesario, puede [crear una máquina virtual en el portal de hello](quick-create-portal.md) o [con Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="562be-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with Azure PowerShell](quick-create-powershell.md).</span></span> <span data-ttu-id="562be-111">Una vez que la máquina virtual está en funcionamiento, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="562be-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="562be-112">Ahora puede conectarse remotamente toohello máquina virtual con este nombre DNS como para el protocolo de escritorio remoto (RDP).</span><span class="sxs-lookup"><span data-stu-id="562be-112">You can now connect remotely toohello VM using this DNS name such as for Remote Desktop Protocol (RDP).</span></span>

## <a name="next-steps"></a><span data-ttu-id="562be-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="562be-113">Next steps</span></span>
<span data-ttu-id="562be-114">Ahora que la máquina virtual tiene un nombre DNS y una IP pública, puede implementar marcos o servicios de aplicaciones comunes, como IIS, SQL o SharePoint.</span><span class="sxs-lookup"><span data-stu-id="562be-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span></span>

<span data-ttu-id="562be-115">En [Información general sobre Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) encontrará sugerencias sobre la creación de implementaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="562be-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

