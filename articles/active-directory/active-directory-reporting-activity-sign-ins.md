---
title: informes de actividad aaaSign en el portal de Azure Active Directory Hola | Documentos de Microsoft
description: "Informes de actividad toosign introducción en el portal de Azure Active Directory Hola"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="332cf-103">Informes de actividad de inicio de sesión en el portal de Azure Active Directory Hola</span><span class="sxs-lookup"><span data-stu-id="332cf-103">Sign-in activity reports in hello Azure Active Directory portal</span></span>

<span data-ttu-id="332cf-104">Con Azure Active Directory (Azure AD) informes en hello [portal de Azure](https://portal.azure.com), puede obtener información de hello necesita toodetermine cómo está haciendo su entorno.</span><span class="sxs-lookup"><span data-stu-id="332cf-104">With Azure Active Directory (Azure AD) reporting in hello [Azure portal](https://portal.azure.com), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="332cf-105">Hola reporting arquitectura en Azure Active Directory consta de Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="332cf-105">hello reporting architecture in Azure Active Directory consists of hello following components:</span></span>

- <span data-ttu-id="332cf-106">**Actividad**</span><span class="sxs-lookup"><span data-stu-id="332cf-106">**Activity**</span></span> 
    - <span data-ttu-id="332cf-107">**Las actividades de inicio de sesión** : información sobre el uso de Hola de las aplicaciones administradas y las actividades de inicio de sesión de usuario</span><span class="sxs-lookup"><span data-stu-id="332cf-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="332cf-108">**Registros de auditoría**: información de la actividad del sistema sobre los usuarios y la administración de grupos, sus aplicaciones administradas y actividades de directorio.</span><span class="sxs-lookup"><span data-stu-id="332cf-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="332cf-109">**Seguridad**</span><span class="sxs-lookup"><span data-stu-id="332cf-109">**Security**</span></span> 
    - <span data-ttu-id="332cf-110">**Inicios de sesión arriesgados** -un inicio de sesión de riesgo es un indicador de un intento de inicio de sesión que es posible que se han realizado por alguien que no es propietario legítimo de Hola de una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="332cf-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="332cf-111">Para más información, consulte Inicios de no seguros.</span><span class="sxs-lookup"><span data-stu-id="332cf-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="332cf-112">**Usuarios marcados en riesgo**: un usuario en peligro es un indicador de una cuenta de usuario que puede haber estado en peligro.</span><span class="sxs-lookup"><span data-stu-id="332cf-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="332cf-113">Para más información, consulte la sección Usuarios marcados en riesgo.</span><span class="sxs-lookup"><span data-stu-id="332cf-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="332cf-114">Este tema ofrece una visión general de las actividades de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="332cf-114">This topic gives you an overview of hello sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="332cf-115">Requisito previo</span><span class="sxs-lookup"><span data-stu-id="332cf-115">Pre-requisite</span></span>

### <a name="who-can-access-hello-data"></a><span data-ttu-id="332cf-116">¿Quién puede tener acceso a datos de hello?</span><span class="sxs-lookup"><span data-stu-id="332cf-116">Who can access hello data?</span></span>
* <span data-ttu-id="332cf-117">Usuarios de rol de administrador de seguridad o seguridad lector Hola</span><span class="sxs-lookup"><span data-stu-id="332cf-117">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="332cf-118">Administradores globales</span><span class="sxs-lookup"><span data-stu-id="332cf-118">Global Admins</span></span>
* <span data-ttu-id="332cf-119">Cualquier usuario (no administradores) puede acceder a sus propios inicios de sesión</span><span class="sxs-lookup"><span data-stu-id="332cf-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a><span data-ttu-id="332cf-120">¿Qué licencia de Azure AD necesita tooaccess actividad de inicio de sesión?</span><span class="sxs-lookup"><span data-stu-id="332cf-120">What Azure AD license do you need tooaccess sign-in activity?</span></span>
* <span data-ttu-id="332cf-121">El inquilino debe tener una licencia de Azure AD Premium asociada toosee Hola todo inicio de sesión-informe de actividad</span><span class="sxs-lookup"><span data-stu-id="332cf-121">Your tenant must have an Azure AD Premium license associated with it toosee hello all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="332cf-122">Actividades de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="332cf-122">Signs-in activities</span></span>

<span data-ttu-id="332cf-123">Con información de hello proporcionada por informe de inicio de sesión de usuario de hello, encontrar respuestas tooquestions como:</span><span class="sxs-lookup"><span data-stu-id="332cf-123">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

* <span data-ttu-id="332cf-124">¿Qué es el patrón de inicio de sesión de Hola de un usuario?</span><span class="sxs-lookup"><span data-stu-id="332cf-124">What is hello sign-in pattern of a user?</span></span>
* <span data-ttu-id="332cf-125">¿Cuántos usuarios tienen usuarios que han iniciado sesión durante una semana?</span><span class="sxs-lookup"><span data-stu-id="332cf-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="332cf-126">¿Cuál es el estado de Hola de estos inicios de sesión?</span><span class="sxs-lookup"><span data-stu-id="332cf-126">What’s hello status of these sign-ins?</span></span>

<span data-ttu-id="332cf-127">Las primera entrada tooall de punto de inicio de sesión en las actividades datos están **inicios de sesión** en la sección de la actividad de hello **Azure Active**.</span><span class="sxs-lookup"><span data-stu-id="332cf-127">Your first entry point tooall sign-in activities data is **Sign-ins** in hello Activity section of **Azure Active**.</span></span>


<span data-ttu-id="332cf-128">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/61.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="332cf-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="332cf-129">Un registro de auditoría tiene una vista de lista predeterminada que muestra:</span><span class="sxs-lookup"><span data-stu-id="332cf-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="332cf-130">usuario relacionado Hola</span><span class="sxs-lookup"><span data-stu-id="332cf-130">hello related user</span></span>
- <span data-ttu-id="332cf-131">usuario de la aplicación Hola Hola ha iniciado sesión en</span><span class="sxs-lookup"><span data-stu-id="332cf-131">hello application hello user has signed-in to</span></span>
- <span data-ttu-id="332cf-132">estado de inicio de sesión de Hola</span><span class="sxs-lookup"><span data-stu-id="332cf-132">hello sign-in status</span></span>
- <span data-ttu-id="332cf-133">hora de inicio de sesión Hola</span><span class="sxs-lookup"><span data-stu-id="332cf-133">hello sign-in time</span></span>

<span data-ttu-id="332cf-134">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/41.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="332cf-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="332cf-135">Puede personalizar la vista de lista Hola haciendo clic en **columnas** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="332cf-135">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="332cf-136">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/19.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="332cf-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="332cf-137">Esto permite los campos adicionales de toodisplay o quitar los campos que ya se muestran.</span><span class="sxs-lookup"><span data-stu-id="332cf-137">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="332cf-138">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/42.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="332cf-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="332cf-139">Si hace clic en un elemento en la vista de lista de hello, obtener todos los detalles disponibles sobre él.</span><span class="sxs-lookup"><span data-stu-id="332cf-139">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="332cf-140">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/43.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="332cf-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="332cf-141">Filtrado de actividades de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="332cf-141">Filtering sign-in activities</span></span>

<span data-ttu-id="332cf-142">toonarrow hacia abajo Hola informó de un nivel de tooa de datos que funciona para usted, puede filtrar datos de inicios de sesión de hello mediante Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="332cf-142">toonarrow down hello reported data tooa level that works for you, you can filter hello sign-ins data using hello following fields:</span></span>

- <span data-ttu-id="332cf-143">Intervalo de tiempo</span><span class="sxs-lookup"><span data-stu-id="332cf-143">Time interval</span></span>
- <span data-ttu-id="332cf-144">Usuario</span><span class="sxs-lookup"><span data-stu-id="332cf-144">User</span></span>
- <span data-ttu-id="332cf-145">Application</span><span class="sxs-lookup"><span data-stu-id="332cf-145">Application</span></span>
- <span data-ttu-id="332cf-146">Cliente</span><span class="sxs-lookup"><span data-stu-id="332cf-146">Client</span></span>
- <span data-ttu-id="332cf-147">Estado de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="332cf-147">Sign-in status</span></span>

<span data-ttu-id="332cf-148">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/44.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="332cf-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="332cf-149">Hola **intervalo de tiempo** filtro permite tooyou toodefine un período de tiempo para hello devolvió datos.</span><span class="sxs-lookup"><span data-stu-id="332cf-149">hello **time interval** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="332cf-150">Los valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="332cf-150">Possible values are:</span></span>

- <span data-ttu-id="332cf-151">1 mes</span><span class="sxs-lookup"><span data-stu-id="332cf-151">1 month</span></span>
- <span data-ttu-id="332cf-152">7 días</span><span class="sxs-lookup"><span data-stu-id="332cf-152">7 days</span></span>
- <span data-ttu-id="332cf-153">24 horas</span><span class="sxs-lookup"><span data-stu-id="332cf-153">24 hours</span></span>
- <span data-ttu-id="332cf-154">Personalizado</span><span class="sxs-lookup"><span data-stu-id="332cf-154">Custom</span></span>

<span data-ttu-id="332cf-155">Cuando se selecciona un intervalo de tiempo personalizado, puede configurar una hora de inicio y una hora de finalización.</span><span class="sxs-lookup"><span data-stu-id="332cf-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="332cf-156">Hola **usuario** filtro le permite toospecify nombre de Hola u Hola nombre principal de usuario (UPN) del usuario de Hola que le interesa.</span><span class="sxs-lookup"><span data-stu-id="332cf-156">hello **user** filter enables you toospecify hello name or hello user principal name (UPN) of hello user you care about.</span></span>

<span data-ttu-id="332cf-157">Hola **aplicación** filtro permite un nombre de hello toospecify de aplicación Hola que le interesa.</span><span class="sxs-lookup"><span data-stu-id="332cf-157">hello **application** filter enables you toospecify hello name of hello application you care about.</span></span>

<span data-ttu-id="332cf-158">Hola **cliente** filtro le permite toospecify información acerca del dispositivo de Hola que le interesa.</span><span class="sxs-lookup"><span data-stu-id="332cf-158">hello **client** filter enables you toospecify information about hello device you care about.</span></span>

<span data-ttu-id="332cf-159">Hola **estado de inicio de sesión** filtro le permite tooselect de hello siguiente filtro:</span><span class="sxs-lookup"><span data-stu-id="332cf-159">hello **sign-in status** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="332cf-160">Todo</span><span class="sxs-lookup"><span data-stu-id="332cf-160">All</span></span>
- <span data-ttu-id="332cf-161">Correcto</span><span class="sxs-lookup"><span data-stu-id="332cf-161">Success</span></span>
- <span data-ttu-id="332cf-162">Error</span><span class="sxs-lookup"><span data-stu-id="332cf-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="332cf-163">Métodos abreviados de las actividades de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="332cf-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="332cf-164">Además tooAzure Active Directory, Hola portal de Azure le ofrece dos toosign en actividades de datos de puntos de entrada adicional:</span><span class="sxs-lookup"><span data-stu-id="332cf-164">In addition tooAzure Active Directory, hello Azure portal provides you with two additional entry points toosign-in activities data:</span></span>

- <span data-ttu-id="332cf-165">Usuarios y grupos</span><span class="sxs-lookup"><span data-stu-id="332cf-165">Users and groups</span></span>
- <span data-ttu-id="332cf-166">Aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="332cf-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="332cf-167">Actividades de inicios de sesión de usuarios y grupos</span><span class="sxs-lookup"><span data-stu-id="332cf-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="332cf-168">Con información de hello proporcionada por informe de inicio de sesión de usuario de hello, encontrar respuestas tooquestions como:</span><span class="sxs-lookup"><span data-stu-id="332cf-168">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

- <span data-ttu-id="332cf-169">¿Qué es el patrón de inicio de sesión de Hola de un usuario?</span><span class="sxs-lookup"><span data-stu-id="332cf-169">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="332cf-170">¿Cuántos usuarios tienen usuarios que han iniciado sesión durante una semana?</span><span class="sxs-lookup"><span data-stu-id="332cf-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="332cf-171">¿Cuál es el estado de Hola de estos inicios de sesión?</span><span class="sxs-lookup"><span data-stu-id="332cf-171">What’s hello status of these sign-ins?</span></span>



<span data-ttu-id="332cf-172">Los datos de toothis de punto de entrada están Hola usuario inicio de sesión gráfico Hola **Introducción** sección en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="332cf-172">Your entry point toothis data is hello user sign-in graph in hello **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="332cf-173">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/45.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="332cf-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="332cf-174">gráfico de inicio de sesión de usuario de Hello muestra agregaciones semanales de inicio de sesión inicios para todos los usuarios en un período de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="332cf-174">hello user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="332cf-175">valor predeterminado de Hola para hello período de tiempo es 30 días.</span><span class="sxs-lookup"><span data-stu-id="332cf-175">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="332cf-176">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/46.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="332cf-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="332cf-177">Al hacer clic en un día en el gráfico de inicio de sesión de hello, obtendrá una lista detallada de las actividades de inicio de sesión de Hola para este día.</span><span class="sxs-lookup"><span data-stu-id="332cf-177">When you click on a day in hello sign-in graph, you get a detailed list of hello sign-in activities for this day.</span></span>

<span data-ttu-id="332cf-178">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/41.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="332cf-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="332cf-179">Cada fila de la lista encontrará hello las actividades de inicio de sesión que Hola información detallada sobre el inicio de sesión en hello seleccionado como:</span><span class="sxs-lookup"><span data-stu-id="332cf-179">Each row in hello sign-in activities list gives you hello detailed information about hello selected sign-in such as:</span></span>

* <span data-ttu-id="332cf-180">¿Quién ha iniciado sesión?</span><span class="sxs-lookup"><span data-stu-id="332cf-180">Who has signed in?</span></span>
* <span data-ttu-id="332cf-181">¿Cuál era hello relacionado con el UPN?</span><span class="sxs-lookup"><span data-stu-id="332cf-181">What was hello related UPN?</span></span>
* <span data-ttu-id="332cf-182">¿La aplicación era destino Hola del inicio de sesión de hello?</span><span class="sxs-lookup"><span data-stu-id="332cf-182">What application was hello target of hello sign-in?</span></span>
* <span data-ttu-id="332cf-183">¿Cuál es la dirección IP de hello del inicio de sesión de hello?</span><span class="sxs-lookup"><span data-stu-id="332cf-183">What is hello IP address of hello sign-in?</span></span>
* <span data-ttu-id="332cf-184">¿Cuál era el estado de hello del inicio de sesión de hello?</span><span class="sxs-lookup"><span data-stu-id="332cf-184">What was hello status of hello sign-in?</span></span>

<span data-ttu-id="332cf-185">Hola **inicios de sesión** opción ofrece una descripción completa de todos los inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="332cf-185">hello **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="332cf-186">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/51.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="332cf-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="332cf-187">Uso de las aplicaciones administradas</span><span class="sxs-lookup"><span data-stu-id="332cf-187">Usage of managed applications</span></span>

<span data-ttu-id="332cf-188">Con una vista centrada en la aplicación de los datos de inicio de sesión, puede responder a preguntas tales como:</span><span class="sxs-lookup"><span data-stu-id="332cf-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="332cf-189">¿Quién está usando mis aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="332cf-189">Who is using my applications?</span></span>
* <span data-ttu-id="332cf-190">¿Qué Hola 3 las aplicaciones principales de su organización?</span><span class="sxs-lookup"><span data-stu-id="332cf-190">What are hello top 3 applications in your organization?</span></span>
* <span data-ttu-id="332cf-191">Recientemente he implementado una aplicación.</span><span class="sxs-lookup"><span data-stu-id="332cf-191">I have recently rolled out an application.</span></span> <span data-ttu-id="332cf-192">¿Cómo sigue?</span><span class="sxs-lookup"><span data-stu-id="332cf-192">How is it doing?</span></span>

<span data-ttu-id="332cf-193">Los datos de toothis de punto de entrada están Hola 3 las aplicaciones principales de su organización en último informe de 30 días Hola Hola **Introducción** sección bajo **aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="332cf-193">Your entry point toothis data is hello top 3 applications in your organization within hello last 30 days report in hello **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="332cf-194">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/64.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="332cf-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="332cf-195">Hola aplicación gráfico semanal agregaciones de uso de inicios de sesión para las aplicaciones de la parte superior a 3 en un período de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="332cf-195">hello app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="332cf-196">valor predeterminado de Hola para hello período de tiempo es 30 días.</span><span class="sxs-lookup"><span data-stu-id="332cf-196">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="332cf-197">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/47.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="332cf-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="332cf-198">Si desea, puede establecer el foco de hello en una aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="332cf-198">If you want to, you can set hello focus on a specific application.</span></span>


<span data-ttu-id="332cf-199">![Informes](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Informes")</span><span class="sxs-lookup"><span data-stu-id="332cf-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="332cf-200">Al hacer clic en un día en el gráfico de uso de aplicación Hola, obtendrá una lista detallada de las actividades de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="332cf-200">When you click on a day in hello app usage graph, you get a detailed list of hello sign-in activities.</span></span>


<span data-ttu-id="332cf-201">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/48.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="332cf-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="332cf-202">Hola **inicios de sesión** opción ofrece una descripción completa de todas las aplicaciones de tooyour de inicio de sesión de eventos.</span><span class="sxs-lookup"><span data-stu-id="332cf-202">hello **Sign-ins** option gives you a complete overview of all sign-in events tooyour applications.</span></span>

<span data-ttu-id="332cf-203">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/49.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="332cf-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="332cf-204">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="332cf-204">Next steps</span></span>

<span data-ttu-id="332cf-205">Si desea más información acerca de los códigos de error de inicio de sesión de la actividad tooknow, vea hello [inicio de sesión de códigos de error de actividad informes en el portal de Azure Active Directory hello](active-directory-reporting-activity-sign-ins-errors.md).</span><span class="sxs-lookup"><span data-stu-id="332cf-205">If you want tooknow more about sign-in activity error codes, see hello [Sign-in activity report error codes in hello Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

