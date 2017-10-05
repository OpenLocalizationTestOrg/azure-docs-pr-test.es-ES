---
title: "Administrar máquinas virtuales con Azure Automation | Microsoft Docs"
description: "Obtenga información acerca de cómo puede usarse el servicio Automatización de Azure para administrar Máquinas virtuales de Azure a escala."
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
ms.openlocfilehash: 15653c5d653ae538bdb66eaf0daee12c35858b45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="d3c53-103">Administración de Máquinas virtuales de Azure mediante Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="d3c53-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="d3c53-104">Esta guía le ofrece el servicio Automatización de Azure y cómo se puede usar para simplificar la administración de máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3c53-104">This guide introduces you to the Azure Automation service and how it can be used to simplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="d3c53-105">¿Qué es Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="d3c53-105">What is Azure Automation?</span></span>
<span data-ttu-id="d3c53-106">[Automatización de Azure](https://azure.microsoft.com/services/automation/) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos.</span><span class="sxs-lookup"><span data-stu-id="d3c53-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="d3c53-107">Mediante Automatización de Azure, se pueden automatizar las tareas de ejecución prolongada, manuales, propensas a errores y que se repiten con frecuencia para aumentar la confiabilidad, la eficiencia y el valioso tiempo para su organización.</span><span class="sxs-lookup"><span data-stu-id="d3c53-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="d3c53-108">Automatización de Azure proporciona un motor de ejecución de flujo de trabajo altamente confiable y de alta disponibilidad que realiza la escalación para satisfacer sus necesidades a medida que crece la organización.</span><span class="sxs-lookup"><span data-stu-id="d3c53-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="d3c53-109">En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d3c53-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="d3c53-110">Puede reducir la sobrecarga operativa y liberar al personal de TI/DevOps para concentrarse en el trabajo que proporciona valor al negocio ejecutando las tareas de administración en la nube automáticamente mediante Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3c53-110">You can lower operational overhead and free up IT and DevOps staff to focus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="d3c53-111">¿Cómo puede ayudar el servicio Automatización de Azure a administrar máquinas virtuales de Azure?</span><span class="sxs-lookup"><span data-stu-id="d3c53-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="d3c53-112">Las máquinas virtuales se pueden administrar en automatización de Azure usando [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3c53-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="d3c53-113">Automatización de Azure incluye los cmdlets de Azure PowerShell, por lo que es posible realizar todas las tareas de administración de máquina virtual dentro del servicio.</span><span class="sxs-lookup"><span data-stu-id="d3c53-113">Azure Automation includes the Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within the service.</span></span> <span data-ttu-id="d3c53-114">También puede emparejar los cmdlets en Automatización de Azure con los cmdlets para otros servicios de Azure, para automatizar tareas complejas a través de los servicios de Azure y sistemas de terceros.</span><span class="sxs-lookup"><span data-stu-id="d3c53-114">You can also pair the cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3c53-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d3c53-115">Next steps</span></span>
<span data-ttu-id="d3c53-116">Ahora que ha aprendido los aspectos básicos de Automatización de Azure y cómo se puede usar para administrar máquinas virtuales de Azure, obtenga más información.</span><span class="sxs-lookup"><span data-stu-id="d3c53-116">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="d3c53-117">Información general sobre Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="d3c53-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="d3c53-118">Mi primer runbook</span><span class="sxs-lookup"><span data-stu-id="d3c53-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="d3c53-119">Mapa de aprendizaje de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="d3c53-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

