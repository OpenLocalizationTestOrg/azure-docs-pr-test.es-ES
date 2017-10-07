---
title: "¿aaaHow toouse contraseñas de aplicación en Azure MFA? | Microsoft Docs"
description: "Esta página le ayudará a los usuarios a entender qué son las contraseñas de aplicación y qué son destinados a tener en cuenta tooAzure MFA."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 3afa2003d8e87576f035bf9440a1dba67bd85f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a>¿Qué son las contraseñas de aplicación en Azure Multi-Factor Authentication?
Determinadas aplicaciones sin explorador, por ejemplo, cliente de correo electrónico nativo de Apple hello usa Exchange Active Sync, actualmente no admiten la autenticación multifactor. La autenticación multifactor se habilita por usuario.  Esto significa que un usuario no puede usar la autenticación multifactor si:

- usuario de Hola se ha habilitado para la autenticación multifactor
- Hola usuario trate de toouse una aplicación sin explorador.

Una contraseña de aplicación permite aplicación Hola de hello usuario toouse.

Una vez que tenga una contraseña de aplicación, utilícela en lugar de la contraseña original para estas aplicaciones sin explorador. Cuando se registre para la verificación en dos pasos, está indicando a Microsoft no toolet cualquier persona inicie sesión con su contraseña si también no pueden realizar la comprobación de segundo de Hola. cliente de correo electrónico nativo de Apple Hello en el teléfono no puede iniciar una sesión que, dado que no se puede solicitar verificación en dos pasos. problema de solución toothis Hello es toocreate una contraseña de aplicación más segura que no usan diarias. Las contraseñas de aplicación solo son para las aplicaciones que no admiten la verificación en dos pasos. Usar la contraseña de aplicación de Hola para que pueden omitir la autenticación multifactor y continuar toowork aplicaciones.


> [!NOTE]
> Los clientes de Office 2013 (incluido Outlook) admiten nuevos protocolos de autenticación que se pueden usar con la verificación en dos pasos. Las contraseñas de aplicación no son necesarias para los clientes de Office 2013.  Para más información, consulte [Anuncio de la versión preliminar pública de la autenticación moderna de Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).


## <a name="how-toouse-app-passwords"></a>¿Cómo toouse las contraseñas de aplicación
Estos son algunos tooknow cosas acerca de las contraseñas de aplicación:

* El usuario no crea sus propias contraseñas de aplicación. Se generan automáticamente.
* Actualmente hay un límite de 40 contraseñas por usuario. 
* Si intentas toocreate una contraseña de aplicación una vez ha alcanzado el límite de hello, tendrá toodelete una de las contraseñas de aplicación existente antes de crear uno nuevo.
* Utilice una contraseña de aplicación por dispositivo, no por aplicación. Por ejemplo, puede crear una contraseña de aplicación para su equipo portátil y utilizar esa contraseña de aplicación para todas las aplicaciones de ese equipo portátil. A continuación, cree un segundo toouse de contraseña de aplicación para todas las aplicaciones en el escritorio. 
* Se le ofrecerá Hola de contraseña de aplicación una primera vez que se registra para la verificación en dos pasos.  Si necesita otras adicionales, puede crearlas.



## <a name="creating-and-deleting-app-passwords"></a>Creación y eliminación de contraseñas de aplicación
Durante el inicio de sesión inicial, se le ofrece una contraseña de aplicación que puede usar.  También puede crear y eliminar las contraseñas de aplicación más adelante. La forma de eliminar las contraseñas depende de cómo use la autenticación multifactor. Hola de respuesta después de preguntas toodetermine dónde debe ir toomanage contraseñas de aplicación: 

1. ¿Utiliza la verificación en dos pasos para su cuenta Microsoft personal? Si es así, debe hacer referencia toohello [contraseñas de aplicación y la verificación en dos pasos](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) artículo para obtener ayuda. Si no, seguir tooquestion dos.

2. En ese caso, significa que usa la verificación en dos pasos para la cuenta profesional o educativa. ¿Se usa toosign en tooOffice 365 aplicaciones? En caso afirmativo, se debe hacer referencia demasiado[crear una contraseña de aplicación para Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) para obtener ayuda. Si no, seguir tooquestion tres. 

3. ¿Utiliza la verificación en dos pasos con Microsoft Azure? En caso afirmativo, continúe toohello [administrar contraseñas de aplicación en el portal de Azure hello](#manage-app-passwords-in-the-Azure-portal) sección de este artículo. Si no, seguir tooquestion cuatro.

4. ¿No está seguro de donde utiliza la verificación en dos pasos? Continuar toohello [administrar contraseñas de aplicación con el portal mis aplicaciones de hello](#manage-app-passwords-with-the-myapps-portal) sección de este artículo. 


## <a name="manage-app-passwords-in-hello-azure-portal"></a>Administrar contraseñas de aplicación Hola portal de Azure
Si usas verificacion con Azure, desea toocreate contraseñas de aplicación a través de hello portal de Azure.

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a>contraseñas de aplicación toocreate Hola portal de Azure
1. Inicie sesión en toohello portal de Azure clásico.
2. En la parte superior de hello, haga clic en el nombre de usuario y seleccione la comprobación de seguridad adicional.
3. En la página de proofup hello, en la parte superior de hello, seleccione las contraseñas de aplicación
4. Haga clic en **Crear**.
5. Escriba un nombre para la contraseña de la aplicación hello y haga clic en **siguiente**
6. Portapapeles de toohello de contraseña de aplicación Hola de copiar y pegar en la aplicación.
   
   ![Nube](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a>contraseñas de aplicación toodelete Hola portal de Azure
1. Inicie sesión en toohello portal de Azure clásico.
2. En la parte superior de hello, haga clic en el nombre de usuario y seleccione la comprobación de seguridad adicional.
3. En parte superior de hello, comprobación de seguridad tooadditional siguiente, seleccione **contraseñas de aplicación.**
4. Contraseña de aplicación siguiente toohello desea toodelete, seleccione **eliminar**.
5. Confirmar eliminación de hello haciendo clic en **Sí**.
6. Una vez que se elimina la contraseña de la aplicación hello, haga clic en **cerrar**.


## <a name="manage-app-passwords-with-hello-myapps-portal"></a>Administrar contraseñas de aplicación con el portal mis aplicaciones de Hola.
Si no estás seguro de cómo usar la autenticación multifactor, siempre puede crear y eliminar las contraseñas de aplicación a través del portal mis aplicaciones de Hola.

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a>toocreate una contraseña de aplicación con Hola portal mis aplicaciones
1. Inicie sesión en demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Haga clic en el nombre de la parte superior de hello derecha y elija **perfil**.
3. Seleccione **Comprobación de seguridad adicional**.
   ![Seleccionar comprobación de seguridad adicional: captura de pantalla](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Seleccione **contraseñas de aplicación**.
   ![Seleccionar contraseñas de aplicación: captura de pantalla](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Haga clic en **Crear**.
6. Escriba un nombre para la contraseña de la aplicación hello y haga clic en **siguiente**.
7. Portapapeles de toohello de contraseña de aplicación Hola de copiar y pegar en la aplicación.
   ![Crear una contraseña de aplicación](./media/multi-factor-authentication-end-user-app-passwords/create2.png)

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a>toodelete una contraseña de aplicación con Hola portal mis aplicaciones
1. Inicie sesión en demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. En la parte superior de hello, seleccione el perfil.
3. Seleccione **Comprobación de seguridad adicional**.

   ![Seleccionar comprobación de seguridad adicional: captura de pantalla](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Seleccione **contraseñas de aplicación**.

   ![Seleccionar contraseñas de aplicación: captura de pantalla](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Haga clic en siguiente contraseña de aplicación de toohello desea toodelete, **eliminar**.

   ![Eliminar una contraseña de aplicación](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. Confirme que desea toodelete esa contraseña haciendo clic en **Sí**.
7. Una vez que se elimina la contraseña de la aplicación hello, haga clic en **cerrar**.

## <a name="next-steps"></a>Pasos siguientes

- [Administrar la configuración de la verificación en dos pasos](multi-factor-authentication-end-user-manage-settings.md)

- Pruebe hello [aplicación Microsoft Authenticator](microsoft-authenticator-app-how-to.md) tooverify los inicios de sesión con las notificaciones de la aplicación, en lugar de recibir llamadas o textos. 
