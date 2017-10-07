---
title: "actualización del servidor de MFA de aaaAzure | Documentos de Microsoft"
description: "Los pasos y orientación tooupgrade Hola versión más reciente de tooa de servidor de autenticación multifactor de Azure."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: aaa8d400e0e5f1c6be3a6d22cde6dd893ef4d546
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-toohello-latest-azure-multi-factor-authentication-server"></a>Actualizar toohello más reciente servidor de autenticación multifactor de Azure

Este artículo le guiará a través de hello proceso de actualización de la versión 6.0 de servidor Azure Multi-factor Authentication (MFA) o superior. Si necesita una versión anterior de PhoneFactor Agent hello tooupgrade, consulte demasiado[actualización hello PhoneFactor Agent tooAzure servidor Multi-factor Authentication](multi-factor-authentication-get-started-server-upgrade.md).

Si está actualizando desde v6.x o toov7.x anterior o posterior, cambien todos los componentes de too.NET 2.0 de .NET 4.5. Todos los componentes también requieren Microsoft Visual C++ 2015 Redistributable Update 1 o una versión superior. instalador de servidor MFA de Hello instala ambas versiones de hello x86 y x64 de estos componentes si no están ya instalados. Si Hola Portal de usuarios y servicio de la aplicación Web móvil que se ejecutan en servidores diferentes, deberá tooinstall esos paquetes antes de actualizar los componentes. Puede buscar actualización más reciente de Microsoft Visual C++ 2015 Redistributable hello en hello [Microsoft Download Center](https://www.microsoft.com/en-us/download/). 

## <a name="install-hello-latest-version-of-azure-mfa-server"></a>Instale Hola la versión más reciente del servidor Azure MFA

1. Siga las instrucciones de hello en [descarga Hola servidor Azure Multi-factor Authentication](multi-factor-authentication-get-started-server.md#download-the-azure-multi-factor-authentication-server) versión más reciente de hello tooget de hello servidor Azure MFA.
2. Realizar una copia de seguridad del archivo de datos del servidor MFA Hola ubicado en C:\Program programa\multi-Factor Authentication Server\Data\PhoneFactor.pfdata (ubicación de instalación de suponiendo un saludo predeterminado) en el servidor principal de MFA.
3. Si ejecuta varios servidores para alta disponibilidad, cambiar los sistemas de Hola que autentican toohello servidor MFA para que detengan enviar tráfico toohello servidores que van a actualizar. Si usa un equilibrador de carga, quitar un servidor de MFA de equilibrador de carga de hello, Hola actualización y, a continuación, vuelva a agregar servidor hello a granja de servidores de Hola.
4. Ejecute el instalador nuevo de hello en cada servidor de MFA. Actualizar los servidores subordinados en primer lugar porque pueden leer Hola antiguo archivo de datos está replicando maestro Hola. 

  No es necesario toouninstall el servidor de MFA actual antes de ejecutar instalador Hola. instalador de Hello lleva a cabo una actualización en contexto. Hello ruta de instalación recoge desde el registro de hello de instalación anterior de hello, por lo que instala en hello misma ubicación (por ejemplo, C:\Program programa\multi-Factor Authentication Server). 
  
5. Si le tooinstall solicitadas Microsoft Visual C++ 2015 Redistributable actualización paquete, Aceptar Hola aviso. Se instalan las versiones de x86 y x64 de Hola de paquetes de saludo.
5. Si usas Hola SDK del servicio Web, se le solicitará tooinstall Hola nuevo SDK del servicio Web. Cuando se instala Hola nuevo SDK del servicio Web, asegúrese de que ese nombre de directorio virtual Hola coincide con directorio virtual Hola instalado anteriormente (por ejemplo, MultiFactorAuthWebServiceSdk).
6. Repita los pasos de hello en todos los servidores subordinados. Promover uno de hello subordinados toobe Hola nuevo maestro y, a continuación, Hola actualización antiguo servidor maestro. 

## <a name="upgrade-hello-user-portal"></a>Actualizar Hola Portal de usuarios

1. Realizar una copia de seguridad del archivo web.config de Hola que se encuentra en el directorio virtual de Hola de hello ubicación de instalación del Portal de usuarios (por ejemplo, C:\inetpub\wwwroot\MultiFactorAuth). Si se realizan cambios en el tema predeterminado toohello, realizar una copia de seguridad de carpeta también de hello App_Themes\Default. Es mejor toocreate una copia de la carpeta predeterminada de Hola y crear un nuevo tema de tema de toochange Hola predeterminado.
2. Si Hola Portal de usuarios se ejecuta en Hola Hola mismo servidor como Hola otros componentes de servidor MFA, instalación de servidor MFA le pide que tooupdate Hola Portal de usuarios. Aceptar el aviso de hello e instale la actualización del Portal de usuarios de Hola. Comprobar ese nombre de directorio virtual Hola coincide con un directorio virtual de hello instalado anteriormente (por ejemplo, MultiFactorAuth).
3. Si Hola Portal de usuarios está en su propio servidor, copiar el archivo de MultiFactorAuthenticationUserPortalSetup64.msi de Hola de hello instale ubicación de uno de los servidores de MFA de Hola y colocarla en el servidor web de Portal de usuarios de Hola. Ejecute al instalador de Hola. 

  Si se produce un error que indica, "Microsoft Visual C++ 2015 Redistributable Update 1 o posterior es necesario," descargar e instalar paquete de actualización más reciente de Hola de hello [Microsoft Download Center](https://www.microsoft.com/download/). Instalar las versiones de x86 y x64 de Hola.

4. Una vez Hola actualizado el software está instalado el Portal de usuarios, comparar copia de seguridad de web.config de hello realizada en el paso 1 con el archivo web.config de la nueva hello. Si no existe ningún atributo nuevo en el archivo web.config nuevo de hello, copie su copia de seguridad web.config en Hola Hola de toooverwrite de directorio virtual nuevo. Otra opción es hello SDK del servicio Web desde el archivo de copia de seguridad de hello en web.config nuevo hello y valores de toocopy y pegar Hola appSettings.

Si tienes Hola Portal de usuarios en varios servidores, repita instalación hello en todos ellos. 


## <a name="upgrade-hello-mobile-app-web-service"></a>Hola actualización de servicio de la aplicación Web móvil

1. Realizar una copia de seguridad del archivo web.config de Hola que está en el directorio virtual de Hola de hello ubicación de instalación del servicio de la aplicación Web móvil (por ejemplo, C:\inetpub\wwwroot\app o C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService).
2. Archivo de copia hello MultiFactorAuthenticationMobileAppWebServiceSetup64.msi de hello ubicación del programa Hola a servidores de MFA de instalación y colóquelo en el servidor de web de registro de aplicación móvil de Hola.
3. Ejecute al instalador de Hola. 

  Si se produce un error que indica que Microsoft Visual C++ 2015 Redistributable Update 1 o posterior es necesario, descargue e instale el paquete de actualización más reciente de Hola desde hello [Microsoft Download Center](https://www.microsoft.com/download/). Instalar las versiones de x86 y x64 de Hola.

4. Una vez instalado el software de servicio de la aplicación Web móvil Hola actualizado, comparar archivo web.config de Hola que se copió en el paso 1 con el nuevo archivo de web.config Hola. Si no existe ningún atributo nuevo en el archivo web.config nuevo de hello, puede copiar al archivo web.config guardados en el directorio virtual de Hola y sobrescribir Hola uno nuevo. Otra opción es hello SDK del servicio Web desde el archivo de copia de seguridad de hello en web.config nuevo hello y valores de toocopy y pegar Hola appSettings.

Si tienes Hola servicio Web de aplicación móvil en varios servidores, repita instalación hello en todos ellos. 

## <a name="upgrade-hello-ad-fs-adapters"></a>Actualizar Hola adaptadores de AD FS


### <a name="if-mfa-runs-on-different-servers-than-ad-fs"></a>Si MFA se ejecuta en distintos servidores de AD FS

Estas instrucciones solo se aplican si ejecuta el Servidor Multi-Factor Authentication por separado de los servidores de AD FS. Si ambos servicios se ejecutan Hola los mismos servidores, omita esta sección y vaya toohello pasos de instalación. 

1. Guardar una copia del archivo MultiFactorAuthenticationAdfsAdapter.config hello que se registró en AD FS o exportar la configuración de hello mediante el siguiente comando de PowerShell de hello: `Export-AdfsAuthenticationProviderConfigurationData -Name [adapter name] -FilePath [path tooconfig file]`. nombre del adaptador Hello es "WindowsAzureMultiFactorAuthentication" o "AzureMfaServerAuthentication" según versión Hola previamente instalada.
2. Copie Hola siguientes archivos de servidores de hello servidor MFA instalación ubicación toohello AD FS:

  - MultiFactorAuthenticationAdfsAdapterSetup64.msi
  - Register-MultiFactorAuthenticationAdfsAdapter.ps1
  - Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
  - MultiFactorAuthenticationAdfsAdapter.config

3. Editar script de Hola Register-MultiFactorAuthenticationAdfsAdapter.ps1 agregando `-ConfigurationFilePath [path]` toohello final de hello `Register-AdfsAuthenticationProvider` comando. Reemplace *[path]* con toohello de ruta de acceso completa de hello MultiFactorAuthenticationAdfsAdapter.config archivo o archivo de configuración de Hola se exportó en el paso anterior de Hola. 

  Compruebe los atributos de hello en hello nueva MultiFactorAuthenticationAdfsAdapter.config toosee si coinciden con el archivo de configuración antiguo de Hola. Si los atributos se agregaron o quitaron en la nueva versión de hello, copiar valores de atributo de Hola de toohello de archivo de configuración anterior de hello uno nuevo o modificar hello toomatch de archivo de configuración anterior.

### <a name="install-new-ad-fs-adapters"></a>Instalación de nuevos adaptadores de AD FS

> [!IMPORTANT] 
> Los usuarios no estarán verificacion tooperform necesaria durante los pasos del 3 al 8 de esta sección. Si tiene AD FS configurado en varios clústeres, puede quitar, actualizar y restaurar la granja de servidores de cada clúster Hola independientemente de Hola otro clústeres tooavoid el tiempo de inactividad.

1. Quite algunos servidores de AD FS de granja de servidores de Hola. Actualización de estos servidores al Hola que otras siguen en ejecución.
2. Instale el nuevo adaptador de AD FS hello en cada servidor quitado de la granja de servidores de hello AD FS. Si Hola servidor MFA está instalado en cada servidor de AD FS, puede actualizar a través del administrador del servidor de MFA de hello UX. En caso contrario, actualice ejecutando MultiFactorAuthenticationAdfsAdapterSetup64.msi. 

  Si se produce un error que indica, "Microsoft Visual C++ 2015 Redistributable Update 1 o posterior es necesario," descargar e instalar paquete de actualización más reciente de Hola de hello [Microsoft Download Center](https://www.microsoft.com/download/). Instalar las versiones de x86 y x64 de Hola.

3. Vaya demasiado**AD FS** > **las directivas de autenticación** > **Editar directiva de autenticación MultiFactor Global**. Desactive la opción **WindowsAzureMultiFactorAuthentication** o **AzureMFAServerAuthentication** (dependiendo de la versión actual de hello instalada). 

  Una vez completado este paso, la verificación en dos pasos a través del Servidor MFA no estará disponible en este clúster de AD FS hasta que finalice el paso 8.

4. Versión más antigua de Hola de anular el registro del adaptador de hello AD FS mediante la ejecución de secuencias de comandos de PowerShell Unregister-MultiFactorAuthenticationAdfsAdapter.ps1 Hola. Asegúrese de que hello *-nombre* parámetro ("WindowsAzureMultiFactorAuthentication" o "AzureMFAServerAuthentication") coincide con nombre de Hola que se muestra en el paso 3. Esto aplica tooall servidores en clúster de hello misma instancia de AD FS porque no hay una configuración central.
5. Registrar nuevo adaptador de AD FS hello mediante la ejecución de secuencias de comandos de PowerShell de Register-MultiFactorAuthenticationAdfsAdapter.ps1 Hola. Esto aplica tooall servidores en clúster de hello misma instancia de AD FS porque no hay una configuración central.
6. Hola de reinicio del servicio de AD FS en cada servidor quitará Hola granja de AD FS.
7. Agregar servidores de Hola actualizar de nuevo el conjunto de servidores de toohello AD FS y quitar Hola otros servidores de granja de servidores de Hola.
8. Vaya demasiado**AD FS** > **las directivas de autenticación** > **Editar directiva de autenticación MultiFactor Global**. Active **AzureMfaServerAuthentication**.
9. Repita el paso 2: servidores de hello tooupdate ahora se quita de la granja de servidores de hello AD FS y reinicie el servicio de hello AD FS en esos servidores.
10. Agregue esos servidores en la granja de servidores de AD FS Hola.

## <a name="next-steps"></a>Pasos siguientes

- Ejemplos de [escenarios avanzados con Azure Multi-Factor Authentication y VPN de terceros](multi-factor-authentication-advanced-vpn-configurations.md)

- [Sincronización de Servidores MFA con Windows Server Active Directory](multi-factor-authentication-get-started-server-dirint.md)

- [Configuración de la autenticación de Windows](multi-factor-authentication-get-started-server-windows.md) para sus aplicaciones
