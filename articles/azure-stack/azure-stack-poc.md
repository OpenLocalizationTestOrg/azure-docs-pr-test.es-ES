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
# <a name="what-is-azure-stack"></a>¿Qué es Azure Stack?

Microsoft Azure Stack es una plataforma en la nube híbrida que le permite proporcionar servicios de Azure desde el centro de datos de la organización.  Pila de Azure es toohelp diseñado en escenarios clave, al igual que cumpla los requisitos de seguridad y cumplimiento de normas, o en las que necesite tooaccess recursos de Azure sin conectividad a internet.  

## <a name="azure-stack-development-kit"></a>Azure Stack Development Kit
Kit de desarrollo de pila de Microsoft Azure es una versión de un único nodo de pila de Azure, que puede usar tooevaluate y obtener información sobre la pila de Azure.  También puede utilizar Azure Stack Development Kit como entorno de desarrollo, donde puede desarrollar con API y herramientas coherentes.  

Debe tener en cuenta estos aspectos con Azure Stack Development Kit:

* Azure Stack Development Kit no se debe usar como entorno de producción y solo debe emplearse para pruebas, evaluación y demostración.  
* La implementación de Azure Stack está asociada a un único proveedor de identidades de Azure Active Directory o Servicios de federación de Active Directory. Puede crear varios usuarios en este directorio y asignar a suscripciones tooeach usuario.
* Con todos los componentes implementados en la máquina único hello, hay limita los recursos físicos disponibles para recursos de inquilinos. Esta configuración no está pensada para la evaluación del rendimiento o la escala.
* Escenarios de redes están limitados debido requisito de NIC de host único/toohello.

## <a name="next-steps"></a>Pasos siguientes
[Características y conceptos principales](azure-stack-key-features.md)

[Innovación de aplicaciones híbridas con Azure y Azure Stack (pdf)](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409)

