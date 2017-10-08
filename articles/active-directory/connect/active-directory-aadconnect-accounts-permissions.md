---
title: Cuentas y permisos de Azure AD Connect | Microsoft Docs
description: Este tema describe las cuentas de hello usado y creado y los permisos necesarios.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.reviewer: cychua
ms.assetid: b93e595b-354a-479d-85ec-a95553dd9cc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 70a7013e0353d74714ec8a3ff54b3e811789a0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-accounts-and-permissions"></a>Azure AD Connect: cuentas y permisos
Asistente para la instalación de Hello Azure AD Connect ofrece dos rutas de acceso diferentes:

* En la configuración rápida, Asistente Hola requiere más privilegios.  Esto es para que puede establecer la configuración de fácilmente, sin necesidad de los usuarios de toocreate o configurar los permisos.
* En la configuración personalizada, el Asistente de hello ofrece más opciones y opciones. Sin embargo, existen algunas situaciones en que es necesario tooensure tiene los permisos correctos de Hola.

## <a name="related-documentation"></a>documentación relacionada
Si no se leyó documentación hello en [integrar las identidades locales con Azure Active Directory](../active-directory-aadconnect.md), hello tabla siguiente proporciona vínculos toorelated temas.

|Tema. |Vínculo|  
| --- | --- |
|Descarga de Azure AD Connect | [Descarga de Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Instalación mediante configuración rápida | [Instalación rápida de Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|Instalación mediante configuración personalizada | [Instalación personalizada de Azure AD Connect](./active-directory-aadconnect-get-started-custom.md)|
|Actualización desde DirSync | [Actualización desde la herramienta de sincronización de Azure AD (DirSync)](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Después de la instalación | [Comprobar la instalación de Hola y asignar licencias](active-directory-aadconnect-whats-next.md)|

## <a name="express-settings-installation"></a>Instalación de la configuración rápida
En la configuración rápida, Asistente para la instalación de hello solicita las credenciales de administrador de organización de AD DS.  Esto es para que se pueda configurar el entorno local de Active Directory con los permisos necesarios para Azure AD Connect. Si va a actualizar desde DirSync, las credenciales de administradores de empresas de DS Hola AD están tooreset usado Hola por contraseña de cuenta de hello utilizada DirSync. También necesitará credenciales de administrador global de Azure AD.

| Página del asistente | Credenciales recopiladas | Permisos necesarios | Se usa para |
| --- | --- | --- | --- |
| N/D |Asistente para instalación de hello ejecución de usuario |Administrador del servidor local de Hola |<li>Crea Hola cuenta local que se utiliza como hello [cuenta de servicio de motor de sincronización](#azure-ad-connect-sync-service-account). |
| Conectar tooAzure AD |Credenciales de directorio de Azure AD |Rol de administrador global en Azure AD |<li>Habilitando la sincronización en el directorio de Azure AD Hola.</li>  <li>Creación de hello [cuenta de Azure AD](#azure-ad-service-account) que se utiliza para operaciones de sincronización en curso en Azure AD.</li> |
| Conectar tooAD DS |Credenciales de Active Directory local |Miembro del grupo de administradores empresariales (EA) hello en Active Directory |<li>Crea un [cuenta](#active-directory-account) en Active Directory y concede permisos tooit. Esto crea la cuenta es información de directorio tooread y escritura usada durante la sincronización.</li> |

### <a name="enterprise-admin-credentials"></a>Credenciales de administrador de organización
Estas credenciales solo se usan durante la instalación de hello y no se utilizan una vez completada la instalación de Hola. Hola, Administrador de organización, Administrador de dominio y no Hola debe asegurarse de que se pueden establecer permisos de hello en Active Directory en todos los dominios.

### <a name="global-admin-credentials"></a>Credenciales de administrador global
Estas credenciales solo se usan durante la instalación de hello y no se utilizan una vez completada la instalación de Hola. Es utilizado toocreate Hola [cuenta de Azure AD](#azure-ad-service-account) usados para sincronizar cambios tooAzure AD. cuenta de Hello también habilita la sincronización como una característica de Azure AD.

### <a name="permissions-for-hello-created-ad-ds-account-for-express-settings"></a>Permisos para hello crean cuenta de AD DS para la configuración rápida
Hola [cuenta](#active-directory-account) creado para leer y escribir tooAD DS tienen los siguientes permisos al crear mediante la configuración rápida de hello:

| Permiso | Usado para |
| --- | --- |
| <li>Replicación de cambios de directorio</li><li>Replicación de todos los cambios de directorio |Sincronización de contraseñas |
| Lectura y escritura de todas las propiedades Usuario |Importación y Exchange híbrido |
| Lectura y escritura de todas las propiedades iNetOrgPerson |Importación y Exchange híbrido |
| Lectura y escritura de todas las propiedades Grupo |Importación y Exchange híbrido |
| Lectura y escritura de todas las propiedades Contacto |Importación y Exchange híbrido |
| Restablecimiento de contraseña |Preparación para habilitar la escritura diferida de contraseñas |

## <a name="custom-settings-installation"></a>Instalación de la configuración personalizada
Azure AD Connect versión 1.1.524.0 y versiones posteriores Asistente de hello opción toolet hello Azure AD Connect crear Hola cuenta usada tooconnect tooActive Directory.  Las versiones anteriores requieren que se crea la cuenta de hello antes de la instalación de Hola. permisos de Hello debe conceder a esta cuenta se pueden encontrar en [crear cuenta de hello AD DS](#create-the-ad-ds-account). 

| Página del asistente | Credenciales recopiladas | Permisos necesarios | Se usa para |
| --- | --- | --- | --- |
| N/D |Asistente para instalación de hello ejecución de usuario |<li>Administrador del servidor local de Hola</li><li>Si usa una versión completa de SQL Server, el usuario de hello debe ser administrador del sistema (SA) en SQL</li> |De forma predeterminada, crea la cuenta local de Hola que se usa como hello [cuenta de servicio de motor de sincronización](#azure-ad-connect-sync-service-account). cuenta de Hello solo se crea al Hola, administrador no especifica una cuenta determinada. |
| Instalar servicios de sincronización, opción de cuenta de servicio |Credenciales de cuenta de usuario local o de AD |Usuario, los permisos se conceden mediante el Asistente para la instalación de Hola |Si Hola, administrador especifica una cuenta, esta cuenta se usa como cuenta de servicio de Hola Hola servicio de sincronización. |
| Conectar tooAzure AD |Credenciales de directorio de Azure AD |Rol de administrador global en Azure AD |<li>Habilitando la sincronización en el directorio de Azure AD Hola.</li>  <li>Creación de hello [cuenta de Azure AD](#azure-ad-service-account) que se utiliza para operaciones de sincronización en curso en Azure AD.</li> |
| Conectar sus directorios |Las credenciales de Active Directory para cada bosque que está conectado tooAzure AD local |permisos de Hello dependen en las características que habilite y se encuentra en [crear cuenta de hello AD DS](#create-the-ad-ds-account) |Esta cuenta es la información de directorio tooread y escritura usada durante la sincronización. |
| Servidores de AD FS |Para cada servidor en la lista de hello, Asistente Hola recopila las credenciales cuando Hola credenciales de inicio de sesión del usuario de hello Ejecutar Asistente de Hola tooconnect insuficiente |Administrador de dominio |Instalación y configuración del rol de servidor de hello AD FS. |
| Servidores proxy de aplicación web |Para cada servidor en la lista de hello, Asistente Hola recopila las credenciales cuando Hola credenciales de inicio de sesión del usuario de hello Ejecutar Asistente de Hola tooconnect insuficiente |Administrador local del equipo de destino de Hola |Instalación y configuración del rol de servidor de WAP. |
| Credenciales de confianza del proxy |Credenciales de confianza de servicio de federación (Hola credenciales Hola utiliza proxy tooenroll para un certificado de confianza de Hola FS |Cuenta de dominio que sea un administrador local del servidor de hello AD FS |Inscripción inicial de certificados de confianza de FS WAP |
| Página de cuenta de servicio de AD FS, "Usar una opción de cuenta de usuario de dominio" |Credenciales de cuenta de usuario de AD |Usuario de dominio |se usa la cuenta de usuario de Hello AD cuyas credenciales se proporcionan como cuenta de inicio de sesión de Hola de hello AD FS. |

### <a name="create-hello-ad-ds-account"></a>Crear cuenta de hello AD DS
Hola cuenta que especifique en hello **conectar sus directorios** página debe estar presente en Active Directory anterior tooinstallation.  También debe tener permisos de hello necesario concedidos. Asistente para la instalación de Hello no comprueba los permisos de Hola y de los problemas solo se encuentran durante la sincronización.

¿Qué permisos necesita depende de características opcionales de Hola habilitar. Si tiene varios dominios, se deben conceder permisos de Hola para todos los dominios en el bosque de Hola. Si no habilita ninguna de estas características, Hola predeterminado **usuario de dominio** permisos son suficientes.

| Característica | Permisos |
| --- | --- |
| característica msDS-ConsistencyGuid |Permisos de escritura toohello msDS-ConsistencyGuid atributo documentado en [conceptos de diseño: uso de msDS-ConsistencyGuid como sourceAnchor](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). | 
| Sincronización de contraseñas |<li>Replicación de cambios de directorio</li>  <li>Replicación de todos los cambios de directorio |
| Implementación híbrida de Exchange |Escribir atributos de toohello de permisos que se describen en [Exchange híbrido reescritura](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) para usuarios, grupos y contactos. |
| Carpeta pública de correo de Exchange |Atributos de toohello de permisos de lectura se documentan en [carpetas públicas de correo electrónico de Exchange](active-directory-aadconnectsync-attributes-synchronized.md#exchange-mail-public-folder) para las carpetas públicas. | 
| Escritura diferida de contraseñas |Escribir atributos de toohello de permisos que se describen en [Introducción a administración de contraseñas](../active-directory-passwords-writeback.md) para los usuarios. |
| Escritura diferida de dispositivos |Los permisos concedidos con un script de PowerShell como se describe en [Escritura diferida de dispositivos](active-directory-aadconnect-feature-device-writeback.md). |
| Escritura diferida de grupos |Objetos de grupo Leer, Crear, Actualizar y Eliminar para **grupos de Office 365** sincronizados.  Para más información, vea [Escritura diferida de grupos](active-directory-aadconnect-feature-preview.md#group-writeback).|

## <a name="upgrade"></a>Actualizar
Cuando se actualiza desde una versión de Azure AD Connect tooa nueva versión, debe Hola los siguientes permisos:

| Principal | Permisos necesarios | Se usa para |
| --- | --- | --- |
| Asistente para instalación de hello ejecución de usuario |Administrador del servidor local de Hola |Archivos binarios de la actualización. |
| Asistente para instalación de hello ejecución de usuario |Miembro de ADSyncAdmins |Realice los cambios tooSync reglas y otra configuración. |
| Asistente para instalación de hello ejecución de usuario |Si usa una versión completa de SQL server: DBO (o similar) de la base de datos de motor de sincronización de Hola |Realice los cambios de nivel de base de datos, como actualizar tablas con nuevas columnas. |

## <a name="more-about-hello-created-accounts"></a>Más información acerca de hello creado cuentas
### <a name="active-directory-account"></a>Cuenta de Active Directory
Si utiliza la configuración rápida, se crea una cuenta en Active Directory que se usa para sincronización. cuenta de Hello creado se encuentra en el dominio raíz del bosque hello en el contenedor de usuarios de Hola y con su nombre como prefijo **MSOL_**. cuenta de Hello se crea con una contraseña larga compleja que no expire. Si tiene una directiva de contraseñas en el dominio, asegúrese de que se permitan contraseñas largas y complejas para esta cuenta.

![Cuenta de AD](./media/active-directory-aadconnect-accounts-permissions/adsyncserviceaccount.png)

Si usa una configuración personalizada, son responsables de crear la cuenta de hello antes de empezar la instalación de Hola.

### <a name="azure-ad-connect-sync-service-account"></a>Cuenta del servicio Azure AD Connect Sync
puede ejecutar el servicio de sincronización de Hello bajo diferentes cuentas. Puede ejecutarse con una **cuenta de servicio virtual** (VSA), una **cuenta de servicio administrada de grupo** (gMSA/sMSA), o una cuenta de usuario normal. Opciones de Hello admitida cambiaron con hello 2017 versión de abril de Connect cuando se realiza una instalación nueva. Si actualiza desde una versión anterior de Azure AD Connect, estas opciones adicionales no están disponibles.

| Tipo de cuenta | Opción de instalación | Descripción |
| --- | --- | --- |
| [Cuenta de servicio virtual](#virtual-service-account) | Rápida y personalizada, abril de 2017 y versiones posteriores | Ésta es la opción de Hola que se utiliza para todas las instalaciones de express, excepto para las instalaciones en un controlador de dominio. Para personalizar, es opción predeterminada de Hola a menos que se use otra opción. |
| [Cuenta de servicio administrada de grupo](#group-managed-service-account) | Personalizada, abril de 2017 y versiones posteriores | Si usa un servidor SQL remoto, se recomienda toouse un grupo de cuenta de servicio administrada. |
| [Cuenta de usuario](#user-account) | Rápida y personalizada, abril de 2017 y versiones posteriores | Durante la instalación, solo se crea una cuenta de usuario con el prefijo AAD_ cuando se instala en Windows Server 2008 y cuando se instala en un controlador de dominio. |
| [Cuenta de usuario](#user-account) | Rápida y personalizada, marzo de 2017 y versiones anteriores | Se crea una cuenta local con el prefijo AAD_ durante la instalación. Cuando se utiliza la instalación personalizada, se puede especificar otra cuenta. |

Si utiliza Connect con una compilación de marzo de 2017 o versiones anteriores, a continuación, no debe restablecer la contraseña de hello en la cuenta de servicio de Hola desde Windows destruye claves de cifrado de Hola por motivos de seguridad. No se puede cambiar otra cuenta de hello cuenta tooany sin volver a instalar Azure AD Connect. Si actualizar tooa compilación de 2017 abril o más adelante, a continuación, es contraseña de hello toochange admitidos en la cuenta de servicio de Hola pero no se puede cambiar la cuenta de hello utilizada.

> [!Important]
> Sólo puede establecer la cuenta de servicio de hello instalación la primera vez. No admite la cuenta de servicio de hello toochange una vez completada la instalación de Hola.

Se trata de una tabla de Hola de forma predeterminada, que se recomienda, y cuenta de servicio de sincronización de opciones admitidas para saludo.

Leyenda:

- **Negrita** indica la opción predeterminada de Hola y Hola la mayoría de los casos la opción recomendada.
- *Cursiva* indica Hola opción recomendada cuando no es una opción predeterminada de Hola.
- 2008: opción predeterminada cuando se instala en Windows Server 2008
- Sin negrita: opción admitida
- Cuenta local, la cuenta de usuario Local en servidor hello
- Cuenta de dominio: cuenta de usuario de dominio
- sMSA: [cuenta de servicio administrada independiente](https://technet.microsoft.com/library/dd548356.aspx)
- gMSA: [cuenta de servicio administrada de grupo](https://technet.microsoft.com/library/hh831782.aspx)

| | LocalDB</br>Express | LocalDB/LocalSQL</br>Personalizado | SQL remoto</br>Personalizado |
| --- | --- | --- | --- |
| **equipo independiente/en grupo de trabajo** | No compatible | **VSA**</br>Cuenta local (2008)</br>Cuenta local |  No compatible |
| **equipo unido a un dominio** | **VSA**</br>Cuenta local (2008) | **VSA**</br>Cuenta local (2008)</br>Cuenta local</br>Cuenta de dominio</br>sMSA, gMSA | **gMSA**</br>Cuenta de dominio |
| **Controlador de dominio** | **Cuenta de dominio** | *gMSA*</br>**Cuenta de dominio**</br>sMSA| *gMSA*</br>**Cuenta de dominio**|

#### <a name="virtual-service-account"></a>Cuenta de servicio virtual
Una cuenta de servicio virtual es un tipo especial de cuenta que no tiene contraseña y está administrada por Windows.

![VSA](./media/active-directory-aadconnect-accounts-permissions/aadsyncvsa.png)

Hola VSA está previsto toobe utilizada con escenarios donde motor de sincronización de Hola y SQL están en hello mismo servidor. Si usas SQL remoto, se recomienda toouse una [cuenta de servicio administrada de grupo](#managed-service-account) en su lugar.

Esta característica requiere Windows Server 2008 R2 o versiones posteriores. Si instalar Azure AD Connect en Windows Server 2008, instalación de hello vuelve toousing una [cuenta de usuario](#user-account) en su lugar.

#### <a name="group-managed-service-account"></a>Cuenta de servicio administrada de grupo
Si usa un servidor SQL remoto, se recomienda toousing una **cuenta de servicio administrada de grupo**. Para obtener más información acerca de cómo tooprepare su Active Directory para la cuenta de servicio administrada de grupo, consulte [Group Managed Service Accounts Overview](https://technet.microsoft.com/library/hh831782.aspx).

toouse esta opción, en hello [instalar los componentes necesarios](active-directory-aadconnect-get-started-custom.md#install-required-components) página, seleccione **usar una cuenta de servicio existente**y seleccione **cuenta de servicio administrada**.  
![VSA](./media/active-directory-aadconnect-accounts-permissions/serviceaccount.png)  
También es compatible toouse una [independiente cuenta de servicio administrada](https://technet.microsoft.com/library/dd548356.aspx). Sin embargo, solo se pueden usar en el equipo local de hello y no hay ninguna ventaja toouse ellas a través de la cuenta de servicio virtual Hola predeterminada.

Esta característica requiere Windows Server 2012 o posterior. Si necesita toouse un sistema operativo anterior y utilizan SQL remoto, debe usar un [cuenta de usuario](#user-account).

#### <a name="user-account"></a>Cuenta de usuario
Se crea una cuenta de servicio local mediante el Asistente para la instalación de hello (a menos que especifique Hola cuenta toouse en una configuración personalizada). cuenta de Hello tiene como prefijo **AAD_** y usar para hello toorun de servicio de sincronización real como. Si instala Azure AD Connect en un controlador de dominio, cuenta de hello se crea en el dominio Hola. Hola **AAD_** cuenta de servicio debe estar ubicada en el dominio de hello si:
   - Se usa un servidor remoto que ejecuta SQL Server.
   - Se usa a un proxy que requiere autenticación.

![Cuenta de servicio de sincronización](./media/active-directory-aadconnect-accounts-permissions/syncserviceaccount.png)

cuenta de Hello se crea con una contraseña larga compleja que no expire.

Esta cuenta es contraseñas de hello toostore usado para hello otras cuentas de una manera segura. Estas otras contraseñas de cuentas se almacenan cifrados en la base de datos de Hola. las claves privadas de Hola para las claves de cifrado de hello están protegidas con cifrado de clave secreta de servicios criptográficos de hello mediante la API de protección de datos (DPAPI) de Windows.

Si usa una versión completa de SQL Server, cuenta de servicio de hello es hello DBO de la base de datos de hello creado para el motor de sincronización de Hola. servicio de Hello no funcionará según lo previsto con ningún otro permiso. También se crea un inicio de sesión SQL.

cuenta de Hello también se concede permisos toofiles, las claves del registro y otro motor de sincronización de objetos relacionados toohello.

### <a name="azure-ad-service-account"></a>Cuenta de servicio de Azure AD
Se crea una cuenta de Azure AD para su uso del servicio de sincronización de Hola. Esta cuenta se puede identificar por su nombre para mostrar.

![Cuenta de AD](./media/active-directory-aadconnect-accounts-permissions/aadsyncserviceaccount.png)

Hola nombre de cuenta de hello servidor Hola se usa en puede identificarse en la segunda parte del nombre de usuario de Hola de Hola. En la imagen de hello, el nombre del servidor de hello es FABRIKAMCON. Si tiene servidores de ensayo, cada servidor tiene su propia cuenta.

cuenta de servicio de Hola se crea con una contraseña larga compleja que no expire. Se ha concedido un rol especial **cuentas de sincronización de Directory** que solo tiene permisos tooperform directory sincronización tareas. No se puede conceder este rol integrado especial fuera de Asistente de Azure AD Connect de Hola. portal de Azure Hello muestra esta cuenta con la función hello **usuario**.

Hay un límite de 20 cuentas de servicio de sincronización en Azure AD. lista de hello tooget existentes Azure AD de cuentas de servicio en Azure AD, ejecute hello siguiente cmdlet de PowerShell de Azure AD:`Get-AzureADDirectoryRole | where {$_.DisplayName -eq "Directory Synchronization Accounts"} | Get-AzureADDirectoryRoleMember`

tooremove sin usar cuentas de servicio de Azure AD, ejecute hello siguiente cmdlet de PowerShell de Azure AD:`Remove-AzureADUser -ObjectId <ObjectId-of-the-account-you-wish-to-remove>`

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](../active-directory-aadconnect.md).
