---
title: "¿Qué es Azure Stack? | Microsoft Docs"
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
ms.openlocfilehash: 65278e7b352df5651f04151210ccc34a58dd321a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-azure-stack"></a>¿Qué es Azure Stack?

Microsoft Azure Stack es una plataforma en la nube híbrida que le permite proporcionar servicios de Azure desde el centro de datos de la organización.  Azure Stack se ha diseñado para ayudarle en escenarios clave, como cumplir los requisitos de seguridad y de cumplimiento, o si necesita tener acceso a recursos de Azure sin conectividad a Internet.  

## <a name="azure-stack-development-kit"></a>Azure Stack Development Kit
Microsoft Azure Stack Development Kit es una versión de nodo único de Azure Stack que puede usar para evaluar y conocer Azure Stack.  También puede utilizar Azure Stack Development Kit como entorno de desarrollo, donde puede desarrollar con API y herramientas coherentes.  

Debe tener en cuenta estos aspectos con Azure Stack Development Kit:

* Azure Stack Development Kit no se debe usar como entorno de producción y solo debe emplearse para pruebas, evaluación y demostración.  
* La implementación de Azure Stack está asociada a un único proveedor de identidades de Azure Active Directory o Servicios de federación de Active Directory. Puede crear varios usuarios en este directorio y asignar las suscripciones a cada usuario.
* Con todos los componentes implementados en un solo equipo, hay recursos físicos limitados disponibles para los recursos de inquilinos. Esta configuración no está pensada para la evaluación del rendimiento o la escala.
* Los escenarios de redes están limitados debido al requisito de host/NIC única.

## <a name="next-steps"></a>Pasos siguientes
[Características y conceptos principales](azure-stack-key-features.md)

[Innovación de aplicaciones híbridas con Azure y Azure Stack (pdf)](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409)

