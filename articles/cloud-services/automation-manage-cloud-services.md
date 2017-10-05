---
title: "Administración de Azure Cloud Services mediante Azure Automation | Microsoft Docs"
description: "Obtenga información acerca de cómo puede usarse el servicio Automatización de Azure para administrar servicios en la nube de Azure a escala."
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
ms.openlocfilehash: 6b5acac1b8647c324988c316cd5602b3dba98a1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="74a3e-103">Administración de Servicios en la nube de Azure mediante Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="74a3e-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="74a3e-104">Esta guía le ofrece el servicio Automatización de Azure y cómo se puede usar para simplificar la administración de los servicios en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="74a3e-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="74a3e-105">¿Qué es Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="74a3e-105">What is Azure Automation?</span></span>
<span data-ttu-id="74a3e-106">[Automatización de Azure](https://azure.microsoft.com/services/automation/) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos.</span><span class="sxs-lookup"><span data-stu-id="74a3e-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="74a3e-107">Mediante Automatización de Azure, se pueden automatizar las tareas de ejecución prolongada, manuales, propensas a errores y que se repiten con frecuencia para aumentar la confiabilidad, la eficiencia y el valioso tiempo para su organización.</span><span class="sxs-lookup"><span data-stu-id="74a3e-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="74a3e-108">Automatización de Azure proporciona un motor de ejecución de flujo de trabajo altamente confiable y de alta disponibilidad que realiza la escalación para satisfacer sus necesidades a medida que crece la organización.</span><span class="sxs-lookup"><span data-stu-id="74a3e-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="74a3e-109">En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="74a3e-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="74a3e-110">Reduzca la sobrecarga operativa y libere al personal de TI/DevOps para concentrarse en el trabajo que proporciona valor al negocio trasladando las tareas de administración en la nube para que se ejecuten automáticamente mediante Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="74a3e-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="74a3e-111">¿Cómo puede ayudar el servicio Automatización de Azure a administrar los servicios en la nube de Azure?</span><span class="sxs-lookup"><span data-stu-id="74a3e-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="74a3e-112">Los servicios en la nube de Azure se pueden administrar en Automatización de Azure mediante el uso de cmdlets de PowerShell que están disponibles en las [herramientas de Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="74a3e-112">Azure cloud services can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="74a3e-113">Automatización de Azure tiene estos cmdlets de PowerShell de servicios en la nube disponibles directamente para que pueda realizar todas las tareas de administración de servicios en la nube dentro del servicio.</span><span class="sxs-lookup"><span data-stu-id="74a3e-113">Azure Automation has these cloud service PowerShell cmdlets available out of the box, so that you can perform all of your cloud service management tasks within the service.</span></span> <span data-ttu-id="74a3e-114">También puede emparejar estos cmdlets en Automatización de Azure con los cmdlets para otros servicios de Azure, para automatizar tareas complejas a través de los servicios de Azure y sistemas de terceros.</span><span class="sxs-lookup"><span data-stu-id="74a3e-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="74a3e-115">Algunos usos de ejemplo de automatización de Azure para administrar servicios en la nube de Azure son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="74a3e-115">Some example uses of Azure Automation to manage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="74a3e-116">Implementación continua de un servicio en la nube siempre que cscfg o cspkg estén actualizados en el almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="74a3e-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="74a3e-117">Reinicio de instancias de servicio en la nube en paralelo (un dominio de actualización a la vez)</span><span class="sxs-lookup"><span data-stu-id="74a3e-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="74a3e-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="74a3e-118">Next Steps</span></span>
<span data-ttu-id="74a3e-119">Ahora que ha aprendido los aspectos básicos de Automatización de Azure y cómo se puede usar para administrar servicios en la nube de Azure, siga estos vínculos para obtener más información acerca de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="74a3e-119">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure cloud services, follow these links to learn more about Azure Automation.</span></span>

* [<span data-ttu-id="74a3e-120">Información general sobre Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="74a3e-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="74a3e-121">Mi primer runbook</span><span class="sxs-lookup"><span data-stu-id="74a3e-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="74a3e-122">Mapa de aprendizaje de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="74a3e-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
