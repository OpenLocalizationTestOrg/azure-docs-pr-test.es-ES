---
title: "aaaManage RemoteApp de Azure mediante la automatización de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo Hola servicio automatización de Azure puede ser usado toomanage Azure RemoteApp."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 589f01ef-f9c1-4e7b-a040-1b46862d3544
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: magoedte;csand
ms.openlocfilehash: a4cb23e292c797256e971acb3b363b025f140f16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="12744-103">Administración de RemoteApp de Azure mediante Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="12744-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="12744-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="12744-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="12744-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="12744-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="12744-106">Esta guía le presentará los toohello servicio de automatización de Azure y cómo puede resultarle toosimplify usa administración de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="12744-106">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="12744-107">¿Qué es Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="12744-107">What is Azure Automation?</span></span>
<span data-ttu-id="12744-108">[Automatización de Azure](../automation/automation-intro.md) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos.</span><span class="sxs-lookup"><span data-stu-id="12744-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="12744-109">Mediante automatización de Azure, las tareas manuales, que se repiten con frecuencia, ejecución prolongada y propensa a errores pueden ser tooincrease automatizadas confiabilidad y eficacia, toovalue de tiempo para su organización.</span><span class="sxs-lookup"><span data-stu-id="12744-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="12744-110">Automatización de Azure ofrece un motor de ejecución de flujo de trabajo altamente confiable y de alta disponibilidad que escala toomeet sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="12744-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="12744-111">En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="12744-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="12744-112">Reducir la sobrecarga operativa y liberar TI y DevOps toofocus de personal en el trabajo que agrega valor empresarial moviendo el toobe de tareas de administración en la nube se ejecute automáticamente mediante la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="12744-112">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="12744-113">¿Cómo puede ayudar el servicio Automatización de Azure a administrar RemoteApp de Azure?</span><span class="sxs-lookup"><span data-stu-id="12744-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="12744-114">RemoteApp puede administrarse en automatización de Azure mediante los cmdlets de PowerShell de Hola que están disponibles en hello [herramientas de Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="12744-114">RemoteApp can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="12744-115">Automatización de Azure tiene estos cmdlets de RemoteApp PowerShell disponibles fuera del cuadro de hello, por lo que puede realizar todas las tareas de administración de RemoteApp en servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="12744-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of hello box, so that you can perform all of your RemoteApp management tasks within hello service.</span></span> <span data-ttu-id="12744-116">También se puede emparejar estos cmdlets en automatización de Azure con los cmdlets de Hola para otros servicios de Azure, tareas complejas tooautomate a través de los servicios de Azure y sistemas de terceros 3rd.</span><span class="sxs-lookup"><span data-stu-id="12744-116">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12744-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12744-117">Next steps</span></span>
<span data-ttu-id="12744-118">Ahora que ha aprendido conceptos básicos de Hola de automatización de Azure y cómo puede ser usado toomanage RemoteApp de Azure, siga estas toolearn de vínculos más información acerca de la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="12744-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure RemoteApp, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="12744-119">Vea Hola automatización de Azure [Tutorial de introducción](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="12744-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

