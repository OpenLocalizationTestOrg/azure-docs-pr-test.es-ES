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
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="e8356-103">Cmdlets de Azure Active Directory para configurar las opciones de grupo</span><span class="sxs-lookup"><span data-stu-id="e8356-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8356-104">Este contenido aplica solo tooOffice 365 grupos.</span><span class="sxs-lookup"><span data-stu-id="e8356-104">This content applies only tooOffice 365 groups.</span></span> <span data-ttu-id="e8356-105">Para obtener más información sobre cómo establecer grupos de seguridad de tooallow usuarios toocreate, `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` tal y como se describe en [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="e8356-105">For more information on how tooallow users toocreate Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="e8356-106">Los grupos de Office 365 se configuran mediante un objeto Settings y un objeto SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="e8356-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="e8356-107">Inicialmente, no verá los objetos de configuración en el directorio, porque el directorio está configurado con la configuración predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8356-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with hello default settings.</span></span> <span data-ttu-id="e8356-108">configuración predeterminada de toochange hello, debe crear un nuevo objeto de configuración utilizando una plantilla de configuración.</span><span class="sxs-lookup"><span data-stu-id="e8356-108">toochange hello default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="e8356-109">Las plantillas de configuración las define Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e8356-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="e8356-110">Hay varias plantillas de configuración diferentes.</span><span class="sxs-lookup"><span data-stu-id="e8356-110">There are several different settings templates.</span></span> <span data-ttu-id="e8356-111">configuración del grupo tooconfigure Office 365 para el directorio, use plantilla Hola denominado "Group.Unified".</span><span class="sxs-lookup"><span data-stu-id="e8356-111">tooconfigure Office 365 group settings for your directory, you use hello template named "Group.Unified".</span></span> <span data-ttu-id="e8356-112">configuración del grupo tooconfigure Office 365 en un único grupo, use plantilla Hola denominado "Group.Unified.Guest".</span><span class="sxs-lookup"><span data-stu-id="e8356-112">tooconfigure Office 365 group settings on a single group, use hello template named "Group.Unified.Guest".</span></span> <span data-ttu-id="e8356-113">Esta plantilla es grupo de toomanage usado invitado acceso tooan Office 365.</span><span class="sxs-lookup"><span data-stu-id="e8356-113">This template is used toomanage guest access tooan Office 365 group.</span></span> 

<span data-ttu-id="e8356-114">cmdlets de Hello forman parte del módulo de hello Azure Active Directory PowerShell V2.</span><span class="sxs-lookup"><span data-stu-id="e8356-114">hello cmdlets are part of hello Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="e8356-115">Para obtener instrucciones cómo toodownload e install Hola module en el equipo, vea el artículo de hello [Azure Active Directory PowerShell versión 2](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="e8356-115">For instructions how toodownload and install hello module on your computer, see hello article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="e8356-116">Puede instalar Hola 2 versión del módulo de Hola de [Galería de PowerShell de hello](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="e8356-116">You can install hello version 2 release of hello module from [hello PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="e8356-117">Recuperación de un valor de configuración específico</span><span class="sxs-lookup"><span data-stu-id="e8356-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="e8356-118">Si conoce el nombre de Hola de hello configuración desea tooretrieve, puede utilizar Hola por debajo del valor actual de la configuración de cmdlet tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="e8356-118">If you know hello name of hello setting you want tooretrieve, you can use hello below cmdlet tooretrieve hello current settings value.</span></span> <span data-ttu-id="e8356-119">En este ejemplo, estamos recuperando Hola valor denominado "UsageGuidelinesUrl."</span><span class="sxs-lookup"><span data-stu-id="e8356-119">In this example, we're retrieving hello value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="e8356-120">Puede obtener información adicional sobre la configuración de directorio y sus nombres en este artículo.</span><span class="sxs-lookup"><span data-stu-id="e8356-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a><span data-ttu-id="e8356-121">Crear configuraciones en el nivel del directorio de Hola</span><span class="sxs-lookup"><span data-stu-id="e8356-121">Create settings at hello directory level</span></span>
<span data-ttu-id="e8356-122">Estos pasos crean configuración en el nivel de directorio, que se aplican tooall Office 365 (grupos unificado) en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8356-122">These steps create settings at directory level, which apply tooall Office 365 groups (Unified groups) in hello directory.</span></span>

1. <span data-ttu-id="e8356-123">Hola DirectorySettings cmdlets, debe especificar Id. de Hola de hello SettingsTemplate desea toouse.</span><span class="sxs-lookup"><span data-stu-id="e8356-123">In hello DirectorySettings cmdlets, you must specify hello ID of hello SettingsTemplate you want toouse.</span></span> <span data-ttu-id="e8356-124">Si no sabe este Id., este cmdlet devuelve la lista de Hola de todas las plantillas de configuración:</span><span class="sxs-lookup"><span data-stu-id="e8356-124">If you do not know this ID, this cmdlet returns hello list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="e8356-125">Esta llamada al cmdlet devuelve todas las plantillas que están disponibles:</span><span class="sxs-lookup"><span data-stu-id="e8356-125">This cmdlet call returns all templates that are available:</span></span>
  
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
2. <span data-ttu-id="e8356-126">tooadd una dirección URL de instrucciones de uso, primero necesitará tooget hello SettingsTemplate objeto que define el valor de dirección URL de directrices de uso de hello; es decir, Hola Group.Unified plantilla:</span><span class="sxs-lookup"><span data-stu-id="e8356-126">tooadd a usage guideline URL, first you need tooget hello SettingsTemplate object that defines hello usage guideline URL value; that is, hello Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="e8356-127">A continuación, cree un nuevo objeto de configuración basado en esa plantilla:</span><span class="sxs-lookup"><span data-stu-id="e8356-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="e8356-128">A continuación, actualice el valor de directrices de uso de hello:</span><span class="sxs-lookup"><span data-stu-id="e8356-128">Then update hello usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="e8356-129">Por último, aplicar la configuración de hello:</span><span class="sxs-lookup"><span data-stu-id="e8356-129">Finally, apply hello settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="e8356-130">Tras completarse correctamente, Hola cmdlet devuelve Id. de Hola de nuevo el objeto de configuración de hello:</span><span class="sxs-lookup"><span data-stu-id="e8356-130">Upon successful completion, hello cmdlet returns hello ID of hello new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="e8356-131">Estos son valores de hello definidos en hello Group.Unified SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="e8356-131">Here are hello settings defined in hello Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="e8356-132">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="e8356-132">**Setting**</span></span> | <span data-ttu-id="e8356-133">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="e8356-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="e8356-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="e8356-134">EnableGroupCreation</span></span><li><span data-ttu-id="e8356-135">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="e8356-135">Type: Boolean</span></span><li><span data-ttu-id="e8356-136">Valor predeterminado: True.</span><span class="sxs-lookup"><span data-stu-id="e8356-136">Default: True</span></span> |<span data-ttu-id="e8356-137">marca de Hola que indica si se permite la creación de grupos unificada en directorio Hola.</span><span class="sxs-lookup"><span data-stu-id="e8356-137">hello flag indicating whether Unified Group creation is allowed in hello directory.</span></span> |
|  <ul><li><span data-ttu-id="e8356-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="e8356-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="e8356-139">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="e8356-139">Type: String</span></span><li><span data-ttu-id="e8356-140">Valor predeterminado: “”</span><span class="sxs-lookup"><span data-stu-id="e8356-140">Default: “”</span></span> |<span data-ttu-id="e8356-141">GUID del grupo de seguridad de Hola para qué hello los miembros pueden grupos unificados de toocreate incluso cuando EnableGroupCreation == false.</span><span class="sxs-lookup"><span data-stu-id="e8356-141">GUID of hello security group for which hello members are allowed toocreate Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="e8356-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="e8356-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="e8356-143">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="e8356-143">Type: String</span></span><li><span data-ttu-id="e8356-144">Valor predeterminado: “”</span><span class="sxs-lookup"><span data-stu-id="e8356-144">Default: “”</span></span> |<span data-ttu-id="e8356-145">Un grupo de instrucciones de uso de vínculo toohello.</span><span class="sxs-lookup"><span data-stu-id="e8356-145">A link toohello Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="e8356-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="e8356-146">ClassificationDescriptions</span></span><li><span data-ttu-id="e8356-147">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="e8356-147">Type: String</span></span><li><span data-ttu-id="e8356-148">Valor predeterminado: “”</span><span class="sxs-lookup"><span data-stu-id="e8356-148">Default: “”</span></span> | <span data-ttu-id="e8356-149">Una lista delimitada por comas de las descripciones de clasificación.</span><span class="sxs-lookup"><span data-stu-id="e8356-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="e8356-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="e8356-150">DefaultClassification</span></span><li><span data-ttu-id="e8356-151">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="e8356-151">Type: String</span></span><li><span data-ttu-id="e8356-152">Valor predeterminado: “”</span><span class="sxs-lookup"><span data-stu-id="e8356-152">Default: “”</span></span> | <span data-ttu-id="e8356-153">clasificación de Hola que sea toobe utilizado como clasificación de hello predeterminada para un grupo si se ha especificado ninguno.</span><span class="sxs-lookup"><span data-stu-id="e8356-153">hello classification that is toobe used as hello default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="e8356-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="e8356-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="e8356-155">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="e8356-155">Type: String</span></span><li><span data-ttu-id="e8356-156">Valor predeterminado: “”</span><span class="sxs-lookup"><span data-stu-id="e8356-156">Default: “”</span></span> |<span data-ttu-id="e8356-157">Todavía no implementado</span><span class="sxs-lookup"><span data-stu-id="e8356-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="e8356-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="e8356-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="e8356-159">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="e8356-159">Type: Boolean</span></span><li><span data-ttu-id="e8356-160">Valor predeterminado: False.</span><span class="sxs-lookup"><span data-stu-id="e8356-160">Default: False</span></span> | <span data-ttu-id="e8356-161">Valor booleano que indica si un usuario invitado puede ser o no un propietario de grupos.</span><span class="sxs-lookup"><span data-stu-id="e8356-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="e8356-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="e8356-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="e8356-163">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="e8356-163">Type: Boolean</span></span><li><span data-ttu-id="e8356-164">Valor predeterminado: True.</span><span class="sxs-lookup"><span data-stu-id="e8356-164">Default: True</span></span> | <span data-ttu-id="e8356-165">Valor booleano que indica si un usuario invitado puede tener contenido de los grupos del tooUnified de acceso.</span><span class="sxs-lookup"><span data-stu-id="e8356-165">Boolean indicating whether or not a guest user can have access tooUnified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="e8356-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="e8356-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="e8356-167">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="e8356-167">Type: String</span></span><li><span data-ttu-id="e8356-168">Valor predeterminado: “”</span><span class="sxs-lookup"><span data-stu-id="e8356-168">Default: “”</span></span> | <span data-ttu-id="e8356-169">dirección url de Hello un vínculo toohello invitado de instrucciones de uso.</span><span class="sxs-lookup"><span data-stu-id="e8356-169">hello url of a link toohello guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="e8356-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="e8356-170">AllowToAddGuests</span></span><li><span data-ttu-id="e8356-171">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="e8356-171">Type: Boolean</span></span><li><span data-ttu-id="e8356-172">Valor predeterminado: True.</span><span class="sxs-lookup"><span data-stu-id="e8356-172">Default: True</span></span> | <span data-ttu-id="e8356-173">Un valor booleano que indica si no se permite tooadd invitados de directorio toothis.</span><span class="sxs-lookup"><span data-stu-id="e8356-173">A boolean indicating whether or not is allowed tooadd guests toothis directory.</span></span>|
|  <ul><li><span data-ttu-id="e8356-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="e8356-174">ClassificationList</span></span><li><span data-ttu-id="e8356-175">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="e8356-175">Type: String</span></span><li><span data-ttu-id="e8356-176">Valor predeterminado: “”</span><span class="sxs-lookup"><span data-stu-id="e8356-176">Default: “”</span></span> |<span data-ttu-id="e8356-177">Una lista delimitada por comas de los valores de clasificación válido que pueden ser grupos tooUnified aplicada.</span><span class="sxs-lookup"><span data-stu-id="e8356-177">A comma-delimited list of valid classification values that can be applied tooUnified Groups.</span></span> |
|  <ul><li><span data-ttu-id="e8356-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="e8356-178">EnableGroupCreation</span></span><li><span data-ttu-id="e8356-179">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="e8356-179">Type: Boolean</span></span><li><span data-ttu-id="e8356-180">Valor predeterminado: True.</span><span class="sxs-lookup"><span data-stu-id="e8356-180">Default: True</span></span> | <span data-ttu-id="e8356-181">Un valor booleano que indica si los usuarios no administradores pueden crear o no nuevos grupos unificados.</span><span class="sxs-lookup"><span data-stu-id="e8356-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-hello-directory-level"></a><span data-ttu-id="e8356-182">Leer los valores en el nivel del directorio de Hola</span><span class="sxs-lookup"><span data-stu-id="e8356-182">Read settings at hello directory level</span></span>
<span data-ttu-id="e8356-183">Estos pasos leen los valores en el nivel de directorio, que se aplican los grupos de Office tooall en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8356-183">These steps read settings at directory level, which apply tooall Office groups in hello directory.</span></span>

1. <span data-ttu-id="e8356-184">Lea toda la configuración de directorio existente:</span><span class="sxs-lookup"><span data-stu-id="e8356-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="e8356-185">Este cmdlet devuelve la lista de las opciones de configuración del directorio:</span><span class="sxs-lookup"><span data-stu-id="e8356-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="e8356-186">Lea toda la configuración de un grupo específico:</span><span class="sxs-lookup"><span data-stu-id="e8356-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="e8356-187">Lea todos los valores de configuración de directorio de un objeto de configuración del directorio específico, con el GUID de identificador de configuración:</span><span class="sxs-lookup"><span data-stu-id="e8356-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="e8356-188">Este cmdlet devuelve Hola nombres y valores de este objeto de configuración para este grupo en particular:</span><span class="sxs-lookup"><span data-stu-id="e8356-188">This cmdlet returns hello names and values in this settings object for this specific group:</span></span>
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

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="e8356-189">Actualización de la configuración de un grupo específico</span><span class="sxs-lookup"><span data-stu-id="e8356-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="e8356-190">Busque la plantilla de configuración de hello denominada "Groups.Unified.Guest"</span><span class="sxs-lookup"><span data-stu-id="e8356-190">Search for hello settings template named "Groups.Unified.Guest"</span></span>
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
2. <span data-ttu-id="e8356-191">Recuperar el objeto de plantilla de hello para la plantilla de Hola Groups.Unified.Guest:</span><span class="sxs-lookup"><span data-stu-id="e8356-191">Retrieve hello template object for hello Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="e8356-192">Crear un nuevo objeto de configuración de plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="e8356-192">Create a new settings object from hello template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="e8356-193">Establecer toohello requerido el valor de hello:</span><span class="sxs-lookup"><span data-stu-id="e8356-193">Set hello setting toohello required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="e8356-194">Crear nueva configuración de Hola para grupo necesario hello en el directorio de hello:</span><span class="sxs-lookup"><span data-stu-id="e8356-194">Create hello new setting for hello required group in hello directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a><span data-ttu-id="e8356-195">Actualizar la configuración en el nivel del directorio de Hola</span><span class="sxs-lookup"><span data-stu-id="e8356-195">Update settings at hello directory level</span></span>

<span data-ttu-id="e8356-196">Estos pasos actualización la configuración en el nivel de directorio, que se aplican tooall unificado grupos en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8356-196">These steps update settings at directory level, which apply tooall Unified groups in hello directory.</span></span> <span data-ttu-id="e8356-197">En estos ejemplos se asume que ya hay un objeto de configuración en el directorio.</span><span class="sxs-lookup"><span data-stu-id="e8356-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="e8356-198">Busque el objeto de configuración existente de hello:</span><span class="sxs-lookup"><span data-stu-id="e8356-198">Find hello existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="e8356-199">Valor de Hola de actualización:</span><span class="sxs-lookup"><span data-stu-id="e8356-199">Update hello value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="e8356-200">Actualización del valor de hello:</span><span class="sxs-lookup"><span data-stu-id="e8356-200">Update hello setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a><span data-ttu-id="e8356-201">Quite la configuración en el nivel del directorio de Hola</span><span class="sxs-lookup"><span data-stu-id="e8356-201">Remove settings at hello directory level</span></span>
<span data-ttu-id="e8356-202">Este paso quita la configuración en el nivel de directorio, que se aplican los grupos de Office tooall en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8356-202">This step removes settings at directory level, which apply tooall Office groups in hello directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="e8356-203">Referencia de sintaxis de cmdlet</span><span class="sxs-lookup"><span data-stu-id="e8356-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="e8356-204">Puede encontrar más documentación de Azure Active Directory PowerShell en el artículo sobre los [cmdlets de Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="e8356-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="e8356-205">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="e8356-205">Additional reading</span></span>

* [<span data-ttu-id="e8356-206">Administrar acceso tooresources con grupos de Active Directory de Azure</span><span class="sxs-lookup"><span data-stu-id="e8356-206">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="e8356-207">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e8356-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
