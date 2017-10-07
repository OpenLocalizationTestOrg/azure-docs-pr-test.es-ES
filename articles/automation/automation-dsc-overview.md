---
title: "información general de DSC de automatización aaaAzure | Documentos de Microsoft"
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
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="21a13-104">Información general de DSC de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="21a13-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="21a13-105">DSC de automatización de Azure es un servicio de Azure que le permite toowrite, administrar y compilar la configuración de estado deseado (DSC) de PowerShell [configuraciones](https://msdn.microsoft.com/powershell/dsc/configurations), importar [recursos de DSC](https://msdn.microsoft.com/powershell/dsc/resources)y asignar nodos de tootarget configuraciones, todo en nube Hola.</span><span class="sxs-lookup"><span data-stu-id="21a13-105">Azure Automation DSC is an Azure service that allows you toowrite, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations tootarget nodes, all in hello cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="21a13-106">¿Por qué usar DSC de Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="21a13-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="21a13-107">DSC de Azure Automation proporciona varias ventajas con respecto a DSC fuera de Azure.</span><span class="sxs-lookup"><span data-stu-id="21a13-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="21a13-108">Servidor de extracción integrado</span><span class="sxs-lookup"><span data-stu-id="21a13-108">Built-in pull server</span></span>

<span data-ttu-id="21a13-109">Automatización de Azure ofrece un [servidor de extracción de DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) para que los nodos de destino recibirán automáticamente las configuraciones, se ajustan estado toohello deseado e informar sobre su cumplimiento.</span><span class="sxs-lookup"><span data-stu-id="21a13-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform toohello desired state, and report back on their compliance.</span></span>
<span data-ttu-id="21a13-110">servidor de extracción integrados de Hello en automatización de Azure elimina Hola necesidad tooset seguridad y mantener su propio servidor de extracción.</span><span class="sxs-lookup"><span data-stu-id="21a13-110">hello built-in pull server in Azure Automation eliminates hello need tooset up and maintain your own pull server.</span></span>
<span data-ttu-id="21a13-111">Automatización de Azure puede tener como destino máquinas físicas o virtuales de Windows o Linux, en la nube de Hola o de forma local.</span><span class="sxs-lookup"><span data-stu-id="21a13-111">Azure Automation can target virtual or physical Windows or Linux machines, in hello cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="21a13-112">Administración de todos los artefactos de DSC</span><span class="sxs-lookup"><span data-stu-id="21a13-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="21a13-113">DSC de automatización de Azure aporta Hola misma capa de administración demasiado[la configuración de estado deseado de PowerShell](https://msdn.microsoft.com/powershell/dsc/overview) como la automatización de Azure proporciona para secuencias de comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="21a13-113">Azure Automation DSC brings hello same management layer too[PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="21a13-114">Hola portal de Azure o desde PowerShell, puede administrar todos sus DSC configuraciones, los recursos y nodos de destino.</span><span class="sxs-lookup"><span data-stu-id="21a13-114">From hello Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Captura de pantalla de hoja de automatización de Azure Hola](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="21a13-116">Importación de datos de informes a Log Analytics</span><span class="sxs-lookup"><span data-stu-id="21a13-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="21a13-117">Los nodos que se administran con el DSC de automatización de Azure enviar detallada estado datos toohello extracción integrada servidor de informes.</span><span class="sxs-lookup"><span data-stu-id="21a13-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data toohello built-in pull server.</span></span>
<span data-ttu-id="21a13-118">Puede configurar toosend de DSC de automatización de Azure en esta área de trabajo de análisis de registros de Microsoft Operations Management Suite (OMS) de tooyour de datos.</span><span class="sxs-lookup"><span data-stu-id="21a13-118">You can configure Azure Automation DSC toosend this data tooyour Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="21a13-119">toolearn toosend DSC estado datos tooyour área de trabajo de análisis de registros, vea [al día Azure DSC de automatización reporting datos tooOMS análisis de registros](automation-dsc-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="21a13-119">toolearn how toosend DSC status data tooyour Log Analytics workspace, see [Forward Azure Automation DSC reporting data tooOMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="21a13-120">Vídeo de presentación</span><span class="sxs-lookup"><span data-stu-id="21a13-120">Introduction video</span></span>

<span data-ttu-id="21a13-121">¿Prefiere ver tooreading?</span><span class="sxs-lookup"><span data-stu-id="21a13-121">Prefer watching tooreading?</span></span> <span data-ttu-id="21a13-122">Eche un vistazo a Hola después de vídeo de mayo de 2015, se presentó por primera vez al DSC de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="21a13-122">Have a look at hello following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="21a13-123">Aunque los conceptos de Hola y ciclo de vida que se describe en este vídeo son correctas, DSC de automatización de Azure ha progresado mucho porque este vídeo se grabó.</span><span class="sxs-lookup"><span data-stu-id="21a13-123">While hello concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="21a13-124">Ahora está disponible con carácter general, tiene una interfaz de usuario mucho más amplia de hello portal de Azure y admite muchas funciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="21a13-124">It is now generally available, has a much more extensive UI in hello Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="21a13-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="21a13-125">Next steps</span></span>

* <span data-ttu-id="21a13-126">toolearn cómo tooonboard toobe de nodos administrados con el DSC de automatización de Azure, consulte [incorporar máquinas para la administración mediante el DSC de automatización de Azure](automation-dsc-onboarding.md)</span><span class="sxs-lookup"><span data-stu-id="21a13-126">toolearn how tooonboard nodes toobe managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="21a13-127">tooget a usar DSC de automatización de Azure, consulte [Introducción a DSC de automatización de Azure](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="21a13-127">tooget started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="21a13-128">toolearn sobre la compilación de configuraciones de DSC para que pueda asignar nodos tootarget, consulte [compilación de configuraciones de DSC de automatización de Azure](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="21a13-128">toolearn about compiling DSC configurations so that you can assign them tootarget nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="21a13-129">Para ver la referencia de cmdlets de PowerShell para DSC de Azure Automation, consulte [Cmdlets de DSC de Azure Automation](/powershell/module/azurerm.automation/#automation).</span><span class="sxs-lookup"><span data-stu-id="21a13-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="21a13-130">Para obtener información de precios, consulte [Precios de DSC de Azure Automation](https://azure.microsoft.com/pricing/details/automation/).</span><span class="sxs-lookup"><span data-stu-id="21a13-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="21a13-131">toosee muestra un ejemplo del uso de DSC de automatización de Azure en una canalización de implementación continua, vea [tooIaaS de implementación continua DSC de automatización de Azure usando máquinas virtuales y Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="21a13-131">toosee an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment tooIaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>
