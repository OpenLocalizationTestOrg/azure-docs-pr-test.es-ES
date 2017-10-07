---
title: "comprobación de paso aaaTwo y AD FS - MFA de Azure | Documentos de Microsoft"
description: "Se trata de una página de autenticación multifactor de Azure de Hola que describe cómo se inicia tooget con MFA de Azure y AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a>Introducción a Azure Multi-Factor Authentication y a los Servicios de federación de Active Directory
<center>![Nube](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center>

Si su organización ha federado su Active Directory local con Azure Active Directory mediante AD FS, tiene a su disposición dos opciones para usar Azure Multi-Factor Authentication.

* Recursos de nube seguros a través del uso de Azure Multi-Factor Authentication o los Servicios de federación de Active Directory
* Protección de recursos en la nube y locales mediante Servidor Azure Multi-Factor Authentication

Hello en la tabla siguiente resume la experiencia de comprobación de hello entre la protección de recursos con la autenticación multifactor Azure y AD FS

| Experiencia de verificación: aplicaciones basadas en explorador | Experiencia de verificación: aplicaciones no basadas en explorador |
|:--- |:--- |:--- |
| Protección de recursos de Azure AD con Azure Multi-Factor Authentication |<li>primer paso de verificación Hola se realiza localmente utilizando AD FS.</li> <li>Hola segundo paso es un método basado en teléfono que se llevan a cabo mediante la autenticación de nube.</li> |
| Protección de los recursos de Azure AD mediante los servicios de federación de Active Directory |<li>primer paso de verificación Hola se realiza localmente utilizando AD FS.</li><li>Hola segundo paso es realiza localmente respondiendo a una notificación de Hola.</li> |

Advertencias sobre las contraseñas de aplicación para usuarios federados:

* Las contraseña de aplicación se comprueban mediante autenticación en la nube y, por lo tanto, omiten las federaciones. La federación solo se usa activamente al configurar una contraseña de aplicación.
* La configuración del control de acceso de cliente local no se cumple con las contraseñas de aplicación.
* Se pierde la capacidad de registro de autenticación local para las contraseñas de aplicación.
* La deshabilitación o eliminación de cuenta puede tardar horas toothree para sincronización de directorios, lo que se retrasa la deshabilitación o eliminación de contraseñas de aplicación en la identidad de nube de Hola.

## <a name="next-steps"></a>Pasos siguientes
Para obtener información sobre cómo configurar la autenticación multifactor Azure u Hola servidor Azure Multi-factor Authentication con AD FS, vea Hola siguientes artículos:

* [Protección de recursos en la nube con Azure Multi-Factor Authentication y AD FS](multi-factor-authentication-get-started-adfs-cloud.md)
* [Protección de recursos en la nube y locales mediante Servidor Azure Multi-Factor Authentication con Windows Server 2012 R2 AD FS](multi-factor-authentication-get-started-adfs-w2k12.md)
* [Protección de recursos en la nube y locales mediante Servidor Azure Multi-Factor Authentication con AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md)
