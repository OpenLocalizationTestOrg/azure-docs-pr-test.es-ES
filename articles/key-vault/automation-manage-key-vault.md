---
title: "Administración de Azure Key Vault con Azure Automation | Microsoft Docs"
description: "Obtenga información acerca de cómo puede usarse el servicio de Automatización de Azure para administrar el Almacén de claves de Azure."
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
ms.openlocfilehash: dee39662472fe54776b591977f2b1ecb39d15b00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="8f259-103">Administración del Almacén de claves de Azure mediante Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="8f259-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="8f259-104">Esta guía le ofrece el servicio Automatización de Azure y cómo se puede usar para simplificar la administración de claves y secretos en el Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f259-104">This guide will introduce you to the Azure Automation service and how it can be used to simplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="8f259-105">¿Qué es Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="8f259-105">What is Azure Automation?</span></span>
<span data-ttu-id="8f259-106">[Automatización de Azure](../automation/automation-intro.md) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos y la configuración de estado deseado.</span><span class="sxs-lookup"><span data-stu-id="8f259-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="8f259-107">Mediante Automatización de Azure, se pueden automatizar las tareas de ejecución prolongada, manuales, propensas a errores y que se repiten para aumentar la confiabilidad, la eficiencia y el valioso tiempo para su organización.</span><span class="sxs-lookup"><span data-stu-id="8f259-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="8f259-108">Automatización de Azure proporciona un motor de ejecución de flujo de trabajo altamente confiable y de alta disponibilidad que realiza la escalación para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="8f259-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="8f259-109">En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8f259-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="8f259-110">Reduzca la sobrecarga operativa y libere al personal de TI/DevOps para concentrarse en el trabajo que proporciona valor al negocio trasladando las tareas de administración en la nube para que se ejecuten automáticamente mediante Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f259-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="8f259-111">¿Cómo puede ayudar Automatización de Azure a administrar el Almacén de claves de Azure?</span><span class="sxs-lookup"><span data-stu-id="8f259-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="8f259-112">Key Vault se puede administrar en Azure Automation mediante los [cmdlets AzureRM de Key Vault](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) y los [cmdlets de Azure Key Vault clásico](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f259-112">Key Vault can be managed in Azure Automation by using the [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="8f259-113">El módulo de Azure para administrar el Almacén de claves clásico está disponible automáticamente en Automatización de Azure, mientras que el [módulo AzureRM-KeyVault](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) se puede importar a Automatización de Azure para poder realizar muchas de las tareas de administración de Almacén de claves dentro del servicio.</span><span class="sxs-lookup"><span data-stu-id="8f259-113">The Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import the [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within the service.</span></span> <span data-ttu-id="8f259-114">También puede emparejar estos cmdlets en Automatización de Azure con los cmdlets para otros servicios de Azure, para automatizar tareas complejas a través de los servicios de Azure y sistemas de terceros.</span><span class="sxs-lookup"><span data-stu-id="8f259-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="8f259-115">Con los cmdlets del Almacén de claves de Azure puede realizar estas tareas entre otras:</span><span class="sxs-lookup"><span data-stu-id="8f259-115">With the Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="8f259-116">Crear y configurar un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="8f259-116">Create and configure a key vault</span></span>
* <span data-ttu-id="8f259-117">Crear o importar una clave</span><span class="sxs-lookup"><span data-stu-id="8f259-117">Create or import a key</span></span>
* <span data-ttu-id="8f259-118">Crear o actualizar un secreto</span><span class="sxs-lookup"><span data-stu-id="8f259-118">Create or update a secret</span></span>
* <span data-ttu-id="8f259-119">Actualizar los atributos de una clave</span><span class="sxs-lookup"><span data-stu-id="8f259-119">Update attributes of a key</span></span>
* <span data-ttu-id="8f259-120">Obtener una clave o un secreto</span><span class="sxs-lookup"><span data-stu-id="8f259-120">Get a key or secret</span></span>
* <span data-ttu-id="8f259-121">Eliminar una clave o un secreto</span><span class="sxs-lookup"><span data-stu-id="8f259-121">Delete a key or secret</span></span>

<span data-ttu-id="8f259-122">Estos son algunos ejemplos de cómo usar PowerShell para administrar el Almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="8f259-122">Here are some examples of using PowerShell to manage Key Vault:</span></span>  

* [<span data-ttu-id="8f259-123">Azure Key Vault - Step by Step (Almacén de claves de Azure: paso a paso)</span><span class="sxs-lookup"><span data-stu-id="8f259-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="8f259-124">Setting Up and Configuring an Azure Key Vault (Instalar y configurar un Almacén de claves de Azure)</span><span class="sxs-lookup"><span data-stu-id="8f259-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="8f259-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8f259-125">Next steps</span></span>
<span data-ttu-id="8f259-126">Ahora que ha aprendido los aspectos básicos de Automatización de Azure y cómo se puede usar para administrar el Almacén de claves de Azure, siga estos vínculos para obtener más información acerca de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f259-126">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Key Vault, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="8f259-127">Consulte el [Tutorial de introducción](../automation/automation-first-runbook-graphical.md)de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f259-127">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="8f259-128">Consulte los [scripts de PowerShell del Almacén de claves de Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="8f259-128">See the [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

