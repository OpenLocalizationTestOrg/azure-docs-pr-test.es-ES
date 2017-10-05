---
title: "Búsqueda de informes de actividad en Azure Portal | Microsoft Docs"
description: "Obtenga información sobre cómo buscar informes de actividad de Azure Active Directory en Azure Portal."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f1875582476c3817b9eb0082b6548cc15043cb98
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="find-activity-reports-in-the-azure-portal"></a><span data-ttu-id="34e0d-103">Búsqueda de informes de actividad en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="34e0d-103">Find activity reports in the Azure portal</span></span>

<span data-ttu-id="34e0d-104">Si migra del Portal de Azure clásico a Azure Portal, los registros de actividad de Azure Active Directory (Azure AD) tendrán un nuevo aspecto.</span><span class="sxs-lookup"><span data-stu-id="34e0d-104">If you are moving from the Azure classic portal to the Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="34e0d-105">En una [entrada de blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/) reciente, explicamos cómo puede ver los registros de actividad en el contexto del recurso en que trabaja en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="34e0d-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in the context of the resource you are working on in the Azure portal.</span></span> <span data-ttu-id="34e0d-106">En este artículo se describe cómo puede buscar los informes que usaba en el Portal de Azure clásico en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="34e0d-106">In this article, we describe how to find reports that you used in the Azure classic portal in the Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="34e0d-107">Novedades</span><span class="sxs-lookup"><span data-stu-id="34e0d-107">What's new</span></span>

<span data-ttu-id="34e0d-108">Los informes del Portal de Azure clásico están separados por categorías:</span><span class="sxs-lookup"><span data-stu-id="34e0d-108">Reports in the Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="34e0d-109">Informes de seguridad</span><span class="sxs-lookup"><span data-stu-id="34e0d-109">Security reports</span></span>
2.  <span data-ttu-id="34e0d-110">Informes de actividad</span><span class="sxs-lookup"><span data-stu-id="34e0d-110">Activity reports</span></span>
3.  <span data-ttu-id="34e0d-111">Informes de aplicaciones integradas</span><span class="sxs-lookup"><span data-stu-id="34e0d-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="34e0d-112">Informes de actividad y de aplicaciones integradas</span><span class="sxs-lookup"><span data-stu-id="34e0d-112">Activity and integrated app reports</span></span>

<span data-ttu-id="34e0d-113">En el caso de los informes basados en contexto en Azure Portal, los informes existentes se combinan en una sola vista.</span><span class="sxs-lookup"><span data-stu-id="34e0d-113">For context-based reporting in the Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="34e0d-114">Una API subyacente única proporciona los datos a la vista.</span><span class="sxs-lookup"><span data-stu-id="34e0d-114">A single, underlying API provides the data to the view.</span></span>

<span data-ttu-id="34e0d-115">Para ver esta vista, vaya a la hoja **Azure Active Directory** y, en **ACTIVIDAD**, seleccione **Registros de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-115">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="34e0d-116">![Registros de auditoría](./media/active-directory-reporting-migration/482.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="34e0d-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="34e0d-117">Los informes siguientes están consolidados en esta vista:</span><span class="sxs-lookup"><span data-stu-id="34e0d-117">The following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="34e0d-118">Informe de auditoría</span><span class="sxs-lookup"><span data-stu-id="34e0d-118">Audit report</span></span>
-   <span data-ttu-id="34e0d-119">Actividad de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="34e0d-119">Password reset activity</span></span>
-   <span data-ttu-id="34e0d-120">Actividad de registro de restablecimiento de contraseñas</span><span class="sxs-lookup"><span data-stu-id="34e0d-120">Password reset registration activity</span></span>
-   <span data-ttu-id="34e0d-121">Actividad de los grupos de autoservicio</span><span class="sxs-lookup"><span data-stu-id="34e0d-121">Self-service groups activity</span></span>
-   <span data-ttu-id="34e0d-122">Cambios de nombre de grupo de Office365</span><span class="sxs-lookup"><span data-stu-id="34e0d-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="34e0d-123">Actividad de aprovisionamiento de cuentas</span><span class="sxs-lookup"><span data-stu-id="34e0d-123">Account provisioning activity</span></span>
-   <span data-ttu-id="34e0d-124">Estado de la sustitución de contraseña</span><span class="sxs-lookup"><span data-stu-id="34e0d-124">Password rollover status</span></span>
-   <span data-ttu-id="34e0d-125">Errores de aprovisionamiento de cuentas</span><span class="sxs-lookup"><span data-stu-id="34e0d-125">Account provisioning errors</span></span>


<span data-ttu-id="34e0d-126">El informe Uso de la aplicación se mejoró y se incluyó en la vista **Inicios de sesión**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-126">The Application Usage report has been enhanced and is included in the **Sign-ins** view.</span></span> <span data-ttu-id="34e0d-127">Para ver esta vista, vaya a la hoja **Azure Active Directory** y, en **ACTIVIDAD**, seleccione **Inicios de sesión**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-127">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="34e0d-128">![Vista de inicios de sesión](./media/active-directory-reporting-migration/483.png "Vista de inicios de sesión")</span><span class="sxs-lookup"><span data-stu-id="34e0d-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="34e0d-129">La vista **Inicios de sesión** incluye todos los inicios de sesión del usuario.</span><span class="sxs-lookup"><span data-stu-id="34e0d-129">The **Sign-ins** view includes all user sign-ins.</span></span> <span data-ttu-id="34e0d-130">Puede usar esta información para obtener información sobre el uso de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="34e0d-130">You can use this information to get application usage information.</span></span> <span data-ttu-id="34e0d-131">También puede consultar la información sobre el uso de las aplicaciones en la información general sobre **Aplicaciones empresariales** en la sección **ADMINISTRAR**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-131">You also can view application usage information in the **Enterprise applications** overview, in the **MANAGE** section.</span></span>

<span data-ttu-id="34e0d-132">![Aplicaciones empresariales](./media/active-directory-reporting-migration/484.png "Aplicaciones empresariales")</span><span class="sxs-lookup"><span data-stu-id="34e0d-132">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="34e0d-133">Acceso a un informe específico</span><span class="sxs-lookup"><span data-stu-id="34e0d-133">Access a specific report</span></span>

<span data-ttu-id="34e0d-134">Si bien Azure Portal ofrece una vista única, también se pueden consultar informes específicos.</span><span class="sxs-lookup"><span data-stu-id="34e0d-134">Although the Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="34e0d-135">Registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="34e0d-135">Audit logs</span></span>

<span data-ttu-id="34e0d-136">En respuesta a los comentarios de los clientes, en Azure Portal puede usar el filtrado avanzado para tener acceso a los datos que desea.</span><span class="sxs-lookup"><span data-stu-id="34e0d-136">In response to customer feedback, in the Azure portal, you can use advanced filtering to access the data you want.</span></span> <span data-ttu-id="34e0d-137">Un filtro que puede usar es una *categoría de actividad*, que muestra los distintos tipos de registros de actividad en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34e0d-137">One filter you can use is an *activity category*, which lists the different types of activity logs in Azure AD.</span></span> <span data-ttu-id="34e0d-138">Para restringir los resultados a lo que busca, puede seleccionar una categoría.</span><span class="sxs-lookup"><span data-stu-id="34e0d-138">To narrow results to what you are looking for, you can select a category.</span></span>

<span data-ttu-id="34e0d-139">Por ejemplo, si solo le interesan las actividades relacionadas con los restablecimientos de contraseña de autoservicio, puede elegir la categoría **Administración de contraseñas de autoservicio**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-139">For example, if you are interested only in activities related to self-service password resets, you can choose the **Self-service Password Management** category.</span></span> <span data-ttu-id="34e0d-140">Las categorías que ve se basan en el recurso en el que trabaja.</span><span class="sxs-lookup"><span data-stu-id="34e0d-140">The categories you see are based on the resource you are working in.</span></span>  

<span data-ttu-id="34e0d-141">![Opciones de categoría en la página Filtrar registros de auditoría](./media/active-directory-reporting-migration/06.png "Opciones de categoría en la página Filtrar registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="34e0d-141">![Category options on the Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on the Filter Audit Logs page")</span></span>

<span data-ttu-id="34e0d-142">Las categorías de actividad incluyen:</span><span class="sxs-lookup"><span data-stu-id="34e0d-142">Activity categories include:</span></span>

- <span data-ttu-id="34e0d-143">Core Directory (Directorio principal)</span><span class="sxs-lookup"><span data-stu-id="34e0d-143">Core Directory</span></span>
- <span data-ttu-id="34e0d-144">Self-service Password Management (Administración de contraseñas de autorservicio)</span><span class="sxs-lookup"><span data-stu-id="34e0d-144">Self-service Password Management</span></span>
- <span data-ttu-id="34e0d-145">Self-service Group Management (Administración de grupos de autoservicio)</span><span class="sxs-lookup"><span data-stu-id="34e0d-145">Self-service Group Management</span></span>
- <span data-ttu-id="34e0d-146">Account Provisioning (Aprovisionamiento de cuentas)</span><span class="sxs-lookup"><span data-stu-id="34e0d-146">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="34e0d-147">Uso de la aplicación</span><span class="sxs-lookup"><span data-stu-id="34e0d-147">Application usage</span></span>

<span data-ttu-id="34e0d-148">Para detalles sobre el uso de todas las aplicaciones o de una sola aplicación, en **ACTIVIDAD**, seleccione **Inicios de sesión**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-148">To view details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**.</span></span> <span data-ttu-id="34e0d-149">Para restringir los resultados, puede filtrar según el nombre del usuario o el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="34e0d-149">To narrow the results, you can filter on user name or application name.</span></span>

<span data-ttu-id="34e0d-150">![Página Filtrar eventos de inicio de sesión](./media/active-directory-reporting-migration/07.png "Página Filtrar eventos de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="34e0d-150">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="34e0d-151">Informes de seguridad</span><span class="sxs-lookup"><span data-stu-id="34e0d-151">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="34e0d-152">Informes de actividades anómalas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="34e0d-152">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="34e0d-153">Los informes de seguridad de actividad anómala en Azure AD del Portal de Azure clásico se consolidaron para brindarle una vista una y centralizada.</span><span class="sxs-lookup"><span data-stu-id="34e0d-153">Azure AD anomalous activity security reports from the Azure classic portal have been consolidated to provide you with one, central view.</span></span> <span data-ttu-id="34e0d-154">Esta vista muestra todos los eventos de riesgo relacionados con la seguridad que Azure AD puede detectar e informar.</span><span class="sxs-lookup"><span data-stu-id="34e0d-154">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="34e0d-155">En la tabla siguiente aparecen los informes de seguridad de actividad anómala de Azure AD y los tipos de eventos de riesgo correspondientes en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="34e0d-155">The following table lists the Azure AD anomalous activity security reports, and corresponding risk event types in the Azure portal.</span></span>

| <span data-ttu-id="34e0d-156">Informe de actividad anómala de Azure AD</span><span class="sxs-lookup"><span data-stu-id="34e0d-156">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="34e0d-157">Tipo de evento de riesgo de Identity Protection</span><span class="sxs-lookup"><span data-stu-id="34e0d-157">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="34e0d-158">Usuarios con credenciales perdidas</span><span class="sxs-lookup"><span data-stu-id="34e0d-158">Users with leaked credentials</span></span> | <span data-ttu-id="34e0d-159">Credenciales con fugas</span><span class="sxs-lookup"><span data-stu-id="34e0d-159">Leaked credentials</span></span> |
| <span data-ttu-id="34e0d-160">Actividad de inicio de sesión irregular</span><span class="sxs-lookup"><span data-stu-id="34e0d-160">Irregular sign-in activity</span></span> | <span data-ttu-id="34e0d-161">Viaje imposible a ubicaciones inusuales</span><span class="sxs-lookup"><span data-stu-id="34e0d-161">Impossible travel to atypical locations</span></span> |
| <span data-ttu-id="34e0d-162">Inicios de sesión desde dispositivos posiblemente infectados</span><span class="sxs-lookup"><span data-stu-id="34e0d-162">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="34e0d-163">Inicios de sesión desde dispositivos infectados</span><span class="sxs-lookup"><span data-stu-id="34e0d-163">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="34e0d-164">Inicios de sesión desde orígenes desconocidos</span><span class="sxs-lookup"><span data-stu-id="34e0d-164">Sign-ins from unknown sources</span></span> | <span data-ttu-id="34e0d-165">Inicios de sesión desde direcciones IP anónimas</span><span class="sxs-lookup"><span data-stu-id="34e0d-165">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="34e0d-166">Inicios de sesión desde direcciones IP con actividad sospechosa</span><span class="sxs-lookup"><span data-stu-id="34e0d-166">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="34e0d-167">Inicios de sesión desde direcciones IP con actividad sospechosa</span><span class="sxs-lookup"><span data-stu-id="34e0d-167">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="34e0d-168">Inicios de sesión desde ubicaciones desconocidas</span><span class="sxs-lookup"><span data-stu-id="34e0d-168">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="34e0d-169">Los informes de seguridad de actividad anómala de Azure AD siguientes no se incluyen como eventos de riesgo en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="34e0d-169">The following Azure AD anomalous activity security reports are not included as risk events in the Azure portal:</span></span>

* <span data-ttu-id="34e0d-170">Inicios de sesión tras varios errores</span><span class="sxs-lookup"><span data-stu-id="34e0d-170">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="34e0d-171">Inicios de sesión desde varias ubicaciones geográficas</span><span class="sxs-lookup"><span data-stu-id="34e0d-171">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="34e0d-172">Estos informes siguen disponibles en el Portal de Azure clásico, pero quedarán en desuso en el futuro.</span><span class="sxs-lookup"><span data-stu-id="34e0d-172">These reports are still available in the Azure classic portal, but they will be deprecated at some time in the future.</span></span>

<span data-ttu-id="34e0d-173">Para más información, consulte [Eventos de riesgo de Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="34e0d-173">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="34e0d-174">Eventos de riesgo detectados</span><span class="sxs-lookup"><span data-stu-id="34e0d-174">Detected risk events</span></span>

<span data-ttu-id="34e0d-175">En Azure Portal, puede tener acceso a los informes sobre eventos de riesgo detectados en la hoja **Azure Active Directory**, en **SEGURIDAD**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-175">In the Azure portal, you can access reports about detected risk events on the **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="34e0d-176">En los informes siguientes se hace un seguimiento de los eventos de riesgo detectados:</span><span class="sxs-lookup"><span data-stu-id="34e0d-176">Detected risk events are tracked in the following reports:</span></span>   

- <span data-ttu-id="34e0d-177">Usuarios en riesgo</span><span class="sxs-lookup"><span data-stu-id="34e0d-177">Users at Risk</span></span>
- <span data-ttu-id="34e0d-178">Inicios de sesión no seguros</span><span class="sxs-lookup"><span data-stu-id="34e0d-178">Risky Sign-ins</span></span>

<span data-ttu-id="34e0d-179">![Informes de seguridad](./media/active-directory-reporting-migration/04.png "Informes de seguridad")</span><span class="sxs-lookup"><span data-stu-id="34e0d-179">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="34e0d-180">Para más información sobre los informes de seguridad, consulte:</span><span class="sxs-lookup"><span data-stu-id="34e0d-180">For more information about security reports, see:</span></span>

- [<span data-ttu-id="34e0d-181">Informe de seguridad de usuarios en riesgo en el portal de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34e0d-181">Users at Risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="34e0d-182">Informe de inicios de sesión poco seguros del portal de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34e0d-182">Risky Sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-the-azure-classic-portal-vs-the-azure-portal"></a><span data-ttu-id="34e0d-183">Informes de actividad en el Portal de Azure clásico frente a Azure Portal</span><span class="sxs-lookup"><span data-stu-id="34e0d-183">Activity reports in the Azure classic portal vs. the Azure portal</span></span>

<span data-ttu-id="34e0d-184">La tabla de esta sección muestra los informes existentes en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="34e0d-184">The table in this section lists existing reports in the Azure classic portal.</span></span> <span data-ttu-id="34e0d-185">También describe cómo puede obtener la misma información en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="34e0d-185">It also describes how you can get the same information in the Azure portal.</span></span>

<span data-ttu-id="34e0d-186">Para ver todos los datos de auditoría, vaya a la hoja **Azure Active Directory** y, en **ACTIVIDAD**, vaya a **Registros de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-186">To view all auditing data, on the **Azure Active Directory** blade, under **ACTIVITY**, go to **Audit logs**.</span></span>

<span data-ttu-id="34e0d-187">![Registros de auditoría](./media/active-directory-reporting-migration/61.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="34e0d-187">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="34e0d-188">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="34e0d-188">Azure classic portal</span></span>                 | <span data-ttu-id="34e0d-189">Para encontrar en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="34e0d-189">To find in the Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="34e0d-190">Registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="34e0d-190">Audit logs</span></span>                           | <span data-ttu-id="34e0d-191">Para **Categoría de actividad**, seleccione **Directorio principal**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-191">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="34e0d-192">Actividad de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="34e0d-192">Password reset activity</span></span>              | <span data-ttu-id="34e0d-193">Para **Categoría de actividad**, seleccione **Administración de contraseñas de autoservicio**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-193">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="34e0d-194">Actividad de registro de restablecimiento de contraseñas</span><span class="sxs-lookup"><span data-stu-id="34e0d-194">Password reset registration activity</span></span> | <span data-ttu-id="34e0d-195">Para **Categoría de actividad**, seleccione **Administración de contraseñas de autoservicio**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-195">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="34e0d-196">Actividad de los grupos de autoservicio</span><span class="sxs-lookup"><span data-stu-id="34e0d-196">Self-service groups activity</span></span>         | <span data-ttu-id="34e0d-197">Para **Categoría de actividad**, seleccione **Administración de grupos de autoservicio**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-197">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="34e0d-198">Actividad de aprovisionamiento de cuentas</span><span class="sxs-lookup"><span data-stu-id="34e0d-198">Account provisioning activity</span></span>        | <span data-ttu-id="34e0d-199">Para **Categoría de actividad**, seleccione **Aprovisionamiento de usuarios de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-199">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="34e0d-200">Estado de la sustitución de contraseña</span><span class="sxs-lookup"><span data-stu-id="34e0d-200">Password rollover status</span></span>             | <span data-ttu-id="34e0d-201">En **Categoría de actividad**, seleccione **Sustitución automática de contraseñas de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-201">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="34e0d-202">Errores de aprovisionamiento de cuentas</span><span class="sxs-lookup"><span data-stu-id="34e0d-202">Account provisioning errors</span></span>          | <span data-ttu-id="34e0d-203">Para **Categoría de actividad**, seleccione **Aprovisionamiento de usuarios de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-203">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="34e0d-204">Cambios de nombre de grupo de Office365</span><span class="sxs-lookup"><span data-stu-id="34e0d-204">Office365 Group Name Changes</span></span>         | <span data-ttu-id="34e0d-205">Para **Categoría de actividad**, seleccione **Administración de contraseñas de autoservicio**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-205">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="34e0d-206">Para **Tipo de recurso de actividad**, seleccione **Grupo**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-206">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="34e0d-207">Para **Origen de la actividad**, seleccione **Grupos de O365**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-207">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="34e0d-208">Para ver el informe **Uso de la aplicación**, vaya a la hoja **Azure Active Directory** y, en **ADMINISTRAR**, seleccione **Aplicaciones empresariales** y, luego, seleccione **Inicios de sesión**.</span><span class="sxs-lookup"><span data-stu-id="34e0d-208">To view the **Application Usage** report, on the **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="34e0d-209">![Informe Inicios de sesión de aplicaciones empresariales](./media/active-directory-reporting-migration/199.png "Informe Inicios de sesión de aplicaciones empresariales")</span><span class="sxs-lookup"><span data-stu-id="34e0d-209">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="34e0d-210">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34e0d-210">Next steps</span></span>

<span data-ttu-id="34e0d-211">Para obtener información general sobre los informes, consulte [Informes de Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="34e0d-211">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
