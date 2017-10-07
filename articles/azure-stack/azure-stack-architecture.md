---
title: aaaMicrosoft arquitectura del Kit de desarrollo de pila de Azure | Documentos de Microsoft
description: Hola vista arquitectura del Kit de desarrollo de pila de Microsoft Azure.
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a7e61ea4-be2f-4e55-9beb-7a079f348e05
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: helaw
ms.openlocfilehash: 32a19ced7ddd57b97ba796679c116132090402e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-stack-development-kit-architecture"></a>Arquitectura de Microsoft Azure Stack Development Kit
Hola Kit de desarrollo de pila de Azure es una implementación de un único nodo de pila de Azure. Todos los componentes de Hola se instalan en máquinas virtuales se ejecutan en una máquina de host único. 

## <a name="logical-architecture-diagram"></a>Diagrama de arquitectura lógica
Hello diagrama siguiente ilustra la arquitectura lógica de hello del kit de desarrollo de hello pila de Azure y sus componentes.

![](media/azure-stack-architecture/image1.png)

## <a name="virtual-machine-roles"></a>Roles de máquina virtual
Hola kit de desarrollo de la pila de Azure ofrece servicios mediante Hola siguiendo las máquinas virtuales en el host de hello:

| Nombre | Descripción |
| ----- | ----- |
| **AzS-ACS01** | Servicios de almacenamiento de Azure Stack.|
| **AzS-ADFS01** | Servicios de federación de Active Directory (AD FS).  |
| **AzS-BGPNAT01** | Enrutador perimetral que proporciona funcionalidades de NAT y VPN para Azure Stack. |
| **AzS-CA01** | Servicios de entidad de certificación para servicios de rol de Azure Stack.|
| **AzS-DC01** | Servicios de Active Directory, DNS y DHCP para Microsoft Azure Stack.|
| **AzS-ERCS01** | Máquina virtual de la consola de recuperación de emergencia. |
| **AzS-GWY01** | Servicios perimetrales de puerta de enlace, como las conexiones de sitio a sitio de VPN para redes de inquilinos.|
| **AzS-NC01** | Controladora de red, que administra los servicios de red de Azure Stack.  |
| **AzS-SLB01** | Servicios de multiplexor del equilibrio de carga en Azure Stack para los inquilinos y los servicios de infraestructura de Azure Stack.  |
| **AzS-SQL01** | Almacén de datos internos para los roles de infraestructura de Azure Stack.  |
| **AzS-WAS01** | Portal de administración de Azure Stack y servicios de Azure Resource Manager.|
| **AzS-WASP01**| Portal del usuario (inquilino) de Azure Stack y servicios de Azure Resource Manager.|
| **AzS-XRP01** | Controlador de administración de infraestructura para la pila de Microsoft Azure, incluidos los proveedores de recursos de proceso, red y almacenamiento de Hola.|


## <a name="next-steps"></a>Pasos siguientes
[Implementación de Azure Stack](azure-stack-deploy.md)

[Primera tootry escenarios](azure-stack-first-scenarios.md)

