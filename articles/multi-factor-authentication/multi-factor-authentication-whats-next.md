---
title: aaaConfigure MFA de Azure | Documentos de Microsoft
description: "Se trata de una página de autenticación multifactor de Azure de Hola que describe qué toodo junto con MFA.  Esto incluye informes, alertas de fraude, omisión por única vez, mensajes de voz personalizados, almacenamiento en caché, direcciones IP de confianza y contraseñas de aplicación."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 75af734e-4b12-40de-aba4-b68d91064ae8
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: kgremban
ms.openlocfilehash: 7f6d0b0975a2c1da2de9b52e978b84475c79b218
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-settings"></a>Configuración de Azure Multi-Factor Authentication
Este artículo le ayudará a administrar Azure Multi-Factor Authentication ahora que ya está preparado y con todo funcionando.  Incluye varios temas que le ayudarán a hello tooget máximo partido de la autenticación multifactor Azure.  No todas estas características están disponibles en todas las versiones de Azure Multi-Factor Authentication.

| Característica | Descripción | 
|:--- |:--- |
| [Alerta de fraude](#fraud-alert) |Alerta de fraude puede ser configurado y configurar para que los usuarios pueden notificar intentos fraudulentos tooaccess sus recursos. |
| [Omisión por única vez](#one-time-bypass) |Una omisión por única vez permite a un usuario tooauthenticate una sola vez al "Omitir" la autenticación multifactor. |
| [Mensajes de voz personalizados](#custom-voice-messages) |Mensajes de voz personalizados le permiten toouse sus propias grabaciones o greetings con la autenticación multifactor. |
| [Almacenamiento en caché](#caching-in-azure-multi-factor-authentication) |Almacenamiento en caché permite tooset un período de tiempo específico para que los intentos de autenticación posteriores correctos automáticamente. |
| [Direcciones IP de confianza](#trusted-ips) |Los administradores de un inquilino administrado o federado pueden usar verificacion de toobypass de IP de confianza para los usuarios que inician sesión desde la intranet local de la compañía de Hola. |
| [Contraseñas de aplicación](#app-passwords) |Una contraseña de aplicación permite a una aplicación que no es compatible con MFA toobypass la autenticación multifactor y seguir trabajando. |
| [Recordar la autenticación multifactor para exploradores y dispositivos recordados](#remember-multi-factor-authentication-for-devices-that-users-trust) |Le permite tooremember dispositivos durante un número determinado de días después de que un usuario ha iniciado sesión correctamente en el uso de MFA. |
| [Métodos de verificación seleccionables](#selectable-verification-methods) |Permite métodos de autenticación de hello toochoose que están disponibles para los usuarios toouse. |

## <a name="access-hello-azure-mfa-management-portal"></a>Hola acceso Portal de administración de MFA de Azure

características de Hello tratadas en este artículo se configuran en hello Portal de administración de autenticación multifactor de Azure. Hay dos maneras tooaccess Hola portal de administración de MFA mediante Hola portal de Azure clásico. Hola en primer lugar es debido a que administra un proveedor de autenticación multifactor. en segundo lugar, Hello es a través de la configuración de servicio MFA de Hola. 

### <a name="use-an-auth-provider"></a>Uso de un proveedor de autenticación

Si usa un proveedor de autenticación multifactor para MFA basada en el consumo, use este portal de administración de método tooaccess Hola.

tooaccess Hola Portal de administración de MFA a través de un proveedor de autenticación multifactor de Azure, inicie sesión en hello portal de Azure clásico como administrador y opción de hello seleccione Active Directory. Haga clic en hello **proveedores de autenticación multifactor** , a continuación, seleccione el directorio y haga clic en hello **administrar** situado en la parte inferior de Hola.

### <a name="use-hello-mfa-service-settings-page"></a>Utilice la página de configuración del servicio de MFA de Hola 

Si tiene un proveedor de autenticación multifactor o un MFA de Azure, Azure AD Premium o Enterprise Mobility + licencia de seguridad, utilice esta página de configuración de servicio MFA de método tooaccess Hola.

tooaccess Hola Portal de administración de MFA a través de la página de configuración del servicio de MFA de inicio de sesión en el portal de Azure clásico como administrador de Hola Hola y seleccione la opción de Active Directory de Hola. Haga clic en el directorio y, a continuación, haga clic en hello **configurar** ficha. En la sección de la autenticación multifactor de hello, seleccione **administrar la configuración del servicio**. En parte inferior de Hola de página de configuración del servicio de MFA de hello, haga clic en hello **Go toohello portal** vínculo.


## <a name="fraud-alert"></a>Alerta de fraude
Alerta de fraude puede ser configurado y configurar para que los usuarios pueden notificar intentos fraudulentos tooaccess sus recursos.  Los usuarios pueden informar de fraude con aplicación móvil de Hola o a través de su teléfono.

### <a name="set-up-fraud-alert"></a>Configuración de la alerta de fraude
1. Navegue toohello Portal de administración de MFA por instrucciones de hello en la parte superior de Hola de esta página.
2. En el Portal de administración de Azure Multi-factor Authentication hello, haga clic en **configuración** en hello sección de configuración.
3. En sección alerta de fraude de página de configuración de Hola Hola, compruebe hello **permitir a los usuarios alertas de fraude toosubmit** casilla de verificación.
4. Seleccione **guardar** tooapply los cambios. 

### <a name="configuration-options"></a>Opciones de configuración

- **Bloquear usuario al notificarse fraudes**: si se informa de que un usuario ha cometido un fraude, se bloquea su cuenta.
- **Código de fraude durante el saludo inicial de tooReport** -los usuarios normalmente presionar verificacion de # tooconfirm. Si lo desean tooreport fraude, entran en un código antes de presionar #. De manera predeterminada, dicho código es **0**, pero se puede personalizar.

> [!NOTE]
> Saludos de voz de Microsoft de forma predeterminada, indique a los usuarios toopress # 0 toosubmit una alerta de fraude. Si desea toouse un código distinto de 0, debe registrar y cargar sus propio saludos de voz personalizados con instrucciones apropiadas.

![Opciones de alerta de fraude (captura de pantalla)](./media/multi-factor-authentication-whats-next/fraud.png)

### <a name="how-users-report-fraud"></a>Cómo notifican un fraude los usuarios 
Una alerta de fraude se puede notificar de dos maneras.  Ya sea a través de aplicaciones móviles de Hola o teléfono Hola.  

#### <a name="report-fraud-with-hello-mobile-app"></a>Denunciar fraude con aplicación móvil de hello
1. Cuando se envíe una verificación tooyour teléfono, selecciónela tooopen Hola Microsoft Authenticator aplicación.
2. Seleccione **Deny** en la notificación de Hola. 
3. Haga clic en **Notificar fraude**.
4. Aplicación de hello cerrar.

#### <a name="report-fraud-with-a-phone"></a>Notificación de fraude con un teléfono
1. Cuando se recibe una llamada de comprobación en tooyour teléfono, respóndala.  
2. tooreport fraude, introduzca el código de fraude de hello (el valor predeterminado es 0) y, a continuación, Hola signo #. Se le notificará que se ha enviado una alerta de fraude.
3. Finalizar la llamada de Hola.

### <a name="view-fraud-reports"></a>Visualización de notificaciones de fraude
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Hola izquierda, seleccione Active Directory.
3. En, seleccione superior hello **proveedores de autenticación multifactor**. Aparecerá una lista de los proveedores de Multi-Factor Authentication.
4. Seleccione el proveedor de autenticación multifactor y haga clic en **administrar** final Hola de página Hola. se abrirá el Portal de administración de Azure Multi-factor Authentication Hola.
5. En hello Portal de administración de Azure Multi-factor Authentication, bajo ver un informe, haga clic en **alerta de fraude**.
6. Especifique el intervalo de fechas de Hola que desea tooview en informe de Hola. También puede especificar nombres de usuario, los números de teléfono y estado del usuario de Hola.
7. Haga clic en **Ejecutar**. Aparecerá un informe de las alertas de fraude. Haga clic en **exportar tooCSV** si desea que el informe de hello tooexport.

## <a name="one-time-bypass"></a>Omisión por única vez
Una omisión por única vez permite a un usuario tooauthenticate una sola vez sin realizar la comprobación de dos pasos. Hola omisión es temporal y expira después de un número especificado de segundos. En situaciones donde Hola de aplicación móvil o teléfono no recibe una notificación o una llamada de teléfono, puede habilitar una omisión por única vez para usuario Hola pueda acceder a recursos de hello deseado.

### <a name="create-a-one-time-bypass"></a>Creación de una omisión por única vez
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Navegue toohello Portal de administración de MFA por instrucciones de hello en la parte superior de Hola de esta página.
3. Hola Portal de administración de Azure Multi-factor Authentication, si ve el nombre de hello del inquilino o el proveedor de MFA de Azure en hello queda con una  **+**  tooit siguiente, haga clic en hello  **+**  vea distintos grupos de replicación del servidor MFA y grupo de hello Azure de manera predeterminada. Seleccione grupo adecuado de Hola.
4. En Administración de usuarios, seleccione **Omisión por única vez**.
5. En la página omisión por única vez de hello, haga clic en **nueva omisión por única vez**.

  ![Nube](./media/multi-factor-authentication-whats-next/create1.png)

6. Escriba el nombre de usuario de hello, el número de Hola de segundos que Hola omisión se existe y Hola motivo de omisión de Hola. Haga clic en **Omitir**.
7. Hello límite de tiempo entra en vigor inmediatamente, ese usuario hello toosign necesidades en antes de Hola por única vez omisión expira. 

### <a name="view-hello-one-time-bypass-report"></a>Hola de vista única omitir informes
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Hola izquierda, seleccione Active Directory.
3. En, seleccione superior hello **proveedores de autenticación multifactor**. Aparecerá una lista de los proveedores de Multi-Factor Authentication.
4. Seleccione el proveedor de autenticación multifactor y haga clic en **administrar** final Hola de página Hola. se abrirá el Portal de administración de Azure Multi-factor Authentication Hola.
5. En el Portal de administración de Azure Multi-factor Authentication, de Hola Hola izquierda, bajo ver un informe, haga clic en **omisión por única vez**.
6. Especifique el intervalo de fechas de Hola que desea tooview en informe de Hola. También puede especificar nombres de usuario, los números de teléfono y estado del usuario de Hola.
7. Haga clic en **Ejecutar**. Aparecerá un informe de las omisiones. Haga clic en **exportar tooCSV** si desea que el informe de hello tooexport.

## <a name="custom-voice-messages"></a>Mensajes de voz personalizados
Mensajes de voz personalizados le permiten toouse sus propias grabaciones o greetings para verificación en dos pasos. Se pueden usar en los registros de Microsoft de suma tooor tooreplace Hola.

Antes de empezar tenga Hola siguiente:

* formatos de archivo de Hello compatibles son .wav y. mp3.
* límite de tamaño de archivo de Hello es 5 MB.
* Los mensajes de autenticación deben durar menos de 20 segundos. Hola comprobación toofail nada más larga podría producir porque el usuario de hello quizás no responda antes de hello mensaje finaliza, provocando Hola comprobación tootime out.

### <a name="set-up-a-custom-message"></a>Configuración de un mensaje personalizado

Hay dos toocreating partes de su mensaje personalizado. En primer lugar, cargue el mensaje de bienvenida y, a continuación, activarla para los usuarios.

tooupload su mensaje personalizado:

1. Cree un mensaje de voz personalizados utilizando uno de los formatos de archivo de hello admitida.
2. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
3. Navegue toohello Portal de administración de MFA por instrucciones de hello en la parte superior de Hola de esta página.
4. En el Portal de administración de Azure Multi-factor Authentication hello, haga clic en **mensajes de voz** en hello sección de configuración.
5. En configurar hello: página de mensajes de voz, haga clic en **nuevo mensaje de voz**.
   ![Nube](./media/multi-factor-authentication-whats-next/custom1.png)
6. En configurar hello: página nuevos mensajes de voz, haga clic en **administrar archivos de sonido**.
   ![Nube](./media/multi-factor-authentication-whats-next/custom2.png)
7. En hello configurar: archivos de sonido, haga clic en **cargar archivo de sonido**.
   ![Nube](./media/multi-factor-authentication-whats-next/custom3.png)
8. En hello configurar: cargar archivo de sonido, haga clic en **examinar** y navegue tooyour mensaje de voz, haga clic en **abiertos**.
9. Agregue una descripción y haga clic en **Cargar**.
10. Una vez que se complete, un mensaje confirmará que se ha cargado correctamente el archivo hello.

mensaje de saludo tooturn en para los usuarios:

1. Hola izquierda, haga clic en **mensajes de voz**.
2. En la sección de mensajes de voz de hello, haga clic en **nuevo mensaje de voz**.
3. En hello lista desplegable idioma, seleccione un idioma.
4. Si este mensaje es para una aplicación específica, especifíquelo en el cuadro de la aplicación hello.
5. Desde la lista desplegable Tipo de mensaje de Hola, seleccione toobe de tipo de mensaje Hola que se reemplaza con el nuevo mensaje personalizado.
6. En hello desplegable archivo de sonido, seleccione archivo de sonido de Hola que ha cargado en la primera parte de Hola.
7. Haga clic en **Crear**. Un mensaje confirmará que ha creado correctamente un mensaje de voz.
    ![Nube](./media/multi-factor-authentication-whats-next/custom5.png)</center>

## <a name="caching-in-azure-multi-factor-authentication"></a>Almacenamiento en caché en Azure Multi-Factor Authentication
Almacenamiento en caché permite tooset un período de tiempo específico para que los intentos de autenticación posteriores dentro de ese período de tiempo correctos automáticamente. Esto se usa principalmente cuando los sistemas locales como VPN de envían varias solicitudes de comprobación mientras la primera solicitud de hello aún está en curso. Esto permite hello las solicitudes posteriores toosucceed automáticamente después de usuario de Hola se realiza correctamente la primera comprobación de hello en curso. 

Almacenamiento en caché no está previsto toobe que se usa para inicios de sesión tooAzure AD.

### <a name="set-up-caching"></a>Configuración del almacenamiento en caché 
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Navegue toohello Portal de administración de MFA por instrucciones de hello en la parte superior de Hola de esta página.
3. En el Portal de administración de Azure Multi-factor Authentication hello, haga clic en **Caching** en hello sección de configuración.
4. En hello configurar almacenamiento en caché de página haga clic en **nueva caché**.
5. Seleccionar tipo de caché de Hola y segundos en caché Hola. Haga clic en **Crear**.

<center>![Nube](./media/multi-factor-authentication-whats-next/cache.png)</center>

## <a name="trusted-ips"></a>IP de confianza
IP de confianza es una característica de Azure MFA que los administradores de un inquilino administrado o federado pueden usar verificacion de toobypass para los usuarios que inician sesión desde la intranet local de la compañía de Hola. Esta característica está disponible con la versión completa de Hola de autenticación multifactor de Azure, no Hola versión gratuita para administradores. Para obtener detalles sobre cómo tooget Hola versión completa de la autenticación multifactor Azure, consulte [la autenticación multifactor Azure](multi-factor-authentication.md).

| Tipo de un inquilino de Azure AD. | Opciones de IP de confianza disponibles |
|:--- |:--- |
| Administrado |<li>Intervalos de direcciones IP específicos, los administradores pueden especificar un intervalo de direcciones IP que se puede omitir la comprobación de dos pasos para los usuarios que inician sesión desde la intranet de la compañía de Hola.</li> |
| Federado |<li>Todos los usuarios de federado: todos los usuarios federados que inician sesión en desde dentro de hello organización omiten verificacion usando una notificación emitida por AD FS.</li><br><li>Intervalos de direcciones IP específicos, los administradores pueden especificar un intervalo de direcciones IP que se puede omitir la comprobación de dos pasos para los usuarios que inician sesión desde la intranet de la compañía de Hola. |

Esta omisión solo funciona desde dentro de la intranet de una empresa. Por ejemplo, si ha seleccionado usuarios federados todos los, y un usuario inicia sesión desde la intranet de la compañía de hello exterior, ese usuario tiene tooauthenticate mediante la verificación en dos pasos aunque Hola presente una notificación de AD FS. 

**Experiencia del usuario final en la red corporativa:**

Si IP de confianza se deshabilita, se requiere la verificación en dos pasos para los flujos del explorador y se requieren las contraseñas de aplicación para las aplicaciones de cliente antiguas. 

Cuando se habilita la IP de confianza, verificación en dos pasos es *no* necesarios para flujos de explorador, y las contraseñas de aplicación hay *no* necesarios para las aplicaciones de cliente enriquecido anteriores, siempre que hello usuario no ha ya ha creado un contraseña de aplicación. Una vez que una contraseña de aplicación está en uso, es necesaria. 

**Experiencia del usuario final fuera de la red corporativa:**

Independientemente de que IP de confianza esté habilitado, se requiere la verificación en dos pasos para los flujos del explorador y se requieren las contraseñas de aplicación para las aplicaciones de cliente antiguas. 

### <a name="tooenable-trusted-ips"></a>tooenable direcciones IP de confianza
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Navegar por páginas de configuración de servicio de MFA de toohello por instrucciones de hello en principio Hola de este artículo.
3. En la página de configuración del servicio de hello en IP de confianza, tiene dos opciones:
   
   * **Para las solicitudes de usuarios federados que se originan en mi intranet** : casilla Hola. Todos los usuarios federados que inician sesión desde la red corporativa de hello omiten verificacion usando una notificación emitida por AD FS.
   * **Para las solicitudes de un intervalo específico de direcciones IP públicas** : escriba las direcciones IP de hello en hello cuadro de texto utilizando la notación CIDR. Por ejemplo: xxx.xxx.xxx.0/24 para direcciones IP en el intervalo de hello xxx.xxx.xxx.1 a xxx.xxx.xxx.254, o xxx.xxx.xxx.xxx/32 para una única dirección IP. Puede escribir un máximo de too50 los intervalos de direcciones IP. Los usuarios que inician sesión desde estas direcciones IP omiten la comprobación en dos pasos.
4. Haga clic en **Guardar**.
5. Una vez que se han aplicado las actualizaciones de hello, haga clic en **cerrar**.

![IP de confianza](./media/multi-factor-authentication-whats-next/trustedips3.png)

## <a name="app-passwords"></a>Contraseñas de aplicación
Algunas aplicaciones, como Office 2010, o las versiones anteriores, y Apple Mail, no admiten la comprobación en dos pasos, No configurado tooaccept una segunda comprobación. toouse estas aplicaciones, necesita toouse "contraseñas de aplicación" en lugar de la contraseña tradicionales. contraseña de aplicación Hola permite toobypass de aplicación Hola verificación en dos pasos y seguir trabajando.

> [!NOTE]
> Autenticación moderna Hola clientes de Office 2013
> 
> Clientes de Office 2013 (como Outlook) y protocolos de autenticación moderna de compatibilidad más reciente y puede tener habilitado toowork con verificación en dos pasos. Una vez habilitada esta opción, estos clientes no necesitan contraseñas de aplicación.  Para más información, consulte [Anuncio de la versión preliminar pública de la autenticación moderna de Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).

### <a name="important-things-tooknow-about-app-passwords"></a>Tooknow aspectos importantes acerca de las contraseñas de aplicación
Hola aquí te mostramos una lista de los aspectos que debe saber acerca de las contraseñas de aplicación importante.

* Las contraseñas de aplicación sólo deberían ser necesario toobe introducido una vez por cada aplicación. Los usuarios no tiene tookeep realizar un seguimiento de ellos y escribirlas cada vez.
* contraseña real Hola se genera automáticamente y no se proporciona por el usuario de Hola. Esto es porque la contraseña generada automáticamente hello es más difícil que un atacante tooguess y es más seguro.
* Hay un límite de 40 contraseñas por usuario. 
* Aplicaciones que las contraseñas y el uso en escenarios locales puede empiezan a generar errores ya que no se conoce contraseña de aplicación Hola fuera de Id. de organización de hello en caché. Un ejemplo es que los mensajes de correo electrónico de Exchange son locales pero correo de hello archivado se encuentra en la nube de Hola. Hola no funciona la misma contraseña.
* Una vez habilitada la autenticación multifactor en una cuenta de usuario, las contraseñas de aplicación pueden usarse con la mayoría de los clientes que no son explorador, como Outlook y Lync, pero no se puede realizar acciones administrativas con contraseñas de aplicación a través de aplicaciones que no son explorador, como Windows PowerShell, incluso si ese usuario tiene una cuenta administrativa.  Asegúrese de crear una cuenta de servicio con una secuencia de comandos de PowerShell de toorun de contraseña segura y no habilite esa cuenta para la verificación en dos pasos.

> [!WARNING]
> Las contraseñas de aplicación no funcionan en entornos híbridos donde los clientes se comunican tanto en el entorno local como en los puntos de conexión de detección automática en la nube. Esto es porque las contraseñas de dominio están tooauthenticate necesaria en las instalaciones y contraseñas de aplicación son necesario tooauthenticate con la nube de Hola.

### <a name="naming-guidance-for-app-passwords"></a>Guía de nomenclatura para las contraseñas de aplicación
Nombres de contraseña de aplicación reflejen dispositivo hello en el que se utilizan. Por ejemplo, si tiene un portátil con aplicaciones sin explorador como Outlook, Word y Excel, cree una contraseña de aplicación denominada Portátil y utilícela en todas estas aplicaciones. A continuación, cree otra contraseña de aplicación denominada Desktop para hello mismas aplicaciones en el equipo de escritorio. 

Microsoft recomienda crear una contraseña de aplicación por dispositivo, no por aplicación.

### <a name="federated-sso-app-passwords"></a>Contraseñas de aplicación federada (SSO)
Azure AD admite la federación (inicio de sesión único) con Active Directory Domain Services (AD DS) de Windows Server. Si su organización está federada con Azure AD y va toobe mediante la autenticación multifactor de Azure y luego Hola siguiente información acerca de las contraseñas de aplicación es importante para usted. Esta sección solo aplica a los clientes de toofederated (SSO).

* Las contraseñas de aplicación las comprueba Azure AD y, por tanto, se omite la federación. La federación solo se usa activamente al configurar la contraseñas de aplicación.
* Para los usuarios federados de (SSO), nunca se vaya toohello proveedor de identidades (IdP) a diferencia del flujo pasivo Hola. las contraseñas de Hola se almacenan en el Id. de organización de Hola. Si el usuario de hello deja la empresa de hello, esa información tiene Id. de tooorganizational tooflow mediante DirSync en tiempo real. La deshabilitación o eliminación de cuenta puede tardar toothree horas toosync, lo que se retrasa la deshabilitación o eliminación de contraseña de aplicación en Azure AD.
* La configuración del control de acceso de cliente local no admite la contraseña de aplicación
* La contraseña de aplicación no tiene la ninguna funcionalidad de auditoría o registro de autenticación local.
* Puede que algunos diseños arquitectónicos avanzados requieran una combinación de nombre de usuario y contraseñas de la organización, y de contraseñas de aplicación cuando se usa comprobación en dos pasos con clientes, en función de dónde se autentiquen. Para los clientes que se autentican en una infraestructura local, usaría un nombre de usuario y una contraseña de la organización. Para los clientes que se autentican en Azure AD, usaría la contraseña de aplicación Hola.

  Por ejemplo, suponga que tiene una arquitectura que consta de hello siguiente:

  * Tiene federada su instancia local de Active Directory con Azure AD
  * Usa Exchange Online
  * Usa Lync que es específicamente local
  * Usa Azure Multi-Factor Authentication

  ![Página de proofup](./media/multi-factor-authentication-whats-next/federated.png)

  En estos casos, debe hacer los siguiente hello:

  * Al firmar-en tooLync, use el nombre de usuario y la contraseña de su organización.
  * Al tratar de libreta de direcciones de hello tooaccess a través de un cliente de Outlook que se conecta tooExchange en línea, use una contraseña de aplicación.

### <a name="allow-app-password-creation"></a>Permiso para la creación de contraseñas de aplicación
De forma predeterminada, los usuarios no pueden crear contraseñas de aplicación. Esta característica debe habilitarse. usuarios de tooallow Hola contraseñas de aplicación de capacidad toocreate, usar hello siguiendo el procedimiento:

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Navegar por páginas de configuración de servicio de MFA de toohello por instrucciones de hello en principio Hola de este artículo.
3. Seleccione a continuación el botón de opción de hello demasiado**permitir toosign de las contraseñas de aplicación de los usuarios toocreate en aplicaciones sin explorador**.

![Crear contraseñas de aplicación](./media/multi-factor-authentication-whats-next/trustedips3.png)

### <a name="create-app-passwords"></a>Creación de contraseñas de aplicación
Los usuarios pueden crear contraseñas de aplicación durante el registro inicial. Tienen una opción al final de Hola Hola del proceso de registro que les permita toocreate las contraseñas de aplicación.

Los usuarios también pueden crear contraseñas de aplicación después del registro cambiando su configuración en el portal de Office 365 portal o hello Azure Hola. Para más información e instrucciones detalladas para los usuarios, consulte [¿Qué son las contraseñas de aplicación en Azure Multi-Factor Authentication?](./end-user/multi-factor-authentication-end-user-app-passwords.md).

## <a name="remember-multi-factor-authentication-for-devices-that-users-trust"></a>Recuerdo de Multi-Factor Authentication para los dispositivos en los que los usuarios confían
Recordar Multi-Factor Authentication para los dispositivos y exploradores en los que los usuarios confían es una característica gratuita para todos los usuarios de MFA. Le permite la opción de hello toogive usuarios MFA tooby fase durante un número determinado de días después de realizar una correcta mediante MFA de inicio de sesión. Esto puede mejorar la facilidad de uso minimizando Hola número de veces que un usuario puede realizar la verificación en dos pasos en hello mismo dispositivo.

Sin embargo, si una cuenta o un dispositivo corren peligro, el hecho de recordar MFA para los dispositivos de confianza puede afectar a la seguridad. Si una cuenta corporativa se pone en peligro o un dispositivo de confianza es objeto de pérdida o robo, debe [restaurar Multi-Factor Authentication en todos los dispositivos](multi-factor-authentication-manage-users-and-devices.md#restore-mfa-on-all-remembered-devices-for-a-user). Esta acción revoca Hola confianza estado de todos los dispositivos y usuario hello es tooperform requiere dos pasos una prueba de nuevo. También puede indicar su toorestore usuarios MFA en sus propios dispositivos con instrucciones de hello en [administrar la configuración de verificación en dos pasos](./end-user/multi-factor-authentication-end-user-manage-settings.md#require-two-step-verification-again-on-a-device-youve-marked-as-trusted)

### <a name="how-it-works"></a>Cómo funciona

Teniendo en cuenta la autenticación multifactor funciona estableciendo una cookie persistente en el Explorador de hello cuando un usuario protege hello "no volver a preguntar para **X** días" cuadro en el inicio de sesión. usuario de Hello no se pedirán MFA nuevo desde ese explorador hasta que expire la cookie de Hola. Si el usuario de hello abre un explorador diferente en Hola mismo dispositivo o borra sus cookies, vuelven a estar tooverify solicitada. 

Hola "no volver a preguntar para **X** días" casilla de verificación no se muestre en aplicaciones sin explorador, si no admite la autenticación moderna. Estas aplicaciones usan tokens de actualización que proporcionan nuevos tokens de acceso cada hora. Cuando se valida un token de actualización, las comprobaciones de Azure AD que Hola verificacion última hora realiza fue en número de hello configurado de días. 

Por lo tanto, teniendo en cuenta MFA en dispositivos de confianza reduce el número de Hola de autenticaciones en las aplicaciones web (que normalmente le pregunte cada vez) pero aumenta Hola número de autenticaciones para que los clientes de moderno-auth (que normalmente solicitar cada 90 días).

> [!NOTE]
>Esta característica no es compatible con la característica de "Mantener la sesión iniciada" hello de AD FS cuando los usuarios realizan la verificación en dos pasos para AD FS mediante servidor Azure MFA Hola o una solución MFA de terceros. Si los usuarios seleccionar la opción "Mantener la sesión iniciada" en AD FS y marcar su dispositivo como de confianza para MFA, estos no ser capaz de tooverify después de que expire Hola número "Recordar MFA" de días. Azure AD solicita una comprobación de nuevo en dos pasos, pero AD FS devuelve un token con notificaciones MFA de hello original y la fecha en lugar de realizar de nuevo la verificación en dos pasos. Como consecuencia se crea un bucle de comprobación entre Azure AD y AD FS. 

### <a name="enable-remember-multi-factor-authentication"></a>Habilitación del recuerdo de la autenticación multifactor
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Navegar por páginas de configuración de servicio de MFA de toohello por instrucciones de hello en principio Hola de este artículo.
3. En la página de configuración del servicio de hello, en administrar la configuración de dispositivos de usuario, compruebe hello **permitir que los usuarios tooremember la autenticación multifactor en dispositivos de confianza** cuadro.
   ![Recordar dispositivos](./media/multi-factor-authentication-whats-next/remember.png)
4. Establecer Hola número de días que desea que tooallow Hola confianza dispositivos toobypass verificacion. valor predeterminado de Hello es 14 días.
5. Haga clic en **Guardar**.
6. Haga clic en **Cerrar**.

### <a name="mark-a-device-as-trusted"></a>Marca de un dispositivo como de confianza

Una vez que se habilitar esta característica, los usuarios pueden marcar un dispositivo como de confianza cuando inician sesión. Para ello, solo deben activar **Don't ask again** (No volver a preguntar).

![No volver a preguntar (captura de pantalla)](./media/multi-factor-authentication-whats-next/trusted.png)

## <a name="selectable-verification-methods"></a>Métodos de verificación seleccionables
Puede elegir los métodos de verificación que pueden emplear los usuarios. tabla de Hello siguiente proporciona una breve descripción de cada método.

Cuando los usuarios inscriben en sus cuentas para MFA, deciden su método de comprobación preferida fuera de las opciones de Hola que ha habilitado. Guía de Hola para su proceso de inscripción se trata en [configurar mi cuenta para la verificación en dos pasos](multi-factor-authentication-end-user-first-time.md)

| Método | Descripción |
|:--- |:--- |
| Llamar a toophone |Hace una llamada de voz automática. Hola usuario respuestas Hola llamar y presiona # en hello phone teclado tooauthenticate. Este número de teléfono no está sincronizada tooon-local de Active Directory. |
| Toophone de mensaje de texto |Envía un mensaje de texto que contiene un código de verificación. usuario de Hello es mensaje de texto toohello tooeither solicitadas de respuesta con código de comprobación de Hola o código de comprobación de hello tooenter en interfaz de inicio de sesión de Hola. |
| Notificación a través de aplicación móvil |Envía un teléfono de tooyour de notificación de inserción o dispositivo registrado. vistas de notificación de Hola Hola usuario y selecciona **compruebe** toocomplete comprobación. <br>está disponible para la aplicación de Microsoft Authenticator Hello [de Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), y [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |
| Código de comprobación desde aplicación móvil |aplicación de Microsoft Authenticator Hello genera un nuevo código de comprobación de OATH cada treinta segundos. usuario de Hello entra en este código de comprobación en la interfaz de inicio de sesión de Hola.<br>está disponible para la aplicación de Microsoft Authenticator Hello [de Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), y [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |

### <a name="how-tooenabledisable-authentication-methods"></a>¿Cómo tooenable o deshabilitar los métodos de autenticación
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Navegar por páginas de configuración de servicio de MFA de toohello por instrucciones de hello en principio Hola de este artículo.
3. En la página de configuración del servicio de hello, en las opciones de comprobación, seleccione/anule la selección de opciones de hello desea toouse.
   ![Opciones de verificación](./media/multi-factor-authentication-whats-next/authmethods.png)
4. Haga clic en **Guardar**.
5. Haga clic en **Cerrar**.

