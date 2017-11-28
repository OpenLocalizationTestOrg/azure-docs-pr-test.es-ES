---
title: "aaaManage máquinas virtuales con automatización de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo Hola servicio automatización de Azure puede ser toomanage usa máquinas virtuales de Azure a escala."
services: virtual-machines-windows, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: ce49f83a-f409-42ee-af74-a8ea2caa9ae8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2016
ms.author: timlt
ms.openlocfilehash: bfe7b3a51b6e82bd7cd5b0a83df7226476ed4f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="bb638-103">Administración de Máquinas virtuales de Azure mediante Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="bb638-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="bb638-104">Esta guía presenta toohello servicio de automatización de Azure y cómo se puede usar toosimplify administrar máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb638-104">This guide introduces you toohello Azure Automation service and how it can be used toosimplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="bb638-105">¿Qué es Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="bb638-105">What is Azure Automation?</span></span>
<span data-ttu-id="bb638-106">[Automatización de Azure](https://azure.microsoft.com/services/automation/) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos.</span><span class="sxs-lookup"><span data-stu-id="bb638-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="bb638-107">Mediante la automatización de Azure, las tareas de ejecución prolongada, manuales, propensa a errores y repiten con frecuencia pueden ser confiabilidad tooincrease automatizada, eficiencia y valor para su organización.</span><span class="sxs-lookup"><span data-stu-id="bb638-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="bb638-108">Automatización de Azure ofrece un motor de ejecución de flujo de trabajo altamente confiable y alta disponibilidad que escala toomeet sus necesidades a medida que crece la organización.</span><span class="sxs-lookup"><span data-stu-id="bb638-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="bb638-109">En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bb638-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="bb638-110">Puede reducir la sobrecarga operativa y liberar TI y DevOps personal toofocus en el trabajo que agrega valor empresarial ejecutando la nube de las tareas de administración automáticamente con la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb638-110">You can lower operational overhead and free up IT and DevOps staff toofocus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="bb638-111">¿Cómo puede ayudar el servicio Automatización de Azure a administrar máquinas virtuales de Azure?</span><span class="sxs-lookup"><span data-stu-id="bb638-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="bb638-112">Las máquinas virtuales se pueden administrar en automatización de Azure usando [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="bb638-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="bb638-113">Automatización de Azure incluye cmdlets de PowerShell de Azure de hello, por lo que puede realizar todas las tareas de administración de la máquina virtual en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb638-113">Azure Automation includes hello Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within hello service.</span></span> <span data-ttu-id="bb638-114">También se puede emparejar cmdlets de hello en automatización de Azure con los cmdlets de Hola para otros servicios de Azure, tareas complejas tooautomate a través de los servicios de Azure y sistemas de terceros.</span><span class="sxs-lookup"><span data-stu-id="bb638-114">You can also pair hello cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb638-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bb638-115">Next steps</span></span>
<span data-ttu-id="bb638-116">Ahora que conoce los fundamentos de Hola de automatización de Azure y cómo puede resultarle toomanage usa máquinas virtuales de Azure, obtener más información:</span><span class="sxs-lookup"><span data-stu-id="bb638-116">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="bb638-117">Información general sobre Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="bb638-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="bb638-118">Mi primer runbook</span><span class="sxs-lookup"><span data-stu-id="bb638-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="bb638-119">Mapa de aprendizaje de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="bb638-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

