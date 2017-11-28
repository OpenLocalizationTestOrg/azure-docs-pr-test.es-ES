---
title: aaaCreate una identidad profesional o educativa en AAD para Windows | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una identidad profesional o educativa en toouse de Azure Active Directory con las máquinas virtuales de Windows."
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
ms.openlocfilehash: dd6e2381fd0aa503483aa786b36232e557729c4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-windows-vms"></a><span data-ttu-id="753b4-103">Crear una identidad de la empresa o centro educativo en Azure Active Directory toouse con máquinas virtuales de Windows</span><span class="sxs-lookup"><span data-stu-id="753b4-103">Creating a Work or School identity in Azure Active Directory toouse with Windows VMs</span></span>
<span data-ttu-id="753b4-104">Si ha creado una cuenta de Azure personal o tiene una suscripción a MSDN personal y crear Hola cuenta de Azure tootake aprovechar créditos de Azure de MSDN de hello, utiliza un *cuenta Microsoft* toocreate de identidad se.</span><span class="sxs-lookup"><span data-stu-id="753b4-104">If you created a personal Azure account or have a personal MSDN subscription and created hello Azure account tootake advantage of hello MSDN Azure credits -- you used a *Microsoft account* identity toocreate it.</span></span> <span data-ttu-id="753b4-105">Muchas de las mejores características de Azure-- [plantillas de grupo de recursos](../../azure-resource-manager/resource-group-overview.md) es un ejemplo: requieren una cuenta profesional o educativa (es decir, una identidad administrada por Azure Active Directory) toowork.</span><span class="sxs-lookup"><span data-stu-id="753b4-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) toowork.</span></span> <span data-ttu-id="753b4-106">Puede seguir instrucciones de hello debajo toocreate que un nuevo trabajo o escuela cuenta porque Afortunadamente, una de las mejores cosas de hello sobre su cuenta personal de Azure es que viene con un dominio de Active Directory de Azure predeterminado que se puede usar toocreate un nuevo trabajo o escuela cuenta que puede usar con características de Azure que lo requieran.</span><span class="sxs-lookup"><span data-stu-id="753b4-106">You can follow hello instructions below toocreate a new work or school account because fortunately, one of hello best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use toocreate a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="753b4-107">Sin embargo, los cambios recientes que sea posible toomanage su suscripción con cualquier tipo de cuenta de Azure con hello `azure login` método de inicio de sesión interactivo descrito [aquí](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="753b4-107">However, recent changes make it possible toomanage your subscription with any type of Azure account using hello `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="753b4-108">Puede usar este mecanismo o bien puede seguir las instrucciones de Hola que siguen.</span><span class="sxs-lookup"><span data-stu-id="753b4-108">You can either use that mechanism, or you can follow hello instructions that follow.</span></span> <span data-ttu-id="753b4-109">También puede [crear una identidad profesional o educativa en Azure Active Directory toouse con máquinas virtuales de Linux](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="753b4-109">You can also [create a work or school identity in Azure Active Directory toouse with Linux VMs](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

