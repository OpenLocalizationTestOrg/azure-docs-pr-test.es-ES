---
title: "aaaManage almacenamiento de Azure mediante automatización de Azure"
description: "Obtenga información acerca de cómo se Hola servicio automatización de Azure pueden toomanage usado el almacenamiento de Azure a escala."
services: storage, automation
documentationcenter: 
author: jodoglevy
manager: eamono
editor: 
ms.assetid: bac41c39-1d95-46aa-a481-ec17bbb21b40
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: eamono
ms.openlocfilehash: 15e34128ffb0ba3315b5260442f628b5978c5197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="b0074-103">Administración de Almacenamiento de Azure mediante Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="b0074-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="b0074-104">Esta guía le presentará los toohello servicio de automatización de Azure y cómo puede resultarle toosimplify usa administración de los blobs, tablas y colas de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b0074-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="b0074-105">¿Qué es Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="b0074-105">What is Azure Automation?</span></span>
<span data-ttu-id="b0074-106">[Automatización de Azure](https://azure.microsoft.com/services/automation/) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos.</span><span class="sxs-lookup"><span data-stu-id="b0074-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="b0074-107">Mediante automatización de Azure, de larga ejecución, manual, propensa a errores y con frecuencia repite tareas se pueden tooincrease automatizadas confiabilidad y eficacia y reducir el tiempo toovalue para su organización.</span><span class="sxs-lookup"><span data-stu-id="b0074-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability and efficiency, and reduce time toovalue for your organization.</span></span>

<span data-ttu-id="b0074-108">Automatización de Azure ofrece un motor de ejecución de flujo de trabajo altamente confiable y alta disponibilidad que escala toomeet sus necesidades a medida que crece la organización.</span><span class="sxs-lookup"><span data-stu-id="b0074-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="b0074-109">En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b0074-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="b0074-110">Reducir la sobrecarga operativa y liberar TI / DevOps toofocus de personal en el trabajo que agrega valor empresarial moviendo el toobe de tareas de administración en la nube se ejecute automáticamente mediante la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="b0074-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="b0074-111">¿Cómo puede ayudar el servicio Automatización de Azure a administrar Almacenamiento de Azure?</span><span class="sxs-lookup"><span data-stu-id="b0074-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="b0074-112">Almacenamiento de Azure puede administrarse en automatización de Azure mediante los cmdlets de PowerShell de Hola que están disponibles en [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0074-112">Azure Storage can be managed in Azure Automation by using hello PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="b0074-113">Automatización de Azure tiene estos cmdlets de PowerShell de almacenamiento disponibles fuera del cuadro de hello, por lo que puede realizar todos los blob, tabla y tareas de administración de cola de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0074-113">Azure Automation has these Storage PowerShell cmdlets available out of hello box, so that you can perform all of your blob, table, and queue management tasks within hello service.</span></span> <span data-ttu-id="b0074-114">También se puede emparejar estos cmdlets en automatización de Azure con los cmdlets de Hola para otros servicios de Azure, tareas complejas tooautomate a través de los servicios de Azure y sistemas de terceros 3rd.</span><span class="sxs-lookup"><span data-stu-id="b0074-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="b0074-115">Hola [Galería de runbooks de automatización de Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contiene una variedad de producto equipo y la Comunidad runbooks tooget iniciado automatizar la administración de almacenamiento de Azure, otros servicios de Azure y sistemas de terceros 3rd.</span><span class="sxs-lookup"><span data-stu-id="b0074-115">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="b0074-116">Los runbooks de la Galería incluyen:</span><span class="sxs-lookup"><span data-stu-id="b0074-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="b0074-117">Quitar Blobs desde Almacenamiento de Azure que llevan varios días mediante el Servicio de automatización</span><span class="sxs-lookup"><span data-stu-id="b0074-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="b0074-118">Descargar un Blob desde Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="b0074-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="b0074-119">Hacer una copia de seguridad de todos los discos para una sola VM de Azure o para todas las VM en un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="b0074-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="b0074-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b0074-120">Next Steps</span></span>
<span data-ttu-id="b0074-121">Ahora que conoce los fundamentos de Hola de automatización de Azure y cómo puede resultarle toomanage usado el almacenamiento de Azure los blobs, tablas y colas, siga estas toolearn de vínculos más información acerca de la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="b0074-121">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Storage blobs, tables, and queues, follow these links toolearn more about Azure Automation.</span></span>

<span data-ttu-id="b0074-122">Vea el tutorial de automatización de Azure de hello [crear o importar un runbook en automatización de Azure](../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="b0074-122">See hello Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../automation/automation-creating-importing-runbook.md).</span></span>

