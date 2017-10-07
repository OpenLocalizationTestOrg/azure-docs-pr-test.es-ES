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
# <a name="develop-for-azure-stack"></a>Desarrollo para Azure Stack
Puede empezar a desarrollar aplicaciones de hoy en día, incluso si no tienes entorno de acceso tooan pila de Azure. Dado que la pila de Azure proporciona servicios de Microsoft Azure que se ejecutan en el centro de datos, puede usar toodevelop herramientas y procesos similar en la pila de Azure como lo haría con Azure.  Con un poco de preparación y la orientación de hello temas siguientes, puede usar Azure tooemulate un entorno de pila de Azure:

* En Azure, puede crear plantillas de Azure Resource Manager también puede implementar tooAzure pila.  Vea [consideraciones de la plantilla](azure-stack-develop-templates.md) para obtener instrucciones sobre el desarrollo de su portabilidad de tooensure de plantillas.
* Existe una diferencia entre la disponibilidad y la versión del servicio entre Azure y Azure Stack. Puede usar hello [módulo de directivas de la pila de Azure](azure-stack-policy-module.md) toowhat de tipos de recursos y la disponibilidad del servicio de Azure toorestrict del disponible en la pila de Azure. Si se restringen los servicios disponibles le ayudará a su aplicación dependen de los servicios disponibles tooAzure pila.
* Hola [plantillas de inicio rápido de Azure pila](https://github.com/Azure/AzureStack-QuickStart-Templates) son ejemplos de escenarios comunes de cómo toodevelop las plantillas, para que puedan implementan tooboth Azure y la pila de Azure.


