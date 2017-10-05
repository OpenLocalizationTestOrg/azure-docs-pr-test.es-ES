---
title: "Información general de DSC de Azure Automation | Microsoft Docs"
description: "Una información general de Configuración de estado deseado (DSC) de Automatización de Azure, sus condiciones y problemas conocidos"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "powershell dsc, configuración de estado deseado, powershell dsc azure"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 468321fa6863d78bc0d179fbe5c2ed6195040d50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="8c157-104">Información general de DSC de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="8c157-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="8c157-105">DSC de Azure Automation es un servicio de Azure que le permite escribir, administrar y compilar [configuraciones](https://msdn.microsoft.com/powershell/dsc/configurations) de configuración de estado deseado (DSC) de PowerShell, importar [recursos de DSC](https://msdn.microsoft.com/powershell/dsc/resources) y asignar configuraciones a nodos de destino, todo en la nube.</span><span class="sxs-lookup"><span data-stu-id="8c157-105">Azure Automation DSC is an Azure service that allows you to write, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations to target nodes, all in the cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="8c157-106">¿Por qué usar DSC de Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="8c157-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="8c157-107">DSC de Azure Automation proporciona varias ventajas con respecto a DSC fuera de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c157-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="8c157-108">Servidor de extracción integrado</span><span class="sxs-lookup"><span data-stu-id="8c157-108">Built-in pull server</span></span>

<span data-ttu-id="8c157-109">Azure Automation proporciona un [servidor de extracción de DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) para que los nodos de destino reciban automáticamente las configuraciones, se ajusten al estado deseado y devuelvan la información de cumplimiento.</span><span class="sxs-lookup"><span data-stu-id="8c157-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform to the desired state, and report back on their compliance.</span></span>
<span data-ttu-id="8c157-110">El servidor de extracción integrado en Azure Automation elimina la necesidad de configurar y mantener su propio servidor de extracción.</span><span class="sxs-lookup"><span data-stu-id="8c157-110">The built-in pull server in Azure Automation eliminates the need to set up and maintain your own pull server.</span></span>
<span data-ttu-id="8c157-111">Azure Automation puede tener como destino máquinas físicas o virtuales Windows o Linux, en la nube o en un entorno local.</span><span class="sxs-lookup"><span data-stu-id="8c157-111">Azure Automation can target virtual or physical Windows or Linux machines, in the cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="8c157-112">Administración de todos los artefactos de DSC</span><span class="sxs-lookup"><span data-stu-id="8c157-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="8c157-113">DSC de Azure Automation lleva a la [configuración de estado deseado de PowerShell](https://msdn.microsoft.com/powershell/dsc/overview) la misma capa de administración que ofrece Azure Automation para el scripting de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c157-113">Azure Automation DSC brings the same management layer to [PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="8c157-114">Desde Azure Portal o desde PowerShell, puede administrar todas las configuraciones, recursos y nodos de destino de DSC.</span><span class="sxs-lookup"><span data-stu-id="8c157-114">From the Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Captura de pantalla de la hoja de Azure Automation](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="8c157-116">Importación de datos de informes a Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8c157-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="8c157-117">Los nodos que se administran con DSC de Azure Automation envían datos de informe de estado detallados al servidor de extracción integrado.</span><span class="sxs-lookup"><span data-stu-id="8c157-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data to the built-in pull server.</span></span>
<span data-ttu-id="8c157-118">Puede configurar DSC de Azure Automation para que envíe estos datos a su área de trabajo de Log Analytics de Microsoft Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="8c157-118">You can configure Azure Automation DSC to send this data to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="8c157-119">Para obtener información sobre cómo enviar datos de estado de DSC al área de trabajo de Log Analytics, vea [Reenvío de datos de informes de DSC de Azure Automation a Log Analytics de OMS](automation-dsc-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="8c157-119">To learn how to send DSC status data to your Log Analytics workspace, see [Forward Azure Automation DSC reporting data to OMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="8c157-120">Vídeo de presentación</span><span class="sxs-lookup"><span data-stu-id="8c157-120">Introduction video</span></span>

<span data-ttu-id="8c157-121">¿Prefiere ver a leer?</span><span class="sxs-lookup"><span data-stu-id="8c157-121">Prefer watching to reading?</span></span> <span data-ttu-id="8c157-122">Eche un vistazo al vídeo siguiente, de mayo de 2015, cuando se anunció DSC de Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8c157-122">Have a look at the following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="8c157-123">Aunque los conceptos y el ciclo de vida que se tratan en este vídeo son correctos, DSC de Azure Automation ha progresado mucho desde que se grabó este vídeo.</span><span class="sxs-lookup"><span data-stu-id="8c157-123">While the concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="8c157-124">Ahora está disponible con carácter general, tiene una interfaz de usuario mucho más amplia en el Portal de Azure y admite muchas funciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="8c157-124">It is now generally available, has a much more extensive UI in the Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="8c157-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8c157-125">Next steps</span></span>

* <span data-ttu-id="8c157-126">Para obtener información sobre cómo incorporar nodos para que se administren con DSC de Azure Automation, consulte [Incorporación de máquinas para administrarlas con DSC de Azure Automation](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="8c157-126">To learn how to onboard nodes to be managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="8c157-127">Para empezar a usar DSC de Azure Automation, consulte [Introducción a DSC de Azure Automation](automation-dsc-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="8c157-127">To get started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="8c157-128">Para obtener información acerca de la compilación de configuraciones de DSC para que poder asignarlas a los nodos de destino, vea [Compilación de configuraciones en DSC de Azure Automation](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="8c157-128">To learn about compiling DSC configurations so that you can assign them to target nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="8c157-129">Para ver la referencia de cmdlets de PowerShell para DSC de Azure Automation, consulte [Cmdlets de DSC de Azure Automation](/powershell/module/azurerm.automation/#automation).</span><span class="sxs-lookup"><span data-stu-id="8c157-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="8c157-130">Para obtener información de precios, consulte [Precios de DSC de Azure Automation](https://azure.microsoft.com/pricing/details/automation/).</span><span class="sxs-lookup"><span data-stu-id="8c157-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="8c157-131">Para ver un ejemplo del uso de DSC de automatización de Azure en una canalización de implementación continua, vea [implementación continua para DSC de automatización de Azure de uso de máquinas virtuales de IaaS y Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="8c157-131">To see an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment to IaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>