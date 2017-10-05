---
title: "Administración de Almacenamiento de Azure mediante Automatización de Azure"
description: "Obtenga información acerca de cómo puede usarse el servicio Automatización de Azure para administrar Almacenamiento de Azure a escala."
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
ms.openlocfilehash: fbf1cd9e73615f8d991f348cb705aa9df8b55b4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="c7b2d-103">Administración de Almacenamiento de Azure mediante Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="c7b2d-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="c7b2d-104">Esta guía le ofrece el servicio Automatización de Azure y cómo se puede usar para simplificar la administración de blobs, tablas y colas de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c7b2d-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="c7b2d-105">¿Qué es Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="c7b2d-105">What is Azure Automation?</span></span>
<span data-ttu-id="c7b2d-106">[Automatización de Azure](https://azure.microsoft.com/services/automation/) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos.</span><span class="sxs-lookup"><span data-stu-id="c7b2d-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="c7b2d-107">Mediante Automatización de Azure, se pueden automatizar las tareas de ejecución prolongada, manuales, propensas a errores y que se repiten con frecuencia para aumentar la confiabilidad y la eficiencia y reducir el tiempo de amortización para su organización.</span><span class="sxs-lookup"><span data-stu-id="c7b2d-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability and efficiency, and reduce time to value for your organization.</span></span>

<span data-ttu-id="c7b2d-108">Automatización de Azure proporciona un motor de ejecución de flujo de trabajo altamente confiable y de alta disponibilidad que realiza la escalación para satisfacer sus necesidades a medida que crece la organización.</span><span class="sxs-lookup"><span data-stu-id="c7b2d-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="c7b2d-109">En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c7b2d-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="c7b2d-110">Reduzca la sobrecarga operativa y libere al personal de TI/DevOps para concentrarse en el trabajo que proporciona valor al negocio trasladando las tareas de administración en la nube para que se ejecuten automáticamente mediante Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="c7b2d-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="c7b2d-111">¿Cómo puede ayudar el servicio Automatización de Azure a administrar Almacenamiento de Azure?</span><span class="sxs-lookup"><span data-stu-id="c7b2d-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="c7b2d-112">Almacenamiento de Azure se puede administrar en Automatización de Azure mediante los cmdlets de PowerShell que están disponibles en [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7b2d-112">Azure Storage can be managed in Azure Automation by using the PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="c7b2d-113">Automatización de Azure tiene estos cmdlets de PowerShell de Almacenamiento disponibles directamente para que pueda realizar todas las tareas de administración de blobs, tablas y colas dentro del servicio.</span><span class="sxs-lookup"><span data-stu-id="c7b2d-113">Azure Automation has these Storage PowerShell cmdlets available out of the box, so that you can perform all of your blob, table, and queue management tasks within the service.</span></span> <span data-ttu-id="c7b2d-114">También puede emparejar estos cmdlets en Automatización de Azure con los cmdlets para otros servicios de Azure, para automatizar tareas complejas a través de los servicios de Azure y sistemas de terceros.</span><span class="sxs-lookup"><span data-stu-id="c7b2d-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="c7b2d-115">La [Galería de runbooks de Automatización de Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contiene una gran variedad de runbooks de comunidad y equipo de producto para empezar a automatizar la administración de Almacenamiento de Azure, otros servicios de Azure y sistemas de terceros.</span><span class="sxs-lookup"><span data-stu-id="c7b2d-115">The [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks to get started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="c7b2d-116">Los runbooks de la Galería incluyen:</span><span class="sxs-lookup"><span data-stu-id="c7b2d-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="c7b2d-117">Quitar Blobs desde Almacenamiento de Azure que llevan varios días mediante el Servicio de automatización</span><span class="sxs-lookup"><span data-stu-id="c7b2d-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="c7b2d-118">Descargar un Blob desde Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="c7b2d-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="c7b2d-119">Hacer una copia de seguridad de todos los discos para una sola VM de Azure o para todas las VM en un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="c7b2d-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="c7b2d-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c7b2d-120">Next Steps</span></span>
<span data-ttu-id="c7b2d-121">Ahora que ha aprendido los aspectos básicos de Automatización de Azure y cómo se puede usar para administrar blobs, tablas y colas de Almacenamiento de Azure, siga estos vínculos para obtener más información acerca de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="c7b2d-121">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Storage blobs, tables, and queues, follow these links to learn more about Azure Automation.</span></span>

<span data-ttu-id="c7b2d-122">Consulte el tutorial de Automatización de Azure [Crear o importar un Runbook en Automatización de Azure](../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="c7b2d-122">See the Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../automation/automation-creating-importing-runbook.md).</span></span>

