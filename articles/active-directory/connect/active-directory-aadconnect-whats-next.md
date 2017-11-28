---
title: "Azure AD Connect: Pasos siguientes y cómo toomanage Azure AD Connect | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooextend Hola tareas operativas y la configuración predeterminada de Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a><span data-ttu-id="6d897-103">Pasos siguientes y cómo toomanage Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="6d897-103">Next steps and how toomanage Azure AD Connect</span></span>
<span data-ttu-id="6d897-104">Utilice los procedimientos operativos hello en este toomeet de artículo toocustomize Connect de Azure Active Directory (Azure AD) necesidades y los requisitos de su organización.</span><span class="sxs-lookup"><span data-stu-id="6d897-104">Use hello operational procedures in this article toocustomize Azure Active Directory (Azure AD) Connect toomeet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="6d897-105">Pasos para agregar administradores de sincronización adicionales</span><span class="sxs-lookup"><span data-stu-id="6d897-105">Add additional sync admins</span></span>
<span data-ttu-id="6d897-106">De forma predeterminada, solo usuario Hola que Hola instalación y administradores locales son toomanage capaz de motor de sincronización de hello instalado.</span><span class="sxs-lookup"><span data-stu-id="6d897-106">By default, only hello user who did hello installation and local admins are able toomanage hello installed sync engine.</span></span> <span data-ttu-id="6d897-107">Para otras personas toobe capaz de tooaccess y administrar el motor de sincronización de hello, busque grupo Hola denominada ADSyncAdmins en el servidor local de Hola y agréguelos toothis grupo.</span><span class="sxs-lookup"><span data-stu-id="6d897-107">For additional people toobe able tooaccess and manage hello sync engine, locate hello group named ADSyncAdmins on hello local server and add them toothis group.</span></span>

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="6d897-108">Asignar licencias tooAzure usuarios de AD Premium y Enterprise Mobility Suite</span><span class="sxs-lookup"><span data-stu-id="6d897-108">Assign licenses tooAzure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="6d897-109">Ahora que los usuarios han estado sincronizado toohello en la nube, necesita tooassign ellos una licencia por lo que pueden empezar a trabajar con aplicaciones de nube, como Office 365.</span><span class="sxs-lookup"><span data-stu-id="6d897-109">Now that your users have been synchronized toohello cloud, you need tooassign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="6d897-110">tooassign una Azure AD Premium o licencia de Enterprise Mobility Suite</span><span class="sxs-lookup"><span data-stu-id="6d897-110">tooassign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="6d897-111">Inicie sesión en toohello portal de Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="6d897-111">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="6d897-112">Hola izquierda, seleccione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d897-112">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="6d897-113">En hello **Active Directory** página, haga doble clic en el directorio de Hola que tiene usuarios de Hola que desee tooset seguridad.</span><span class="sxs-lookup"><span data-stu-id="6d897-113">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="6d897-114">Hola parte superior de página de directorio de hello, seleccione **licencias**.</span><span class="sxs-lookup"><span data-stu-id="6d897-114">At hello top of hello directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="6d897-115">En hello **licencias** página, seleccione **Active Directory Premium** o **Enterprise Mobility Suite**y, a continuación, haga clic en **asignar**.</span><span class="sxs-lookup"><span data-stu-id="6d897-115">On hello **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="6d897-116">En el cuadro de diálogo de hello, seleccione los usuarios que desee tooassign licencias y, a continuación, haga clic en hello marca de verificación icono toosave Hola cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d897-116">In hello dialog box, select hello users you want tooassign licenses to, and then click hello check mark icon toosave hello changes.</span></span>

## <a name="verify-hello-scheduled-synchronization-task"></a><span data-ttu-id="6d897-117">Comprobar la tarea de sincronización programada de Hola</span><span class="sxs-lookup"><span data-stu-id="6d897-117">Verify hello scheduled synchronization task</span></span>
<span data-ttu-id="6d897-118">Utilizar el estado de Hola de hello toocheck portal Azure de una sincronización.</span><span class="sxs-lookup"><span data-stu-id="6d897-118">Use hello Azure portal toocheck hello status of a synchronization.</span></span>

### <a name="tooverify-hello-scheduled-synchronization-task"></a><span data-ttu-id="6d897-119">tarea de sincronización programada de hello tooverify</span><span class="sxs-lookup"><span data-stu-id="6d897-119">tooverify hello scheduled synchronization task</span></span>
1. <span data-ttu-id="6d897-120">Inicie sesión en toohello portal de Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="6d897-120">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="6d897-121">Hola izquierda, seleccione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d897-121">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="6d897-122">En hello **Active Directory** página, haga doble clic en el directorio de Hola que tiene usuarios de Hola que desee tooset seguridad.</span><span class="sxs-lookup"><span data-stu-id="6d897-122">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="6d897-123">Hola parte superior de página de directorio de hello, seleccione **integración de directorios**.</span><span class="sxs-lookup"><span data-stu-id="6d897-123">At hello top of hello directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="6d897-124">En **integración con active directory local**, Hola Nota hora de última sincronización.</span><span class="sxs-lookup"><span data-stu-id="6d897-124">Under **integration with local active directory**, note hello last sync time.</span></span>

<span data-ttu-id="6d897-125"><center>![Hora de sincronización de directorios](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="6d897-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="6d897-126">Inicio de una tarea de sincronización programada</span><span class="sxs-lookup"><span data-stu-id="6d897-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="6d897-127">Si necesita toorun una tarea de sincronización, puede hacerlo ejecutando a través del Asistente de Azure AD Connect de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="6d897-127">If you need toorun a synchronization task, you can do this by running through hello Azure AD Connect wizard again.</span></span>  <span data-ttu-id="6d897-128">Debe tooprovide sus credenciales de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d897-128">You need tooprovide your Azure AD credentials.</span></span>  <span data-ttu-id="6d897-129">En el Asistente de hello, seleccione hello **personalizar las opciones de sincronización** de tareas y haga clic en **siguiente** toomove a través del Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d897-129">In hello wizard, select hello **Customize synchronization options** task, and click **Next** toomove through hello wizard.</span></span> <span data-ttu-id="6d897-130">Al final de hello, asegúrese de que hello **iniciar el proceso de sincronización de hello tan pronto como finalice la configuración inicial de hello** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="6d897-130">At hello end, ensure that hello **Start hello synchronization process as soon as hello initial configuration completes** box is selected.</span></span>

<span data-ttu-id="6d897-131"><center>![Inicio de la sincronización](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="6d897-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="6d897-132">Para obtener más información sobre la sincronización de hello Azure AD Connect programador, consulte [el programador de conectarse de Azure AD](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="6d897-132">For more information on hello Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="6d897-133">Tareas adicionales disponibles en Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="6d897-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="6d897-134">Después de la instalación inicial de Azure AD Connect, puede siempre Hola volver a iniciar a Asistente de hello Azure AD Connect página o escritorio acceso directo de inicio.</span><span class="sxs-lookup"><span data-stu-id="6d897-134">After your initial installation of Azure AD Connect, you can always start hello wizard again from hello Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="6d897-135">Observará que pasar por el Asistente de Hola de nuevo proporciona algunas opciones nuevas en forma de Hola de tareas adicionales.</span><span class="sxs-lookup"><span data-stu-id="6d897-135">You will notice that going through hello wizard again provides some new options in hello form of additional tasks.</span></span>  

<span data-ttu-id="6d897-136">Hello tabla siguiente proporciona un resumen de estas tareas y una breve descripción de cada tarea.</span><span class="sxs-lookup"><span data-stu-id="6d897-136">hello following table provides a summary of these tasks and a brief description of each task.</span></span>

![Lista de tareas adicionales](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="6d897-138">Tarea adicional</span><span class="sxs-lookup"><span data-stu-id="6d897-138">Additional task</span></span> | <span data-ttu-id="6d897-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d897-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6d897-140">**Escenario de vista Hola seleccionado**</span><span class="sxs-lookup"><span data-stu-id="6d897-140">**View hello selected scenario**</span></span> |<span data-ttu-id="6d897-141">Visualice su solución actual de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6d897-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="6d897-142">Incluye la configuración general, los directorios sincronizados y la configuración de sincronización.</span><span class="sxs-lookup"><span data-stu-id="6d897-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="6d897-143">**Personalizar las opciones de sincronización**</span><span class="sxs-lookup"><span data-stu-id="6d897-143">**Customize synchronization options**</span></span> |<span data-ttu-id="6d897-144">Cambiar la configuración actual de hello como agregar configuración adicional de toohello de bosques de Active Directory, o habilitar las opciones de sincronización como un usuario, grupo, dispositivo o reescritura de contraseña.</span><span class="sxs-lookup"><span data-stu-id="6d897-144">Change hello current configuration like adding additional Active Directory forests toohello configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="6d897-145">**Habilitar el modo provisional**</span><span class="sxs-lookup"><span data-stu-id="6d897-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="6d897-146">La información de fases que no se sincroniza inmediatamente y no exporta tooAzure AD o en local de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6d897-146">Stage information that is not immediately synchronized and is not exported tooAzure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="6d897-147">Con esta característica, puede obtener una vista previa sincronizaciones Hola antes de que ocurran.</span><span class="sxs-lookup"><span data-stu-id="6d897-147">With this feature, you can preview hello synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6d897-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d897-148">Next steps</span></span>
<span data-ttu-id="6d897-149">Más información acerca de la [integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="6d897-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
