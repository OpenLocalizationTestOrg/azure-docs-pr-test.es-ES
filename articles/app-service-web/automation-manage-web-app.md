---
title: "Administración de Azure Web Apps mediante Azure Automation | Microsoft Docs"
description: "Obtenga información acerca de cómo puede usarse el servicio para administrar Aplicaciones web de Azure."
services: app-service\web, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: c960a44f-f941-401d-afba-a4bc0f0394eb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte
ms.openlocfilehash: a96332346747114620ee6ebd2a2d0c4417d4a213
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="af0a3-103">Administración de aplicaciones web de Azure mediante Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="af0a3-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="af0a3-104">Esta guía le ofrece el servicio Automatización de Azure y cómo se puede usar para simplificar la administración de Aplicaciones web de Azure.</span><span class="sxs-lookup"><span data-stu-id="af0a3-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="af0a3-105">¿Qué es Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="af0a3-105">What is Azure Automation?</span></span>
<span data-ttu-id="af0a3-106">[Automatización de Azure](../automation/automation-intro.md) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos.</span><span class="sxs-lookup"><span data-stu-id="af0a3-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="af0a3-107">Mediante Automatización de Azure, se pueden automatizar las tareas de ejecución prolongada, manuales, propensas a errores y que se repiten para aumentar la confiabilidad, la eficiencia y el valioso tiempo para su organización.</span><span class="sxs-lookup"><span data-stu-id="af0a3-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="af0a3-108">Automatización de Azure proporciona un motor de ejecución de flujo de trabajo altamente confiable y de alta disponibilidad que realiza la escalación para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="af0a3-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="af0a3-109">En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="af0a3-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="af0a3-110">Reduzca la sobrecarga operativa y libere al personal de TI/DevOps para concentrarse en el trabajo que proporciona valor al negocio trasladando las tareas de administración en la nube para que se ejecuten automáticamente mediante Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="af0a3-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="af0a3-111">¿Cómo puede ayudar Automatización de Azure a administrar Aplicaciones web de Azure?</span><span class="sxs-lookup"><span data-stu-id="af0a3-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="af0a3-112">Las aplicaciones web se pueden administrar en Automatización de Azure mediante los cmdlets de PowerShell que están disponibles en los [módulos de Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="af0a3-112">Web App can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="af0a3-113">Puede [instalar estos cmdlets de Aplicaciones web de PowerShell en Automatización de Azure](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/)para que pueda realizar todas las tareas de administración de Aplicaciones web dentro del servicio.</span><span class="sxs-lookup"><span data-stu-id="af0a3-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within the service.</span></span> <span data-ttu-id="af0a3-114">También puede emparejar estos cmdlets en Automatización de Azure con los cmdlets para otros servicios de Azure, para automatizar tareas complejas a través de los servicios de Azure y sistemas de terceros.</span><span class="sxs-lookup"><span data-stu-id="af0a3-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="af0a3-115">Estos son algunos ejemplos de administración de Servicios de aplicaciones con Automatización:</span><span class="sxs-lookup"><span data-stu-id="af0a3-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="af0a3-116">Scripts para administrar Aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="af0a3-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="af0a3-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af0a3-117">Next steps</span></span>
<span data-ttu-id="af0a3-118">Ahora que ha aprendido los aspectos básicos de Automatización de Azure y cómo se puede usar para administrar Aplicaciones web de Azure, siga estos vínculos para obtener más información acerca de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="af0a3-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Web App, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="af0a3-119">Consulte el [Tutorial de introducción](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="af0a3-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

