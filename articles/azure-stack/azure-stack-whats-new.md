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
# <a name="whats-new-in-azure-stack"></a>Novedades de la pila de Azure
Esta versión proporciona nuevas características para los inquilinos y los administradores.

## <a name="content-services-and-tools"></a>Contenido, servicios y herramientas
* [Los servicios de federación de Active Directory (AD FS)](azure-stack-key-features.md#identity) soporte técnico proporciona opciones de identidad para escenarios donde la conectividad de red es limitado o intermitente.
* Puede usar conjuntos de escalas de máquina Virtual de Azure tooprovide administrado escalabilidad y escala de cargas de trabajo basadas en VM de IaaS. 
* Usar tamaños de máquinas virtuales de serie D de Azure para lograr coherencia y aumentar el rendimiento.
* Implementar y crear plantillas con discos de Temp que sean coherentes con Azure.
* [Distribución de Marketplace](azure-stack-download-azure-marketplace-item.md) permite contenido toouse de hello Azure Marketplace y que estén disponibles en la pila de Azure.

## <a name="infrastructure-and-operations"></a>Infraestructura y operaciones
* Aislamiento de administrador y usuario [portales](azure-stack-manage-portals.md) y las API proporcionan una seguridad mejorada.
* Utilice la funcionalidad de administración de infraestructura mejorada, por ejemplo, alertar mejorada.
* Con hello [conector de Windows Azure Pack](azure-stack-manage-windows-azure-pack.md), puede ver y administrar máquinas virtuales de IaaS que se hospedan en el paquete de Windows Azure. Para obtener esta versión preliminar, pruebe este escenario solo en entornos de prueba (paquete de Windows Azure y Azure pila). Se requiere configuración adicional.
* Azure admite ahora de pila [multiempresa](azure-stack-enable-multitenancy.md) para escenarios donde es necesario tooprovide IaaS y PaaS servicios toousers fuera de su dominio de Active Directory de Azure.  Por ejemplo, puede que desee tooprovide Azure pila servicios tooa empresa mediante sus identidades. Puede configurar Hola de pila de Azure tootrust identidades de la otra organización y permiten a los usuarios de ese toosign de organización para las suscripciones y consumir los servicios.  

## <a name="next-steps"></a>Pasos siguientes
* [Comprender la arquitectura de prueba de concepto de pila de Azure](azure-stack-architecture.md)      
* [Comprender los requisitos previos de implementación](azure-stack-deploy.md)
* [Implementación de Azure Stack](azure-stack-run-powershell-script.md)

