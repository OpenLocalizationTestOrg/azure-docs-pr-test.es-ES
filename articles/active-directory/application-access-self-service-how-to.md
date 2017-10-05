---
title: "Configuración de la asignación a la aplicación de autoservicio | Microsoft Docs"
description: Habilitar el acceso de autoservicio a las aplicaciones para permitir a los usuarios buscar sus propias aplicaciones
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7991dc19d41c5eb8e149c3ee08069e1a162929cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-self-service-application-assignment"></a><span data-ttu-id="d26dd-103">Configuración de la asignación a la aplicación de autoservicio</span><span class="sxs-lookup"><span data-stu-id="d26dd-103">How to configure self-service application assignment</span></span>

<span data-ttu-id="d26dd-104">Antes de que los usuarios puedan detectar automáticamente las aplicaciones de su panel de acceso, debe habilitar el **acceso de autoservicio a las aplicaciones** de cualquier aplicación que desee permitir que los usuarios puedan detectar automáticamente y solicitar acceso a ella.</span><span class="sxs-lookup"><span data-stu-id="d26dd-104">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

<span data-ttu-id="d26dd-105">Esta característica es una excelente manera de ahorrar tiempo y dinero como grupo de TI y es muy recomendable como parte de una implementación de aplicaciones moderna con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d26dd-105">This feature is a great way for you to save time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="d26dd-106">Con esta característica, puede:</span><span class="sxs-lookup"><span data-stu-id="d26dd-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="d26dd-107">Permitir que los usuarios detecten automáticamente las aplicaciones desde el [panel de acceso a las aplicaciones](https://myapps.microsoft.com/) sin molestar al grupo de TI.</span><span class="sxs-lookup"><span data-stu-id="d26dd-107">Let users self-discover applications from the [Application Access Panel](https://myapps.microsoft.com/) without bothering the IT group.</span></span>

-   <span data-ttu-id="d26dd-108">Agregar esos usuarios a un grupo preconfigurado para que pueda ver quién ha solicitado acceso, quitar el acceso y administrar los roles que tienen asignados.</span><span class="sxs-lookup"><span data-stu-id="d26dd-108">Add those users to a pre-configured group so you can see who has requested access, remove access, and manage the roles assigned to them.</span></span>

-   <span data-ttu-id="d26dd-109">Si lo desea, puede permitir que un aprobador de la empresa apruebe las solicitudes de acceso a la aplicación para que no tenga que hacerlo el grupo de TI.</span><span class="sxs-lookup"><span data-stu-id="d26dd-109">Optionally allow a business approver to approve application access requests so the IT group doesn’t have to.</span></span>

-   <span data-ttu-id="d26dd-110">También puede configurar un máximo de 10 usuarios que pueden aprobar el acceso a esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="d26dd-110">Optionally configure up to 10 individuals who may approve access to this application.</span></span>

-   <span data-ttu-id="d26dd-111">Permitir que un aprobador de la empresa establezca las contraseñas que los usuarios pueden usar para iniciar sesión en la aplicación directamente desde el [panel de acceso a las aplicaciones](https://myapps.microsoft.com/) del aprobador.</span><span class="sxs-lookup"><span data-stu-id="d26dd-111">Optionally allow a business approver to set the passwords those users can use to sign in to the application, right from the business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="d26dd-112">Asignar automáticamente usuarios asignados de autoservicio directamente a un rol de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d26dd-112">Optionally automatically assign self-service assigned users to an application role directly.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="d26dd-113">Habilitar el acceso de autoservicio a las aplicaciones para permitir a los usuarios buscar sus propias aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d26dd-113">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="d26dd-114">El acceso de autoservicio a las aplicaciones es una excelente manera de permitir a los usuarios detectar automáticamente aplicaciones y, si lo desea, permitir que el grupo de negocios apruebe el acceso a esas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d26dd-114">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="d26dd-115">Puede permitir que el grupo de negocios administre las credenciales asignadas a esos usuarios para que puedan realizar un inicio de sesión único con contraseña en las aplicaciones directamente desde sus paneles de acceso.</span><span class="sxs-lookup"><span data-stu-id="d26dd-115">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="d26dd-116">Para habilitar el acceso de autoservicio a las aplicaciones, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d26dd-116">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="d26dd-117">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="d26dd-117">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d26dd-118">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="d26dd-118">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d26dd-119">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d26dd-119">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d26dd-120">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d26dd-120">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d26dd-121">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d26dd-121">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="d26dd-122">Si no ve que la aplicación que desea aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="d26dd-122">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="d26dd-123">Seleccione la aplicación en la que desea habilitar el acceso de autoservicio de la lista.</span><span class="sxs-lookup"><span data-stu-id="d26dd-123">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="d26dd-124">Cuando se cargue la aplicación, haga clic en **Autoservicio** en el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d26dd-124">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d26dd-125">Para habilitar el acceso de autoservicio a las aplicaciones para esta aplicación, establezca la opción **¿Quiere permitir que los usuarios soliciten acceso a esta aplicación?** en **Sí.**</span><span class="sxs-lookup"><span data-stu-id="d26dd-125">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="d26dd-126">A continuación, seleccione el grupo al que se deben agregar los usuarios que solicitan acceso a esta aplicación, haga clic en el selector situado junto a la etiqueta **¿A qué grupo se deberían agregar los usuarios asignados?** y seleccione un grupo.</span><span class="sxs-lookup"><span data-stu-id="d26dd-126">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="d26dd-127">**Opcional:** si desea requerir la aprobación de la empresa antes de permitir el acceso a los usuarios, establezca la opción **¿Quiere requerir una aprobación para conceder acceso a esta aplicación?** en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="d26dd-127">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="d26dd-128">**Opcional: para las aplicaciones que solo utilizan el inicio de sesión único con contraseña,** si desea permitir que los aprobadores de la empresa especifiquen las contraseñas que se envían a esta aplicación para los usuarios aprobados, establezca la opción **¿Quiere permitir que los aprobadores establezcan las contraseñas de los usuarios de esta aplicación?** en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="d26dd-128">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="d26dd-129">**Opcional:** para especificar los aprobadores de la empresa que tienen permiso para aprobar el acceso a esta aplicación, haga clic en el selector situado junto a la etiqueta **¿Quién tiene permiso para aprobar el acceso a esta aplicación?** para seleccionar hasta 10 aprobadores individuales de la empresa.</span><span class="sxs-lookup"><span data-stu-id="d26dd-129">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

   >[!NOTE]
   ><span data-ttu-id="d26dd-130">No se admiten grupos.</span><span class="sxs-lookup"><span data-stu-id="d26dd-130">Groups are not supported.</span></span>
   >
   >

13. <span data-ttu-id="d26dd-131">**Opcional:** **para las aplicaciones que exponen roles**, si desea asignar usuarios aprobados de autoservicio a un rol, haga clic en el selector situado junto a la etiqueta **¿A qué rol deben asignarse los usuarios de esta aplicación?** para seleccionar el rol al que se deben asignar estos usuarios.</span><span class="sxs-lookup"><span data-stu-id="d26dd-131">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="d26dd-132">Haga clic en el botón **Guardar** de la parte superior de la hoja para terminar.</span><span class="sxs-lookup"><span data-stu-id="d26dd-132">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="d26dd-133">Cuando se haya completado la configuración de la aplicación de autoservicio, los usuarios pueden navegar a sus [paneles de acceso a las aplicaciones](https://myapps.microsoft.com/) y hacer clic en el botón **+ Agregar** para buscar las aplicaciones para las que se ha habilitado el acceso de autoservicio.</span><span class="sxs-lookup"><span data-stu-id="d26dd-133">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="d26dd-134">Los aprobadores de la empresa pueden también ver una notificación en sus [paneles de acceso a las aplicaciones](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="d26dd-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="d26dd-135">Puede habilitar un correo electrónico que les informa cuando un usuario ha solicitado el acceso a una aplicación que requiere su aprobación.</span><span class="sxs-lookup"><span data-stu-id="d26dd-135">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="d26dd-136">Estas aprobaciones admiten flujos de trabajo de aprobación única, lo que significa que si especifica varios aprobadores, cualquier aprobador individual puede aprobar el acceso a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d26dd-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d26dd-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d26dd-137">Next steps</span></span>
[<span data-ttu-id="d26dd-138">Configuración de Azure Active Directory para la administración de grupos de autoservicio</span><span class="sxs-lookup"><span data-stu-id="d26dd-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
