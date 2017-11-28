---
title: "aaaManage administración de API de Azure mediante la automatización de Azure"
description: "Obtenga información acerca de cómo Hola servicio automatización de Azure puede ser usado toomanage administración de API de Azure."
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
ms.openlocfilehash: 05b8e3cad786fa701feb88f7b6d9629f16686d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="32b79-103">Administración de Administración de API de Azure mediante Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="32b79-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="32b79-104">Esta guía le presentará los toohello servicio de automatización de Azure y cómo puede resultarle toosimplify usa administración de administración de API de Azure.</span><span class="sxs-lookup"><span data-stu-id="32b79-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="32b79-105">¿Qué es Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="32b79-105">What is Azure Automation?</span></span>
<span data-ttu-id="32b79-106">[Automatización de Azure](https://azure.microsoft.com/services/automation/) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos.</span><span class="sxs-lookup"><span data-stu-id="32b79-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="32b79-107">Mediante automatización de Azure, pueden ser, repetidas, larga ejecución, tareas manuales y propensas a errores tooincrease automatizadas confiabilidad y eficacia, toovalue de tiempo para su organización.</span><span class="sxs-lookup"><span data-stu-id="32b79-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="32b79-108">Automatización de Azure ofrece un motor de ejecución de flujo de trabajo altamente confiable y de alta disponibilidad que escala toomeet sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="32b79-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="32b79-109">En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="32b79-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="32b79-110">Reducir la sobrecarga operativa y liberar TI y DevOps toofocus de personal en el trabajo que agrega valor empresarial moviendo el toobe de tareas de administración en la nube se ejecute automáticamente mediante la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="32b79-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="32b79-111">¿Cómo puede ayudar Automatización de Azure a administrar Administración de API de Azure?</span><span class="sxs-lookup"><span data-stu-id="32b79-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="32b79-112">Administración de API puede administrarse en automatización de Azure mediante hello [cmdlets de Windows PowerShell para la API de administración de API de Azure](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span><span class="sxs-lookup"><span data-stu-id="32b79-112">API Management can be managed in Azure Automation by using hello [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="32b79-113">En la automatización de Azure puede escribir tooperform de secuencias de comandos de flujo de trabajo de PowerShell muchas de las tareas de administración de API con cmdlets de Hola.</span><span class="sxs-lookup"><span data-stu-id="32b79-113">Within Azure Automation you can write PowerShell workflow scripts tooperform many of your API Management tasks using hello cmdlets.</span></span> <span data-ttu-id="32b79-114">También se puede emparejar estos cmdlets en automatización de Azure con los cmdlets de Hola para otros servicios de Azure, tareas complejas tooautomate a través de los servicios de Azure y sistemas de terceros 3rd.</span><span class="sxs-lookup"><span data-stu-id="32b79-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="32b79-115">Estos son algunos ejemplos del uso de Administración de API con Automatización:</span><span class="sxs-lookup"><span data-stu-id="32b79-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="32b79-116">Azure API Management – Using PowerShell for backup and restore</span><span class="sxs-lookup"><span data-stu-id="32b79-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="32b79-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32b79-117">Next Steps</span></span>
<span data-ttu-id="32b79-118">Ahora que conoce los fundamentos de Hola de automatización de Azure y cómo puede resultarle toomanage usa administración de API de Azure, siga estas toolearn de vínculos más.</span><span class="sxs-lookup"><span data-stu-id="32b79-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure API Management, follow these links toolearn more.</span></span>

* <span data-ttu-id="32b79-119">Vea Hola automatización de Azure [tutorial de introducción](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="32b79-119">See hello Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

