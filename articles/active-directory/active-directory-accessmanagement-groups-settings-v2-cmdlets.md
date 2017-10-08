---
title: "ejemplos de aaaPowerShell para la administración de grupos en Active Directory de Azure | Documentos de Microsoft"
description: "Esta página proporciona PowerShell ejemplos toohelp administrar grupos en Azure Active Directory"
keywords: "Azure AD, Azure Active Directory, PowerShell, grupos, administración de grupos"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7a5023dc-2727-4c25-8254-b531fc3244ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: ba049babc436e99a290f20899b3a87bcfa811d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a>Cmdlets de la versión 2 de Azure Active Directory para la administración de grupos
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-groups-create-azure-portal.md)
> * [Portal de Azure clásico](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Este artículo contiene ejemplos de cómo toouse PowerShell toomanage los grupos en Azure Active Directory (Azure AD).  También indica cómo tooget configurado con el módulo de PowerShell de Azure AD Hola. En primer lugar, debe [descargar el módulo de PowerShell de Azure AD hello](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="installing-hello-azure-ad-powershell-module"></a>Instalando el módulo de PowerShell de Azure AD Hola
Hola tooinstall módulo de PowerShell de Azure AD, utilice Hola siguientes comandos:

    PS C:\Windows\system32> install-module azuread

se instaló tooverify que Hola módulo, use Hola siguiente comando:

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

Ahora puede empezar a usar cmdlets de hello en el módulo de Hola. Para obtener una descripción completa de cmdlets de hello en el módulo de hello Azure AD, consulte documentación de referencia en línea toohello [Azure Active Directory PowerShell versión 2](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="connecting-toohello-directory"></a>Conexión toohello directorio
Antes de poder empezar a administrar grupos mediante los cmdlets de PowerShell de Azure AD, debe conectar el directorio de toohello de sesión de PowerShell que desea toomanage. Usar hello siguiente comando:

    PS C:\Windows\system32> Connect-AzureAD

Hello cmdlet le pide que para hello las credenciales desea toouse tooaccess su directorio. En este ejemplo, estamos utilizando karen@drumkit.onmicrosoft.com tooaccess Hola directorio de demostración. Hello cmdlet devuelve una sesión de hello tooshow de confirmación se ha conectado correctamente tooyour directorio:

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

Ahora puede empezar a usar grupos de toomanage de cmdlets de organización de hello en el directorio.

## <a name="retrieving-groups"></a>Recuperación de grupos
tooretrieve los grupos existentes del directorio que puede usar Hola cmdlet Get-AzureADGroups. tooretrieve todos los grupos en el directorio hello, use el cmdlet de hello sin parámetros:

    PS C:\Windows\system32> get-azureadgroup

Hola cmdlet devuelve todos los grupos en el directorio conectado Hola.

Puede usar hello - objectID parámetro tooretrieve un grupo específico para el que se especifique objectID del grupo de hello:

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

Hola cmdlet devuelve ahora grupo hello cuyo objectID coincide con valor de Hola de parámetro hello especificado:

    DeletionTimeStamp            :
    ObjectId                     : e29bae11-4ac0-450c-bc37-6dae8f3da61b
    ObjectType                   : Group
    Description                  :
    DirSyncEnabled               :
    DisplayName                  : Pacific NW Support
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 9bb4139b-60a1-434a-8c0d-7c1f8eee2df9
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

Puede buscar un grupo específico mediante Hola - parámetro filter. Este parámetro toma una cláusula de filtro ODATA y devuelve todos los grupos que coinciden con el filtro de hello, como en el siguiente ejemplo de Hola:

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

> [!NOTE] 
> Hola AzureAD PowerShell cmdlets implementar Hola estándar de consulta de OData. Para obtener más información, consulte **$filter** en [opciones de consulta de sistema de OData con el extremo de OData de hello](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).

## <a name="creating-groups"></a>Creación de grupos
toocreate un nuevo grupo en el directorio, use el cmdlet New-AzureADGroup Hola. Este cmdlet crea un nuevo grupo de seguridad llamado "Marketing":

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a>Actualización de grupos
tooupdate un grupo existente, use el cmdlet de hello AzureADGroup del conjunto. En este ejemplo, estamos cambiando Hola propiedad DisplayName del grupo de Hola "Administradores de Intune". En primer lugar, estamos encontrando grupo hello mediante el cmdlet Get-AzureADGroup de Hola y de filtro mediante el atributo DisplayName de hello:

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

A continuación, vamos a cambiar Hola descripción toohello nuevo valor de la propiedad "Administradores de dispositivos de Intune":

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

Ahora si encontramos nuevo grupo de hello, vemos que la propiedad Description de hello es tooreflect actualizada Hola nuevo valor:

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Device Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

## <a name="deleting-groups"></a>Eliminación de grupos
grupos de toodelete desde el directorio, use el cmdlet Remove-AzureADGroup de hello como sigue:

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a>Administración de miembros de grupos
Si necesita tooadd nuevos miembros tooa grupo, usar el cmdlet de hello AzureADGroupMember agregar. Este comando agrega un grupo de administradores de Intune de toohello de miembro que se utiliza en el ejemplo de Hola anterior:

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

parámetro - ObjectId Hello es hello ObjectID de hello grupo toowhich queremos tooadd miembro y - RefObjectId hello es hello ObjectID del usuario de hello queremos tooadd como un grupo de toohello de miembro.

miembros existentes de hello tooget de un grupo, use el cmdlet Get-AzureADGroupMember de hello, como en este ejemplo:

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

miembro de hello tooremove previamente agregamos toohello grupo, use el cmdlet Remove-AzureADGroupMember hello, tal y como se muestra aquí:

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

tooverify Hola la cuenta de grupo de un usuario, use el cmdlet de Select AzureADGroupIdsUserIsMemberOf de Hola. Este cmdlet toma como sus parámetros Hola ObjectId del usuario de hello las pertenencias a grupos de hello toocheck y una lista de grupos de para qué pertenencias a grupos de toocheck Hola. lista de Hola de grupos debe ser proporcionado en forma de Hola de una variable de complejo de tipo "Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck", por lo que primero debemos creamos una variable con ese tipo:

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

A continuación, se proporcionan valores de hello groupIds toocheck en atributo Hola "GroupIds" de esta variable complejo:

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

Ahora, si lo deseamos pertenencias a grupos de toocheck Hola de un usuario con ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea con los grupos de hello en $g, debemos usar:

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


valor de Hello devuelto es una lista de grupos de los cuales este usuario es miembro. También puede aplicar este toocheck método pertenencia contactos, grupos o entidades de servicio para una determinada lista de grupos, mediante Select-AzureADGroupIdsContactIsMemberOf, seleccione AzureADGroupIdsGroupIsMemberOf o Seleccione AzureADGroupIdsServicePrincipalIsMemberOf

## <a name="managing-owners-of-groups"></a>Administración de propietarios de grupos
grupo tooa tooadd propietarios, use el cmdlet de hello AzureADGroupOwner agregar:

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

parámetro - ObjectId Hello es hello ObjectID de hello grupo toowhich queremos tooadd un propietario y - RefObjectId hello es hello ObjectID del usuario de hello queremos tooadd como propietario del grupo de Hola.

los propietarios de hello tooretrieve de un grupo, utilice cmdlet Get-AzureADGroupOwner de hello:

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

Hola cmdlet devuelve la lista de Hola de propietarios del grupo especificado de hello:

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

Si desea tooremove un propietario de un grupo, utilice cmdlet Remove-AzureADGroupOwner de hello:

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a>Alias reservados 
Cuando se crea un grupo, determinados extremos permiten Hola usuario final toospecify un toobe mailNickname o alias que se usa como parte de la dirección de correo electrónico de saludo del grupo de Hola. Solo se pueden crear grupos con hello siguiendo el alias de correo electrónico con privilegios elevados por un administrador global de Azure AD. 
  
* abuse 
* admin 
* administrator 
* hostmaster 
* majordomo 
* postmaster 
* root 
* secure 
* security 
* ssl-admin 
* webmaster 

## <a name="next-steps"></a>Pasos siguientes
Puede encontrar más documentación de Azure Active Directory PowerShell en el artículo sobre los [cmdlets de Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).

* [Administrar acceso tooresources con grupos de Active Directory de Azure](active-directory-manage-groups.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
