---
title: "Uso de SAP en máquinas virtuales Linux | Microsoft Docs"
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
ms.openlocfilehash: 078865245989578d17b6eb0b59b379aa2056f31c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="58002-103">Uso de SAP en máquinas virtuales Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="58002-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="58002-104">La informática en la nube es un término ampliamente usado que está cobrando cada vez más importancia en la industria de TI, desde pequeñas empresas hasta las grandes corporaciones y multinacionales.</span><span class="sxs-lookup"><span data-stu-id="58002-104">Cloud Computing is a widely used term which is gaining more and more importance within the IT industry, from small companies up to large and multinational corporations.</span></span> <span data-ttu-id="58002-105">Microsoft Azure es la plataforma de servicios en la nube de Microsoft que ofrece una amplia gama de nuevas posibilidades.</span><span class="sxs-lookup"><span data-stu-id="58002-105">Microsoft Azure is the Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="58002-106">Ahora los clientes pueden aprovisionar y desaprovisionar rápidamente aplicaciones como servicios en la nube, por lo que no se verán limitados por restricciones técnicas o presupuestarias.</span><span class="sxs-lookup"><span data-stu-id="58002-106">Now customers are able to rapidly provision and de-provision applications as Cloud-Services, so they are not limited to technical or budgeting restrictions.</span></span> <span data-ttu-id="58002-107">En lugar de invertir tiempo y presupuesto en infraestructura de hardware, las empresas pueden centrarse en la aplicación, en los procesos empresariales y en sus ventajas para clientes y usuarios.</span><span class="sxs-lookup"><span data-stu-id="58002-107">Instead of investing time and budget into hardware infrastructure, companies can focus on the application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="58002-108">Con las máquinas virtuales de Microsoft Azure, Microsoft ofrece una completa plataforma de infraestructura como servicio (IaaS).</span><span class="sxs-lookup"><span data-stu-id="58002-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="58002-109">Las aplicaciones de basadas en SAP NetWeaver son compatibles en las máquinas virtuales de Azure (IaaS).</span><span class="sxs-lookup"><span data-stu-id="58002-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="58002-110">Las notas del producto siguientes describen cómo planear e implementar aplicaciones basadas en SAP NetWeaver en máquinas virtuales Windows en Azure.</span><span class="sxs-lookup"><span data-stu-id="58002-110">The whitepapers below describe how to plan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="58002-111">También puede implementar aplicaciones basadas en SAP NetWeaver en [máquinas virtuales Windows](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58002-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="58002-112">SAP NetWeaver en máquinas virtuales Linux de SUSE de Azure</span><span class="sxs-lookup"><span data-stu-id="58002-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="58002-113">Título: Pruebas de SAP NetWeaver en máquinas virtuales de SUSE Linux de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="58002-113">Title: Testing SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="58002-114">Resumen: no hay ninguna compatibilidad oficial con SAP para la ejecución de SAP NetWeaver en máquinas virtuales con Linux de Azure en este momento.</span><span class="sxs-lookup"><span data-stu-id="58002-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="58002-115">Sin embargo, es posible que los clientes quieran hacer algunas pruebas o que consideren la posibilidad de ejecutar sistemas de aprendizaje o demostración SAP en máquinas virtuales con Linux en Azure siempre que no sea necesario para ponerse en contacto con el soporte de SAP.</span><span class="sxs-lookup"><span data-stu-id="58002-115">Nevertheless customers might want to do some testing or might consider to run SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="58002-116">Este artículo debe ayudar a configurar las máquinas virtuales con Linux de Azure SUSE para la ejecución de SAP y ofrece algunas sugerencias básicas con el fin de evitar posibles problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="58002-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order to avoid common potential pitfalls.</span></span>

<span data-ttu-id="58002-117">Actualización: diciembre de 2015</span><span class="sxs-lookup"><span data-stu-id="58002-117">Updated: December 2015</span></span>

<span data-ttu-id="58002-118">[Este artículo se puede encontrar aquí](../../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58002-118">[This article can be found here](../../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

