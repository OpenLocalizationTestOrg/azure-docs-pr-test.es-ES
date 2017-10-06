---
title: "Profundización: SSPR de Azure AD | Microsoft Docs"
description: "Profundización del autoservicio de restablecimiento de contraseña de Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 618c5908-5bf6-4f0d-bf88-5168dfb28a88
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: c177192bbe69d179a25d174b06a0813ec28e2615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-password-reset-in-azure-ad-deep-dive"></a>Profundización del autoservicio de restablecimiento de contraseña de Azure AD

Funcionamiento de SSPR ¿Qué significa que la opción de interfaz de hello? Seguir leyendo toofind más información acerca de la contraseña de autoservicio de Azure AD restablecer.

## <a name="how-does-hello-password-reset-portal-work"></a>Cómo restablecer contraseña Hola trabajo portal

Cuando un usuario navega toohello portal de restablecimiento de contraseña, un flujo de trabajo es iniciado toodetermine:

   * ¿Cómo se debe traducir página Hola?
   * ¿Es la cuenta de usuario de hello válido?
   * ¿Qué organización pertenece usuario Hola a?
   * ¿Donde se administra la contraseña del usuario de hello?
   * ¿Es la característica de Hola de toouse con licencia de usuario de hello?


Lea estos pasos hello toolearn acerca de la lógica de hello detrás de la página de restablecimiento de contraseña de Hola.

1. El usuario hace clic Hola no puede acceder a su vínculo de la cuenta o va directamente demasiado[https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com).
2. Basado en Hola de configuración regional del explorador de hello experiencia se representa en el idioma correspondiente de Hola. Hello experiencia de restablecimiento de contraseña se traducen Hola mismos idiomas que sea compatible con Office 365.
3. El usuario escribe un identificador de usuario y pasa un captcha.
4. Azure AD comprueba si el usuario de hello toouse capaz de esta característica haciendo Hola siguiente:
   * Comprueba que el usuario hello tiene esta característica está habilitada y asignada una licencia de Azure AD.
     * Si el usuario de hello no tiene esta característica está habilitada o una licencia asignada, usuario de hello es más frecuentes toocontact su tooreset administrador su contraseña.
   * Comprueba que el usuario hello tiene datos de desafío derecho Hola definidos en su cuenta de acuerdo con la directiva del administrador.
     * Si la directiva requiere solo un desafío, se asegura que el usuario hello tiene datos correspondientes Hola definidos para al menos uno de los desafíos de hello habilitados por la directiva del Administrador de Hola.
       * Si el usuario de hello no está configurado, Hola usuario es aconsejable toocontact su tooreset administrador su contraseña.
     * Si directiva Hola requiere dos desafíos, se asegura que el usuario hello tiene datos correspondientes Hola definidos para al menos dos de los desafíos de hello habilitados por la directiva del Administrador de Hola.
       * Si Hola usuario no está configurado, entonces se Hola usuario es aconsejable toocontact su tooreset administrador su contraseña.
   * Comprueba si la contraseña del usuario de Hola se administra de forma local (federados o sincronizados de hash de contraseña).
     * Si la escritura diferida está implementada y la contraseña del usuario de Hola se administra de forma local, el usuario de Hola se permite tooproceed tooauthenticate y restablece su contraseña.
     * Si no se ha implementado la escritura diferida y contraseña del usuario de Hola se administra de forma local, entonces es usuario de Hola más frecuentes toocontact su tooreset administrador su contraseña.
5. Si se determina que el usuario hello es capaz de toosuccessfully restablecer su contraseña, a continuación, Hola se le guía en el proceso de restablecimiento de Hola.

## <a name="authentication-methods"></a>Métodos de autenticación

Si está habilitado el restablecimiento de contraseña de autoservicio (SSPR), debe seleccionar al menos una de las siguientes opciones para los métodos de autenticación de Hola. Se recomienda encarecidamente elegir al menos dos métodos de autenticación para que los usuarios tengan más flexibilidad.

* Email
* Teléfono móvil
* Teléfono del trabajo
* Preguntas de seguridad

### <a name="what-fields-are-used-in-hello-directory-for-authentication-data"></a>Qué campos se utilizan en el directorio de Hola para datos de autenticación

* Teléfono del trabajo correspondiente tooOffice teléfono
    * Los usuarios son no se puede tooset este campo propios debe definirse por un administrador
* Teléfono móvil corresponde tooeither teléfono de autenticación (no visible públicamente) o un teléfono móvil (visible públicamente)
    * servicio de Hello busca primero el teléfono de autenticación, a continuación, vuelve tooMobile teléfono si no está presente
* Dirección de correo electrónico alternativa corresponde tooeither correo electrónico de autenticación (no visible públicamente) o correo electrónico alternativa
    * servicio de Hello busca primero el correo electrónico de autenticación, a continuación, se produce un error tooAlternate back-correo electrónico

De forma predeterminada, solo Hola nube atributos teléfono del trabajo y el teléfono móvil sincronizan tooyour directorio en la nube de su directorio local para los datos de autenticación.

Los usuarios pueden solo restablecer su contraseña si tienen datos presentes en los métodos de autenticación de Hola que Administrador de hello habilitó y requiere.

Si los usuarios no desea que sus toobe de número de teléfono móvil visible en el directorio de hello pero sería como toouse, para restablecer la contraseña, los administradores no deben rellenarla en directorio de hello y, a continuación, debe rellenar el usuario Hola sus **teléfono de autenticación**  atributo a través de hello [portal de registro de restablecimiento de contraseña](http://aka.ms/ssprsetup). Los administradores pueden ver esta información en el perfil de usuario de hello pero no está publicada en otra parte. Si una cuenta de administrador de Azure registra el número de teléfono de autenticación, se rellena en el campo de teléfono móvil de Hola y es visible.

### <a name="number-of-authentication-methods-required"></a>Número de métodos de autenticación requeridos

Esta opción determina el número mínimo de Hola de métodos de autenticación disponibles Hola un usuario debe superar tooreset o desbloquear su contraseña y se puede establecer tooeither 1 o 2.

Los usuarios pueden elegir toosupply más métodos de autenticación si están habilitadas por el Administrador de Hola.

Si un usuario no tiene métodos de hello mínimo necesario registrados, verá una página de error que hay que les dirija toorequest un tooreset administrador su contraseña.

### <a name="how-secure-are-my-security-questions"></a>Nivel de protección de las cuestiones de seguridad

Si usas preguntas de seguridad, se recomienda ellos en uso con otro método que pueden ser menos seguras que otros métodos puesto que algunas personas pueden saber respuestas hello tooanother preguntas de los usuarios.

> [!NOTE] 
> Preguntas de seguridad se almacenan de forma privada y segura en un objeto de usuario en el directorio de Hola y solo las pueden responder los usuarios durante el registro. No hay ninguna manera de que un administrador tooread o modificar un usuario preguntas o respuestas.
>

### <a name="security-question-localization"></a>Localización de preguntas de seguridad

Todas las preguntas predefinidas que siguen están localizadas en el conjunto completo de Hola de idiomas de Office 365 en función de la configuración regional del explorador del usuario de Hola.

* ¿En qué ciudad conoció a su cónyuge o pareja?
* ¿En qué ciudad se conocieron sus padres?
* ¿En qué ciudad vive su hermano más próximo?
* ¿En qué ciudad nació su padre?
* ¿En qué ciudad tuvo su primer trabajo?
* ¿En qué ciudad nació su madre?
* ¿En qué ciudad estaba en la Nochevieja del año 2000?
* ¿Cuál es Hola apellido de su profesor favorito en alto * centro educativo?
* ¿Qué es el nombre de Hola de una universidad aplicados toobut no asistió?
* ¿Cuál es el nombre de hello del lugar de hello en el que celebró su primer matrimonio?
* ¿Cuál es el segundo apellido de su padre?
* ¿Cuál es su comida favorita?
* ¿Cuál es el nombre y apellido de su abuela materna?
* ¿Cuál es el segundo apellido de su madre?
* ¿Cuáles son el año y mes de nacimiento del mayor de sus hermanos? (por ejemplo, noviembre de 1985)
* ¿Cuál es el segundo apellido del mayor de sus hermanos?
* ¿Cuál es el nombre y apellido de su abuelo paterno?
* ¿Cuántos años se lleva con el menor de sus hermanos?
* ¿En qué escuela cursó el sexto curso?
* ¿Qué salió Hola nombre y apellido de su mejor amigo de la infancia?
* ¿Qué salió Hola nombre y apellido de su primera pareja?
* ¿Cuál era el apellido de Hola de su maestro de primaria favorito?
* ¿Cuál era la marca de Hola y el modelo de su primer coche o moto?
* ¿Cuál era llamaba Hola Hola primera escuela a la que asistió?
* ¿Cuál era el nombre de Hola de salud de hello en el que nació?
* ¿Cuál era el nombre de Hola de calle de Hola de su primera casa de la infancia?
* ¿Cuál era el nombre de Hola de su héroe de la infancia?
* ¿Cuál era el nombre de Hola de su peluche favorito?
* ¿Cuál era el nombre de Hola de su primera mascota?
* ¿Cuál era su apodo en la infancia?
* ¿Cuál era su deporte favorito en el instituto?
* ¿Cuál fue su primer trabajo?
* ¿Qué se Hola últimos cuatro dígitos de su número de teléfono de la infancia?
* Cuando era joven, ¿qué quería toobe mayor?
* ¿Cuál es Hola persona más famosa que ha conocido?

### <a name="custom-security-questions"></a>Preguntas de seguridad personalizadas

Las preguntas de seguridad personalizadas no se localizan para diferentes configuraciones regionales. Se muestran todas las preguntas personalizadas en hello mismo idioma que se escriben en la interfaz de usuario administrativo de hello incluso si la configuración regional del explorador del usuario de hello es diferente. Si tiene preguntas localizados, use preguntas Hola predefinido.

longitud máxima de Hola de una pregunta de seguridad personalizado es de 200 caracteres.

### <a name="security-question-requirements"></a>Requisitos de las preguntas de seguridad

* El límite mínimo de caracteres de las respuestas es de 3 caracteres
* El límite máximo de caracteres de las respuestas es de 40 caracteres
* Los usuarios no pueden responder a Hola misma pregunta de más de una vez
* Los usuarios no pueden proporcionar Hola mismo responder toomore a una pregunta
* Puede ser cualquier conjunto de caracteres usado toodefine preguntas y respuestas, incluidos los caracteres Unicode
* número de Hola de preguntas definidas debe ser mayor que o igual a toohello número de preguntas necesario tooregister

## <a name="registration"></a>Registro

### <a name="require-users-tooregister-when-signing-in"></a>Requerir a los usuarios tooregister cuando inicien sesión en

Si se habilita esta opción requiere que un usuario que está habilitado para contraseña restablece registro de restablecimiento de contraseña de hello toocomplete si iniciar sesión tooapplications con Azure AD toosign en como las siguientes:

* Office 365
* Azure Portal
* Panel de acceso
* Aplicaciones federadas
* Aplicaciones personalizadas mediante Azure AD

Deshabilitar esta característica seguirá permitiendo a los usuarios toomanually registrar su información de contacto, visita [http://aka.ms/ssprsetup](http://aka.ms/ssprsetup) o haciendo clic en hello **registrarse para restablecer la contraseña** vínculo situado bajo Hola pestaña de perfil en el panel de acceso de Hola.

> [!NOTE]
> Los usuarios pueden descartar el portal de registro de restablecimiento de contraseña de hello haciendo clic en Cancelar o cerrando una ventana hello pero se les solicita cada vez que inicie sesión hasta que terminen de registro.
>

### <a name="number-of-days-before-users-are-asked-tooreconfirm-their-authentication-information"></a>Número de días antes de que los usuarios son más frecuentes tooreconfirm su información de autenticación

Esta opción determina Hola período de tiempo entre la configuración y confirmando la información de autenticación y solo está disponible si habilita hello **requieren tooregister a los usuarios cuando inician sesión en** opción.

Los valores válidos son 0 y 730 días, y 0 significa no preguntar a los usuarios tooreconfirm su información de autenticación

## <a name="notifications"></a>Notificaciones

### <a name="notify-users-on-password-resets"></a>¿Quiere notificar a los usuarios los restablecimientos de contraseña?

Si esta opción se establece tooyes, usuario de Hola que está restableciendo la contraseña recibe un correo electrónico que les informa de que se ha cambiado su contraseña a través de hello SSPR tootheir portal principal y direcciones de correo electrónico alternativa en el archivo en Azure AD. A ningún otro usuario se le informa de este evento de restablecimiento.

### <a name="notify-all-admins-when-other-admins-reset-their-passwords"></a>Notificación a todos los administradores cuando otros administradores restablecen sus contraseñas

Si esta opción se establece tooyes, entonces **todos los administradores** recibir una dirección de correo electrónico principal de tootheir de correo electrónico en el archivo en Azure AD que les informa de que otro administrador ha cambiado su contraseña mediante Autoservicio.

Ejemplo: hay cuatro administradores en un entorno. El administrador "A" restablece su contraseña mediante SSPR. Los administradores B, C y D reciben un correo electrónico que les alertan de que esto ocurre.

## <a name="on-premises-integration"></a>Integración local

Si ha instalado, configurado y habilitado Azure AD Connect, tendrá más opciones para las integraciones locales.

### <a name="write-back-passwords-tooyour-on-premises-directory"></a>Escritura diferida de directorio local de contraseñas tooyour

Controla si no está habilitada la escritura diferida de contraseñas para este directorio y, si lo está, indica el estado de Hola de servicio de escritura diferida de hello en local. Esto es útil si desea tootemporarily Deshabilitar reescritura de contraseña de hello sin volver a configurar Azure AD Connect.

* Si cambia de hello es tooyes de conjunto, reescritura se habilita y se federado y sincronizado de hash de contraseña a los usuarios será capaz de tooreset sus contraseñas.
* Si cambia de hello es toono de conjunto, reescritura se deshabilita y se federado y sincronizado de hash de contraseña a los usuarios no será capaz de tooreset sus contraseñas.

### <a name="allow-users-toounlock-accounts-without-resetting-their-password"></a>Permitir que a los usuarios toounlock cuentas sin restablecer la contraseña

Indica si los usuarios que visitan el portal de restablecimiento de contraseña de hello deben ser Hola determinada opción toounlock su Active Directory local cuentas sin restablecer la contraseña. De forma predeterminada, Azure AD siempre desbloqueará cuentas al realizar un restablecimiento de contraseña, esta configuración le permite tooseparate esas dos operaciones. 

* Si establece demasiado "Sí", a continuación, los usuarios se Hola determinada opción tooreset su contraseña y desbloquear la cuenta de hello, o toounlock sin restablecer la contraseña de Hola.
* Si se establece demasiado "no", los usuarios solo será capaz de tooperform un restablecimiento de contraseña combinado y la cuenta de operación de desbloqueo.

## <a name="network-requirements"></a>Requisitos de red

### <a name="firewall-rules"></a>Reglas de firewall

[Lista de direcciones IP y direcciones URL de Microsoft Office](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)

Para Azure AD Connect versión 1.1.443.0 y versiones posteriores, se necesita la salida siguiente de toohello de acceso HTTPS
* passwordreset.microsoftonline.com
* servicebus.windows.net

Para un acceso más detallado, puede encontrar Hola actualizar lista del centro de datos de intervalos IP Microsoft Azure que se actualiza todos los miércoles y colocado en el siguiente de hello efecto el lunes [aquí](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="idle-connection-timeouts"></a>Tiempos de espera de conexiones inactivas

herramienta de Hello Azure AD Connect envía pings/keepalive periódica tooServiceBus extremos tooensure que las conexiones de Hola se mantengan activos. Debería herramienta Hola detectar que se está eliminadas demasiadas conexiones, automáticamente aumentará frecuencia Hola de punto de conexión de ping toohello. Hola más bajo 'hacer ping en intervalos' quita toois 1 ping cada 60 segundos, sin embargo, recomendamos encarecidamente que los servidores proxy o firewalls permiten toopersist de conexiones inactivas de al menos 2 a 3 minutos. *En el caso de las versiones anteriores, se sugiere una persistencia de 4 minutos, o más.

## <a name="active-directory-permissions"></a>Permisos de Active Directory

Hello cuenta especificada en la utilidad de hello Azure AD Connect debe tener restablecer contraseña, cambiar la contraseña, escribir permisos en lockoutTime y permisos de escritura en pwdLastSet, derechos en cualquiera de los objetos raíz Hola de extendidos **cada dominio** en ese bosque **o** en unidades organizativas de usuarios de hello desea toobe en el ámbito de Autoservicio.

Si no está seguro de qué Hola cuenta anterior hace referencia a, abra la UI de configuración de Azure Active Directory Connect de Hola y haga clic en la opción de configuración de hello vista actual. cuenta de Hello que necesita tooadd permiso toois aparecen en "Sincronizar directorios"

Al establecer estos permisos permite cuenta de servicio del agente de administración Hola para cada contraseñas toomanage de bosque en nombre de las cuentas de usuario en ese bosque. **Si no tooassign estos permisos, a continuación, aunque parezca que reescritura toobe configurado correctamente, los usuarios encuentran errores al intentar toomanage sus contraseñas locales desde la nube de Hola.**

> [!NOTE]
> Puede tardar una hora de tooan o más de estos objetos de tooall de tooreplicate de permisos en el directorio.
>

tooset los permisos adecuados de Hola para toooccur de reescritura de contraseña

1. Abra Usuarios y equipos de usuarios de Active Directory con una cuenta que tenga permisos de administración de dominio adecuado de Hola
2. Desde el menú de vista de hello, asegúrese de que está activado características avanzadas
3. En el panel izquierdo de hello, haga clic en el objeto de Hola que representa la raíz de Hola de dominio de Hola y elija Propiedades
    * Haga clic en la ficha seguridad de Hola
    * Luego, haga clic en Opciones avanzadas.
4. Desde la ficha de permisos de hello, haga clic en Agregar
5. Seleccionar cuenta de hello que se aplican permisos demasiado (desde el programa de instalación de Azure AD Connect)
6. En Hola se aplica toodrop cuadro desplegable, seleccione objetos de usuario descendiente
7. En permisos, casillas Hola siguientes Hola
    * Contraseña sin expiración
    * Restablecimiento de contraseña
    * Cambiar contraseña
    * Escribir lockoutTime
    * Escribir pwdLastSet
8. Haga clic en Aplicar o Aceptar a través de tooapply y salga de los cuadros de diálogo abiertos.

## <a name="how-does-password-reset-work-for-b2b-users"></a>¿Cómo funciona el restablecimiento de contraseña para usuarios B2B?
El restablecimiento y cambio de contraseña son totalmente compatibles con todas las configuraciones de B2B.  Continúe leyendo para hello tres explícita B2B casos compatibles con el restablecimiento de contraseña.

1. **Los usuarios de una organización de socios comerciales con un inquilino de Azure AD existente** : si la organización de Hola se asocian con tiene un inquilino de Azure AD existente, se **respetar las directivas de restablecimiento de contraseña están habilitadas en dicho inquilino**. Para restablece toowork de contraseña, Hola asociado organización necesidades simplemente toomake seguro está habilitado el Autoservicio de Azure AD, que no es cargo adicional para los clientes de Office 365, y puede habilitarse siguiendo los pasos de Hola de nuestro [Introducción a administración de contraseñas ](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords) guía.
2. **Los usuarios que se registró mediante [registro de autoservicio](active-directory-self-service-signup.md)**  : si la organización de Hola se asocian con usó hello [registro de autoservicio](active-directory-self-service-signup.md) tooget característica en un inquilino, se les permiten restablecer con correo electrónico de Hello registran.
3. **B2B usuarios** -los nuevos usuarios de B2B siguieron Hola nueva [capacidades de Azure AD B2B](active-directory-b2b-what-is-azure-ad-b2b.md) también será capaz de tooreset sus contraseñas con correo electrónico de Hola que registraron durante el proceso de invitación de Hola.

tootest, toohttp://passwordreset.microsoftonline.com vaya con uno de estos usuarios asociados. Siempre que tengan un correo electrónico alternativo o un correo electrónico de autenticación definido, el restablecimiento de contraseña funcionará según lo esperado.

## <a name="next-steps"></a>Pasos siguientes

Hola siguientes vínculos proporciona más información sobre el uso de Azure AD de restablecimiento de contraseña

* [**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD 
* [**Licencias**](active-directory-passwords-licensing.md): configuración de licencias de Azure AD
* [**Datos** ](active-directory-passwords-data.md) : comprender los datos de Hola que es necesarios y cómo se utiliza para la administración de contraseñas
* [**Implementación** ](active-directory-passwords-best-practices.md) -planear e implementar a los usuarios de Autoservicio tooyour usando la orientación de hello encontrar aquí
* [**Directiva**](active-directory-passwords-policy.md): información sobre las directivas de contraseñas de Azure AD y cómo establecerlas
* [**Escritura diferida de contraseñas**](active-directory-passwords-writeback.md): cómo funciona la escritura diferida de contraseñas con el directorio local
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Hola apariencia y funcionamiento del programa Hola a la experiencia de Autoservicio de su empresa.
* [**Informes**](active-directory-passwords-reporting.md): detectan si los usuarios acceden a la funcionalidad de SSPR, cuándo lo hacen y dónde.
* [**Preguntas más frecuentes**](active-directory-passwords-faq.md): ¿Cómo? ¿Por qué? ¿Qué? ¿Dónde? ¿Quién? ¿Cuándo? -Responde tooquestions siempre deseara tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Obtenga información acerca de cómo problemas comunes de tooresolve que vemos con SSPR

