---
title: "configuración del grupo aaaConfigure mediante cmdlets de Azure Active Directory | Documentos de Microsoft"
description: "Cómo administrar la configuración de Hola para grupos mediante cmdlets de Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 9f2090e6-3af4-4f07-bbb2-1d18dae89b73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro;
ms.openlocfilehash: 46db49d9dec3eaa41c97ca74c57854189eddc16d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a>Cmdlets de Azure Active Directory para configurar las opciones de grupo

> [!IMPORTANT]
> Este contenido aplica solo tooOffice 365 grupos. Para obtener más información sobre cómo establecer grupos de seguridad de tooallow usuarios toocreate, `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` tal y como se describe en [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0). 

Los grupos de Office 365 se configuran mediante un objeto Settings y un objeto SettingsTemplate. Inicialmente, no verá los objetos de configuración en el directorio, porque el directorio está configurado con la configuración predeterminada de Hola. configuración predeterminada de toochange hello, debe crear un nuevo objeto de configuración utilizando una plantilla de configuración. Las plantillas de configuración las define Microsoft. Hay varias plantillas de configuración diferentes. configuración del grupo tooconfigure Office 365 para el directorio, use plantilla Hola denominado "Group.Unified". configuración del grupo tooconfigure Office 365 en un único grupo, use plantilla Hola denominado "Group.Unified.Guest". Esta plantilla es grupo de toomanage usado invitado acceso tooan Office 365. 

cmdlets de Hello forman parte del módulo de hello Azure Active Directory PowerShell V2. Para obtener instrucciones cómo toodownload e install Hola module en el equipo, vea el artículo de hello [Azure Active Directory PowerShell versión 2](https://docs.microsoft.com/powershell/azuread/). Puede instalar Hola 2 versión del módulo de Hola de [Galería de PowerShell de hello](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="retrieve-a-specific-settings-value"></a>Recuperación de un valor de configuración específico
Si conoce el nombre de Hola de hello configuración desea tooretrieve, puede utilizar Hola por debajo del valor actual de la configuración de cmdlet tooretrieve Hola. En este ejemplo, estamos recuperando Hola valor denominado "UsageGuidelinesUrl." Puede obtener información adicional sobre la configuración de directorio y sus nombres en este artículo.

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a>Crear configuraciones en el nivel del directorio de Hola
Estos pasos crean configuración en el nivel de directorio, que se aplican tooall Office 365 (grupos unificado) en el directorio de Hola.

1. Hola DirectorySettings cmdlets, debe especificar Id. de Hola de hello SettingsTemplate desea toouse. Si no sabe este Id., este cmdlet devuelve la lista de Hola de todas las plantillas de configuración:
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  Esta llamada al cmdlet devuelve todas las plantillas que están disponibles:
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define hello different settings that can be used for hello associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. tooadd una dirección URL de instrucciones de uso, primero necesitará tooget hello SettingsTemplate objeto que define el valor de dirección URL de directrices de uso de hello; es decir, Hola Group.Unified plantilla:
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. A continuación, cree un nuevo objeto de configuración basado en esa plantilla:
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. A continuación, actualice el valor de directrices de uso de hello:
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. Por último, aplicar la configuración de hello:
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

Tras completarse correctamente, Hola cmdlet devuelve Id. de Hola de nuevo el objeto de configuración de hello:
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
Estos son valores de hello definidos en hello Group.Unified SettingsTemplate.

| **Configuración** | **Descripción** |
| --- | --- |
|  <ul><li>EnableGroupCreation<li>Tipo: Boolean<li>Valor predeterminado: True. |marca de Hola que indica si se permite la creación de grupos unificada en directorio Hola. |
|  <ul><li>GroupCreationAllowedGroupId<li>Tipo: String<li>Valor predeterminado: “” |GUID del grupo de seguridad de Hola para qué hello los miembros pueden grupos unificados de toocreate incluso cuando EnableGroupCreation == false. |
|  <ul><li>UsageGuidelinesUrl<li>Tipo: String<li>Valor predeterminado: “” |Un grupo de instrucciones de uso de vínculo toohello. |
|  <ul><li>ClassificationDescriptions<li>Tipo: String<li>Valor predeterminado: “” | Una lista delimitada por comas de las descripciones de clasificación. |
|  <ul><li>DefaultClassification<li>Tipo: String<li>Valor predeterminado: “” | clasificación de Hola que sea toobe utilizado como clasificación de hello predeterminada para un grupo si se ha especificado ninguno.|
|  <ul><li>PrefixSuffixNamingRequirement<li>Tipo: String<li>Valor predeterminado: “” |Todavía no implementado
|  <ul><li>AllowGuestsToBeGroupOwner<li>Tipo: Boolean<li>Valor predeterminado: False. | Valor booleano que indica si un usuario invitado puede ser o no un propietario de grupos. |
|  <ul><li>AllowGuestsToAccessGroups<li>Tipo: Boolean<li>Valor predeterminado: True. | Valor booleano que indica si un usuario invitado puede tener contenido de los grupos del tooUnified de acceso. |
|  <ul><li>GuestUsageGuidelinesUrl<li>Tipo: String<li>Valor predeterminado: “” | dirección url de Hello un vínculo toohello invitado de instrucciones de uso. |
|  <ul><li>AllowToAddGuests<li>Tipo: Boolean<li>Valor predeterminado: True. | Un valor booleano que indica si no se permite tooadd invitados de directorio toothis.|
|  <ul><li>ClassificationList<li>Tipo: String<li>Valor predeterminado: “” |Una lista delimitada por comas de los valores de clasificación válido que pueden ser grupos tooUnified aplicada. |
|  <ul><li>EnableGroupCreation<li>Tipo: Boolean<li>Valor predeterminado: True. | Un valor booleano que indica si los usuarios no administradores pueden crear o no nuevos grupos unificados. |


## <a name="read-settings-at-hello-directory-level"></a>Leer los valores en el nivel del directorio de Hola
Estos pasos leen los valores en el nivel de directorio, que se aplican los grupos de Office tooall en el directorio de Hola.

1. Lea toda la configuración de directorio existente:
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  Este cmdlet devuelve la lista de las opciones de configuración del directorio:
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. Lea toda la configuración de un grupo específico:
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. Lea todos los valores de configuración de directorio de un objeto de configuración del directorio específico, con el GUID de identificador de configuración:
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  Este cmdlet devuelve Hola nombres y valores de este objeto de configuración para este grupo en particular:
  ```
  Name                          Value
  ----                          -----
  ClassificationDescriptions
  DefaultClassification
  PrefixSuffixNamingRequirement
  AllowGuestsToBeGroupOwner     False 
  AllowGuestsToAccessGroups     True
  GuestUsageGuidelinesUrl
  GroupCreationAllowedGroupId
  AllowToAddGuests              True
  UsageGuidelinesUrl            <https://guideline.com>
  ClassificationList
  EnableGroupCreation           True
  ```

## <a name="update-settings-for-a-specific-group"></a>Actualización de la configuración de un grupo específico

1. Busque la plantilla de configuración de hello denominada "Groups.Unified.Guest"
  ```
  Get-AzureADDirectorySettingTemplate
  
  Id                                   DisplayName            Description
  --                                   -----------            -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified          ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest    Settings for a specific Unified Group
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application            ...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule Settings ...
  ```
2. Recuperar el objeto de plantilla de hello para la plantilla de Hola Groups.Unified.Guest:
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. Crear un nuevo objeto de configuración de plantilla de hello:
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. Establecer toohello requerido el valor de hello:
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. Crear nueva configuración de Hola para grupo necesario hello en el directorio de hello:
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a>Actualizar la configuración en el nivel del directorio de Hola

Estos pasos actualización la configuración en el nivel de directorio, que se aplican tooall unificado grupos en el directorio de Hola. En estos ejemplos se asume que ya hay un objeto de configuración en el directorio.

1. Busque el objeto de configuración existente de hello:
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. Valor de Hola de actualización:
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. Actualización del valor de hello:
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a>Quite la configuración en el nivel del directorio de Hola
Este paso quita la configuración en el nivel de directorio, que se aplican los grupos de Office tooall en el directorio de Hola.
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a>Referencia de sintaxis de cmdlet
Puede encontrar más documentación de Azure Active Directory PowerShell en el artículo sobre los [cmdlets de Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="additional-reading"></a>Lecturas adicionales

* [Administrar acceso tooresources con grupos de Active Directory de Azure](active-directory-manage-groups.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
