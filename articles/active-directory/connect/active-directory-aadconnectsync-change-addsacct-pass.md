---
title: "Azure AD Connect sync: cambiar contraseña de cuenta de hello AD DS | Documentos de Microsoft"
description: "Este documento de tema describe cómo se cambia tooupdate Azure AD Connect después de la contraseña de Hola de cuenta de hello AD DS."
services: active-directory
keywords: "cuenta de AD DS, cuenta de Active Directory, contraseña"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a>Cambiar la contraseña de la cuenta de hello AD DS
cuenta de Hello AD DS refiere la cuenta de usuario de toohello utilizada toocommunicate de Azure AD Connect con local de Active Directory. Si cambia la contraseña Hola de hello cuenta AD DS, debe actualizar servicio de sincronización de Connect de Azure AD con hello nueva contraseña. En caso contrario, Hola que sincronización ya no se puede sincronizar correctamente con hello Active Directory local y se producirán Hola siguientes errores:

* Hola operación Synchronization Service Manager, cualquier importación o exportación con local se produce un error de AD con **credenciales de inicio no** error.

* En el Visor de eventos de Windows, el registro de eventos de aplicación Hola contiene un error con **6000 de Id. de evento** y mensaje **'agente de administración de Hola "contoso.com" error toorun porque las credenciales de hello no eran válidas'** .


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a>¿Cómo tooupdate Hola servicio de sincronización con la nueva contraseña de cuenta de AD DS
Hola de tooupdate servicio de sincronización con la nueva contraseña de hello:

1. Iniciar Hola Synchronization Service Manager (servicio de sincronización de inicio →).
</br>![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  

2. Vaya toohello **conectores** ficha.

3. Seleccione hello **conector AD** correspondiente cuenta de toohello AD DS para la que se ha cambiado su contraseña.

4. En **Acciones**, seleccione **Propiedades**.

5. En el cuadro de diálogo emergente de hello, seleccione **conectar tooActive Directory bosque**:

6. Escriba Hola nueva contraseña de cuenta de AD DS Hola Hola **contraseña** cuadro de texto.

7. Haga clic en **Aceptar** toosave Hola nueva contraseña y el cuadro de diálogo emergente de hello cerrar.

8. Reinicio Hola servicio Azure AD Connect sincronización en el Administrador de Control de servicios de Windows. Se trata de tooensure que cualquier contraseña antigua de toohello de referencia se quita de la caché de memoria de Hola.

## <a name="next-steps"></a>Pasos siguientes
**Temas de introducción**

* [Sincronización de Azure AD Connect: comprender y personalizar la sincronización](active-directory-aadconnectsync-whatis.md)

* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
