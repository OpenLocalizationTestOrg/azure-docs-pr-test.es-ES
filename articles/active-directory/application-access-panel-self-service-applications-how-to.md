---
title: acceso a las aplicaciones de autoservicio aaaHow toouse | Documentos de Microsoft
description: "Habilitar aplicación self-service acceso tooallow usuarios toofind sus propias aplicaciones"
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
ms.openlocfilehash: 03a44c20d544a6232fa802bcffaf70e5030ad3ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-self-service-application-access"></a><span data-ttu-id="46014-103">Cómo tener acceso aplicaciones de autoservicio de toouse</span><span class="sxs-lookup"><span data-stu-id="46014-103">How toouse self-service application access</span></span>

<span data-ttu-id="46014-104">Antes de que los usuarios pueden detectar automáticamente las aplicaciones de su panel de acceso, deberá tooenable **acceso a la aplicación de autoservicio** aplicaciones tooany que desea tooallow usuarios tooself-detectar y solicitar acceso a.</span><span class="sxs-lookup"><span data-stu-id="46014-104">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

<span data-ttu-id="46014-105">Esta característica es una excelente manera de toosave tiempo y dinero como un grupo de TI y se recomienda encarecidamente como parte de una implementación de aplicaciones modernas con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46014-105">This feature is a great way for you toosave time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="46014-106">Con esta característica, puede:</span><span class="sxs-lookup"><span data-stu-id="46014-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="46014-107">Permitir que los usuarios detectar automáticamente las aplicaciones de hello [Panel de acceso de la aplicación](https://myapps.microsoft.com/) sin molestarle Hola TI grupo.</span><span class="sxs-lookup"><span data-stu-id="46014-107">Let users self-discover applications from hello [Application Access Panel](https://myapps.microsoft.com/) without bothering hello IT group.</span></span>

-   <span data-ttu-id="46014-108">Agregue esos grupo preconfigurada de tooa de usuarios para que pueda ver que ha solicitado el acceso, quitar el acceso y administrar roles de hello asignados toothem.</span><span class="sxs-lookup"><span data-stu-id="46014-108">Add those users tooa pre-configured group so you can see who has requested access, remove access, and manage hello roles assigned toothem.</span></span>

-   <span data-ttu-id="46014-109">Si lo desea permitir que un aprobador empresariales las solicitudes de acceso de aplicación tooapprove para que hello grupo de TI no tiene que.</span><span class="sxs-lookup"><span data-stu-id="46014-109">Optionally allow a business approver tooapprove application access requests so hello IT group doesn’t have to.</span></span>

-   <span data-ttu-id="46014-110">Opcionalmente, configure hasta too10 personas pueden aprobar aplicación toothis de access.</span><span class="sxs-lookup"><span data-stu-id="46014-110">Optionally configure up too10 individuals who may approve access toothis application.</span></span>

-   <span data-ttu-id="46014-111">Si lo desea permitir un aprobador business contraseñas de hello tooset estos usuarios pueden utilizar toosign en aplicación toohello, directamente desde del aprobador Hola business [Panel de acceso de la aplicación](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="46014-111">Optionally allow a business approver tooset hello passwords those users can use toosign in toohello application, right from hello business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="46014-112">Si lo desea asignar rol de aplicación de los usuarios asignados autoservicio tooan directamente.</span><span class="sxs-lookup"><span data-stu-id="46014-112">Optionally automatically assign self-service assigned users tooan application role directly.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="46014-113">Habilitar aplicación self-service acceso tooallow usuarios toofind sus propias aplicaciones</span><span class="sxs-lookup"><span data-stu-id="46014-113">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="46014-114">Acceso a la aplicación de autoservicio es una tooself de los usuarios de manera estupenda tooallow-detectar las aplicaciones, si lo desea permitir el acceso de tooapprove de grupo de negocios de hello toothose aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="46014-114">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="46014-115">Puede permitir credenciales de Hola de hello business grupo toomanage asignan a usuarios toothose para derecho de inicio de sesión único en aplicaciones de contraseña de sus paneles de acceso.</span><span class="sxs-lookup"><span data-stu-id="46014-115">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="46014-116">aplicación de tooan de acceso de tooenable aplicación self-service, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="46014-116">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="46014-117">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="46014-117">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="46014-118">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="46014-118">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="46014-119">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="46014-119">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="46014-120">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46014-120">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="46014-121">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="46014-121">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="46014-122">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="46014-122">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="46014-123">Seleccionar aplicación hello desea tooenable acceso de autoservicio toofrom Hola lista.</span><span class="sxs-lookup"><span data-stu-id="46014-123">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="46014-124">Una vez que se carga la aplicación hello, haga clic en **self-service** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="46014-124">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="46014-125">tooenable acceso a la aplicación de autoservicio para esta aplicación, activar hello **permitir que los usuarios de aplicación de toorequest access toothis?** alternar demasiado**sí.**</span><span class="sxs-lookup"><span data-stu-id="46014-125">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="46014-126">A continuación, tooselect Hola grupo toowhich los usuarios que solicitan acceso toothis aplicación debe agregarse, haga clic en siguiente toohello etiqueta de selector de hello **toowhich grupo debería asignar se agregan usuarios?** y seleccione un grupo.</span><span class="sxs-lookup"><span data-stu-id="46014-126">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="46014-127">**Opcional:** si desea que toorequire la aprobación de un negocio antes de que los usuarios tienen permiso de acceso, establezca hello **requieren aprobación antes de conceder acceso toothis aplicación?** alternar demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="46014-127">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="46014-128">**Opcional: para aplicaciones que utilizan la contraseña de inicio de sesión único en solo,** si desea que tooallow esas contraseñas hello toospecify de aprobadores empresariales que se envían toothis aplicación para los usuarios aprobados, establezca hello **permitir aprobadores tooset ¿contraseñas de usuario para esta aplicación?**  alternar demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="46014-128">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="46014-129">**Opcional:** toospecify Hola business aprobadores se permiten la aplicación de toothis de tooapprove access, haga clic en siguiente toohello etiqueta de selector de hello **que se permite la aplicación de tooapprove access toothis?** tooselect seguridad too10 aprobadores de negocios individuales.</span><span class="sxs-lookup"><span data-stu-id="46014-129">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

   * <span data-ttu-id="46014-130">No se admiten grupos.</span><span class="sxs-lookup"><span data-stu-id="46014-130">Groups are not supported.</span></span>

13. <span data-ttu-id="46014-131">**Opcional:** **para las aplicaciones que exponen funciones**, si desea que el rol de tooa de tooassign usuarios aprobados de autoservicio, haga clic en hello selector siguiente toohello **toowhich rol deben asignarse a los usuarios en este ¿aplicación?**  tooselect Hola rol toowhich se deben asignar estos usuarios.</span><span class="sxs-lookup"><span data-stu-id="46014-131">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="46014-132">Haga clic en hello **guardar** situado en la parte superior de Hola de hello hoja toofinish.</span><span class="sxs-lookup"><span data-stu-id="46014-132">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="46014-133">Cuando se haya completado la configuración de la aplicación de autoservicio, los usuarios pueden navegar tootheir [Panel de acceso de la aplicación](https://myapps.microsoft.com/) y haga clic en hello **+ agregar** botón toofind Hola aplicaciones toowhich ha habilitado Acceso de autoservicio.</span><span class="sxs-lookup"><span data-stu-id="46014-133">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="46014-134">Los aprobadores de la empresa pueden también ver una notificación en sus [paneles de acceso a las aplicaciones](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="46014-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="46014-135">Puede habilitar un correo electrónico que les informa de cuándo un usuario ha solicitado la aplicación de tooan de acceso que requiere su aprobación.</span><span class="sxs-lookup"><span data-stu-id="46014-135">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="46014-136">Estas aprobaciones admiten una aprobación única sólo flujos de trabajo, lo que significa que si especifica varios aprobadores, cualquier aprobador único puede aprobar aplicación toohello de access.</span><span class="sxs-lookup"><span data-stu-id="46014-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46014-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46014-137">Next steps</span></span>
[<span data-ttu-id="46014-138">Configuración de Azure Active Directory para la administración de grupos de autoservicio</span><span class="sxs-lookup"><span data-stu-id="46014-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
