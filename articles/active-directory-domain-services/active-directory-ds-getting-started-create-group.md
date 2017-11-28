---
title: "Azure Active Directory Domain Services: Creación del grupo de administradores de controlador de dominio de Azure AD | Microsoft Docs"
description: "Habilitación de Azure Active Directory Domain Services mediante el Portal de Azure clásico"
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
ms.openlocfilehash: 5ed0125e05928cf0f6d9941e099b433ecb46e6e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a><span data-ttu-id="f7612-103">Habilitación de Azure Active Directory Domain Services mediante el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="f7612-103">Enable Azure Active Directory Domain Services using the Azure classic portal</span></span>
<span data-ttu-id="f7612-104">Este artículo describe y le guía por las tareas de configuración que son necesarias para habilitar Azure Active Directory Domain Services (Azure AD DS) para su inquilino de Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f7612-104">This article describes and walks through the configuration tasks that are required for you to enable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="f7612-105">[**Pruebe la nueva experiencia de Azure Portal (versión preliminar) en su lugar**](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="f7612-105">[**Try the new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-the-azure-ad-dc-administrators-group"></a><span data-ttu-id="f7612-106">Tarea 1: Creación del grupo de administradores de controlador de dominio de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7612-106">Task 1: create the Azure AD DC administrators group</span></span>
<span data-ttu-id="f7612-107">Esta primera tarea consiste en crear un grupo administrativo en el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7612-107">The first task is to create an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="f7612-108">Este grupo administrativo especial se llama *Administradores de DC de AAD*.</span><span class="sxs-lookup"><span data-stu-id="f7612-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="f7612-109">A los miembros de este grupo se les concederán permisos administrativos en los equipos unidos al domino administrado en Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="f7612-109">Members of this group are granted administrative permissions on machines that are domain-joined to the Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="f7612-110">En equipos unidos a un dominio, este grupo se agrega al grupo de administradores.</span><span class="sxs-lookup"><span data-stu-id="f7612-110">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="f7612-111">Además, los miembros de este grupo también podrá usar Escritorio remoto para conectarse de forma remota a las máquinas unidas a un dominio.</span><span class="sxs-lookup"><span data-stu-id="f7612-111">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="f7612-112">No tiene permisos de administrador de dominio o administrador de organización en el dominio administrado creado mediante Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="f7612-112">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="f7612-113">En los dominios administrados, estos permisos están reservados por el servicio y no están disponibles para los usuarios del inquilino.</span><span class="sxs-lookup"><span data-stu-id="f7612-113">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="f7612-114">Sin embargo, puede usar el grupo administrativo especial creado en esta tarea de configuración para realizar algunas operaciones con privilegios.</span><span class="sxs-lookup"><span data-stu-id="f7612-114">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="f7612-115">Estas operaciones incluyen unir equipos al dominio, formar parte del grupo de administradores en los equipos unidos a un dominio y configurar una directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="f7612-115">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="f7612-116">En esta tarea de configuración, creará el grupo administrativo y agregará uno o varios usuarios del directorio al grupo.</span><span class="sxs-lookup"><span data-stu-id="f7612-116">In this configuration task, you create the administrative group and add one or more users in your directory to the group.</span></span> <span data-ttu-id="f7612-117">Para crear el grupo administrativo para Azure Active Directory Domain Services, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f7612-117">To create the administrative group for Azure Active Directory Domain Services, do the following:</span></span>

1. <span data-ttu-id="f7612-118">Vaya al [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="f7612-118">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="f7612-119">En el panel izquierdo, seleccione el botón **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f7612-119">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="f7612-120">Seleccione el inquilino (directorio) de Azure AD para el que quiere habilitar Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="f7612-120">Select the Azure AD tenant (directory) for which you want to enable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="f7612-121">Puede crear un único dominio para cada directorio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7612-121">You can create only one domain for each Azure AD directory.</span></span>

    ![Selección de un directorio de Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="f7612-123">En la página del **directorio de vista previa**, haga clic en la pestaña **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="f7612-123">On the **preview directory** page, click the **Groups** tab.</span></span>
5. <span data-ttu-id="f7612-124">Para agregar un grupo a su inquilino de Azure AD, en el panel de tareas en la parte inferior de la ventana, haga clic en **Agregar grupo**.</span><span class="sxs-lookup"><span data-stu-id="f7612-124">To add a group to your Azure AD tenant, on the task pane at the bottom of the window, click **Add Group**.</span></span>

    ![Botón Agregar grupo](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="f7612-126">En el cuadro de diálogo **Agregar grupo**, cree un grupo denominado **Administradores de controlador de dominio de AAD** y, a continuación, establezca **Tipo de grupo** en **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="f7612-126">In the **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** to **Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="f7612-127">Para permitir el acceso dentro de su dominio administrado de Azure Active Directory Domain Services, cree un grupo con este nombre exacto.</span><span class="sxs-lookup"><span data-stu-id="f7612-127">To enable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![Cuadro de diálogo Agregar grupo](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="f7612-129">En el cuadro **Descripción**, escriba una descripción que permita que otras personas entiendan que este grupo concede permisos administrativos en Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="f7612-129">In the **Description** box, enter a description that enables others to understand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="f7612-130">Después de crear el grupo, haga clic en el nombre del grupo para ver sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="f7612-130">After you've created the group, click the group name to view its properties.</span></span>
9. <span data-ttu-id="f7612-131">Para agregar usuarios como miembros del grupo, en la parte inferior de la ventana, haga clic en el botón **Agregar miembros**.</span><span class="sxs-lookup"><span data-stu-id="f7612-131">To add users as members of the group, at the bottom of the window, click the **Add Members** button.</span></span>

    ![Botón Agregar miembros del grupo](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="f7612-133">En el cuadro de diálogo **Agregar miembros**, seleccione los usuarios que deben ser miembros de este grupo y, a continuación, haga clic la marca de verificación en la esquina inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="f7612-133">In the **Add members** dialog box, select the users who should be members of this group, and then click the checkmark icon at the lower right.</span></span>

    ![Agregar usuarios al grupo de administradores](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="f7612-135">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="f7612-135">Next step</span></span>
<span data-ttu-id="f7612-136">Tarea 2: [Creación o selección de una red virtual de Azure](active-directory-ds-getting-started-vnet.md)</span><span class="sxs-lookup"><span data-stu-id="f7612-136">[Task 2: create or select an Azure virtual network](active-directory-ds-getting-started-vnet.md)</span></span>
