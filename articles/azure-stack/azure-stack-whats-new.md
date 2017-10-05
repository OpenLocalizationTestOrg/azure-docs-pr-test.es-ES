---
title: Novedades de la pila de Azure | Documentos de Microsoft
description: Novedades de la pila de Azure
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 872b0651-0a92-4d28-b2e6-07d0a4a9a25a
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/13/2017
ms.author: helaw
ms.openlocfilehash: 28cc736704a9700845a6d2f53f4fbd06b8a81201
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-azure-stack"></a><span data-ttu-id="e46bf-103">Novedades de la pila de Azure</span><span class="sxs-lookup"><span data-stu-id="e46bf-103">What's new in Azure Stack</span></span>
<span data-ttu-id="e46bf-104">Esta versión proporciona nuevas características para los inquilinos y los administradores.</span><span class="sxs-lookup"><span data-stu-id="e46bf-104">This release provides new features for both tenants and administrators.</span></span>

## <a name="content-services-and-tools"></a><span data-ttu-id="e46bf-105">Contenido, servicios y herramientas</span><span class="sxs-lookup"><span data-stu-id="e46bf-105">Content, services, and tools</span></span>
* <span data-ttu-id="e46bf-106">[Los servicios de federación de Active Directory (AD FS)](azure-stack-key-features.md#identity) soporte técnico proporciona opciones de identidad para escenarios donde la conectividad de red es limitado o intermitente.</span><span class="sxs-lookup"><span data-stu-id="e46bf-106">[Active Directory Federation Services (AD FS)](azure-stack-key-features.md#identity) support provides identity options for scenarios where network connectivity is limited or intermittent.</span></span>
* <span data-ttu-id="e46bf-107">Puede utilizar conjuntos de escalas de máquina Virtual de Azure para proporcionar escalabilidad administrado y escala de cargas de trabajo basadas en VM de IaaS.</span><span class="sxs-lookup"><span data-stu-id="e46bf-107">You can use Azure Virtual Machine Scale Sets to provide managed scale-out and scale-in of IaaS VM-based workloads.</span></span> 
* <span data-ttu-id="e46bf-108">Usar tamaños de máquinas virtuales de serie D de Azure para lograr coherencia y aumentar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="e46bf-108">Use Azure D-Series VM sizes for increased performance and consistency.</span></span>
* <span data-ttu-id="e46bf-109">Implementar y crear plantillas con discos de Temp que sean coherentes con Azure.</span><span class="sxs-lookup"><span data-stu-id="e46bf-109">Deploy and create templates with Temp Disks that are consistent with Azure.</span></span>
* <span data-ttu-id="e46bf-110">[Distribución de Marketplace](azure-stack-download-azure-marketplace-item.md) le permite usar el contenido de Azure Marketplace y que estén disponibles en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="e46bf-110">[Marketplace Syndication](azure-stack-download-azure-marketplace-item.md) allows you to use content from the Azure Marketplace and make available in Azure Stack.</span></span>

## <a name="infrastructure-and-operations"></a><span data-ttu-id="e46bf-111">Infraestructura y operaciones</span><span class="sxs-lookup"><span data-stu-id="e46bf-111">Infrastructure and operations</span></span>
* <span data-ttu-id="e46bf-112">Aislamiento de administrador y usuario [portales](azure-stack-manage-portals.md) y las API proporcionan una seguridad mejorada.</span><span class="sxs-lookup"><span data-stu-id="e46bf-112">Isolated administrator and user [portals](azure-stack-manage-portals.md) and APIs provide enhanced security.</span></span>
* <span data-ttu-id="e46bf-113">Utilice la funcionalidad de administración de infraestructura mejorada, por ejemplo, alertar mejorada.</span><span class="sxs-lookup"><span data-stu-id="e46bf-113">Use enhanced infrastructure management functionality, such as improved alerting.</span></span>
* <span data-ttu-id="e46bf-114">Mediante el [conector de Windows Azure Pack](azure-stack-manage-windows-azure-pack.md), puede ver y administrar máquinas virtuales de IaaS que se hospedan en el paquete de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="e46bf-114">Using the [Windows Azure Pack Connector](azure-stack-manage-windows-azure-pack.md), you can view and manage IaaS virtual machines that are hosted on Windows Azure Pack.</span></span> <span data-ttu-id="e46bf-115">Para obtener esta versión preliminar, pruebe este escenario solo en entornos de prueba (paquete de Windows Azure y Azure pila).</span><span class="sxs-lookup"><span data-stu-id="e46bf-115">For this preview release, try this scenario only in test environments (both Windows Azure Pack and Azure Stack).</span></span> <span data-ttu-id="e46bf-116">Se requiere configuración adicional.</span><span class="sxs-lookup"><span data-stu-id="e46bf-116">Additional configuration is required.</span></span>
* <span data-ttu-id="e46bf-117">Azure admite ahora de pila [multiempresa](azure-stack-enable-multitenancy.md) para escenarios donde es necesario para proporcionar servicios IaaS y PaaS a los usuarios fuera de su dominio de Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="e46bf-117">Azure Stack now supports [multi-tenancy](azure-stack-enable-multitenancy.md) for scenarios where you need to provide IaaS and PaaS services to users outside of your Azure Active Directory domain.</span></span>  <span data-ttu-id="e46bf-118">Por ejemplo, puede que desee proporcionar servicios de Azure pila a una empresa asociada mediante sus identidades.</span><span class="sxs-lookup"><span data-stu-id="e46bf-118">For example, you may want to provide Azure Stack services to a partner company using their identities.</span></span> <span data-ttu-id="e46bf-119">Puede configurar la pila de Azure para que confíe en las identidades de la otra organización y permitir a los usuarios de dicha organización registrarse para suscripciones y consumir servicios.</span><span class="sxs-lookup"><span data-stu-id="e46bf-119">You can configure Azure Stack to trust the other organization's identities, and enable users from that organization to sign up for subscriptions and consume services.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e46bf-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e46bf-120">Next steps</span></span>
* [<span data-ttu-id="e46bf-121">Comprender la arquitectura de prueba de concepto de pila de Azure</span><span class="sxs-lookup"><span data-stu-id="e46bf-121">Understand Azure Stack POC architecture</span></span>](azure-stack-architecture.md)      
* [<span data-ttu-id="e46bf-122">Comprender los requisitos previos de implementación</span><span class="sxs-lookup"><span data-stu-id="e46bf-122">Understand deployment prerequisites</span></span>](azure-stack-deploy.md)
* [<span data-ttu-id="e46bf-123">Implementación de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e46bf-123">Deploy Azure Stack</span></span>](azure-stack-run-powershell-script.md)

