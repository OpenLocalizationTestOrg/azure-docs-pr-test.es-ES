---
title: "Servicio de Web de aplicación móvil de MFA Server aaaAzure | Documentos de Microsoft"
description: "aplicación de Microsoft Authenticator Hello ofrece una opción de autenticación fuera de banda adicional.  Permite hello toousers de notificaciones de inserción MFA server toouse."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 6c8d6fcc-70f4-4da4-9610-c76d66635b8b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 4175b68fcbf85ec3fd53d8edf4e07306c75a4c71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-mobile-app-authentication-with-azure-multi-factor-authentication-server"></a>Habilitación de la autenticación de aplicación móvil con Servidor Azure Multi-Factor Authentication

aplicación de Microsoft Authenticator Hello ofrece una opción de comprobación de fuera de banda adicional. En lugar de colocar una llamada de teléfono automática o un usuario de toohello SMS durante el inicio de sesión, la autenticación multifactor Azure inserta una aplicación de Microsoft Authenticator toohello de notificación del usuario de hello smartphone o Tablet PC. Hola usuario simplemente toca **compruebe** (o escribir un código PIN y toca "Autenticar") en Hola toocomplete de aplicación en su inicio de sesión.

Se recomienda usar una aplicación móvil para la verificación en dos pasos cuando la recepción telefónica es poco confiable. Si usa la aplicación hello como un generador de token OATH, que no requiere ninguna conexión de red o internet.

Dependiendo de su entorno, puede que desee toodeploy el servicio de web de aplicación móvil de hello en hello mismo servidor como servidor de autenticación multifactor de Azure o en otro servidor orientado a internet.

## <a name="requirements"></a>Requisitos

aplicación de Microsoft Authenticator de hello toouse, siguiente Hola es necesarias para que hello aplicación pueda comunicarse correctamente con el servicio Web de aplicación móvil:

* Servidor Azure Multi-Factor Authentication v6.0 o superior.
* Debe instalar el servicio web de aplicación móvil en un servidor web con conexión a Internet con Microsoft® [Internet Information Services (IIS) 7.x o superior](http://www.iis.net/).
* ASP.NET v4.0.30319 está instalado, registrado y establecer tooAllowed
* Entre los servicios de rol necesarios, se incluyen ASP.NET y Compatibilidad con la metabase de IIS 6.
* Se debe poder tener acceso al servicio web de aplicación móvil mediante una dirección URL pública.
* El servicio web de aplicación móvil debe estar protegido con un certificado SSL.
* Instalar Hola SDK de servicio Web de Azure Multi-factor Authentication en IIS 7.x o superior en hello **mismo servidor como servidor Azure Multi-factor Authentication Hola**
* Hola SDK de servicio Web de Azure Multi-factor Authentication está protegido con un certificado SSL.
* Servicio Web de aplicación móvil puede conectarse toohello SDK de servicio Web de Azure Multi-factor Authentication mediante SSL
* Servicio Web de aplicación móvil puede autenticar toohello SDK de servicio Web de Azure MFA con hello credenciales de una cuenta de servicio que sea miembro del grupo de seguridad de "PhoneFactor Admins" Hola. Esta cuenta de servicio y el grupo existen en Active Directory si Hola servidor Azure Multi-factor Authentication está en un servidor unido a un dominio. Esta cuenta de servicio y el grupo existen localmente en hello servidor Azure Multi-factor Authentication si no es tooa Unidos a un dominio.

## <a name="install-hello-mobile-app-web-service"></a>Instalar el servicio web de aplicación móvil de Hola

Antes de instalar el servicio web de aplicación móvil de hello, tenga en cuenta de hello detalles siguientes:

* Necesita una cuenta de servicio que forme parte del grupo "PhoneFactor Admins". Esta cuenta puede ser Hola igual que uno Hola usada para la instalación del Portal de usuarios de Hola.
* Es útil tooopen un explorador web en el servidor web de hello orientado a Internet y explorar dirección URL de toohello de hello SDK del servicio Web que se escribió en el archivo web.config de Hola. Si explorador Hola puede llegar a servicio web de toohello correctamente, debe solicitarle las credenciales. Escriba el nombre de usuario de Hola y la contraseña que escribiste en el archivo web.config de hello tal y como aparece en el archivo hello. Asegúrese de que no aparezca ningún error ni advertencia de certificado.
* Si un proxy inverso o firewall está sentado frente a servidor web de servicio de la aplicación Web móvil de Hola y realización de la descarga de SSL, puede editar el archivo web.config de servicio Web de aplicación móvil de Hola para que hello servicio Web de aplicación móvil pueda usar http en lugar de https. SSL sigue siendo necesario de hello proxy de aplicación móvil toohello inverso/firewall. Agregar Hola después toohello clave \<appSettings\> sección:

        <add key="SSL_REQUIRED" value="false"/>

### <a name="install-hello-web-service-sdk"></a>Instalar SDK del servicio web Hola

En estos escenarios, si hello SDK de servicio Web de Azure Multi-factor Authentication es **no** ya instalados en hello servidor Azure Multi-factor Authentication (MFA), Hola completa los pasos siguientes.

1. Abra la consola de servidor de autenticación multifactor de Hola.
2. Vaya toohello **SDK del servicio Web** y seleccione **instalar SDK del servicio Web**.
3. Instalación de hello completa con los valores predeterminados de Hola a menos que necesite toochange les por algún motivo.
4. Enlazar un sitio de toohello de certificado SSL en IIS.

Si tiene alguna pregunta acerca de cómo configurar un certificado SSL en un servidor IIS, vea el artículo de hello [cómo configurar SSL en IIS tooSet](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Hola SDK del servicio Web debe estar protegido con un certificado SSL. Un certificado autofirmado es adecuado para este propósito. Importar certificado Hola Hola "Entidades de certificación de raíz de confianza" almacén de cuenta de equipo Local de hello en el servidor web de Portal de usuarios de Hola para que confíe en ese certificado cuando se inicie la conexión de SSL de Hola.

![SDK del servicio web de configuración del Servidor MFA](./media/multi-factor-authentication-get-started-server-webservice/sdk.png)

### <a name="install-hello-service"></a>Instalar servicio de Hola

1. **En el servidor MFA hello**, busque la ruta de instalación de toohello.
2. Navegue toohello carpeta donde hello servidor Azure MFA es predeterminado de hello instalada es **C:\Program Files\Azure Multi-factor Authentication**.
3. Buscar archivo de instalación de hello **MultiFactorAuthenticationMobileAppWebServiceSetup64**. Si el servidor de hello **no** orientado a Internet, servidor de copia Hola instalación archivos toohello orientado a Internet.
4. Si hello es servidor MFA **no** conmutador orientado a internet toohello **servidor orientado a internet**.
5. Ejecute hello **MultiFactorAuthenticationMobileAppWebServiceSetup64** instalar el archivo como un administrador, cambiar Hola sitio si lo desea y cambiar el nombre corto de hello Virtual directory tooa si lo desea.
6. Después de la instalación de hello acabado, examinar demasiado**C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService** (o el directorio correspondiente según el nombre del directorio virtual de hello) y edite el archivo Web.Config de Hola.

   * Buscar la clave de hello **"WEB_SERVICE_SDK_AUTHENTICATION_USERNAME"** y cambiar **valor = ""** demasiado**valor = "Dominio\usuario"** donde dominio ombre de usuario es una cuenta de servicio que forma parte de Grupo de "PhoneFactor Admins".
   * Buscar la clave de hello **"WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD"** y cambiar **valor = ""** demasiado**valor = "Contraseña"** donde contraseña es la contraseña Hola Hola servicio Cuenta especificada en la línea anterior de Hola.
   * Buscar hello **configuración de pfMobile App Web Service_pfwssdk_PfWsSdk** configuración y cambie el valor de Hola de **http://localhost:4898/PfWsSdk.asmx** toohello URL del SDK de servicio Web (ejemplo: https://mfa.contoso.com/ MultiFactorAuthWebServiceSdk/PfWsSdk.asmx).
   * Guarde el archivo Web.Config de hello y cierre el Bloc de notas.

   > [!NOTE]
   > Dado que SSL se utiliza para esta conexión, debe hacer referencia Hola SDK del servicio Web por **nombre de dominio completo (FQDN)** y **no dirección IP**. Hello certificado SSL habría emitió para hello FQDN y hello dirección URL usada debe coincidir con hello nombre certificado Hola.

7. Si el sitio Web de Hola que se instaló el servicio de Web de aplicación móvil ya no se ha enlazado con un certificado firmado públicamente, instalar certificado de hello en el servidor de hello, abra el Administrador de IIS y enlazar el sitio Web de hello certificado toohello.
8. Abra un explorador web desde cualquier equipo y explorar dirección URL de toohello donde se instaló el servicio Web de aplicación móvil (ejemplo: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService). Asegúrese de que no aparezca ningún error ni advertencia de certificado.

## <a name="configure-hello-mobile-app-settings-in-hello-azure-multi-factor-authentication-server"></a>Configurar opciones de aplicación móvil de Hola Hola servidor Azure Multi-factor Authentication

Ahora que está instalado el servicio web de aplicación móvil de hello, necesita tooconfigure Hola servidor Azure Multi-factor Authentication toowork con el portal de Hola.

1. En la consola de servidor de autenticación multifactor de hello, haga clic en el icono de Portal de usuarios de Hola. Comprobación de los métodos de autenticación, si los usuarios pueden toocontrol **aplicación móvil** en la pestaña de configuración de hello, en **permiten a los usuarios tooselect método**. Sin esta característica está habilitada, los usuarios finales son toocontact requiere la activación de toocomplete del departamento de soporte técnico para hello aplicación móvil.
2. Comprobar hello **permitir que los usuarios tooactivate aplicación móvil** cuadro.
3. Comprobar hello **permitir inscripción de usuario** cuadro.
4. Haga clic en hello **aplicación móvil** icono.
5. Escriba la URL Hola usada con el directorio virtual Hola que se creó al instalar MultiFactorAuthenticationMobileAppWebServiceSetup64 (ejemplo: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService/) en el campo de hello  **Dirección URL del servicio Web de aplicación móvil:**.
6. Rellenar hello **nombre de la cuenta** campo con toodisplay de nombre de hello empresa u organización en la aplicación móvil de Hola para esta cuenta.
   ![Valores de la aplicación móvil para la configuración del servidor MFA](./media/multi-factor-authentication-get-started-server-webservice/mobile.png)

## <a name="next-steps"></a>Pasos siguientes

- [Escenarios avanzados con Azure Multi-Factor Authentication y VPN de terceros](multi-factor-authentication-advanced-vpn-configurations.md).