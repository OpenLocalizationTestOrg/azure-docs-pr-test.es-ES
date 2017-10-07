---
title: "aaaSettings y preguntas más frecuentes de itinerancia de datos | Documentos de Microsoft"
description: "Proporciona respuestas toosome preguntas los administradores de TI podrían tener sobre la configuración y sincronización de datos de aplicaciones."
services: active-directory
keywords: "configuración de enterprise state roaming, nube de windows, preguntas más frecuentes sobre enterprise state roaming"
documentationcenter: 
author: tanning
manager: swadhwa
editor: curtand
ms.assetid: c0824f5c-129b-4240-969f-921f6a64eae7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4d6d6619b3a5fbd1d274603808d89b73ed942cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="settings-and-data-roaming-faq"></a>Preguntas más frecuentes sobre itinerancia de datos y configuración
Este tema responde a algunas preguntas que los administradores de TI podrían tener sobre la sincronización de datos de aplicación y la configuración.

## <a name="what-data-roams"></a>¿Qué datos se movilizan?
**Configuración de Windows**: Hola configuración de PC que está integrada en el sistema operativo de Windows hello. Por lo general, ésta es configuración personalizar su PC, e incluyen hello después amplias categorías:

* *Tema*, que incluye características como la configuración de tema y la barra de tareas del escritorio.
* *Configuración de Internet Explorer*, como pestañas abiertas recientemente y favoritos.
* *Configuración del explorador Edge*, como favoritos y lista de lectura.
* *Contraseñas*, entre las que se incluyen las contraseñas de Internet, perfiles de Wi-Fi, y otras.
* *Preferencias de idioma*, que incluye la configuración de la distribución del teclado, el idioma del sistema, la fecha y hora, y mucho más.
* *Características de facilidad de acceso*, como el tema de contraste alto, narrador o lupa
* *Otra configuración de Windows*, como la configuración de símbolo del sistema y la lista de aplicaciones.

**Datos de la aplicación**: aplicaciones universales de Windows pueden escribir tooa de datos de configuración de la carpeta móviles y los datos escritos toothis carpeta se sincronizará automáticamente. Es una toodesign para desarrolladores de aplicaciones individuales toohello una ventaja de tootake de aplicación de esta capacidad. Para obtener más información acerca de cómo toodevelop una aplicación Universal de Windows que usa la movilidad, consulte Hola [appdata almacenamiento API](https://msdn.microsoft.com/library/windows/apps/mt299098.aspx) hello y [appdata de Windows 8 blog para desarrolladores de movilidad](http://blogs.msdn.com/b/windowsappdev/archive/2012/07/17/roaming-your-app-data.aspx).

## <a name="what-account-is-used-for-settings-sync"></a>¿Qué cuenta se usa para la sincronización de configuración?
En Windows 8 y Windows 8.1, la sincronización de configuración siempre utiliza cuentas de Microsoft de consumidor. Los usuarios empresariales tenían Hola capacidad tooconnect un tootheir de cuenta de Microsoft sincronización de Active Directory dominio cuenta toogain acceso toosettings. En Windows 10, esta funcionalidad de cuenta de Microsoft conectada se ha sustituido por una plataforma de cuenta principal o secundaria.

cuenta de Hello principal se define como la cuenta de hello usa toosign en tooWindows. Puede ser una cuenta de Microsoft, una cuenta de Azure Active Directory (Azure AD), una cuenta de Active Directory local o una cuenta local. En la cuenta principal de toohello de suma, los usuarios de Windows 10 pueden agregar uno o varios dispositivos de tootheir de cuentas de nube secundaria. Esta cuenta secundaria suele ser una cuenta de Microsoft, una cuenta de Azure AD o alguna otra cuenta como Gmail o Facebook. Estas cuentas secundarias proporcionan acceso a servicios de tooadditional como inicio de sesión único y Hola tienda Windows, pero no son capaces de activar y sincronización de configuración.

En Windows 10, solo Hola cuenta principal para el dispositivo de hello puede usarse para la sincronización de configuración (vea [¿cómo puedo actualizar desde sincronización de configuración de cuenta de Microsoft en la sincronización de configuración de tooAzure AD de Windows 8 en Windows 10?](active-directory-windows-enterprise-state-roaming-faqs.md#how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-to-azure-ad-settings-sync-in-windows-10)).

Datos nunca se mezclan entre cuentas de usuario diferentes de hello en dispositivo Hola. La sincronización de la configuración tiene dos reglas:

* Configuración de Windows siempre lo acompañará cuenta principal de Hola.
* Datos de la aplicación se etiqueta con hello cuenta usada tooacquire Hola aplicación. Sola aplicaciones etiquetadas con la cuenta principal de Hola se sincronizarán. Etiquetado de la propiedad en la aplicación se determina cuando una aplicación se carga lateral a través de la tienda de Windows hello o administración de dispositivos móviles (MDM).

Si no se puede identificar el propietario de una aplicación, se moverá con la cuenta principal de Hola. Si un dispositivo se actualiza desde Windows 8 o Windows 8.1 tooWindows 10, todas las aplicaciones de Hola se etiquetarán como adquiridos por cuenta de Microsoft de Hola. Esto es porque la mayoría de los usuarios adquirir aplicaciones a través de la tienda Windows hello y no había ninguna compatibilidad del almacén de Windows con Azure AD cuentas anteriores tooWindows 10. Si una aplicación se instala a través de una licencia sin conexión, se etiquetarán aplicación hello con la cuenta principal de hello en dispositivo de Hola.

> [!NOTE]
> Dispositivos Windows 10 que son propiedad de la empresa y están conectado tooAzure AD ya no pueden conectarse a su cuenta de dominio de tooa de cuentas de Microsoft. Hola capacidad tooconnect una cuenta de dominio de tooa de cuenta de Microsoft y tienen sincronización de datos de todos los usuarios de Hola se quitará toohello Microsoft cuenta (es decir, Hola Microsoft itinerancia a través de la cuenta de Microsoft hello conectado y la funcionalidad de Active Directory) Dispositivos de Windows 10 que están combinada tooa conectados Active Directory o el entorno de Azure AD.
>
>

## <a name="how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-tooazure-ad-settings-sync-in-windows-10"></a>¿Cómo puedo actualizar desde sincronización de configuración de cuenta de Microsoft en la sincronización de configuración de tooAzure AD de Windows 8 en Windows 10?
Si está toohello Unidos a un dominio de Active Directory con Windows 8 o Windows 8.1 con una cuenta de Microsoft conectada, se sincronizará configuración a través de la cuenta de Microsoft. Después de actualizar tooWindows 10, se le seguirá toosync configuración de usuario a través de la cuenta de Microsoft siempre y cuando los usuarios unidos al dominio y el dominio de Active Directory de hello no se conecta con Azure AD.

Si Hola local de dominio de Active Directory conectarse con Azure AD, el dispositivo intentará configuración toosync mediante la cuenta de Azure AD Hola conectado. Si Administrador de hello Azure AD no habilita Enterprise itinerancia de estado, su conectado cuenta de Azure AD detendrá la sincronización de configuración. Si es un usuario de Windows 10 y ha iniciado sesión con una identidad de Azure AD, iniciará la sincronización de la configuración de Windows en cuanto el administrador habilite la sincronización de configuración a través de Azure AD.

Si almacena sus datos personales en el dispositivo de la empresa, debe tener en cuenta que sistema operativo Windows y datos de la aplicación se iniciará sincronizando tooAzure AD. Esto tiene Hola siguientes implicaciones:

* Configuración de su cuenta Microsoft personal se desfase aparte de configuración de hello en el trabajo o escuela cuentas de Azure AD. Esto es porque la cuenta de Microsoft de Hola y configuración de Azure AD se sincronizan ahora usa cuentas independientes.
* Ahora, la sincronización de los datos personales, como contraseñas Wi-Fi, credenciales web y favoritos de Internet Explorer (que anteriormente se realizaba a través de una cuenta Microsoft conectada), se llevará a cabo mediante Azure AD.

## <a name="how-do-microsoft-account-and-azure-ad-enterprise-state-roaming-interoperability-work"></a>¿Cómo funciona la interoperabilidad de la cuenta de Microsoft y Enterprise State Roaming de Azure AD?
En noviembre de 2015 de Hola o versiones posteriores de Windows 10, itinerancia de estado de Enterprise solo se admite para una sola cuenta a la vez. Si inicias sesión en tooWindows mediante un trabajo o escuela cuenta de Azure AD, se sincronizarán todos los datos a través de Azure AD. Si inicias sesión en tooWindows mediante una cuenta personal de Microsoft, se sincronizarán todos los datos a través de hello cuenta Microsoft. Appdata universal se trasladará con solo Hola cuenta principal de inicio de sesión en el dispositivo de Hola y se moverá solo si la licencia de la aplicación hello pertenece a la cuenta principal de Hola. No se sincronizará appdata universal para las aplicaciones de hello pertenecen a las cuentas secundarias.

## <a name="do-settings-sync-for-azure-ad-accounts-from-multiple-tenants"></a>¿Se sincroniza la configuración para las cuentas de Azure AD desde varios inquilinos?
Cuando AD de Azure varias cuentas de diferentes inquilinos de Azure AD están en hello mismo dispositivo, debe actualizar toocommunicate de registro del dispositivo de hello con Azure Rights Management (Azure RMS) para cada inquilino de Azure AD.  

1. Encontrar Hola GUID para cada inquilino de Azure AD. Abra Hola portal de Azure clásico y seleccione a un inquilino de Azure AD. Hola GUID para el inquilino de hello es en dirección URL de hello en la barra de direcciones de hello del explorador. Por ejemplo: `https://manage.windowsazure.com/YourAccount.onmicrosoft.com#Workspaces/ActiveDirectoryExtension/Directory/Tenant GUID/directoryQuickStart`
2. Una vez haya Hola GUID, necesitará clave de registro de hello tooadd **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\SettingSync\WinMSIPC\<GUID de Id. de inquilino >**.
   De hello **GUID de Id. de inquilino** clave, cree un nuevo valor de cadena múltiple (REG-MULTI-SZ) denominado **AllowedRMSServerUrls**. Para sus datos, especifique Hola licencias direcciones URL del punto de distribución de hello otros inquilinos de Azure que Hola accesos de dispositivo.
3. Puede encontrar Hola licencias direcciones URL del punto de distribución mediante la ejecución de hello **Get-AadrmConfiguration** cmdlet. Si los valores de hello para hello **LicensingIntranetDistributionPointUrl** y **LicensingExtranetDistributionPointUrl** son diferentes, especifique ambos valores. Si hello valores son Hola igual, especifique el valor de hello solo una vez.

## <a name="what-are-hello-roaming-settings-options-for-existing-windows-desktop-applications"></a>¿Qué opciones de configuración de movilidad de Hola para aplicaciones de escritorio de Windows existentes?
La itinerancia solo funciona en las aplicaciones universales de Windows. Hay dos opciones disponibles para habilitar la itinerancia en aplicaciones de escritorio de Windows existentes:

* Hola [Desktop puente](http://aka.ms/desktopbridge) le ayuda a poner el toohello de aplicaciones de escritorio de Windows existente plataforma Universal de Windows. Desde aquí, serán cambios mínimos en el código necesario tootake ventaja de movilidad de datos de aplicación de Azure AD. Hola escritorio puente proporciona las aplicaciones con una identidad de aplicación, que es necesario tooenable datos de aplicaciones móviles para aplicaciones de escritorio existentes.
* [User Experience Virtualization (UE-V)](https://technet.microsoft.com/library/dn458947.aspx) le permite crear una plantilla de configuración personalizada para aplicaciones de escritorio de Windows existentes y habilitar la itinerancia para las aplicaciones de Win32. Esta opción no requiere código de toochange de desarrollo de aplicaciones de Hola de aplicación hello. UE-V es limitado local tooon Active Directory móviles para los clientes que han comprado Hola Microsoft Desktop Optimization Pack.

Los administradores pueden configurar datos de una aplicación de escritorio de Windows de UE-V tooroam cambiando la itinerancia de configuración de sistema operativo Windows y los datos de aplicación Universal a través de [las directivas de grupo de UE-V](https://technet.microsoft.com/itpro/mdop/uev-v2/configuring-ue-v-2x-with-group-policy-objects-both-uevv2), incluido:

* La directiva de grupo "Roam Windows settings" (Usar un perfil itinerante en la configuración de Windows)
* La directiva de grupo "Do not synchronize Windows Apps" (No sincronizar aplicaciones de Windows)
* Movilidad en la sección de hello las aplicaciones de Internet Explorer

Hola futuras, Microsoft puede investigar toomake formas QUE UE-V totalmente integrado en Windows y ampliar la configuración de tooroam de UE-V a través de la nube de Azure AD de Hola.

## <a name="can-i-store-synced-settings-and-data-on-premises"></a>¿Se pueden almacenar configuraciones sincronizados y datos locales?
Itinerancia de estado de Enterprise almacena todos los datos sincronizados en hello nube de Azure. UE-V ofrece una solución de itinerancia local.

## <a name="who-owns-hello-data-thats-being-roamed"></a>¿Quién posee datos Hola que se está movidos?
las empresas de Hello propias Hola datos accesibles a través de itinerancia de estado de empresa. Los datos se almacenan en un centro de datos de Azure. Todos los datos de usuario se cifran en tránsito y en reposo en la nube de hello con Azure RMS. Se trata de una sincronización de configuración basada en cuentas de tooMicrosoft mejora en comparación, que cifra solo determinados datos confidenciales, como las credenciales de usuario antes de que abandona el dispositivo de Hola.

Microsoft está comprometido toosafeguarding los datos del cliente. Los datos de configuración de los usuarios empresariales se cifran automáticamente mediante Azure RMS cada vez que salen de un dispositivo Windows 10, de tal forma que ningún usuario pueda leer estos datos. Si su organización tiene una suscripción de pago de Azure RMS, puede utilizar otras características de Azure RMS, como realizar un seguimiento y revocar documentos, automáticamente proteger correos electrónicos que contienen información confidencial y administrar sus propias claves (Hola "traiga su propia clave" solución, también se conoce como BYOK). Para más información sobre estas características y cómo funciona Azure RMS, consulte [¿Qué es Azure Rights Management?](https://technet.microsoft.com/jj585026.aspx)

## <a name="can-i-manage-sync-for-a-specific-app-or-setting"></a>¿Puedo administrar la sincronización para una aplicación o configuración específica?
En Windows 10, no hay ningún toodisable de configuración de MDM o directiva de grupo móviles para una aplicación individual. Los administradores de inquilinos pueden deshabilitar la sincronización de los datos de la aplicación en todas las aplicaciones en un dispositivo administrado, pero no hay ningún control más preciso de nivel de aplicación o dentro de la aplicación.

## <a name="how-can-i-enable-or-disable-roaming"></a>¿Cómo se puede habilitar o deshabilitar la itinerancia?
Hola **configuración** aplicación, vaya demasiado**cuentas** > **sincronizar la configuración**. Desde esta página, puede ver qué cuenta se va a usa tooroam configuración, y puede habilitar o deshabilitar los grupos individuales de toobe configuración movido.

## <a name="what-is-microsofts-recommendation-for-enabling-roaming-in-windows-10"></a>¿Cuál es la recomendación de Microsoft para habilitar la itinerancia en Windows 10?
Microsoft tiene diferentes soluciones de itinerancia de configuración, incluidos los perfiles de usuario móviles, UE-V y Enterprise State Roaming.  Microsoft está comprometido toomaking una inversión en estado de empresa móvil en futuras versiones de Windows. Si su organización no está listo para imprimir o se encuentra cómodo con móvil datos toohello en la nube, se recomienda que use UE-V como la tecnología móvil principal. Si su organización requiere móviles proporciona compatibilidad para aplicaciones de escritorio de Windows existentes, pero es toomove diligente toohello en la nube, se recomienda que use Enterprise estado móvil y UE-V. Aunque UE-V y Enterprise State Roaming son tecnologías muy similares, no son mutuamente excluyentes. Se complementan entre sí toohelp Asegúrese de que su organización proporciona Hola móviles servicios que necesitan los usuarios.  

Cuando se usa la itinerancia de estado de Enterprise y UE-V, se aplica Hola siguiendo reglas:

* Itinerancia de estado de empresa es agente móvil principal de hello en dispositivo Hola. UE-V está siendo usado toosupplement Hola "Brecha en Win32".
* Movilidad de la configuración de Windows y los datos de aplicación UWP modernos de UE-V debe estar deshabilitado cuando con grupo de hello UE-V directivas. Estas están ya cubiertas por Enterprise State Roaming.

## <a name="how-does-enterprise-state-roaming-support-virtual-desktop-infrastructure-vdi"></a>¿Cómo admite Enterprise State Roaming la infraestructura de escritorio virtual (VDI)?
Enterprise State Roaming es compatible con las SKU de cliente de Windows 10, pero no con las de servidor. Si un cliente de la máquina virtual se hospeda en una máquina de hipervisor y remotamente iniciar sesión en la máquina virtual de toohello, moverá los datos. Si varios usuarios comparten el mismo sistema operativo y los usuarios remotamente iniciar sesión en el servidor de tooa para una experiencia de escritorio completa de hello, movilidad podría no funcionar. no se admite oficialmente el escenario de Hello último basados en sesión.

## <a name="what-happens-when-my-organization-purchases-azure-rms-after-using-roaming"></a>¿Qué ocurre cuando mi organización adquiere Azure RMS después de usar la itinerancia?
Si su organización ya está usando móviles en Windows 10 con hello suscripción gratuita de uso limitado de Azure RMS, comprar una suscripción de pago Azure RMS no tendrá ningún impacto en la funcionalidad de Hola de característica móvil hello, y será ningún cambio de configuración requiere el Administrador de TI.

## <a name="known-issues"></a>Problemas conocidos
Consulte la documentación de Hola Hola [solución de problemas](active-directory-windows-enterprise-state-roaming-troubleshooting.md) sección para obtener una lista de problemas conocidos. 

## <a name="related-topics"></a>Temas relacionados
* [Información general de Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Habilitación de Enterprise State Roaming en Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [Configuración de MDM y directivas de grupo](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Referencia de la configuración de movilidad de Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Solución de problemas](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
