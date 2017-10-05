---
title: "Preguntas más frecuentes sobre itinerancia de datos y configuración | Microsoft Docs"
description: "Responde a algunas preguntas que los administradores de TI podrían tener sobre la sincronización de datos de aplicación y la configuración."
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
ms.openlocfilehash: 9968d9fa1ebbc92b5647a23c75e75fb819f5d5ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="settings-and-data-roaming-faq"></a>Preguntas más frecuentes sobre itinerancia de datos y configuración
Este tema responde a algunas preguntas que los administradores de TI podrían tener sobre la sincronización de datos de aplicación y la configuración.

## <a name="what-data-roams"></a>¿Qué datos se movilizan?
**Configuración de Windows**: la configuración de PC que está integrada en el sistema operativo Windows. Por lo general, estas son opciones que personalizan el equipo del usuario, e incluyen las categorías generales siguientes:

* *Tema*, que incluye características como la configuración de tema y la barra de tareas del escritorio.
* *Configuración de Internet Explorer*, como pestañas abiertas recientemente y favoritos.
* *Configuración del explorador Edge*, como favoritos y lista de lectura.
* *Contraseñas*, entre las que se incluyen las contraseñas de Internet, perfiles de Wi-Fi, y otras.
* *Preferencias de idioma*, que incluye la configuración de la distribución del teclado, el idioma del sistema, la fecha y hora, y mucho más.
* *Características de facilidad de acceso*, como el tema de contraste alto, narrador o lupa
* *Otra configuración de Windows*, como la configuración de símbolo del sistema y la lista de aplicaciones.

**Datos de la aplicación**: las aplicaciones universales de Windows pueden escribir los datos de configuración en una carpeta de itinerancia y todos los datos escritos en esta carpeta se sincronizarán automáticamente. Depende del desarrollador de las aplicaciones individuales el diseñar una aplicación para sacar partido a esta funcionalidad. Para más información acerca de cómo desarrollar una aplicación universal de Windows que use la itinerancia, consulte [Almacenar y recuperar la configuración y otros datos de aplicación](https://msdn.microsoft.com/library/windows/apps/mt299098.aspx) y el [blog para desarrolladores de itinerancia de datos de aplicación de Windows 8](http://blogs.msdn.com/b/windowsappdev/archive/2012/07/17/roaming-your-app-data.aspx).

## <a name="what-account-is-used-for-settings-sync"></a>¿Qué cuenta se usa para la sincronización de configuración?
En Windows 8 y Windows 8.1, la sincronización de configuración siempre utiliza cuentas de Microsoft de consumidor. Los usuarios empresariales tenían la capacidad de conectar una cuenta de Microsoft a su cuenta de dominio de Active Directory para obtener acceso a la sincronización de configuración. En Windows 10, esta funcionalidad de cuenta de Microsoft conectada se ha sustituido por una plataforma de cuenta principal o secundaria.

La cuenta principal se define como la cuenta utilizada para iniciar sesión en Windows. Puede ser una cuenta de Microsoft, una cuenta de Azure Active Directory (Azure AD), una cuenta de Active Directory local o una cuenta local. Además de la cuenta principal, los usuarios de Windows 10 pueden agregar una o más cuentas de nube secundarias a su dispositivo. Esta cuenta secundaria suele ser una cuenta de Microsoft, una cuenta de Azure AD o alguna otra cuenta como Gmail o Facebook. Estas cuentas secundarias proporcionan acceso a servicios adicionales, como el inicio de sesión único o a la Tienda Windows, pero no pueden activar la sincronización de configuración.

En Windows 10, solo puede usarse la cuenta principal del dispositivo para la sincronización de configuración (consulte [¿Cómo actualizo desde la sincronización de configuración de cuenta de Microsoft en Windows 8 a la sincronización de configuración de Azure AD en Windows 10?](active-directory-windows-enterprise-state-roaming-faqs.md#how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-to-azure-ad-settings-sync-in-windows-10)).

Los datos nunca se mezclan entre las distintas cuentas de usuario en el dispositivo. La sincronización de la configuración tiene dos reglas:

* La configuración de Windows siempre usará un perfil itinerante con la cuenta principal.
* Los datos de la aplicación se etiquetarán con la cuenta utilizada para adquirir la aplicación. Solo se sincronizarán las aplicaciones etiquetadas con la cuenta principal. El etiquetado de la propiedad de la aplicación se determina cuando se carga una aplicación a través de la Tienda Windows o de la administración de dispositivos móviles (MDM).

Si no se puede identificar al propietario de una aplicación, se movilizará con la cuenta principal. Si un dispositivo se actualiza desde Windows 8 o Windows 8.1 a Windows 10, todas las aplicaciones se etiquetarán como adquiridas por la cuenta de Microsoft. Esto es debido a que la mayoría de los usuarios adquieren aplicaciones a través de la Tienda Windows y no había compatibilidad de la Tienda Windows con las cuentas de Azure AD antes de Windows 10. Si se instala una aplicación a través de una licencia sin conexión, la aplicación se etiquetará mediante la cuenta principal en el dispositivo.

> [!NOTE]
> Los dispositivos Windows 10 corporativos y que estén asociados a Azure AD ya no pueden conectar sus cuentas Microsoft a una cuenta de dominio. La capacidad de conectar una cuenta de Microsoft con una cuenta de dominio y de tener toda la sincronización de datos del usuario en la cuenta de Microsoft (es decir, itinerancia de la cuenta de Microsoft a través de la funcionalidad "cuenta de Microsoft y Active Directory conectados") se quita de los dispositivos Windows 10 que se unen a un entorno Active Directory o Azure AD conectado.
>
>

## <a name="how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-to-azure-ad-settings-sync-in-windows-10"></a>¿Cómo actualizo desde la sincronización de configuración de cuenta de Microsoft en Windows 8 a la sincronización de configuración de Azure AD en Windows 10?
Si es un usuario unido al dominio de Active Directory que ejecuta Windows 8 o Windows 8.1 con una cuenta de Microsoft conectada, sincronizará la configuración a través de la cuenta de usuario de Microsoft. Después de actualizar a Windows 10, continuará la sincronización de la configuración de usuario a través de la cuenta de Microsoft, siempre que sea un usuario unido a dominio y el dominio de Active Directory no se conecte con Azure AD.

Si el dominio de Active Directory local se conecta con Azure AD, su dispositivo comenzará a intentar sincronizar la configuración mediante la cuenta de Azure AD conectada. Si el administrador de Azure AD no permite Enterprise State Roaming, su cuenta de Azure AD conectada detendrá la sincronización de la configuración. Si es un usuario de Windows 10 y ha iniciado sesión con una identidad de Azure AD, iniciará la sincronización de la configuración de Windows en cuanto el administrador habilite la sincronización de configuración a través de Azure AD.

Si almacena sus datos personales en los dispositivos corporativos, debe ser consciente de que el sistema operativo Windows y los datos de la aplicación comenzarán a sincronizarse en Azure AD. Esto tiene las implicaciones siguientes:

* La configuración de su cuenta personal de Microsoft se separará de la configuración de sus cuentas profesionales o educativas de Azure AD. Esto es debido a que la sincronización de la cuenta de Microsoft y de la configuración de Azure AD ahora usan cuentas distintas.
* Ahora, la sincronización de los datos personales, como contraseñas Wi-Fi, credenciales web y favoritos de Internet Explorer (que anteriormente se realizaba a través de una cuenta Microsoft conectada), se llevará a cabo mediante Azure AD.

## <a name="how-do-microsoft-account-and-azure-ad-enterprise-state-roaming-interoperability-work"></a>¿Cómo funciona la interoperabilidad de la cuenta de Microsoft y Enterprise State Roaming de Azure AD?
En la versión de noviembre de 2015 o posterior de Windows 10, Enterprise State Roaming solo puede utilizarse para una sola cuenta a la vez. Si inicia sesión en Windows con una cuenta profesional o educativa de Azure AD, todos los datos se sincronizarán a través de Azure AD. Si inicia sesión en Windows mediante una cuenta personal de Microsoft, todos los datos se sincronizarán a través de la cuenta de Microsoft. Los datos de aplicación universal usarán un perfil itinerante solo con la cuenta de inicio de sesión principal del dispositivo y solo usarán un perfil itinerante si la licencia de la aplicación es propiedad de la cuenta principal. No se sincronizarán los datos de aplicación universal de las aplicaciones que son propiedad de cuentas secundarias.

## <a name="do-settings-sync-for-azure-ad-accounts-from-multiple-tenants"></a>¿Se sincroniza la configuración para las cuentas de Azure AD desde varios inquilinos?
Cuando varias cuentas de AD Azure de distintos inquilinos de Azure AD se encuentran en el mismo dispositivo, debe actualizar el registro del dispositivo para comunicarse con el servicio Azure Rights Management (RMS) para cada inquilino de Azure AD.  

1. Busque el GUID para cada inquilino de Azure AD. Abra el Portal de Azure clásico y seleccione un inquilino de Azure AD. El GUID del inquilino es la dirección URL que aparece en la barra de direcciones del explorador. Por ejemplo: `https://manage.windowsazure.com/YourAccount.onmicrosoft.com#Workspaces/ActiveDirectoryExtension/Directory/Tenant GUID/directoryQuickStart`
2. Una vez que se tenga el GUID, será preciso agregar la clave del Registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\SettingSync\WinMSIPC\<GUID del identificador de inquilino>**.
   En la clave del **GUID del identificador de inquilino**, cree un nuevo valor de cadena múltiple (REG-MULTI-SZ) denominado **AllowedRMSServerUrls**. Para sus datos, especifique las direcciones URL del punto de distribución licencias de los otros inquilinos de Azure a los que accede el dispositivo.
3. Puede encontrar las direcciones URL de los puntos de distribución de licencias ejecutando el cmdlet **Get-AadrmConfiguration** . Si los valores de **LicensingIntranetDistributionPointUrl** y **LicenseingExtranetDistributionPointUrl** son diferentes, especifique ambos. Si los valores son iguales, especifique solo un valor.

## <a name="what-are-the-roaming-settings-options-for-existing-windows-desktop-applications"></a>¿Cuáles son las opciones de configuración de itinerancia de las aplicaciones de escritorio de Windows existentes?
La itinerancia solo funciona en las aplicaciones universales de Windows. Hay dos opciones disponibles para habilitar la itinerancia en aplicaciones de escritorio de Windows existentes:

* [Desktop Bridge](http://aka.ms/desktopbridge) le ayuda transferir fácilmente sus aplicaciones de escritorio de Windows a la plataforma universal de Windows. A partir de aquí, habrá que realizar cambios mínimos en el código para aprovechar las ventajas de la itinerancia de datos de la aplicación de Azure AD. Desktop Bridge proporciona a las aplicaciones una identidad de aplicación, que se requiere para habilitar la itinerancia de datos de las aplicaciones de escritorio existentes.
* [User Experience Virtualization (UE-V)](https://technet.microsoft.com/library/dn458947.aspx) le permite crear una plantilla de configuración personalizada para aplicaciones de escritorio de Windows existentes y habilitar la itinerancia para las aplicaciones de Win32. Esta opción no precisa que el desarrollador cambie el código de la aplicación. Solo los clientes que han comprado el paquete de optimización de escritorio de Microsoft pueden utilizar UE-V para habilitar la itinerancia de Active Directory local.

Los administradores pueden configurar UE-V para usar un perfil itinerante en los datos de aplicación de escritorio de Windows cambiando la itinerancia de la configuración de sistema operativo Windows y de los datos de aplicación universal mediante las [directivas de grupo de UE-V](https://technet.microsoft.com/itpro/mdop/uev-v2/configuring-ue-v-2x-with-group-policy-objects-both-uevv2), entre ellas:

* La directiva de grupo "Roam Windows settings" (Usar un perfil itinerante en la configuración de Windows)
* La directiva de grupo "Do not synchronize Windows Apps" (No sincronizar aplicaciones de Windows)
* Itinerancia de Internet Explorer en la sección de aplicaciones

En el futuro, Microsoft podría investigar formas de integrar UE-V profundamente en Windows y ampliar UE-V para movilizar la configuración a través de la nube de Azure AD.

## <a name="can-i-store-synced-settings-and-data-on-premises"></a>¿Se pueden almacenar configuraciones sincronizados y datos locales?
Enterprise State Roaming almacena todos los datos sincronizados en la nube de Azure. UE-V ofrece una solución de itinerancia local.

## <a name="who-owns-the-data-thats-being-roamed"></a>¿Quién administra los datos que usan un perfil itinerante?
Las empresas tienen la propiedad de los datos que usan un perfil itinerante mediante Enterprise State Roaming. Los datos se almacenan en un centro de datos de Azure. Todos los datos de usuario se cifran en tránsito y en reposo en la nube mediante Azure RMS. Esto es una mejora comparado con la sincronización de la configuración basada en la cuenta de Microsoft, donde solo ser cifran determinados datos confidenciales, como las credenciales de usuario, antes de dejar el dispositivo.

Microsoft se compromete a proteger los datos de los clientes. Los datos de configuración de los usuarios empresariales se cifran automáticamente mediante Azure RMS cada vez que salen de un dispositivo Windows 10, de tal forma que ningún usuario pueda leer estos datos. Si la organización tiene una suscripción de pago para Azure RMS, puede utilizar otras características de Azure RMS, como el seguimiento y revocación de documentos, proteger automáticamente correos electrónicos que contienen información confidencial y administrar sus propias claves (la solución "bring your own key" solución, también conocida como BYOK). Para más información sobre estas características y cómo funciona Azure RMS, consulte [¿Qué es Azure Rights Management?](https://technet.microsoft.com/jj585026.aspx)

## <a name="can-i-manage-sync-for-a-specific-app-or-setting"></a>¿Puedo administrar la sincronización para una aplicación o configuración específica?
En Windows 10, no hay ninguna configuración de MDM o de directiva de grupo para deshabilitar la itinerancia en una aplicación individual. Los administradores de inquilinos pueden deshabilitar la sincronización de los datos de la aplicación en todas las aplicaciones en un dispositivo administrado, pero no hay ningún control más preciso de nivel de aplicación o dentro de la aplicación.

## <a name="how-can-i-enable-or-disable-roaming"></a>¿Cómo se puede habilitar o deshabilitar la itinerancia?
En la aplicación **Configuración**, vaya a **Cuentas** > **Sincronizar la configuración**. En esta página, puede ver qué cuenta se usa para movilizar la configuración y puede habilitar o deshabilitar los grupos de configuración individuales que se van a movilizar.

## <a name="what-is-microsofts-recommendation-for-enabling-roaming-in-windows-10"></a>¿Cuál es la recomendación de Microsoft para habilitar la itinerancia en Windows 10?
Microsoft tiene diferentes soluciones de itinerancia de configuración, incluidos los perfiles de usuario móviles, UE-V y Enterprise State Roaming.  En futuras versiones de Windows, Microsoft se ha comprometido a invertir en Enterprise State Roaming. Si su organización no está preparada o no está cómoda con el desplazamiento de datos a la nube, recomendamos utilizar UE-V como tecnología de itinerancia principal. Si su organización necesita habilitar la itinerancia en sus aplicaciones de escritorio de Windows y está dispuesta a migrar los datos a la nube, recomendamos utilizar Enterprise State Roaming y UE-V. Aunque UE-V y Enterprise State Roaming son tecnologías muy similares, no son mutuamente excluyentes. Se complementan entre sí para garantizar que su organización proporciona los servicios de itinerancia que necesitan los usuarios.  

Al utilizar Enterprise State Roaming y UE-V, se aplican las siguientes reglas:

* Enterprise State Roaming es el agente de movilidad principal en el dispositivo. UE-V se utiliza para complementar el "intervalo de Win32".
* La itinerancia de UE-V para la configuración de Windows y los datos de la aplicación UWP moderna deben estar deshabilitados cuando se usan las directivas de grupo de UE-V. Estas están ya cubiertas por Enterprise State Roaming.

## <a name="how-does-enterprise-state-roaming-support-virtual-desktop-infrastructure-vdi"></a>¿Cómo admite Enterprise State Roaming la infraestructura de escritorio virtual (VDI)?
Enterprise State Roaming es compatible con las SKU de cliente de Windows 10, pero no con las de servidor. Si una máquina virtual cliente está hospedada en una máquina de hipervisor e inicia sesión de manera remota a la máquina virtual, los datos del usuario usarán un perfil itinerante. Si varios usuarios comparten el mismo sistema operativo e inicia sesión en un servidor de manera remota para disfrutar de una experiencia de escritorio completa, es posible que la itinerancia no funcione. No se admite oficialmente el escenario basado en la última sesión.

## <a name="what-happens-when-my-organization-purchases-azure-rms-after-using-roaming"></a>¿Qué ocurre cuando mi organización adquiere Azure RMS después de usar la itinerancia?
Si su organización ya está usando la itinerancia en Windows 10 con la suscripción gratuita de uso limitado de Azure RMS y compra una suscripción de Azure RMS de pago, no afectará a la funcionalidad de la característica de itinerancia y el administrador de TI no tendrá que realizar cambios en la configuración.

## <a name="known-issues"></a>Problemas conocidos
Consulte la documentación en la sección de [solución de problemas](active-directory-windows-enterprise-state-roaming-troubleshooting.md) para obtener una lista de problemas conocidos. 

## <a name="related-topics"></a>Temas relacionados
* [Información general de Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Habilitación de Enterprise State Roaming en Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [Configuración de MDM y directivas de grupo](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Referencia de la configuración de movilidad de Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Solución de problemas](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
