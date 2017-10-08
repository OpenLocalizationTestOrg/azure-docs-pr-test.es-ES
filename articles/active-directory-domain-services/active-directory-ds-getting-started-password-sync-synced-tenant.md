---
title: "Active Directory Domain Services: habilitación de la sincronización de contraseñas | Microsoft Docs"
description: "Introducción a los Servicios de dominio de Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: a7a6ee0f83d3d9bdaf236717efb39155a26934e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Habilitar la sincronización de contraseña tooAzure los servicios de dominio de Active Directory
En las tareas anteriores, habilitó Azure Active Directory Domain Services para su inquilino de Azure Active Directory (Azure AD). tarea siguiente de Hello es tooenable sincronización de hashes de credenciales que requiere para tooAzure de autenticación de NT LAN Manager (NTLM) y Kerberos servicios de dominio de AD. Una vez haya configurado la sincronización de credenciales, los usuarios pueden iniciar sesión toohello dominio administrado con sus credenciales corporativas.

Hola pasos implicados son diferentes para cuentas de usuario de vs de cuentas de usuario solo en la nube que se sincronizan desde su directorio local mediante Azure AD Connect. Si su inquilino de Azure AD tiene una combinación de la nube solo los usuarios y los usuarios de sus instalaciones en AD, necesita tooperform ambos pasos.

<br>

> [!div class="op_single_selector"]
> * **Las cuentas de usuario solo en la nube**: [sincronizar contraseñas para cuentas de usuario solo en la nube dominio administrado tooyour](active-directory-ds-getting-started-password-sync.md)
> * **Las cuentas de usuario local**: [sincronizar contraseñas para cuentas de usuario que se ha sincronizado desde local AD tooyour administrado dominio](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a>Tarea 5: habilitar la sincronización de contraseña tooyour dominio administrado para cuentas de usuario se sincronizan con sus instalaciones en AD
Azure sincronizó un inquilino de AD se establece toosynchronize con el directorio local de su organización mediante Azure AD Connect. De forma predeterminada, Azure AD Connect no sincroniza NTLM y Kerberos tooAzure de hashes de credenciales AD. toouse servicios de dominio de AD de Azure, deberá tooconfigure Azure AD Connect toosynchronize códigos hash de credenciales necesarios para la autenticación NTLM y Kerberos. Hola pasos Habilitar sincronización de hashes de credenciales de hello necesaria del inquilino de Azure AD tooyour directorio local.

> [!NOTE]
> Si su organización tiene cuentas de usuario que se sincronizan desde su directorio local, debe habilitar la sincronización de hash de NTLM y Kerberos en el dominio administrado de orden toouse Hola. Una cuenta de usuario sincronizado es una cuenta que se creó en el directorio local y sincroniza a tooyour inquilino de Azure AD mediante Azure AD Connect.
>
>

### <a name="install-or-update-azure-ad-connect"></a>Instalación o actualización de Azure AD Connect
Instalar hello más reciente recomendada equipo unido a un lanzamiento de Azure AD Connect en un dominio. Si tiene una instancia existente del programa de instalación de Azure AD Connect, necesita tooupdate, versión más reciente de hello toouse de Azure AD Connect. tooavoid conoce problemas o errores que pueden ya se han corregido, asegúrese de usar siempre la versión más reciente de Hola de Azure AD Connect.

**[Descarga de Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**

Versión recomendada: **1.1.553.0**, publicada el 27 de junio de 2017.

> [!WARNING]
> DEBE instalar hello más reciente recomienda versión de inquilino de Azure AD Connect tooenable Hola contraseña heredado credenciales (necesario para la autenticación NTLM y Kerberos) toosynchronize tooyour Azure AD. Esta funcionalidad no está disponible en versiones anteriores de Azure AD Connect o con la herramienta de sincronización de directorios de hello heredado.
>
>

Instrucciones de instalación de Azure AD Connect están disponibles en los siguientes Hola artículo - [Introducción a Azure AD Connect](../active-directory/active-directory-aadconnect.md)

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a>Habilitar la sincronización de NTLM y Kerberos tooAzure de hashes de credenciales AD
Ejecute hello siguiente script de PowerShell en cada bosque de AD, sincronización de contraseñas total tooforce y habilitar a inquilino de todos los usuarios locales credencial hashes toosync tooyour Azure AD. Esta secuencia de comandos permite hashes de credenciales de hello necesarios para el inquilino de tooyour sincronizada Azure AD de toobe de autenticación NTLM o Kerberos.

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

Según el tamaño de hello del directorio (número de usuarios, grupos etc.), la sincronización de credenciales se aplica un algoritmo hash tooAzure AD lleva tiempo. las contraseñas de Hola se podrán usar en el dominio administrado de los servicios de dominio de AD de Azure de hello poco después de que han sincronizado hashes de credenciales de hello tooAzure AD.

<br>

## <a name="related-content"></a>Contenido relacionado
* [Habilitar la sincronización de contraseña tooAAD los servicios de dominio de un solo en la nube Azure directorio de AD](active-directory-ds-getting-started-password-sync.md)
* [Administración de un dominio administrado con Servicios de dominio de Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Unirse a un dominio administrado de Windows máquina virtual tooan servicios de dominio de AD de Azure](active-directory-ds-admin-guide-join-windows-vm.md)
* [Unirse a un dominio administrado de Red Hat Enterprise Linux máquina virtual tooan servicios de dominio de AD de Azure](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
