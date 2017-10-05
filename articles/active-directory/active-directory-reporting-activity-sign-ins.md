---
title: "Informes de actividad de inicio de sesión en el portal de Azure Active Directory | Microsoft Docs"
description: "Introducción a los informes de actividad de inicio de sesión en el portal de Azure Active Directory"
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
ms.openlocfilehash: b9e61950654ba427b09dd608d354589a0804aaa5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="87fd8-103">Informes de actividad de inicio de sesión en el portal de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87fd8-103">Sign-in activity reports in the Azure Active Directory portal</span></span>

<span data-ttu-id="87fd8-104">Con los informes de Azure Active Directory (Azure AD) que encontrará en [Azure Portal](https://portal.azure.com), puede obtener toda la información que necesita para determinar cómo marcha el entorno.</span><span class="sxs-lookup"><span data-stu-id="87fd8-104">With Azure Active Directory (Azure AD) reporting in the [Azure portal](https://portal.azure.com), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="87fd8-105">La arquitectura de los informes de Azure Active Directory consta de los siguientes componentes:</span><span class="sxs-lookup"><span data-stu-id="87fd8-105">The reporting architecture in Azure Active Directory consists of the following components:</span></span>

- <span data-ttu-id="87fd8-106">**Actividad**</span><span class="sxs-lookup"><span data-stu-id="87fd8-106">**Activity**</span></span> 
    - <span data-ttu-id="87fd8-107">**Actividades de inicio de sesión** : información sobre el uso de las aplicaciones administradas y las actividades de inicio de sesión de usuario</span><span class="sxs-lookup"><span data-stu-id="87fd8-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="87fd8-108">**Registros de auditoría**: información de la actividad del sistema sobre los usuarios y la administración de grupos, sus aplicaciones administradas y actividades de directorio.</span><span class="sxs-lookup"><span data-stu-id="87fd8-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="87fd8-109">**Seguridad**</span><span class="sxs-lookup"><span data-stu-id="87fd8-109">**Security**</span></span> 
    - <span data-ttu-id="87fd8-110">**Inicios de sesión peligrosos**: un inicio de sesión peligroso es un indicador de un intento de inicio de sesión que puede haber realizado alguien que no es el propietario legítimo de una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="87fd8-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="87fd8-111">Para más información, consulte Inicios de no seguros.</span><span class="sxs-lookup"><span data-stu-id="87fd8-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="87fd8-112">**Usuarios marcados en riesgo**: un usuario en peligro es un indicador de una cuenta de usuario que puede haber estado en peligro.</span><span class="sxs-lookup"><span data-stu-id="87fd8-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="87fd8-113">Para más información, consulte la sección Usuarios marcados en riesgo.</span><span class="sxs-lookup"><span data-stu-id="87fd8-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="87fd8-114">Este tema ofrece una visión general de las actividades de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="87fd8-114">This topic gives you an overview of the sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="87fd8-115">Requisito previo</span><span class="sxs-lookup"><span data-stu-id="87fd8-115">Pre-requisite</span></span>

### <a name="who-can-access-the-data"></a><span data-ttu-id="87fd8-116">¿Quién puede acceder a los datos?</span><span class="sxs-lookup"><span data-stu-id="87fd8-116">Who can access the data?</span></span>
* <span data-ttu-id="87fd8-117">Usuarios de los roles de administrador o lector de seguridad</span><span class="sxs-lookup"><span data-stu-id="87fd8-117">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="87fd8-118">Administradores globales</span><span class="sxs-lookup"><span data-stu-id="87fd8-118">Global Admins</span></span>
* <span data-ttu-id="87fd8-119">Cualquier usuario (no administradores) puede acceder a sus propios inicios de sesión</span><span class="sxs-lookup"><span data-stu-id="87fd8-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-to-access-sign-in-activity"></a><span data-ttu-id="87fd8-120">¿Qué licencia de Azure AD se necesita para acceder a la actividad de inicio de sesión?</span><span class="sxs-lookup"><span data-stu-id="87fd8-120">What Azure AD license do you need to access sign-in activity?</span></span>
* <span data-ttu-id="87fd8-121">El inquilino debe tener una licencia de Azure AD Premium asociada para ver el informe de actividades de inicio de sesión activas</span><span class="sxs-lookup"><span data-stu-id="87fd8-121">Your tenant must have an Azure AD Premium license associated with it to see the all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="87fd8-122">Actividades de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="87fd8-122">Signs-in activities</span></span>

<span data-ttu-id="87fd8-123">Con la información proporcionada por el informe de inicio de sesión del usuario, puede encontrar respuestas a preguntas tales como:</span><span class="sxs-lookup"><span data-stu-id="87fd8-123">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

* <span data-ttu-id="87fd8-124">¿Cuál es el patrón de inicio de sesión de un usuario?</span><span class="sxs-lookup"><span data-stu-id="87fd8-124">What is the sign-in pattern of a user?</span></span>
* <span data-ttu-id="87fd8-125">¿Cuántos usuarios tienen usuarios que han iniciado sesión durante una semana?</span><span class="sxs-lookup"><span data-stu-id="87fd8-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="87fd8-126">¿Cuál es el estado de estos inicios de sesión?</span><span class="sxs-lookup"><span data-stu-id="87fd8-126">What’s the status of these sign-ins?</span></span>

<span data-ttu-id="87fd8-127">El primer punto de entrada a todos los datos de actividades de inicio de sesión es **Inicios de sesión** en la sección Actividad de **Azure Active**.</span><span class="sxs-lookup"><span data-stu-id="87fd8-127">Your first entry point to all sign-in activities data is **Sign-ins** in the Activity section of **Azure Active**.</span></span>


<span data-ttu-id="87fd8-128">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/61.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="87fd8-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="87fd8-129">Un registro de auditoría tiene una vista de lista predeterminada que muestra:</span><span class="sxs-lookup"><span data-stu-id="87fd8-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="87fd8-130">el usuario relacionado,</span><span class="sxs-lookup"><span data-stu-id="87fd8-130">the related user</span></span>
- <span data-ttu-id="87fd8-131">la aplicación en que el usuario ha iniciado sesión,</span><span class="sxs-lookup"><span data-stu-id="87fd8-131">the application the user has signed-in to</span></span>
- <span data-ttu-id="87fd8-132">el estado de inicio de sesión,</span><span class="sxs-lookup"><span data-stu-id="87fd8-132">the sign-in status</span></span>
- <span data-ttu-id="87fd8-133">la hora de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="87fd8-133">the sign-in time</span></span>

<span data-ttu-id="87fd8-134">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/41.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="87fd8-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="87fd8-135">Puede personalizar la vista de lista; para ello, haga clic en **Columnas** en la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="87fd8-135">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="87fd8-136">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/19.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="87fd8-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="87fd8-137">Esto le permite mostrar los campos adicionales o quitar los campos que ya se están mostrando.</span><span class="sxs-lookup"><span data-stu-id="87fd8-137">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="87fd8-138">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/42.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="87fd8-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="87fd8-139">Si hace clic en un elemento de la vista de lista, puede obtener todos los detalles disponibles sobre él.</span><span class="sxs-lookup"><span data-stu-id="87fd8-139">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="87fd8-140">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/43.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="87fd8-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="87fd8-141">Filtrado de actividades de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="87fd8-141">Filtering sign-in activities</span></span>

<span data-ttu-id="87fd8-142">Para restringir los datos del informe a un nivel que se adapte a sus necesidades, puede filtrar los datos de inicio de sesión con los siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="87fd8-142">To narrow down the reported data to a level that works for you, you can filter the sign-ins data using the following fields:</span></span>

- <span data-ttu-id="87fd8-143">Intervalo de tiempo</span><span class="sxs-lookup"><span data-stu-id="87fd8-143">Time interval</span></span>
- <span data-ttu-id="87fd8-144">Usuario</span><span class="sxs-lookup"><span data-stu-id="87fd8-144">User</span></span>
- <span data-ttu-id="87fd8-145">Application</span><span class="sxs-lookup"><span data-stu-id="87fd8-145">Application</span></span>
- <span data-ttu-id="87fd8-146">Cliente</span><span class="sxs-lookup"><span data-stu-id="87fd8-146">Client</span></span>
- <span data-ttu-id="87fd8-147">Estado de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="87fd8-147">Sign-in status</span></span>

<span data-ttu-id="87fd8-148">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/44.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="87fd8-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="87fd8-149">El filtro **Intervalo de tiempo** permite definir un período de tiempo para los datos devueltos.</span><span class="sxs-lookup"><span data-stu-id="87fd8-149">The **time interval** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="87fd8-150">Los valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="87fd8-150">Possible values are:</span></span>

- <span data-ttu-id="87fd8-151">1 mes</span><span class="sxs-lookup"><span data-stu-id="87fd8-151">1 month</span></span>
- <span data-ttu-id="87fd8-152">7 días</span><span class="sxs-lookup"><span data-stu-id="87fd8-152">7 days</span></span>
- <span data-ttu-id="87fd8-153">24 horas</span><span class="sxs-lookup"><span data-stu-id="87fd8-153">24 hours</span></span>
- <span data-ttu-id="87fd8-154">Personalizado</span><span class="sxs-lookup"><span data-stu-id="87fd8-154">Custom</span></span>

<span data-ttu-id="87fd8-155">Cuando se selecciona un intervalo de tiempo personalizado, puede configurar una hora de inicio y una hora de finalización.</span><span class="sxs-lookup"><span data-stu-id="87fd8-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="87fd8-156">El filtro **usuario** permite especificar el nombre o el nombre principal de usuario (UPN) del usuario que le interesa.</span><span class="sxs-lookup"><span data-stu-id="87fd8-156">The **user** filter enables you to specify the name or the user principal name (UPN) of the user you care about.</span></span>

<span data-ttu-id="87fd8-157">El filtro **aplicación** permite especificar el nombre de la aplicación que le interesa.</span><span class="sxs-lookup"><span data-stu-id="87fd8-157">The **application** filter enables you to specify the name of the application you care about.</span></span>

<span data-ttu-id="87fd8-158">El filtro **cliente** permite especificar información sobre el dispositivo que le interesa.</span><span class="sxs-lookup"><span data-stu-id="87fd8-158">The **client** filter enables you to specify information about the device you care about.</span></span>

<span data-ttu-id="87fd8-159">El filtro **estado de inicio de sesión** permite seleccionar uno de los filtros siguientes:</span><span class="sxs-lookup"><span data-stu-id="87fd8-159">The **sign-in status** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="87fd8-160">Todo</span><span class="sxs-lookup"><span data-stu-id="87fd8-160">All</span></span>
- <span data-ttu-id="87fd8-161">Correcto</span><span class="sxs-lookup"><span data-stu-id="87fd8-161">Success</span></span>
- <span data-ttu-id="87fd8-162">Error</span><span class="sxs-lookup"><span data-stu-id="87fd8-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="87fd8-163">Métodos abreviados de las actividades de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="87fd8-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="87fd8-164">Además de Azure Active Directory, Azure Portal proporciona dos puntos de entrada adicionales para datos de actividades de inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="87fd8-164">In addition to Azure Active Directory, the Azure portal provides you with two additional entry points to sign-in activities data:</span></span>

- <span data-ttu-id="87fd8-165">Usuarios y grupos</span><span class="sxs-lookup"><span data-stu-id="87fd8-165">Users and groups</span></span>
- <span data-ttu-id="87fd8-166">Aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="87fd8-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="87fd8-167">Actividades de inicios de sesión de usuarios y grupos</span><span class="sxs-lookup"><span data-stu-id="87fd8-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="87fd8-168">Con la información proporcionada por el informe de inicio de sesión del usuario, puede encontrar respuestas a preguntas tales como:</span><span class="sxs-lookup"><span data-stu-id="87fd8-168">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

- <span data-ttu-id="87fd8-169">¿Cuál es el patrón de inicio de sesión de un usuario?</span><span class="sxs-lookup"><span data-stu-id="87fd8-169">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="87fd8-170">¿Cuántos usuarios tienen usuarios que han iniciado sesión durante una semana?</span><span class="sxs-lookup"><span data-stu-id="87fd8-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="87fd8-171">¿Cuál es el estado de estos inicios de sesión?</span><span class="sxs-lookup"><span data-stu-id="87fd8-171">What’s the status of these sign-ins?</span></span>



<span data-ttu-id="87fd8-172">El punto de entrada a los datos es el gráfico de inicio de sesión del usuario en la sección **Introducción** de **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="87fd8-172">Your entry point to this data is the user sign-in graph in the **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="87fd8-173">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/45.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="87fd8-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="87fd8-174">El gráfico de inicio de sesión de usuario muestra agregaciones semanales de inicios de sesión para todos los usuarios en un período determinado.</span><span class="sxs-lookup"><span data-stu-id="87fd8-174">The user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="87fd8-175">El valor predeterminado para el período es 30 días.</span><span class="sxs-lookup"><span data-stu-id="87fd8-175">The default for the time period is 30 days.</span></span>

<span data-ttu-id="87fd8-176">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/46.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="87fd8-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="87fd8-177">Al hacer clic en un día en el gráfico de inicio de sesión, obtiene una lista detallada de las actividades de inicio de sesión de ese día.</span><span class="sxs-lookup"><span data-stu-id="87fd8-177">When you click on a day in the sign-in graph, you get a detailed list of the sign-in activities for this day.</span></span>

<span data-ttu-id="87fd8-178">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/41.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="87fd8-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="87fd8-179">Cada fila de la lista de actividades de inicio de sesión le ofrece la información detallada acerca del inicio de sesión seleccionado como:</span><span class="sxs-lookup"><span data-stu-id="87fd8-179">Each row in the sign-in activities list gives you the detailed information about the selected sign-in such as:</span></span>

* <span data-ttu-id="87fd8-180">¿Quién ha iniciado sesión?</span><span class="sxs-lookup"><span data-stu-id="87fd8-180">Who has signed in?</span></span>
* <span data-ttu-id="87fd8-181">¿Cuál era el UPN relacionado?</span><span class="sxs-lookup"><span data-stu-id="87fd8-181">What was the related UPN?</span></span>
* <span data-ttu-id="87fd8-182">¿Qué aplicación era el destino del inicio de sesión?</span><span class="sxs-lookup"><span data-stu-id="87fd8-182">What application was the target of the sign-in?</span></span>
* <span data-ttu-id="87fd8-183">¿Cuál es la dirección IP del inicio de sesión?</span><span class="sxs-lookup"><span data-stu-id="87fd8-183">What is the IP address of the sign-in?</span></span>
* <span data-ttu-id="87fd8-184">¿Cuál es el estado del inicio de sesión?</span><span class="sxs-lookup"><span data-stu-id="87fd8-184">What was the status of the sign-in?</span></span>

<span data-ttu-id="87fd8-185">La opción **Inicios de sesión** ofrece información general completa sobre todos los inicios de sesión de usuarios.</span><span class="sxs-lookup"><span data-stu-id="87fd8-185">The **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="87fd8-186">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/51.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="87fd8-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="87fd8-187">Uso de las aplicaciones administradas</span><span class="sxs-lookup"><span data-stu-id="87fd8-187">Usage of managed applications</span></span>

<span data-ttu-id="87fd8-188">Con una vista centrada en la aplicación de los datos de inicio de sesión, puede responder a preguntas tales como:</span><span class="sxs-lookup"><span data-stu-id="87fd8-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="87fd8-189">¿Quién está usando mis aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="87fd8-189">Who is using my applications?</span></span>
* <span data-ttu-id="87fd8-190">¿Cuáles son las tres aplicaciones principales en su organización?</span><span class="sxs-lookup"><span data-stu-id="87fd8-190">What are the top 3 applications in your organization?</span></span>
* <span data-ttu-id="87fd8-191">Recientemente he implementado una aplicación.</span><span class="sxs-lookup"><span data-stu-id="87fd8-191">I have recently rolled out an application.</span></span> <span data-ttu-id="87fd8-192">¿Cómo sigue?</span><span class="sxs-lookup"><span data-stu-id="87fd8-192">How is it doing?</span></span>

<span data-ttu-id="87fd8-193">El punto de entrada a los datos son las tres aplicaciones principales de su organización en el informe de los últimos 30 días en la sección **Introducción** en **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="87fd8-193">Your entry point to this data is the top 3 applications in your organization within the last 30 days report in the **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="87fd8-194">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/64.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="87fd8-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="87fd8-195">Agregaciones semanales del gráfico de uso de la aplicación de inicios de sesión para las tres aplicaciones principales en un período determinado.</span><span class="sxs-lookup"><span data-stu-id="87fd8-195">The app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="87fd8-196">El valor predeterminado para el período es 30 días.</span><span class="sxs-lookup"><span data-stu-id="87fd8-196">The default for the time period is 30 days.</span></span>

<span data-ttu-id="87fd8-197">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/47.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="87fd8-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="87fd8-198">Si lo desea, puede establecer el foco en una aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="87fd8-198">If you want to, you can set the focus on a specific application.</span></span>


<span data-ttu-id="87fd8-199">![Informes](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Informes")</span><span class="sxs-lookup"><span data-stu-id="87fd8-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="87fd8-200">Al hacer clic en un día del gráfico de uso de la aplicación, obtendrá una lista detallada de las actividades de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="87fd8-200">When you click on a day in the app usage graph, you get a detailed list of the sign-in activities.</span></span>


<span data-ttu-id="87fd8-201">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/48.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="87fd8-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="87fd8-202">La opción **Inicios de sesión** ofrece una descripción completa de todos los eventos de inicio de sesión para sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="87fd8-202">The **Sign-ins** option gives you a complete overview of all sign-in events to your applications.</span></span>

<span data-ttu-id="87fd8-203">![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/49.png "Actividad de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="87fd8-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="87fd8-204">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="87fd8-204">Next steps</span></span>

<span data-ttu-id="87fd8-205">Si desea obtener más información acerca de los códigos de error de las actividades de inicio de sesión, consulte [Códigos de error de informes de actividad de inicio de sesión en el portal de Azure Active Directory](active-directory-reporting-activity-sign-ins-errors.md).</span><span class="sxs-lookup"><span data-stu-id="87fd8-205">If you want to know more about sign-in activity error codes, see the [Sign-in activity report error codes in the Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

