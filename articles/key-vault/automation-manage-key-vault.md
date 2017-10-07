---
title: "aaaManage almacén de claves de Azure mediante automatización de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se Hola servicio automatización de Azure pueden toomanage usa el almacén de claves de Azure."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="3a8bc-103">Administración del Almacén de claves de Azure mediante Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="3a8bc-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="3a8bc-104">Esta guía le presentará los toohello servicio de automatización de Azure y cómo puede resultarle toosimplify usa administración de sus claves y secretos en el almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="3a8bc-104">This guide will introduce you toohello Azure Automation service and how it can be used toosimplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="3a8bc-105">¿Qué es Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="3a8bc-105">What is Azure Automation?</span></span>
<span data-ttu-id="3a8bc-106">[Automatización de Azure](../automation/automation-intro.md) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos y la configuración de estado deseado.</span><span class="sxs-lookup"><span data-stu-id="3a8bc-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="3a8bc-107">Mediante automatización de Azure, pueden ser, repetidas, larga ejecución, tareas manuales y propensas a errores tooincrease automatizadas confiabilidad y eficacia, toovalue de tiempo para su organización.</span><span class="sxs-lookup"><span data-stu-id="3a8bc-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="3a8bc-108">Automatización de Azure ofrece un motor de ejecución de flujo de trabajo altamente confiable y de alta disponibilidad que escala toomeet sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="3a8bc-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="3a8bc-109">En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3a8bc-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="3a8bc-110">Reducir la sobrecarga operativa y liberar TI y DevOps toofocus de personal en el trabajo que agrega valor empresarial moviendo el toobe de tareas de administración en la nube se ejecute automáticamente mediante la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="3a8bc-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="3a8bc-111">¿Cómo puede ayudar Automatización de Azure a administrar el Almacén de claves de Azure?</span><span class="sxs-lookup"><span data-stu-id="3a8bc-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="3a8bc-112">El almacén de claves se pueden administrar en automatización de Azure mediante hello [cmdlets del almacén de claves de AzureRM](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) y [cmdlets del almacén de claves de Azure clásico](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a8bc-112">Key Vault can be managed in Azure Automation by using hello [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="3a8bc-113">Hola módulo de Azure para administrar el almacén de claves clásico está disponible automáticamente en automatización de Azure y se puede importar hello [AzureRM KeyVault módulo](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) en automatización de Azure, por lo que puede realizar muchas de la administración de almacén de claves tareas de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a8bc-113">hello Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import hello [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within hello service.</span></span> <span data-ttu-id="3a8bc-114">También se puede emparejar estos cmdlets en automatización de Azure con los cmdlets de Hola para otros servicios de Azure, tareas complejas tooautomate a través de los servicios de Azure y sistemas de terceros 3rd.</span><span class="sxs-lookup"><span data-stu-id="3a8bc-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="3a8bc-115">Con los cmdlets del almacén de claves de Azure Hola puede realizar estas tareas, entre otros:</span><span class="sxs-lookup"><span data-stu-id="3a8bc-115">With hello Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="3a8bc-116">Crear y configurar un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="3a8bc-116">Create and configure a key vault</span></span>
* <span data-ttu-id="3a8bc-117">Crear o importar una clave</span><span class="sxs-lookup"><span data-stu-id="3a8bc-117">Create or import a key</span></span>
* <span data-ttu-id="3a8bc-118">Crear o actualizar un secreto</span><span class="sxs-lookup"><span data-stu-id="3a8bc-118">Create or update a secret</span></span>
* <span data-ttu-id="3a8bc-119">Actualizar los atributos de una clave</span><span class="sxs-lookup"><span data-stu-id="3a8bc-119">Update attributes of a key</span></span>
* <span data-ttu-id="3a8bc-120">Obtener una clave o un secreto</span><span class="sxs-lookup"><span data-stu-id="3a8bc-120">Get a key or secret</span></span>
* <span data-ttu-id="3a8bc-121">Eliminar una clave o un secreto</span><span class="sxs-lookup"><span data-stu-id="3a8bc-121">Delete a key or secret</span></span>

<span data-ttu-id="3a8bc-122">Estos son algunos ejemplos del uso de PowerShell toomanage el almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="3a8bc-122">Here are some examples of using PowerShell toomanage Key Vault:</span></span>  

* [<span data-ttu-id="3a8bc-123">Azure Key Vault - Step by Step (Almacén de claves de Azure: paso a paso)</span><span class="sxs-lookup"><span data-stu-id="3a8bc-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="3a8bc-124">Setting Up and Configuring an Azure Key Vault (Instalar y configurar un Almacén de claves de Azure)</span><span class="sxs-lookup"><span data-stu-id="3a8bc-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="3a8bc-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3a8bc-125">Next steps</span></span>
<span data-ttu-id="3a8bc-126">Ahora que conoce los fundamentos de Hola de automatización de Azure y cómo puede resultarle toomanage usa el almacén de claves de Azure, siga estas toolearn de vínculos más información acerca de la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="3a8bc-126">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Key Vault, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="3a8bc-127">Vea Hola automatización de Azure [Tutorial de introducción](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="3a8bc-127">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="3a8bc-128">Vea hello [scripts de PowerShell de almacén de claves de Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="3a8bc-128">See hello [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

