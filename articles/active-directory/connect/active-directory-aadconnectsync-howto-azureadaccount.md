---
title: 'Azure AD Connect sync: la cuenta de servicio toomanage hello Azure AD | Documentos de Microsoft'
description: Este tema documenta la cuenta de servicio toorestore hello Azure AD.
services: active-directory
keywords: "AADSTS70002, AADSTS50054, cómo tooreset Hola contraseña de hello Azure AD Connect sync cuenta de servicio de conector"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a>Azure AD Connect sync: la cuenta de servicio toomanage hello Azure AD
cuenta de servicio de Hello usada por hello conector de Azure AD se supone que toobe servicio gratuito. Si necesita tooreset sus credenciales, este tema es para usted. Por ejemplo, si un administrador Global tiene por error Hola de restablecimiento de contraseñas de cuenta de servicio de hello mediante PowerShell.

## <a name="reset-hello-credentials"></a>Restablecer credenciales de Hola
Si la cuenta de servicio de hello definida en hello conector de Azure AD no puede ponerse en contacto con Azure AD debido a problemas de tooauthentication, se puede restablecer contraseña Hola.

1. Inicie sesión en el servidor de sincronización de Azure AD Connect toohello e inicie PowerShell.
2. Ejecute `Add-ADSyncAADServiceAccount`.  
   ![Cmdlet addadsyncaadserviceaccount de PowerShell](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)
3. Proporcione las credenciales de administrador global de Azure AD.

Este cmdlet restablece la contraseña de hello para la cuenta de servicio de Hola y actualizarla en Azure AD y en el motor de sincronización de Hola.

## <a name="known-issues-these-steps-can-solve"></a>Problemas conocidos que pueden solucionarse siguiendo estos pasos
Esta sección es una lista de errores notificados por los clientes que se corrigieron por un credenciales restablecer en hello cuenta de servicio de Azure AD.

- - -
Evento 6900  
servidor de Hello encontró un error inesperado al procesar una notificación de cambio de contraseña:  
AADSTS70002: error al validar las credenciales. AADSTS50054: se utilizó una contraseña antigua para realizar la autenticación.

- - -
Evento 659  
Error al recuperar la configuración de sincronización de directivas de contraseña. Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:  
AADSTS70002: error al validar las credenciales. AADSTS50054: se utilizó una contraseña antigua para realizar la autenticación.

## <a name="next-steps"></a>Pasos siguientes
**Temas de introducción**

* [Sincronización de Azure AD Connect: comprender y personalizar la sincronización](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)

