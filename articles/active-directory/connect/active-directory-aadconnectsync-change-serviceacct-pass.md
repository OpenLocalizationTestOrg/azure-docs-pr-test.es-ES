---
title: "Azure AD Connect sync: cambiar cuenta de servicio de sincronización conectarse hello Azure AD | Documentos de Microsoft"
description: "Este documento de tema describe la clave de cifrado de Hola y cómo tooabandon después de la contraseña de hello es cambiado."
services: active-directory
keywords: "Cuenta del servicio Sincronización de Azure AD, contraseña"
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
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a>Cambiar la contraseña de la cuenta de servicio de sincronización de hello Azure AD Connect
Si cambia la contraseña de la cuenta de servicio de sincronización de hello Azure AD Connect, Hola servicio de sincronización no será capaz de inicio correctamente hasta que haya abandonado la clave de cifrado de Hola y reinicializar la contraseña de la cuenta de servicio de sincronización de hello Azure AD Connect. 

Azure AD Connect, como parte de servicios de sincronización de hello usa un contraseñas de hello toostore clave de cifrado de hello AD DS y las cuentas de servicio de Azure AD.  Estas cuentas se cifran antes de que se almacenen en la base de datos de Hola. 

Hello clave de cifrado utilizada se protege utilizando [protección de datos (DPAPI) de Windows](https://msdn.microsoft.com/library/ms995355.aspx). DPAPI protege la clave de cifrado de hello con hello **contraseña de cuenta de servicio de sincronización de hello Azure AD Connect**. 

Si necesita la contraseña de la cuenta de servicio de toochange Hola puede usar los procedimientos de hello en [clave de cifrado de Abandoning hello Azure AD Sync conectarse](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish esto.  Estos procedimientos también deben utilizarse si necesita clave de cifrado de hello tooabandon por cualquier motivo.

##<a name="issues-that-arise-from-changing-hello-password"></a>Problemas que surgen al cambiar contraseña de Hola
Hay dos aspectos que deben toobe realiza cuando se cambia la contraseña de cuenta de servicio de Hola.

En primer lugar, necesita toochange Hola contraseña en el Administrador de Control de servicios de Windows hello.  Hasta que se solucione el problema, verá los siguientes errores:


- Si intentas hello toostart servicio de sincronización en el Administrador de Control de servicios de Windows, recibe el error de Hola "**Windows no pudo iniciar servicio de sincronización de Microsoft Azure AD de hello en el equipo Local**". **Error 1069: el servicio de hello no se inició debido a error de inicio de sesión de tooa.** "
- En el Visor de eventos de Windows, el registro de eventos del sistema de hello contiene un error con **7038 de Id. de evento** y el mensaje "**Hola servicio ADSync estaba toolog no se puede como con contraseña Hola configurada actualmente debido toohello siguiente error: nombre de usuario de Hola o la contraseña es incorrecta.** "

En segundo lugar, en condiciones específicas, si se actualiza la contraseña de hello, Hola servicio de sincronización puede ya no recuperar clave de cifrado de hello mediante DPAPI. Sin la clave de cifrado de Hola Hola que servicio de sincronización no se puede descifrar hello las contraseñas necesarias toosynchronize a/desde local de AD y Azure AD.
Verá errores como los siguientes:

- En el Administrador de Control de servicios de Windows, si intenta toostart Hola servicio de sincronización y no puede recuperar la clave de cifrado de hello, se produce un error error "** Windows no pudo iniciar Hola sincronización de Microsoft Azure AD en el equipo Local. Para obtener más información, revise el registro de sucesos del sistema de Hola. Si se trata de un servicio de terceros, póngase en contacto con el proveedor de servicios de Hola y consulte el código de error específico tooservice **-21451857952 ***. "
- En el Visor de eventos de Windows, el registro de eventos de aplicación Hola contiene un error con **6028 de Id. de evento** y mensaje de error *"**no se puede tener acceso a clave de cifrado del servidor de Hola.* *"*

tooensure que no reciben estos errores, siga los procedimientos de hello en [clave de cifrado de Abandoning hello Azure AD Sync conectarse](#abandoning-the-azure-ad-connect-sync-encryption-key) al cambiar contraseña de Hola.
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a>Abandonar la clave de cifrado de hello sincronización conectarse de Azure AD
>[!IMPORTANT]
>Hello procedimientos siguientes solo aplican tooAzure AD Connect compilación 1.1.443.0 o anterior.

Usar hello después de la clave de cifrado de procedimientos tooabandon Hola.

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a>¿Qué toodo si necesita la clave de cifrado de hello tooabandon

Si necesita la clave de cifrado de hello tooabandon, utilícelo Hola siguiendo los procedimientos tooaccomplish.

1. [Abandonar la clave de cifrado existente Hola](#abandon-the-existing-encryption-key)

2. [Proporcionar contraseña Hola de hello cuenta AD DS](#provide-the-password-of-the-ad-ds-account)

3. [Reinicializar contraseña Hola de hello cuenta de sincronización de Azure AD](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [Iniciar servicio de sincronización de Hola](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a>Abandonar la clave de cifrado existente Hola
Abandonar la clave de cifrado existente de hello, por lo que puede crearse esa nueva clave de cifrado:

1. Inicie sesión en tooyour servidor Connect de Azure AD como administrador.

2. Inicie una nueva sesión de PowerShell.

3. Desplácese toofolder:`$env:Program Files\Microsoft Azure AD Sync\bin\`

4. Ejecute el comando de hello:`./miiskmu.exe /a`

![Utilidad de clave de cifrado de sincronización de Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a>Proporcionar contraseña Hola de hello cuenta AD DS
Como ya no se pueden descifrar las contraseñas existentes de hello almacenadas dentro de la base de datos de hello, debes tooprovide Hola servicio de sincronización con la contraseña de Hola de cuenta de hello AD DS. Hola servicio de sincronización cifra las contraseñas de hello con hello nueva clave de cifrado:

1. Iniciar Hola Synchronization Service Manager (servicio de sincronización de inicio →).
</br>![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  
2. Vaya toohello **conectores** ficha.
3. Seleccione hello **conector AD** correspondiente tooyour AD local. Si tiene más de un conector de AD, repita Hola siguiendo los pasos para cada uno de ellos.
4. En **Acciones**, seleccione **Propiedades**.
5. En el cuadro de diálogo emergente de hello, seleccione **conectar tooActive Directory bosque**:
6. Escriba la contraseña de Hola de cuenta de AD DS Hola Hola **contraseña** cuadro de texto. Si no conoce su contraseña, debe establecer tooa valor conocido antes de realizar este paso.
7. Haga clic en **Aceptar** toosave Hola nueva contraseña y el cuadro de diálogo emergente de hello cerrar.
![Utilidad de clave de cifrado de sincronización de Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key6.png)

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a>Reinicializar contraseña Hola de hello cuenta de sincronización de Azure AD
No se proporciona directamente contraseña Hola de toohello de cuenta de servicio servicio de sincronización de hello Azure AD. En su lugar, debe toouse Hola cmdlet **ADSyncAADServiceAccount agregar** tooreinitialize Hola cuenta de servicio de Azure AD. Hola cmdlet restablece la contraseña de la cuenta de hello y facilita toohello disponible el servicio de sincronización:

1. Iniciar una nueva sesión de PowerShell en el servidor de Azure AD Connect Hola.
2. Ejecute el cmdlet `Add-ADSyncAADServiceAccount`.
3. En el cuadro de diálogo emergente de hello, proporcione las credenciales de administrador Global de hello Azure AD para el inquilino de Azure AD.
![Utilidad de clave de cifrado de sincronización de Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key7.png)
4. Si se realiza correctamente, verá el símbolo del sistema de PowerShell de Hola.

#### <a name="start-hello-synchronization-service"></a>Iniciar servicio de sincronización de Hola
Ahora que Hola servicio de sincronización tiene la clave de cifrado de toohello de acceso y todas las contraseñas de Hola que necesita, puede reiniciar el servicio de Hola Hola Administrador de Control de servicios de Windows:


1. Vaya tooWindows Administrador de Control de servicios (servicios de inicio →).
2. Seleccione **Sincronización de Microsoft Azure AD** y haga clic en Reiniciar.

## <a name="next-steps"></a>Pasos siguientes
**Temas de introducción**

* [Sincronización de Azure AD Connect: comprender y personalizar la sincronización](active-directory-aadconnectsync-whatis.md)

* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
