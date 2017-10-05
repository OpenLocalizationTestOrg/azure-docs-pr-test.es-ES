---
title: "Creación de una identidad profesional o educativa en AAD para Windows | Microsoft Docs"
description: "Aprenda a crear una identidad profesional o educativa en Azure Active Directory para su uso con máquinas virtuales Windows."
services: virtual-machines-windows
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d07dca34-618a-48aa-9971-03d9c1210f4a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 7694b959a384aaed213adc31e02debca31b7c131
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-to-use-with-windows-vms"></a><span data-ttu-id="e7a65-103">Creación de una identidad profesional o educativa en Azure Active Directory para usarla con máquinas virtuales Windows</span><span class="sxs-lookup"><span data-stu-id="e7a65-103">Creating a Work or School identity in Azure Active Directory to use with Windows VMs</span></span>
<span data-ttu-id="e7a65-104">Si creó una cuenta de Azure personal o tiene una suscripción a MSDN personal y creó la cuenta de Azure para beneficiarse de los créditos de Azure de MSDN, usó una identidad de *cuenta de Microsoft* para crearla.</span><span class="sxs-lookup"><span data-stu-id="e7a65-104">If you created a personal Azure account or have a personal MSDN subscription and created the Azure account to take advantage of the MSDN Azure credits -- you used a *Microsoft account* identity to create it.</span></span> <span data-ttu-id="e7a65-105">Muchas características excelentes de Azure (las [plantillas de grupo de recursos](../../azure-resource-manager/resource-group-overview.md) son un ejemplo) requieren una cuenta profesional o educativa (una identidad administrada por Azure Active Directory) para que funcione.</span><span class="sxs-lookup"><span data-stu-id="e7a65-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) to work.</span></span> <span data-ttu-id="e7a65-106">Puede seguir las instrucciones que se indican a continuación para crear una cuenta profesional o educativa porque, afortunadamente, una de las ventajas de su cuenta de Azure personal es que se incluye con un dominio de Azure Active Directory predeterminado que se puede usar para crear una nueva cuenta profesional o educativa que puede usar con las características de Azure que lo requieran.</span><span class="sxs-lookup"><span data-stu-id="e7a65-106">You can follow the instructions below to create a new work or school account because fortunately, one of the best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use to create a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="e7a65-107">Sin embargo, los cambios recientes hacen posible administrar la suscripción con cualquier tipo de cuenta de Azure mediante el método de inicio de sesión interactivo `azure login` que se describe [aquí](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="e7a65-107">However, recent changes make it possible to manage your subscription with any type of Azure account using the `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="e7a65-108">Puede usar ese mecanismo o seguir las instrucciones que se indican a continuación.</span><span class="sxs-lookup"><span data-stu-id="e7a65-108">You can either use that mechanism, or you can follow the instructions that follow.</span></span> <span data-ttu-id="e7a65-109">También puede [crear una identidad profesional o educativa en Azure Active Directory para usarla con máquinas virtuales Linux](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7a65-109">You can also [create a work or school identity in Azure Active Directory to use with Linux VMs](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

