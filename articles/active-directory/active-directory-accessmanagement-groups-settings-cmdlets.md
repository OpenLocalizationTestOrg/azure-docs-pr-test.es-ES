---
title: "Configuración de grupos mediante cmdlets de Azure Active Directory | Microsoft Docs"
description: "Administración de la configuración de grupos mediante cmdlets de Azure Active Directory"
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
ms.openlocfilehash: 0d89f12955b90c7e1a8301b7c3a1a92e7f62d085
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="814d9-103">Cmdlets de Azure Active Directory para configurar las opciones de grupo</span><span class="sxs-lookup"><span data-stu-id="814d9-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="814d9-104">Este contenido se aplica únicamente a grupos de Office 365.</span><span class="sxs-lookup"><span data-stu-id="814d9-104">This content applies only to Office 365 groups.</span></span> <span data-ttu-id="814d9-105">Para obtener más información sobre cómo permitir a los usuarios crear grupos de seguridad, establezca `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` como se describe en [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="814d9-105">For more information on how to allow users to create Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="814d9-106">Los grupos de Office 365 se configuran mediante un objeto Settings y un objeto SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="814d9-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="814d9-107">Al principio no ve ningún objeto de configuración en el directorio porque este se ha configurado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="814d9-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with the default settings.</span></span> <span data-ttu-id="814d9-108">Para cambiar la configuración predeterminada, debe crear un nuevo objeto Settings utilizando una plantilla SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="814d9-108">To change the default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="814d9-109">Las plantillas de configuración las define Microsoft.</span><span class="sxs-lookup"><span data-stu-id="814d9-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="814d9-110">Hay varias plantillas de configuración diferentes.</span><span class="sxs-lookup"><span data-stu-id="814d9-110">There are several different settings templates.</span></span> <span data-ttu-id="814d9-111">Para configurar los valores del grupo de Office 365 para su directorio, utiliza la plantilla denominada "Group.Unified".</span><span class="sxs-lookup"><span data-stu-id="814d9-111">To configure Office 365 group settings for your directory, you use the template named "Group.Unified".</span></span> <span data-ttu-id="814d9-112">Para configurar los valores del grupo de Office 365 en un único grupo, utilice la plantilla denominada "Group.Unified.Guest".</span><span class="sxs-lookup"><span data-stu-id="814d9-112">To configure Office 365 group settings on a single group, use the template named "Group.Unified.Guest".</span></span> <span data-ttu-id="814d9-113">Esta plantilla se usa para administrar el acceso de invitado a un grupo de Office 365.</span><span class="sxs-lookup"><span data-stu-id="814d9-113">This template is used to manage guest access to an Office 365 group.</span></span> 

<span data-ttu-id="814d9-114">Los cmdlets forman parte del módulo Azure Active Directory PowerShell V2.</span><span class="sxs-lookup"><span data-stu-id="814d9-114">The cmdlets are part of the Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="814d9-115">Para obtener instrucciones sobre cómo descargar e instalar el módulo en el equipo, consulte el artículo [Azure Active Directory PowerShell versión 2](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="814d9-115">For instructions how to download and install the module on your computer, see the article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="814d9-116">Puede instalar la versión 2 del módulo desde [la Galería de PowerShell](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="814d9-116">You can install the version 2 release of the module from [the PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="814d9-117">Recuperación de un valor de configuración específico</span><span class="sxs-lookup"><span data-stu-id="814d9-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="814d9-118">Si conoce el nombre de la configuración que desea recuperar, puede usar el siguiente cmdlet para recuperar el valor de configuración actual.</span><span class="sxs-lookup"><span data-stu-id="814d9-118">If you know the name of the setting you want to retrieve, you can use the below cmdlet to retrieve the current settings value.</span></span> <span data-ttu-id="814d9-119">En este ejemplo, se recuperará el valor de una configuración denominada "UsageGuidelinesUrl".</span><span class="sxs-lookup"><span data-stu-id="814d9-119">In this example, we're retrieving the value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="814d9-120">Puede obtener información adicional sobre la configuración de directorio y sus nombres en este artículo.</span><span class="sxs-lookup"><span data-stu-id="814d9-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-the-directory-level"></a><span data-ttu-id="814d9-121">Creación de una configuración en el nivel de directorio</span><span class="sxs-lookup"><span data-stu-id="814d9-121">Create settings at the directory level</span></span>
<span data-ttu-id="814d9-122">Con estos pasos se crean configuraciones en el nivel de directorio, las cuales se aplican a todos los grupos de Office 365 (grupos unificados) del directorio.</span><span class="sxs-lookup"><span data-stu-id="814d9-122">These steps create settings at directory level, which apply to all Office 365 groups (Unified groups) in the directory.</span></span>

1. <span data-ttu-id="814d9-123">En los cmdlets DirectorySettings, debe especificar el identificador de la plantilla SettingsTemplate que desea usar.</span><span class="sxs-lookup"><span data-stu-id="814d9-123">In the DirectorySettings cmdlets, you must specify the ID of the SettingsTemplate you want to use.</span></span> <span data-ttu-id="814d9-124">Si no conoce este identificador, este cmdlet devuelve la lista de plantillas de configuración:</span><span class="sxs-lookup"><span data-stu-id="814d9-124">If you do not know this ID, this cmdlet returns the list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="814d9-125">Esta llamada al cmdlet devuelve todas las plantillas que están disponibles:</span><span class="sxs-lookup"><span data-stu-id="814d9-125">This cmdlet call returns all templates that are available:</span></span>
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define the different settings that can be used for the associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. <span data-ttu-id="814d9-126">Para agregar una dirección URL de instrucciones de uso, primero debe obtener el objeto SettingsTemplate que define el valor pertinente, es decir, la plantilla Group.Unified:</span><span class="sxs-lookup"><span data-stu-id="814d9-126">To add a usage guideline URL, first you need to get the SettingsTemplate object that defines the usage guideline URL value; that is, the Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="814d9-127">A continuación, cree un nuevo objeto de configuración basado en esa plantilla:</span><span class="sxs-lookup"><span data-stu-id="814d9-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="814d9-128">Luego, actualice el valor de instrucciones de uso:</span><span class="sxs-lookup"><span data-stu-id="814d9-128">Then update the usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="814d9-129">Por último, aplique la configuración:</span><span class="sxs-lookup"><span data-stu-id="814d9-129">Finally, apply the settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="814d9-130">Tras completarse correctamente, el cmdlet devuelve el identificador del nuevo objeto de configuración:</span><span class="sxs-lookup"><span data-stu-id="814d9-130">Upon successful completion, the cmdlet returns the ID of the new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="814d9-131">Esta es la configuración definida en el objeto SettingsTemplate Group.Unified.</span><span class="sxs-lookup"><span data-stu-id="814d9-131">Here are the settings defined in the Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="814d9-132">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="814d9-132">**Setting**</span></span> | <span data-ttu-id="814d9-133">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="814d9-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="814d9-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="814d9-134">EnableGroupCreation</span></span><li><span data-ttu-id="814d9-135">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="814d9-135">Type: Boolean</span></span><li><span data-ttu-id="814d9-136">Valor predeterminado: True.</span><span class="sxs-lookup"><span data-stu-id="814d9-136">Default: True</span></span> |<span data-ttu-id="814d9-137">Marca que indica si se permite la creación de grupos unificados en el directorio.</span><span class="sxs-lookup"><span data-stu-id="814d9-137">The flag indicating whether Unified Group creation is allowed in the directory.</span></span> |
|  <ul><li><span data-ttu-id="814d9-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="814d9-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="814d9-139">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="814d9-139">Type: String</span></span><li><span data-ttu-id="814d9-140">Valor predeterminado: “”</span><span class="sxs-lookup"><span data-stu-id="814d9-140">Default: “”</span></span> |<span data-ttu-id="814d9-141">El GUID del grupo de seguridad para el se permite a los miembros crear grupos unificados incluso cuando EnableGroupCreation == false.</span><span class="sxs-lookup"><span data-stu-id="814d9-141">GUID of the security group for which the members are allowed to create Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="814d9-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="814d9-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="814d9-143">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="814d9-143">Type: String</span></span><li><span data-ttu-id="814d9-144">Valor predeterminado: “”</span><span class="sxs-lookup"><span data-stu-id="814d9-144">Default: “”</span></span> |<span data-ttu-id="814d9-145">Un vínculo a las instrucciones de uso de grupos.</span><span class="sxs-lookup"><span data-stu-id="814d9-145">A link to the Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="814d9-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="814d9-146">ClassificationDescriptions</span></span><li><span data-ttu-id="814d9-147">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="814d9-147">Type: String</span></span><li><span data-ttu-id="814d9-148">Valor predeterminado: “”</span><span class="sxs-lookup"><span data-stu-id="814d9-148">Default: “”</span></span> | <span data-ttu-id="814d9-149">Una lista delimitada por comas de las descripciones de clasificación.</span><span class="sxs-lookup"><span data-stu-id="814d9-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="814d9-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="814d9-150">DefaultClassification</span></span><li><span data-ttu-id="814d9-151">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="814d9-151">Type: String</span></span><li><span data-ttu-id="814d9-152">Valor predeterminado: “”</span><span class="sxs-lookup"><span data-stu-id="814d9-152">Default: “”</span></span> | <span data-ttu-id="814d9-153">La clasificación que se va a utilizar como la clasificación predeterminada para un grupo si no se ha especificado ninguno.</span><span class="sxs-lookup"><span data-stu-id="814d9-153">The classification that is to be used as the default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="814d9-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="814d9-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="814d9-155">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="814d9-155">Type: String</span></span><li><span data-ttu-id="814d9-156">Valor predeterminado: “”</span><span class="sxs-lookup"><span data-stu-id="814d9-156">Default: “”</span></span> |<span data-ttu-id="814d9-157">Todavía no implementado</span><span class="sxs-lookup"><span data-stu-id="814d9-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="814d9-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="814d9-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="814d9-159">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="814d9-159">Type: Boolean</span></span><li><span data-ttu-id="814d9-160">Valor predeterminado: False.</span><span class="sxs-lookup"><span data-stu-id="814d9-160">Default: False</span></span> | <span data-ttu-id="814d9-161">Valor booleano que indica si un usuario invitado puede ser o no un propietario de grupos.</span><span class="sxs-lookup"><span data-stu-id="814d9-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="814d9-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="814d9-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="814d9-163">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="814d9-163">Type: Boolean</span></span><li><span data-ttu-id="814d9-164">Valor predeterminado: True.</span><span class="sxs-lookup"><span data-stu-id="814d9-164">Default: True</span></span> | <span data-ttu-id="814d9-165">Valor booleano que indica si un usuario invitado puede tener o no acceso al contenido de grupos unificados.</span><span class="sxs-lookup"><span data-stu-id="814d9-165">Boolean indicating whether or not a guest user can have access to Unified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="814d9-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="814d9-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="814d9-167">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="814d9-167">Type: String</span></span><li><span data-ttu-id="814d9-168">Valor predeterminado: “”</span><span class="sxs-lookup"><span data-stu-id="814d9-168">Default: “”</span></span> | <span data-ttu-id="814d9-169">La dirección URL de un vínculo a las instrucciones de uso del invitado.</span><span class="sxs-lookup"><span data-stu-id="814d9-169">The url of a link to the guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="814d9-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="814d9-170">AllowToAddGuests</span></span><li><span data-ttu-id="814d9-171">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="814d9-171">Type: Boolean</span></span><li><span data-ttu-id="814d9-172">Valor predeterminado: True.</span><span class="sxs-lookup"><span data-stu-id="814d9-172">Default: True</span></span> | <span data-ttu-id="814d9-173">Un valor booleano que indica si está permitido o no agregar invitados a este directorio.</span><span class="sxs-lookup"><span data-stu-id="814d9-173">A boolean indicating whether or not is allowed to add guests to this directory.</span></span>|
|  <ul><li><span data-ttu-id="814d9-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="814d9-174">ClassificationList</span></span><li><span data-ttu-id="814d9-175">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="814d9-175">Type: String</span></span><li><span data-ttu-id="814d9-176">Valor predeterminado: “”</span><span class="sxs-lookup"><span data-stu-id="814d9-176">Default: “”</span></span> |<span data-ttu-id="814d9-177">Una lista de valores de clasificación delimitados por coma que se puede aplicar a grupos unificados.</span><span class="sxs-lookup"><span data-stu-id="814d9-177">A comma-delimited list of valid classification values that can be applied to Unified Groups.</span></span> |
|  <ul><li><span data-ttu-id="814d9-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="814d9-178">EnableGroupCreation</span></span><li><span data-ttu-id="814d9-179">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="814d9-179">Type: Boolean</span></span><li><span data-ttu-id="814d9-180">Valor predeterminado: True.</span><span class="sxs-lookup"><span data-stu-id="814d9-180">Default: True</span></span> | <span data-ttu-id="814d9-181">Un valor booleano que indica si los usuarios no administradores pueden crear o no nuevos grupos unificados.</span><span class="sxs-lookup"><span data-stu-id="814d9-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-the-directory-level"></a><span data-ttu-id="814d9-182">Lectura de la configuración en el nivel de directorio</span><span class="sxs-lookup"><span data-stu-id="814d9-182">Read settings at the directory level</span></span>
<span data-ttu-id="814d9-183">Con estos pasos se lee la configuración en el nivel de directorio, la cual se aplica a todos los grupos de Office del directorio.</span><span class="sxs-lookup"><span data-stu-id="814d9-183">These steps read settings at directory level, which apply to all Office groups in the directory.</span></span>

1. <span data-ttu-id="814d9-184">Lea toda la configuración de directorio existente:</span><span class="sxs-lookup"><span data-stu-id="814d9-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="814d9-185">Este cmdlet devuelve la lista de las opciones de configuración del directorio:</span><span class="sxs-lookup"><span data-stu-id="814d9-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="814d9-186">Lea toda la configuración de un grupo específico:</span><span class="sxs-lookup"><span data-stu-id="814d9-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="814d9-187">Lea todos los valores de configuración de directorio de un objeto de configuración del directorio específico, con el GUID de identificador de configuración:</span><span class="sxs-lookup"><span data-stu-id="814d9-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="814d9-188">Este cmdlet devuelve los nombres y valores de este objeto de configuración para este grupo en particular:</span><span class="sxs-lookup"><span data-stu-id="814d9-188">This cmdlet returns the names and values in this settings object for this specific group:</span></span>
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

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="814d9-189">Actualización de la configuración de un grupo específico</span><span class="sxs-lookup"><span data-stu-id="814d9-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="814d9-190">Busque la plantilla de configuración denominada "Groups.Unified.Guest"</span><span class="sxs-lookup"><span data-stu-id="814d9-190">Search for the settings template named "Groups.Unified.Guest"</span></span>
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
2. <span data-ttu-id="814d9-191">Recupere el objeto de plantilla para la plantilla Groups.Unified.Guest:</span><span class="sxs-lookup"><span data-stu-id="814d9-191">Retrieve the template object for the Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="814d9-192">Cree un nuevo objeto de configuración a partir de la plantilla:</span><span class="sxs-lookup"><span data-stu-id="814d9-192">Create a new settings object from the template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="814d9-193">Establezca la configuración al valor requerido:</span><span class="sxs-lookup"><span data-stu-id="814d9-193">Set the setting to the required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="814d9-194">Cree la nueva configuración para el grupo necesario en el directorio:</span><span class="sxs-lookup"><span data-stu-id="814d9-194">Create the new setting for the required group in the directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-the-directory-level"></a><span data-ttu-id="814d9-195">Actualización de la configuración en el nivel de directorio</span><span class="sxs-lookup"><span data-stu-id="814d9-195">Update settings at the directory level</span></span>

<span data-ttu-id="814d9-196">Con estos pasos se actualizan configuraciones en el nivel de directorio, las cuales se aplican a todos los grupos unificados del directorio.</span><span class="sxs-lookup"><span data-stu-id="814d9-196">These steps update settings at directory level, which apply to all Unified groups in the directory.</span></span> <span data-ttu-id="814d9-197">En estos ejemplos se asume que ya hay un objeto de configuración en el directorio.</span><span class="sxs-lookup"><span data-stu-id="814d9-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="814d9-198">Busque el objeto de configuración existente:</span><span class="sxs-lookup"><span data-stu-id="814d9-198">Find the existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="814d9-199">Actualice el valor:</span><span class="sxs-lookup"><span data-stu-id="814d9-199">Update the value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="814d9-200">Actualice la configuración:</span><span class="sxs-lookup"><span data-stu-id="814d9-200">Update the setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-the-directory-level"></a><span data-ttu-id="814d9-201">Eliminación de la configuración en el nivel de directorio</span><span class="sxs-lookup"><span data-stu-id="814d9-201">Remove settings at the directory level</span></span>
<span data-ttu-id="814d9-202">Con estos pasos se elimina la configuración en el nivel de directorio, lo cual se aplica a todos los grupos de Office del directorio.</span><span class="sxs-lookup"><span data-stu-id="814d9-202">This step removes settings at directory level, which apply to all Office groups in the directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="814d9-203">Referencia de sintaxis de cmdlet</span><span class="sxs-lookup"><span data-stu-id="814d9-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="814d9-204">Puede encontrar más documentación de Azure Active Directory PowerShell en el artículo sobre los [cmdlets de Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="814d9-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="814d9-205">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="814d9-205">Additional reading</span></span>

* [<span data-ttu-id="814d9-206">Administración del acceso a los recursos con grupos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="814d9-206">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="814d9-207">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="814d9-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
