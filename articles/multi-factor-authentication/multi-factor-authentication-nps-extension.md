---
title: aaaUse capacidades existentes de NPS servidores tooprovide MFA de Azure | Documentos de Microsoft
description: "Hola extensión de servidor de directivas de red para la autenticación multifactor Azure es una solución sencilla tooadd dos pasos en la nube vericiation capacidades tooyour infraestructura de autenticación existente."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: e9fc495b06873d45f06233f1aa618db9d94f8bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication"></a>Integración de la infraestructura existente de NPS con Azure Multi-Factor Authentication

extensión de servidor de directivas de redes (NPS) para Azure MFA Hola agrega basada en la nube MFA capacidades tooyour infraestructura de autenticación con los servidores existentes. Con hello extensión NPS, puede agregar la llamada de teléfono, mensaje de texto o flujo de autenticación existente de teléfono aplicación comprobación tooyour sin necesidad de tooinstall, configurar y mantener servidores nuevos. 

Esta extensión se creó para las organizaciones que desean las conexiones VPN de tooprotect sin implementar Hola servidor Azure MFA. Hola extensión NPS actúa como un adaptador entre RADIUS y tooprovide en la nube de Azure MFA un segundo factor de autenticación de usuarios federados o sincronizados.

Cuando se utiliza la extensión NPS de Hola para Azure MFA, flujo de autenticación de hello incluye Hola de los componentes siguientes: 

1. **Servidor VPN de NAS** recibe solicitudes de los clientes VPN y los convierte en servidores de tooNPS de solicitudes RADIUS. 
2. **Servidor NPS** conecta tooActive Directory tooperform Hola autenticación principal para hello RADIUS solicita y, cuando se realiza correctamente, pasa las extensiones de hello solicitud tooany instalado.  
3. **Extensión de NPS** desencadena una solicitud tooAzure MFA para la autenticación secundaria Hola. Una vez que la extensión de hello recibe respuesta Hola y Hola desafío MFA se realiza correctamente, completa la solicitud de autenticación de hello proporcionando servidor NPS de hello con tokens de seguridad que incluyen una notificación MFA, emitida por el STS de Azure.  
4. **Azure MFA** se comunica con los detalles de usuario de Azure Active Directory tooretrieve hello y realiza la autenticación secundaria de hello mediante un usuario de toohello método configurado de comprobación.

Hola siguiente diagrama ilustra este flujo de solicitud de autenticación de alto nivel: 

![Diagrama de flujo de autenticación](./media/multi-factor-authentication-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a>Planeamiento de la implementación

Hola extensión NPS controla automáticamente la redundancia, por lo que no necesita una configuración especial.

Puede crear tantos servidores NPS habilitados para Azure MFA como necesite. Si instala varios servidores, debe usar un certificado de cliente distinto para cada uno de ellos. La creación de un certificado para cada servidor significa que puede actualizar individualmente cada certificado y no preocuparse por el tiempo de inactividad en los servidores.

Servidores VPN de enrutan las solicitudes de autenticación, por lo que necesitan toobe consciente de nuevos servidores NPS habilitado para Azure MFA Hola.

## <a name="prerequisites"></a>Requisitos previos

Hola extensión NPS está pensado toowork con la infraestructura existente. Asegúrese de que tiene Hola siguiendo los requisitos previos antes de comenzar.

### <a name="licenses"></a>Licencias

Hola extensión de NPS para Azure MFA está disponible toocustomers con [licencias para la autenticación multifactor Azure](multi-factor-authentication.md) (incluido con Azure AD Premium, EMS o una suscripción de MFA).

### <a name="software"></a>Software

Windows Server 2008 R2 SP1 o superior.

### <a name="libraries"></a>Bibliotecas

Estas bibliotecas se instalan automáticamente con la extensión de Hola.
-   [Paquetes redistribuibles de Visual C++ para Visual Studio 2013 (X64)](https://www.microsoft.com/download/details.aspx?id=40784)
-   [Módulo Microsoft Azure Active Directory para Windows PowerShell versión1.1.166.0](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

### <a name="azure-active-directory"></a>Azure Active Directory

Todos los usuarios con la extensión NPS Hola deben ser sincronizado tooAzure Active Directory mediante Azure AD Connect y debe estar registrado para MFA.

Cuando se instala la extensión de hello, necesita credenciales de administrador y el Id. de directorio de Hola para su inquilino de Azure AD. Puede encontrar el identificador de directorio en hello [portal de Azure](https://portal.azure.com). Inicie sesión como administrador, seleccione hello **Azure Active Directory** situado a la izquierda hello, a continuación, seleccione **propiedades**. Hola copia GUID en hello **Id. de directorio** cuadro y guárdelo. Este GUID se usa como Id. de inquilino de hello cuando instala Hola extensión NPS.

![Busque el identificador de directorio en las propiedades de Azure Active Directory.](./media/multi-factor-authentication-nps-extension/find-directory-id.png)

## <a name="prepare-your-environment"></a>Preparación del entorno

Antes de instalar la extensión NPS hello, que desee tooprepare se entorno toohandle Hola tráfico de autenticación.

### <a name="enable-hello-nps-role-on-a-domain-joined-server"></a>Habilitar el rol NPS de hello en un servidor unido a un dominio

servidor NPS Hola conecta tooAzure Active Directory y autentica las solicitudes MFA de Hola. Elija un servidor para este rol. Se recomienda elegir un servidor que no controla las solicitudes de otros servicios, porque Hola extensión NPS produce errores para las solicitudes que no son RADIUS.

1. En el servidor, abra hello **agregar Roles y características Asistente** de hello menú Quickstart administrador del servidor.
2. Elija **Instalación basada en características o en roles** como tipo de instalación.
3. Seleccione hello **servicios de acceso y directivas de redes** rol de servidor. Una ventana puede emergente tooinform de características necesarias toorun este rol.
4. Continúe con el Asistente de hello hasta la página de confirmación de Hola. Seleccione **Instalar**.

Ahora que tiene un servidor designado para NPS, también debe configurar este servidor toohandle las solicitudes RADIUS entrantes de hello solución VPN.

### <a name="configure-your-vpn-solution-toocommunicate-with-hello-nps-server"></a>Configurar la toocommunicate de solución VPN con el servidor NPS de Hola

Dependiendo de qué solución VPN que utilice, Hola tooconfigure pasos varían en su directiva de autenticación de RADIUS. Configure el servidor de directivas toopoint tooyour RADIUS NPS.

### <a name="sync-domain-users-toohello-cloud"></a>Nube de toohello de usuarios de dominio de sincronización

Este paso ya puede ser completa en su inquilino, pero es buena comprobación toodouble que Azure AD Connect se ha sincronizado sus bases de datos recientemente.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) como administrador.
2. Seleccione **Azure Active Directory** > **Azure AD Connect**.
3. Compruebe que el estado de sincronización es **Habilitado** y que la última sincronización fue hace menos de una hora.

Si necesita tookick desactivar una nueva ronda de sincronización, nos Hola instrucciones [Azure AD Connect sync: programador](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).

### <a name="determine-which-authentication-methods-your-users-can-use"></a>Determinación de los métodos de autenticación que pueden utilizar los usuarios

Existen dos factores que afectan a la disponibilidad de los métodos de autenticación con una implementación de extensión NPS:

1. algoritmo de cifrado de contraseña de Hello utilizado entre el cliente RADIUS de hello (VPN, servidor Netscaler, u otros) y servidores NPS de Hola.
   - **PAP** admite todos los métodos de autenticación de Hola de MFA de Azure en la nube de hello: llamada de teléfono, mensaje de texto unidireccional, notificación de aplicación móvil y código de comprobación de la aplicación móvil.
   - **CHAPV2** y **EAP** admiten llamadas de teléfono y notificaciones de aplicación móvil.
2. Hola métodos que Hola aplicación cliente de entrada (VPN, servidor Netscaler, u otros) puede controlar. ¿Por ejemplo, cliente VPN de hello tener alguna manera tooallow Hola usuario tootype en un código de comprobación de un texto o aplicación móvil?

Cuando se implementa la extensión NPS hello, utilice estos tooevaluate factores qué métodos están disponibles para los usuarios. Si el cliente RADIUS es compatible con PAP, pero el cliente de hello UX no tiene campos de entrada para un código de comprobación, a continuación, llamada de teléfono y notificación de aplicación móvil son Hola dos opciones admitidas.

Puede [deshabilitar los métodos de autenticación no compatibles](multi-factor-authentication-whats-next.md#selectable-verification-methods) en Azure.

### <a name="enable-users-for-mfa"></a>Habilitar a los usuarios para MFA

Antes de implementar la extensión NPS completa hello, necesita tooenable MFA para los usuarios de Hola que desea verificacion de tooperform. Más inmediatamente, extensión de hello tootest que implementarlo, necesita al menos una prueba cuenta totalmente registrado para la autenticación multifactor.

Use estos tooget pasos inició una cuenta de prueba:
1. Inicie sesión en demasiado[https://aka.ms/mfasetup](https://aka.ms/mfasetup) con una cuenta de prueba. 
2. Siga tooset de mensajes de Hola un método de comprobación.
3. Cree una directiva de acceso condicional o [cambiar el estado de usuario de hello](multi-factor-authentication-get-started-user-states.md) toorequire verificacion de cuenta de prueba de Hola. 

Los usuarios también necesitan toofollow tooenroll de estos pasos antes de que pueden autenticarse con la extensión NPS Hola.

## <a name="install-hello-nps-extension"></a>Instalar extensión NPS Hola

> [!IMPORTANT]
> Instalar extensión NPS de hello en un servidor distinto al punto de acceso VPN de Hola.

### <a name="download-and-install-hello-nps-extension-for-azure-mfa"></a>Descargar e instalar la extensión NPS de Hola para Azure MFA

1.  [Descargar Hola NPS extensión](https://aka.ms/npsmfa) de hello Microsoft Download Center.
2.  Copie Hola binario toohello desea tooconfigure el servidor de directivas de red.
3.  Ejecutar *setup.exe* y siga las instrucciones de instalación de Hola. Si se producen errores, compruebe que Hola dos bibliotecas de la sección de requisitos previos de Hola se han instalado correctamente.

### <a name="run-hello-powershell-script"></a>Ejecutar script de PowerShell de Hola

instalador de Hello crea un script de PowerShell en esta ubicación: `C:\Program Files\Microsoft\AzureMfa\Config` (donde C:\ es la unidad de instalación). Este script de PowerShell realiza Hola siguientes acciones:

-   Creación de un certificado autofirmado.
-   Asociar la clave pública de Hola Hola certificado toohello entidad de servicio en Azure AD.
-   Almacén de certificados de hello en el almacén de certificados del equipo local de Hola.
-   Privada clave tooNetwork GRANT toohello el certificado de acceso usuario.
-   Reinicie Hola NPS.

A menos que desee toouse sus propios certificados (en lugar de hello certificados autofirmados que genera el script de PowerShell de Hola), ejecute hello Script de PowerShell instalación de hello toocomplete. Si se instala la extensión de hello en varios servidores, cada uno debe tener su propio certificado.

1. Ejecute Windows PowerShell como administrador.
2. Cambie los directorios.

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. Ejecutar script de PowerShell de hello creado por el instalador de Hola.

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. PowerShell le pide el identificador de inquilino. Usar hello GUID de Id. de directorio que copió del portal de Azure en la sección de requisitos previos de Hola Hola.
5. Inicie sesión en tooAzure AD como administrador.
6. PowerShell muestra un mensaje de confirmación cuando haya finalizado la secuencia de comandos de Hola.  

Repita estos pasos en todos los servidores NPS adicionales que desee tooset hacia arriba para equilibrio de carga.

>[!NOTE]
>Si utiliza sus propios certificados en lugar de generar certificados con hello script de PowerShell, asegúrese de que estén alineados toohello convención de nomenclatura de NPS. debe ser el nombre de sujeto de Hello **CN =\<TenantID\>, OU = Microsoft NPS extensión**. 

## <a name="configure-your-nps-extension"></a>Configuración de la extensión de NPS

En esta sección se incluyen consideraciones de diseño y sugerencias para las implementaciones correctas de la extensión de NPS.

### <a name="configuration-limitations"></a>Limitaciones de configuración

- Hola extensión NPS para MFA de Azure no incluye herramientas toomigrate usuarios y la configuración de nube de servidor MFA toohello. Por este motivo, se recomienda utilizar la extensión de Hola para nuevas implementaciones, en lugar de implementación existente. Si se usa la extensión de hello en una implementación existente, los usuarios tienen tooperform prueba el nuevo toopopulate detalles de su MFA en la nube de Hola.  
- Hola extensión NPS usa Hola los usuario de Hola de tooidentify de Active directory en Azure MFA para realizar la extensión de Hola de hello autenticación secundaria pueden ser toouse configurado un identificador diferente como inicio de sesión alternativo personalizado de Active Directory o Id. de local UPN de Hola campo que no sea de UPN. Vea [configuración las opciones avanzadas para hello extensión NPS para la autenticación multifactor](multi-factor-authentication-advanced-vpn-configurations.md) para obtener más información.
- No todos los protocolos de cifrado son compatibles con todos los métodos de comprobación.
   - **PAP** admite llamadas de teléfono, mensajes de texto unidireccionales, notificaciones de aplicación móvil y códigos de comprobación de aplicación móvil
   - **CHAPV2** y **EAP** admiten llamadas de teléfono y notificaciones de aplicación móvil.

### <a name="control-radius-clients-that-require-mfa"></a>Control de clientes RADIUS que requieren MFA

Una vez que habilite MFA para un cliente RADIUS mediante Hola extensión de NPS, todas las autenticaciones para este cliente son necesario tooperform MFA. Si desea tooenable MFA para algunos clientes RADIUS, pero no otros, puede configurar dos servidores NPS e instalar extensión de hello en solo uno de ellos. Configurar a los clientes RADIUS que desea toorequire MFA toosend solicitudes toohello NPS configurado servidor con la extensión de hello y otro servidor NPS de toohello de los clientes RADIUS no está configurado con la extensión de Hola.

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a>Preparación para los usuarios que no están inscritos en MFA

Si tiene usuarios que no están inscritos para MFA, puede determinar lo que sucede cuando intentan tooauthenticate. Usar la configuración del registro de hello *REQUIRE_USER_MATCH* en la ruta de acceso de registro de hello *HKLM\Software\Microsoft\AzureMFA* toocontrol comportamiento de Hola de características. Esta opción tiene una única opción de configuración:

| Clave | Valor | Valor predeterminado |
| --- | ----- | ------- |
| REQUIRE_USER_MATCH | TRUE/FALSE | No establezca (tooTRUE equivalente) |

Hola propósito de esta configuración es toodetermine qué toodo cuando un usuario no está inscrito para MFA. Cuando clave hello no existe, no se establece o se establece tooTRUE y usuario hello no está inscrito, a continuación, extensión Hola se produce un error de desafío MFA de Hola. Cuando se establece la tooFALSE de clave de Hola y Hola usuario no está inscrito, autenticación continúa sin realizar MFA.

Puede elegir toocreate esta clave y establecer tooFALSE y los usuarios la incorporación, y pueden no todas se pueden inscribir en Azure MFA todavía. Sin embargo, puesto que la clave de configuración Hola permite a los usuarios que no están inscritos para toosign MFA en, debe quitar esta clave antes de ir tooproduction.

## <a name="troubleshooting"></a>Solución de problemas

### <a name="how-do-i-verify-that-hello-client-cert-is-installed-as-expected"></a>¿Cómo puedo comprobar que ese certificado de cliente de Hola se instala según lo previsto?

Busque creado por el instalador de hello en el almacén de certificados de Hola y compruebe que Hola clave privada de certificado autofirmado hello tiene permisos concedidos toouser **servicio de red**. certificado de Hello tiene un nombre de sujeto de **CN \<tenantid\>, OU = extensión de NPS de Microsoft**

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-toomy-tenant-in-azure-active-directory"></a>¿Cómo se puede comprobar que el certificado de cliente es toomy asociado inquilinos en Azure Active Directory?

Abra símbolo del sistema de PowerShell y ejecución Hola siguientes comandos:

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

Estos comandos imprimen todos los certificados de hello asociar a su inquilino de su instancia de hello extensión NPS en la sesión de PowerShell. Busque el certificado al exportar el certificado de cliente como un archivo "había codificado en Base 64 X.509(.cer)" sin clave privada de Hola y lo comparará con la lista de Hola desde PowerShell.

Válido-desde y válido-hasta que las marcas de tiempo, que se encuentran en un formato legible, pueden ser usado toofilter out misfits obvios si comando hello devuelve más de un certificado.

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a>¿Por qué las solicitudes provocan un error de token de ADAL?

Este error puede deberse tooone varias razones. Siga estos pasos toohelp solucionar problemas:

1. Reinicie el servidor NPS.
2. Compruebe que el certificado de cliente esté instalado según lo previsto.
3. Compruebe que Hola certificado está asociado con el inquilino en Azure AD.
4. Compruebe que https://login.microsoftonline.com/ es accesible desde servidor hello ejecuta la extensión de Hola.

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-hello-user-is-not-found"></a>¿Por qué producirá un error en la autenticación con un error en los registros HTTP que indica que no se encuentra ese usuario Hola?

Compruebe que se ejecuta AD Connect, y ese usuario Hola está presente en Active Directory de Windows y Azure Active Directory.

------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a>¿Por qué aparecen errores de conexión de HTTP en los registros con errores en todas las autenticaciones?

Compruebe que https://adnotifications.windowsazure.com sea accesible desde el servidor hello ejecuta la extensión de NPS Hola.


## <a name="next-steps"></a>Pasos siguientes

- Configurar los Id. alternativos de inicio de sesión, o configurar una lista de excepciones para direcciones IP que no debe realizar la comprobación de dos pasos en [configuración las opciones avanzadas para hello extensión NPS para la autenticación multifactor](nps-extension-advanced-configuration.md)

- [Resolver mensajes de error de hello extensión NPS para la autenticación multifactor de Azure](multi-factor-authentication-nps-errors.md)
