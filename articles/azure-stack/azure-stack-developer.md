---
title: aplicaciones de aaaDevelop para la pila de Azure | Documentos de Microsoft
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
ms.openlocfilehash: 9bea75d0f0ecf19c05ff55ac3ef4e778d53a1912
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-stack"></a><span data-ttu-id="b24f6-103">Desarrollo para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b24f6-103">Develop for Azure Stack</span></span>
<span data-ttu-id="b24f6-104">Puede empezar a desarrollar aplicaciones de hoy en día, incluso si no tienes entorno de acceso tooan pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="b24f6-104">You can get started developing applications today, even if you don't have access tooan Azure Stack environment.</span></span> <span data-ttu-id="b24f6-105">Dado que la pila de Azure proporciona servicios de Microsoft Azure que se ejecutan en el centro de datos, puede usar toodevelop herramientas y procesos similar en la pila de Azure como lo haría con Azure.</span><span class="sxs-lookup"><span data-stu-id="b24f6-105">Because Azure Stack delivers Microsoft Azure services that run in your datacenter, you can use similar tools and processes toodevelop against Azure Stack as you would with Azure.</span></span>  <span data-ttu-id="b24f6-106">Con un poco de preparación y la orientación de hello temas siguientes, puede usar Azure tooemulate un entorno de pila de Azure:</span><span class="sxs-lookup"><span data-stu-id="b24f6-106">With a bit of preparation and guidance from hello following topics, you can use Azure tooemulate an Azure Stack environment:</span></span>

* <span data-ttu-id="b24f6-107">En Azure, puede crear plantillas de Azure Resource Manager también puede implementar tooAzure pila.</span><span class="sxs-lookup"><span data-stu-id="b24f6-107">In Azure, you can create Azure Resource Manager templates that are also deployable tooAzure Stack.</span></span>  <span data-ttu-id="b24f6-108">Vea [consideraciones de la plantilla](azure-stack-develop-templates.md) para obtener instrucciones sobre el desarrollo de su portabilidad de tooensure de plantillas.</span><span class="sxs-lookup"><span data-stu-id="b24f6-108">See [template considerations](azure-stack-develop-templates.md) for guidance on developing your templates tooensure portability.</span></span>
* <span data-ttu-id="b24f6-109">Existe una diferencia entre la disponibilidad y la versión del servicio entre Azure y Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b24f6-109">There is a delta in service availability and service versioning between Azure and Azure Stack.</span></span> <span data-ttu-id="b24f6-110">Puede usar hello [módulo de directivas de la pila de Azure](azure-stack-policy-module.md) toowhat de tipos de recursos y la disponibilidad del servicio de Azure toorestrict del disponible en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="b24f6-110">You can use hello [Azure Stack policy module](azure-stack-policy-module.md) toorestrict Azure service availability and resource types toowhat's available in Azure Stack.</span></span> <span data-ttu-id="b24f6-111">Si se restringen los servicios disponibles le ayudará a su aplicación dependen de los servicios disponibles tooAzure pila.</span><span class="sxs-lookup"><span data-stu-id="b24f6-111">Constraining available services will help your application rely on services available tooAzure Stack.</span></span>
* <span data-ttu-id="b24f6-112">Hola [plantillas de inicio rápido de Azure pila](https://github.com/Azure/AzureStack-QuickStart-Templates) son ejemplos de escenarios comunes de cómo toodevelop las plantillas, para que puedan implementan tooboth Azure y la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="b24f6-112">hello [Azure Stack Quickstart Templates](https://github.com/Azure/AzureStack-QuickStart-Templates) are common scenario examples of how toodevelop your templates so they can be deployed tooboth Azure and Azure Stack.</span></span>


