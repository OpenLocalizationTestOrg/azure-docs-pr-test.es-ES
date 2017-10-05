---
title: Desarrollo de aplicaciones para Azure Stack | Microsoft Docs
description: "Obtenga información acerca de las consideraciones a la hora de desarrollar prototipos de aplicaciones en Azure Stack"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d3ebc6b1-0ffe-4d3e-ba4a-388239d6cdc3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 28bca0c94e88b31012c4c53ace47d8bfe6cbe163
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-stack"></a><span data-ttu-id="bcb2e-103">Desarrollo para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="bcb2e-103">Develop for Azure Stack</span></span>
<span data-ttu-id="bcb2e-104">Puede empezar a desarrollar aplicaciones hoy mismo, incluso si no tiene acceso a un entorno de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="bcb2e-104">You can get started developing applications today, even if you don't have access to an Azure Stack environment.</span></span> <span data-ttu-id="bcb2e-105">Dado que Azure Stack proporciona servicios de Microsoft Azure que se ejecutan en el centro de datos, puede usar herramientas y procesos similares para desarrollar con Azure Stack tal como lo haría con Azure.</span><span class="sxs-lookup"><span data-stu-id="bcb2e-105">Because Azure Stack delivers Microsoft Azure services that run in your datacenter, you can use similar tools and processes to develop against Azure Stack as you would with Azure.</span></span>  <span data-ttu-id="bcb2e-106">Con un poco de preparación y la orientación que le proporcionarán los siguientes temas, puede usar Azure para emular un entorno de Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="bcb2e-106">With a bit of preparation and guidance from the following topics, you can use Azure to emulate an Azure Stack environment:</span></span>

* <span data-ttu-id="bcb2e-107">En Azure, puede crear plantillas de Azure Resource Manager que también se pueden implementar en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="bcb2e-107">In Azure, you can create Azure Resource Manager templates that are also deployable to Azure Stack.</span></span>  <span data-ttu-id="bcb2e-108">Consulte el artículo [template considerations](azure-stack-develop-templates.md) (consideraciones de las plantillas) para obtener ayuda acerca de cómo desarrollar las plantillas para garantizar la portabilidad.</span><span class="sxs-lookup"><span data-stu-id="bcb2e-108">See [template considerations](azure-stack-develop-templates.md) for guidance on developing your templates to ensure portability.</span></span>
* <span data-ttu-id="bcb2e-109">Existe una diferencia entre la disponibilidad y la versión del servicio entre Azure y Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="bcb2e-109">There is a delta in service availability and service versioning between Azure and Azure Stack.</span></span> <span data-ttu-id="bcb2e-110">Puede usar el [módulo de directivas de Azure Stack](azure-stack-policy-module.md) para restringir los tipos de recursos y la disponibilidad del servicio de Azure a fin de adaptarlos a la disponibilidad de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="bcb2e-110">You can use the [Azure Stack policy module](azure-stack-policy-module.md) to restrict Azure service availability and resource types to what's available in Azure Stack.</span></span> <span data-ttu-id="bcb2e-111">La restricción de los servicios disponibles permitirá que su aplicación se base en los servicios disponibles de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="bcb2e-111">Constraining available services will help your application rely on services available to Azure Stack.</span></span>
* <span data-ttu-id="bcb2e-112">Las [plantillas de inicio rápido de Azure Stack](https://github.com/Azure/AzureStack-QuickStart-Templates) son ejemplos comunes de escenarios acerca de cómo desarrollar las plantillas para que se puedan implementar en Azure y en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="bcb2e-112">The [Azure Stack Quickstart Templates](https://github.com/Azure/AzureStack-QuickStart-Templates) are common scenario examples of how to develop your templates so they can be deployed to both Azure and Azure Stack.</span></span>


