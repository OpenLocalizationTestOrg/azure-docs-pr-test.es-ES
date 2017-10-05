---
title: Ejemplos de PowerShell para administrar grupos en Azure Active Directory | Microsoft Docs
description: "En esta página se proporcionan ejemplos de PowerShell para ayudarlo a administrar grupos de Azure Active Directory."
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
ms.openlocfilehash: a81820bc778c26f6e8051e2817ebd2b9c24b697a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="61d37-104">Cmdlets de la versión 2 de Azure Active Directory para la administración de grupos</span><span class="sxs-lookup"><span data-stu-id="61d37-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="61d37-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="61d37-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="61d37-106">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="61d37-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="61d37-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="61d37-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="61d37-108">En este artículo se incluyen ejemplos de cómo usar PowerShell para administrar grupos en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="61d37-108">This article contains examples of how to use PowerShell to manage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="61d37-109">También se indica cómo configurar el módulo de Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="61d37-109">It also tells you how to get set up with the Azure AD PowerShell module.</span></span> <span data-ttu-id="61d37-110">En primer lugar, debe [descargar el módulo de Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="61d37-110">First, you must [download the Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-the-azure-ad-powershell-module"></a><span data-ttu-id="61d37-111">Instalación del módulo de Azure AD PowerShell</span><span class="sxs-lookup"><span data-stu-id="61d37-111">Installing the Azure AD PowerShell module</span></span>
<span data-ttu-id="61d37-112">Para instalar el módulo de Azure AD PowerShell, use los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="61d37-112">To install the Azure AD PowerShell module, use the following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="61d37-113">Para comprobar que se ha instalado el módulo, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="61d37-113">To verify that the module was installed, use the following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="61d37-114">Ahora puede empezar a usar los cmdlets del módulo.</span><span class="sxs-lookup"><span data-stu-id="61d37-114">Now you can start using the cmdlets in the module.</span></span> <span data-ttu-id="61d37-115">Para ver una descripción completa de los cmdlets del módulo de Azure AD, consulte la documentación de referencia en línea para obtener [Azure Active Directory PowerShell versión 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="61d37-115">For a full description of the cmdlets in the Azure AD module, please refer to the online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-to-the-directory"></a><span data-ttu-id="61d37-116">Conexión al directorio</span><span class="sxs-lookup"><span data-stu-id="61d37-116">Connecting to the directory</span></span>
<span data-ttu-id="61d37-117">Antes de empezar a administrar los grupos mediante los cmdlets de Azure AD PowerShell, debe conectar la sesión de PowerShell al directorio que quiera administrar.</span><span class="sxs-lookup"><span data-stu-id="61d37-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session to the directory you want to manage.</span></span> <span data-ttu-id="61d37-118">Use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="61d37-118">Use the following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="61d37-119">El cmdlet le pide las credenciales que quiere utilizar para tener acceso al directorio.</span><span class="sxs-lookup"><span data-stu-id="61d37-119">The cmdlet prompts you for the credentials you want to use to access your directory.</span></span> <span data-ttu-id="61d37-120">En este ejemplo, vamos a utilizar karen@drumkit.onmicrosoft.com para tener acceso al directorio de demostración.</span><span class="sxs-lookup"><span data-stu-id="61d37-120">In this example, we are using karen@drumkit.onmicrosoft.com to access the demonstration directory.</span></span> <span data-ttu-id="61d37-121">El cmdlet devuelve una confirmación para mostrar que la sesión se ha conectado correctamente al directorio:</span><span class="sxs-lookup"><span data-stu-id="61d37-121">The cmdlet returns a confirmation to show the session was connected successfully to your directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="61d37-122">Ahora puede empezar a usar los cmdlets de Azure AD para administrar grupos en el directorio.</span><span class="sxs-lookup"><span data-stu-id="61d37-122">Now you can start using the AzureAD cmdlets to manage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="61d37-123">Recuperación de grupos</span><span class="sxs-lookup"><span data-stu-id="61d37-123">Retrieving groups</span></span>
<span data-ttu-id="61d37-124">Para recuperar grupos que ya se encuentren en el directorio, puede usar el cmdlet Get-AzureADGroups.</span><span class="sxs-lookup"><span data-stu-id="61d37-124">To retrieve existing groups from your directory you can use the Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="61d37-125">Para recuperar todos los grupos del directorio, ejecute el cmdlet sin parámetros:</span><span class="sxs-lookup"><span data-stu-id="61d37-125">To retrieve all groups in the directory, use the cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="61d37-126">El cmdlet devuelve todos los grupos del directorio conectado.</span><span class="sxs-lookup"><span data-stu-id="61d37-126">The cmdlet returns all groups in the connected directory.</span></span>

<span data-ttu-id="61d37-127">Puede usar el parámetro -objectID si quiere recuperar un grupo específico para el que especifica el id. de objeto del grupo:</span><span class="sxs-lookup"><span data-stu-id="61d37-127">You can use the -objectID parameter to retrieve a specific group for which you specify the group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="61d37-128">El cmdlet devuelve ahora el grupo cuyo id. de objeto coincide con el valor del parámetro especificado:</span><span class="sxs-lookup"><span data-stu-id="61d37-128">The cmdlet now returns the group whose objectID matches the value of the parameter you entered:</span></span>

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

<span data-ttu-id="61d37-129">Puede buscar un grupo específico mediante el parámetro - filter.</span><span class="sxs-lookup"><span data-stu-id="61d37-129">You can search for a specific group using the -filter parameter.</span></span> <span data-ttu-id="61d37-130">Este parámetro toma una cláusula de filtro ODATA y devuelve todos los grupos que coinciden con él, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="61d37-130">This parameter takes an ODATA filter clause and returns all groups that match the filter, as in the following example:</span></span>

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
> <span data-ttu-id="61d37-131">Los cmdlets de Azure AD PowerShell implementan el estándar de consulta de OData.</span><span class="sxs-lookup"><span data-stu-id="61d37-131">The AzureAD PowerShell cmdlets implement the OData query standard.</span></span> <span data-ttu-id="61d37-132">Para obtener más información, consulte **$filter** en [Opciones de la consulta del sistema OData mediante el punto de conexión de OData](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span><span class="sxs-lookup"><span data-stu-id="61d37-132">For more information, see **$filter** in [OData system query options using the OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="61d37-133">Creación de grupos</span><span class="sxs-lookup"><span data-stu-id="61d37-133">Creating groups</span></span>
<span data-ttu-id="61d37-134">Para crear un nuevo grupo en el directorio, use el cmdlet New-AzureADGroup.</span><span class="sxs-lookup"><span data-stu-id="61d37-134">To create a new group in your directory, use the New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="61d37-135">Este cmdlet crea un nuevo grupo de seguridad llamado "Marketing":</span><span class="sxs-lookup"><span data-stu-id="61d37-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="61d37-136">Actualización de grupos</span><span class="sxs-lookup"><span data-stu-id="61d37-136">Updating groups</span></span>
<span data-ttu-id="61d37-137">Para actualizar un grupo que ya exista, utilice el cmdlet Set-AzureADGroup.</span><span class="sxs-lookup"><span data-stu-id="61d37-137">To update an existing group, use the Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="61d37-138">En este ejemplo, vamos a cambiar la propiedad DisplayName del grupo "Administradores de Intune".</span><span class="sxs-lookup"><span data-stu-id="61d37-138">In this example, we’re changing the DisplayName property of the group “Intune Administrators.”</span></span> <span data-ttu-id="61d37-139">En primer lugar, buscaremos el grupo mediante el cmdlet Get-AzureADGroup y aplicaremos un filtro usando el atributo DisplayName:</span><span class="sxs-lookup"><span data-stu-id="61d37-139">First, we’re finding the group using the Get-AzureADGroup cmdlet and filter using the DisplayName attribute:</span></span>

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

<span data-ttu-id="61d37-140">Después, vamos a cambiar la propiedad Description del nuevo valor de "Administradores de dispositivos de Intune":</span><span class="sxs-lookup"><span data-stu-id="61d37-140">Next, we’re changing the Description property to the new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="61d37-141">Ahora, si encontramos el grupo nuevo, veremos que la propiedad Description se actualiza para reflejar el nuevo valor:</span><span class="sxs-lookup"><span data-stu-id="61d37-141">Now if we find the group again, we see the Description property is updated to reflect the new value:</span></span>

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

## <a name="deleting-groups"></a><span data-ttu-id="61d37-142">Eliminación de grupos</span><span class="sxs-lookup"><span data-stu-id="61d37-142">Deleting groups</span></span>
<span data-ttu-id="61d37-143">Para eliminar grupos del directorio, use el cmdlet Remove-AzureADGroup de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="61d37-143">To delete groups from your directory, use the Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="61d37-144">Administración de miembros de grupos</span><span class="sxs-lookup"><span data-stu-id="61d37-144">Managing members of groups</span></span>
<span data-ttu-id="61d37-145">Si necesita agregar nuevos miembros a un grupo, utilice el cmdlet Add-AzureADGroupMember.</span><span class="sxs-lookup"><span data-stu-id="61d37-145">If you need to add new members to a group, use the Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="61d37-146">Este comando agrega un miembro al grupo de administradores de Intune que utilizamos en el ejemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="61d37-146">This command adds a member to the Intune Administrators group we used in the previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="61d37-147">El parámetro -ObjectId es el id. de objeto del grupo al que desea agregar un miembro y RefObjectId es el del usuario que desea agregar como miembro al grupo.</span><span class="sxs-lookup"><span data-stu-id="61d37-147">The -ObjectId parameter is the ObjectID of the group to which we want to add a member, and the -RefObjectId is the ObjectID of the user we want to add as a member to the group.</span></span>

<span data-ttu-id="61d37-148">Para obtener los miembros existentes de un grupo, use el cmdlet Get-AzureADGroupMember, como en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61d37-148">To get the existing members of a group, use the Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="61d37-149">Para quitar al miembro que agregamos anteriormente al grupo, use el cmdlet Remove-AzureADGroupMember, como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="61d37-149">To remove the member we previously added to the group, use the Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="61d37-150">Para comprobar si un usuario pertenece a uno o varios grupos, use el cmdlet Select-AzureADGroupIdsUserIsMemberOf.</span><span class="sxs-lookup"><span data-stu-id="61d37-150">To verify the group membership(s) of a user, use the Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="61d37-151">Este cmdlet toma como parámetros el id. de objeto del usuario que se comprueba si pertenece a uno o varios grupos, así como una lista de grupos para realizar dicha comprobación.</span><span class="sxs-lookup"><span data-stu-id="61d37-151">This cmdlet takes as its parameters the ObjectId of the user for which to check the group memberships, and a list of groups for which to check the memberships.</span></span> <span data-ttu-id="61d37-152">La lista de grupos debe proporcionarse como una variable compleja del tipo Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck, así que, antes, debemos creamos una variable con ese tipo:</span><span class="sxs-lookup"><span data-stu-id="61d37-152">The list of groups must be provided in the form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="61d37-153">Después, proporcionamos los valores de los id. de grupo para comprobar el atributo GroupIds de esta variable compleja:</span><span class="sxs-lookup"><span data-stu-id="61d37-153">Next, we provide values for the groupIds to check in the attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="61d37-154">Ahora, si queremos comprobar si un usuario con el id. de objeto 72cd4bbd-2594-40a2-935c-016f3cfeeeea pertenece a uno de los grupos de $g, debemos usar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="61d37-154">Now, if we want to check the group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against the groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="61d37-155">El valor devuelto es una lista con los grupos de los que es miembro este usuario.</span><span class="sxs-lookup"><span data-stu-id="61d37-155">The value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="61d37-156">También puede aplicar este método para comprobar si determinados contactos, grupos o entidades de seguridad pertenecen a los grupos de una lista concreta. Para ello, utilice Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf o Select-AzureADGroupIdsServicePrincipalIsMemberOf.</span><span class="sxs-lookup"><span data-stu-id="61d37-156">You can also apply this method to check Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="61d37-157">Administración de propietarios de grupos</span><span class="sxs-lookup"><span data-stu-id="61d37-157">Managing owners of groups</span></span>
<span data-ttu-id="61d37-158">Para agregar propietarios a un grupo, utilice el cmdlet Add-AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="61d37-158">To add owners to a group, use the Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="61d37-159">El parámetro -ObjectId es el id. de objeto del grupo al que desea agregar un propietario y RefObjectId es el del usuario que desea agregar como propietario al grupo.</span><span class="sxs-lookup"><span data-stu-id="61d37-159">The -ObjectId parameter is the ObjectID of the group to which we want to add an owner, and the -RefObjectId is the ObjectID of the user we want to add as an owner of the group.</span></span>

<span data-ttu-id="61d37-160">Para recuperar los propietarios de un grupo, utilice el cmdlet Get-AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="61d37-160">To retrieve the owners of a group, use the Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="61d37-161">El cmdlet devuelve la lista de propietarios del grupo especificado:</span><span class="sxs-lookup"><span data-stu-id="61d37-161">The cmdlet returns the list of owners for the specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="61d37-162">Si desea quitar un propietario de un grupo, utilice el cmdlet Remove-AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="61d37-162">If you want to remove an owner from a group, use the Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="61d37-163">Alias reservados</span><span class="sxs-lookup"><span data-stu-id="61d37-163">Reserved aliases</span></span> 
<span data-ttu-id="61d37-164">Cuando se crea un grupo, algunos de los puntos de conexión permiten al usuario final especificar un mailNickname o alias que se usarán como parte de la dirección de correo electrónico del grupo.</span><span class="sxs-lookup"><span data-stu-id="61d37-164">When a group is created, certain endpoints allow the end user to specify a mailNickname or alias to be used as part of the email address of the group.</span></span> <span data-ttu-id="61d37-165">Los grupos con los siguientes alias de correo electrónico con privilegios elevados solo puede crearlos un administrador global de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61d37-165">Groups with the following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="61d37-166">abuse</span><span class="sxs-lookup"><span data-stu-id="61d37-166">abuse</span></span> 
* <span data-ttu-id="61d37-167">admin</span><span class="sxs-lookup"><span data-stu-id="61d37-167">admin</span></span> 
* <span data-ttu-id="61d37-168">administrator</span><span class="sxs-lookup"><span data-stu-id="61d37-168">administrator</span></span> 
* <span data-ttu-id="61d37-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="61d37-169">hostmaster</span></span> 
* <span data-ttu-id="61d37-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="61d37-170">majordomo</span></span> 
* <span data-ttu-id="61d37-171">postmaster</span><span class="sxs-lookup"><span data-stu-id="61d37-171">postmaster</span></span> 
* <span data-ttu-id="61d37-172">root</span><span class="sxs-lookup"><span data-stu-id="61d37-172">root</span></span> 
* <span data-ttu-id="61d37-173">secure</span><span class="sxs-lookup"><span data-stu-id="61d37-173">secure</span></span> 
* <span data-ttu-id="61d37-174">security</span><span class="sxs-lookup"><span data-stu-id="61d37-174">security</span></span> 
* <span data-ttu-id="61d37-175">ssl-admin</span><span class="sxs-lookup"><span data-stu-id="61d37-175">ssl-admin</span></span> 
* <span data-ttu-id="61d37-176">webmaster</span><span class="sxs-lookup"><span data-stu-id="61d37-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="61d37-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="61d37-177">Next steps</span></span>
<span data-ttu-id="61d37-178">Puede encontrar más documentación de Azure Active Directory PowerShell en el artículo sobre los [cmdlets de Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="61d37-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="61d37-179">Administración del acceso a los recursos con grupos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61d37-179">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="61d37-180">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61d37-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
