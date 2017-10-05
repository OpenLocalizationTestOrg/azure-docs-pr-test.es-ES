---
title: "Solución de problemas comunes durante la creación del VHD | Microsoft Docs"
description: "Responde a preguntas sobre solución de problemas comunes y errores durante la creación del VHD."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c4e88a9fbb15dd90d619b159ae1065dfacc1907f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-common-issues-encountered-during-vhd-creation"></a><span data-ttu-id="e2fdc-103">Solución de problemas comunes detectados durante la creación del VHD</span><span class="sxs-lookup"><span data-stu-id="e2fdc-103">How to troubleshoot common issues encountered during VHD creation</span></span>
<span data-ttu-id="e2fdc-104">En este artículo se proporciona ayuda a un publicador o coadministrador de Azure Marketplace que puede experimentar un problema o que tiene preguntas comunes mientras publica o administra sus soluciones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e2fdc-104">This article is provided to help an Azure Marketplace publisher and/or co-administrator that may experience an issue or have common questions while publishing or managing their virtual machine solution(s).</span></span>

1. <span data-ttu-id="e2fdc-105">¿Cómo se cambia el nombre del host?</span><span class="sxs-lookup"><span data-stu-id="e2fdc-105">How do I change the name of the host?</span></span>
   
    <span data-ttu-id="e2fdc-106">Una vez creada la máquina virtual, los usuarios no pueden actualizar el nombre del host.</span><span class="sxs-lookup"><span data-stu-id="e2fdc-106">Once VM is created, users can’t update the name of the host.</span></span>
2. <span data-ttu-id="e2fdc-107">¿Cómo se restablece el servicio Escritorio remoto o su contraseña de inicio de sesión?</span><span class="sxs-lookup"><span data-stu-id="e2fdc-107">How to reset the Remote Desktop service or its login password?</span></span>
   
   * [<span data-ttu-id="e2fdc-108">Referencia para máquinas virtuales con Windows</span><span class="sxs-lookup"><span data-stu-id="e2fdc-108">Reference for Windows VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [<span data-ttu-id="e2fdc-109">Referencia para máquinas virtuales con Linux</span><span class="sxs-lookup"><span data-stu-id="e2fdc-109">Reference for Linux VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. <span data-ttu-id="e2fdc-110">¿Cómo generar certificados SSH nuevos?</span><span class="sxs-lookup"><span data-stu-id="e2fdc-110">How to generate new ssh certificates?</span></span>
   
   <span data-ttu-id="e2fdc-111">Consulte el siguiente vínculo: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span><span class="sxs-lookup"><span data-stu-id="e2fdc-111">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span></span>
4. <span data-ttu-id="e2fdc-112">¿Cómo configurar un certificado VPN abierto?</span><span class="sxs-lookup"><span data-stu-id="e2fdc-112">How to configure an open VPN certificate?</span></span>
   
   <span data-ttu-id="e2fdc-113">Vea la información facilitada en el siguiente vínculo: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span><span class="sxs-lookup"><span data-stu-id="e2fdc-113">Please refer to the link: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span></span>
5. <span data-ttu-id="e2fdc-114">¿Cuál es la directiva de soporte técnico para ejecutar software de servidor de Microsoft en el entorno de máquina virtual de Microsoft Azure (infraestructura como servicio)?</span><span class="sxs-lookup"><span data-stu-id="e2fdc-114">What is the support policy for running Microsoft server software in the Microsoft Azure virtual machine environment (infrastructure-as-a-service)?</span></span>
   
   <span data-ttu-id="e2fdc-115">Acceda al artículo del siguiente vínculo: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="e2fdc-115">Please refer to the link: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
6. <span data-ttu-id="e2fdc-116">¿Las máquinas virtuales tienen un identificador único?</span><span class="sxs-lookup"><span data-stu-id="e2fdc-116">Do Virtual Machines have any unique identifier?</span></span>
   
   <span data-ttu-id="e2fdc-117">Azure codifica un identificador exclusivo de máquina virtual de Azure en cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e2fdc-117">Azure encodes Azure VM Unique ID in every VM.</span></span> <span data-ttu-id="e2fdc-118">Vea los detalles en este blog y en la documentación.</span><span class="sxs-lookup"><span data-stu-id="e2fdc-118">See details in this blog and documentation.</span></span>
7. <span data-ttu-id="e2fdc-119">¿Cómo se puede administrar la extensión de script personalizada en la tarea de inicio en una máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="e2fdc-119">In a VM how can I manage the custom script extension in the startup task?</span></span>
   
   <span data-ttu-id="e2fdc-120">Consulte este vínculo: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span><span class="sxs-lookup"><span data-stu-id="e2fdc-120">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span></span>
8. <span data-ttu-id="e2fdc-121">¿Cómo se crea una máquina virtual desde Azure Portal usando el VHD que se carga en Premium Storage?</span><span class="sxs-lookup"><span data-stu-id="e2fdc-121">How to create a VM from the Azure portal using the VHD that is uploaded to premium storage?</span></span>
   
   <span data-ttu-id="e2fdc-122">Aún no se admite esta característica.</span><span class="sxs-lookup"><span data-stu-id="e2fdc-122">We do not support this feature yet.</span></span>
9. <span data-ttu-id="e2fdc-123">¿Se admite una aplicación de 32 bits en Azure Marketplace?</span><span class="sxs-lookup"><span data-stu-id="e2fdc-123">Is a 32-bit app supported in the Azure Marketplace?</span></span>
   
   <span data-ttu-id="e2fdc-124">Consulte el vínculo para obtener información detallada sobre la directiva de soporte técnico: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="e2fdc-124">Please refer to the link for details on the support policy: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
10. <span data-ttu-id="e2fdc-125">Cada vez que trato de crear una imagen desde el VHD, se produce el error ". VHD ya está registrado con el repositorio de imágenes como un recurso" en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2fdc-125">Every time I am trying to create an image from my VHDs, I get the error “.VHD is already registered with image repository as the resource” in PowerShell.</span></span> <span data-ttu-id="e2fdc-126">No he creado ninguna imagen antes ni he encontrado ninguna imagen con este nombre en Azure.</span><span class="sxs-lookup"><span data-stu-id="e2fdc-126">I did not create any image before nor did I find any image with this name in Azure.</span></span> <span data-ttu-id="e2fdc-127">¿Cómo se resuelve este problema?</span><span class="sxs-lookup"><span data-stu-id="e2fdc-127">How do I resolve this?</span></span>
    
    <span data-ttu-id="e2fdc-128">Esto suele suceder si el usuario ha aprovisionado una máquina virtual desde este VHD y existe un bloqueo en ese VHD.</span><span class="sxs-lookup"><span data-stu-id="e2fdc-128">This usually happen if the user provisioned a VM from this VHD and there is a lock on that VHD.</span></span> <span data-ttu-id="e2fdc-129">Compruebe que no haya ninguna máquina virtual asignada desde este VHD.</span><span class="sxs-lookup"><span data-stu-id="e2fdc-129">Please check that there is no VM allocated from this VHD.</span></span> <span data-ttu-id="e2fdc-130">Si el error persiste, cree una incidencia de soporte técnico mediante este vínculo o desde el Portal de publicación sobre este asunto (los detalles se proporcionan en la respuesta a la pregunta 11).</span><span class="sxs-lookup"><span data-stu-id="e2fdc-130">If the error still persist , then please raise a support ticket using this link or from the Publishing portal regarding this (details are given in the answer of question 11).</span></span>