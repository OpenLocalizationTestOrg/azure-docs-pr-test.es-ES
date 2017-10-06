---
title: vista de grupo de aaaIntroduction toosecurity en Monitor de red de Azure | Documentos de Microsoft
description: "Esta página proporciona una visión general de hello capacidad de vista de seguridad de Monitor de red"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="4631c-103">Vista de grupo de seguridad de introducción toonetwork en Monitor de red de Azure</span><span class="sxs-lookup"><span data-stu-id="4631c-103">Introduction toonetwork security group view in Azure Network Watcher</span></span>

<span data-ttu-id="4631c-104">Los grupos de seguridad de red pueden asociarse a un nivel de subred o a un nivel de NIC.</span><span class="sxs-lookup"><span data-stu-id="4631c-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="4631c-105">Cuando se asocia a un nivel de subred, se aplican a instancias de máquina virtual de tooall hello en la subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="4631c-105">When associated at a subnet level, it applies tooall hello VM instances in hello subnet.</span></span> <span data-ttu-id="4631c-106">Vista de grupo de seguridad de red devuelve todas las reglas que están asociadas en un nivel de formación y la subred para una máquina virtual que proporciona una visión general de configuración de Hola y Hola configurado NSG.</span><span class="sxs-lookup"><span data-stu-id="4631c-106">Network Security Group view returns all hello configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into hello configuration.</span></span> <span data-ttu-id="4631c-107">Además, las reglas de seguridad eficaz Hola se devuelven para cada una de las NICs hello en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4631c-107">In addition, hello effective security rules are returned for each of hello NICs in a VM.</span></span> <span data-ttu-id="4631c-108">Con la vista de grupos de seguridad de red, se puede evaluar una máquina virtual en busca de vulnerabilidades de red, como puertos abiertos.</span><span class="sxs-lookup"><span data-stu-id="4631c-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="4631c-109">También puede validar si el grupo de seguridad de red está funcionando según lo previsto en función de un [configurado de comparación entre Hola y Hola reglas de seguridad eficaz](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4631c-109">You can also validate if your Network Security Group is working as expected based on a [comparison between hello configured and hello effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="4631c-110">Un caso de uso más extendido se encuentra en el cumplimiento de seguridad y auditoría.</span><span class="sxs-lookup"><span data-stu-id="4631c-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="4631c-111">Puede definir un conjunto prescriptivo de reglas de seguridad como modelo para la regulación de la seguridad de su organización.</span><span class="sxs-lookup"><span data-stu-id="4631c-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="4631c-112">Una auditoría periódica del cumplimiento puede implementarse en un mecanismo de programación mediante la comparación de reglas preceptivas de hello con reglas de hello efectivo para cada una de las máquinas virtuales de hello en la red.</span><span class="sxs-lookup"><span data-stu-id="4631c-112">A periodic compliance audit can be implemented in a programmatic way by comparing hello prescriptive rules with hello effective rules for each of hello VMs in your network.</span></span>

<span data-ttu-id="4631c-113">Hola reglas portales se dividen por efectivo, subred, interfaz de red y de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4631c-113">In hello portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="4631c-114">Esto proporciona una vista sencilla en máquina virtual de hello las reglas aplicadas tooa.</span><span class="sxs-lookup"><span data-stu-id="4631c-114">This provides a simple view into hello rules applied tooa virtual machine.</span></span> <span data-ttu-id="4631c-115">Un botón de descarga es siempre tooeasily descargar todas las reglas de seguridad de hello con independencia de la pestaña de hello en un archivo CSV.</span><span class="sxs-lookup"><span data-stu-id="4631c-115">A download button is provided tooeasily download all hello security rules no matter hello tab into a CSV file.</span></span>

![vista de grupos de seguridad][1]

<span data-ttu-id="4631c-117">Se pueden seleccionar reglas y se abre una nueva hoja prefijos de grupo de seguridad de red de origen y de destino de hello tooshow.</span><span class="sxs-lookup"><span data-stu-id="4631c-117">Rules can be selected and a new blade opens up tooshow hello Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="4631c-118">En esta hoja puede navegar directamente toohello recurso de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="4631c-118">From this blade you can navigate directly toohello Network Security Group resource.</span></span>

![obtención de detalles][2]

### <a name="next-steps"></a><span data-ttu-id="4631c-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4631c-120">Next steps</span></span>

<span data-ttu-id="4631c-121">Obtenga información acerca de cómo tooaudit la seguridad de red de grupo Configuración visitando [configuración del grupo de seguridad de red de auditoría con PowerShell](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="4631c-121">Learn how tooaudit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









