---
title: "Azure AD Connect: instalación personalizada | Microsoft Docs"
description: "Este documento describe las opciones de instalación personalizada de Hola para Azure AD Connect. Use estos tooinstall instrucciones Active Directory a través de Azure AD Connect."
services: active-directory
keywords: "qué es Azure AD Connect, instalar Active Directory, componentes necesarios para Azure AD"
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 6d42fb79-d9cf-48da-8445-f482c4c536af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: c49724fab78c5a1688662043f69506fff6f82104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="custom-installation-of-azure-ad-connect"></a>Instalación personalizada de Azure AD Connect
Azure AD Connect **configuración personalizada** se utiliza cuando desea más opciones para la instalación de Hola. Se utiliza si tiene varios bosques o si desea tooconfigure características opcionales que no se tratan en la instalación rápida de Hola. Se utiliza en todos los casos donde hello [ **instalación rápida** ](active-directory-aadconnect-get-started-express.md) opción no cumple su implementación o topología.

Antes de empezar a instalar Azure AD Connect, asegúrese de que demasiado[descargar Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) y los pasos de requisitos previos de hello completa de [Azure AD Connect: Hardware y los requisitos previos](active-directory-aadconnect-prerequisites.md). Asegúrese también de que posee las cuentas necesarias que se describen en [Azure AD Connect: cuentas y permisos](active-directory-aadconnect-accounts-permissions.md).

Si la configuración personalizada no coincide con la topología, por ejemplo tooupgrade DirSync, consulte [documentación relacionada con](#related-documentation) para otros escenarios.

## <a name="custom-settings-installation-of-azure-ad-connect"></a>Instalación de Azure AD Connect con Configuración personalizada
### <a name="express-settings"></a>Configuración rápida
En esta página, haga clic en **personalizar** toostart una instalación de configuración personalizada.

### <a name="install-required-components"></a>Instalación de los componentes necesarios
Al instalar servicios de sincronización de hello, puede dejar desactivada sección de configuración opcional de Hola y Azure AD Connect establece todo automáticamente. Configura una instancia de SQL Server 2012 Express LocalDB, crear grupos adecuados de Hola y asignar permisos. Si desea que los valores predeterminados de toochange hello, puede usar Hola siguientes opciones de configuración opcional de Hola de toounderstand de tabla que están disponibles.

![Componentes necesarios](./media/active-directory-aadconnect-get-started-custom/requiredcomponents.png)

| Configuración opcional | Description |
| --- | --- |
| Usar un SQL Server existente |Le permite toospecify Hola nombre y SQL Server nombre de la instancia de Hola. Elija esta opción si ya tiene un servidor de base de datos que desearía toouse. Escriba nombre de instancia de hello seguido por un número de coma y el puerto en **nombre de instancia** si SQL Server no tiene la exploración habilitada. |
| Usar una cuenta de servicio existente |De forma predeterminada Azure AD Connect usa una cuenta de servicio virtual para toouse de servicios de sincronización de Hola. Si usa un servidor SQL remoto o usa un proxy que requiere autenticación, deberá toouse un **cuenta de servicio administrada** o use una cuenta de servicio de dominio de Hola y Hola conozcan. En esos casos, escriba Hola cuenta toouse. Asegúrese de que usuario Hola ejecutando la instalación de hello es una SA de SQL por lo que puede crearse un inicio de sesión para la cuenta de servicio de Hola. Consulte [Permisos y cuentas de Azure AD Connect](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) |
| Especificar grupos de sincronización personalizada |De forma predeterminada Azure AD Connect crea cuatro grupos toohello local server cuando se instalan los servicios de sincronización de Hola. Estos grupos son: grupo de administradores, grupo de operadores, grupo de examinar y Hola grupo de restablecimiento de contraseña. Puede especificar sus grupos aquí. grupos de Hello deben ser locales en servidor hello y no se encuentra en el dominio de Hola. |

### <a name="user-sign-in"></a>Inicio de sesión de usuario
Después de instalar componentes de hello necesario, se le pide tooselect a los usuarios un único método de inicio de sesión. Hello en la tabla siguiente proporciona una breve descripción de las opciones disponibles de Hola. Para obtener una descripción completa de métodos de inicio de sesión de hello, consulte [inicio de sesión de usuario](active-directory-aadconnect-user-signin.md).

![Inicio de sesión del usuario](./media/active-directory-aadconnect-get-started-custom/usersignin2.png)

| Inicio de sesión único | Description |
| --- | --- |
| Sincronización de contraseñas |Los usuarios son toosign capaz de servicios en la nube tooMicrosoft, como Office 365, utilizando Hola misma contraseña que usan en su red local. las contraseñas de los usuarios de Hello están sincronizado tooAzure AD como un hash de contraseña y autenticación se produce en la nube de Hola. Consulte [Sincronización de contraseñas](active-directory-aadconnectsync-implement-password-synchronization.md) para más información. |
|Autenticación de paso a través (versión preliminar)|Los usuarios son toosign capaz de servicios en la nube tooMicrosoft, como Office 365, utilizando Hola misma contraseña que usan en su red local.  contraseña de los usuarios de Hola se pasa a través de toohello local Active Directory controlador toobe validado.
| Federación con AD FS |Los usuarios son toosign capaz de servicios en la nube tooMicrosoft, como Office 365, utilizando Hola misma contraseña que usan en su red local.  los usuarios de Hola se redirigen tootheir toosign de la instancia de AD FS en local y la autenticación produce en local. |
| No configurar |No se instala ni configura ninguna característica. Elija esta opción si ya tiene un servidor de federación de terceros u otra solución existente ya instalada. |
|Habilitar el inicio de sesión único|Esta opción está disponible con la sincronización de contraseñas y la autenticación de paso a través y proporciona un inicio de sesión único en la experiencia para los usuarios de escritorio en la red corporativa de Hola.  Para más información, consulte [Inicio de sesión único](active-directory-aadconnect-sso.md). </br>Tenga en cuenta para los clientes de AD FS esta opción no está disponible porque AD FS ya ofertas Hola de mismo nivel de inicio de sesión único.</br>(si no se libera PTA en hello vez)
|Opción de inicio de sesión|Esta opción está disponible para los clientes de sincronización de contraseña y proporciona un inicio de sesión único en la experiencia para los usuarios de escritorio en la red corporativa de Hola.  </br>Para más información, consulte [Inicio de sesión único](active-directory-aadconnect-sso.md). </br>Tenga en cuenta para los clientes de AD FS esta opción no está disponible porque AD FS ya ofertas Hola de mismo nivel de inicio de sesión único.


### <a name="connect-tooazure-ad"></a>Conectar tooAzure AD
En pantalla de bienvenida conectar tooAzure AD, escriba una cuenta de administrador global y una contraseña. Si seleccionó **federación con AD FS** en la página anterior de hello, no inicie sesión con una cuenta en un dominio tiene previsto tooenable para la federación. Una recomendación es una cuenta en el valor predeterminado de hello toouse **onmicrosoft.com** dominio, que viene con su directorio Azure AD.

Esta cuenta es sólo toocreate usa una cuenta de servicio en Azure AD y no se utiliza cuando Hola asistente haya finalizado.  
![Inicio de sesión del usuario](./media/active-directory-aadconnect-get-started-custom/connectaad.png)

Si la cuenta de administrador global tiene MFA habilitado, necesita contraseña de hello tooprovide nuevo al cabo de hello inicio de sesión emergente y completa Hola desafío MFA. desafío de Hello pudo proporcionar un código de comprobación o una llamada de teléfono.  
![Inicio de sesión del usuario en MFA](./media/active-directory-aadconnect-get-started-custom/connectaadmfa.png)

También puede tener la cuenta de administrador global de Hello [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md) habilitado.

Si aparece un error y tiene problemas de conectividad, consulte [Solución de problemas de conectividad con Azure AD Connect](active-directory-aadconnect-troubleshoot-connectivity.md).

## <a name="pages-under-hello-section-sync"></a>Páginas bajo la sección de hello sincronización

### <a name="connect-your-directories"></a>Conectar sus directorios
tooconnect tooyour servicios de dominio de Active Directory, Azure AD Connect necesita el nombre del bosque de Hola y credenciales de una cuenta con permisos suficientes.

![Directorio de conexión](./media/active-directory-aadconnect-get-started-custom/connectdir01.png)

Después de escribir el nombre de bosque de Hola y haga clic en **Agregar directorio**, un cuadro de diálogo emergente aparece y le pide que con hello siguientes opciones:

| Opción | Descripción |
| --- | --- |
| Usar cuenta existente | Seleccione esta opción si desea cuenta tooprovide una existente de AD DS toobe usa Azure AD Connect para conectarse toohello AD bosque durante la sincronización de directorios. También puede especificar parte de dominio de hello en formato NetBios o FQDN, es decir, FABRIKAM\syncuser o fabrikam.com\syncuser. Esta cuenta puede ser una cuenta de usuario normal porque solo necesita permisos de lectura de hello predeterminados. Sin embargo, en función del escenario, puede que necesite permisos adicionales. Para más información, consulte [Azure AD Connect: cuentas y permisos](active-directory-aadconnect-accounts-permissions.md#create-the-ad-ds-account). |
| Crear nueva cuenta | Seleccione esta opción si desea que Azure AD Connect Asistente toocreate Hola AD DS se requiere una cuenta, Azure AD Connect para conectarse toohello AD bosque durante la sincronización de directorios. Cuando se selecciona esta opción, escriba Hola username y password para una cuenta de administrador de empresa. Hello cuenta de administrador de empresa proporcionada se usará, Azure AD Connect Hola de toocreate asistente necesario cuenta AD DS. También puede especificar parte de dominio de hello en formato NetBios o FQDN, es decir, FABRIKAM\administrator o fabrikam.com\administrator. |

![Directorio de conexión](./media/active-directory-aadconnect-get-started-custom/connectdir02.png)


### <a name="azure-ad-sign-in-configuration"></a>Configuración de inicio de sesión de Azure AD
Esta página le permite tooreview Hola UPN dominios en local de AD DS y que se han comprobado en Azure AD. Esta página también permite tooconfigure Hola atributo toouse para userPrincipalName Hola.

![Dominios sin comprobar](./media/active-directory-aadconnect-get-started-custom/aadsigninconfig.png)  
Revise los dominios marcados como **Not Added** (Sin agregar) y **Not Verified** (Sin comprobar). Asegúrese de que los dominios que usa se han comprobado en Azure AD. Haga clic en símbolo de actualización de hello cuando haya comprobado los dominios. Para obtener más información, vea [agregar y comprobar el dominio de Hola](../active-directory-add-domain.md)

**UserPrincipalName** -Hola atributo userPrincipalName es usuarios de atributo Hola usar cuando inician sesión en tooAzure AD y Office 365. dominios de Hello usa, también conocido como Hola sufijo UPN, deben comprobarse en Azure AD antes de que los usuarios de Hola se sincronizan. Microsoft recomienda tookeep Hola predeterminado atributo userPrincipalName. Si este atributo es no es enrutable y no se puede comprobar, entonces es posible tooselect otro atributo. Por ejemplo, puede seleccionar correo electrónico como atributo de hello mantienen Hola del identificador de inicio de sesión. El uso de cualquier atributo distinto de userPrincipalName se conoce como **id. alternativo**. valor del atributo Id. alternativo de Hello debe seguir Hola RFC822 estándar. Un id. alternativo puede usarse con la sincronización de contraseñas y con la federación.

>[!NOTE]
> Al habilitar la autenticación de paso a través debe tener al menos un dominio comprobado en orden toocontinue a través del Asistente de Hola.

> [!WARNING]
> El uso de un identificador alternativo no es compatible con todas las cargas de trabajo de Office 365. Para obtener más información, consulte demasiado[configurar Id. de inicio de sesión alternativo](https://technet.microsoft.com/library/dn659436.aspx).
>
>

### <a name="domain-and-ou-filtering"></a>Filtrado por dominio y unidad organizativa
De forma predeterminada, todos los dominios y las unidades organizativas se sincronizan. Si no hay algunos dominios o unidades organizativas que no desea toosynchronize tooAzure AD, puede anular la selección de estos dominios y unidades organizativas.  
![Filtrado de DomainOU](./media/active-directory-aadconnect-get-started-custom/domainoufiltering.png)  
Esta página del Asistente para hello consiste en configurar el filtrado basado en dominio y unidad organizativa. Si tiene previsto toomake cambios, consulte [filtrado basado en dominio](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) y [filtrado basado en la unidad organizativa](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) antes de realizar estos cambios. Algunas unidades organizativas son esenciales para la funcionalidad de hello y no deben ser no seleccionados.

Si usa el filtrado basado en unidad organizativa con la versión de Azure AD Connect anterior a 1.1.524.0, las unidades organizativas nuevas que se agreguen posteriormente se sincronizan de forma predeterminada. Si desea que el comportamiento de hello nuevos que no se deben sincronizar las unidades organizativas, a continuación, puede configurar una vez se ha completado el Asistente de hello con [filtrado basado en la unidad organizativa](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Para Azure AD Connect versión 1.1.524.0 o después, puede indicar si desea que la nueva toobe unidades organizativas sincronizado o no.

Si tiene previsto toouse [filtrado basado en el grupo](#sync-filtering-based-on-groups), a continuación, asegúrese de hello OU con grupo de hello es incluido y no se filtran con filtrado de unidad organizativa. El filtrado de la unidad organizativa se evalúa antes del filtrado basado en el grupo.

También es posible que algunos dominios no sean accesibles debido a restricciones de toofirewall. De forma predeterminada estos dominios no estarán seleccionados y tendrán una indicación de advertencia.  
![Dominios no accesibles](./media/active-directory-aadconnect-get-started-custom/unreachable.png)  
Si aparece esta advertencia, asegúrese de que estos dominios no están realmente disponibles y Hola advertencia es normal.

### <a name="uniquely-identifying-your-users"></a>Identificación de forma exclusiva de usuarios

#### <a name="select-how-users-should-be-identified-in-your-on-premises-directories"></a>Seleccione cómo deben identificarse los usuarios en los directorios locales
Hola coincidencia entre bosques característica permite toodefine cómo los usuarios de los bosques de AD DS se representan en Azure AD. Un usuario puede estar representado solo una vez en todos los bosques o tener una combinación de cuentas habilitadas y deshabilitadas. usuario de Hello también pueden representarse como un contacto en varios bosques.

![Único](./media/active-directory-aadconnect-get-started-custom/unique.png)

| Configuración | Description |
| --- | --- |
| [Los usuarios solo se representan una vez en todos los bosques](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Todos los usuarios se crean como objetos individuales en Azure AD. objetos de Hello no están unidos en el metaverso Hola. |
| [Atributo Mail](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Esta opción une a los usuarios y contactos si el atributo de correo electrónico de hello tiene Hola mismo valor en bosques diferentes. Esta opción se utiliza cuando los contactos se han creado mediante GALSync. Si elige esta opción, los objetos de usuario cuyo atributo de correo electrónico no se rellena no estarán sincronizado tooAzure AD. |
| [ObjectSID y msExchangeMasterAccountSID/ msRTCSIP-OriginatorSid](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Esta opción une un usuario habilitado en un bosque de cuentas con un usuario deshabilitado en un bosque de recursos. En Exchange, esta configuración se conoce como buzón vinculado. También se puede utilizar esta opción si solo usa Lync y Exchange no está presente en el bosque de recursos de Hola. |
| sAMAccountName y MailNickName |Esta opción une en atributos donde es Id. de inicio de sesión de hello esperado puede encontrarse usuario Hola. |
| Un atributo específico |Esta opción le permite tooselect su propio atributo. Si elige esta opción, los objetos de usuario cuyo atributo (seleccionado) no se rellena no estarán sincronizado tooAzure AD. **Limitación:** que toopick seguro de un atributo que ya se encuentra en el metaverso Hola. Si elige un atributo personalizado (no de metaverso hello), no se puede completar el Asistente de Hola. |

#### <a name="select-how-users-should-be-identified-with-azure-ad---source-anchor"></a>Seleccione cómo deben identificarse los usuarios con Azure AD: delimitador de origen
Hola atributo sourceAnchor es un atributo que es inmutable, durante la vigencia de Hola de un objeto de usuario. Es clave principal Hola vincular usuario local de hello con hello en Azure AD.

| Configuración | Descripción |
| --- | --- |
| Dejar que Azure administre delimitador de origen de Hola para mí | Seleccione esta opción si desea atributo de hello toopick de Azure AD para usted. Si selecciona esta opción, el Asistente de Azure AD Connect aplica lógica de selección de atributo hello sourceAnchor se describe en la sección del artículo [Azure AD Connect: diseñar conceptos: uso de msDS-ConsistencyGuid como sourceAnchor](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Asistente de Hello indica qué atributo se ha detectado como atributo de hello delimitador de origen una vez finalizada la instalación personalizada. |
| Un atributo específico | Seleccione esta opción si desea toospecify un atributo de AD existente como atributo de hello sourceAnchor. |

Puesto que no se puede cambiar el atributo de hello, debe tener un atributo buena toouse. Un buen candidato es objectGUID. Este atributo no se cambia, a menos que la cuenta de usuario de Hola se mueve entre bosques o dominios. En un entorno de varios bosques donde mover cuentas entre bosques, debe usarse otro atributo, como un atributo con hello employeeID. Evite los atributos que puedan cambiar si una persona se casa o se cambian las asignaciones. No se pueden utilizar los atributos con @-sign, por lo que no se puede utilizar el correo electrónico ni userPrincipalName. atributo de Hello también distingue mayúsculas de minúsculas por lo que cuando se mueve un objeto entre bosques, debe seguro toopreserve Hola mayúscula o minúscula. Los atributos binarios tienen codificación base64, pero otros tipos de atributo permanecerán en su estado sin codificar. En escenarios de federación y en algunas interfaces de Azure AD, este atributo se conoce también como immutableID. Para obtener más información acerca de delimitador de origen Hola puede encontrarse en hello [conceptos de diseño](active-directory-aadconnect-design-concepts.md#sourceanchor).

### <a name="sync-filtering-based-on-groups"></a>Filtrado de sincronización basado en grupos
Hola filtrado en la característica grupos permite toosync solo un pequeño subconjunto de objetos para una prueba piloto. toouse esta característica, cree un grupo para este fin en su Active Directory local. A continuación, agregar usuarios y grupos que deben estar sincronizado tooAzure AD como miembros directos. Más adelante puede agregar y quitar usuarios toothis grupo toomaintain Hola lista de objetos que deben estar presentes en Azure AD. Todos los objetos que desea toosynchronize deben ser un miembro directo del grupo de Hola. Los usuarios, grupos, contactos y equipos o dispositivos deben ser miembros directos. No se resuelve la pertenencia a grupos anidados. Cuando se agrega un grupo al agregar un miembro, sólo Hola grupo y no a sus miembros.

![Filtrado de sincronización ](./media/active-directory-aadconnect-get-started-custom/filter2.png)

> [!WARNING]
> Esta característica es solo previsto toosupport una implementación piloto. No se debe usar en una implementación de producción completa.
>
>

En una implementación de producción completo, será necesario toomaintain de disco duro de toobe un único grupo con toosynchronize de todos los objetos. En su lugar, debe usar uno de los métodos de hello en [Configurar filtrado](active-directory-aadconnectsync-configure-filtering.md).

### <a name="optional-features"></a>Características opcionales
Esta pantalla le permite características opcionales de hello tooselect para los escenarios específicos.

![Características opcionales](./media/active-directory-aadconnect-get-started-custom/optional.png)

> [!WARNING]
> Si actualmente tiene DirSync o Azure AD Sync active, no Active cualquiera de las características de la escritura diferida de hello en Azure AD Connect.
>
>

| Características opcionales | Description |
| --- | --- |
| Implementación híbrida de Exchange |Hello característica de implementación híbrida de Exchange permite Hola coexistencia de buzones de correo Exchange tanto de forma local y en Office 365. Azure AD Connect sincroniza un conjunto específico de [atributos](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) de Azure AD en su directorio local. |
| Carpetas públicas de correo de Exchange | característica de carpetas públicas de correo electrónico de Exchange de Hello permite objetos habilitados para correo electrónico de carpetas públicas de toosynchronize desde su tooAzure de Active Directory local AD. |
| Aplicación Azure AD y filtro de atributos |Al habilitar la aplicación de Azure AD y el filtrado de atributos, hello conjunto de atributos sincronizados puede personalizarse. Esta opción agrega a dos más páginas toohello Asistente para configuración. Para más información, consulte [Aplicación Azure AD y filtro de atributos](#azure-ad-app-and-attribute-filtering). |
| Sincronización de contraseñas |Si ha seleccionado la federación como solución de inicio de sesión de hello, a continuación, puede habilitar esta opción. A continuación, la sincronización de contraseñas se puede usar como opción de copia de seguridad. Para más información, consulte [Sincronización de contraseñas](active-directory-aadconnectsync-implement-password-synchronization.md). </br></br>Si ha seleccionado la autenticación de paso a través, esta opción está habilitada por el soporte técnico de tooensure predeterminado para los clientes heredados y como una opción de copia de seguridad. Para más información, consulte [Sincronización de contraseñas](active-directory-aadconnectsync-implement-password-synchronization.md).|
| Escritura diferida de contraseñas |Al habilitar la escritura diferida de contraseñas, los cambios de contraseña que se originan en Azure AD se reescriben directorio local de tooyour. Para más información, consulte [Introducción a la administración de contraseñas](../active-directory-passwords-getting-started.md). |
| Escritura diferida de grupos |Si usas hello **grupos de Office 365** característica, puede tener estos grupos representados en su Active Directory local. Esta opción solo está disponible si dispone de Exchange en su Active Directory local. Para más información, consulte [Escritura diferida de grupos](active-directory-aadconnect-feature-preview.md#group-writeback). |
| Escritura diferida de dispositivos |Le permite toowriteback los objetos de dispositivo en Azure AD tooyour en Active Directory local para escenarios de acceso condicional. Para más información, consulte [Habilitación de la escritura diferida de dispositivos](active-directory-aadconnect-feature-device-writeback.md). |
| Sincronización de atributos de las extensiones de directorios |Al habilitar la sincronización de atributos de las extensiones de directorio, los atributos especificados están sincronizado tooAzure AD. Para más información, consulte [Extensiones de directorio](active-directory-aadconnectsync-feature-directory-extensions.md). |

### <a name="azure-ad-app-and-attribute-filtering"></a>Aplicación Azure AD y filtro de atributos
Si desea toolimit qué tooAzure de toosynchronize atributos AD, inicio, a continuación, seleccionando los servicios que usa. Si realiza cambios en la configuración de esta página, un nuevo servicio tiene toobe seleccionarse explícitamente ejecutando de nuevo el Asistente para la instalación de Hola.

![Aplicaciones de características opcionales](./media/active-directory-aadconnect-get-started-custom/azureadapps2.png)

En función de servicios de hello seleccionados en el paso anterior de hello, esta página muestra todos los atributos que se sincronizan. Esta lista es una combinación de todos los tipos de objeto que se están sincronizando. Si no hay algunos atributos en particular necesita toonot sincronización, puede anular la selección de estos atributos.

![Atributos de características opcionales](./media/active-directory-aadconnect-get-started-custom/azureadattributes2.png)

> [!WARNING]
> Si quita los atributos, se podrá ver afectada la funcionalidad. Para conocer los procedimientos recomendados, consulte [Atributos sincronizados con Azure Active Directory](active-directory-aadconnectsync-attributes-synchronized.md#attributes-to-synchronize).
>
>

### <a name="directory-extension-attribute-sync"></a>Sincronización de atributos de las extensiones de directorios
Puede extender el esquema de hello en Azure AD con atributos personalizados agregados por su organización u otros atributos de Active Directory. toouse esta característica, seleccione **sincronización de atributos de extensión de directorio** en hello **características opcionales** página. Puede seleccionar más toosync de atributos en esta página.

![Sincronización de Azure AD Connect: Extensiones de directorio](./media/active-directory-aadconnect-get-started-custom/extension2.png)

Para más información, consulte [Extensiones de directorio](active-directory-aadconnectsync-feature-directory-extensions.md).

### <a name="enabling-single-sign-on-sso"></a>Habilitación del inicio de sesión único (SSO)
Configurar inicio de sesión único para su uso con la autenticación de la sincronización de contraseña o acceso directo es un proceso sencillo que sólo es necesario toocomplete una vez para cada bosque que se está sincronizada tooAzure AD. La configuración se realiza en dos pasos:

1.  Crear cuenta de equipo necesarias de hello en su Active Directory local.
2.  Configurar la zona de intranet de Hola de máquinas de cliente hello toosupport único inicio de sesión.

#### <a name="create-hello-computer-account-in-active-directory"></a>Creación de cuentas de equipo de hello en Active Directory
Para cada bosque que se ha agregado en Azure AD Connect, necesitará credenciales de administrador de dominio de toosupply para que se puedan crear cuenta de equipo de hello en cada bosque. credenciales de Hello son solo usa toocreate Hola cuenta y no se almacena o utilizadas para cualquier otra operación. Basta con agregar credenciales de hello en hello **habilitar único inicio de sesión** página del Asistente de hello Azure AD Connect como se muestra:

![Habilitar el inicio de sesión único](./media/active-directory-aadconnect-get-started-custom/enablesso.png)

>[!NOTE]
>Puede omitir un bosque particular si no desea toouse inicio de sesión único con ese bosque.

#### <a name="configure-hello-intranet-zone-for-client-machines"></a>Configurar la zona de Intranet de Hola para equipos cliente
tooensure que Hola cliente inicios de sesión automáticamente en la intranet de hello zona necesita tooensure que dos direcciones URL forman parte de la zona de intranet de Hola. Esto garantiza que ese equipo unido a un dominio Hola envía automáticamente un tooAzure de vale de Kerberos AD cuando está conectado toohello red corporativa.
En un equipo que dispone de herramientas de administración de directiva de grupo Hola.

1.  Abrir las herramientas de administración de directivas de grupo Hola
2.  Editar directiva de grupo de Hola que vayan a ser usuarios tooall aplicada. Por ejemplo, hello directiva predeterminada de dominio.
3.  Navegue demasiado**usuario Configuración del equipo\Plantillas administrativas\Componentes de Windows\Internet Internet Control Internet\página** y seleccione **tooZone lista de asignación de sitio** por imagen Hola a continuación.
4.  Habilitar directiva de Hola y escriba Hola siguientes dos elementos en el cuadro de diálogo de Hola.

        Value: `https://autologon.microsoftazuread-sso.com`  
        Data: 1  
        Value: `https://aadg.windows.net.nsatc.net`  
        Data: 1

5.  Debería ser similar siguiente toohello:  
![Zonas de intranet](./media/active-directory-aadconnect-get-started-custom/sitezone.png)

6.  Haga clic en **Ok** (Aceptar) dos veces.

## <a name="configuring-federation-with-ad-fs"></a>Configuración de federación con AD FS
La configuración de AD FS con Azure AD Connect es muy sencilla y solo se necesitan unos cuantos clics. Hola siguiente es necesario antes de la configuración de Hola.

* Un servidor de Windows Server 2012 R2 para servidor de federación de hello con administración remota habilitada
* Un servidor de Windows Server 2012 R2 para servidor de Proxy de aplicación Web de hello con administración remota habilitada
* Nombre que pretenda toouse (por ejemplo sts.contoso.com) de servicio de un certificado SSL para la federación de Hola

### <a name="ad-fs-configuration-pre-requisites"></a>Requisitos previos de la configuración de AD FS
tooconfigure de AD FS mediante Azure AD Connect de la granja de servidores, asegúrese de que WinRM está habilitado en los servidores remotos de Hola. Además, vaya a través de requisito de hello puertos enumerado en [tabla 3: Azure AD Connect y WAP o servidores de federación](active-directory-aadconnect-ports.md#table-3---azure-ad-connect-and-ad-fs-federation-serverswap).

### <a name="create-a-new-ad-fs-farm-or-use-an-existing-ad-fs-farm"></a>Creación de una nueva granja de AD FS o utilización de una granja de AD FS existente
Puede usar una granja de servidores de AD FS existente o puede elegir toocreate una nueva granja de AD FS. Si elige una nueva toocreate, son certificado SSL de hello tooprovide necesarios. Si el certificado SSL de hello está protegido por una contraseña, se pedirá la contraseña de Hola.

![Granja de AD FS](./media/active-directory-aadconnect-get-started-custom/adfs1.png)

Si decide toouse en una granja de AD FS, se realizan directamente toohello configurar la relación de confianza de hello entre la pantalla de AD FS y Azure.

### <a name="specify-hello-ad-fs-servers"></a>Especificar servidores de hello AD FS
Especifique los servidores de Hola que desee tooinstall AD FS en. Puede agregar uno o más servidores según su necesidades de planeación de capacidad. Combine todos los servidores tooActive directorio antes de realizar esta configuración. Microsoft recomienda instalar un único servidor de AD FS para las implementaciones piloto y de prueba. A continuación, agregar e implementar sus necesidades de escalado de más toomeet de servidores mediante la ejecución de Azure AD Connect nuevo tras la configuración inicial.

> [!NOTE]
> Asegúrese de que todos los servidores están unidos a un tooan AD dominio antes de realizar esta configuración.
>
>

![Servidores de AD FS](./media/active-directory-aadconnect-get-started-custom/adfs2.png)

### <a name="specify-hello-web-application-proxy-servers"></a>Especificar servidores de Proxy de aplicación Web de Hola
Especifique servidores Hola que desea incluir como los servidores de proxy de aplicación Web. servidor de proxy de aplicación de Hello web se implementa en la red Perimetral (con conexión a extranet) y es compatible con las solicitudes de autenticación de extranet Hola. Puede agregar uno o más servidores según su necesidades de planeación de capacidad. Microsoft recomienda instalar un único servidor proxy de aplicación web para las implementaciones piloto y de prueba. A continuación, agregar e implementar sus necesidades de escalado de más toomeet de servidores mediante la ejecución de Azure AD Connect nuevo tras la configuración inicial. Se recomienda tener un número equivalente de autenticación de toosatisfy de servidores proxy de intranet de Hola.

> [!NOTE]
> <li> Si cuenta Hola que usa no es un administrador local en los servidores de AD FS hello, se pedirá las credenciales de administrador.</li>
> <li> Asegúrese de que hay conectividad HTTP/HTTPS entre servidor de Azure AD Connect de Hola y Hola Proxy de aplicación Web antes de ejecutar este paso.</li>
> <li> Asegúrese de que hay conectividad HTTP/HTTPS entre servidor de aplicaciones Web de Hola y Hola AD FS server tooallow autenticación solicitudes tooflow a través de.</li>
>

![Aplicación web](./media/active-directory-aadconnect-get-started-custom/adfs3.png)

Son las credenciales solicitadas tooenter para que hello servidor de aplicaciones web puede establecer un conexión segura toohello AD FS servidor. Estas credenciales deben toobe un administrador local en el servidor de AD FS Hola.

![Proxy](./media/active-directory-aadconnect-get-started-custom/adfs4.png)

### <a name="specify-hello-service-account-for-hello-ad-fs-service"></a>Especificar cuenta de servicio de Hola para hello servicio AD FS
servicio de Hello AD FS requiere un dominio de servicio a los usuarios de cuenta tooauthenticate e información de usuario de búsqueda en Active Directory. Puede admitir dos tipos de cuentas de servicio:

* **Cuenta de servicio administrada de grupo**: se introdujo en Active Directory Domain Services con Windows Server 2012. Este tipo de cuenta proporciona servicios, como AD FS, una sola cuenta sin necesidad de contraseña de cuenta de hello tooupdate con regularidad. Utilice esta opción si ya tiene controladores de dominio de Windows Server 2012 en dominio de Hola que pertenecen los servidores de AD FS a.
* **Cuenta de usuario de dominio** -este tipo de cuenta requiere tooprovide una contraseña periódicamente y actualizar la contraseña de hello cuando los cambios de contraseña de Hola o expira. Utilice esta opción sólo cuando no tiene controladores de dominio de Windows Server 2012 en dominio de Hola que pertenecen los servidores de AD FS a.

Si ha seleccionado Cuenta de servicio administrada de grupo y esta característica no se ha usado nunca en Active Directory, se le pedirán las credenciales de administrador de organización. Estas credenciales son el almacén de claves usados tooinitiate hello y habilitar la característica de hello en Active Directory.

> [!NOTE]
> Azure AD Connect realiza una comprobación toodetect si el servicio de hello AD FS ya está registrado como un SPN en el dominio de Hola.  AD DS no permitirá toobe del SPN duplicado registrado al mismo tiempo.  Si se encuentra un SPN duplicado, no será capaz de tooproceed más hasta que se quite Hola SPN.

![Cuenta de servicio de AD FS](./media/active-directory-aadconnect-get-started-custom/adfs5.png)

### <a name="select-hello-azure-ad-domain-that-you-wish-toofederate"></a>Seleccione dominio hello Azure AD que desea toofederate
Esta configuración es la relación de federación de hello toosetup utilizado entre AD FS y Azure. Configura tooAzure de tokens de seguridad de AD FS tooissue AD y tokens de Azure AD tootrust Hola de esta instancia concreta de AD FS. Esta página solo permite tooconfigure un único dominio en la instalación inicial de Hola. Si vuelve a ejecutar Azure AD Connect después podrá configurar más dominios.

![Dominio de Azure AD](./media/active-directory-aadconnect-get-started-custom/adfs6.png)

### <a name="verify-hello-azure-ad-domain-selected-for-federation"></a>Comprobar el dominio de hello Azure AD seleccionado para la federación
Cuando se selecciona hello toobe de dominio federado, Azure AD Connect proporciona información necesaria tooverify un dominio no comprobado. Vea [agregar y comprobar el dominio de hello](../active-directory-add-domain.md) para saber cómo toouse esta información.

![Dominio de Azure AD](./media/active-directory-aadconnect-get-started-custom/verifyfeddomain.png)

> [!NOTE]
> Dominio AD Connect intentos tooverify Hola durante Hola configurar fase. Si sigues tooconfigure sin agregar registros DNS necesarios de hello, Asistente Hola configuración no es capaz de toocomplete Hola.
>
>

## <a name="configure-and-verify-pages"></a>Configurar y comprobar páginas
configuración de saludo se realiza en esta página.

> [!NOTE]
> Si configuró la federación, antes de seguir con la instalación, asegúrese de que ha configurado la [Resolución de nombres para los servidores de federación](active-directory-aadconnect-prerequisites.md#name-resolution-for-federation-servers).
>
>

![Tooconfigure listo](./media/active-directory-aadconnect-get-started-custom/readytoconfigure2.png)

### <a name="staging-mode"></a>Modo provisional
Es posible toosetup un nuevo servidor de sincronización en paralelo con el modo de almacenamiento provisional. Es solo compatibles toohave un servidor de sincronización exportando tooone directorio en la nube de Hola. Pero si desea que toomove desde otro servidor, por ejemplo una ejecución de sincronización de directorios, puede habilitar Azure Connect de AD en modo de almacenamiento provisional. Cuando se habilita, sincronización de Hola motor importar y sincronizar los datos como es habitual, pero no exporta nada tooAzure AD o AD. Hola características sincronización y la contraseña de escritura diferida de contraseñas están deshabilitados mientras está en modo de almacenamiento provisional.

![Modo provisional](./media/active-directory-aadconnect-get-started-custom/stagingmode.png)

Mientras esté en modo de almacenamiento provisional, es el motor de sincronización de toohello toomake posibles cambios necesarios y revisar lo que estará toobe exportado. Cuando la configuración de hello es correcto, vuelva a ejecutar el Asistente para la instalación de Hola y deshabilitar el modo de almacenamiento provisional. Datos ahora están exportado tooAzure AD desde este servidor. Asegúrese de toodisable seguro Hola a otro servidor en hello activamente está exportando el mismo servidor de tiempo para que sólo una.

Para más información, consulte [Modo provisional](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-your-federation-configuration"></a>Comprobación de la configuración de la federación
Azure AD Connect comprueba las opciones de DNS de hello automáticamente al hacer clic en el botón verificar de Hola.

**Comprobaciones de conectividad a Internet**

* Resolver el FQDN de la federación: Azure AD Connect comprueba si se puede resolver el FQDN de la federación hello tooensure una conectividad de DNS. Si Azure AD Connect no puede resolver el FQDN de hello, se producirá un error en la comprobación de Hola. Asegúrese de que existe un registro DNS para el servicio de federación de hello FQDN de comprobación de orden toosuccessfully Hola completa.
* Registro DNS D: Azure AD Connect comprueba si hay un registro D para el servicio de federación. En ausencia de Hola de un registro, se producirá un error en comprobación de Hola. Crear un registro y no un registro CNAME para el FQDN de la federación en orden toosuccessfully completar la comprobación de Hola.

**Comprobaciones de conectividad a la extranet**

* Resolver el FQDN de la federación: Azure AD Connect comprueba si se puede resolver el FQDN de la federación hello tooensure una conectividad de DNS.

![Complete](./media/active-directory-aadconnect-get-started-custom/completed.png)

![Verify](./media/active-directory-aadconnect-get-started-custom/adfs7.png)

Además, lleve a cabo Hola siguiendo los pasos de comprobación:

* Validar que pueden iniciar sesión desde un explorador desde una máquina unida al dominio de intranet de hello: conectar toohttps://myapps.microsoft.com y comprobar el inicio de sesión en hello con su cuenta ha iniciado sesión. cuenta de administrador de Hello integrado AD DS no está sincronizado y no se puede usar para la comprobación.
* Validar que pueden iniciar sesión desde un dispositivo de hello extranet. En un equipo doméstico o un dispositivo móvil, conéctese toohttps://myapps.microsoft.com y proporcionar las credenciales.
* Valide el inicio de sesión de un cliente mejorado. Conectar toohttps://testconnectivity.microsoft.com, elija hello **Office 365** Hola de pestaña y seleccione **Office 365 Single Sign-On prueba**.

## <a name="next-steps"></a>Pasos siguientes
Una vez finalizada la instalación de hello, la sesión e iníciela de nuevo tooWindows antes de usar el administrador del servicio de sincronización o Editor de reglas de sincronización.

Ahora que tiene instalado de Azure AD Connect puede [comprobar la instalación de Hola y asignar licencias](active-directory-aadconnect-whats-next.md).

Obtener más información sobre estas características, que estaban habilitadas con la instalación de hello: [evitar eliminaciones accidentales](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) y [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Más información acerca de estos temas comunes: [programador y cómo sincronizar tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
