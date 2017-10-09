---
title: "una colección de Azure RemoteApp de usuario tooyour aaaAdd | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd usuarios tooyour colección RemoteApp de Azure"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a>¿Cómo tooadd una colección de Azure RemoteApp tooyour de usuario
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Antes de que los usuarios pueden ver y usar las aplicaciones de Azure RemoteApp, tendrá toogrant acceso tooyour colección. Esto forma parte fácil hello: en hello **acceso de usuario** pestaña, escriba la información de la cuenta de hello para el usuario de Hola y, a continuación, haga clic en la casilla de verificación Hola.

¿Qué información de cuenta necesita? Que depende Hola tipo de colección que ha creado (en la nube o híbridas) y si utilizas Office 365 ProPlus en esa colección.

## <a name="supported-user-identities"></a>Identidades de usuario admitido
tipos de colecciones diferentes Hello (nube frente a híbrido) admiten el uso de distintas identidades de usuario para acceso tooapplications.  

Para una colección híbrida de RemoteApp, es necesario tooset seguridad de una infraestructura de dominio de Active Directory local y un inquilino de Azure Active Directory con la integración de directorio (y, opcionalmente, inicio de sesión único). Además, es necesario toocreate algunos objetos de Active Directory en el directorio local de Hola.  

Para una colección en la nube de RemoteApp, se puede conceder a cualquier usuario con Azure Active Directory admite identidades de usuario acceso tooRemoteApp tooinclude Accounts de Microsoft.  Vea la siguiente tabla de Hola.

Los usuarios de Office 365 son usuarios de Azure Active Directory. Si tienen cuentas de colección híbrida con sincronización de directorios de Azure Active Directory, se les puede conceder acceso de usuario en una implementación híbrida de RemoteApp.   

Puede utilizar esta tabla como una referencia rápida para el que se admite la identidad en la colección y cuáles son los requisitos de Active Directory de Hola.

| Cuentas de usuario | Nube | Híbrida |
| --- | --- | --- |
| Cuenta Microsoft |Sí |No |
| Azure Active Directory (Azure AD) | | |
| Solo nube de Azure AD |Sí |No |
| ADsync con sincronización de contraseñas |Sí |Sí |
| ADsync sin sincronización de contraseñas |Sí |No |
| ADsync con AD FS |Sí |yes |
| [Proveedores de identidades de terceros compatibles con Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx) (por ejemplo, Ping) |Sí |Sí |
| Multi-Factor Authentication |Sí |Sí |

Consulte [más información](remoteapp-ad.md) sobre cómo configurar Active Directory para RemoteApp.

> [!NOTE]
> los usuarios de Azure Active Directory de Hello deben ser de inquilino de Hola que esté asociada con su suscripción. (Puede ver y modificar su suscripción en hello **configuración** portal Hola de. Vea [inquilino de Azure Active Directory de cambio hello usa RemoteApp](remoteapp-changetenant.md) para obtener más información.)
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Información de la cuenta de usuario de Office 365 ProPlus
Si utilizas Office 365 ProPlus imagen de plantilla hello en la colección de *o* si ha creado una imagen personalizada que usa Office 365, solo se permiten los usuarios de Azure Active Directory tooadd que tienen suscripciones de Office 365 para hello dominio predeterminado de su suscripción. Consulte [Uso de Office 365 con RemoteApp de Azure](remoteapp-o365.md) para obtener más información.

