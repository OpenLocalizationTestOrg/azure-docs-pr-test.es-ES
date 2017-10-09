---
title: "aaaManage servicios de nube de Azure mediante la automatización de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se Hola servicio automatización de Azure pueden toomanage usa servicios de nube de Azure a escala."
services: cloud-services, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: 3789810a-2892-4eef-bf29-c781c1b5af48
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2016
ms.author: timlt
ms.openlocfilehash: 8e920fb94955466bfec71cc332444f5f0ee497a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="73c05-103">Administración de Servicios en la nube de Azure mediante Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="73c05-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="73c05-104">Esta guía le presentará los toohello servicio de automatización de Azure y cómo puede resultarle toosimplify usa administración de los servicios de nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="73c05-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="73c05-105">¿Qué es Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="73c05-105">What is Azure Automation?</span></span>
<span data-ttu-id="73c05-106">[Automatización de Azure](https://azure.microsoft.com/services/automation/) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos.</span><span class="sxs-lookup"><span data-stu-id="73c05-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="73c05-107">Mediante automatización de Azure, las tareas de ejecución prolongada, manuales, propensa a errores y repiten con frecuencia pueden ser tooincrease automatizadas confiabilidad y eficacia, toovalue de tiempo para su organización.</span><span class="sxs-lookup"><span data-stu-id="73c05-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="73c05-108">Automatización de Azure ofrece un motor de ejecución de flujo de trabajo altamente confiable y alta disponibilidad que escala toomeet sus necesidades a medida que crece la organización.</span><span class="sxs-lookup"><span data-stu-id="73c05-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="73c05-109">En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="73c05-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="73c05-110">Reducir la sobrecarga operativa y liberar TI / DevOps toofocus de personal en el trabajo que agrega valor empresarial moviendo el toobe de tareas de administración en la nube se ejecute automáticamente mediante la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="73c05-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="73c05-111">¿Cómo puede ayudar el servicio Automatización de Azure a administrar los servicios en la nube de Azure?</span><span class="sxs-lookup"><span data-stu-id="73c05-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="73c05-112">Servicios de nube de Azure pueden administrarse en automatización de Azure mediante los cmdlets de PowerShell de Hola que están disponibles en hello [herramientas de Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="73c05-112">Azure cloud services can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="73c05-113">Automatización de Azure tiene estos cmdlets de PowerShell de servicio de nube disponible fuera del cuadro de hello, por lo que puede realizar todas las tareas de administración de servicio de nube en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="73c05-113">Azure Automation has these cloud service PowerShell cmdlets available out of hello box, so that you can perform all of your cloud service management tasks within hello service.</span></span> <span data-ttu-id="73c05-114">También se puede emparejar estos cmdlets en automatización de Azure con los cmdlets de Hola para otros servicios de Azure, tareas complejas tooautomate a través de los servicios de Azure y sistemas de terceros 3rd.</span><span class="sxs-lookup"><span data-stu-id="73c05-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="73c05-115">Algunos ejemplos de uso de toomanage de automatización de Azure que incluyen servicios en la nube:</span><span class="sxs-lookup"><span data-stu-id="73c05-115">Some example uses of Azure Automation toomanage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="73c05-116">Implementación continua de un servicio en la nube siempre que cscfg o cspkg estén actualizados en el almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="73c05-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="73c05-117">Reinicio de instancias de servicio en la nube en paralelo (un dominio de actualización a la vez)</span><span class="sxs-lookup"><span data-stu-id="73c05-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="73c05-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="73c05-118">Next Steps</span></span>
<span data-ttu-id="73c05-119">Ahora que ha aprendido los conceptos básicos de Hola de automatización de Azure y cómo puede resultarle toomanage usa servicios de nube de Azure, siga estas toolearn de vínculos más información acerca de la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="73c05-119">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure cloud services, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="73c05-120">Información general sobre Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="73c05-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="73c05-121">Mi primer runbook</span><span class="sxs-lookup"><span data-stu-id="73c05-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="73c05-122">Mapa de aprendizaje de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="73c05-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
