---
title: "aaaProblem con acceso a la aplicación de autoservicio | Documentos de Microsoft"
description: "Solucionar problemas de acceso de la aplicación de servicio de tooself relacionada de problemas"
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
ms.openlocfilehash: 2487be1df191a4e7fd0bcc0ebbe4ea62fae0fd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="7ec56-103">Problemas al usar el acceso de autoservicio a las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7ec56-103">Problem using self-service application access</span></span>

<span data-ttu-id="7ec56-104">Acceso a la aplicación de autoservicio es una tooself de los usuarios de manera estupenda tooallow-detectar las aplicaciones, si lo desea permitir el acceso de tooapprove de grupo de negocios de hello toothose aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7ec56-104">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="7ec56-105">Puede permitir credenciales de Hola de hello business grupo toomanage asignan a usuarios toothose para derecho de inicio de sesión único en aplicaciones de contraseña de sus paneles de acceso.</span><span class="sxs-lookup"><span data-stu-id="7ec56-105">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="7ec56-106">Antes de que los usuarios pueden detectar automáticamente las aplicaciones de su panel de acceso, deberá tooenable **acceso a la aplicación de autoservicio** aplicaciones tooany que desea tooallow usuarios tooself-detectar y solicitar acceso a.</span><span class="sxs-lookup"><span data-stu-id="7ec56-106">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="7ec56-107">General emite toocheck primero</span><span class="sxs-lookup"><span data-stu-id="7ec56-107">General issues toocheck first</span></span>

-   <span data-ttu-id="7ec56-108">Asegúrese de que el acceso de autoservicio a las aplicaciones está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="7ec56-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="7ec56-109">Consulte "Cómo acceder aplicaciones de autoservicio de tooconfigure".</span><span class="sxs-lookup"><span data-stu-id="7ec56-109">See “How tooconfigure self-service application access”.</span></span>

-   <span data-ttu-id="7ec56-110">Asegúrese de que Hola usuario o grupo se ha habilitado el acceso de toorequest aplicación self-service.</span><span class="sxs-lookup"><span data-stu-id="7ec56-110">Make sure hello user or group has been enabled toorequest self-service application access.</span></span>

-   <span data-ttu-id="7ec56-111">Asegúrese de que el usuario Hola está visitando el lugar correcto de hello para el acceso a aplicaciones de autoservicio.</span><span class="sxs-lookup"><span data-stu-id="7ec56-111">Make sure hello user is visiting hello correct place for self-service application access.</span></span> <span data-ttu-id="7ec56-112">los usuarios pueden navegar tootheir [Panel de acceso de la aplicación](https://myapps.microsoft.com/) y haga clic en hello **+ agregar** botón toofind Hola aplicaciones toowhich ha habilitado el acceso de autoservicio.</span><span class="sxs-lookup"><span data-stu-id="7ec56-112">users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled self-service access.</span></span>

-   <span data-ttu-id="7ec56-113">Si recientemente se ha configurado el acceso a la aplicación de autoservicio, toosign de entrada y salida vuelva a intentarlo en el Panel de acceso del usuario de hello después de unos toosee minutos si han aparecido cambios de acceso de autoservicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ec56-113">If self-service application access was just recently configured, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello self-service access changes have appeared.</span></span>

## <a name="how-tooconfigure-self-service-application-access"></a><span data-ttu-id="7ec56-114">Cómo tener acceso aplicaciones de autoservicio de tooconfigure</span><span class="sxs-lookup"><span data-stu-id="7ec56-114">How tooconfigure self-service application access</span></span>

<span data-ttu-id="7ec56-115">aplicación de tooan de acceso de tooenable aplicación self-service, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="7ec56-115">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="7ec56-116">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="7ec56-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7ec56-117">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="7ec56-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7ec56-118">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="7ec56-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7ec56-119">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7ec56-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7ec56-120">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7ec56-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="7ec56-121">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="7ec56-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7ec56-122">Seleccionar aplicación hello desea tooenable acceso de autoservicio toofrom Hola lista.</span><span class="sxs-lookup"><span data-stu-id="7ec56-122">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="7ec56-123">Una vez que se carga la aplicación hello, haga clic en **self-service** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="7ec56-123">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7ec56-124">tooenable acceso a la aplicación de autoservicio para esta aplicación, activar hello **permitir que los usuarios de aplicación de toorequest access toothis?** alternar demasiado**sí.**</span><span class="sxs-lookup"><span data-stu-id="7ec56-124">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="7ec56-125">A continuación, tooselect Hola grupo toowhich los usuarios que solicitan acceso toothis aplicación debe agregarse, haga clic en siguiente toohello etiqueta de selector de hello **toowhich grupo debería asignar se agregan usuarios?** y seleccione un grupo.</span><span class="sxs-lookup"><span data-stu-id="7ec56-125">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="7ec56-126">**Opcional:** si desea que toorequire la aprobación de un negocio antes de que los usuarios tienen permiso de acceso, establezca hello **requieren aprobación antes de conceder acceso toothis aplicación?** alternar demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="7ec56-126">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="7ec56-127">**Opcional: para aplicaciones que utilizan la contraseña de inicio de sesión único en solo,** si desea que tooallow esas contraseñas hello toospecify de aprobadores empresariales que se envían toothis aplicación para los usuarios aprobados, establezca hello **permitir aprobadores tooset ¿contraseñas de usuario para esta aplicación?**  alternar demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="7ec56-127">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="7ec56-128">**Opcional:** toospecify Hola business aprobadores se permiten la aplicación de toothis de tooapprove access, haga clic en siguiente toohello etiqueta de selector de hello **que se permite la aplicación de tooapprove access toothis?** tooselect seguridad too10 aprobadores de negocios individuales.</span><span class="sxs-lookup"><span data-stu-id="7ec56-128">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="7ec56-129">No se admiten grupos.</span><span class="sxs-lookup"><span data-stu-id="7ec56-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="7ec56-130">**Opcional:** **para las aplicaciones que exponen funciones**, si desea que el rol de tooa de tooassign usuarios aprobados de autoservicio, haga clic en hello selector siguiente toohello **toowhich rol deben asignarse a los usuarios en este ¿aplicación?**  tooselect Hola rol toowhich se deben asignar estos usuarios.</span><span class="sxs-lookup"><span data-stu-id="7ec56-130">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="7ec56-131">Haga clic en hello **guardar** situado en la parte superior de Hola de hello hoja toofinish.</span><span class="sxs-lookup"><span data-stu-id="7ec56-131">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="7ec56-132">Cuando se haya completado la configuración de la aplicación de autoservicio, los usuarios pueden navegar tootheir [Panel de acceso de la aplicación](https://myapps.microsoft.com/) y haga clic en hello **+ agregar** botón toofind Hola aplicaciones toowhich ha habilitado Acceso de autoservicio.</span><span class="sxs-lookup"><span data-stu-id="7ec56-132">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="7ec56-133">Los aprobadores de la empresa pueden también ver una notificación en sus [paneles de acceso a las aplicaciones](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="7ec56-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="7ec56-134">Puede habilitar un correo electrónico que les informa de cuándo un usuario ha solicitado la aplicación de tooan de acceso que requiere su aprobación.</span><span class="sxs-lookup"><span data-stu-id="7ec56-134">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="7ec56-135">Estas aprobaciones admiten una aprobación única sólo flujos de trabajo, lo que significa que si especifica varios aprobadores, cualquier aprobador único puede aprobar aplicación toohello de access.</span><span class="sxs-lookup"><span data-stu-id="7ec56-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="7ec56-136">Si estos pasos no resuelven el problema de Hola</span><span class="sxs-lookup"><span data-stu-id="7ec56-136">If these troubleshooting steps do not resolve hello issue</span></span> 

<span data-ttu-id="7ec56-137">Abra una incidencia de soporte técnico con hello siguiente información si está disponible:</span><span class="sxs-lookup"><span data-stu-id="7ec56-137">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="7ec56-138">Id. de error de correlación</span><span class="sxs-lookup"><span data-stu-id="7ec56-138">Correlation error ID</span></span>

-   <span data-ttu-id="7ec56-139">UPN (dirección de correo electrónico del usuario)</span><span class="sxs-lookup"><span data-stu-id="7ec56-139">UPN (user email address)</span></span>

-   <span data-ttu-id="7ec56-140">TenantID</span><span class="sxs-lookup"><span data-stu-id="7ec56-140">TenantID</span></span>

-   <span data-ttu-id="7ec56-141">Tipo de explorador</span><span class="sxs-lookup"><span data-stu-id="7ec56-141">Browser type</span></span>

-   <span data-ttu-id="7ec56-142">Zona horaria y hora/período de tiempo durante el que se produce el error</span><span class="sxs-lookup"><span data-stu-id="7ec56-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="7ec56-143">Seguimientos de Fiddler</span><span class="sxs-lookup"><span data-stu-id="7ec56-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ec56-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7ec56-144">Next steps</span></span>
[<span data-ttu-id="7ec56-145">Configuración de Azure Active Directory para la administración de grupos de autoservicio</span><span class="sxs-lookup"><span data-stu-id="7ec56-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
