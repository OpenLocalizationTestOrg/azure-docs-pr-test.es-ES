---
title: "Introducción a App Service: Azure Stack | Microsoft Docs"
description: "Introducción a App Service en Azure Stack"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: 1d763f592212b3a2dcc2f03ebe317eed84e9e2de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-on-azure-stack-overview"></a>Introducción a App Service en Azure Stack

Servicio de aplicaciones de Azure en la pila de Azure es hello Azure oferta poner tooAzure pila. Hola servicio de aplicaciones en el instalador de la pila de Azure crea Hola siguiendo el conjunto de instancias de rol:

*  Controller
*  Administración (se crean dos instancias)
*  FrontEnd
*  Publicador
*  Trabajo (en modo compartido)

Además, Hola servicio de aplicaciones en el instalador de la pila de Azure crea un servidor de archivos.
    
## <a name="whats-new-in-hello-first-release-candidate-of-app-service-on-azure-stack"></a>¿Novedades de hello primera versión release candidate de servicio de aplicaciones en la pila de Azure?
![Servicio de aplicaciones de portal de Azure pila Hola][1]

Hola primera versión release candidate de servicio de aplicaciones en la pila de Azure se basa en la vista previa terceros de Hola y aporta mejoras y nuevas funcionalidades:

* Azure Functions en entornos de Azure Stack basado en los Servicios de federación de Active Directory (AD FS) 
* Inicio de sesión único, soporte para el portal de funciones de Hola y Hola herramientas de desarrollo avanzadas (Kudu)
* Compatibilidad con Java para aplicaciones web, móviles y de API
* Administración de niveles de trabajo por la escala de máquinas virtuales establece tooimprove capacidades de escalabilidad horizontal para los administradores de servicios
* Localización de la experiencia de administración de Hola
* Mayor estabilidad del servicio de Hola
* Actualizaciones de la experiencia con el portal del inquilino y actualizaciones del proceso de instalación

## <a name="limitations-of-hello-technical-preview"></a>Limitaciones de vista previa técnica de Hola

No hay ninguna compatibilidad para Hola servicio de aplicaciones en versiones preliminares de pila de Azure, aunque se supervisará Hola foro de MSDN de pila de Azure. No se deben poner cargas de trabajo de producción en esta versión preliminar. Tampoco existen actualizaciones entre versiones preliminares de App Service en Azure Stack. Hello fines principales de estas versiones de vista previa son tooshow que ofrecemos también y tooobtain comentarios. 

## <a name="what-is-an-app-service-plan"></a>¿Qué es un plan de App Service?

Hola proveedor de recursos de servicio de aplicaciones usa Hola el mismo código que usa el servicio de aplicaciones de Azure. Como resultado, merece la pena describir algunos conceptos comunes. En el servicio de aplicaciones, Hola precios contenedor para las aplicaciones se denomina hello plan de servicio de aplicaciones. Representa conjunto de Hola de máquinas virtuales dedicadas usa toohold sus aplicaciones. Dentro de una suscripción determinada, pueden haber varios planes de App Service. 

En Azure, hay trabajados compartidos y dedicados. Un trabajo compartido admite el hospedaje de aplicaciones para varios inquilinos de alta densidad, y solo existe un conjunto de trabajos compartidos. Solo un inquilino usa los servidores dedicados que pueden ser de tres tamaños: pequeño, mediano y grande. necesidades de Hola de clientes local no se puede describir siempre mediante el uso de estos términos. En el servicio de aplicaciones en la pila de Azure, los administradores de proveedor de recursos pueden definir los niveles de trabajo Hola desean toomake disponible. Los administradores pueden definir varios conjuntos de trabajos compartidos o diferentes conjuntos de trabajos dedicados en función de sus necesidades únicas de hospedaje. Mediante el uso de esas definiciones de nivel de trabajo, pueden definir sus propias SKU de precios.

## <a name="portal-features"></a>Características del portal

Servicio de aplicaciones en la pila de Azure usa Hola terminar la misma interfaz de usuario que utiliza el servicio de aplicación de Azure, como ocurre con hello hacer una copia. Algunas características están deshabilitadas y no funcionan en Azure Stack. Hola expectativas específicas de Azure o servicios que requieren estas características aún no están disponibles en la pila de Azure. 

## <a name="next-steps"></a>Pasos siguientes

- [Antes de empezar a trabajar con App Service en Azure Stack](azure-stack-app-service-before-you-get-started.md)
- [Instalar Hola proveedor de recursos de servicio de aplicaciones](azure-stack-app-service-deploy.md)

También puede probar otros [plataforma como servicio (PaaS)](azure-stack-tools-paas-services.md), como hello [proveedor de recursos de SQL Server](azure-stack-sql-resource-provider-deploy.md) hello y [proveedor de recursos MySQL](azure-stack-mysql-resource-provider-deploy.md).

<!--Image references-->
[1]: ./media/azure-stack-app-service-overview/AppService_Portal.png
