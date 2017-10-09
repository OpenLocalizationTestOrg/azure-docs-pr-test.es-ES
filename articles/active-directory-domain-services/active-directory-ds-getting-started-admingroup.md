---
title: "Azure Active Directory Domain Services: introducción | Microsoft Docs"
description: Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure (vista previa)
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
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="302da-103">Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure (vista previa)</span><span class="sxs-lookup"><span data-stu-id="302da-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="302da-104">Tarea 3: Configuración de un grupo administrativo</span><span class="sxs-lookup"><span data-stu-id="302da-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="302da-105">En esta tarea de configuración, se crea un grupo administrativo en el directorio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="302da-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="302da-106">Este grupo administrativo especial se llama *Administradores de DC de AAD*.</span><span class="sxs-lookup"><span data-stu-id="302da-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="302da-107">Miembros de este grupo se conceden permisos administrativos en los equipos que están unidos al dominio toohello de dominio administrados.</span><span class="sxs-lookup"><span data-stu-id="302da-107">Members of this group are granted administrative permissions on machines that are domain-joined toohello managed domain.</span></span> <span data-ttu-id="302da-108">En equipos unidos a un dominio, este grupo se agrega el grupo de administradores de toohello.</span><span class="sxs-lookup"><span data-stu-id="302da-108">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="302da-109">Además, los miembros de este grupo pueden utilizar Escritorio remoto tooconnect remotamente toodomain-equipos unidos a un.</span><span class="sxs-lookup"><span data-stu-id="302da-109">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="302da-110">No tiene permisos de administrador de dominio o administrador de organización en el dominio administrado Hola que ha creado mediante el uso de servicios de dominio de Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="302da-110">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="302da-111">En los dominios administrados, estos permisos están reservados por el servicio de hello y no están disponibles toousers dentro de inquilino de Hola.</span><span class="sxs-lookup"><span data-stu-id="302da-111">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="302da-112">Sin embargo, puede utilizar grupo administrativo especial Hola creado en este tooperform de tareas de configuración algunas operaciones privilegiadas.</span><span class="sxs-lookup"><span data-stu-id="302da-112">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="302da-113">Estas operaciones incluyen unirse a dominio de equipos toohello, que pertenece el grupo de administración de toohello en equipos unidos a un dominio y la configuración de directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="302da-113">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="302da-114">Asistente de Hello crea automáticamente grupo administrativo de hello en su directorio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="302da-114">hello wizard automatically creates hello administrative group in your Azure AD directory.</span></span> <span data-ttu-id="302da-115">Este grupo se llama "Administradores de DC de AAD".</span><span class="sxs-lookup"><span data-stu-id="302da-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="302da-116">Si tiene un grupo existente con este nombre en el directorio de Azure AD, el Asistente de hello selecciona este grupo.</span><span class="sxs-lookup"><span data-stu-id="302da-116">If you have an existing group with this name in your Azure AD directory, hello wizard selects this group.</span></span> <span data-ttu-id="302da-117">Puede configurar la pertenencia a grupos con hello **grupo de administradores** página del asistente.</span><span class="sxs-lookup"><span data-stu-id="302da-117">You can configure group membership using hello **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="302da-118">pertenencia a grupos de tooconfigure, haga clic en **administradores de controlador de dominio de AAD**.</span><span class="sxs-lookup"><span data-stu-id="302da-118">tooconfigure group membership, click **AAD DC Administrators**.</span></span>

    ![Configuración de la pertenencia a grupos](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="302da-120">Haga clic en hello **agregar miembros** botón tooadd a los usuarios de su grupo de administradores de toohello de directorio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="302da-120">Click hello **Add members** button tooadd users from your Azure AD directory toohello administrator group.</span></span>

3. <span data-ttu-id="302da-121">Cuando haya terminado, haga clic en **Aceptar** toomove en toohello **resumen** página del Asistente para saludo.</span><span class="sxs-lookup"><span data-stu-id="302da-121">When you are done, click **OK** toomove on toohello **Summary** page of hello wizard.</span></span>

4. <span data-ttu-id="302da-122">En hello **resumen** página del Asistente de hello, revisión Hola de configuración de dominio administrados Hola.</span><span class="sxs-lookup"><span data-stu-id="302da-122">On hello **Summary** page of hello wizard, review hello configuration settings for hello managed domain.</span></span> <span data-ttu-id="302da-123">Puede volver atrás paso tooany de cambios de hello Asistente toomake, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="302da-123">You can go back tooany step of hello wizard toomake changes, if necessary.</span></span> <span data-ttu-id="302da-124">Cuando haya terminado, haga clic en **Aceptar** toocreate Hola administrado nuevo dominio.</span><span class="sxs-lookup"><span data-stu-id="302da-124">When you are done, click **OK** toocreate hello new managed domain.</span></span>

    ![Resumen](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="302da-126">Verá una notificación que muestra el progreso de saludo de la implementación de servicios de dominio de AD de Azure.</span><span class="sxs-lookup"><span data-stu-id="302da-126">You see a notification that shows hello progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="302da-127">Haga clic en la notificación de hello toosee detallada progreso para la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="302da-127">Click hello notification toosee detailed progress for hello deployment.</span></span>

    ![Notificación: implementación en curso](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="302da-129">Aprovisionamiento del dominio administrado</span><span class="sxs-lookup"><span data-stu-id="302da-129">Provision your managed domain</span></span>
<span data-ttu-id="302da-130">proceso de Hola de aprovisionar el dominio administrado puede tardar hasta hora tooan.</span><span class="sxs-lookup"><span data-stu-id="302da-130">hello process of provisioning your managed domain can take up tooan hour.</span></span>

1. <span data-ttu-id="302da-131">Mientras que la implementación está en curso, puede buscar "servicios de dominio' en hello **buscar recursos** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="302da-131">While your deployment is in progress, you can search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="302da-132">Seleccione **servicios de dominio de AD de Azure** Hola resultados de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="302da-132">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="302da-133">Hola **servicios de dominio de AD de Azure** hoja muestra hello dominio administrado que se está aprovisionando.</span><span class="sxs-lookup"><span data-stu-id="302da-133">hello **Azure AD Domain Services** blade lists hello managed domain that is being provisioned.</span></span>

    ![Búsqueda del dominio administrado que se va aprovisionar](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="302da-135">Haga clic en Hola Hola administrado toosee de dominio (por ejemplo, ' contoso100.com') para obtener más detalles sobre el dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="302da-135">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Domain Services: estado de aprovisionamiento](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="302da-137">Hola **Introducción** ficha muestra ese dominio de saludo se está aprovisionando actualmente.</span><span class="sxs-lookup"><span data-stu-id="302da-137">hello **Overview** tab shows that hello domain is currently being provisioned.</span></span> <span data-ttu-id="302da-138">No se puede configurar dominio administrado Hola hasta que está aprovisionado por completo.</span><span class="sxs-lookup"><span data-stu-id="302da-138">You cannot configure hello managed domain until it is fully provisioned.</span></span> <span data-ttu-id="302da-139">Puede llevar hasta hora tooan para su toobe de dominio administrados aprovisionado por completo.</span><span class="sxs-lookup"><span data-stu-id="302da-139">It may take up tooan hour for your managed domain toobe fully provisioned.</span></span>

    ![<span data-ttu-id="302da-140">Servicios de dominio - ficha información general durante Hola estado de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="302da-140">Domain Services - Overview tab during hello provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="302da-141">Cuando el dominio administrado Hola está aprovisionado por completo, Hola **información general sobre** ficha muestra el estado del dominio de hello como **ejecutando**.</span><span class="sxs-lookup"><span data-stu-id="302da-141">When hello managed domain is fully provisioned, hello **Overview** tab shows hello domain status as **Running**.</span></span>

    ![Domain Services: pestaña Información general después del aprovisionamiento completo](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="302da-143">En hello **propiedades** ficha, verá dos direcciones IP en el dominio que están disponibles para la red virtual de hello controladores.</span><span class="sxs-lookup"><span data-stu-id="302da-143">On hello **Properties** tab, you see two IP addresses at which domain controllers are available for hello virtual network.</span></span>

    ![Domain Services: pestaña Propiedades después del aprovisionamiento completo](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="302da-145">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="302da-145">Next step</span></span>
[<span data-ttu-id="302da-146">Tarea 4: actualizar la configuración de DNS de Hola de hello red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="302da-146">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
