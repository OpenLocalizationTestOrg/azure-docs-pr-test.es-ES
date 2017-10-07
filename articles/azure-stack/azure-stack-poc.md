---
title: "¿aaaWhat es la pila de Azure? | Microsoft Docs"
description: "Azure Stack Development Kit es un entorno para evaluar las características y los escenarios de Azure Stack."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: helaw
ms.custom: mvc
ms.openlocfilehash: 3f7c84f2302a6411f49a07de171501fbd72812e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-stack"></a><span data-ttu-id="24c25-104">¿Qué es Azure Stack?</span><span class="sxs-lookup"><span data-stu-id="24c25-104">What is Azure Stack?</span></span>

<span data-ttu-id="24c25-105">Microsoft Azure Stack es una plataforma en la nube híbrida que le permite proporcionar servicios de Azure desde el centro de datos de la organización.</span><span class="sxs-lookup"><span data-stu-id="24c25-105">Microsoft Azure Stack is a hybrid cloud platform that lets you deliver Azure services from your organization’s datacenter.</span></span>  <span data-ttu-id="24c25-106">Pila de Azure es toohelp diseñado en escenarios clave, al igual que cumpla los requisitos de seguridad y cumplimiento de normas, o en las que necesite tooaccess recursos de Azure sin conectividad a internet.</span><span class="sxs-lookup"><span data-stu-id="24c25-106">Azure Stack is designed toohelp you in key scenarios, like meeting security and compliance requirements, or where you need tooaccess Azure resources without internet connectivity.</span></span>  

## <a name="azure-stack-development-kit"></a><span data-ttu-id="24c25-107">Azure Stack Development Kit</span><span class="sxs-lookup"><span data-stu-id="24c25-107">Azure Stack Development Kit</span></span>
<span data-ttu-id="24c25-108">Kit de desarrollo de pila de Microsoft Azure es una versión de un único nodo de pila de Azure, que puede usar tooevaluate y obtener información sobre la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="24c25-108">Microsoft Azure Stack Development Kit is a single-node version of Azure Stack, which you can use tooevaluate and learn about Azure Stack.</span></span>  <span data-ttu-id="24c25-109">También puede utilizar Azure Stack Development Kit como entorno de desarrollo, donde puede desarrollar con API y herramientas coherentes.</span><span class="sxs-lookup"><span data-stu-id="24c25-109">You can also use Azure Stack Development Kit as a developer environment, where you can develop using consistent APIs and tooling.</span></span>  

<span data-ttu-id="24c25-110">Debe tener en cuenta estos aspectos con Azure Stack Development Kit:</span><span class="sxs-lookup"><span data-stu-id="24c25-110">You should be aware of these points with Azure Stack Development Kit:</span></span>

* <span data-ttu-id="24c25-111">Azure Stack Development Kit no se debe usar como entorno de producción y solo debe emplearse para pruebas, evaluación y demostración.</span><span class="sxs-lookup"><span data-stu-id="24c25-111">Azure Stack Development Kit must not be used as a production environment and should only be used for testing, evaluation, and demonstration.</span></span>  
* <span data-ttu-id="24c25-112">La implementación de Azure Stack está asociada a un único proveedor de identidades de Azure Active Directory o Servicios de federación de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="24c25-112">Your deployment of Azure Stack is associated with a single Azure Active Directory or Active Directory Federation Services identity provider.</span></span> <span data-ttu-id="24c25-113">Puede crear varios usuarios en este directorio y asignar a suscripciones tooeach usuario.</span><span class="sxs-lookup"><span data-stu-id="24c25-113">You can create multiple users in this directory and assign subscriptions tooeach user.</span></span>
* <span data-ttu-id="24c25-114">Con todos los componentes implementados en la máquina único hello, hay limita los recursos físicos disponibles para recursos de inquilinos.</span><span class="sxs-lookup"><span data-stu-id="24c25-114">With all components deployed on hello single machine, there are limited physical resources available for tenant resources.</span></span> <span data-ttu-id="24c25-115">Esta configuración no está pensada para la evaluación del rendimiento o la escala.</span><span class="sxs-lookup"><span data-stu-id="24c25-115">This configuration is not intended for scale or performance evaluation.</span></span>
* <span data-ttu-id="24c25-116">Escenarios de redes están limitados debido requisito de NIC de host único/toohello.</span><span class="sxs-lookup"><span data-stu-id="24c25-116">Networking scenarios are limited due toohello single host/NIC requirement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24c25-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="24c25-117">Next steps</span></span>
[<span data-ttu-id="24c25-118">Características y conceptos principales</span><span class="sxs-lookup"><span data-stu-id="24c25-118">Key features and concepts</span></span>](azure-stack-key-features.md)

[<span data-ttu-id="24c25-119">Innovación de aplicaciones híbridas con Azure y Azure Stack (pdf)</span><span class="sxs-lookup"><span data-stu-id="24c25-119">Hybrid Application innovation with Azure and Azure Stack (pdf)</span></span>](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409)

