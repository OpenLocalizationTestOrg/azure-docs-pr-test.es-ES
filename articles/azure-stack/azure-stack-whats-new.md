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
# <a name="whats-new-in-azure-stack"></a>Novedades de la pila de Azure
Esta versión proporciona nuevas características para los inquilinos y los administradores.

## <a name="content-services-and-tools"></a>Contenido, servicios y herramientas
* [Los servicios de federación de Active Directory (AD FS)](azure-stack-key-features.md#identity) soporte técnico proporciona opciones de identidad para escenarios donde la conectividad de red es limitado o intermitente.
* Puede utilizar conjuntos de escalas de máquina Virtual de Azure para proporcionar escalabilidad administrado y escala de cargas de trabajo basadas en VM de IaaS. 
* Usar tamaños de máquinas virtuales de serie D de Azure para lograr coherencia y aumentar el rendimiento.
* Implementar y crear plantillas con discos de Temp que sean coherentes con Azure.
* [Distribución de Marketplace](azure-stack-download-azure-marketplace-item.md) le permite usar el contenido de Azure Marketplace y que estén disponibles en la pila de Azure.

## <a name="infrastructure-and-operations"></a>Infraestructura y operaciones
* Aislamiento de administrador y usuario [portales](azure-stack-manage-portals.md) y las API proporcionan una seguridad mejorada.
* Utilice la funcionalidad de administración de infraestructura mejorada, por ejemplo, alertar mejorada.
* Mediante el [conector de Windows Azure Pack](azure-stack-manage-windows-azure-pack.md), puede ver y administrar máquinas virtuales de IaaS que se hospedan en el paquete de Windows Azure. Para obtener esta versión preliminar, pruebe este escenario solo en entornos de prueba (paquete de Windows Azure y Azure pila). Se requiere configuración adicional.
* Azure admite ahora de pila [multiempresa](azure-stack-enable-multitenancy.md) para escenarios donde es necesario para proporcionar servicios IaaS y PaaS a los usuarios fuera de su dominio de Active Directory de Azure.  Por ejemplo, puede que desee proporcionar servicios de Azure pila a una empresa asociada mediante sus identidades. Puede configurar la pila de Azure para que confíe en las identidades de la otra organización y permitir a los usuarios de dicha organización registrarse para suscripciones y consumir servicios.  

## <a name="next-steps"></a>Pasos siguientes
* [Comprender la arquitectura de prueba de concepto de pila de Azure](azure-stack-architecture.md)      
* [Comprender los requisitos previos de implementación](azure-stack-deploy.md)
* [Implementación de Azure Stack](azure-stack-run-powershell-script.md)

