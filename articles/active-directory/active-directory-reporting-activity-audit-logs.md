---
title: los informes de actividad aaaAudit de portal de Azure Active Directory Hola | Documentos de Microsoft
description: "Informes de actividad en el portal de Azure Active Directory de Hola de auditoría de toohello de introducción"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="5acf6-103">Informes de actividad en el portal de Azure Active Directory Hola de auditoría</span><span class="sxs-lookup"><span data-stu-id="5acf6-103">Audit activity reports in hello Azure Active Directory portal</span></span> 

<span data-ttu-id="5acf6-104">Con los informes en Azure Active Directory (Azure AD), puede obtener información de hello necesita toodetermine cómo está haciendo su entorno.</span><span class="sxs-lookup"><span data-stu-id="5acf6-104">With reporting in Azure Active Directory (Azure AD), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="5acf6-105">arquitectura de los informes en Azure AD de Hello consta de Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="5acf6-105">hello reporting architecture in Azure AD consists of hello following components:</span></span>

- <span data-ttu-id="5acf6-106">**Actividad**</span><span class="sxs-lookup"><span data-stu-id="5acf6-106">**Activity**</span></span> 
    - <span data-ttu-id="5acf6-107">**Las actividades de inicio de sesión** : información sobre el uso de Hola de las aplicaciones administradas y las actividades de inicio de sesión de usuario</span><span class="sxs-lookup"><span data-stu-id="5acf6-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="5acf6-108">**Registros de auditoría**: información de la actividad del sistema sobre los usuarios y la administración de grupos, sus aplicaciones administradas y actividades de directorio.</span><span class="sxs-lookup"><span data-stu-id="5acf6-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="5acf6-109">**Seguridad**</span><span class="sxs-lookup"><span data-stu-id="5acf6-109">**Security**</span></span> 
    - <span data-ttu-id="5acf6-110">**Inicios de sesión arriesgados** -un inicio de sesión de riesgo es un indicador de un intento de inicio de sesión que es posible que se han realizado por alguien que no es propietario legítimo de Hola de una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="5acf6-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="5acf6-111">Para más información, consulte Inicios de no seguros.</span><span class="sxs-lookup"><span data-stu-id="5acf6-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="5acf6-112">**Usuarios marcados en riesgo**: un usuario en peligro es un indicador de una cuenta de usuario que puede haber estado en peligro.</span><span class="sxs-lookup"><span data-stu-id="5acf6-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="5acf6-113">Para más información, consulte la sección Usuarios marcados en riesgo.</span><span class="sxs-lookup"><span data-stu-id="5acf6-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="5acf6-114">Este tema ofrece una visión general de las actividades de auditoría de Hola.</span><span class="sxs-lookup"><span data-stu-id="5acf6-114">This topic gives you an overview of hello audit activities.</span></span>
 
## <a name="who-can-access-hello-data"></a><span data-ttu-id="5acf6-115">¿Quién puede tener acceso a datos de hello?</span><span class="sxs-lookup"><span data-stu-id="5acf6-115">Who can access hello data?</span></span>
* <span data-ttu-id="5acf6-116">Usuarios de rol de administrador de seguridad o seguridad lector Hola</span><span class="sxs-lookup"><span data-stu-id="5acf6-116">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="5acf6-117">Administradores globales</span><span class="sxs-lookup"><span data-stu-id="5acf6-117">Global Admins</span></span>
* <span data-ttu-id="5acf6-118">Los usuarios individuales (no administradores) pueden ver sus propias actividades</span><span class="sxs-lookup"><span data-stu-id="5acf6-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="5acf6-119">Registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="5acf6-119">Audit logs</span></span>

<span data-ttu-id="5acf6-120">registros de auditoría de Hello en Azure Active Directory proporcionan registros de las actividades del sistema para el cumplimiento.</span><span class="sxs-lookup"><span data-stu-id="5acf6-120">hello audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="5acf6-121">Es el primer tooall de punto de entrada datos de auditoría **registros de auditoría** en hello **actividad** sección de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5acf6-121">Your first entry point tooall auditing data is **Audit logs** in hello **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="5acf6-122">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/61.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="5acf6-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="5acf6-123">Un registro de auditoría tiene una vista de lista predeterminada que muestra:</span><span class="sxs-lookup"><span data-stu-id="5acf6-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="5acf6-124">Hola fecha y hora de aparición de Hola</span><span class="sxs-lookup"><span data-stu-id="5acf6-124">hello date and time of hello occurrence</span></span>
- <span data-ttu-id="5acf6-125">Hola iniciador / actor (*que*) de una actividad</span><span class="sxs-lookup"><span data-stu-id="5acf6-125">hello initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="5acf6-126">Hola actividad (*qué*)</span><span class="sxs-lookup"><span data-stu-id="5acf6-126">hello activity (*what*)</span></span> 
- <span data-ttu-id="5acf6-127">destino de Hola</span><span class="sxs-lookup"><span data-stu-id="5acf6-127">hello target</span></span>

<span data-ttu-id="5acf6-128">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/18.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="5acf6-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="5acf6-129">Puede personalizar la vista de lista Hola haciendo clic en **columnas** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="5acf6-129">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="5acf6-130">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/19.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="5acf6-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="5acf6-131">Esto permite los campos adicionales de toodisplay o quitar los campos que ya se muestran.</span><span class="sxs-lookup"><span data-stu-id="5acf6-131">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="5acf6-132">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/21.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="5acf6-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="5acf6-133">Si hace clic en un elemento en la vista de lista de hello, obtener todos los detalles disponibles sobre él.</span><span class="sxs-lookup"><span data-stu-id="5acf6-133">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="5acf6-134">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/22.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="5acf6-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="5acf6-135">Filtrado de registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="5acf6-135">Filtering audit logs</span></span>

<span data-ttu-id="5acf6-136">toonarrow hacia abajo Hola informó de un nivel de tooa de datos que funciona para usted, puede filtrar datos de auditoría de hello mediante Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="5acf6-136">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="5acf6-137">Intervalo de fechas</span><span class="sxs-lookup"><span data-stu-id="5acf6-137">Date range</span></span>
- <span data-ttu-id="5acf6-138">Iniciado por (actor)</span><span class="sxs-lookup"><span data-stu-id="5acf6-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="5acf6-139">Categoría</span><span class="sxs-lookup"><span data-stu-id="5acf6-139">Category</span></span>
- <span data-ttu-id="5acf6-140">Tipo de recurso de actividad</span><span class="sxs-lookup"><span data-stu-id="5acf6-140">Activity resource type</span></span>
- <span data-ttu-id="5acf6-141">Actividad</span><span class="sxs-lookup"><span data-stu-id="5acf6-141">Activity</span></span>

<span data-ttu-id="5acf6-142">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/23.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="5acf6-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="5acf6-143">Hola **intervalo de fechas** filtro permite tooyou toodefine un período de tiempo para hello devolvió datos.</span><span class="sxs-lookup"><span data-stu-id="5acf6-143">hello **date range** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="5acf6-144">Los valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="5acf6-144">Possible values are:</span></span>

- <span data-ttu-id="5acf6-145">1 mes</span><span class="sxs-lookup"><span data-stu-id="5acf6-145">1 month</span></span>
- <span data-ttu-id="5acf6-146">7 días</span><span class="sxs-lookup"><span data-stu-id="5acf6-146">7 days</span></span>
- <span data-ttu-id="5acf6-147">24 horas</span><span class="sxs-lookup"><span data-stu-id="5acf6-147">24 hours</span></span>
- <span data-ttu-id="5acf6-148">Personalizado</span><span class="sxs-lookup"><span data-stu-id="5acf6-148">Custom</span></span>

<span data-ttu-id="5acf6-149">Cuando se selecciona un intervalo de tiempo personalizado, puede configurar una hora de inicio y una hora de finalización.</span><span class="sxs-lookup"><span data-stu-id="5acf6-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="5acf6-150">Hola **iniciadas por** filtro permite toodefine nombre de un actor o su nombre principal universal (UPN).</span><span class="sxs-lookup"><span data-stu-id="5acf6-150">hello **initiated by** filter enables you toodefine an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="5acf6-151">Hola **categoría** filtro le permite tooselect de hello siguiente filtro:</span><span class="sxs-lookup"><span data-stu-id="5acf6-151">hello **category** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="5acf6-152">Todo</span><span class="sxs-lookup"><span data-stu-id="5acf6-152">All</span></span>
- <span data-ttu-id="5acf6-153">Core category (Categoría principal)</span><span class="sxs-lookup"><span data-stu-id="5acf6-153">Core category</span></span>
- <span data-ttu-id="5acf6-154">Core Directory (Directorio principal)</span><span class="sxs-lookup"><span data-stu-id="5acf6-154">Core directory</span></span>
- <span data-ttu-id="5acf6-155">Self-service Password Management (Administración de contraseñas de autorservicio)</span><span class="sxs-lookup"><span data-stu-id="5acf6-155">Self-service password management</span></span>
- <span data-ttu-id="5acf6-156">Self-service group management (Administración de grupos de autoservicio)</span><span class="sxs-lookup"><span data-stu-id="5acf6-156">Self-service group management</span></span>
- <span data-ttu-id="5acf6-157">Account provisioning- Automated password rollover (Aprovisionamiento de cuentas: sustitución automática de contraseñas)</span><span class="sxs-lookup"><span data-stu-id="5acf6-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="5acf6-158">Invited users (Usuarios invitados)</span><span class="sxs-lookup"><span data-stu-id="5acf6-158">Invited users</span></span>
- <span data-ttu-id="5acf6-159">MIM service (Servicio MIM)</span><span class="sxs-lookup"><span data-stu-id="5acf6-159">MIM service</span></span>
- <span data-ttu-id="5acf6-160">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5acf6-160">Identity Protection</span></span>
- <span data-ttu-id="5acf6-161">B2C</span><span class="sxs-lookup"><span data-stu-id="5acf6-161">B2C</span></span>

<span data-ttu-id="5acf6-162">Hola **tipo de recurso de la actividad** filtro le permite tooselect uno de los siguientes Hola filtros:</span><span class="sxs-lookup"><span data-stu-id="5acf6-162">hello **activity resource type** filter enables you tooselect one of hello following filters:</span></span>

- <span data-ttu-id="5acf6-163">Todo</span><span class="sxs-lookup"><span data-stu-id="5acf6-163">All</span></span> 
- <span data-ttu-id="5acf6-164">Grupo</span><span class="sxs-lookup"><span data-stu-id="5acf6-164">Group</span></span>
- <span data-ttu-id="5acf6-165">Directorio</span><span class="sxs-lookup"><span data-stu-id="5acf6-165">Directory</span></span>
- <span data-ttu-id="5acf6-166">Usuario</span><span class="sxs-lookup"><span data-stu-id="5acf6-166">User</span></span>
- <span data-ttu-id="5acf6-167">Application</span><span class="sxs-lookup"><span data-stu-id="5acf6-167">Application</span></span>
- <span data-ttu-id="5acf6-168">Directiva</span><span class="sxs-lookup"><span data-stu-id="5acf6-168">Policy</span></span>
- <span data-ttu-id="5acf6-169">Dispositivo</span><span class="sxs-lookup"><span data-stu-id="5acf6-169">Device</span></span>
- <span data-ttu-id="5acf6-170">Otros</span><span class="sxs-lookup"><span data-stu-id="5acf6-170">Other</span></span>

<span data-ttu-id="5acf6-171">Cuando se selecciona **grupo** como **tipo de recurso de la actividad**, obtendrá una categoría de filtro adicional que le permite tooalso proporcionan un **origen**:</span><span class="sxs-lookup"><span data-stu-id="5acf6-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you tooalso provide a **Source**:</span></span>

- <span data-ttu-id="5acf6-172">Azure AD</span><span class="sxs-lookup"><span data-stu-id="5acf6-172">Azure AD</span></span>
- <span data-ttu-id="5acf6-173">O365</span><span class="sxs-lookup"><span data-stu-id="5acf6-173">O365</span></span>


<span data-ttu-id="5acf6-174">Hola **actividad** filtro se basa en la categoría de Hola y selección de tipo de recurso de actividad que realice.</span><span class="sxs-lookup"><span data-stu-id="5acf6-174">hello **activity** filter is based on hello category and Activity resource type selection you make.</span></span> <span data-ttu-id="5acf6-175">Puede seleccionar una actividad específica que desee toosee o elegir todos.</span><span class="sxs-lookup"><span data-stu-id="5acf6-175">You can select a specific activity you want toosee or choose all.</span></span> 

<span data-ttu-id="5acf6-176">Puede obtener lista de Hola de todas las actividades de auditoría mediante Hola API Graph https://graph.windows.net/$ tenantdomain/actividades/auditActivityTypes? api-version = beta, donde $tenantdomain = el nombre de dominio o consulte el artículo toohello [informe de auditoría eventos](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="5acf6-176">You can get hello list of all Audit Activities using hello Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer toohello article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="5acf6-177">Métodos abreviados de los registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="5acf6-177">Audit logs shortcuts</span></span>

<span data-ttu-id="5acf6-178">Además demasiado**Azure Active Directory**, hello portal de Azure proporciona dos puntos de entrada adicionales tooaudit datos:</span><span class="sxs-lookup"><span data-stu-id="5acf6-178">In addition too**Azure Active Directory**, hello Azure portal provides you with two additional entry points tooaudit data:</span></span>

- <span data-ttu-id="5acf6-179">Usuarios y grupos</span><span class="sxs-lookup"><span data-stu-id="5acf6-179">Users and groups</span></span>
- <span data-ttu-id="5acf6-180">Aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="5acf6-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="5acf6-181">Registros de auditoría de los usuarios y grupos</span><span class="sxs-lookup"><span data-stu-id="5acf6-181">Users and groups audit logs</span></span>

<span data-ttu-id="5acf6-182">Con informes de auditoría basadas en el grupo y usuario, puede obtener respuestas tooquestions como:</span><span class="sxs-lookup"><span data-stu-id="5acf6-182">With user and group-based audit reports, you can get answers tooquestions such as:</span></span>

- <span data-ttu-id="5acf6-183">¿Qué tipos de actualizaciones han sido usuarios Hola aplicado?</span><span class="sxs-lookup"><span data-stu-id="5acf6-183">What types of updates have been applied hello users?</span></span>

- <span data-ttu-id="5acf6-184">¿Cuántos usuarios han cambiado?</span><span class="sxs-lookup"><span data-stu-id="5acf6-184">How many users were changed?</span></span>

- <span data-ttu-id="5acf6-185">¿Cuántas contraseñas han cambiado?</span><span class="sxs-lookup"><span data-stu-id="5acf6-185">How many passwords were changed?</span></span>

- <span data-ttu-id="5acf6-186">¿Qué ha hecho un administrador en un directorio?</span><span class="sxs-lookup"><span data-stu-id="5acf6-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="5acf6-187">¿Cuáles son los grupos de Hola que se han agregado?</span><span class="sxs-lookup"><span data-stu-id="5acf6-187">What are hello groups that have been added?</span></span>

- <span data-ttu-id="5acf6-188">¿Hay grupos con cambios de pertenencia?</span><span class="sxs-lookup"><span data-stu-id="5acf6-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="5acf6-189">¿Se cambiaron los propietarios de Hola de grupo?</span><span class="sxs-lookup"><span data-stu-id="5acf6-189">Have hello owners of group been changed?</span></span>

- <span data-ttu-id="5acf6-190">¿Qué licencias se han asignado un usuario o grupo de tooa?</span><span class="sxs-lookup"><span data-stu-id="5acf6-190">What licenses have been assigned tooa group or a user?</span></span>

<span data-ttu-id="5acf6-191">Si su intención es tooreview datos toousers relacionados y grupos de la auditoría, puede encontrar una vista filtrada en **registros de auditoría** en hello **actividad** sección de hello **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5acf6-191">If you just want tooreview auditing data that is related toousers and groups, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Users and Groups**.</span></span> <span data-ttu-id="5acf6-192">Este punto de entrada tiene **Usuarios y grupos** como **Tipo de recurso de actividad** preseleccionado.</span><span class="sxs-lookup"><span data-stu-id="5acf6-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="5acf6-193">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/93.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="5acf6-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="5acf6-194">Registros de auditoría de aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="5acf6-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="5acf6-195">Informes de auditoría basado en la aplicación, puede obtener respuestas tooquestions como:</span><span class="sxs-lookup"><span data-stu-id="5acf6-195">With application-based audit reports, you can get answers tooquestions such as:</span></span>

* <span data-ttu-id="5acf6-196">¿Cuáles son las aplicaciones de Hola que se han agregado o actualizado?</span><span class="sxs-lookup"><span data-stu-id="5acf6-196">What are hello applications that have been added or updated?</span></span>
* <span data-ttu-id="5acf6-197">¿Cuáles son las aplicaciones de Hola que se han quitado?</span><span class="sxs-lookup"><span data-stu-id="5acf6-197">What are hello applications that have been removed?</span></span>
* <span data-ttu-id="5acf6-198">¿Ha cambiado el principal de servicio para una aplicación?</span><span class="sxs-lookup"><span data-stu-id="5acf6-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="5acf6-199">¿Se cambiaron los nombres de Hola de las aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="5acf6-199">Have hello names of applications been changed?</span></span>
* <span data-ttu-id="5acf6-200">¿Que dio consentimiento tooan aplicación?</span><span class="sxs-lookup"><span data-stu-id="5acf6-200">Who gave consent tooan application?</span></span>

<span data-ttu-id="5acf6-201">Si su intención es tooreview datos que está relacionado tooyour aplicaciones de la auditoría, puede encontrar una vista filtrada en **registros de auditoría** en hello **actividad** sección de hello **aplicaciones empresariales**  hoja.</span><span class="sxs-lookup"><span data-stu-id="5acf6-201">If you just want tooreview auditing data that is related tooyour applications, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Enterprise applications** blade.</span></span> <span data-ttu-id="5acf6-202">Este punto de entrada tiene **Aplicaciones empresariales** como **Tipo de recurso de actividad** preseleccionado.</span><span class="sxs-lookup"><span data-stu-id="5acf6-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="5acf6-203">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/134.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="5acf6-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="5acf6-204">Puede filtrar aún más esta vista hacia abajo toojust **grupos** o simplemente **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5acf6-204">You can filter this view further down toojust **groups** or just **users**.</span></span>

<span data-ttu-id="5acf6-205">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/25.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="5acf6-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="5acf6-206">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5acf6-206">Next steps</span></span>

<span data-ttu-id="5acf6-207">Para obtener información general de informes, vea hello [reporting de Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5acf6-207">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

