---
title: "Azure Active Directory Domain Services: introducción | Microsoft Docs"
description: "Habilitación de Azure Active Directory Domain Services mediante Azure Portal (versión preliminar)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: f87bcf33d3b1eb21c7d84814e4c4086f664e293d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="f4ec0-103">Habilitación de Azure Active Directory Domain Services mediante Azure Portal (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="f4ec0-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="f4ec0-104">Tarea 3: Configuración de un grupo administrativo</span><span class="sxs-lookup"><span data-stu-id="f4ec0-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="f4ec0-105">En esta tarea de configuración, se crea un grupo administrativo en el directorio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="f4ec0-106">Este grupo administrativo especial se llama *Administradores de DC de AAD*.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="f4ec0-107">A los miembros de este grupo se les conceden permisos administrativos en máquinas que estén unidas al domino administrado.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-107">Members of this group are granted administrative permissions on machines that are domain-joined to the managed domain.</span></span> <span data-ttu-id="f4ec0-108">En equipos unidos a un dominio, este grupo se agrega al grupo de administradores.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-108">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="f4ec0-109">Además, los miembros de este grupo también podrá usar Escritorio remoto para conectarse de forma remota a las máquinas unidas a un dominio.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-109">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="f4ec0-110">No tiene permisos de administrador de dominio o administrador de organización en el dominio administrado creado mediante Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-110">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="f4ec0-111">En los dominios administrados, estos permisos están reservados por el servicio y no están disponibles para los usuarios del inquilino.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-111">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="f4ec0-112">Sin embargo, puede usar el grupo administrativo especial creado en esta tarea de configuración para realizar algunas operaciones con privilegios.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-112">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="f4ec0-113">Estas operaciones incluyen unir equipos al dominio, formar parte del grupo de administradores en los equipos unidos a un dominio y configurar una directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-113">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="f4ec0-114">El asistente crea automáticamente el grupo administrativo en el directorio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-114">The wizard automatically creates the administrative group in your Azure AD directory.</span></span> <span data-ttu-id="f4ec0-115">Este grupo se llama "Administradores de DC de AAD".</span><span class="sxs-lookup"><span data-stu-id="f4ec0-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="f4ec0-116">Si tiene un grupo existente con este nombre en el directorio de Azure AD, el asistente lo selecciona.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-116">If you have an existing group with this name in your Azure AD directory, the wizard selects this group.</span></span> <span data-ttu-id="f4ec0-117">Puede configurar la pertenencia a grupos mediante la página **Grupo de administradores** del asistente.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-117">You can configure group membership using the **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="f4ec0-118">Para configurar la pertenencia a grupos, haga clic en **Administradores de DC de AAD**.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-118">To configure group membership, click **AAD DC Administrators**.</span></span>

    ![Configuración de la pertenencia a grupos](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="f4ec0-120">Haga clic en el botón **Agregar miembros** para agregar usuarios del directorio de Azure AD al grupo de administradores.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-120">Click the **Add members** button to add users from your Azure AD directory to the administrator group.</span></span>

3. <span data-ttu-id="f4ec0-121">Cuando haya terminado, haga clic en **Aceptar** para ir a la página **Resumen** del asistente.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-121">When you are done, click **OK** to move on to the **Summary** page of the wizard.</span></span>

4. <span data-ttu-id="f4ec0-122">En la página **Resumen** del asistente, revise la configuración del dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-122">On the **Summary** page of the wizard, review the configuration settings for the managed domain.</span></span> <span data-ttu-id="f4ec0-123">Puede volver a cualquier paso del asistente para realizar cambios, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-123">You can go back to any step of the wizard to make changes, if necessary.</span></span> <span data-ttu-id="f4ec0-124">Cuando haya terminado, haga clic en **Aceptar** para crear el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-124">When you are done, click **OK** to create the new managed domain.</span></span>

    ![Resumen](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="f4ec0-126">Verá una notificación que muestra el progreso de la implementación de la instancia de Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-126">You see a notification that shows the progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="f4ec0-127">Haga clic en la notificación para ver el progreso detallado de la implementación.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-127">Click the notification to see detailed progress for the deployment.</span></span>

    ![Notificación: implementación en curso](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="f4ec0-129">Aprovisionamiento del dominio administrado</span><span class="sxs-lookup"><span data-stu-id="f4ec0-129">Provision your managed domain</span></span>
<span data-ttu-id="f4ec0-130">El proceso de aprovisionamiento del dominio administrado puede tardar hasta una hora.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-130">The process of provisioning your managed domain can take up to an hour.</span></span>

1. <span data-ttu-id="f4ec0-131">Mientras la implementación está en curso, puede buscar "servicios de dominio" en el cuadro de búsqueda **buscar recursos**.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-131">While your deployment is in progress, you can search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="f4ec0-132">En el resultado de la búsqueda, seleccione **Azure AD Domain Services**.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-132">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="f4ec0-133">La hoja **Azure AD Domain Services** muestra el dominio administrado que se está aprovisionando.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-133">The **Azure AD Domain Services** blade lists the managed domain that is being provisioned.</span></span>

    ![Búsqueda del dominio administrado que se va aprovisionar](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="f4ec0-135">Haga clic en el nombre del dominio administrado (por ejemplo, "contoso100.com") para ver más detalles sobre el dominio.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-135">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Domain Services: estado de aprovisionamiento](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="f4ec0-137">La pestaña **Información general** muestra que el dominio se está aprovisionando.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-137">The **Overview** tab shows that the domain is currently being provisioned.</span></span> <span data-ttu-id="f4ec0-138">No se puede configurar el dominio administrado hasta que está aprovisionado por completo.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-138">You cannot configure the managed domain until it is fully provisioned.</span></span> <span data-ttu-id="f4ec0-139">El dominio administrado puede tardar una hora en aprovisionarse por completo.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-139">It may take up to an hour for your managed domain to be fully provisioned.</span></span>

    ![<span data-ttu-id="f4ec0-140">Domain Services: pestaña Información general durante el estado de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="f4ec0-140">Domain Services - Overview tab during the provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="f4ec0-141">Cuando el dominio administrado está aprovisionado por completo, la pestaña **Información general** muestra el estado del dominio como **En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-141">When the managed domain is fully provisioned, the **Overview** tab shows the domain status as **Running**.</span></span>

    ![Domain Services: pestaña Información general después del aprovisionamiento completo](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="f4ec0-143">En la pestaña **Propiedades**, se ven dos direcciones IP en las que hay controladores de dominio disponibles para Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="f4ec0-143">On the **Properties** tab, you see two IP addresses at which domain controllers are available for the virtual network.</span></span>

    ![Domain Services: pestaña Propiedades después del aprovisionamiento completo](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="f4ec0-145">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="f4ec0-145">Next step</span></span>
[<span data-ttu-id="f4ec0-146">Tarea 4: Actualización de la configuración DNS en Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="f4ec0-146">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
