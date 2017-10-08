---
title: aaaFinding no administrada de aplicaciones en la nube con Cloud App Discovery | Documentos de Microsoft
description: "Proporciona información sobre cómo buscar y administrar aplicaciones con Cloud App Discovery, ¿cuáles son las ventajas de Hola y cómo funciona."
services: active-directory
keywords: cloud app discovery, administrar aplicaciones
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a>Búsqueda de aplicaciones de nube no administradas con Cloud App Discovery
## <a name="overview"></a>Información general
En las empresas modernas, los departamentos de TI a menudo no son conscientes de las aplicaciones de nube de Hola que los miembros de su organización utilizan toodo su trabajo. Es fácil toosee ¿por qué los administradores tendrían preocupado datos toocorporate de acceso no autorizado, posible pérdida de datos y otros riesgos de seguridad. Esta falta de conciencia puede hacer que un plan para tratar estos riesgos de seguridad parezca abrumador.

Cloud App Discovery es una característica de Premium de Azure Active Directory (AD) que permite que las aplicaciones de nube toodiscover que se utilizan los usuarios de hello en su organización.

**Con Cloud App Discovery, puede:**

* Buscar aplicaciones que se va a usar en la nube de Hola y medir ese uso por número de usuarios, volumen de tráfico o número de aplicación de toohello de las solicitudes web.
* Identificar a los usuarios de Hola que usan una aplicación.
* Exporte datos para análisis sin conexión.
* Lleve estas aplicaciones bajo el control de TI y habilite el inicio de sesión único para la administración de usuarios.

## <a name="how-it-works"></a>Cómo funciona
1. Los agentes de uso de aplicaciones se instalan en los equipos de los usuarios.
2. información de uso de aplicación Hola capturada los agentes de Hola se envía a través de un servicio de detección de aplicaciones de canal seguro y cifrado toohello en la nube.
3. Hola servicio Cloud App Discovery evalúa los datos de Hola y genera informes.

![Diagrama de Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

tooget a trabajar con Cloud App Discovery, vea [introducción con Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)

## <a name="related-articles"></a>Artículos relacionados
* [Consideraciones de seguridad y privacidad de Cloud App Discovery](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [Guía de implementación de la directiva de grupo de Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [Guía de implementación de System Center de Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [Configuración del registro de Cloud App Discovery para servidores proxy con puertos personalizados](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [Registro de cambios del agente de Cloud App Discovery ](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [Preguntas más frecuentes de Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)

