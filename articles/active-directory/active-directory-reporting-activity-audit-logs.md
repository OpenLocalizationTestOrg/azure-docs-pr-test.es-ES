---
title: "Informes de actividad de auditoría en el portal de Azure Active Directory | Microsoft Docs"
description: "Introducción a los informes de actividad de auditoría en el portal de Azure Active Directory"
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
ms.openlocfilehash: f2d0332d815c82d7d47625e020de2e9c5099deeb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="audit-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="3ca59-103">Informes de actividad de auditoría en el portal de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ca59-103">Audit activity reports in the Azure Active Directory portal</span></span> 

<span data-ttu-id="3ca59-104">Con los informes de Azure Active Directory (Azure AD), puede obtener toda la información que necesita para determinar cómo marcha el entorno.</span><span class="sxs-lookup"><span data-stu-id="3ca59-104">With reporting in Azure Active Directory (Azure AD), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="3ca59-105">La arquitectura de los informes de Azure AD consta de los siguientes componentes:</span><span class="sxs-lookup"><span data-stu-id="3ca59-105">The reporting architecture in Azure AD consists of the following components:</span></span>

- <span data-ttu-id="3ca59-106">**Actividad**</span><span class="sxs-lookup"><span data-stu-id="3ca59-106">**Activity**</span></span> 
    - <span data-ttu-id="3ca59-107">**Actividades de inicio de sesión** : información sobre el uso de las aplicaciones administradas y las actividades de inicio de sesión de usuario</span><span class="sxs-lookup"><span data-stu-id="3ca59-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="3ca59-108">**Registros de auditoría**: información de la actividad del sistema sobre los usuarios y la administración de grupos, sus aplicaciones administradas y actividades de directorio.</span><span class="sxs-lookup"><span data-stu-id="3ca59-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="3ca59-109">**Seguridad**</span><span class="sxs-lookup"><span data-stu-id="3ca59-109">**Security**</span></span> 
    - <span data-ttu-id="3ca59-110">**Inicios de sesión peligrosos**: un inicio de sesión peligroso es un indicador de un intento de inicio de sesión que puede haber realizado alguien que no es el propietario legítimo de una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="3ca59-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="3ca59-111">Para más información, consulte Inicios de no seguros.</span><span class="sxs-lookup"><span data-stu-id="3ca59-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="3ca59-112">**Usuarios marcados en riesgo**: un usuario en peligro es un indicador de una cuenta de usuario que puede haber estado en peligro.</span><span class="sxs-lookup"><span data-stu-id="3ca59-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="3ca59-113">Para más información, consulte la sección Usuarios marcados en riesgo.</span><span class="sxs-lookup"><span data-stu-id="3ca59-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="3ca59-114">Este tema ofrece una visión general de las actividades de auditoría.</span><span class="sxs-lookup"><span data-stu-id="3ca59-114">This topic gives you an overview of the audit activities.</span></span>
 
## <a name="who-can-access-the-data"></a><span data-ttu-id="3ca59-115">¿Quién puede acceder a los datos?</span><span class="sxs-lookup"><span data-stu-id="3ca59-115">Who can access the data?</span></span>
* <span data-ttu-id="3ca59-116">Usuarios de los roles de administrador o lector de seguridad</span><span class="sxs-lookup"><span data-stu-id="3ca59-116">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="3ca59-117">Administradores globales</span><span class="sxs-lookup"><span data-stu-id="3ca59-117">Global Admins</span></span>
* <span data-ttu-id="3ca59-118">Los usuarios individuales (no administradores) pueden ver sus propias actividades</span><span class="sxs-lookup"><span data-stu-id="3ca59-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="3ca59-119">Registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="3ca59-119">Audit logs</span></span>

<span data-ttu-id="3ca59-120">Los registros de auditoría de Azure Active Directory proporcionan registros de las actividades del sistema de cara al cumplimiento.</span><span class="sxs-lookup"><span data-stu-id="3ca59-120">The audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="3ca59-121">El primer punto de entrada a todos los datos de auditoría es **Registros de auditoría** en la sección **Actividad** de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3ca59-121">Your first entry point to all auditing data is **Audit logs** in the **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="3ca59-122">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/61.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="3ca59-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="3ca59-123">Un registro de auditoría tiene una vista de lista predeterminada que muestra:</span><span class="sxs-lookup"><span data-stu-id="3ca59-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="3ca59-124">la fecha y hora de la repetición</span><span class="sxs-lookup"><span data-stu-id="3ca59-124">the date and time of the occurrence</span></span>
- <span data-ttu-id="3ca59-125">el iniciador/actor (*quién*) de una actividad</span><span class="sxs-lookup"><span data-stu-id="3ca59-125">the initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="3ca59-126">la actividad (*qué*)</span><span class="sxs-lookup"><span data-stu-id="3ca59-126">the activity (*what*)</span></span> 
- <span data-ttu-id="3ca59-127">el destino</span><span class="sxs-lookup"><span data-stu-id="3ca59-127">the target</span></span>

<span data-ttu-id="3ca59-128">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/18.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="3ca59-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="3ca59-129">Puede personalizar la vista de lista, haga clic en **Columnas** en la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="3ca59-129">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="3ca59-130">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/19.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="3ca59-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="3ca59-131">Esto le permite mostrar los campos adicionales o quitar los campos que ya se están mostrando.</span><span class="sxs-lookup"><span data-stu-id="3ca59-131">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="3ca59-132">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/21.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="3ca59-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="3ca59-133">Si hace clic en un elemento de la vista de lista, puede obtener todos los detalles disponibles sobre él.</span><span class="sxs-lookup"><span data-stu-id="3ca59-133">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="3ca59-134">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/22.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="3ca59-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="3ca59-135">Filtrado de registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="3ca59-135">Filtering audit logs</span></span>

<span data-ttu-id="3ca59-136">Para restringir los datos del informe a un nivel que se adapte a sus necesidades, puede filtrar los datos de auditoría con los siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="3ca59-136">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span></span>

- <span data-ttu-id="3ca59-137">Intervalo de fechas</span><span class="sxs-lookup"><span data-stu-id="3ca59-137">Date range</span></span>
- <span data-ttu-id="3ca59-138">Iniciado por (actor)</span><span class="sxs-lookup"><span data-stu-id="3ca59-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="3ca59-139">Categoría</span><span class="sxs-lookup"><span data-stu-id="3ca59-139">Category</span></span>
- <span data-ttu-id="3ca59-140">Tipo de recurso de actividad</span><span class="sxs-lookup"><span data-stu-id="3ca59-140">Activity resource type</span></span>
- <span data-ttu-id="3ca59-141">Actividad</span><span class="sxs-lookup"><span data-stu-id="3ca59-141">Activity</span></span>

<span data-ttu-id="3ca59-142">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/23.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="3ca59-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="3ca59-143">El filtro **Intervalo de fechas** permite definir un período de tiempo para los datos devueltos.</span><span class="sxs-lookup"><span data-stu-id="3ca59-143">The **date range** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="3ca59-144">Los valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="3ca59-144">Possible values are:</span></span>

- <span data-ttu-id="3ca59-145">1 mes</span><span class="sxs-lookup"><span data-stu-id="3ca59-145">1 month</span></span>
- <span data-ttu-id="3ca59-146">7 días</span><span class="sxs-lookup"><span data-stu-id="3ca59-146">7 days</span></span>
- <span data-ttu-id="3ca59-147">24 horas</span><span class="sxs-lookup"><span data-stu-id="3ca59-147">24 hours</span></span>
- <span data-ttu-id="3ca59-148">Personalizado</span><span class="sxs-lookup"><span data-stu-id="3ca59-148">Custom</span></span>

<span data-ttu-id="3ca59-149">Cuando se selecciona un intervalo de tiempo personalizado, puede configurar una hora de inicio y una hora de finalización.</span><span class="sxs-lookup"><span data-stu-id="3ca59-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="3ca59-150">El filtro **Iniciado por** le permite definir el nombre de un actor o su nombre principal universal (UPN).</span><span class="sxs-lookup"><span data-stu-id="3ca59-150">The **initiated by** filter enables you to define an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="3ca59-151">El filtro **Categoría** le permite seleccionar uno de los filtros siguientes:</span><span class="sxs-lookup"><span data-stu-id="3ca59-151">The **category** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="3ca59-152">Todo</span><span class="sxs-lookup"><span data-stu-id="3ca59-152">All</span></span>
- <span data-ttu-id="3ca59-153">Core category (Categoría principal)</span><span class="sxs-lookup"><span data-stu-id="3ca59-153">Core category</span></span>
- <span data-ttu-id="3ca59-154">Core Directory (Directorio principal)</span><span class="sxs-lookup"><span data-stu-id="3ca59-154">Core directory</span></span>
- <span data-ttu-id="3ca59-155">Self-service Password Management (Administración de contraseñas de autorservicio)</span><span class="sxs-lookup"><span data-stu-id="3ca59-155">Self-service password management</span></span>
- <span data-ttu-id="3ca59-156">Self-service group management (Administración de grupos de autoservicio)</span><span class="sxs-lookup"><span data-stu-id="3ca59-156">Self-service group management</span></span>
- <span data-ttu-id="3ca59-157">Account provisioning- Automated password rollover (Aprovisionamiento de cuentas: sustitución automática de contraseñas)</span><span class="sxs-lookup"><span data-stu-id="3ca59-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="3ca59-158">Invited users (Usuarios invitados)</span><span class="sxs-lookup"><span data-stu-id="3ca59-158">Invited users</span></span>
- <span data-ttu-id="3ca59-159">MIM service (Servicio MIM)</span><span class="sxs-lookup"><span data-stu-id="3ca59-159">MIM service</span></span>
- <span data-ttu-id="3ca59-160">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3ca59-160">Identity Protection</span></span>
- <span data-ttu-id="3ca59-161">B2C</span><span class="sxs-lookup"><span data-stu-id="3ca59-161">B2C</span></span>

<span data-ttu-id="3ca59-162">El filtro **Tipo de recurso de actividad** le permite seleccionar uno de los filtros siguientes:</span><span class="sxs-lookup"><span data-stu-id="3ca59-162">The **activity resource type** filter enables you to select one of the following filters:</span></span>

- <span data-ttu-id="3ca59-163">Todo</span><span class="sxs-lookup"><span data-stu-id="3ca59-163">All</span></span> 
- <span data-ttu-id="3ca59-164">Grupo</span><span class="sxs-lookup"><span data-stu-id="3ca59-164">Group</span></span>
- <span data-ttu-id="3ca59-165">Directorio</span><span class="sxs-lookup"><span data-stu-id="3ca59-165">Directory</span></span>
- <span data-ttu-id="3ca59-166">Usuario</span><span class="sxs-lookup"><span data-stu-id="3ca59-166">User</span></span>
- <span data-ttu-id="3ca59-167">Application</span><span class="sxs-lookup"><span data-stu-id="3ca59-167">Application</span></span>
- <span data-ttu-id="3ca59-168">Directiva</span><span class="sxs-lookup"><span data-stu-id="3ca59-168">Policy</span></span>
- <span data-ttu-id="3ca59-169">Dispositivo</span><span class="sxs-lookup"><span data-stu-id="3ca59-169">Device</span></span>
- <span data-ttu-id="3ca59-170">Otros</span><span class="sxs-lookup"><span data-stu-id="3ca59-170">Other</span></span>

<span data-ttu-id="3ca59-171">Cuando se selecciona **Grupo** como **Tipo de recurso de actividad**, obtendrá una categoría de filtro adicional que le permite proporcionar también un **Origen**:</span><span class="sxs-lookup"><span data-stu-id="3ca59-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you to also provide a **Source**:</span></span>

- <span data-ttu-id="3ca59-172">Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ca59-172">Azure AD</span></span>
- <span data-ttu-id="3ca59-173">O365</span><span class="sxs-lookup"><span data-stu-id="3ca59-173">O365</span></span>


<span data-ttu-id="3ca59-174">El filtro **Actividad** se basa en la selección de categoría y de tipo de recurso de actividad que realice.</span><span class="sxs-lookup"><span data-stu-id="3ca59-174">The **activity** filter is based on the category and Activity resource type selection you make.</span></span> <span data-ttu-id="3ca59-175">Puede seleccionar la actividad específica que desea ver o elegir todas.</span><span class="sxs-lookup"><span data-stu-id="3ca59-175">You can select a specific activity you want to see or choose all.</span></span> 

<span data-ttu-id="3ca59-176">Para obtener la lista de todas las actividades de auditoría, use API Graph https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, donde $tenantdomain = el nombre de dominio, o bien consulte el artículo sobre [eventos del informe de auditoría](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="3ca59-176">You can get the list of all Audit Activities using the Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer to the article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="3ca59-177">Métodos abreviados de los registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="3ca59-177">Audit logs shortcuts</span></span>

<span data-ttu-id="3ca59-178">Además de **Azure Active Directory**, Azure Portal proporciona dos puntos de entrada adicionales para auditar datos:</span><span class="sxs-lookup"><span data-stu-id="3ca59-178">In addition to **Azure Active Directory**, the Azure portal provides you with two additional entry points to audit data:</span></span>

- <span data-ttu-id="3ca59-179">Usuarios y grupos</span><span class="sxs-lookup"><span data-stu-id="3ca59-179">Users and groups</span></span>
- <span data-ttu-id="3ca59-180">Aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="3ca59-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="3ca59-181">Registros de auditoría de los usuarios y grupos</span><span class="sxs-lookup"><span data-stu-id="3ca59-181">Users and groups audit logs</span></span>

<span data-ttu-id="3ca59-182">Con los informes de auditoría basadas en grupos y usuarios, puede obtener respuestas a preguntas como:</span><span class="sxs-lookup"><span data-stu-id="3ca59-182">With user and group-based audit reports, you can get answers to questions such as:</span></span>

- <span data-ttu-id="3ca59-183">¿Qué tipos de actualizaciones se han aplicado a los usuarios?</span><span class="sxs-lookup"><span data-stu-id="3ca59-183">What types of updates have been applied the users?</span></span>

- <span data-ttu-id="3ca59-184">¿Cuántos usuarios han cambiado?</span><span class="sxs-lookup"><span data-stu-id="3ca59-184">How many users were changed?</span></span>

- <span data-ttu-id="3ca59-185">¿Cuántas contraseñas han cambiado?</span><span class="sxs-lookup"><span data-stu-id="3ca59-185">How many passwords were changed?</span></span>

- <span data-ttu-id="3ca59-186">¿Qué ha hecho un administrador en un directorio?</span><span class="sxs-lookup"><span data-stu-id="3ca59-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="3ca59-187">¿Cuáles son los grupos que se han agregado?</span><span class="sxs-lookup"><span data-stu-id="3ca59-187">What are the groups that have been added?</span></span>

- <span data-ttu-id="3ca59-188">¿Hay grupos con cambios de pertenencia?</span><span class="sxs-lookup"><span data-stu-id="3ca59-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="3ca59-189">¿Se han cambiado los propietarios del grupo?</span><span class="sxs-lookup"><span data-stu-id="3ca59-189">Have the owners of group been changed?</span></span>

- <span data-ttu-id="3ca59-190">¿Qué licencias se han asignado a un grupo o un usuario?</span><span class="sxs-lookup"><span data-stu-id="3ca59-190">What licenses have been assigned to a group or a user?</span></span>

<span data-ttu-id="3ca59-191">Si desea revisar los datos de auditoría relacionados con usuarios y grupos, puede buscar una vista filtrada en **Registros de auditoría** en la sección **Actividad** de **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3ca59-191">If you just want to review auditing data that is related to users and groups, you can find a filtered view under **Audit logs** in the **Activity** section of the **Users and Groups**.</span></span> <span data-ttu-id="3ca59-192">Este punto de entrada tiene **Usuarios y grupos** como **Tipo de recurso de actividad** preseleccionado.</span><span class="sxs-lookup"><span data-stu-id="3ca59-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="3ca59-193">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/93.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="3ca59-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="3ca59-194">Registros de auditoría de aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="3ca59-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="3ca59-195">Con los informes de auditoría basadas en aplicaciones, puede obtener respuestas a preguntas tales como:</span><span class="sxs-lookup"><span data-stu-id="3ca59-195">With application-based audit reports, you can get answers to questions such as:</span></span>

* <span data-ttu-id="3ca59-196">¿Cuáles son las aplicaciones que se han agregado o actualizado?</span><span class="sxs-lookup"><span data-stu-id="3ca59-196">What are the applications that have been added or updated?</span></span>
* <span data-ttu-id="3ca59-197">¿Cuáles son las aplicaciones que se han quitado?</span><span class="sxs-lookup"><span data-stu-id="3ca59-197">What are the applications that have been removed?</span></span>
* <span data-ttu-id="3ca59-198">¿Ha cambiado el principal de servicio para una aplicación?</span><span class="sxs-lookup"><span data-stu-id="3ca59-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="3ca59-199">¿Se han cambiado los nombres de las aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="3ca59-199">Have the names of applications been changed?</span></span>
* <span data-ttu-id="3ca59-200">¿Quién dio el consentimiento a una aplicación?</span><span class="sxs-lookup"><span data-stu-id="3ca59-200">Who gave consent to an application?</span></span>

<span data-ttu-id="3ca59-201">Si desea revisar los datos de auditoría relacionados con las aplicaciones, puede buscar una vista filtrada en **Registros de auditoría** en la sección **Actividad** de la hoja **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3ca59-201">If you just want to review auditing data that is related to your applications, you can find a filtered view under **Audit logs** in the **Activity** section of the **Enterprise applications** blade.</span></span> <span data-ttu-id="3ca59-202">Este punto de entrada tiene **Aplicaciones empresariales** como **Tipo de recurso de actividad** preseleccionado.</span><span class="sxs-lookup"><span data-stu-id="3ca59-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="3ca59-203">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/134.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="3ca59-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="3ca59-204">Puede filtrar aún más esta vista hasta simplemente **grupos** o simplemente **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3ca59-204">You can filter this view further down to just **groups** or just **users**.</span></span>

<span data-ttu-id="3ca59-205">![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/25.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="3ca59-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="3ca59-206">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3ca59-206">Next steps</span></span>

<span data-ttu-id="3ca59-207">Para obtener información general sobre los informes, consulte [Informes de Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3ca59-207">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

