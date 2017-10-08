---
title: "Solución de problemas: Elemento \"Active Directory\" falta o no está disponible | Documentos de Microsoft"
description: "¿Qué toodo al elemento de menú de Active Directory no aparece en hello Portal de administración de Azure."
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a>Solución de problemas: El elemento "Active Directory" falta o no está disponible
Muchas de las instrucciones de hello para el uso de servicios y características de Azure Active Directory comienzan por "toohello Portal de administración de Azure y haga clic en **Active Directory**." Pero ¿qué hacer si no aparece el elemento de menú o extensión de Active Directory de Hola o si está marcado como **no está disponible**? Este tema está diseñado toohelp. Describe las condiciones de hello en las que **Active Directory** no aparece o no está disponible y se explica cómo tooproceed.

## <a name="active-directory-is-missing"></a>Falta Active Directory
Normalmente, un **Active Directory** elemento aparece en el menú de navegación izquierdo de Hola. instrucciones de Hello en los procedimientos de Azure Active Directory, se supone que este elemento aparece en la vista.

![Captura de pantalla: Active Directory en Azure](./media/active-directory-troubleshooting/typical-view.png)

elemento de Active Directory de Hello aparece en el menú de navegación izquierdo de hello cuando cualquiera de hello condiciones siguientes es verdadera. En caso contrario, el elemento de hello no aparece.

* usuario actual de Hello iniciado sesión con una cuenta de Microsoft (anteriormente conocida como Windows Live ID).
  
    OR
* Hola inquilino de Azure tiene un directorio y cuenta de hello actual es un administrador de directorios.
  
    OR
* Hola inquilino de Azure tiene al menos un espacio de nombres de Control de acceso de Azure AD (ACS). Para obtener más información, consulte [Espacio de nombres de Control de acceso](https://msdn.microsoft.com/library/azure/gg185908.aspx).
  
    OR
* Hola inquilino de Azure tiene al menos un proveedor de autenticación multifactor de Azure. Para obtener más información, consulte [Administración de proveedores de Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

toocreate un espacio de nombres de Control de acceso o un proveedor de la autenticación multifactor, haga clic en **+ nuevo** > **servicios de aplicaciones** > **deActiveDirectory**.

directorio de tooa de tooget derechos administrativos, haya un administrador asignar a un administrador cuenta tooyour del rol. Para obtener detalles, consulte [Asignación de roles de administrador en Azure AD](active-directory-assign-admin-roles.md).

## <a name="active-directory-is-not-available"></a>Active Directory no está disponible
Cuando se hace clic en **+Nuevo** > **App Services**, aparece el elemento **Active Directory**. En concreto, elemento de Active Directory de hello aparece cuando cualquiera de las características de Active Directory de hello, como directorio, Control de acceso o proveedor de autenticación multifactor, están disponibles toohello usuario actual.

Sin embargo, mientras se carga la página de hello, elemento de hello aparece atenuado y está marcado como **no está disponible**. Se trata de un estado temporal. Si espera unos segundos, el elemento de hello estará disponible. Si se prolonga el retraso de hello, Actualizar página web de Hola a menudo resuelve problema Hola.

![Captura de pantalla: Active Directory no está disponible](./media/active-directory-troubleshooting/not-available.png)

