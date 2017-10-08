---
title: aaaVulnerabilities detectado por Azure Active Directory Identity Protection | Documentos de Microsoft
description: "Información general de vulnerabilidades de hello detectadas por Azure Active Directory Identity Protection."
services: active-directory
keywords: "azure active directory identity protection, detección de aplicaciones en la nube, administración de aplicaciones, seguridad, riesgo, nivel de riesgo, punto vulnerable, directiva de seguridad"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a>Vulnerabilidades detectadas por Azure Active Directory Identity Protection
Los puntos vulnerables son puntos débiles de su entorno que pueden ser aprovechados por un atacante. Se recomienda que solucionar estos postura de seguridad de las vulnerabilidades tooimprove Hola de su organización y evitar que los atacantes aprovecharse de ellos.


![vulnerabilidades](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilidades")



Hello las secciones siguientes proporcionan una visión general de las vulnerabilidades de hello notificados por protección de identidad.

## <a name="multi-factor-authentication-registration-not-configured"></a>Registro de la autenticación multifactor no configurado
Esta vulnerabilidad le ayuda a controlar la implementación de Hola de Azure la autenticación multifactor en su organización. 

La autenticación multifactor Azure ofrece una segunda capa toouser de autenticación de seguridad. Ayuda a proteger acceso toodata y aplicaciones al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple. Ofrece una autenticación segura a través de una gran variedad de opciones sencillas, como llamadas telefónicas, mensajes de texto o notificaciones de aplicaciones móviles, lo que permite a los usuarios elegir el mecanismo que prefieran.

Se recomienda pedir Azure Multi-Factor Authentication para los inicios de sesión de usuario. La autenticación multifactor desempeña un papel clave en las directivas de acceso condicional basadas en riesgos disponibles mediante Identity Protection.

Para obtener más detalles, consulte [Qué es Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)

## <a name="unmanaged-cloud-apps"></a>Aplicaciones en la nube no administradas
Este punto vulnerable ayuda a identificar aplicaciones en la nube no administradas en su organización.

En las empresas modernas, los departamentos de TI a menudo son conscientes de todas las aplicaciones de nube de Hola que los usuarios de su organización usa toodo su trabajo. Es fácil toosee ¿por qué los administradores tendrían preocupado datos toocorporate de acceso no autorizado, posible pérdida de datos y otros riesgos de seguridad. 

Le recomendamos que su organización implemente aplicaciones de nube de Cloud App Discovery toodiscover no administrado y toomanage estas aplicaciones con Azure Active Directory.

Para obtener más detalles, consulte [Búsqueda de aplicaciones de nube no administradas con Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).

## <a name="security-alerts-from-privileged-identity-management"></a>Alertas de seguridad de administración de identidades con privilegios
Este punto vulnerable ayuda a detectar y resolver alertas acerca de las identidades con privilegios en su organización.  

tooenable toocarry de los usuarios con privilegios en operaciones de salida, las organizaciones necesitan los usuarios de toogrant temporales o permanentes privilegios de acceso en Azure AD, recursos de Azure u Office 365 u otras aplicaciones de SaaS. Cada uno de estos usuarios privilegiados aumenta Hola superficie expuesta a ataques de su organización. Esta vulnerabilidad le ayuda a identificar a los usuarios con acceso con privilegios innecesario y tomar las medidas adecuadas tooreduce o eliminar el riesgo de Hola que suponen. 

Se recomienda que su organización utiliza Azure AD Privileged Identity Management toomanage, control y las identidades de monitor con privilegios y sus tooresources de acceso de Azure AD, así como otros servicios en línea de Microsoft como Office 365 o Microsoft Intune.

Para obtener más detalles, consulte [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md). 

## <a name="see-also"></a>Otras referencias
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

