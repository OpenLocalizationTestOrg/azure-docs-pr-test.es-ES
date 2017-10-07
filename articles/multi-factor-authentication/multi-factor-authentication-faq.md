---
title: "P+F de autenticación multifactor aaaAzure | Documentos de Microsoft"
description: "Preguntas más frecuentes y respuestas relacionadas con tooAzure la autenticación multifactor. Multi-Factor Authentication es un método para comprobar la identidad de un usuario que requiere usar más de un nombre de usuario y contraseña. Proporciona una capa adicional de inicio de sesión de seguridad toouser y las transacciones."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8305cf4c41bf8e9802df192fecdb7e463eff9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-multi-factor-authentication"></a>Preguntas más frecuentes relacionadas con Azure Multi-Factor Authentication
Estas preguntas más frecuentes preguntas más frecuentes sobre la autenticación multifactor Azure y el uso de servicio de la autenticación multifactor de Hola. Se desglosa en preguntas acerca del servicio de hello en general, modelos, experiencias de usuario, de facturación y solución de problemas.

## <a name="general"></a>General
**P.: ¿Cómo controla Servidor Azure Multi-Factor Authentication los datos de usuario?**

Con el servidor de autenticación multifactor, datos de usuario se almacenan únicamente en servidores locales de Hola. Ningún dato de usuario persistentes se almacena en la nube de Hola. Cuando el usuario de hello realiza la verificación en dos pasos, servidor Multi-factor Authentication envía datos toohello servicio de nube de Azure Multi-factor Authentication para la autenticación. Comunicación entre el servidor de autenticación multifactor y Hola servicio de nube de la autenticación multifactor usa Secure Sockets Layer (SSL) o seguridad de capa de transporte (TLS) en el puerto 443 de salida.

Cuando se envían solicitudes de autenticación toohello servicio en la nube, los datos se recopilan para la autenticación y el uso de informes. Los campos de datos que se incluyen en los registros de comprobación en dos pasos son los siguientes:

* **Id. único** (cualquier nombre de usuario o id. de Servidor Multi-Factor Authentication local)
* **Nombre y apellidos** (opcional)
* **Dirección de correo electrónico** (opcional)
* **Número de teléfono** (al realizar la autenticación de una llamada de voz o SMS)
* **Token de dispositivo** (al realizar la autenticación de una aplicación móvil)
* **Modo de autenticación**
* **Resultado de la autenticación**
* **Nombre de Servidor Multi-Factor Authentication**
* **IP de Servidor Multi-Factor Authentication**
* **IP de cliente** (si está disponible)

campos opcionales Hola pueden configurarse en el servidor de autenticación multifactor.

Hola resultados de comprobación (éxito o denegación) y hello motivo si se deniega, se almacena con los datos de autenticación de Hola. Los datos están disponibles en los informes de autenticación y uso.

## <a name="billing"></a>Facturación
Pueden responder preguntas sobre facturación mayoría consultando hello tooeither [página de precios de autenticación multifactor](https://azure.microsoft.com/pricing/details/multi-factor-authentication/) u Hola documentación sobre [cómo tooget la autenticación multifactor Azure](multi-factor-authentication-versions-plans.md).

**P: ¿es mi organización cargada por envío de llamadas de teléfono de Hola y mensajes de texto que se utilizan para la autenticación?**

No, no se le cobrará para colocar las llamadas de teléfono o toousers a través de la autenticación multifactor Azure envían los mensajes de texto. Si utiliza un proveedor MFA por autenticación, se le facturará para cada autenticación pero no para el método hello utilizado.

Los usuarios podrían cobrará por llamadas de teléfono de Hola o mensajes de texto que reciben, servicio de teléfono personal tootheir correspondiente.

**P: ¿modelo de facturación por usuario Hola me cobra por habilitado todos los usuarios, o simplemente hello las que realiza la verificación en dos pasos?**

Facturación se basa en el número de Hola de usuarios configurados toouse la autenticación multifactor, independientemente de si deben realizar verificacion ese mes.

**P.: ¿Cómo funciona la facturación de Multi-Factor Authentication?**

Cuando se crea un proveedor de MFA por usuario o por autenticación, se factura mensualmente a la suscripción de Azure de su organización según el uso. Este modelo de facturación es similar toohow Azure facturas para el uso de máquinas virtuales y sitios Web.

Al adquirir una suscripción para la autenticación multifactor de Azure, su organización paga sólo la tarifa de licencia anual de Hola para cada usuario. Las licencias MFA así como los conjuntos de productos de Office 365, Azure AD Premium o Enterprise Mobility + Security se facturan de esta manera. 

Obtener más información sobre las diferentes opciones en [cómo tooget la autenticación multifactor Azure](multi-factor-authentication-versions-plans.md).

**P: ¿Existe una versión gratuita de Azure Multi-Factor Authentication?**

En algunos casos, sí.

La autenticación multifactor para administradores de Azure ofrece un subconjunto de características de Azure MFA sin costo alguno para el acceso a los servicios en línea tooMicrosoft, incluidos los portales de administrador de Azure y Office 365 Hola. Esta oferta solo aplica a los administradores de tooglobal en instancias de Azure Active Directory que no tienen la versión completa de Hola de Azure MFA a través de una licencia MFA, un paquete o un proveedor independiente de basado en el consumo. Si los administradores usan la versión gratuita de hello y, a continuación, adquiera una versión completa de MFA de Azure, todos los administradores globales son elevado toohello pagada versión automáticamente.

La autenticación multifactor para usuarios de Office 365 ofrece un subconjunto de características de Azure MFA sin costo alguno acceso tooOffice 365 servicios, como Exchange Online y SharePoint Online. Esta oferta aplica toousers que tienen una licencia de Office 365 asignada, al instancia correspondiente de Hola de Azure Active Directory no tiene la versión completa de Hola de Azure MFA a través de una licencia MFA, un paquete o un proveedor independiente de basado en el consumo.

**P.: ¿Puede mi organización cambiar entre los modelos de facturación de consumo por usuario y por autenticación en cualquier momento?**

Si la organización adquiere MFA como servicio independiente con facturación basada en el consumo, se elige un modelo de facturación cuando se crea un proveedor de MFA. No puede cambiar el modelo de facturación de hello después de crea un proveedor de MFA. Sin embargo, puede eliminar el proveedor de MFA de hello y, a continuación, crear una con un modelo de facturación diferente.

Cuando se crea un proveedor de MFA, puede ser vinculado tooan Azure Active Directory (también conocido como "inquilino de Azure AD"). Hello actual proveedor de MFA está vinculado tooan Azure AD inquilino, puede eliminar el proveedor de MFA de Hola y crear uno que esté vinculado toohello AD de Azure mismo inquilino. Como alternativa, si ha adquirido suficiente MFA, Azure AD Premium o Enterprise Mobility + Security (EMS) licencias toocover todos los usuarios que están habilitados para MFA, puede eliminar proveedor de MFA de Hola por completo.

Si su proveedor MFA es *no* inquilino tooan vinculado Azure AD, o bien vincula Hola nuevo MFA proveedor tooa Azure AD diferentes inquilino, configuración de usuario y opciones de configuración no se transfieren. Además, Azure MFA servidores existentes necesita toobe vuelve a activar utilizando credenciales de activación que se generan a través de Hola nuevo proveedor de MFA. Reactivar Hola servidores MFA toolink les toohello nuevo proveedor de MFA no afecta a la llamada de teléfono y autenticación de mensajes de texto, pero la aplicación móvil notificaciones dejará de funcionar para todos los usuarios hasta que vuelvan a activar aplicación móvil de Hola.

Encuentre más información sobre los proveedores de MFA en [Introducción al Proveedor de Azure Multi-Factor Authentication](multi-factor-authentication-get-started-auth-provider.md).

**P: ¿Mi organización puede cambiar entre la facturación basada en el consumo y las suscripciones (un modelo basado en licencias) en cualquier momento?**

En algunos casos, sí.

Si el directorio tiene un proveedor de Azure Multi-Factor Authentication *por usuario*, puede agregar licencias de MFA. Los usuarios con licencias no se contarán en la facturación basada en el consumo de Hola por usuario. Los usuarios sin licencias todavía pueden habilitarse para MFA a través del proveedor de MFA de Hola. Si compra y asignar licencias para todos los usuarios habían configurada toouse la autenticación multifactor, puede eliminar el proveedor de la autenticación multifactor Azure Hola. Siempre puede crear otro proveedor MFA por usuario si tiene más usuarios que licencias de Hola futuras.

Si un directorio tiene una *por autenticación* proveedor de autenticación multifactor de Azure, siempre se facturan para cada autenticación, como proveedor MFA de hello es suscripción tooyour vinculado. Puede asignar toousers de licencias MFA, pero todavía se le facturarán para cada solicitud de verificación en dos pasos, si procede de un usuario con una licencia MFA asignada o no.

**P: ¿mi organización tiene toouse y sincronizar identidades toouse la autenticación multifactor Azure?**

Si la organización usa un modelo de facturación basado en el consumo, Azure Active Directory es opcional, no obligatorio. Si el proveedor de MFA no está vinculado tooan inquilino de Azure AD, solo se pueden implementar servidor Azure Multi-factor Authentication o SDK de Azure Multi-factor Authentication hello en local.

Azure Active Directory es necesario para el modelo de licencias de hello porque licencias se agregan a inquilino de Azure AD toohello cuando adquiere y asignarles toousers en el directorio de Hola.

## <a name="manage-and-support-user-accounts"></a>Administración y soporte técnico de las cuentas de usuario

**P: ¿qué debo decir a mi toodo a los usuarios si no recibe una respuesta en el número de teléfono, o no tiene su teléfono con ellos?**

Es de esperar que todos los usuarios hayan configurado más de un método de comprobación. Indíquele tootry vuelva a iniciar sesión, pero seleccione un método de verificación diferente en la página de inicio de sesión de Hola.

Puede apuntar el toohello usuarios [Guía de solución de problemas del usuario final](./end-user/multi-factor-authentication-end-user-troubleshoot.md).


**P: ¿qué debo hacer si uno de Mis usuarios no se puede obtener en tootheir cuenta?**

Puede restablecer la cuenta de usuario de hello hacerlos toogo a través del proceso de registro de hello nuevo. Obtenga más información sobre [administrar la configuración de usuarios y dispositivos con Azure Multi-factor Authentication en la nube de hello](multi-factor-authentication-manage-users-and-devices.md).

**P: ¿Qué debo hacer si a uno de los usuarios se le pierde el teléfono en el que usa las contraseñas de aplicación?**

acceso no autorizado tooprevent eliminar las contraseñas de aplicación de todos los usuarios de Hola. Después de que el usuario de hello tiene un dispositivo de reemplazo, puede volver a crear contraseñas de Hola. Obtenga más información sobre [administrar la configuración de usuarios y dispositivos con Azure Multi-factor Authentication en la nube de hello](multi-factor-authentication-manage-users-and-devices.md).

**P: ¿qué ocurre si un usuario no puede iniciar sesión en aplicaciones de explorador toonon?**

Si su organización todavía usa clientes heredados y [Hola el uso de contraseñas de aplicación](multi-factor-authentication-whats-next.md#app-passwords), a continuación, los usuarios no pueden iniciar sesión en los clientes heredados de toothese con su nombre de usuario y contraseña. En su lugar, necesita demasiado[configurar contraseñas de aplicación](./end-user/multi-factor-authentication-end-user-app-passwords.md). Los usuarios deben borrar (delete) su información de inicio de sesión, reiniciar la aplicación hello y, a continuación, inicie sesión con su nombre de usuario y *contraseña de aplicación* en lugar de su contraseña regular.

Si su organización no tiene clientes heredados, no debe permitir a los usuarios las contraseñas de aplicación de toocreate.

> [!NOTE]
> Autenticación moderna para clientes de Office 2013
>
> Las contraseñas de aplicación solo son necesarias para las aplicaciones que no admiten la autenticación moderna. Los clientes de Office 2013 admiten protocolos de autenticación moderna, pero necesitan toobe configurado. Los clientes de Office más recientes admiten automáticamente protocolos de autenticación moderna. Para obtener más información, vea hello [anuncio de versión preliminar pública de la autenticación moderna de Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).

**P: ¿Mis usuarios afirman que a veces no recibirán mensajes de texto hello, o responder a mensajes de texto de manera tootwo pero agota el tiempo de espera de comprobación de Hola.**

No se garantiza la entrega de mensajes de texto y la recepción de respuestas SMS bidireccional porque hay factores incontrolables que podrían afectar a la confiabilidad de hello del servicio de Hola. Estos factores incluyen país de destino de Hola y operador de telefonía móvil hello, intensidad de la señal de Hola.

Si los usuarios suelen tengan problemas con la recepción de forma confiable los mensajes de texto, indíquele toouse móviles llamada de teléfono o aplicación método hello en su lugar. aplicación móvil de Hello puede recibir notificaciones tanto a través de la red de telefonía móvil y conexiones Wi-Fi. Además, aplicación móvil de hello puede generar códigos de comprobación aunque Hola dispositivo no tiene señal en absoluto. está disponible para la aplicación de Microsoft Authenticator Hello [Android](http://go.microsoft.com/fwlink/?Linkid=825072), [IOS](http://go.microsoft.com/fwlink/?Linkid=825073), y [de Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071).

En la medida de lo posible, recomendamos usar SMS unidireccionales en lugar de bidireccionales si tiene que usar mensajes de texto. SMS unidireccionales son más confiables y se evita que los usuarios de incurrir en cargos de SMS globales de mensaje de texto tooa usuarios de confianza que se envió desde otro país.

**P: ¿puedo cambiar Hola cantidad de tiempo que mis usuarios tienen código de comprobación de hello tooenter de un mensaje de texto antes agote el tiempo de espera de sistema de hello?**

En algunos casos, sí es posible. 

Para SMS unidireccionales con el servidor Azure MFA v7.0 o superior, puede configurar el tiempo de espera de hello estableciendo una clave del registro. Después de hello servicio en la nube MFA envía mensajes de bienvenida del texto, código de comprobación de hello (o código de acceso de un solo uso) se devuelve toohello servidor MFA. Hola servidor MFA almacena el código de hello en memoria durante 300 segundos de forma predeterminada. Si el usuario hello no escriba código de hello antes Hola 300 segundos transcurridos, se deniega la autenticación. Use estos pasos toochange Hola tiempo de espera predeterminado establecer:

1. Vaya tooHKLM\Software\Wow6432Node\Positive Networks\PhoneFactor.
2. Cree una clave de Registro DWORD denominada **pfsvc_pendingSmsTimeoutSeconds** y establecer el tiempo de hello en segundos que desea que los códigos de acceso única de hello servidor Azure MFA toostore.

>[!TIP] 
>Si tiene varios servidores de MFA, solo Hola que procesa la solicitud de autenticación original de hello sabe código de comprobación de Hola que envió toohello usuario. Cuando el usuario de hello introduce código de hello, Hola toovalidate de solicitud de autenticación se debe enviar toohello mismo servidor. Si la validación de código de Hola se envía tooa otro servidor, se deniega la autenticación de Hola. 

Para SMS bidireccional con el servidor de MFA de Azure, puede configurar configuración de tiempo de espera de Hola Hola Portal de administración de MFA. Si los usuarios no responder toohello SMS dentro del período de tiempo de espera definido de hello, se deniega la autenticación. 

Para SMS unidireccionales con Azure MFA en la nube de hello (incluidos Hola extensión de servidor de directivas de red de Hola o adaptador de AD FS), no puede configurar la configuración de tiempo de espera de Hola. Azure AD almacena el código de comprobación de Hola durante 180 segundos. 

**P.: ¿Puedo utilizar tokens de hardware con Servidor Microsoft Azure Multi-Factor Authentication?**

Si usa Servidor Azure Multi-Factor Authentication, puede importar los tokens de contraseña de un solo uso de duración definida (TOTP) y los de autenticación abierta (OATH) de terceros y, después, utilizarlos para realizar la comprobación en dos pasos.

Puede utilizar tokens de ActiveIdentity que son tokens de OATH TOTP si coloca la clave secreta de hello en un archivo CSV e importar tooAzure servidor Multi-factor Authentication. Puede utilizar tokens OATH con servicios de federación de Active Directory (ADFS), la autenticación basada en formularios de Internet Information Server (IIS) y servicio de autenticación remota telefónica de usuario (RADIUS) como sistema de cliente de hello puede aceptar Hola proporcionados por el usuario.

Puede importar tokens OATH TOTP de terceros con hello siguientes formatos:  

- Contenedor de claves simétricas portátil (PSKC)  
- CSV si archivo hello contiene un número de serie, una clave secreta en formato Base 32 y un intervalo de tiempo  

**P: ¿puedo usar los servicios de Terminal de toosecure de servidor de autenticación multifactor de Azure?**

Sí, pero si usa Windows Server 2012 R2 o versiones posteriores, solo puede proteger Terminal Services con Puerta de enlace de Escritorio remoto (Puerta de enlace de RD).

Cambios de seguridad en Windows Server 2012 R2 cambiar cómo servidor Azure Multi-factor Authentication se conecta toohello paquete de seguridad de entidad de seguridad Local (LSA) en Windows Server 2012 y versiones anteriores. Para las versiones de Terminal Services en Windows 2012 o versiones anteriores, puede [proteger una aplicación con la autenticación de Windows](multi-factor-authentication-get-started-server-windows.md#to-secure-an-application-with-windows-authentication-use-the-following-procedure). Sin embargo, si va a utilizar Windows Server 2012 R2, necesita el servicio Puerta de enlace de Escritorio remoto.

**P: Configuré el identificador de llamada en Servidor MFA, pero mis usuarios siguen recibiendo llamadas de Multi-Factor Authentication provenientes de un autor de llamada anónimo.**

Cuando la autenticación multifactor llamadas se establecen a través de la red telefónica pública de hello, a veces se enrutan a través de un operador que no es compatible con Id. Por este motivo, identificador de llamada no está garantizado, aunque Hola sistema de la autenticación multifactor siempre lo envía.

**P: ¿por qué mis usuarios están solicitada tooregister su información de seguridad?**
Hay varias razones que los usuarios podrían ser solicitada tooregister su información de seguridad:

- usuario de Hola se ha habilitado para MFA por su administrador en Azure AD, pero no tiene información de seguridad todavía registrado para su cuenta.
- usuario de Hola se habilitó para el restablecimiento de contraseña en Azure AD. información de seguridad de Hello les ayudará a restablecer su contraseña en hello futuras si alguna vez se olvida.
- usuario de Hello tiene acceso a una aplicación que tiene un toorequire de directiva de acceso condicional MFA y no se ha registrado previamente para MFA.
- usuario de Hello está registrando un dispositivo con Azure AD (incluyendo Azure AD Join) y su organización requiere MFA para el registro de dispositivos, pero usuario hello no se ha registrado previamente para MFA.
- usuario de Hello está generando Windows Hello para empresas en Windows 10 (que requiere MFA) y no se ha registrado previamente para MFA.
- organización de Hello ha creado y habilitado una directiva de registro de MFA que se ha aplicado toohello usuario.
- usuario de Hello previamente había registrado para MFA, pero elige un método de comprobación que un administrador ha deshabilitado desde entonces. usuario de Hello, por tanto, debe pasar a través del registro MFA nuevo tooselect un nuevo método de comprobación de forma predeterminada.


## <a name="errors"></a>Errors
**P.: ¿Qué deben hacer los usuarios si ven un mensaje de error que indica que la solicitud de autenticación no es para una cuenta activada al usar notificaciones de aplicación móvil?**

Indíquele toofollow este procedimiento tooremove su cuenta desde la aplicación móvil de hello, a continuación, agregarlo de nuevo:

1. Vaya demasiado[su perfil de portal de Azure](https://account.activedirectory.windowsazure.com/profile/) e inicie sesión con su cuenta profesional.
2. Seleccione **Comprobación de seguridad adicional**.
3. Quitar cuenta existente de Hola de aplicación móvil de Hola.
4. Haga clic en **configurar**y, a continuación, siga la aplicación móvil de hello instrucciones tooreconfigure Hola.

**P: ¿qué deben hacer los usuarios si ve un mensaje de error 0x800434D4L al iniciar sesión en la aplicación sin explorador de tooa?**

se produce el error 0x800434D4L Hello cuando intente toosign en aplicación de explorador no tooa, instalado en un equipo local, que no funciona con las cuentas que requieren verificación en dos pasos.

Una solución alternativa para este error es toohave independiente las cuentas de usuario para relacionadas con la administración y operaciones no administrativas. Más adelante, puede vincular buzones de correo entre su cuenta de administrador y una cuenta sin derechos administrativos para que puede iniciar sesión en tooOutlook con su cuenta sin derechos administrativos. Para obtener más detalles sobre esta solución, obtenga información acerca de cómo demasiado[dar un Hola administrador capacidad tooopen y vista Hola el contenido del buzón de un usuario](http://help.outlook.com/141/gg709759.aspx?sl=1).

## <a name="next-steps"></a>Pasos siguientes
Si su pregunta no responde aquí, déjelo en comentarios de Hola final Hola de página Hola. O bien, aquí se muestran algunas opciones adicionales para obtener ayuda:

* Hola de búsqueda [Microsoft Support Knowledge Base](https://www.microsoft.com/en-us/Search/result.aspx?form=mssupport&q=phonefactor&form=mssupport) para problemas técnicos de toocommon de soluciones.
* Buscar y examinar preguntas técnicas y respuestas de la Comunidad de Hola o pida a su pregunta en hello [foros de Azure Active Directory](https://social.msdn.microsoft.com/Forums/azure/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).
* Si usted es un cliente heredado de PhoneFactor y tiene alguna pregunta o necesita ayuda para restablecer una contraseña, use hello [de restablecimiento de contraseña](mailto:phonefactorsupport@microsoft.com) vincular tooopen un caso de soporte técnico.
* Póngase en contacto con un profesional de soporte técnico a través de [Soporte técnico de Servidor Azure Multi-Factor Authentication (PhoneFactor)](https://support.microsoft.com/oas/default.aspx?prid=14947). Al ponerse en contacto con nosotros, nos resultará de gran utilidad que incluya tanta información sobre su problema como sea posible. Puede proporcionar la información incluye página Hola donde vio error hello, código de error específico de hello, Id. de sesión específico de Hola e Id. de Hola de usuario de Hola que vio el error de Hola.
