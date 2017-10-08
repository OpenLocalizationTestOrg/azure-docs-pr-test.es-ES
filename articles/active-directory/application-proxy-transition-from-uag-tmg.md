---
title: "aaaUpgrade tooAzure AD Proxy de aplicación | Documentos de Microsoft"
description: "Elija qué solución de proxy es la mejor si va a actualizar desde Microsoft Forefront o Unified Access Gateway."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7dc2633140b384e25792470dadbb7f3fa7992a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="compare-remote-access-solutions"></a>Comparación de soluciones de acceso remoto

El proxy de aplicación de Azure Active Directory es una de las dos soluciones de acceso remoto que Microsoft ofrece. Hola otro es Proxy de aplicación Web, versión de Hola local. Estas dos soluciones reemplazan a los productos anteriores que ofrecía Microsoft: Microsoft Forefront Threat Management Gateway (TMG) y Unified Access Gateway (UAG). Use este artículo toounderstand cómo comparan estos cuatro soluciones tooeach otro. Para las personas que aún utilicen hello en desuso soluciones TMG o UAG, use este plan de artículo toohelp su tooone de migración de hello Proxy de aplicación. 


## <a name="feature-comparison"></a>Comparación de características

Use esta tabla toounderstand cómo Threat Management Gateway (TMG), Unified Access Gateway (UAG), Proxy de aplicación Web (WAP) y Proxy de aplicación de Azure AD (AP) comparan tooeach otro.

| Característica | TMG | UAG | WAP | AP |
| ------- | --- | --- | --- | --- |
| Autenticación de certificados | Sí | Sí | - | - |
| Publicar de forma selectiva las aplicaciones de explorador | Sí | Sí | Sí | Sí |
| Autenticación previa e inicio de sesión único | Sí | Sí | Sí | Sí | 
| Firewall de capa 2/3 | Sí | Sí | - | - |
| Funcionalidades de proxy de reenvío | Sí | - | - | - |
| Funcionalidades de VPN | Sí | Sí | - | - |
| Amplia compatibilidad con protocolos | - | Sí | Sí, si se ejecuta a través de HTTP | Sí, si ejecuta a través de HTTP o a través de Puerta de enlace de escritorio remoto |
| Actúa como servidor proxy ADFS | - | Sí | Sí | - |
| Un portal para el acceso a las aplicaciones | - | Sí | - | Sí |
| Traducción de vínculos del cuerpo de respuesta | Sí | Sí | - | Sí | 
| Autenticación con encabezados | - | Sí | - | Sí, con PingAccess | 
| Seguridad de escala en la nube | - | - | - | Sí | 
| Acceso condicional | - | Sí | - | Sí |
| Ningún componente de zona de hello desmilitarizada (DMZ) | - | - | - | Sí |
| No hay conexiones entrantes | - | - | - | Sí |

Para la mayoría de los escenarios, se recomienda aplicación de Azure AD como solución moderna Hola. Web Application Proxy solo se prefiere en los escenarios que requieran un servidor proxy para AD FS y no pueda usar dominios personalizados en Azure Active Directory. 

El Proxy de aplicación de Azure AD ofrece ventajas único cuando compara toosimilar productos, incluido:

- Extensión de recursos de Azure AD local tooon
   - Seguridad y protección de escala en la nube
   - Características como el acceso condicional y la autenticación multifactor son tooenable fácil
- Ningún componente de zona desmilitarizada de Hola
- No se requieren conexiones entrantes
- Panel de un acceso de manera que los usuarios pueden ir toofor todas sus aplicaciones, incluido Office 365, Azure AD integrado aplicaciones SaaS, y en sus instalaciones de aplicaciones web. 


## <a name="next-steps"></a>Pasos siguientes

- [Usar aplicaciones tooon local de aplicación de Azure AD tooprovide el acceso remoto seguro](active-directory-application-proxy-get-started.md)
- [Transición de Forefront TMG y UAG tooApplication Proxy](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/).
