---
title: "aaaUsing SAP en máquinas virtuales de Linux | Documentos de Microsoft"
description: "Aprenda a usar SAP en máquinas virtuales de Linux (VM)en Microsoft Azure"
services: virtual-machines-linux,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: f9cd93dc-71ad-48a4-8778-4e48aec484a6
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: fd4aad83d99ef5286488aaab6552fd67a5e35a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="4bc80-103">Uso de SAP en máquinas virtuales Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="4bc80-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="4bc80-104">Informática en la nube es un término ampliamente utilizado que está adquiriendo cada vez más importancia en hello sector de TI, desde las pequeñas empresas de las organizaciones toolarge y multinacional.</span><span class="sxs-lookup"><span data-stu-id="4bc80-104">Cloud Computing is a widely used term which is gaining more and more importance within hello IT industry, from small companies up toolarge and multinational corporations.</span></span> <span data-ttu-id="4bc80-105">Microsoft Azure es la plataforma de servicios de nube de Microsoft que ofrece una amplia gama de nuevas posibilidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="4bc80-105">Microsoft Azure is hello Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="4bc80-106">Ahora los clientes están toorapidly puede aprovisionar y eliminación aprovisionar aplicaciones como servicios en la nube, por lo que no son tootechnical limitado o restricciones presupuestarias.</span><span class="sxs-lookup"><span data-stu-id="4bc80-106">Now customers are able toorapidly provision and de-provision applications as Cloud-Services, so they are not limited tootechnical or budgeting restrictions.</span></span> <span data-ttu-id="4bc80-107">En lugar de invertir tiempo y presupuesto en infraestructura de hardware, las empresas pueden centrarse en la aplicación hello, procesos empresariales y sus ventajas para los clientes y los usuarios.</span><span class="sxs-lookup"><span data-stu-id="4bc80-107">Instead of investing time and budget into hardware infrastructure, companies can focus on hello application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="4bc80-108">Con las máquinas virtuales de Microsoft Azure, Microsoft ofrece una completa plataforma de infraestructura como servicio (IaaS).</span><span class="sxs-lookup"><span data-stu-id="4bc80-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="4bc80-109">Las aplicaciones de basadas en SAP NetWeaver son compatibles en las máquinas virtuales de Azure (IaaS).</span><span class="sxs-lookup"><span data-stu-id="4bc80-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="4bc80-110">notas del producto Hola siguientes describen cómo tooplan e implementar SAP NetWeaver aplicaciones basadas en máquinas virtuales de Windows en Azure.</span><span class="sxs-lookup"><span data-stu-id="4bc80-110">hello whitepapers below describe how tooplan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="4bc80-111">También puede implementar aplicaciones basadas en SAP NetWeaver en [máquinas virtuales Windows](../../virtual-machines-windows-classic-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4bc80-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../virtual-machines-windows-classic-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="4bc80-112">SAP NetWeaver en máquinas virtuales Linux de SUSE de Azure</span><span class="sxs-lookup"><span data-stu-id="4bc80-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="4bc80-113">título: aaaTesting SAP NetWeaver en máquinas virtuales de Microsoft Azure SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="4bc80-113">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="4bc80-114">Resumen: no hay ninguna compatibilidad oficial con SAP para la ejecución de SAP NetWeaver en máquinas virtuales con Linux de Azure en este momento.</span><span class="sxs-lookup"><span data-stu-id="4bc80-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="4bc80-115">No obstante, los clientes pueden toodo algunas pruebas o podrían considerar toorun, sistemas de demostración o aprendizaje de SAP en máquinas virtuales de Linux de Azure, siempre que no es necesario para ponerse en contacto con soporte técnico SAP.</span><span class="sxs-lookup"><span data-stu-id="4bc80-115">Nevertheless customers might want toodo some testing or might consider toorun SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="4bc80-116">Este artículo debe ayuda para configurar las máquinas virtuales de Azure SUSE Linux para ejecutar SAP y proporciona algunas sugerencias básicas en orden tooavoid dificultades comunes de las posibles.</span><span class="sxs-lookup"><span data-stu-id="4bc80-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order tooavoid common potential pitfalls.</span></span>

<span data-ttu-id="4bc80-117">Actualización: diciembre de 2015</span><span class="sxs-lookup"><span data-stu-id="4bc80-117">Updated: December 2015</span></span>

<span data-ttu-id="4bc80-118">[Este artículo se puede encontrar aquí](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4bc80-118">[This article can be found here](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

