---
title: "Administración de grupos en Azure Active Directory | Microsoft Docs"
description: "Cómo crear y administrar grupos para administrar usuarios de Azure mediante Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 2cc2b63312b331a19c61cd7b59a4cac78edf32e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="managing-groups-in-azure-active-directory"></a><span data-ttu-id="ecacd-103">Administración de grupos en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ecacd-103">Managing groups in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ecacd-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ecacd-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="ecacd-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="ecacd-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="ecacd-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecacd-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="ecacd-107">Una de las características de la administración de usuarios de Azure Active Directory (Azure AD) es la capacidad para crear grupos de usuarios.</span><span class="sxs-lookup"><span data-stu-id="ecacd-107">One of the features of Azure Active Directory (Azure AD) user management is the ability to create groups of users.</span></span> <span data-ttu-id="ecacd-108">Los grupos se usan para realizar tareas de administración, como asignar licencias o permisos a varios usuarios a la vez.</span><span class="sxs-lookup"><span data-stu-id="ecacd-108">You use a group to perform management tasks such as assigning licenses or permissions to a number of users at once.</span></span> <span data-ttu-id="ecacd-109">También puede usarlos para asignar permiso de acceso a:</span><span class="sxs-lookup"><span data-stu-id="ecacd-109">You can also use groups to assign access permission to</span></span>

* <span data-ttu-id="ecacd-110">Recursos, como objetos en el directorio;</span><span class="sxs-lookup"><span data-stu-id="ecacd-110">Resources such as objects in the directory</span></span>
* <span data-ttu-id="ecacd-111">Recursos de fuera del directorio, como aplicaciones de SaaS, servicios de Azure, sitios de SharePoint o recursos locales.</span><span class="sxs-lookup"><span data-stu-id="ecacd-111">Resources external to the directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span></span>

<span data-ttu-id="ecacd-112">Además, el propietario de un recurso también puede asignar acceso a un recurso a un grupo de Azure AD cuyo propietario sea otro usuario.</span><span class="sxs-lookup"><span data-stu-id="ecacd-112">In addition, a resource owner can also assign access to a resource to an Azure AD group owned by someone else.</span></span> <span data-ttu-id="ecacd-113">La asignación otorga acceso al recurso a los miembros de dicho grupo.</span><span class="sxs-lookup"><span data-stu-id="ecacd-113">This assignment grants the members of that group access to the resource.</span></span> <span data-ttu-id="ecacd-114">A continuación, el propietario del grupo administra la pertenencia al grupo.</span><span class="sxs-lookup"><span data-stu-id="ecacd-114">Then, the owner of the group manages membership in the group.</span></span> <span data-ttu-id="ecacd-115">El propietario del recurso delega efectivamente en el propietario del grupo el permiso para asignar usuarios a sus recursos.</span><span class="sxs-lookup"><span data-stu-id="ecacd-115">Effectively, the resource owner delegates to the owner of the group the permission to assign users to their resource.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ecacd-116">Microsoft recomienda administrar Azure AD con el [Centro de administración de Azure AD](https://aad.portal.azure.com) en Azure Portal en lugar de usar el portal de Azure clásico al que se hace referencia en este artículo.</span><span class="sxs-lookup"><span data-stu-id="ecacd-116">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="ecacd-117">Para administrar grupos en el Centro de administración de Azure AD, consulte [Creación de un grupo y adición de miembros en Azure Active Directory](active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ecacd-117">For how to manage groups in the Azure AD admin center, see [Create a group and add members in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="ecacd-118">¿Cómo se crea un grupo?</span><span class="sxs-lookup"><span data-stu-id="ecacd-118">How do I create a group?</span></span>
<span data-ttu-id="ecacd-119">En función de los servicios a los que se haya suscrito su organización, podrá crear grupos mediante:</span><span class="sxs-lookup"><span data-stu-id="ecacd-119">Depending on the services to which your organization has subscribed, you can create a group using one of the following:</span></span>

* <span data-ttu-id="ecacd-120">el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="ecacd-120">the Azure classic portal</span></span>
* <span data-ttu-id="ecacd-121">el portal de cuentas de Office 365</span><span class="sxs-lookup"><span data-stu-id="ecacd-121">the Office 365 account portal</span></span>
* <span data-ttu-id="ecacd-122">el portal de cuentas de Windows Intune</span><span class="sxs-lookup"><span data-stu-id="ecacd-122">the Windows Intune account portal</span></span>

<span data-ttu-id="ecacd-123">Aquí se describirán las tareas tal como se realizan en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="ecacd-123">We'll describe tasks as performed in the Azure classic portal.</span></span> <span data-ttu-id="ecacd-124">Para más información acerca del uso de portales que no sean el de Azure para administrar un directorio de Azure AD, consulte [Administración del directorio de Azure AD](active-directory-administer.md).</span><span class="sxs-lookup"><span data-stu-id="ecacd-124">For more information about using non-Azure portals to manage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span></span>

1. <span data-ttu-id="ecacd-125">En el [Portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y, luego, el nombre del directorio de la organización.</span><span class="sxs-lookup"><span data-stu-id="ecacd-125">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="ecacd-126">Seleccione la pestaña **Grupos** .</span><span class="sxs-lookup"><span data-stu-id="ecacd-126">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="ecacd-127">Seleccione **Agregar grupo**.</span><span class="sxs-lookup"><span data-stu-id="ecacd-127">Select **Add Group**.</span></span>
4. <span data-ttu-id="ecacd-128">En la ventana **Agregar grupo** , especifique el nombre y la descripción de un grupo.</span><span class="sxs-lookup"><span data-stu-id="ecacd-128">In the **Add Group** window, specify the name and the description of a group.</span></span>

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a><span data-ttu-id="ecacd-129">Asignación o eliminación de usuarios individuales de un grupo de seguridad</span><span class="sxs-lookup"><span data-stu-id="ecacd-129">How do I add or remove individual users in a security group?</span></span>
<span data-ttu-id="ecacd-130">**Para agregar un usuario individual a un grupo**</span><span class="sxs-lookup"><span data-stu-id="ecacd-130">**To add an individual user to a group**</span></span>

1. <span data-ttu-id="ecacd-131">En el [Portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y, luego, el nombre del directorio de la organización.</span><span class="sxs-lookup"><span data-stu-id="ecacd-131">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="ecacd-132">Seleccione la pestaña **Grupos** .</span><span class="sxs-lookup"><span data-stu-id="ecacd-132">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="ecacd-133">Abra el grupo al que desea agregar miembros.</span><span class="sxs-lookup"><span data-stu-id="ecacd-133">Open the group to which you want to add members.</span></span> <span data-ttu-id="ecacd-134">Abra la pestaña **Miembros** del grupo seleccionado, en caso de que no se muestre.</span><span class="sxs-lookup"><span data-stu-id="ecacd-134">Open the **Members** tab of the selected group if it not already displaying.</span></span>
4. <span data-ttu-id="ecacd-135">Seleccione **Agregar miembros**.</span><span class="sxs-lookup"><span data-stu-id="ecacd-135">Select **Add Members**.</span></span>
5. <span data-ttu-id="ecacd-136">En la página **Agregar miembros** , seleccione el nombre del usuario o el grupo que desee agregar como miembro de este grupo.</span><span class="sxs-lookup"><span data-stu-id="ecacd-136">On the **Add Members** page, select the name of the user or a group that you want to add as a member of this group.</span></span> <span data-ttu-id="ecacd-137">Asegúrese de que este nombre se agrega al panel **Seleccionado** .</span><span class="sxs-lookup"><span data-stu-id="ecacd-137">Make sure that this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="ecacd-138">**Para quitar un usuario individual de un grupo**</span><span class="sxs-lookup"><span data-stu-id="ecacd-138">**To remove an individual user from a group**</span></span>

1. <span data-ttu-id="ecacd-139">En el [Portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y, luego, el nombre del directorio de la organización.</span><span class="sxs-lookup"><span data-stu-id="ecacd-139">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="ecacd-140">Seleccione la pestaña **Grupos** .</span><span class="sxs-lookup"><span data-stu-id="ecacd-140">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="ecacd-141">Abra el grupo del que desea quitar miembros.</span><span class="sxs-lookup"><span data-stu-id="ecacd-141">Open the group from which you want to remove members.</span></span>
4. <span data-ttu-id="ecacd-142">Seleccione la pestaña **Miembros**, seleccione el nombre del miembro que desee quitar de este grupo y haga clic en **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="ecacd-142">Select the **Members** tab, select the name of the member that you want to remove from this group, and then click **Remove**.</span></span>
5. <span data-ttu-id="ecacd-143">En el símbolo del sistema, confirme que desea quitar este miembro del grupo.</span><span class="sxs-lookup"><span data-stu-id="ecacd-143">Confirm at the prompt that you want to remove this member from the group.</span></span>

## <a name="how-can-i-manage-the-membership-of-a-group-dynamically"></a><span data-ttu-id="ecacd-144">¿Cómo puedo administrar la pertenencia de un grupo dinámicamente?</span><span class="sxs-lookup"><span data-stu-id="ecacd-144">How can I manage the membership of a group dynamically?</span></span>
<span data-ttu-id="ecacd-145">En Azure AD, puede configurar fácilmente una regla sencilla que determine qué usuarios van a ser miembros del grupo.</span><span class="sxs-lookup"><span data-stu-id="ecacd-145">In Azure AD, you can very easily set up a simple rule to determine which users are to be members of the group.</span></span> <span data-ttu-id="ecacd-146">Una regla sencilla es aquélla que hace solo una comparación única.</span><span class="sxs-lookup"><span data-stu-id="ecacd-146">A simple rule is one that makes only a single comparison.</span></span> <span data-ttu-id="ecacd-147">Por ejemplo, si se asigna un grupo a una aplicación SaaS, puede configurar una regla que agregue los usuarios que tengan el puesto "Representante de ventas".</span><span class="sxs-lookup"><span data-stu-id="ecacd-147">For example, if a group is assigned to a SaaS application, you can set up a rule to add users who have a job title of "Sales Rep."</span></span> <span data-ttu-id="ecacd-148">Esta regla otorga acceso a esta aplicación SaaS a todos los usuarios del directorio que tengan dicho puesto.</span><span class="sxs-lookup"><span data-stu-id="ecacd-148">This rule then grants access to this SaaS application to all users with that job title in your directory.</span></span>

<span data-ttu-id="ecacd-149">Cuando los atributos de un usuario cambian, el sistema evalúa todas las reglas de grupos dinámicos de un directorio para ver si la modificación de los atributos del usuario en cuestión desencadenaría adiciones o retiradas en el grupo.</span><span class="sxs-lookup"><span data-stu-id="ecacd-149">When any attributes of a user change, the system evaluates all dynamic group rules in a directory to see if the attribute change of the user would trigger any group adds or removes.</span></span> <span data-ttu-id="ecacd-150">Si un usuario cumple una regla de un grupo, se agrega a este como miembro.</span><span class="sxs-lookup"><span data-stu-id="ecacd-150">If a user satisfies a rule on a group, they are added as a member to that group.</span></span> <span data-ttu-id="ecacd-151">Si, por el contrario, deja de cumplir la regla del grupo al que pertenece, se le quita como miembro de este.</span><span class="sxs-lookup"><span data-stu-id="ecacd-151">If they no longer satisfy the rule of a group they are a member of, they are removed as a members from that group.</span></span>

> [!NOTE]
> <span data-ttu-id="ecacd-152">Puede configurar una regla de pertenencia dinámica a grupos de seguridad o en grupos de Office 365.</span><span class="sxs-lookup"><span data-stu-id="ecacd-152">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span> <span data-ttu-id="ecacd-153">Actualmente, las pertenencias a grupos anidados no son compatibles con la asignación basada en grupos a aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ecacd-153">Nested group memberships aren't currently supported for group-based assignment to applications.</span></span>
>
> <span data-ttu-id="ecacd-154">La pertenencia dinámica a grupos requiere que haya una licencia de Azure AD Premium asignada</span><span class="sxs-lookup"><span data-stu-id="ecacd-154">Dynamic memberships for groups require an Azure AD Premium license to be assigned to</span></span>
>
> * <span data-ttu-id="ecacd-155">Al administrador que administra la regla en un grupo</span><span class="sxs-lookup"><span data-stu-id="ecacd-155">The administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="ecacd-156">Todos los miembros del grupo</span><span class="sxs-lookup"><span data-stu-id="ecacd-156">All members of the group</span></span>
>
>

<span data-ttu-id="ecacd-157">**Para habilitar la pertenencia dinámica para un grupo**</span><span class="sxs-lookup"><span data-stu-id="ecacd-157">**To enable dynamic membership for a group**</span></span>

1. <span data-ttu-id="ecacd-158">En el [Portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y, luego, el nombre del directorio de la organización.</span><span class="sxs-lookup"><span data-stu-id="ecacd-158">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="ecacd-159">Seleccione la pestaña **Grupos** y abra el grupo que desee editar.</span><span class="sxs-lookup"><span data-stu-id="ecacd-159">Select the **Groups** tab, and open the group you want to edit.</span></span>
3. <span data-ttu-id="ecacd-160">Seleccione la pestaña **Configurar** y en **Habilitar pertenencia dinámica**, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="ecacd-160">Select the **Configure** tab, and then set **Enable Dynamic Memberships** to **Yes**.</span></span>
4. <span data-ttu-id="ecacd-161">Configure una sola regla sencilla para que el grupo controle el funcionamiento de la pertenencia dinámica para este grupo.</span><span class="sxs-lookup"><span data-stu-id="ecacd-161">Set up a simple single rule for the group to control how dynamic membership for this group functions.</span></span> <span data-ttu-id="ecacd-162">Asegúrese de que la opción **Agregar usuarios donde** está seleccionada y, a continuación, seleccione una propiedad de usuario en la lista (por ejemplo, department, jobTitle, etc.).</span><span class="sxs-lookup"><span data-stu-id="ecacd-162">Make sure the **Add users where** option is selected, and then select a user property from the list (for example, department, jobTitle, etc.),</span></span>
5. <span data-ttu-id="ecacd-163">A continuación, seleccione una condición (No es igual a, Es igual a, No empieza por, Empieza por, No contiene, Contiene, No coincide, Coincide).</span><span class="sxs-lookup"><span data-stu-id="ecacd-163">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span></span>
6. <span data-ttu-id="ecacd-164">Especifique un valor de comparación para la propiedad de usuario seleccionada.</span><span class="sxs-lookup"><span data-stu-id="ecacd-164">Specify a comparison value for the selected user property.</span></span>

<span data-ttu-id="ecacd-165">Para obtener información acerca de cómo crear reglas *avanzadas* (reglas que pueden contener comparaciones múltiples) para la pertenencia a grupos dinámicos, consulte [Uso de atributos para crear reglas avanzadas](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="ecacd-165">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="ecacd-166">Información adicional</span><span class="sxs-lookup"><span data-stu-id="ecacd-166">Additional information</span></span>
<span data-ttu-id="ecacd-167">Estos artículos proporcionan información adicional sobre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ecacd-167">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="ecacd-168">Administración del acceso a los recursos con grupos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ecacd-168">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="ecacd-169">Cmdlets de Azure Active Directory para configurar las opciones de grupo</span><span class="sxs-lookup"><span data-stu-id="ecacd-169">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="ecacd-170">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ecacd-170">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="ecacd-171">¿Qué es Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ecacd-171">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="ecacd-172">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ecacd-172">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
