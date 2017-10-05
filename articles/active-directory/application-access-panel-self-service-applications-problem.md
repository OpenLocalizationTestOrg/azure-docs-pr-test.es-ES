---
title: Problemas al usar el acceso de autoservicio a las aplicaciones | Microsoft Docs
description: Solucionar problemas relacionados con el acceso de autoservicio a las aplicaciones
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
ms.reviewer: japere
ms.openlocfilehash: 217726709a1fdb02275de5a76a1352ea9c350600
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="35af5-103">Problemas al usar el acceso de autoservicio a las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="35af5-103">Problem using self-service application access</span></span>

<span data-ttu-id="35af5-104">El acceso de autoservicio a las aplicaciones es una excelente manera de permitir a los usuarios detectar automáticamente aplicaciones y, si lo desea, permitir que el grupo de negocios apruebe el acceso a esas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="35af5-104">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="35af5-105">Puede permitir que el grupo de negocios administre las credenciales asignadas a esos usuarios para que puedan realizar un inicio de sesión único con contraseña en las aplicaciones directamente desde sus paneles de acceso.</span><span class="sxs-lookup"><span data-stu-id="35af5-105">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="35af5-106">Antes de que los usuarios puedan detectar automáticamente las aplicaciones de su panel de acceso, debe habilitar el **acceso de autoservicio a las aplicaciones** de cualquier aplicación que desee permitir que los usuarios puedan detectar automáticamente y solicitar acceso a ella.</span><span class="sxs-lookup"><span data-stu-id="35af5-106">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="35af5-107">Problemas generales para comprobar primero</span><span class="sxs-lookup"><span data-stu-id="35af5-107">General issues to check first</span></span>

-   <span data-ttu-id="35af5-108">Asegúrese de que el acceso de autoservicio a las aplicaciones está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="35af5-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="35af5-109">Consulte "Configuración del acceso de autoservicio a las aplicaciones".</span><span class="sxs-lookup"><span data-stu-id="35af5-109">See “How to configure self-service application access”.</span></span>

-   <span data-ttu-id="35af5-110">Asegúrese de que se ha habilitado al usuario o grupo para solicitar el acceso de autoservicio a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="35af5-110">Make sure the user or group has been enabled to request self-service application access.</span></span>

-   <span data-ttu-id="35af5-111">Asegúrese de que el usuario está visitando el lugar correcto para el acceso de autoservicio a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="35af5-111">Make sure the user is visiting the correct place for self-service application access.</span></span> <span data-ttu-id="35af5-112">Los usuarios pueden navegar a sus [paneles de acceso a las aplicaciones](https://myapps.microsoft.com/) y hacer clic en el botón **+ Agregar** para buscar las aplicaciones para las que se ha habilitado el acceso de autoservicio.</span><span class="sxs-lookup"><span data-stu-id="35af5-112">users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled self-service access.</span></span>

-   <span data-ttu-id="35af5-113">Si ha configurado recientemente el acceso de autoservicio a las aplicaciones, intente iniciar sesión y cerrar sesión en el panel de acceso del usuario después de unos minutos para ver si los cambios del acceso de autoservicio han aparecido.</span><span class="sxs-lookup"><span data-stu-id="35af5-113">If self-service application access was just recently configured, try to sign in and out again into the user’s Access Panel after a few minutes to see if the self-service access changes have appeared.</span></span>

## <a name="how-to-configure-self-service-application-access"></a><span data-ttu-id="35af5-114">Configuración del acceso de autoservicio a las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="35af5-114">How to configure self-service application access</span></span>

<span data-ttu-id="35af5-115">Para habilitar el acceso de autoservicio a las aplicaciones, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="35af5-115">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="35af5-116">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="35af5-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="35af5-117">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="35af5-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="35af5-118">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="35af5-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="35af5-119">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="35af5-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="35af5-120">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="35af5-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="35af5-121">Si no ve que la aplicación que desea aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="35af5-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="35af5-122">Seleccione la aplicación en la que desea habilitar el acceso de autoservicio de la lista.</span><span class="sxs-lookup"><span data-stu-id="35af5-122">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="35af5-123">Cuando se cargue la aplicación, haga clic en **Autoservicio** en el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="35af5-123">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="35af5-124">Para habilitar el acceso de autoservicio a las aplicaciones para esta aplicación, establezca la opción **¿Quiere permitir que los usuarios soliciten acceso a esta aplicación?** en **Sí.**</span><span class="sxs-lookup"><span data-stu-id="35af5-124">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="35af5-125">A continuación, seleccione el grupo al que se deben agregar los usuarios que solicitan acceso a esta aplicación, haga clic en el selector situado junto a la etiqueta **¿A qué grupo se deberían agregar los usuarios asignados?** y seleccione un grupo.</span><span class="sxs-lookup"><span data-stu-id="35af5-125">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="35af5-126">**Opcional:** si desea requerir la aprobación de la empresa antes de permitir el acceso a los usuarios, establezca la opción **¿Quiere requerir una aprobación para conceder acceso a esta aplicación?** en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="35af5-126">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="35af5-127">**Opcional: para las aplicaciones que solo utilizan el inicio de sesión único con contraseña,** si desea permitir que los aprobadores de la empresa especifiquen las contraseñas que se envían a esta aplicación para los usuarios aprobados, establezca la opción **¿Quiere permitir que los aprobadores establezcan las contraseñas de los usuarios de esta aplicación?** en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="35af5-127">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="35af5-128">**Opcional:** para especificar los aprobadores de la empresa que tienen permiso para aprobar el acceso a esta aplicación, haga clic en el selector situado junto a la etiqueta **¿Quién tiene permiso para aprobar el acceso a esta aplicación?** para seleccionar hasta 10 aprobadores individuales de la empresa.</span><span class="sxs-lookup"><span data-stu-id="35af5-128">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="35af5-129">No se admiten grupos.</span><span class="sxs-lookup"><span data-stu-id="35af5-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="35af5-130">**Opcional:** **para las aplicaciones que exponen roles**, si desea asignar usuarios aprobados de autoservicio a un rol, haga clic en el selector situado junto a la etiqueta **¿A qué rol deben asignarse los usuarios de esta aplicación?** para seleccionar el rol al que se deben asignar estos usuarios.</span><span class="sxs-lookup"><span data-stu-id="35af5-130">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="35af5-131">Haga clic en el botón **Guardar** de la parte superior de la hoja para terminar.</span><span class="sxs-lookup"><span data-stu-id="35af5-131">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="35af5-132">Cuando se haya completado la configuración de la aplicación de autoservicio, los usuarios pueden navegar a sus [paneles de acceso a las aplicaciones](https://myapps.microsoft.com/) y hacer clic en el botón **+ Agregar** para buscar las aplicaciones para las que se ha habilitado el acceso de autoservicio.</span><span class="sxs-lookup"><span data-stu-id="35af5-132">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="35af5-133">Los aprobadores de la empresa pueden también ver una notificación en sus [paneles de acceso a las aplicaciones](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="35af5-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="35af5-134">Puede habilitar un correo electrónico que les informa cuando un usuario ha solicitado el acceso a una aplicación que requiere su aprobación.</span><span class="sxs-lookup"><span data-stu-id="35af5-134">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="35af5-135">Estas aprobaciones solo admiten flujos de trabajo de aprobación única, lo que significa que, si especifica varios aprobadores, cualquier aprobador individual puede aprobar el acceso a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="35af5-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="35af5-136">Si después de seguir estos pasos el problema no se ha resuelto,</span><span class="sxs-lookup"><span data-stu-id="35af5-136">If these troubleshooting steps do not resolve the issue</span></span> 

<span data-ttu-id="35af5-137">abra una incidencia de soporte técnico con la información siguiente si está disponible:</span><span class="sxs-lookup"><span data-stu-id="35af5-137">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="35af5-138">Id. de error de correlación</span><span class="sxs-lookup"><span data-stu-id="35af5-138">Correlation error ID</span></span>

-   <span data-ttu-id="35af5-139">UPN (dirección de correo electrónico del usuario)</span><span class="sxs-lookup"><span data-stu-id="35af5-139">UPN (user email address)</span></span>

-   <span data-ttu-id="35af5-140">TenantID</span><span class="sxs-lookup"><span data-stu-id="35af5-140">TenantID</span></span>

-   <span data-ttu-id="35af5-141">Tipo de explorador</span><span class="sxs-lookup"><span data-stu-id="35af5-141">Browser type</span></span>

-   <span data-ttu-id="35af5-142">Zona horaria y hora/período de tiempo durante el que se produce el error</span><span class="sxs-lookup"><span data-stu-id="35af5-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="35af5-143">Seguimientos de Fiddler</span><span class="sxs-lookup"><span data-stu-id="35af5-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="35af5-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="35af5-144">Next steps</span></span>
[<span data-ttu-id="35af5-145">Configuración de Azure Active Directory para la administración de grupos de autoservicio</span><span class="sxs-lookup"><span data-stu-id="35af5-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
