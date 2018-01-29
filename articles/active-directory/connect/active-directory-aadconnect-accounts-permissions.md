---
title: Cuentas y permisos de Azure AD Connect | Microsoft Docs
description: "En este tema se describen las cuentas usadas y creadas, así como los permisos necesarios."
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
editor: 
ms.reviewer: cychua
ms.assetid: b93e595b-354a-479d-85ec-a95553dd9cc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2017
ms.author: billmath
ms.openlocfilehash: cde406bd745fe61757eaa69c9fc0cfc98a42d205
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2017
---
# <a name="azure-ad-connect-accounts-and-permissions"></a>Azure AD Connect: cuentas y permisos
El asistente para instalación de Azure AD Connect ofrece dos itinerarios diferentes:

* En la Configuración rápida, el asistente necesita más privilegios.  Esto es para que pueda establecer la configuración con facilidad, sin necesidad de crear usuarios ni de configurar permisos.
* En la Configuración personalizada, el asistente ofrece más opciones. Sin embargo, existen algunas situaciones en que debe asegurarse de que tiene los permisos correctos.

## <a name="related-documentation"></a>documentación relacionada
Si no leyó la documentación que se encuentra en [Integración de las identidades locales con Azure Active Directory](../active-directory-aadconnect.md), en la tabla siguiente se proporcionan vínculos a temas relacionados.

|Tema. |Vínculo|  
| --- | --- |
|Descarga de Azure AD Connect | [Descarga de Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Instalación mediante configuración rápida | [Instalación rápida de Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|Instalación mediante configuración personalizada | [Instalación personalizada de Azure AD Connect](./active-directory-aadconnect-get-started-custom.md)|
|Actualización desde DirSync | [Actualización desde la herramienta de sincronización de Azure AD (DirSync)](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Después de la instalación | [Comprobación de la instalación y asignación de licencias ](active-directory-aadconnect-whats-next.md)|

## <a name="express-settings-installation"></a>Instalación de la configuración rápida
En la Configuración rápida, el Asistente para instalación solicita las credenciales de administrador de organización de AD DS.  Esto es para que se pueda configurar el entorno local de Active Directory con los permisos necesarios para Azure AD Connect. Si va a actualizar desde DirSync, las credenciales de administradores de organización de AD DS se usan para restablecer la contraseña de la cuenta utilizada por DirSync. También necesitará credenciales de administrador global de Azure AD.

| Página del asistente | Credenciales recopiladas | Permisos necesarios | Se usa para |
| --- | --- | --- | --- |
| N/D |Usuario que ejecuta el asistente para instalación |Administrador del servidor local |<li>Crea la cuenta local que se usa como [cuenta de servicio de motor de sincronización](#azure-ad-connect-sync-service-account). |
| Conectarse a Azure |Credenciales de directorio de Azure AD |Rol de administrador global en Azure AD |<li>Habilitación de la sincronización en el directorio de Azure AD</li>  <li>Creación de la [cuenta de Azure AD](#azure-ad-service-account) que se usa para operaciones de sincronización continua en Azure AD.</li> |
| Conectarse a AD DS |Credenciales de Active Directory local |Miembro del grupo de administradores de empresa (EA) en Active Directory |<li>Crea un [cuenta](#active-directory-account) en Active Directory y concede permisos en ella. Esta cuenta creada se usa para leer y escribir información de directorio durante la sincronización.</li> |

### <a name="enterprise-admin-credentials"></a>Credenciales de administrador de organización
Estas credenciales solo se usan durante la instalación y no se usan una vez completada la misma. El administrador de empresa, y no el del dominio, debe asegurarse de que se pueden establecer los permisos de Active Directory en todos los dominios.

### <a name="global-admin-credentials"></a>Credenciales de administrador global
Estas credenciales solo se usan durante la instalación y no se usan una vez completada la misma. Se utiliza para crear la [cuenta de Azure AD](#azure-ad-service-account) usada para sincronizar cambios en Azure AD. La cuenta también habilita la sincronización como una característica de Azure AD.

### <a name="permissions-for-the-created-ad-ds-account-for-express-settings"></a>Permisos de la cuenta de AD DS creada para la configuración rápida
Cuando se cree la [cuenta](#active-directory-account) para leer y escribir en AD DS con la configuración rápida, tendrá los permisos siguientes:

| Permiso | Usado para |
| --- | --- |
| <li>Replicación de cambios de directorio</li><li>Replicación de todos los cambios de directorio |Sincronización de contraseñas |
| Lectura y escritura de todas las propiedades Usuario |Importación y Exchange híbrido |
| Lectura y escritura de todas las propiedades iNetOrgPerson |Importación y Exchange híbrido |
| Lectura y escritura de todas las propiedades Grupo |Importación y Exchange híbrido |
| Lectura y escritura de todas las propiedades Contacto |Importación y Exchange híbrido |
| Restablecimiento de contraseña |Preparación para habilitar la escritura diferida de contraseñas |

## <a name="custom-settings-installation"></a>Instalación de la configuración personalizada
Azure AD Connect 1.1.524.0 y las versiones posteriores ofrecen la opción para permitir que el asistente de Azure AD Connect cree la cuenta utilizada para conectarse a Active Directory.  Las versiones anteriores requieren que la cuenta se cree antes de la instalación. Los permisos que debe conceder a esta cuenta se pueden encontrar en [Creación de la cuenta de AD DS](#create-the-ad-ds-account). 

| Página del asistente | Credenciales recopiladas | Permisos necesarios | Se usa para |
| --- | --- | --- | --- |
| N/D |Usuario que ejecuta el asistente para instalación |<li>Administrador del servidor local</li><li>Si usa SQL Server completo, el usuario debe ser administrador del sistema (SA) en SQL.</li> |De forma predeterminada, crea la cuenta local que se usa como [cuenta de servicio del motor de sincronización](#azure-ad-connect-sync-service-account). La cuenta solo se crea cuando el administrador no especifica una cuenta determinada. |
| Instalar servicios de sincronización, opción de cuenta de servicio |Credenciales de cuenta de usuario local o de AD |Usuario, el asistente para instalación concede los permisos |Si el administrador especifica una cuenta, esta se usa como cuenta de servicio para el servicio de sincronización. |
| Conectarse a Azure |Credenciales de directorio de Azure AD |Rol de administrador global en Azure AD |<li>Habilitación de la sincronización en el directorio de Azure AD</li>  <li>Creación de la [cuenta de Azure AD](#azure-ad-service-account) que se usa para operaciones de sincronización continua en Azure AD.</li> |
| Conectar sus directorios |Credenciales de Active Directory local para cada bosque que se conecta a Azure AD |Los permisos dependen de qué características permite y se pueden encontrar en [Creación de la cuenta de AD DS](#create-the-ad-ds-account) |Esta cuenta se usa para leer y escribir información de directorio durante la sincronización. |
| Servidores de AD FS |Para cada servidor de la lista, el asistente recopila credenciales cuando las credenciales de inicio de sesión del usuario que ejecuta el asistente no son suficientes para conectarse. |Administrador de dominio |Instalación y configuración del rol de servidor de AD FS. |
| Servidores proxy de aplicación web |Para cada servidor de la lista, el asistente recopila credenciales cuando las credenciales de inicio de sesión del usuario que ejecuta el asistente no son suficientes para conectarse. |Administrador local en la máquina de destino |Instalación y configuración del rol de servidor de WAP. |
| Credenciales de confianza del proxy |Credenciales de confianza del servicio de federación (las credenciales que el proxy usa para inscribirse para obtener un certificado de confianza de FS) |Cuenta de dominio que es un administrador local del servidor de AD FS |Inscripción inicial de certificados de confianza de FS WAP |
| Página de cuenta de servicio de AD FS, "Usar una opción de cuenta de usuario de dominio" |Credenciales de cuenta de usuario de AD |Usuario de dominio |La cuenta de usuario de AD cuyas credenciales se proporcionan se usa como cuenta de inicio de sesión del servicio AD FS. |

### <a name="create-the-ad-ds-account"></a>Creación de la cuenta de AD DS
La cuenta especificada en la página **Conectar sus directorios** debe estar presente en Active Directory antes de la instalación.  También debe tener los permisos necesarios concedidos. El asistente para instalación no comprueba los permisos y los problemas solo se encuentran durante la sincronización.

Los permisos que requiera dependen de las características opcionales que habilite. Si tiene varios dominios, se deben conceder los permisos para todos los dominios del bosque. Si no habilita ninguna de estas características, los permisos **Usuario de dominio** predeterminados son suficientes.

| Característica | Permisos |
| --- | --- |
| característica msDS-ConsistencyGuid |Permisos de escritura para el atributo msDS-ConsistencyGuid documentado en [Conceptos de diseño: Using msDS-ConsistencyGuid as sourceAnchor (Uso de msDS-ConsistencyGuid como sourceAnchor)](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). | 
| Sincronización de contraseñas |<li>Replicación de cambios de directorio</li>  <li>Replicación de todos los cambios de directorio |
| Implementación híbrida de Exchange |Permisos de escritura en los atributos que se documentan en [Escritura diferida híbrida de Exchange](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) para usuarios, grupos y contactos. |
| Carpeta pública de correo de Exchange |Permisos de lectura para los atributos que se documentan en [carpetas públicas de correo electrónico de Exchange](active-directory-aadconnectsync-attributes-synchronized.md#exchange-mail-public-folder) para las carpetas públicas. | 
| Escritura diferida de contraseñas |Permisos de escritura en los atributos que se documentan en [Introducción a la administración de contraseñas](../active-directory-passwords-writeback.md) para los usuarios. |
| Escritura diferida de dispositivos |Los permisos concedidos con un script de PowerShell como se describe en [Escritura diferida de dispositivos](active-directory-aadconnect-feature-device-writeback.md). |
| Escritura diferida de grupos |Objetos de grupo Leer, Crear, Actualizar y Eliminar para **grupos de Office 365** sincronizados.  Para más información, vea [Escritura diferida de grupos](active-directory-aadconnect-feature-preview.md#group-writeback).|

## <a name="upgrade"></a>Actualizar
Al actualizar desde una versión de Azure AD Connect a una nueva versión, necesita los siguientes permisos:

>[!IMPORTANT]
>A partir de la compilación 1.1.484, Azure AD Connect introdujo un error de regresión que requiere permisos de administrador del sistema para actualizar la base de datos SQL.  Este error sigue estando presente en la última compilación 1.1.614.  Si va a actualizar a esta versión, necesitará permisos de administrador del sistema.  Los permisos de dbo no son suficientes.  Si intenta actualizar Azure AD Connect sin tener permisos de administrador del sistema, se producirá un error en la actualización y Azure AD Connect dejará de funcionar correctamente después.  Microsoft conoce este problema y está trabajando para corregir este problema.


| Principal | Permisos necesarios | Se usa para |
| --- | --- | --- |
| Usuario que ejecuta el asistente para instalación |Administrador del servidor local |Archivos binarios de la actualización. |
| Usuario que ejecuta el asistente para instalación |Miembro de ADSyncAdmins |Realice cambios en las reglas de sincronización y en otra configuración. |
| Usuario que ejecuta el asistente para instalación |Si utiliza un servidor SQL completo: DBO (o similar) de la base de datos del motor de sincronización |Realice los cambios de nivel de base de datos, como actualizar tablas con nuevas columnas. |

## <a name="more-about-the-created-accounts"></a>Más información acerca de las cuentas creadas
### <a name="active-directory-account"></a>Cuenta de Active Directory
Si utiliza la configuración rápida, se crea una cuenta en Active Directory que se usa para sincronización. La cuenta creada se ubica en el dominio raíz del bosque en el contenedor Usuarios y su nombre tiene el prefijo **MSOL_**. La cuenta se crea con una contraseña larga compleja que no expira. Si tiene una directiva de contraseñas en el dominio, asegúrese de que se permitan contraseñas largas y complejas para esta cuenta.

![Cuenta de AD](./media/active-directory-aadconnect-accounts-permissions/adsyncserviceaccount.png)

Si usa una configuración personalizada, es responsable de crear la cuenta antes de iniciar la instalación.

### <a name="azure-ad-connect-sync-service-account"></a>Cuenta del servicio Azure AD Connect Sync
El servicio de sincronización puede ejecutarse con diferentes cuentas. Puede ejecutarse con una **cuenta de servicio virtual** (VSA), una **cuenta de servicio administrada de grupo** (gMSA/sMSA), o una cuenta de usuario normal. Las opciones admitidas cambiaron con la versión de abril de 2017 de Connect cuando se realiza una instalación nueva. Si actualiza desde una versión anterior de Azure AD Connect, estas opciones adicionales no están disponibles.

| Tipo de cuenta | Opción de instalación | Descripción |
| --- | --- | --- |
| [Cuenta de servicio virtual](#virtual-service-account) | Rápida y personalizada, abril de 2017 y versiones posteriores | Es la opción utilizada para todas las instalaciones rápidas, excepto para las instalaciones en un controlador de dominio. Para las instalaciones personalizadas, es la opción predeterminada a menos que se use otra opción. |
| [Cuenta de servicio administrada de grupo](#group-managed-service-account) | Personalizada, abril de 2017 y versiones posteriores | Si utiliza un servidor SQL remoto, se recomienda usar una cuenta de servicio administrada de grupo. |
| [Cuenta de usuario](#user-account) | Rápida y personalizada, abril de 2017 y versiones posteriores | Durante la instalación, solo se crea una cuenta de usuario con el prefijo AAD_ cuando se instala en Windows Server 2008 y cuando se instala en un controlador de dominio. |
| [Cuenta de usuario](#user-account) | Rápida y personalizada, marzo de 2017 y versiones anteriores | Se crea una cuenta local con el prefijo AAD_ durante la instalación. Cuando se utiliza la instalación personalizada, se puede especificar otra cuenta. |

Si utiliza Connect con una compilación de marzo de 2017 o anterior, no debe restablecer la contraseña en la cuenta de servicio, ya que Windows destruye las claves de cifrado por motivos de seguridad. No se puede cambiar la cuenta a cualquier otra cuenta sin volver a instalar Azure AD Connect. Si se actualiza a una compilación de abril de 2017 o posterior, es posible cambiar la contraseña de la cuenta de servicio, pero no puede cambiar la cuenta utilizada.

> [!Important]
> Solo se puede establecer la cuenta de servicio en la primera instalación. No es posible cambiar la cuenta de servicio una vez completada la instalación.

Esta es la tabla de los valores predeterminados, recomendados y admitidos para la cuenta del servicio de sincronización.

Leyenda:

- **Negrita** indica la opción predeterminada y, en la mayoría de los casos, la opción recomendada.
- *Cursiva* indica la opción recomendada si no es la opción predeterminada.
- 2008: opción predeterminada cuando se instala en Windows Server 2008
- Sin negrita: opción admitida
- Cuenta local: cuenta de usuario local en el servidor
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

Una VSA está pensada para usarse en escenarios donde el motor de sincronización y SQL están en el mismo servidor. Si usa SQL remoto, se recomienda utilizar una [cuenta de servicio administrada de grupo](#managed-service-account) en su lugar.

Esta característica requiere Windows Server 2008 R2 o versiones posteriores. Si instala Azure AD Connect en Windows Server 2008, la instalación vuelve a utilizar una [cuenta de usuario](#user-account) en su lugar.

#### <a name="group-managed-service-account"></a>Cuenta de servicio administrada de grupo
Si usa un servidor SQL remoto, se recomienda utilizar una **cuenta de servicio administrada de grupo**. Para más información sobre cómo preparar Active Directory para la cuenta de servicio administrada de grupo, consulte [Información general de las cuentas de servicio administradas de grupo](https://technet.microsoft.com/library/hh831782.aspx).

Para usar esta opción, en la página [Instalar los componentes necesarios](active-directory-aadconnect-get-started-custom.md#install-required-components), seleccione **Usar una cuenta de servicio existente** y seleccione **Cuenta de servicio administrada**.  
![VSA](./media/active-directory-aadconnect-accounts-permissions/serviceaccount.png)  
También se puede usar una [cuenta de servicio administrada independiente](https://technet.microsoft.com/library/dd548356.aspx). Sin embargo, solo se pueden utilizar en el equipo local y no hay ningún beneficio al usarlas en lugar de la cuenta de servicio virtual predeterminada.

Esta característica requiere Windows Server 2012 o posterior. Si necesita usar un sistema operativo anterior y usar SQL remoto, debe usar una [cuenta de usuario](#user-account).

#### <a name="user-account"></a>Cuenta de usuario
El asistente para instalación crea una cuenta de servicio local (a menos que especifique la cuenta que se desea usar en la configuración personalizada). La cuenta lleva delante **AAD_** y se usa para el servicio de sincronización real como cuenta de ejecución. Si instala Azure AD Connect en un controlador de dominio, la cuenta se crea en el dominio. La cuenta de servicio **AAD_** debe estar ubicada en el dominio si:
   - Se usa un servidor remoto que ejecuta SQL Server.
   - Se usa a un proxy que requiere autenticación.

![Cuenta de servicio de sincronización](./media/active-directory-aadconnect-accounts-permissions/syncserviceaccount.png)

La cuenta se crea con una contraseña larga compleja que no expira.

Esta se utiliza para almacenar de forma segura las contraseñas de las otras cuentas, que se almacenan cifradas en la base de datos. Las claves privadas de las claves de cifrado se protegen con el cifrado de clave secreta de los servicios criptográficos mediante la API de protección de datos de Windows (DPAPI).

Si usa SQL Server completo, la cuenta de servicio es el DBO de la base de datos creada para el motor de sincronización. El servicio no funcionará como se pretende con ningún otro permiso. También se crea un inicio de sesión SQL.

A la cuenta también se le conceden permisos para archivos, claves del Registro y otros objetos relacionados con el motor de sincronización.

### <a name="azure-ad-service-account"></a>Cuenta de servicio de Azure AD
Se crea una cuenta de Azure AD para el uso del servicio de sincronización. Esta cuenta se puede identificar por su nombre para mostrar.

![Cuenta de AD](./media/active-directory-aadconnect-accounts-permissions/aadsyncserviceaccount.png)

El nombre del servidor en el que se usa la cuenta se puede identificar en la segunda parte del nombre de usuario. En la imagen el nombre del servidor es FABRIKAMCON. Si tiene servidores de ensayo, cada servidor tiene su propia cuenta.

La cuenta de servicio se crea con una contraseña larga compleja que no expira. Se le concede el rol especial **Cuentas de sincronización de directorio** que solo tiene permisos para realizar tareas de sincronización de directorios. No se puede conceder este rol integrado especial fuera del asistente de Azure AD Connect. En Azure Portal se muestra esta cuenta con el rol **Usuario**.

Hay un límite de 20 cuentas de servicio de sincronización en Azure AD. Para obtener la lista de cuentas de servicio de Azure AD existentes en Azure AD, ejecute el siguiente cmdlet de Azure AD PowerShell: `Get-AzureADDirectoryRole | where {$_.DisplayName -eq "Directory Synchronization Accounts"} | Get-AzureADDirectoryRoleMember`

Para quitar las cuentas de servicio de Azure AD sin usar, ejecute el siguiente cmdlet de Azure AD PowerShell: `Remove-AzureADUser -ObjectId <ObjectId-of-the-account-you-wish-to-remove>`

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](../active-directory-aadconnect.md).
