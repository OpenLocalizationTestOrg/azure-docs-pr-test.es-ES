---
title: "Administración de Azure RemoteApp mediante Azure Automation | Microsoft Docs"
description: "Obtenga información acerca de cómo puede usarse el servicio Automatización de Azure para administrar RemoteApp de Azure."
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
ms.openlocfilehash: 59ac11f153c0bd74a1106400dbbf5790968b657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="3acb6-103">Administración de RemoteApp de Azure mediante Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="3acb6-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3acb6-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="3acb6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3acb6-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="3acb6-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3acb6-106">Esta guía le ofrece el servicio Automatización de Azure y cómo se puede usar para simplificar la administración de RemoteApp de Azure.</span><span class="sxs-lookup"><span data-stu-id="3acb6-106">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="3acb6-107">¿Qué es Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="3acb6-107">What is Azure Automation?</span></span>
<span data-ttu-id="3acb6-108">[Automatización de Azure](../automation/automation-intro.md) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos.</span><span class="sxs-lookup"><span data-stu-id="3acb6-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="3acb6-109">Mediante Automatización de Azure, se pueden automatizar las tareas de ejecución prolongada, manuales, propensas a errores y que se repiten con frecuencia para aumentar la confiabilidad, la eficiencia y el valioso tiempo para su organización.</span><span class="sxs-lookup"><span data-stu-id="3acb6-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="3acb6-110">Automatización de Azure proporciona un motor de ejecución de flujo de trabajo altamente confiable y de alta disponibilidad que realiza la escalación para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="3acb6-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="3acb6-111">En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3acb6-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="3acb6-112">Reduzca la sobrecarga operativa y libere al personal de TI/DevOps para concentrarse en el trabajo que proporciona valor al negocio trasladando las tareas de administración en la nube para que se ejecuten automáticamente mediante Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="3acb6-112">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="3acb6-113">¿Cómo puede ayudar el servicio Automatización de Azure a administrar RemoteApp de Azure?</span><span class="sxs-lookup"><span data-stu-id="3acb6-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="3acb6-114">RemoteApp se puede administrar en Automatización de Azure mediante los cmdlets de PowerShell que están disponibles en las [Herramientas de Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="3acb6-114">RemoteApp can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="3acb6-115">Automatización de Azure tiene estos cmdlets de PowerShell de RemoteApp disponibles directamente para que pueda realizar todas las tareas de administración de RemoteApp dentro del servicio.</span><span class="sxs-lookup"><span data-stu-id="3acb6-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of the box, so that you can perform all of your RemoteApp management tasks within the service.</span></span> <span data-ttu-id="3acb6-116">También puede emparejar estos cmdlets en Automatización de Azure con los cmdlets para otros servicios de Azure, para automatizar tareas complejas a través de los servicios de Azure y sistemas de terceros.</span><span class="sxs-lookup"><span data-stu-id="3acb6-116">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3acb6-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3acb6-117">Next steps</span></span>
<span data-ttu-id="3acb6-118">Ahora que ha aprendido los aspectos básicos de Automatización de Azure y cómo se puede usar para administrar RemoteApp de Azure, siga estos vínculos para obtener más información acerca de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="3acb6-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure RemoteApp, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="3acb6-119">Consulte el [Tutorial de introducción](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="3acb6-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

