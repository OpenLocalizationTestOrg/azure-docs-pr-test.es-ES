---
title: "aaaManage aplicación Web de Azure mediante la automatización de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo Hola servicio automatización de Azure puede ser usado toomanage aplicación Web de Azure."
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
ms.openlocfilehash: 6d80351a2927f26753cfbaead6e1c0c3c94e86e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="ac3f8-103">Administración de aplicaciones web de Azure mediante Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="ac3f8-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="ac3f8-104">Esta guía le presentará los toohello servicio de automatización de Azure y cómo puede resultarle toosimplify usa administración de aplicación Web de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac3f8-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="ac3f8-105">¿Qué es Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="ac3f8-105">What is Azure Automation?</span></span>
<span data-ttu-id="ac3f8-106">[Automatización de Azure](../automation/automation-intro.md) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos.</span><span class="sxs-lookup"><span data-stu-id="ac3f8-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="ac3f8-107">Mediante automatización de Azure, pueden ser, repetidas, larga ejecución, tareas manuales y propensas a errores tooincrease automatizadas confiabilidad y eficacia, toovalue de tiempo para su organización.</span><span class="sxs-lookup"><span data-stu-id="ac3f8-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="ac3f8-108">Automatización de Azure ofrece un motor de ejecución de flujo de trabajo altamente confiable y de alta disponibilidad que escala toomeet sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="ac3f8-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="ac3f8-109">En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ac3f8-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="ac3f8-110">Reducir la sobrecarga operativa y liberar TI y DevOps toofocus de personal en el trabajo que agrega valor empresarial moviendo el toobe de tareas de administración en la nube se ejecute automáticamente mediante la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac3f8-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="ac3f8-111">¿Cómo puede ayudar Automatización de Azure a administrar Aplicaciones web de Azure?</span><span class="sxs-lookup"><span data-stu-id="ac3f8-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="ac3f8-112">Aplicación Web puede administrarse en automatización de Azure mediante los cmdlets de PowerShell de Hola que están disponibles en hello [módulos de PowerShell de Azure](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="ac3f8-112">Web App can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="ac3f8-113">También puede [instalar estos cmdlets de PowerShell de aplicación Web en la automatización de Azure](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), de modo que puede realizar todas las tareas de administración de la aplicación Web en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac3f8-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within hello service.</span></span> <span data-ttu-id="ac3f8-114">También se puede emparejar estos cmdlets en automatización de Azure con los cmdlets de Hola para otras tareas complejas de tooautomate de servicios de Azure a través de los servicios de Azure y sistemas de terceros 3rd.</span><span class="sxs-lookup"><span data-stu-id="ac3f8-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="ac3f8-115">Estos son algunos ejemplos de administración de Servicios de aplicaciones con Automatización:</span><span class="sxs-lookup"><span data-stu-id="ac3f8-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="ac3f8-116">Scripts para administrar Aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="ac3f8-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="ac3f8-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ac3f8-117">Next steps</span></span>
<span data-ttu-id="ac3f8-118">Ahora que conoce los fundamentos de Hola de automatización de Azure y cómo puede ser usado toomanage aplicación Web de Azure, siga estas toolearn de vínculos más información acerca de la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac3f8-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Web App, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="ac3f8-119">Vea Hola automatización de Azure [Tutorial de introducción](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="ac3f8-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

