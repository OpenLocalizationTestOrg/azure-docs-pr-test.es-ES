---
title: portal de aaaUser de servidor de MFA de Azure | Documentos de Microsoft
description: "Se trata de una página de autenticación multifactor de Azure de Hola que describe cómo se inicia tooget con Azure MFA y el portal de usuarios de Hola."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 06b419fa-3507-4980-96a4-d2e3960e1772
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 0e36644c3d780249fb98d5da654e9d267c63561a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="user-portal-for-hello-azure-multi-factor-authentication-server"></a>Portal de usuarios para saludo del servidor de autenticación multifactor de Azure

portal de usuarios de Hello es un sitio web IIS que permite a los usuarios tooenroll en Azure la autenticación multifactor (MFA) y mantener sus cuentas. Un usuario puede cambiar su número de teléfono, cambiar su código PIN o elija toobypass verificacion durante su siguiente inicio de sesión.

Los usuarios iniciar sesión en el portal de usuarios de toohello con su nombre de usuario y contraseña, a continuación, completar una llamada de verificación en dos pasos o responder toocomplete de preguntas de seguridad de la autenticación. Si se permite la inscripción de usuario, los usuarios configurar sus hello PIN y el número de teléfono primera vez que inicien sesión en el portal de usuarios de toohello.

Los administradores del portal de usuarios se puede configurar y conceder permiso tooadd nuevos usuarios y actualizar usuarios existentes.

Dependiendo de su entorno, puede que desee toodeploy portal de usuarios de hello en hello mismo servidor como servidor de autenticación multifactor de Azure o en otro servidor orientado a internet.

![Portal de usuarios de MFA](./media/multi-factor-authentication-get-started-portal/portal.png)

> [!NOTE]
> portal de usuarios de Hello solo está disponible con el servidor de autenticación multifactor. Si utiliza la autenticación multifactor en la nube de hello, consulte su toohello usuarios [su cuenta para la verificación en dos pasos de instalación](./end-user/multi-factor-authentication-end-user-first-time.md) o [administrar la configuración de verificación en dos pasos](./end-user/multi-factor-authentication-end-user-manage-settings.md).

## <a name="install-hello-web-service-sdk"></a>Instalar SDK del servicio web Hola

En estos escenarios, si hello SDK de servicio Web de Azure Multi-factor Authentication es **no** ya instalados en hello servidor Azure Multi-factor Authentication (MFA), Hola completa los pasos siguientes.

1. Abra la consola de servidor de autenticación multifactor de Hola.
2. Vaya toohello **SDK del servicio Web** y seleccione **instalar SDK del servicio Web**.
3. Instalación de hello completa con los valores predeterminados de Hola a menos que necesite toochange les por algún motivo.
4. Enlazar un sitio de toohello de certificado SSL en IIS.

Si tiene alguna pregunta acerca de cómo configurar un certificado SSL en un servidor IIS, vea el artículo de hello [cómo configurar SSL en IIS tooSet](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Hola SDK del servicio Web debe estar protegido con un certificado SSL. Un certificado autofirmado es adecuado para este propósito. Importar certificado Hola Hola "Entidades de certificación de raíz de confianza" almacén de cuenta de equipo Local de hello en el servidor web de Portal de usuarios de Hola para que confíe en ese certificado cuando se inicie la conexión de SSL de Hola.

![SDK del servicio web de configuración del Servidor MFA](./media/multi-factor-authentication-get-started-portal/sdk.png)

## <a name="deploy-hello-user-portal-on-hello-same-server-as-hello-azure-multi-factor-authentication-server"></a>Implementar el portal de usuarios de hello en hello mismo servidor como servidor Azure Multi-factor Authentication Hola

Hello requisitos previos siguientes son necesarios tooinstall portal de usuarios de hello en hello **mismo servidor** como Hola servidor Azure Multi-factor Authentication:

* IIS, incluido ASP.NET y compatibilidad con la metabase de IIS 6 (para IIS 7 o posterior).
* Una cuenta con derechos de administrador para el equipo de Hola y dominio, si es aplicable. cuenta de Hello tiene grupos de seguridad de Active Directory de toocreate de permisos.
* Portal de usuarios de hello segura con un certificado SSL.
* Hola SDK de servicio Web de Azure Multi-factor Authentication segura con un certificado SSL.

toodeploy Hola portal, seguimiento de usuario de estos pasos:

1. Abra la consola de servidor de autenticación multifactor de Azure de hello, haga clic en hello **Portal de usuarios** icono Hola deja menú, a continuación, haga clic en **instalar Portal de usuarios**.
2. Instalación de hello completa con los valores predeterminados de Hola a menos que necesite toochange les por algún motivo.
3. Enlazar un sitio de toohello de certificado SSL en IIS

   > [!NOTE]
   > Este certificado SSL suele ser un certificado SSL firmado públicamente.

4. Abra un explorador web desde cualquier equipo y explorar dirección URL de toohello donde se instaló el portal de usuarios de hello (ejemplo: https://mfa.contoso.com/MultiFactorAuth). Asegúrese de que no aparezca ningún error ni advertencia de certificado.

![Instalación del Portal de usuarios del servidor MFA](./media/multi-factor-authentication-get-started-portal/install.png)

Si tiene alguna pregunta acerca de cómo configurar un certificado SSL en un servidor IIS, vea el artículo de hello [cómo configurar SSL en IIS tooSet](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="deploy-hello-user-portal-on-a-separate-server"></a>Implementar el portal de usuarios de hello en un servidor independiente

Si servidor de Hola donde se ejecuta el servidor de autenticación multifactor de Azure no es accesible desde internet, debe instalar el portal de usuarios de hello en un **servidor independiente y orientado a internet**.

Si su organización usa Hola aplicación Authenticator de Microsoft como uno de los métodos de comprobación de Hola y desea toodeploy portal de usuarios de hello en su propio servidor, realizar Hola según los requisitos:

* Usar la versión 6.0 o posterior del programa Hola a servidor de autenticación multifactor de Azure.
* Instalar el portal de usuarios de hello en un servidor de web accesibles desde internet ejecuta Microsoft internet Information Services (IIS) 6.x o superior.
* Cuando se usa IIS 6.x, asegúrese de ASP.NET v2.0.50727 está instalado, registrado y establecido demasiado**permitido**.
* Si usa IIS 7.x o superior, IIS, incluida la autenticación básica, ASP.NET y la compatibilidad con la metabase de IIS 6.
* Portal de usuarios de hello segura con un certificado SSL.
* Hola SDK de servicio Web de Azure Multi-factor Authentication segura con un certificado SSL.
* Asegúrese de que portal de usuarios de hello puede conectarse toohello SDK de servicio Web de Azure Multi-factor Authentication a través de SSL.
* Asegúrese de que portal de usuarios de hello puede autenticar toohello SDK de servicio Web de Azure Multi-factor Authentication con credenciales de Hola de una cuenta de servicio en el grupo de seguridad de "PhoneFactor Admins" Hola. Esta cuenta de servicio y el grupo deben existir en Active Directory si Hola servidor Azure Multi-factor Authentication se ejecuta en un servidor unido a un dominio. Esta cuenta de servicio y el grupo existen localmente en hello servidor Azure Multi-factor Authentication si no es tooa Unidos a un dominio.

Instalar portal de usuarios de hello en un servidor distinto del servidor Azure Multi-factor Authentication Hola requiere Hola pasos:

1. **En el servidor MFA hello**, examinar ruta de instalación de toohello (ejemplo: C:\Program programa\multi-Factor Authentication Server) y copiar el archivo de hello **MultiFactorAuthenticationUserPortalSetup64** tooa ubicación donde se instalará el servidor de conexión a internet toohello accesible.
2. **En servidor de web a través de internet de hello**, ejecute el archivo de instalación de hello MultiFactorAuthenticationUserPortalSetup64 como administrador, cambiar Hola sitio si lo desea y cambiar el nombre corto de hello Virtual directory tooa si lo desea.
3. Enlazar un sitio de toohello de certificado SSL en IIS.

   > [!NOTE]
   > Este certificado SSL suele ser un certificado SSL firmado públicamente.

4. Examinar demasiado**C:\inetpub\wwwroot\MultiFactorAuth**
5. Editar el archivo Web.Config de hello en el Bloc de notas

    * Buscar la clave de hello **"USE_WEB_SERVICE_SDK"** y cambiar **valor = "false"** demasiado**valor = "true"**
    * Buscar la clave de hello **"WEB_SERVICE_SDK_AUTHENTICATION_USERNAME"** y cambiar **valor = ""** demasiado**valor = "Dominio\usuario"** donde dominio ombre de usuario es una cuenta de servicio que forma parte de Grupo de "PhoneFactor Admins".
    * Buscar la clave de hello **"WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD"** y cambiar **valor = ""** demasiado**valor = "Contraseña"** donde contraseña es la contraseña Hola Hola servicio Cuenta especificada en la línea anterior de Hola.
    * Buscar valor hello **https://www.contoso.com/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx** y cambie esta toohello de dirección URL de marcador de posición URL de SDK del servicio Web se instaló en el paso 2.
    * Guarde el archivo Web.Config de hello y cierre el Bloc de notas.

6. Abra un explorador web desde cualquier equipo y explorar dirección URL de toohello donde se instaló el portal de usuarios de hello (ejemplo: https://mfa.contoso.com/MultiFactorAuth). Asegúrese de que no aparezca ningún error ni advertencia de certificado.

Si tiene alguna pregunta acerca de cómo configurar un certificado SSL en un servidor IIS, vea el artículo de hello [cómo configurar SSL en IIS tooSet](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="configure-user-portal-settings-in-hello-azure-multi-factor-authentication-server"></a>Configurar las opciones de portal de usuario en hello servidor Azure Multi-factor Authentication

Ahora se instala dicho portal de usuarios de hello, deberá tooconfigure Hola servidor Azure Multi-factor Authentication toowork con el portal de Hola.

1. En la consola de servidor de autenticación multifactor de Azure de hello, haga clic en hello **Portal de usuarios** icono. En la pestaña de configuración de hello, escriba portal de usuarios de hello URL toohello con hello **dirección URL del Portal de usuario** cuadro de texto. Si se ha habilitado la funcionalidad de correo electrónico, esta dirección URL se incluye en los mensajes de correo electrónico de Hola se envían toousers cuando se importan en hello servidor Azure Multi-factor Authentication.
2. Elija la configuración de Hola que desea toouse Hola Portal de usuarios. Por ejemplo, si los usuarios pueden toochoose Asegúrese de los métodos de autenticación, que **permitir que los usuarios tooselect método** se activa, junto con los métodos de Hola que pueden elegir.
3. Definir quién debe ser administradores en hello **administradores** ficha. Puede crear permisos administrativos granulares con casillas de verificación de Hola y listas desplegables en los cuadros de hello Agregar/editar.

Configuración opcional:
- **Preguntas de seguridad** -definir aprobado preguntas de seguridad para el idioma de hello y entorno aparecen en.
- **Sesiones superadas**: configure la integración del portal de usuario con un sitio web basado en formularios con MFA.
- **IP de confianza** -permitir que los usuarios tooskip MFA al autenticar en una lista de direcciones IP o intervalos de confianza.

![Configurar el Portal de usuarios del servidor MFA](./media/multi-factor-authentication-get-started-portal/config.png)

Servidor de la autenticación multifactor de Azure ofrece varias opciones para el portal de usuarios de Hola. Hello tabla siguiente proporciona una lista de estas opciones y una explicación de lo que se utilizan.

| Configuración del portal de usuarios | Description |
|:--- |:--- |
| URL del portal de usuarios | Escriba la dirección URL de Hola de donde se hospeda el portal de Hola. |
| Autenticación principal | Especificar tipo de Hola de toouse de autenticación cuando inicien sesión en el portal de toohello. Autenticación de Windows, Radius o LDAP. |
| Permitir que los usuarios toolog en | Permitir a los usuarios tooenter un nombre de usuario y una contraseña en página de inicio de sesión de hello para el portal de usuarios de Hola. Si no se selecciona esta opción, cuadros de hello aparecen atenuadas. |
| Permitir inscripción de usuario | Permitir un tooenroll de usuario en la autenticación multifactor y tomarlas tooa pantalla de configuración que les solicite información adicional, como el número de teléfono. Solicitar teléfono de reserva permite a los usuarios toospecify un número de teléfono secundario. Símbolo del sistema de terceros token OATH permite toospecify a los usuarios un token OATH de terceros. |
| Permitir que los usuarios tooinitiate omisión por única vez | Permitir que los usuarios tooinitiate una omisión por única vez. Si un usuario configure esta opción, será necesario Hola efecto siguiente tiempo Hola usuario inicia sesión. Solicitar un bypass segundos proporciona usuario Hola con un cuadro para que puedan cambiar el valor predeterminado de Hola de 300 segundos. En caso contrario, la omisión por única vez Hola sólo es buena durante 300 segundos. |
| Permitir a los usuarios tooselect (método) | Permitir que los usuarios toospecify su método de contacto principal. Este método puede consistir en una llamada de teléfono, un mensaje de texto, una aplicación móvil o un token OATH. |
| Permitir a los usuarios tooselect idioma | Permitir a los usuarios de lenguaje de hello toochange que se usa para hello llamada de teléfono, mensaje de texto, aplicación móvil o token OATH. |
| Permitir que la aplicación móvil de los usuarios tooactivate | Permitir que los usuarios toogenerate un activación código toocomplete Hola aplicación móvil activación proceso que se usa con el servidor de Hola.  También puede establecer el número de Hola de dispositivos que se pueden activar aplicación de hello en, entre 1 y 10. |
| Usar preguntas de seguridad para la reserva | Permite preguntas de seguridad en caso de que la verificación en dos pasos genere un error. Puede especificar el número de Hola de preguntas de seguridad que se debe responder correctamente. |
| Permitir que el token OATH de terceros de los usuarios tooassociate | Permitir que los usuarios toospecify un token OATH de terceros. |
| Usar token OATH para la reserva | Permitir uso Hola de un token OATH en caso de que no es correcta la verificación en dos pasos. También puede especificar el tiempo de espera de sesión de hello en minutos. |
| Habilitación del registro | Habilitar el registro en el portal de usuarios de Hola. Hello archivos de registro se encuentra en: C:\Program programa\multi-Factor Authentication Server\Logs. |

Estos valores se convierten en usuario toohello visible en el portal de hello una vez que están activados y han iniciado sesión en el portal de usuarios de toohello.

![Configuración del portal de usuarios](./media/multi-factor-authentication-get-started-portal/portalsettings.png)

### <a name="self-service-user-enrollment"></a>Autoservicio de inscripción de usuarios

Si desea que su toosign a los usuarios e inscribir, debe seleccionar hello **permitir que los usuarios toolog en** y **permitir la inscripción de usuario** opciones en la ficha de configuración de Hola. Recuerde que la configuración de Hola que seleccione afectan a la experiencia de inicio de sesión del usuario de Hola.

Por ejemplo, cuando un usuario inicia sesión en el portal de usuarios de toohello para hello primera vez, a continuación, se toman toohello página de configuración de usuario de autenticación multifactor de Azure. Dependiendo de cómo haya configurado la autenticación multifactor Azure, usuario de hello puede ser capaz de tooselect su método de autenticación.

Si selecciona método de comprobación de llamada de voz de Hola o han sido previamente configurado toouse ese método, página de hello solicita Hola usuario tooenter su número de teléfono principal y la extensión, si corresponde. También pueden ser permitido tooenter un número de teléfono de reserva.

![Registrar número de teléfono principal y de reserva](./media/multi-factor-authentication-get-started-portal/backupphone.png)

Si el usuario de hello toouse requiere un PIN para la autenticación, página Hola les solicita toocreate un PIN. Después de escribir sus números de teléfono y PIN (si procede), el usuario de hello, haga clic en hello **Llamarme ahora tooAuthenticate** botón. La autenticación multifactor Azure realiza el número de teléfono principal del usuario toohello de comprobación de llamada de teléfono. usuario Hola debe responder llamada de teléfono de Hola y escriba su PIN (si procede) y presione # toomove toohello siguiente paso del proceso de inscripción automática de Hola.

Si el usuario Hola selecciona el método de verificación de los mensajes de texto de Hola o se ha configurado previamente toouse ese método, página Hola pide a usuario Hola su número de teléfono móvil. Si el usuario de hello toouse requiere un PIN para la autenticación, página de hello también les solicita tooenter un PIN.  Después de escribir su número de teléfono y PIN (si procede), el usuario de hello, haga clic en hello **Enviarme un SMS ahora tooAuthenticate** botón. La autenticación multifactor Azure realiza teléfono móvil SMS comprobación toohello de un usuario. usuario de Hello recibe el mensaje de texto hello con un solo-tiempo-código de acceso (OTP) y, a continuación, mensaje de toohello de respuestas con ese OTP más su PIN (si procede).

![SMS del portal de usuarios](./media/multi-factor-authentication-get-started-portal/text.png)

Si Hola seleccionará el método de comprobación de aplicación móvil de hello, página Hola solicita la aplicación hello usuario tooinstall Hola Microsoft Authenticator en su dispositivo y generar un código de activación. Después de instalar la aplicación hello, usuario de hello, hace clic en botón Generar código de activación de Hola.

> [!NOTE]
> aplicación de Microsoft Authenticator de hello toouse, usuario Hola debe habilitar las notificaciones de inserción para su dispositivo.

página de Hello, a continuación, muestra un código de activación y una dirección URL junto con una imagen de código de barras. Si el usuario de hello toouse requiere un PIN para la autenticación, página de hello además les solicita tooenter un PIN. usuario Hola entra en el código de activación de Hola y la dirección URL en la aplicación de Microsoft Authenticator de Hola o usa imagen de código de barras de hello código de barras escáner tooscan Hola y hace clic en el botón Activar de Hola.

Una vez completada la activación de hello, usuario de hello, haga clic en hello **Autenticarme ahora** botón. La autenticación multifactor Azure realiza la aplicación móvil del usuario de toohello de comprobación. usuario de Hello debe introducir su PIN (si procede) y presione el botón de autenticar de hello en su aplicación móvil toomove en toohello siguiente paso del proceso de inscripción automática de Hola.

Si han configurado los administradores de Hola Hola servidor Azure Multi-factor Authentication toocollect seguridad preguntas y respuestas, usuario hello, a continuación, se toma la página de preguntas de seguridad toohello. usuario de Hello debe seleccionar cuatro preguntas de seguridad y proporcionar respuestas preguntas tootheir seleccionado.

![Preguntas de seguridad del portal de usuarios](./media/multi-factor-authentication-get-started-portal/secq.png)

inscripción automática de usuarios de Hola se habrá completada y usuario de hello ha iniciado sesión en el portal de usuarios de toohello. Los usuarios puedan iniciar sesión en el portal de usuarios de toohello en cualquier momento en hello futuras toochange sus números de teléfono, PIN, métodos de autenticación y preguntas de seguridad si cambiar sus métodos se permite los administradores.

## <a name="next-steps"></a>Pasos siguientes

- [Implementar el servicio Web de aplicación móvil de Azure Multi-factor Authentication Server Hola](multi-factor-authentication-get-started-server-webservice.md)
