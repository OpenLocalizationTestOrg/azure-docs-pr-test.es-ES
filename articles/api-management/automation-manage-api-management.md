---
title: "Administración de Administración de API de Azure mediante Automatización de Azure"
description: "Obtenga información acerca de cómo puede usarse el servicio de Automatización de Azure para administrar Administración de API de Azure."
services: api-management, automation
documentationcenter: 
author: csand-msft
manager: eamono
editor: 
ms.assetid: 2e53c9af-f738-47f8-b1b6-593050a7c51b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 73a1135482b88ea7c228bc8b228d47c57b2e70a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="cbebb-103">Administración de Administración de API de Azure mediante Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="cbebb-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="cbebb-104">Esta guía le ofrece el servicio Automatización de Azure y cómo se puede usar para simplificar la administración de Administración de API de Azure.</span><span class="sxs-lookup"><span data-stu-id="cbebb-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="cbebb-105">¿Qué es Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="cbebb-105">What is Azure Automation?</span></span>
<span data-ttu-id="cbebb-106">[Automatización de Azure](https://azure.microsoft.com/services/automation/) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos.</span><span class="sxs-lookup"><span data-stu-id="cbebb-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="cbebb-107">Mediante Automatización de Azure, se pueden automatizar las tareas de ejecución prolongada, manuales, propensas a errores y que se repiten para aumentar la confiabilidad, la eficiencia y el valioso tiempo para su organización.</span><span class="sxs-lookup"><span data-stu-id="cbebb-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="cbebb-108">Automatización de Azure proporciona un motor de ejecución de flujo de trabajo altamente confiable y de alta disponibilidad que realiza la escalación para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="cbebb-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="cbebb-109">En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cbebb-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="cbebb-110">Reduzca la sobrecarga operativa y libere al personal de TI/DevOps para concentrarse en el trabajo que proporciona valor al negocio trasladando las tareas de administración en la nube para que se ejecuten automáticamente mediante Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="cbebb-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="cbebb-111">¿Cómo puede ayudar Automatización de Azure a administrar Administración de API de Azure?</span><span class="sxs-lookup"><span data-stu-id="cbebb-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="cbebb-112">Administración de API se puede administrar en Automatización de Azure mediante el uso de [cmdlets de Windows PowerShell para la API de Administración de API de Azure](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span><span class="sxs-lookup"><span data-stu-id="cbebb-112">API Management can be managed in Azure Automation by using the [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="cbebb-113">En Automatización de Azure puede escribir scripts de flujo de trabajo de PowerShell para llevar a cabo muchas de las tareas de Administración de API con los cmdlets.</span><span class="sxs-lookup"><span data-stu-id="cbebb-113">Within Azure Automation you can write PowerShell workflow scripts to perform many of your API Management tasks using the cmdlets.</span></span> <span data-ttu-id="cbebb-114">También puede emparejar estos cmdlets en Automatización de Azure con los cmdlets para otros servicios de Azure, para automatizar tareas complejas a través de los servicios de Azure y sistemas de terceros.</span><span class="sxs-lookup"><span data-stu-id="cbebb-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="cbebb-115">Estos son algunos ejemplos del uso de Administración de API con Automatización:</span><span class="sxs-lookup"><span data-stu-id="cbebb-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="cbebb-116">Azure API Management – Using PowerShell for backup and restore</span><span class="sxs-lookup"><span data-stu-id="cbebb-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="cbebb-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cbebb-117">Next Steps</span></span>
<span data-ttu-id="cbebb-118">Ahora que ha aprendido los aspectos básicos de Automatización de Azure y cómo se puede usar para administrar Administración de API de Azure, siga estos vínculos para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="cbebb-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure API Management, follow these links to learn more.</span></span>

* <span data-ttu-id="cbebb-119">Consulte el [tutorial de introducción](../automation/automation-first-runbook-graphical.md)de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="cbebb-119">See the Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

