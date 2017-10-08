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
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="7c32a-104">Cmdlets de la versión 2 de Azure Active Directory para la administración de grupos</span><span class="sxs-lookup"><span data-stu-id="7c32a-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7c32a-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7c32a-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="7c32a-106">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="7c32a-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="7c32a-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c32a-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="7c32a-108">Este artículo contiene ejemplos de cómo toouse PowerShell toomanage los grupos en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7c32a-108">This article contains examples of how toouse PowerShell toomanage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="7c32a-109">También indica cómo tooget configurado con el módulo de PowerShell de Azure AD Hola.</span><span class="sxs-lookup"><span data-stu-id="7c32a-109">It also tells you how tooget set up with hello Azure AD PowerShell module.</span></span> <span data-ttu-id="7c32a-110">En primer lugar, debe [descargar el módulo de PowerShell de Azure AD hello](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="7c32a-110">First, you must [download hello Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-hello-azure-ad-powershell-module"></a><span data-ttu-id="7c32a-111">Instalando el módulo de PowerShell de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="7c32a-111">Installing hello Azure AD PowerShell module</span></span>
<span data-ttu-id="7c32a-112">Hola tooinstall módulo de PowerShell de Azure AD, utilice Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="7c32a-112">tooinstall hello Azure AD PowerShell module, use hello following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="7c32a-113">se instaló tooverify que Hola módulo, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7c32a-113">tooverify that hello module was installed, use hello following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="7c32a-114">Ahora puede empezar a usar cmdlets de hello en el módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c32a-114">Now you can start using hello cmdlets in hello module.</span></span> <span data-ttu-id="7c32a-115">Para obtener una descripción completa de cmdlets de hello en el módulo de hello Azure AD, consulte documentación de referencia en línea toohello [Azure Active Directory PowerShell versión 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="7c32a-115">For a full description of hello cmdlets in hello Azure AD module, please refer toohello online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-toohello-directory"></a><span data-ttu-id="7c32a-116">Conexión toohello directorio</span><span class="sxs-lookup"><span data-stu-id="7c32a-116">Connecting toohello directory</span></span>
<span data-ttu-id="7c32a-117">Antes de poder empezar a administrar grupos mediante los cmdlets de PowerShell de Azure AD, debe conectar el directorio de toohello de sesión de PowerShell que desea toomanage.</span><span class="sxs-lookup"><span data-stu-id="7c32a-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session toohello directory you want toomanage.</span></span> <span data-ttu-id="7c32a-118">Usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7c32a-118">Use hello following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="7c32a-119">Hello cmdlet le pide que para hello las credenciales desea toouse tooaccess su directorio.</span><span class="sxs-lookup"><span data-stu-id="7c32a-119">hello cmdlet prompts you for hello credentials you want toouse tooaccess your directory.</span></span> <span data-ttu-id="7c32a-120">En este ejemplo, estamos utilizando karen@drumkit.onmicrosoft.com tooaccess Hola directorio de demostración.</span><span class="sxs-lookup"><span data-stu-id="7c32a-120">In this example, we are using karen@drumkit.onmicrosoft.com tooaccess hello demonstration directory.</span></span> <span data-ttu-id="7c32a-121">Hello cmdlet devuelve una sesión de hello tooshow de confirmación se ha conectado correctamente tooyour directorio:</span><span class="sxs-lookup"><span data-stu-id="7c32a-121">hello cmdlet returns a confirmation tooshow hello session was connected successfully tooyour directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="7c32a-122">Ahora puede empezar a usar grupos de toomanage de cmdlets de organización de hello en el directorio.</span><span class="sxs-lookup"><span data-stu-id="7c32a-122">Now you can start using hello AzureAD cmdlets toomanage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="7c32a-123">Recuperación de grupos</span><span class="sxs-lookup"><span data-stu-id="7c32a-123">Retrieving groups</span></span>
<span data-ttu-id="7c32a-124">tooretrieve los grupos existentes del directorio que puede usar Hola cmdlet Get-AzureADGroups.</span><span class="sxs-lookup"><span data-stu-id="7c32a-124">tooretrieve existing groups from your directory you can use hello Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="7c32a-125">tooretrieve todos los grupos en el directorio hello, use el cmdlet de hello sin parámetros:</span><span class="sxs-lookup"><span data-stu-id="7c32a-125">tooretrieve all groups in hello directory, use hello cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="7c32a-126">Hola cmdlet devuelve todos los grupos en el directorio conectado Hola.</span><span class="sxs-lookup"><span data-stu-id="7c32a-126">hello cmdlet returns all groups in hello connected directory.</span></span>

<span data-ttu-id="7c32a-127">Puede usar hello - objectID parámetro tooretrieve un grupo específico para el que se especifique objectID del grupo de hello:</span><span class="sxs-lookup"><span data-stu-id="7c32a-127">You can use hello -objectID parameter tooretrieve a specific group for which you specify hello group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="7c32a-128">Hola cmdlet devuelve ahora grupo hello cuyo objectID coincide con valor de Hola de parámetro hello especificado:</span><span class="sxs-lookup"><span data-stu-id="7c32a-128">hello cmdlet now returns hello group whose objectID matches hello value of hello parameter you entered:</span></span>

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

<span data-ttu-id="7c32a-129">Puede buscar un grupo específico mediante Hola - parámetro filter.</span><span class="sxs-lookup"><span data-stu-id="7c32a-129">You can search for a specific group using hello -filter parameter.</span></span> <span data-ttu-id="7c32a-130">Este parámetro toma una cláusula de filtro ODATA y devuelve todos los grupos que coinciden con el filtro de hello, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="7c32a-130">This parameter takes an ODATA filter clause and returns all groups that match hello filter, as in hello following example:</span></span>

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
> <span data-ttu-id="7c32a-131">Hola AzureAD PowerShell cmdlets implementar Hola estándar de consulta de OData.</span><span class="sxs-lookup"><span data-stu-id="7c32a-131">hello AzureAD PowerShell cmdlets implement hello OData query standard.</span></span> <span data-ttu-id="7c32a-132">Para obtener más información, consulte **$filter** en [opciones de consulta de sistema de OData con el extremo de OData de hello](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span><span class="sxs-lookup"><span data-stu-id="7c32a-132">For more information, see **$filter** in [OData system query options using hello OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="7c32a-133">Creación de grupos</span><span class="sxs-lookup"><span data-stu-id="7c32a-133">Creating groups</span></span>
<span data-ttu-id="7c32a-134">toocreate un nuevo grupo en el directorio, use el cmdlet New-AzureADGroup Hola.</span><span class="sxs-lookup"><span data-stu-id="7c32a-134">toocreate a new group in your directory, use hello New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="7c32a-135">Este cmdlet crea un nuevo grupo de seguridad llamado "Marketing":</span><span class="sxs-lookup"><span data-stu-id="7c32a-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="7c32a-136">Actualización de grupos</span><span class="sxs-lookup"><span data-stu-id="7c32a-136">Updating groups</span></span>
<span data-ttu-id="7c32a-137">tooupdate un grupo existente, use el cmdlet de hello AzureADGroup del conjunto.</span><span class="sxs-lookup"><span data-stu-id="7c32a-137">tooupdate an existing group, use hello Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="7c32a-138">En este ejemplo, estamos cambiando Hola propiedad DisplayName del grupo de Hola "Administradores de Intune".</span><span class="sxs-lookup"><span data-stu-id="7c32a-138">In this example, we’re changing hello DisplayName property of hello group “Intune Administrators.”</span></span> <span data-ttu-id="7c32a-139">En primer lugar, estamos encontrando grupo hello mediante el cmdlet Get-AzureADGroup de Hola y de filtro mediante el atributo DisplayName de hello:</span><span class="sxs-lookup"><span data-stu-id="7c32a-139">First, we’re finding hello group using hello Get-AzureADGroup cmdlet and filter using hello DisplayName attribute:</span></span>

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

<span data-ttu-id="7c32a-140">A continuación, vamos a cambiar Hola descripción toohello nuevo valor de la propiedad "Administradores de dispositivos de Intune":</span><span class="sxs-lookup"><span data-stu-id="7c32a-140">Next, we’re changing hello Description property toohello new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="7c32a-141">Ahora si encontramos nuevo grupo de hello, vemos que la propiedad Description de hello es tooreflect actualizada Hola nuevo valor:</span><span class="sxs-lookup"><span data-stu-id="7c32a-141">Now if we find hello group again, we see hello Description property is updated tooreflect hello new value:</span></span>

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

## <a name="deleting-groups"></a><span data-ttu-id="7c32a-142">Eliminación de grupos</span><span class="sxs-lookup"><span data-stu-id="7c32a-142">Deleting groups</span></span>
<span data-ttu-id="7c32a-143">grupos de toodelete desde el directorio, use el cmdlet Remove-AzureADGroup de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="7c32a-143">toodelete groups from your directory, use hello Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="7c32a-144">Administración de miembros de grupos</span><span class="sxs-lookup"><span data-stu-id="7c32a-144">Managing members of groups</span></span>
<span data-ttu-id="7c32a-145">Si necesita tooadd nuevos miembros tooa grupo, usar el cmdlet de hello AzureADGroupMember agregar.</span><span class="sxs-lookup"><span data-stu-id="7c32a-145">If you need tooadd new members tooa group, use hello Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="7c32a-146">Este comando agrega un grupo de administradores de Intune de toohello de miembro que se utiliza en el ejemplo de Hola anterior:</span><span class="sxs-lookup"><span data-stu-id="7c32a-146">This command adds a member toohello Intune Administrators group we used in hello previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="7c32a-147">parámetro - ObjectId Hello es hello ObjectID de hello grupo toowhich queremos tooadd miembro y - RefObjectId hello es hello ObjectID del usuario de hello queremos tooadd como un grupo de toohello de miembro.</span><span class="sxs-lookup"><span data-stu-id="7c32a-147">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd a member, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as a member toohello group.</span></span>

<span data-ttu-id="7c32a-148">miembros existentes de hello tooget de un grupo, use el cmdlet Get-AzureADGroupMember de hello, como en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7c32a-148">tooget hello existing members of a group, use hello Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="7c32a-149">miembro de hello tooremove previamente agregamos toohello grupo, use el cmdlet Remove-AzureADGroupMember hello, tal y como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="7c32a-149">tooremove hello member we previously added toohello group, use hello Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="7c32a-150">tooverify Hola la cuenta de grupo de un usuario, use el cmdlet de Select AzureADGroupIdsUserIsMemberOf de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c32a-150">tooverify hello group membership(s) of a user, use hello Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="7c32a-151">Este cmdlet toma como sus parámetros Hola ObjectId del usuario de hello las pertenencias a grupos de hello toocheck y una lista de grupos de para qué pertenencias a grupos de toocheck Hola.</span><span class="sxs-lookup"><span data-stu-id="7c32a-151">This cmdlet takes as its parameters hello ObjectId of hello user for which toocheck hello group memberships, and a list of groups for which toocheck hello memberships.</span></span> <span data-ttu-id="7c32a-152">lista de Hola de grupos debe ser proporcionado en forma de Hola de una variable de complejo de tipo "Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck", por lo que primero debemos creamos una variable con ese tipo:</span><span class="sxs-lookup"><span data-stu-id="7c32a-152">hello list of groups must be provided in hello form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="7c32a-153">A continuación, se proporcionan valores de hello groupIds toocheck en atributo Hola "GroupIds" de esta variable complejo:</span><span class="sxs-lookup"><span data-stu-id="7c32a-153">Next, we provide values for hello groupIds toocheck in hello attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="7c32a-154">Ahora, si lo deseamos pertenencias a grupos de toocheck Hola de un usuario con ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea con los grupos de hello en $g, debemos usar:</span><span class="sxs-lookup"><span data-stu-id="7c32a-154">Now, if we want toocheck hello group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against hello groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="7c32a-155">valor de Hello devuelto es una lista de grupos de los cuales este usuario es miembro.</span><span class="sxs-lookup"><span data-stu-id="7c32a-155">hello value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="7c32a-156">También puede aplicar este toocheck método pertenencia contactos, grupos o entidades de servicio para una determinada lista de grupos, mediante Select-AzureADGroupIdsContactIsMemberOf, seleccione AzureADGroupIdsGroupIsMemberOf o Seleccione AzureADGroupIdsServicePrincipalIsMemberOf</span><span class="sxs-lookup"><span data-stu-id="7c32a-156">You can also apply this method toocheck Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="7c32a-157">Administración de propietarios de grupos</span><span class="sxs-lookup"><span data-stu-id="7c32a-157">Managing owners of groups</span></span>
<span data-ttu-id="7c32a-158">grupo tooa tooadd propietarios, use el cmdlet de hello AzureADGroupOwner agregar:</span><span class="sxs-lookup"><span data-stu-id="7c32a-158">tooadd owners tooa group, use hello Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="7c32a-159">parámetro - ObjectId Hello es hello ObjectID de hello grupo toowhich queremos tooadd un propietario y - RefObjectId hello es hello ObjectID del usuario de hello queremos tooadd como propietario del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c32a-159">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd an owner, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as an owner of hello group.</span></span>

<span data-ttu-id="7c32a-160">los propietarios de hello tooretrieve de un grupo, utilice cmdlet Get-AzureADGroupOwner de hello:</span><span class="sxs-lookup"><span data-stu-id="7c32a-160">tooretrieve hello owners of a group, use hello Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="7c32a-161">Hola cmdlet devuelve la lista de Hola de propietarios del grupo especificado de hello:</span><span class="sxs-lookup"><span data-stu-id="7c32a-161">hello cmdlet returns hello list of owners for hello specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="7c32a-162">Si desea tooremove un propietario de un grupo, utilice cmdlet Remove-AzureADGroupOwner de hello:</span><span class="sxs-lookup"><span data-stu-id="7c32a-162">If you want tooremove an owner from a group, use hello Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="7c32a-163">Alias reservados</span><span class="sxs-lookup"><span data-stu-id="7c32a-163">Reserved aliases</span></span> 
<span data-ttu-id="7c32a-164">Cuando se crea un grupo, determinados extremos permiten Hola usuario final toospecify un toobe mailNickname o alias que se usa como parte de la dirección de correo electrónico de saludo del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c32a-164">When a group is created, certain endpoints allow hello end user toospecify a mailNickname or alias toobe used as part of hello email address of hello group.</span></span> <span data-ttu-id="7c32a-165">Solo se pueden crear grupos con hello siguiendo el alias de correo electrónico con privilegios elevados por un administrador global de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c32a-165">Groups with hello following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="7c32a-166">abuse</span><span class="sxs-lookup"><span data-stu-id="7c32a-166">abuse</span></span> 
* <span data-ttu-id="7c32a-167">admin</span><span class="sxs-lookup"><span data-stu-id="7c32a-167">admin</span></span> 
* <span data-ttu-id="7c32a-168">administrator</span><span class="sxs-lookup"><span data-stu-id="7c32a-168">administrator</span></span> 
* <span data-ttu-id="7c32a-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="7c32a-169">hostmaster</span></span> 
* <span data-ttu-id="7c32a-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="7c32a-170">majordomo</span></span> 
* <span data-ttu-id="7c32a-171">postmaster</span><span class="sxs-lookup"><span data-stu-id="7c32a-171">postmaster</span></span> 
* <span data-ttu-id="7c32a-172">root</span><span class="sxs-lookup"><span data-stu-id="7c32a-172">root</span></span> 
* <span data-ttu-id="7c32a-173">secure</span><span class="sxs-lookup"><span data-stu-id="7c32a-173">secure</span></span> 
* <span data-ttu-id="7c32a-174">security</span><span class="sxs-lookup"><span data-stu-id="7c32a-174">security</span></span> 
* <span data-ttu-id="7c32a-175">ssl-admin</span><span class="sxs-lookup"><span data-stu-id="7c32a-175">ssl-admin</span></span> 
* <span data-ttu-id="7c32a-176">webmaster</span><span class="sxs-lookup"><span data-stu-id="7c32a-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7c32a-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7c32a-177">Next steps</span></span>
<span data-ttu-id="7c32a-178">Puede encontrar más documentación de Azure Active Directory PowerShell en el artículo sobre los [cmdlets de Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="7c32a-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="7c32a-179">Administrar acceso tooresources con grupos de Active Directory de Azure</span><span class="sxs-lookup"><span data-stu-id="7c32a-179">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="7c32a-180">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c32a-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
