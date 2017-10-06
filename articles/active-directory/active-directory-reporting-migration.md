---
title: los informes de actividad de aaaFind de hello portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo se notifica toofind actividad de Azure Active Directory en hello portal de Azure."
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
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a><span data-ttu-id="af189-103">Buscar informes de actividad en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="af189-103">Find activity reports in hello Azure portal</span></span>

<span data-ttu-id="af189-104">Si va a mover de hello Azure toohello portal clásico de portal de Azure, obtendrá un nuevo aspecto en registros de actividad de Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="af189-104">If you are moving from hello Azure classic portal toohello Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="af189-105">En una encuesta reciente [entrada de blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), explicamos cómo puede ver registros de actividad en el contexto de hello del recurso de saludo está trabajando en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="af189-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in hello context of hello resource you are working on in hello Azure portal.</span></span> <span data-ttu-id="af189-106">En este artículo se describe cómo toofind informa que usó en el portal de Azure clásico en el portal de Azure Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="af189-106">In this article, we describe how toofind reports that you used in hello Azure classic portal in hello Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="af189-107">Novedades</span><span class="sxs-lookup"><span data-stu-id="af189-107">What's new</span></span>

<span data-ttu-id="af189-108">Informes en el portal de Azure clásico Hola se dividen en categorías:</span><span class="sxs-lookup"><span data-stu-id="af189-108">Reports in hello Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="af189-109">Informes de seguridad</span><span class="sxs-lookup"><span data-stu-id="af189-109">Security reports</span></span>
2.  <span data-ttu-id="af189-110">Informes de actividad</span><span class="sxs-lookup"><span data-stu-id="af189-110">Activity reports</span></span>
3.  <span data-ttu-id="af189-111">Informes de aplicaciones integradas</span><span class="sxs-lookup"><span data-stu-id="af189-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="af189-112">Informes de actividad y de aplicaciones integradas</span><span class="sxs-lookup"><span data-stu-id="af189-112">Activity and integrated app reports</span></span>

<span data-ttu-id="af189-113">Para generación de informes basada en contexto en hello portal de Azure, los informes existentes se combinan en una sola vista.</span><span class="sxs-lookup"><span data-stu-id="af189-113">For context-based reporting in hello Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="af189-114">Una única API subyacente proporciona Hola datos toohello vista.</span><span class="sxs-lookup"><span data-stu-id="af189-114">A single, underlying API provides hello data toohello view.</span></span>

<span data-ttu-id="af189-115">toosee esta vista, en hello **Azure Active Directory** hoja, en **actividad**, seleccione **registros de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="af189-115">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="af189-116">![Registros de auditoría](./media/active-directory-reporting-migration/482.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="af189-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="af189-117">Hola siguientes informes está consolidado en esta vista:</span><span class="sxs-lookup"><span data-stu-id="af189-117">hello following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="af189-118">Informe de auditoría</span><span class="sxs-lookup"><span data-stu-id="af189-118">Audit report</span></span>
-   <span data-ttu-id="af189-119">Actividad de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="af189-119">Password reset activity</span></span>
-   <span data-ttu-id="af189-120">Actividad de registro de restablecimiento de contraseñas</span><span class="sxs-lookup"><span data-stu-id="af189-120">Password reset registration activity</span></span>
-   <span data-ttu-id="af189-121">Actividad de los grupos de autoservicio</span><span class="sxs-lookup"><span data-stu-id="af189-121">Self-service groups activity</span></span>
-   <span data-ttu-id="af189-122">Cambios de nombre de grupo de Office365</span><span class="sxs-lookup"><span data-stu-id="af189-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="af189-123">Actividad de aprovisionamiento de cuentas</span><span class="sxs-lookup"><span data-stu-id="af189-123">Account provisioning activity</span></span>
-   <span data-ttu-id="af189-124">Estado de la sustitución de contraseña</span><span class="sxs-lookup"><span data-stu-id="af189-124">Password rollover status</span></span>
-   <span data-ttu-id="af189-125">Errores de aprovisionamiento de cuentas</span><span class="sxs-lookup"><span data-stu-id="af189-125">Account provisioning errors</span></span>


<span data-ttu-id="af189-126">Hola informes de uso de la aplicación se ha mejorado y se incluye en hello **inicios de sesión** vista.</span><span class="sxs-lookup"><span data-stu-id="af189-126">hello Application Usage report has been enhanced and is included in hello **Sign-ins** view.</span></span> <span data-ttu-id="af189-127">toosee esta vista, en hello **Azure Active Directory** hoja, en **actividad**, seleccione **inicios de sesión**.</span><span class="sxs-lookup"><span data-stu-id="af189-127">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="af189-128">![Vista de inicios de sesión](./media/active-directory-reporting-migration/483.png "Vista de inicios de sesión")</span><span class="sxs-lookup"><span data-stu-id="af189-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="af189-129">Hola **inicios de sesión** vista incluye todos los inicios de sesión. Puede utilizar esta información de uso de aplicaciones de tooget de información.</span><span class="sxs-lookup"><span data-stu-id="af189-129">hello **Sign-ins** view includes all user sign-ins. You can use this information tooget application usage information.</span></span> <span data-ttu-id="af189-130">También puede ver información de uso de la aplicación Hola **aplicaciones empresariales** información general, en hello **administrar** sección.</span><span class="sxs-lookup"><span data-stu-id="af189-130">You also can view application usage information in hello **Enterprise applications** overview, in hello **MANAGE** section.</span></span>

<span data-ttu-id="af189-131">![Aplicaciones empresariales](./media/active-directory-reporting-migration/484.png "Aplicaciones empresariales")</span><span class="sxs-lookup"><span data-stu-id="af189-131">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="af189-132">Acceso a un informe específico</span><span class="sxs-lookup"><span data-stu-id="af189-132">Access a specific report</span></span>

<span data-ttu-id="af189-133">Aunque Hola portal de Azure ofrece una vista única, también puede buscar en informes específicos.</span><span class="sxs-lookup"><span data-stu-id="af189-133">Although hello Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="af189-134">Registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="af189-134">Audit logs</span></span>

<span data-ttu-id="af189-135">Comentarios de respuesta toocustomer, Hola portal de Azure, puede usar avanzadas filtrado tooaccess Hola de datos que desee.</span><span class="sxs-lookup"><span data-stu-id="af189-135">In response toocustomer feedback, in hello Azure portal, you can use advanced filtering tooaccess hello data you want.</span></span> <span data-ttu-id="af189-136">Es un filtro que se puede usar un *categoría de actividad*, que enumeran Hola diferentes tipos de actividad registra en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af189-136">One filter you can use is an *activity category*, which lists hello different types of activity logs in Azure AD.</span></span> <span data-ttu-id="af189-137">toonarrow toowhat de resultados que está buscando, puede seleccionar una categoría.</span><span class="sxs-lookup"><span data-stu-id="af189-137">toonarrow results toowhat you are looking for, you can select a category.</span></span>

<span data-ttu-id="af189-138">Por ejemplo, si está interesado en los restablecimientos de contraseña de tooself servicio relacionado de actividades, puede elegir hello **administración de contraseñas de autoservicio** categoría.</span><span class="sxs-lookup"><span data-stu-id="af189-138">For example, if you are interested only in activities related tooself-service password resets, you can choose hello **Self-service Password Management** category.</span></span> <span data-ttu-id="af189-139">categorías de Hello que verá se basan en recursos de hello en que si está trabajando.</span><span class="sxs-lookup"><span data-stu-id="af189-139">hello categories you see are based on hello resource you are working in.</span></span>  

<span data-ttu-id="af189-140">![Opciones de la categoría en la página de registros de auditoría de filtro de hello](./media/active-directory-reporting-migration/06.png "opciones de la categoría en la página de registros de auditoría de filtro de Hola")</span><span class="sxs-lookup"><span data-stu-id="af189-140">![Category options on hello Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on hello Filter Audit Logs page")</span></span>

<span data-ttu-id="af189-141">Las categorías de actividad incluyen:</span><span class="sxs-lookup"><span data-stu-id="af189-141">Activity categories include:</span></span>

- <span data-ttu-id="af189-142">Core Directory (Directorio principal)</span><span class="sxs-lookup"><span data-stu-id="af189-142">Core Directory</span></span>
- <span data-ttu-id="af189-143">Self-service Password Management (Administración de contraseñas de autorservicio)</span><span class="sxs-lookup"><span data-stu-id="af189-143">Self-service Password Management</span></span>
- <span data-ttu-id="af189-144">Self-service Group Management (Administración de grupos de autoservicio)</span><span class="sxs-lookup"><span data-stu-id="af189-144">Self-service Group Management</span></span>
- <span data-ttu-id="af189-145">Account Provisioning (Aprovisionamiento de cuentas)</span><span class="sxs-lookup"><span data-stu-id="af189-145">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="af189-146">Uso de la aplicación</span><span class="sxs-lookup"><span data-stu-id="af189-146">Application usage</span></span>

<span data-ttu-id="af189-147">tooview los detalles sobre el uso de la aplicación para todas las aplicaciones o para una sola aplicación en **actividad**, seleccione **inicios de sesión**. resultados de hello toonarrow, puede filtrar por nombre de usuario o nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="af189-147">tooview details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**. toonarrow hello results, you can filter on user name or application name.</span></span>

<span data-ttu-id="af189-148">![Página Filtrar eventos de inicio de sesión](./media/active-directory-reporting-migration/07.png "Página Filtrar eventos de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="af189-148">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="af189-149">Informes de seguridad</span><span class="sxs-lookup"><span data-stu-id="af189-149">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="af189-150">Informes de actividades anómalas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="af189-150">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="af189-151">Seguridad de Azure AD actividad anómala informes desde el portal de Azure clásico Hola han sido tooprovide consolidado a una, vista central.</span><span class="sxs-lookup"><span data-stu-id="af189-151">Azure AD anomalous activity security reports from hello Azure classic portal have been consolidated tooprovide you with one, central view.</span></span> <span data-ttu-id="af189-152">Esta vista muestra todos los eventos de riesgo relacionados con la seguridad que Azure AD puede detectar e informar.</span><span class="sxs-lookup"><span data-stu-id="af189-152">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="af189-153">Hello en la tabla siguiente enumera los tipos de eventos de riesgo correspondientes en hello portal de Azure e informes de seguridad de actividad anómala de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af189-153">hello following table lists hello Azure AD anomalous activity security reports, and corresponding risk event types in hello Azure portal.</span></span>

| <span data-ttu-id="af189-154">Informe de actividad anómala de Azure AD</span><span class="sxs-lookup"><span data-stu-id="af189-154">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="af189-155">Tipo de evento de riesgo de Identity Protection</span><span class="sxs-lookup"><span data-stu-id="af189-155">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="af189-156">Usuarios con credenciales perdidas</span><span class="sxs-lookup"><span data-stu-id="af189-156">Users with leaked credentials</span></span> | <span data-ttu-id="af189-157">Credenciales con fugas</span><span class="sxs-lookup"><span data-stu-id="af189-157">Leaked credentials</span></span> |
| <span data-ttu-id="af189-158">Actividad de inicio de sesión irregular</span><span class="sxs-lookup"><span data-stu-id="af189-158">Irregular sign-in activity</span></span> | <span data-ttu-id="af189-159">Viaje imposible tooatypical ubicaciones</span><span class="sxs-lookup"><span data-stu-id="af189-159">Impossible travel tooatypical locations</span></span> |
| <span data-ttu-id="af189-160">Inicios de sesión desde dispositivos posiblemente infectados</span><span class="sxs-lookup"><span data-stu-id="af189-160">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="af189-161">Inicios de sesión desde dispositivos infectados</span><span class="sxs-lookup"><span data-stu-id="af189-161">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="af189-162">Inicios de sesión desde orígenes desconocidos</span><span class="sxs-lookup"><span data-stu-id="af189-162">Sign-ins from unknown sources</span></span> | <span data-ttu-id="af189-163">Inicios de sesión desde direcciones IP anónimas</span><span class="sxs-lookup"><span data-stu-id="af189-163">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="af189-164">Inicios de sesión desde direcciones IP con actividad sospechosa</span><span class="sxs-lookup"><span data-stu-id="af189-164">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="af189-165">Inicios de sesión desde direcciones IP con actividad sospechosa</span><span class="sxs-lookup"><span data-stu-id="af189-165">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="af189-166">Inicios de sesión desde ubicaciones desconocidas</span><span class="sxs-lookup"><span data-stu-id="af189-166">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="af189-167">Hola después de seguridad de la actividad anómala de Azure AD informa que no se incluyen como eventos de riesgo en hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="af189-167">hello following Azure AD anomalous activity security reports are not included as risk events in hello Azure portal:</span></span>

* <span data-ttu-id="af189-168">Inicios de sesión tras varios errores</span><span class="sxs-lookup"><span data-stu-id="af189-168">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="af189-169">Inicios de sesión desde varias ubicaciones geográficas</span><span class="sxs-lookup"><span data-stu-id="af189-169">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="af189-170">Estos informes siguen estando disponibles en el portal de Azure clásico hello, pero dejará de utilizarse en algún momento futuro Hola.</span><span class="sxs-lookup"><span data-stu-id="af189-170">These reports are still available in hello Azure classic portal, but they will be deprecated at some time in hello future.</span></span>

<span data-ttu-id="af189-171">Para más información, consulte [Eventos de riesgo de Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="af189-171">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="af189-172">Eventos de riesgo detectados</span><span class="sxs-lookup"><span data-stu-id="af189-172">Detected risk events</span></span>

<span data-ttu-id="af189-173">Hola portal de Azure, puede tener acceso a informes acerca de los eventos de riesgo detectados en hello **Azure Active Directory** hoja, en **seguridad**.</span><span class="sxs-lookup"><span data-stu-id="af189-173">In hello Azure portal, you can access reports about detected risk events on hello **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="af189-174">Se realiza el seguimiento de eventos de riesgo detectados en hello después de informes:</span><span class="sxs-lookup"><span data-stu-id="af189-174">Detected risk events are tracked in hello following reports:</span></span>   

- <span data-ttu-id="af189-175">Usuarios en riesgo</span><span class="sxs-lookup"><span data-stu-id="af189-175">Users at Risk</span></span>
- <span data-ttu-id="af189-176">Inicios de sesión no seguros</span><span class="sxs-lookup"><span data-stu-id="af189-176">Risky Sign-ins</span></span>

<span data-ttu-id="af189-177">![Informes de seguridad](./media/active-directory-reporting-migration/04.png "Informes de seguridad")</span><span class="sxs-lookup"><span data-stu-id="af189-177">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="af189-178">Para más información sobre los informes de seguridad, consulte:</span><span class="sxs-lookup"><span data-stu-id="af189-178">For more information about security reports, see:</span></span>

- [<span data-ttu-id="af189-179">Usuarios de informes de seguridad de riesgo en el portal de Azure Active Directory Hola</span><span class="sxs-lookup"><span data-stu-id="af189-179">Users at Risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="af189-180">Riesgo informe de inicios de sesión en el portal de Azure Active Directory Hola</span><span class="sxs-lookup"><span data-stu-id="af189-180">Risky Sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a><span data-ttu-id="af189-181">Informes de actividad en hello portal de Azure clásico frente a Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="af189-181">Activity reports in hello Azure classic portal vs. hello Azure portal</span></span>

<span data-ttu-id="af189-182">tabla de Hello en esta sección enumeran los informes existentes en hello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="af189-182">hello table in this section lists existing reports in hello Azure classic portal.</span></span> <span data-ttu-id="af189-183">También se describe cómo puede obtener Hola la misma información en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="af189-183">It also describes how you can get hello same information in hello Azure portal.</span></span>

<span data-ttu-id="af189-184">tooview todos los datos, en Hola de auditoría **Azure Active Directory** hoja, en **actividad**, vaya demasiado**registros de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="af189-184">tooview all auditing data, on hello **Azure Active Directory** blade, under **ACTIVITY**, go too**Audit logs**.</span></span>

<span data-ttu-id="af189-185">![Registros de auditoría](./media/active-directory-reporting-migration/61.png "Registros de auditoría")</span><span class="sxs-lookup"><span data-stu-id="af189-185">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="af189-186">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="af189-186">Azure classic portal</span></span>                 | <span data-ttu-id="af189-187">toofind Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="af189-187">toofind in hello Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="af189-188">Registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="af189-188">Audit logs</span></span>                           | <span data-ttu-id="af189-189">Para **Categoría de actividad**, seleccione **Directorio principal**.</span><span class="sxs-lookup"><span data-stu-id="af189-189">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="af189-190">Actividad de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="af189-190">Password reset activity</span></span>              | <span data-ttu-id="af189-191">Para **Categoría de actividad**, seleccione **Administración de contraseñas de autoservicio**.</span><span class="sxs-lookup"><span data-stu-id="af189-191">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="af189-192">Actividad de registro de restablecimiento de contraseñas</span><span class="sxs-lookup"><span data-stu-id="af189-192">Password reset registration activity</span></span> | <span data-ttu-id="af189-193">Para **Categoría de actividad**, seleccione **Administración de contraseñas de autoservicio**.</span><span class="sxs-lookup"><span data-stu-id="af189-193">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="af189-194">Actividad de los grupos de autoservicio</span><span class="sxs-lookup"><span data-stu-id="af189-194">Self-service groups activity</span></span>         | <span data-ttu-id="af189-195">Para **Categoría de actividad**, seleccione **Administración de grupos de autoservicio**.</span><span class="sxs-lookup"><span data-stu-id="af189-195">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="af189-196">Actividad de aprovisionamiento de cuentas</span><span class="sxs-lookup"><span data-stu-id="af189-196">Account provisioning activity</span></span>        | <span data-ttu-id="af189-197">Para **Categoría de actividad**, seleccione **Aprovisionamiento de usuarios de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="af189-197">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="af189-198">Estado de la sustitución de contraseña</span><span class="sxs-lookup"><span data-stu-id="af189-198">Password rollover status</span></span>             | <span data-ttu-id="af189-199">En **Categoría de actividad**, seleccione **Sustitución automática de contraseñas de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="af189-199">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="af189-200">Errores de aprovisionamiento de cuentas</span><span class="sxs-lookup"><span data-stu-id="af189-200">Account provisioning errors</span></span>          | <span data-ttu-id="af189-201">Para **Categoría de actividad**, seleccione **Aprovisionamiento de usuarios de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="af189-201">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="af189-202">Cambios de nombre de grupo de Office365</span><span class="sxs-lookup"><span data-stu-id="af189-202">Office365 Group Name Changes</span></span>         | <span data-ttu-id="af189-203">Para **Categoría de actividad**, seleccione **Administración de contraseñas de autoservicio**.</span><span class="sxs-lookup"><span data-stu-id="af189-203">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="af189-204">Para **Tipo de recurso de actividad**, seleccione **Grupo**.</span><span class="sxs-lookup"><span data-stu-id="af189-204">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="af189-205">Para **Origen de la actividad**, seleccione **Grupos de O365**.</span><span class="sxs-lookup"><span data-stu-id="af189-205">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="af189-206">Hola tooview **uso de la aplicación** informes en hello **Azure Active Directory** hoja, en **administrar**, seleccione **aplicaciones empresariales**y, a continuación, seleccione **inicios de sesión**.</span><span class="sxs-lookup"><span data-stu-id="af189-206">tooview hello **Application Usage** report, on hello **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="af189-207">![Informe Inicios de sesión de aplicaciones empresariales](./media/active-directory-reporting-migration/199.png "Informe Inicios de sesión de aplicaciones empresariales")</span><span class="sxs-lookup"><span data-stu-id="af189-207">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="af189-208">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af189-208">Next steps</span></span>

<span data-ttu-id="af189-209">Para obtener información general de informes, vea hello [reporting de Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="af189-209">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
