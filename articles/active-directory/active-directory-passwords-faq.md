---
title: "Preguntas más frecuentes: SSPR de Azure AD | Microsoft Docs"
description: "Preguntas más frecuentes sobre autoservicio de restablecimiento de contraseña de Azure AD"
services: active-directory
keywords: "Administración de contraseñas de Active Directory, administración de contraseñas, autoservicio de restablecimiento de contraseña de Azure AD"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a>Preguntas más frecuentes sobre la administración de contraseñas

Hola siguientes es algunas preguntas frecuentes para todos los aspectos relacionados con toopassword restablecer.

Si tiene alguna pregunta sobre Azure AD general y una contraseña de autoservicio de restablecimiento, que no se trata aquí, puede pedir Comunidad Hola para obtener ayuda en hello [foros de Azure Ad](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD). Los miembros de la Comunidad de hello incluyen ingenieros, directores de producto, MVP y colegas profesionales de TI.

Estas preguntas más frecuentes se dividen en hello las secciones siguientes:

* [**Preguntas sobre el registro de restablecimiento de contraseña**](#password-reset-registration)
* [**Preguntas sobre el restablecimiento de contraseña**](#password-reset)
* [**Preguntas sobre el cambio de contraseña**](#password-change)
* [**Preguntas sobre los informes de la administración de contraseñas**](#password-management-reports)
* [**Preguntas sobre la escritura diferida de contraseñas**](#password-writeback)

## <a name="password-reset-registration"></a>Registro de restablecimiento de contraseña
* **P: ¿Mis usuarios pueden registrar sus propios datos de restablecimiento de contraseña?**

  > **R:** Sí, siempre y cuando se habilita el restablecimiento de contraseña y cuenten con licencia, pueden ir toohello portal de registro de restablecimiento de contraseña en http://aka.ms/ssprsetup tooregister su información de autenticación. Los usuarios también pueden registrarse va de panel de acceso de toohello en http://myapps.microsoft.com, haga clic en la ficha perfil de Hola y haga clic en hello registrar para la opción de restablecimiento de contraseña.
  >
  >
* **P: ¿Puedo definir los datos de restablecimiento de contraseña en nombre de mis usuarios?**

  > **R:** Sí, puede hacerlo con Azure AD Connect, PowerShell, hello [portal de Azure](https://portal.azure.com), o el portal de administración de Office de Hola. Para obtener más información, vea el artículo de hello [datos usados por Azure AD autoservicio de restablecimiento de contraseña](active-directory-passwords-data.md).
  >
  >
* **P: ¿Puedo sincronizar localmente los datos de las preguntas de seguridad?**

  > **R.:** No es posible hacerlo actualmente.
  >
  >
* **P: ¿Mis usuarios pueden registrar datos de manera tal que otros usuarios no puedan verlos?**

  > **R:** Sí, cuando un usuario registra datos mediante Hola se guarda la Portal de registro de restablecimiento de contraseña en los campos privados de autenticación que solo están visibles por los administradores globales y Hola por el usuario.
    >
    > [!NOTE]
    > Si un **cuenta de administrador de Azure** registra el número de teléfono de autenticación que también se rellena en el campo de teléfono móvil de Hola y es visible.
    >
  >
  >
* **P: ¿Mis usuarios tienen toobe registrado para poder usar el restablecimiento de contraseña?**

  > **R:** No, si define suficiente información de autenticación en su nombre, los usuarios no tienen tooregister. Restablecimiento de contraseña funciona como correctamente ha aplicado formato a los datos almacenados en los campos correspondientes de hello en el directorio de Hola.
  >
  >
* **P: ¿puedo sincronizar o establecer los campos de teléfono de autenticación, correo electrónico de autenticación o teléfono de autenticación alternativo de hello en nombre de Mis usuarios?**

  > **R.:** No es posible hacerlo actualmente.
  >
  >
* **P: ¿cómo portal de registro de hello sabe qué tooshow opciones Mis usuarios?**

  > **R:** portal de registro de restablecimiento de contraseña de hello solo muestra Hola opciones que ha habilitado para los usuarios. Estas opciones se encuentran en hello sección Directiva de restablecimiento de contraseña de usuario de la ficha configurar de su directorio. Por ejemplo, esto significa que si no habilita preguntas de seguridad, a continuación, los usuarios no son tooregister capaz de esa opción.
  >
  >
* **P: ¿Cuándo se considera que un usuario está registrado?**

  > **R:** se considera que un usuario se registra para SSPR cuando se hayan registrado al menos Hola **número de métodos necesarios tooreset** que haya establecido en hello [portal de Azure](https://portal.azure.com).
  >
  >
## <a name="password-reset"></a>Restablecimiento de contraseña
* **P: ¿Cuánto debo esperar tooreceive un correo electrónico, SMS o llamada de teléfono de restablecimiento de contraseña?**

  > **R:** correo electrónico, mensajes SMS, y llamadas telefónicas deben llegar en menos de un minuto, con hello habitual es que tarden 5 y 20 segundos.
    >Si no se reciben una notificación de hello en este período de tiempo:
        > * Compruebe la carpeta de correo no deseado.
        > * Compruebe el número de Hola o correo electrónico contactado es hello uno que espera.
        > * Compruebe los datos de autenticación de hello en el directorio de hello tiene el formato correcto.
                >     * Ejemplo: "+1 4255551234" o "user@contoso.com"
  >
  >
* **P: ¿Qué idiomas admite el restablecimiento de contraseña?**

  > **R:** Hola de interfaz de usuario de restablecimiento de contraseña, mensajes SMS y voz llamadas están localizadas en hello mismos idiomas que se admiten en Office 365.
  >
  >
* **P: ¿qué partes de la experiencia de restablecimiento de contraseña de hello obtengan marca cuando establezco organizativa de personalización de marca en mi directorio de la pestaña de configuración?**

  > **R:** portal de restablecimiento de contraseña de hello muestra el logotipo de su organización y le permite tooconfigure Hola póngase en contacto con su administrador vínculo toopoint tooa correo electrónico personalizadas o dirección URL. Cualquier correo electrónico que se envía a través de restablecimiento de contraseña incluye el logotipo de su organización, colores, el nombre de cuerpo de saludo de correo electrónico de Hola y personalizada a partir del nombre.
  >
  >
* **P: ¿Cómo puedo informar a Mis usuarios sobre dónde toogo tooreset sus contraseñas?**

  > **R:** puede enviar su toohttps://passwordreset.microsoftonline.com a los usuarios directamente, o puede indicar hello tooclick **no se puede tener acceso a su vínculo de la cuenta** se encuentra en cualquier página de inicio de sesión de trabajo o centro educativo. También puede publicar estos vínculos en un tooyour fácilmente accesible de contexto a los usuarios.
  >
  >
* **P: ¿Puedo usar esta página desde un dispositivo móvil?**

  > **R.:** Sí, esta página funciona en dispositivos móviles.
  >
  >
* **P: ¿Se admite el desbloqueo de cuentas locales de Active Directory cuando los usuarios restablecen sus contraseñas?**

  > **R:** Sí, cuando un usuario restablece la contraseña y se ha implementado la escritura diferida de contraseñas mediante Azure AD Connect, esa cuenta de usuario se desbloquea automáticamente al restablecer la contraseña.
  >
  >
* **P: ¿Cómo puedo integrar directamente el restablecimiento de contraseña en la experiencia de inicio de sesión de escritorio de mi usuario?**

  > **R:** si es un cliente de Azure AD Premium, puede instalar Microsoft Identity Manager sin ningún costo adicional e implementar Hola local contraseña restablecimiento solución toomeet este requisito.
  >
  >
* **P: ¿Puedo establecer distintas preguntas de seguridad para diferentes configuraciones regionales?**

  > **R.:** No es posible hacerlo actualmente.
  >
  >
* **P: ¿cuántas preguntas se pueden configurar para la opción de autenticación de preguntas de seguridad de hello?**

  > **R:** puede configurar las preguntas de seguridad personalizado too20 Hola [portal de Azure](https://portal.azure.com).
  >
  >
* **P: ¿Qué longitud pueden tener las preguntas de seguridad?**

  > **R.:** Las preguntas de seguridad pueden tener entre 3 y 200 caracteres.
  >
  >
* **P: ¿cuánto tiempo puede respuestas toosecurity preguntas?**

  > **R:** respuestas pueden tener 3 caracteres too40.
  >
  >
* **P: ¿se rechazan respuestas duplicadas toosecurity preguntas?**

  > **R:** Sí, se rechazan respuestas duplicadas toosecurity preguntas.
  >
  >
* **P: ¿puede un registro de usuario Hola misma pregunta de seguridad más de una vez?**

  > **R:** No. Una vez que un usuario registra una pregunta específica, no puede registrar esa pregunta por segunda vez.
  >
  >
* **P: ¿es posible tooset un límite mínimo de preguntas de seguridad de registro y restablecimiento?**

  > **R.:** Sí, es posible establecer un límite para el registro y otro para el restablecimiento. Es posible que se requieran entre 3 y 5 preguntas para el registro y entre 3 y 5 para el restablecimiento.
  >
  >
* **P: si un usuario ha registrado más Hola número máximo de preguntas necesario tooreset, ¿cómo se seleccionan las preguntas de seguridad durante el restablecimiento?**

  > **R:** seguridad N preguntas se seleccionan aleatoriamente fuera del número total de Hola de preguntas que un usuario ha registrado, donde N es hello **número de preguntas necesario tooreset**. Por ejemplo, si un usuario tiene 5 preguntas de seguridad registrados, pero sólo 3 son necesario tooreset, 3 de hello 5 se selecciona aleatoriamente y presentadas en el restablecimiento. Si Hola usuario recibe respuestas de hello toohello preguntas incorrecto, el proceso de selección de hello vuelve a suceder tooprevent ataques por repetición.
  >
  >
* **P: ¿Es posible evitar que los usuarios intenten restablecer la contraseña muchas veces en un período de tiempo breve?**

  > **R:** Sí, hay características de seguridad integradas en tooprotect de restablecimiento de contraseña de uso indebido. Los usuarios solo pueden intentar 5 restablecimientos de contraseña en un período de una hora antes de que se les bloquee durante 24 horas. Los usuarios solo pueden probar toovalidate un número de teléfono 5 veces en una hora antes de que se bloquee durante 24 horas. Los usuarios solo pueden intentar un método de autenticación 5 veces dentro de una hora antes de que se les bloquee durante 24 horas.
  >
  >
* **P: ¿durante cuánto tiempo son código de acceso de un solo uso de SMS y correo electrónico de hello válidos?**

  > **R:** Hola duración de la sesión para restablecer la contraseña es 105 minutos. Desde principio Hola de hello operación de restablecimiento de contraseña, usuario de hello tiene 105 minutos tooreset su contraseña. Hello código de acceso de un solo uso de SMS y correo electrónico no son válidos después de que expire este período de tiempo.
  >
  >

## <a name="password-change"></a>Cambio de contraseña
* **P: ¿dónde deberían Mis usuarios ir toochange sus contraseñas?**

  > **R:** a los usuarios pueden cambiar sus contraseñas en cualquier lugar vean su imagen de perfil o el icono (al igual que en hello superior derecho de sus [Office 365](https://portal.office.com) o [Panel de acceso](https://myapps.microsoft.com) experiencias. Los usuarios pueden cambiar sus contraseñas de hello [página del Panel de acceso de perfil](https://account.activedirectory.windowsazure.com/r#/profile). Los usuarios también pueden ser más frecuentes toochange sus contraseñas automáticamente en la pantalla de inicio de sesión de bienvenida Azure AD si sus contraseñas han caducado. Por último, los usuarios pueden navegar toohello [Portal de cambio de contraseña de Azure AD](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directamente si lo desean toochange sus contraseñas.
  >
  >
* **P: ¿pueden mis usuarios se notificará en hello Portal de Office cuando expira la contraseña local?**

  > **R:** esto es posible hoy si utilizas AD FS siguiendo las instrucciones de hello aquí: [enviar notificaciones de directiva de contraseña con ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396). Esto no es posible hoy si usa la sincronización de hash de contraseña. Esto es porque no se sincronizar directivas de contraseña local, por lo que no es posible que nos toocloud de notificaciones de expiración toopost experiencias. En cualquier caso, también es posible demasiado[notificar a los usuarios cuyas contraseñas están sobre tooexpire mediante PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).
  >
  >

## <a name="password-management-reports"></a>Informes de administración de contraseñas
* **P: ¿cuánto tarda para datos tooshow seguridad en informes de administración de contraseñas de hello?**

  > **R:** los datos aparecerán en informes de administración de contraseñas de hello en entre 5 y 10 minutos. Algunas instancias pueden tardar hasta tooan hora tooappear.
  >
  >
* **P: ¿Cómo puedo filtrar los informes de administración de contraseñas de hello?**

  > **R:** puede filtrar los informes de administración de contraseñas de hello haciendo clic en hello lupa pequeña toohello derecha de las etiquetas de columna de hello, cerca de parte superior de Hola de informe de Hola. Si desea toodo de filtrado exhaustivo, puede descargar Hola informe tooexcel y crear una tabla dinámica.
  >
  >
* **P: ¿cuál es el número máximo de Hola de eventos se almacenan en los informes de administración de contraseñas de hello?**

  > **R:** seguridad too75, 000 contraseña contraseña o restablecimiento del registro los eventos de restablecimiento se almacenan en informes de administración de contraseñas de hello, expansión de copia de seguridad too30 días.  Estamos trabajando tooexpand este número tooinclude más eventos.
  >
  >
* **P: ¿cómo lejos vaya Hola informes de administración de contraseñas?**

  > **R:** administración de contraseñas de hello informa de las operaciones de presentación que se producen en hello últimos 30 días. Por ahora, si necesita tooarchive estos datos, puede descargar informes de hello periódicamente y guardarlos en una ubicación diferente.
  >
  >
* **P: ¿existe un número máximo de filas que pueden aparecer en informes de administración de contraseñas de hello?**

  > **R:** Sí, un máximo de 75.000 filas puede aparecer en cualquiera de los informes de administración de contraseñas de hello, si se muestran en Hola interfaz de usuario o que se va a descargar.
  >
  >
* **P: ¿existe una tooaccess API Hola contraseña restablecimiento o registro de datos de informes?**

  > **R:** Sí, vea Hola siguientes documentación toolearn cómo puede tener acceso a contraseñas de hello restablecer flujo de datos de informes.  [Obtenga información acerca de cómo tooaccess de restablecimiento de contraseña eventos de informe mediante programación](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).
  >
  >

## <a name="password-writeback"></a>Escritura diferida de contraseñas
* **P: ¿cómo funciona la escritura diferida de contraseñas entre bastidores de hello?**

  > **R:** vea [cómo funciona la escritura diferida de contraseñas](active-directory-passwords-writeback.md) para obtener una explicación de lo que ocurre cuando se habilita la escritura diferida de contraseñas y cómo fluyen los datos a través del sistema de hello en el entorno local.
  >
  >
* **P: ¿cuánto tiempo tarda la escritura diferida de contraseñas la toowork?  ¿Existe un retraso en la sincronización, como ocurre con la sincronización de hash de contraseña?**

  > **R.:** La escritura diferida de contraseñas es inmediata. Se trata de una canalización sincrónica que funciona radicalmente distinto a la sincronización de hash de contraseña. Escritura diferida de contraseñas permite a los usuarios tooget comentarios en tiempo real sobre la correcta de Hola de su contraseña restablecer o cambiar la operación. tiempo medio de Hola para una reescritura de una contraseña correcta es inferior a 500 ms..
  >
  >
* **P: Si mi cuenta local está deshabilitada, ¿en qué afecta a mi acceso y a mi cuenta en la nube?**

  > **R:** si el identificador local está deshabilitado, la nube de identificador/acceso también se deshabilitará al siguiente intervalo de sincronización Hola a través de la conexión de AAD byt de forma predeterminada se trata cada 30 minutos.
  >
  >
* **¿P: si mi cuenta local está restringido por una directiva de contraseña de Active Directory local, SSPR obedecen a esta directiva cuando se cambia la contraseña de hello?**

  > **R:** Sí, SSPR se basa en y se rige por directiva de contraseñas de AD, incluida la directiva de contraseñas de dominio de AD típica, así como las directivas de contraseña específica definida como destino tooa dado usuario a local de Hola.
  >
  >
* **P: ¿Para qué tipos de cuentas funciona la escritura diferida de contraseñas?**

  > **R:** La escritura diferida de contraseñas funciona para usuarios federados y usuarios con sincronización de hash de contraseña.
  >
  >
* **P: ¿La escritura diferida de contraseñas aplica las directivas de contraseñas de mi dominio?**

  > **R:** Sí, la escritura diferida de contraseñas aplica la vigencia, el historial, la complejidad y los filtros de contraseñas, además de cualquier otra restricción que pueda aplicar sobre las contraseñas en su dominio local.
  >
  >
* **P: ¿Es segura la escritura diferida de contraseñas?  ¿Cómo puedo estar seguro de no ser víctima del ataque de un hacker?**

  > **R:** Sí, la escritura diferida de contraseñas es segura. tooread más información acerca de las capas de hello cuatro de seguridad implementado por el servicio de escritura diferida de contraseña de hello, desproteger hello [modelo de seguridad de escritura diferida de contraseñas](active-directory-passwords-writeback.md#password-writeback-security-model) sección en cómo funciona la escritura diferida de contraseñas.
  >
  >

## <a name="next-steps"></a>Pasos siguientes

Hola siguientes vínculos proporciona más información sobre el uso de Azure AD de restablecimiento de contraseña

* [**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD 
* [**Licencias**](active-directory-passwords-licensing.md): configuración de licencias de Azure AD
* [**Datos** ](active-directory-passwords-data.md) : comprender los datos de Hola que es necesarios y cómo se utiliza para la administración de contraseñas
* [**Implementación** ](active-directory-passwords-best-practices.md) -planear e implementar a los usuarios de Autoservicio tooyour usando la orientación de hello encontrar aquí
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Hola apariencia y funcionamiento del programa Hola a la experiencia de Autoservicio de su empresa.
* [**Informes**](active-directory-passwords-reporting.md): detectan si los usuarios acceden a la funcionalidad de SSPR, cuándo lo hacen y dónde.
* [**Directiva**](active-directory-passwords-policy.md): información sobre las directivas de contraseñas de Azure AD y cómo establecerlas
* [**Escritura diferida de contraseñas**](active-directory-passwords-writeback.md): cómo funciona la escritura diferida de contraseñas con el directorio local
* [**Profundización técnica** ](active-directory-passwords-how-it-works.md) -ir detrás de hello cortina toounderstand cómo funciona
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Obtenga información acerca de cómo problemas comunes de tooresolve que vemos con SSPR
