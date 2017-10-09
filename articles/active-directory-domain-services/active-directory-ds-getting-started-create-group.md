---
title: 'Azure Active Directory Domain Services: Crear el grupo de administradores de controlador de dominio de hello Azure AD | Documentos de Microsoft'
description: "Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure clásico"
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
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="8ab43-103">Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="8ab43-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>
<span data-ttu-id="8ab43-104">Este artículo describe y le guía a través de las tareas de configuración de Hola que necesita tooenable Azure Active Directory Domain Services (Azure AD DS) para su inquilino de Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ab43-104">This article describes and walks through hello configuration tasks that are required for you tooenable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="8ab43-105">[**Pruebe en su lugar hello (versión preliminar) Azure experiencia del nuevo portal**](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="8ab43-105">[**Try hello new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a><span data-ttu-id="8ab43-106">Tarea 1: crear el grupo de administradores de controlador de dominio de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ab43-106">Task 1: create hello Azure AD DC administrators group</span></span>
<span data-ttu-id="8ab43-107">Hola primera tarea es toocreate un grupo administrativo en el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ab43-107">hello first task is toocreate an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="8ab43-108">Este grupo administrativo especial se llama *Administradores de DC de AAD*.</span><span class="sxs-lookup"><span data-stu-id="8ab43-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="8ab43-109">Miembros de este grupo se conceden permisos administrativos en los equipos que están en el dominio de servicios de dominio de Active Directory de Azure administrados toohello Unidos a un dominio.</span><span class="sxs-lookup"><span data-stu-id="8ab43-109">Members of this group are granted administrative permissions on machines that are domain-joined toohello Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="8ab43-110">En equipos unidos a un dominio, este grupo se agrega el grupo de administradores de toohello.</span><span class="sxs-lookup"><span data-stu-id="8ab43-110">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="8ab43-111">Además, los miembros de este grupo pueden utilizar Escritorio remoto tooconnect remotamente toodomain-equipos unidos a un.</span><span class="sxs-lookup"><span data-stu-id="8ab43-111">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="8ab43-112">No tiene permisos de administrador de dominio o administrador de organización en el dominio administrado Hola que ha creado mediante el uso de servicios de dominio de Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab43-112">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="8ab43-113">En los dominios administrados, estos permisos están reservados por el servicio de hello y no están disponibles toousers dentro de inquilino de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ab43-113">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="8ab43-114">Sin embargo, puede utilizar grupo administrativo especial Hola creado en este tooperform de tareas de configuración algunas operaciones privilegiadas.</span><span class="sxs-lookup"><span data-stu-id="8ab43-114">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="8ab43-115">Estas operaciones incluyen unirse a dominio de equipos toohello, que pertenece el grupo de administración de toohello en equipos unidos a un dominio y la configuración de directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="8ab43-115">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="8ab43-116">En esta tarea de configuración, cree el grupo administrativo de Hola y agregar uno o más usuarios en el grupo de toohello de directorio.</span><span class="sxs-lookup"><span data-stu-id="8ab43-116">In this configuration task, you create hello administrative group and add one or more users in your directory toohello group.</span></span> <span data-ttu-id="8ab43-117">grupo administrativo de hello toocreate para Azure Active Directory Domain Services Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="8ab43-117">toocreate hello administrative group for Azure Active Directory Domain Services, do hello following:</span></span>

1. <span data-ttu-id="8ab43-118">Vaya toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="8ab43-118">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="8ab43-119">En el panel izquierdo de hello, seleccione hello **Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="8ab43-119">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="8ab43-120">Seleccione el inquilino de Azure AD de hello (directorio) para el que desea que los servicios de dominio de Active Directory de tooenable Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab43-120">Select hello Azure AD tenant (directory) for which you want tooenable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="8ab43-121">Puede crear un único dominio para cada directorio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ab43-121">You can create only one domain for each Azure AD directory.</span></span>

    ![Selección de un directorio de Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="8ab43-123">En hello **directorio de vista previa** página, haga clic en hello **grupos** ficha.</span><span class="sxs-lookup"><span data-stu-id="8ab43-123">On hello **preview directory** page, click hello **Groups** tab.</span></span>
5. <span data-ttu-id="8ab43-124">Haga clic en un inquilino de Azure AD tooyour grupo, en panel de tareas de hello en parte inferior de Hola de ventana hello, de tooadd **Agregar grupo**.</span><span class="sxs-lookup"><span data-stu-id="8ab43-124">tooadd a group tooyour Azure AD tenant, on hello task pane at hello bottom of hello window, click **Add Group**.</span></span>

    ![botón Agregar grupo de Hola](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="8ab43-126">Hola **Agregar grupo** diálogo cuadro, cree un grupo denominado **administradores de controlador de dominio de AAD**y, a continuación, establezca **tipo de grupo** demasiado**seguridad**.</span><span class="sxs-lookup"><span data-stu-id="8ab43-126">In hello **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** too**Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="8ab43-127">acceso de tooenable dentro de su dominio administrado en servicios de dominio de Active Directory de Azure, cree un grupo con este nombre exacto.</span><span class="sxs-lookup"><span data-stu-id="8ab43-127">tooenable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![cuadro de diálogo Agregar grupo de Hola](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="8ab43-129">Hola **descripción** cuadro, escriba una descripción que permite a otros toounderstand que este grupo concede permisos administrativos en servicios de dominio de Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab43-129">In hello **Description** box, enter a description that enables others toounderstand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="8ab43-130">Después de crear el grupo de hello, haga clic en tooview de nombre de grupo de hello sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="8ab43-130">After you've created hello group, click hello group name tooview its properties.</span></span>
9. <span data-ttu-id="8ab43-131">tooadd usuarios como miembros del grupo de hello, en parte inferior de Hola de ventana hello, haga clic en hello **agregar miembros** botón.</span><span class="sxs-lookup"><span data-stu-id="8ab43-131">tooadd users as members of hello group, at hello bottom of hello window, click hello **Add Members** button.</span></span>

    ![Botón Agregar miembros del grupo](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="8ab43-133">Hola **agregar miembros** cuadro de diálogo, seleccione Hola quienes deben ser miembros de este grupo y, a continuación, haga clic en el icono de marca de verificación de hello en hello inferior derecho.</span><span class="sxs-lookup"><span data-stu-id="8ab43-133">In hello **Add members** dialog box, select hello users who should be members of this group, and then click hello checkmark icon at hello lower right.</span></span>

    ![Agregar grupo de usuarios tooadministrators](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="8ab43-135">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="8ab43-135">Next step</span></span>
<span data-ttu-id="8ab43-136">Tarea 2: [Creación o selección de una red virtual de Azure](active-directory-ds-getting-started-vnet.md)</span><span class="sxs-lookup"><span data-stu-id="8ab43-136">[Task 2: create or select an Azure virtual network](active-directory-ds-getting-started-vnet.md)</span></span>
