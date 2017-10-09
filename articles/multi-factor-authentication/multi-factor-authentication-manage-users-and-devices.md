---
title: aaaAdmins administrar usuarios y dispositivos - MFA de Azure | Documentos de Microsoft
description: "Describe cómo toochange configuración de usuario, como forzar Hola usuarios toodo Hola prueba el proceso de nuevo."
documentationcenter: 
services: multi-factor-authentication
author: kgremban
manager: femila
ms.assetid: aac3b922-7cc1-428c-9044-273579aa7b5a
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8c35435e4f6504014d9a4f6f1b837639c3b53481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-user-settings-with-azure-multi-factor-authentication-in-hello-cloud"></a>Administrar la configuración de usuario con autenticación multifactor de Azure en la nube de Hola
Como administrador, puede administrar Hola después de la configuración de usuario y dispositivo:

* Requieren métodos de contacto de los usuarios tooprovide nuevo
* Eliminar contraseñas de aplicación
* Requerir MFA en todos los dispositivos de confianza 

## <a name="require-users-tooprovide-contact-methods-again"></a>Requieren métodos de contacto de los usuarios tooprovide nuevo
Esta opción fuerza proceso de registro de hello usuario toocomplete Hola de nuevo. Las aplicaciones sin explorador continuar toowork si el usuario hello tiene las contraseñas de aplicación para ellos.  Puede eliminar las contraseñas de aplicación de los usuarios de hello seleccionando también **eliminar todas las contraseñas de aplicación existentes generadas por usuarios de hello seleccionado**.

### <a name="how-toorequire-users-tooprovide-contact-methods-again"></a>¿Cómo toorequire usuarios tooprovide métodos de contacto nuevo
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Hola izquierda, seleccione **Azure Active Directory** > **usuarios y grupos** > **todos los usuarios**.
3. Seleccione **Multi-Factor Authentication**. se abre la página de la autenticación multifactor de Hola. 
4. Compruebe Hola cuadro siguiente toohello o varios usuarios que desea toomanage. Aparecerá una lista de opciones de paso rápido en hello derecho. 
5. Seleccione **Administrar configuración de usuario**.
6. Casilla de Hola para **requieren los usuarios seleccionados tooprovide métodos de contacto nuevo**.
   ![Proporcionar métodos de contacto](./media/multi-factor-authentication-manage-users-and-devices/reproofup.png)
7. Haga clic en **guardar**.
8. Haga clic en **Cerrar**.

## <a name="delete-users-existing-app-passwords"></a>Eliminar las contraseñas de aplicación existentes de los usuarios
Esta acción elimina todas las contraseñas de aplicación Hola que ha creado un usuario. Las aplicaciones sin explorador asociadas con estas contraseñas de aplicación dejan de funcionar hasta que se cree una nueva contraseña de aplicación.

### <a name="how-toodelete-users-existing-app-passwords"></a>¿Cómo toodelete a los usuarios existentes de las contraseñas de aplicación
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Hola izquierda, seleccione **Azure Active Directory** > **usuarios y grupos** > **todos los usuarios**.
3. Seleccione **Multi-Factor Authentication**. se abre la página de la autenticación multifactor de Hola. 
6. Compruebe Hola cuadro siguiente toohello o varios usuarios que desea toomanage. Aparecerá una lista de opciones de paso rápido en hello derecho. 
7. Seleccione **Administrar configuración de usuario**.
8. Casilla de Hola para **eliminar todas las contraseñas de aplicación existentes generadas por usuarios de hello seleccionado**.
   ![Eliminar contraseñas de aplicación](./media/multi-factor-authentication-manage-users-and-devices/deleteapppasswords.png)
9. Haga clic en **guardar**.
10. Haga clic en **Cerrar**.

## <a name="restore-mfa-on-all-remembered-devices-for-a-user"></a>Restauración de MFA en todos los dispositivos recordados de un usuario
Una de hello características configurables de autenticación multifactor de Azure es dar a los usuarios Hola opción toomark dispositivos de confianza. Para más información, vea [Configuración de Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md#remember-multi-factor-authentication-for-devices-that-users-trust).

Los usuarios pueden optar por no usar la verificación en dos pasos durante un número de días configurable en sus dispositivos habituales. Si se pone en peligro una cuenta o un dispositivo de confianza se pierde, toobe tooremove capaz de hello confianza estado es necesario y requieren verificación en dos pasos.

Hola **restaurar la autenticación multifactor en todos los dispositivos recordados** valor significa que ese usuario Hola será Hola de comprobación de dos pasos de sus tooperform próxima vez que inicie sesión, independientemente de si eligió toomark sus dispositivo como de confianza. 

### <a name="how-toorestore-mfa-on-all-suspended-devices-for-a-user"></a>Cómo toorestore MFA en todos los dispositivos suspendidos para un usuario
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Hola izquierda, seleccione **Azure Active Directory** > **usuarios y grupos** > **todos los usuarios**.
3. Seleccione **Multi-Factor Authentication**. se abre la página de la autenticación multifactor de Hola. 
6. Compruebe Hola cuadro siguiente toohello o varios usuarios que desea toomanage. Aparecerá una lista de opciones de paso rápido en hello derecho. 
7. Seleccione **Administrar configuración de usuario**.
8. Casilla de Hola para **restaurar la autenticación multifactor en todos los dispositivos recordados**
   ![eliminar las contraseñas de aplicación](./media/multi-factor-authentication-manage-users-and-devices/rememberdevices.png)
9. Haga clic en **guardar**.
10. Haga clic en **Cerrar**.

## <a name="next-steps"></a>Pasos siguientes

- Obtener más información acerca de cómo demasiado[configuración de configurar la autenticación multifactor Azure](multi-factor-authentication-whats-next.md)

- Si los usuarios necesitan ayuda, señale hacia hello [Guía de usuario para la verificación en dos pasos](./end-user/multi-factor-authentication-end-user.md)
