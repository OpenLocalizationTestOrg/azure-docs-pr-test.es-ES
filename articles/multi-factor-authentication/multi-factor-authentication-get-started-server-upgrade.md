---
title: aaaUpgrade PhoneFactor tooAzure servidor MFA | Documentos de Microsoft
description: Empezar a trabajar con el servidor Azure MFA cuando se actualiza desde el agente de phonefactor anterior Hola.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 42838ff7-bdf2-4d06-bacc-b3839a00cd76
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.openlocfilehash: 15b7b8517929c30f66e6a39cd44c69d12d25c6d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hello-phonefactor-agent-tooazure-multi-factor-authentication-server"></a>Actualizar hello PhoneFactor Agent tooAzure servidor Multi-factor Authentication
tooupgrade Hola PhoneFactor Agent v5.x o anterior tooAzure servidor Multi-factor Authentication, desinstalar hello PhoneFactor Agent y afiliado componentes en primer lugar. Hola, a continuación, servidor de autenticación multifactor y sus componentes afiliados pueden instalarse.

## <a name="uninstall-hello-phonefactor-agent"></a>Desinstalar hello PhoneFactor Agent

1. En primer lugar, copia el archivo de datos de PhoneFactor de Hola. ubicación de instalación predeterminada de Hello es C:\Program Files\PhoneFactor\Data\Phonefactor.pfdata.

2. Si está instalado Hola Portal de usuarios:
  1. Desplazarse por las carpetas de instalación de toohello y copia el archivo web.config de Hola. ubicación de instalación de Hello predeterminada es C:\inetpub\wwwroot\PhoneFactor.

  2. Si ha agregado el portal de temas personalizados toohello, realizar una copia de la carpeta personalizada hello C:\inetpub\wwwroot\PhoneFactor\App_Themes directorio.

  3. Desinstalar Hola Portal de usuarios a través de hello PhoneFactor Agent (sólo está disponible si se instala en hello mismo servidor que Hola PhoneFactor Agent) o a través de programas de Windows y las características.

3. Si está instalado Hola servicio Web de aplicación móvil:

  1. Vaya toohello carpeta de instalación y hacer copia de seguridad del archivo web.config de Hola. ubicación de instalación de Hello predeterminada es C:\inetpub\wwwroot\PhoneFactorPhoneAppWebService.

  2. Desinstalar Hola servicio Web de aplicación móvil a través de programas de Windows y las características.

4. Si está instalado el SDK del servicio Web de hello, debe desinstalar a través de hello PhoneFactor Agent o programas de Windows y las características.

5. Desinstalar hello PhoneFactor Agent a través de programas de Windows y las características.

## <a name="install-hello-multi-factor-authentication-server"></a>Instalar Hola servidor Multi-factor Authentication

Hello ruta de instalación recoge desde el registro de hello de instalación de PhoneFactor Agent anterior hello, por lo tanto debe instalar en hello mismo ubicación (por ejemplo, C:\Program programa\phonefactor). Las instalaciones nuevas tendrán una ruta de instalación predeterminada diferente (por ejemplo, C:\Archivos de programa\Servidor Multi-Factor Authentication). Hola Hola anterior que phonefactor Agent deben actualizarse durante la instalación, por lo que los usuarios y la configuración todavía debe ser que existe después de instalar Hola nuevo servidor de autenticación multifactor a la izquierda el archivo de datos.

1. Si se le solicita, activar Hola servidor Multi-factor Authentication y asegúrese de que se asigna el grupo de replicación correcto toohello.

2. Si instala el SDK del servicio Web se instaló previamente, el Hola Hola nuevo SDK del servicio Web a través de la interfaz de usuario de servidor de autenticación multifactor de Hola.

  Hola de forma predeterminada, el nombre de directorio virtual es ahora **MultiFactorAuthWebServiceSdk** en lugar de **PhoneFactorWebServiceSdk**. Si desea que el nombre anterior de toouse hello, debe cambiar nombre hello del directorio virtual de Hola durante la instalación. En caso contrario, si permite Hola install toouse Hola nuevo nombre predeterminado, tiene toochange Hola dirección URL en todas las aplicaciones que Hola referencia toopoint SDK del servicio Web (como Hola Portal de usuarios y el servicio de la aplicación Web móvil) en la ubicación correcta de Hola.

3. Si instala Hola Portal de usuarios se instaló previamente en hello servidor PhoneFactor Agent, Hola nuevo Portal de usuarios de la autenticación multifactor a través de la interfaz de usuario de servidor de autenticación multifactor de Hola.

  Hola de forma predeterminada, el nombre de directorio virtual es ahora **MultiFactorAuth** en lugar de **PhoneFactor**. Si desea que el nombre anterior de toouse hello, debe cambiar nombre hello del directorio virtual de Hola durante la instalación. En caso contrario, si permite que Hola install toouse Hola nuevo nombre predeterminado, debe haga clic en el icono de Portal de usuarios de Hola Hola servidor Multi-factor Authentication y actualizar Hola dirección URL del Portal de usuario en la pestaña de configuración de Hola.

4. Si hello Portal de usuario o el servicio Web de aplicación móvil estaba instalado previamente en un servidor diferente de hello PhoneFactor Agent:

  1. Vaya toohello ubicación de instalación (por ejemplo, C:\Program programa\phonefactor) y copiar uno o más toohello instaladores otro servidor. Hay instaladores de 32 bits y 64 bits para hello Portal de usuarios y el servicio de la aplicación Web móvil. Se denominan MultiFactorAuthenticationUserPortalSetupXX.msi y MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi.

  2. Hola tooinstall Portal de usuarios en el servidor web de hello, abra un símbolo del sistema como administrador y ejecute MultiFactorAuthenticationUserPortalSetupXX.msi.

    Hola de forma predeterminada, el nombre de directorio virtual es ahora **MultiFactorAuth** en lugar de **PhoneFactor**. Si desea que el nombre anterior de toouse hello, debe cambiar nombre hello del directorio virtual de Hola durante la instalación. En caso contrario, si permite que Hola install toouse Hola nuevo nombre predeterminado, debe haga clic en el icono de Portal de usuarios de Hola Hola servidor Multi-factor Authentication y actualizar Hola dirección URL del Portal de usuario en la pestaña de configuración de Hola. Los usuarios existentes necesitan toobe informado de hello nueva dirección URL.

  3. Vaya toohello ubicación de instalación de Portal de usuarios (por ejemplo, C:\inetpub\wwwroot\MultiFactorAuth) y edite el archivo web.config de Hola. Copiar valores de hello en secciones de hello appSettings y applicationSettings del archivo web.config original que se copió antes de la actualización de hello en el archivo web.config de la nueva Hola. Si el nuevo nombre de directorio virtual predeterminado Hola se mantiene al instalar Hola SDK del servicio Web, cambie la dirección URL de hello en la ubicación correcta de hello applicationSettings sección toopoint toohello. Si los demás valores predeterminados se han cambiado en el archivo web.config anterior de hello, se aplican los mismos cambios toohello nuevo archivo web.config.

  4. Hola tooinstall servicio de la aplicación Web móvil en el servidor web de hello, abra un símbolo del sistema como administrador y ejecute hello MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi.

    Hola de forma predeterminada, el nombre de directorio virtual es ahora **MultiFactorAuthMobileAppWebService** en lugar de **PhoneFactorPhoneAppWebService**. Si desea que el nombre anterior de toouse hello, debe cambiar nombre hello del directorio virtual de Hola durante la instalación. Puede que desee toochoose un toomake nombre más corto más sencilla para los usuarios finales tootype en sus dispositivos móviles. En caso contrario, si permite Hola install toouse Hola nuevo nombre predeterminado, debe haga clic en el icono de la aplicación móvil de Hola Hola servidor Multi-factor Authentication y actualizar Hola URL de servicio Web de aplicación móvil.

  5. Vaya ubicación de instalación de servicio de la aplicación Web móvil toohello (por ejemplo, C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService) y edite el archivo web.config de Hola. Copiar valores de hello en secciones de hello appSettings y applicationSettings del archivo web.config original que se copió antes de la actualización de hello en el archivo web.config de la nueva Hola. Si el nuevo nombre de directorio virtual predeterminado Hola se mantiene al instalar Hola SDK del servicio Web, cambie la dirección URL de hello en la ubicación correcta de hello applicationSettings sección toopoint toohello. Si los demás valores predeterminados se han cambiado en el archivo web.config anterior de hello, se aplican los mismos cambios toohello nuevo archivo web.config.

## <a name="next-steps"></a>Pasos siguientes

- [Instalar el portal de usuarios de hello](multi-factor-authentication-get-started-portal.md) para hello servidor Azure Multi-factor Authentication.

- [Configuración de la autenticación de Windows](multi-factor-authentication-get-started-server-windows.md) para sus aplicaciones. 
