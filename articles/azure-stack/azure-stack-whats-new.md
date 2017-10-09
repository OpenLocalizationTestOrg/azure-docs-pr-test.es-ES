---
title: aaaWhat de nuevo en la pila de Azure | Documentos de Microsoft
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
ms.openlocfilehash: 32b4bd7deebb12a92e4abbdaacdbcebaa5125e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="whats-new-in-azure-stack"></a><span data-ttu-id="8eaf0-103">Novedades de la pila de Azure</span><span class="sxs-lookup"><span data-stu-id="8eaf0-103">What's new in Azure Stack</span></span>
<span data-ttu-id="8eaf0-104">Esta versión proporciona nuevas características para los inquilinos y los administradores.</span><span class="sxs-lookup"><span data-stu-id="8eaf0-104">This release provides new features for both tenants and administrators.</span></span>

## <a name="content-services-and-tools"></a><span data-ttu-id="8eaf0-105">Contenido, servicios y herramientas</span><span class="sxs-lookup"><span data-stu-id="8eaf0-105">Content, services, and tools</span></span>
* <span data-ttu-id="8eaf0-106">[Los servicios de federación de Active Directory (AD FS)](azure-stack-key-features.md#identity) soporte técnico proporciona opciones de identidad para escenarios donde la conectividad de red es limitado o intermitente.</span><span class="sxs-lookup"><span data-stu-id="8eaf0-106">[Active Directory Federation Services (AD FS)](azure-stack-key-features.md#identity) support provides identity options for scenarios where network connectivity is limited or intermittent.</span></span>
* <span data-ttu-id="8eaf0-107">Puede usar conjuntos de escalas de máquina Virtual de Azure tooprovide administrado escalabilidad y escala de cargas de trabajo basadas en VM de IaaS.</span><span class="sxs-lookup"><span data-stu-id="8eaf0-107">You can use Azure Virtual Machine Scale Sets tooprovide managed scale-out and scale-in of IaaS VM-based workloads.</span></span> 
* <span data-ttu-id="8eaf0-108">Usar tamaños de máquinas virtuales de serie D de Azure para lograr coherencia y aumentar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="8eaf0-108">Use Azure D-Series VM sizes for increased performance and consistency.</span></span>
* <span data-ttu-id="8eaf0-109">Implementar y crear plantillas con discos de Temp que sean coherentes con Azure.</span><span class="sxs-lookup"><span data-stu-id="8eaf0-109">Deploy and create templates with Temp Disks that are consistent with Azure.</span></span>
* <span data-ttu-id="8eaf0-110">[Distribución de Marketplace](azure-stack-download-azure-marketplace-item.md) permite contenido toouse de hello Azure Marketplace y que estén disponibles en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="8eaf0-110">[Marketplace Syndication](azure-stack-download-azure-marketplace-item.md) allows you toouse content from hello Azure Marketplace and make available in Azure Stack.</span></span>

## <a name="infrastructure-and-operations"></a><span data-ttu-id="8eaf0-111">Infraestructura y operaciones</span><span class="sxs-lookup"><span data-stu-id="8eaf0-111">Infrastructure and operations</span></span>
* <span data-ttu-id="8eaf0-112">Aislamiento de administrador y usuario [portales](azure-stack-manage-portals.md) y las API proporcionan una seguridad mejorada.</span><span class="sxs-lookup"><span data-stu-id="8eaf0-112">Isolated administrator and user [portals](azure-stack-manage-portals.md) and APIs provide enhanced security.</span></span>
* <span data-ttu-id="8eaf0-113">Utilice la funcionalidad de administración de infraestructura mejorada, por ejemplo, alertar mejorada.</span><span class="sxs-lookup"><span data-stu-id="8eaf0-113">Use enhanced infrastructure management functionality, such as improved alerting.</span></span>
* <span data-ttu-id="8eaf0-114">Con hello [conector de Windows Azure Pack](azure-stack-manage-windows-azure-pack.md), puede ver y administrar máquinas virtuales de IaaS que se hospedan en el paquete de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="8eaf0-114">Using hello [Windows Azure Pack Connector](azure-stack-manage-windows-azure-pack.md), you can view and manage IaaS virtual machines that are hosted on Windows Azure Pack.</span></span> <span data-ttu-id="8eaf0-115">Para obtener esta versión preliminar, pruebe este escenario solo en entornos de prueba (paquete de Windows Azure y Azure pila).</span><span class="sxs-lookup"><span data-stu-id="8eaf0-115">For this preview release, try this scenario only in test environments (both Windows Azure Pack and Azure Stack).</span></span> <span data-ttu-id="8eaf0-116">Se requiere configuración adicional.</span><span class="sxs-lookup"><span data-stu-id="8eaf0-116">Additional configuration is required.</span></span>
* <span data-ttu-id="8eaf0-117">Azure admite ahora de pila [multiempresa](azure-stack-enable-multitenancy.md) para escenarios donde es necesario tooprovide IaaS y PaaS servicios toousers fuera de su dominio de Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="8eaf0-117">Azure Stack now supports [multi-tenancy](azure-stack-enable-multitenancy.md) for scenarios where you need tooprovide IaaS and PaaS services toousers outside of your Azure Active Directory domain.</span></span>  <span data-ttu-id="8eaf0-118">Por ejemplo, puede que desee tooprovide Azure pila servicios tooa empresa mediante sus identidades.</span><span class="sxs-lookup"><span data-stu-id="8eaf0-118">For example, you may want tooprovide Azure Stack services tooa partner company using their identities.</span></span> <span data-ttu-id="8eaf0-119">Puede configurar Hola de pila de Azure tootrust identidades de la otra organización y permiten a los usuarios de ese toosign de organización para las suscripciones y consumir los servicios.</span><span class="sxs-lookup"><span data-stu-id="8eaf0-119">You can configure Azure Stack tootrust hello other organization's identities, and enable users from that organization toosign up for subscriptions and consume services.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="8eaf0-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8eaf0-120">Next steps</span></span>
* [<span data-ttu-id="8eaf0-121">Comprender la arquitectura de prueba de concepto de pila de Azure</span><span class="sxs-lookup"><span data-stu-id="8eaf0-121">Understand Azure Stack POC architecture</span></span>](azure-stack-architecture.md)      
* [<span data-ttu-id="8eaf0-122">Comprender los requisitos previos de implementación</span><span class="sxs-lookup"><span data-stu-id="8eaf0-122">Understand deployment prerequisites</span></span>](azure-stack-deploy.md)
* [<span data-ttu-id="8eaf0-123">Implementación de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8eaf0-123">Deploy Azure Stack</span></span>](azure-stack-run-powershell-script.md)

