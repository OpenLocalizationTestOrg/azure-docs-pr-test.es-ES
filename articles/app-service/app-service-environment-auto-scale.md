---
title: aaaAutoscaling y v1 de entorno del servicio de aplicaciones
description: "Escalado automático y entorno del Servicio de aplicaciones"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 1a03cf494309e80596b64471d1a067b2f64a9fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a><span data-ttu-id="fa081-103">Escalado automático y App Service Environment v1</span><span class="sxs-lookup"><span data-stu-id="fa081-103">Autoscaling and App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="fa081-104">Este artículo trata sobre Hola v1 de entorno del servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fa081-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="fa081-105">Hay una versión más reciente de hello entorno del servicio de aplicación que es más fácil toouse y se ejecuta en una infraestructura más eficaz.</span><span class="sxs-lookup"><span data-stu-id="fa081-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="fa081-106">toolearn más información acerca de la nueva versión de hello iniciar con hello [toohello Introducción entono](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="fa081-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

<span data-ttu-id="fa081-107">Los entornos del Servicio de aplicaciones de Azure admiten el *escalado automático*.</span><span class="sxs-lookup"><span data-stu-id="fa081-107">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="fa081-108">Puede usar el escalado automático basado en métricas o programación grupos de trabajo individuales.</span><span class="sxs-lookup"><span data-stu-id="fa081-108">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![Opciones de escalado automático para un grupo de trabajo.][intro]

<span data-ttu-id="fa081-110">Ajuste automático optimiza el uso de recursos automáticamente aumentar y reducir un toofit de entorno de servicio de aplicaciones su perfil de presupuesto y carga.</span><span class="sxs-lookup"><span data-stu-id="fa081-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment toofit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="fa081-111">Configuración del escalado automático de grupo de trabajo</span><span class="sxs-lookup"><span data-stu-id="fa081-111">Configure worker pool autoscale</span></span>
<span data-ttu-id="fa081-112">Puede tener acceso a funcionalidad de escalado automático de Hola de hello **configuración** ficha de grupo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa081-112">You can access hello autoscale functionality from hello **Settings** tab of hello worker pool.</span></span>

![Pestaña Configuración de grupo de trabajo de Hola.][settings-scale]

<span data-ttu-id="fa081-114">Desde allí, Hola interfaz debe ser bastante conocido porque es Hola planear la misma experiencia que verá al escalar un servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fa081-114">From there, hello interface should be fairly familiar since it is hello same experience that you see when you scale an App Service plan.</span></span> 

![Configuración de la escala manual.][scale-manual]

<span data-ttu-id="fa081-116">También puede configurar un perfil de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="fa081-116">You can also configure an autoscale profile.</span></span>

![Configuración del escalado automático.][scale-profile]

<span data-ttu-id="fa081-118">Perfiles de escalado automático son límites de tooset útil sobre la escala.</span><span class="sxs-lookup"><span data-stu-id="fa081-118">Autoscale profiles are useful tooset limits on your scale.</span></span> <span data-ttu-id="fa081-119">De este modo tener una experiencia de rendimiento coherente, mediante el establecimiento de un valor de escala de límite inferior (1) y un techo de gasto predecible, mediante el establecimiento de un límite superior (2).</span><span class="sxs-lookup"><span data-stu-id="fa081-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![Configuración de la escala en el perfil.][scale-profile2]

<span data-ttu-id="fa081-121">Después de definir un perfil, puede agregar tooscale de reglas de escalado automático hacia arriba o hacia abajo, número de Hola de instancias de grupo de trabajo de hello dentro de los límites de hello definidas por el perfil de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa081-121">After you define a profile, you can add autoscale rules tooscale up or down hello number of instances in hello worker pool within hello bounds defined by hello profile.</span></span> <span data-ttu-id="fa081-122">Las reglas de escalado automático se basan en las métricas.</span><span class="sxs-lookup"><span data-stu-id="fa081-122">Autoscale rules are based on metrics.</span></span>

![Regla de escala.][scale-rule]

 <span data-ttu-id="fa081-124">Cualquier grupo de trabajo o las métricas de front-end pueden ser toodefine usa reglas de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="fa081-124">Any worker pool or front-end metrics can be used toodefine autoscale rules.</span></span> <span data-ttu-id="fa081-125">Estas métricas son Hola mismas métricas puede supervisar en los gráficos de hoja de recursos de Hola o establecer alertas para.</span><span class="sxs-lookup"><span data-stu-id="fa081-125">These metrics are hello same metrics you can monitor in hello resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="fa081-126">Ejemplo de escalado automático</span><span class="sxs-lookup"><span data-stu-id="fa081-126">Autoscale example</span></span>
<span data-ttu-id="fa081-127">La mejor manera de ilustrar el escalado automático de un entorno del Servicio de aplicaciones es mediante un escenario.</span><span class="sxs-lookup"><span data-stu-id="fa081-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="fa081-128">Este artículo explica todas las consideraciones de hello necesarios al configurar escalado automático.</span><span class="sxs-lookup"><span data-stu-id="fa081-128">This article explains all hello necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="fa081-129">Hola artículo le guiará a través de hello las interacciones que surte reproducción al factor de escala automática entornos de servicio de aplicaciones que se hospedan en el entorno del servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fa081-129">hello article walks you through hello interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="fa081-130">Introducción al escenario</span><span class="sxs-lookup"><span data-stu-id="fa081-130">Scenario introduction</span></span>
<span data-ttu-id="fa081-131">Frank es un administrador del sistema para una empresa que ha migrado una parte de las cargas de trabajo de Hola que administra tooan entorno de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fa081-131">Frank is a sysadmin for an enterprise who has migrated a portion of hello workloads that he manages tooan App Service environment.</span></span>

<span data-ttu-id="fa081-132">Hello es el entorno de servicio de aplicaciones Configurar escala toomanual como sigue:</span><span class="sxs-lookup"><span data-stu-id="fa081-132">hello App Service environment is configured toomanual scale as follows:</span></span>

* <span data-ttu-id="fa081-133">**Servidores front-end** : 3</span><span class="sxs-lookup"><span data-stu-id="fa081-133">**Front ends:** 3</span></span>
* <span data-ttu-id="fa081-134">**Grupo de trabajo 1**: 10</span><span class="sxs-lookup"><span data-stu-id="fa081-134">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="fa081-135">**Grupo de trabajo 2**: 5</span><span class="sxs-lookup"><span data-stu-id="fa081-135">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="fa081-136">**Grupo de trabajo 3**: 5</span><span class="sxs-lookup"><span data-stu-id="fa081-136">**Worker pool 3**: 5</span></span>

<span data-ttu-id="fa081-137">El grupo de trabajo 1 se usa para las cargas de trabajo de producción, en tanto que los grupos de trabajo 2 y 3 se usan para las cargas de trabajo de control de calidad y desarrollo.</span><span class="sxs-lookup"><span data-stu-id="fa081-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="fa081-138">Hello aplicación planes de servicio para preguntas y respuestas y desarrollo están configurados toomanual escala.</span><span class="sxs-lookup"><span data-stu-id="fa081-138">hello App Service plans for QA and dev are configured toomanual scale.</span></span> <span data-ttu-id="fa081-139">producción de Hello plan de servicio de aplicaciones se establece tooautoscale toodeal con variaciones en la carga y el tráfico.</span><span class="sxs-lookup"><span data-stu-id="fa081-139">hello production App Service plan is set tooautoscale toodeal with variations in load and traffic.</span></span>

<span data-ttu-id="fa081-140">Frank está muy familiarizado con la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="fa081-140">Frank is very familiar with hello application.</span></span> <span data-ttu-id="fa081-141">Sabe que las horas punta Hola de carga son entre las 9:00 A.M. y 6:00 P.M. porque se trata de una aplicación de línea de negocio (LOB) que los empleados usan mientras están en office Hola.</span><span class="sxs-lookup"><span data-stu-id="fa081-141">He knows that hello peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in hello office.</span></span> <span data-ttu-id="fa081-142">El uso cae después, una vez que los usuarios han terminado la jornada.</span><span class="sxs-lookup"><span data-stu-id="fa081-142">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="fa081-143">Fuera de horas punta, hay cierta carga porque los usuarios pueden acceder de forma remota aplicación hello mediante sus dispositivos móviles o equipos domésticos.</span><span class="sxs-lookup"><span data-stu-id="fa081-143">Outside peak hours, there is still some load because users can access hello app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="fa081-144">producción de Hello plan de servicio de aplicaciones ya está configurado tooautoscale según el uso de CPU con hello siguientes reglas:</span><span class="sxs-lookup"><span data-stu-id="fa081-144">hello production App Service plan is already configured tooautoscale based on CPU usage with hello following rules:</span></span>

![Configuración específica para las aplicaciones LOB.][asp-scale]

| <span data-ttu-id="fa081-146">**Perfil de escalado automático: Días laborables: plan del Servicio de aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="fa081-146">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="fa081-147">**Perfil de escalado automático: Fines de semana: plan del Servicio de aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="fa081-147">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="fa081-148">**Nombre:** perfil Día laborable</span><span class="sxs-lookup"><span data-stu-id="fa081-148">**Name:** Weekday profile</span></span> |<span data-ttu-id="fa081-149">**Nombre:** perfil Fin de semana</span><span class="sxs-lookup"><span data-stu-id="fa081-149">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="fa081-150">**Escalar por:** Reglas de rendimiento y programación</span><span class="sxs-lookup"><span data-stu-id="fa081-150">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="fa081-151">**Escalar por:** Reglas de rendimiento y programación</span><span class="sxs-lookup"><span data-stu-id="fa081-151">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="fa081-152">**Perfil:** Días laborables</span><span class="sxs-lookup"><span data-stu-id="fa081-152">**Profile:** Weekdays</span></span> |<span data-ttu-id="fa081-153">**Perfil:** Fin de semana</span><span class="sxs-lookup"><span data-stu-id="fa081-153">**Profile:** Weekend</span></span> |
| <span data-ttu-id="fa081-154">**Tipo:** periodicidad</span><span class="sxs-lookup"><span data-stu-id="fa081-154">**Type:** Recurrence</span></span> |<span data-ttu-id="fa081-155">**Tipo:** periodicidad</span><span class="sxs-lookup"><span data-stu-id="fa081-155">**Type:** Recurrence</span></span> |
| <span data-ttu-id="fa081-156">**Intervalo de destino:** 5 instancias too20</span><span class="sxs-lookup"><span data-stu-id="fa081-156">**Target range:** 5 too20 instances</span></span> |<span data-ttu-id="fa081-157">**Intervalo de destino:** 3 instancias too10</span><span class="sxs-lookup"><span data-stu-id="fa081-157">**Target range:** 3 too10 instances</span></span> |
| <span data-ttu-id="fa081-158">**Días:** lunes, martes, miércoles, jueves, viernes</span><span class="sxs-lookup"><span data-stu-id="fa081-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="fa081-159">**Días:** sábado, domingo</span><span class="sxs-lookup"><span data-stu-id="fa081-159">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="fa081-160">**Hora de inicio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="fa081-160">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="fa081-161">**Hora de inicio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="fa081-161">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="fa081-162">**Zona horaria:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="fa081-162">**Time zone:** UTC-08</span></span> |<span data-ttu-id="fa081-163">**Zona horaria:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="fa081-163">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="fa081-164">**Regla de escalado automático (escalar verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="fa081-164">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="fa081-165">**Regla de escalado automático (escalar verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="fa081-165">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="fa081-166">**Recurso:** Producción (entorno del Servicio de aplicaciones)</span><span class="sxs-lookup"><span data-stu-id="fa081-166">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="fa081-167">**Recurso:** Producción (entorno del Servicio de aplicaciones)</span><span class="sxs-lookup"><span data-stu-id="fa081-167">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="fa081-168">**Métrica:** % de CPU</span><span class="sxs-lookup"><span data-stu-id="fa081-168">**Metric:** CPU %</span></span> |<span data-ttu-id="fa081-169">**Métrica:** % de CPU</span><span class="sxs-lookup"><span data-stu-id="fa081-169">**Metric:** CPU %</span></span> |
| <span data-ttu-id="fa081-170">**Operación:** Mayor que 60%</span><span class="sxs-lookup"><span data-stu-id="fa081-170">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="fa081-171">**Operación:** Mayor que 80%</span><span class="sxs-lookup"><span data-stu-id="fa081-171">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="fa081-172">**Duración:** 5 minutos</span><span class="sxs-lookup"><span data-stu-id="fa081-172">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="fa081-173">**Duración:** 10 minutos</span><span class="sxs-lookup"><span data-stu-id="fa081-173">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="fa081-174">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="fa081-174">**Time aggregation:** Average</span></span> |<span data-ttu-id="fa081-175">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="fa081-175">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="fa081-176">**Acción:** Aumentar recuento en 2</span><span class="sxs-lookup"><span data-stu-id="fa081-176">**Action:** Increase count by 2</span></span> |<span data-ttu-id="fa081-177">**Acción:** Aumentar recuento en 1</span><span class="sxs-lookup"><span data-stu-id="fa081-177">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="fa081-178">**Tiempo de finalización (minutos):** 15</span><span class="sxs-lookup"><span data-stu-id="fa081-178">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="fa081-179">**Tiempo de finalización (minutos):** 20</span><span class="sxs-lookup"><span data-stu-id="fa081-179">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="fa081-180">**Regla de escalado automático (reducir verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="fa081-180">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="fa081-181">**Regla de escalado automático (reducir verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="fa081-181">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="fa081-182">**Recurso:** Producción (entorno del Servicio de aplicaciones)</span><span class="sxs-lookup"><span data-stu-id="fa081-182">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="fa081-183">**Recurso:** Producción (entorno del Servicio de aplicaciones)</span><span class="sxs-lookup"><span data-stu-id="fa081-183">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="fa081-184">**Métrica:** % de CPU</span><span class="sxs-lookup"><span data-stu-id="fa081-184">**Metric:** CPU %</span></span> |<span data-ttu-id="fa081-185">**Métrica:** % de CPU</span><span class="sxs-lookup"><span data-stu-id="fa081-185">**Metric:** CPU %</span></span> |
| <span data-ttu-id="fa081-186">**Operación:** menor que el 30 %</span><span class="sxs-lookup"><span data-stu-id="fa081-186">**Operation:** Less than 30%</span></span> |<span data-ttu-id="fa081-187">**Operación:** menor que el 20 %</span><span class="sxs-lookup"><span data-stu-id="fa081-187">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="fa081-188">**Duración:** 10 minutos</span><span class="sxs-lookup"><span data-stu-id="fa081-188">**Duration:** 10 minutes</span></span> |<span data-ttu-id="fa081-189">**Duración:** 15 minutos</span><span class="sxs-lookup"><span data-stu-id="fa081-189">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="fa081-190">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="fa081-190">**Time aggregation:** Average</span></span> |<span data-ttu-id="fa081-191">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="fa081-191">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="fa081-192">**Acción:** Reducir recuento en 1</span><span class="sxs-lookup"><span data-stu-id="fa081-192">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="fa081-193">**Acción:** Reducir recuento en 1</span><span class="sxs-lookup"><span data-stu-id="fa081-193">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="fa081-194">**Tiempo de finalización (minutos):** 20</span><span class="sxs-lookup"><span data-stu-id="fa081-194">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="fa081-195">**Tiempo de finalización (minutos):** 10</span><span class="sxs-lookup"><span data-stu-id="fa081-195">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="fa081-196">Tasa de inflación del plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="fa081-196">App Service plan inflation rate</span></span>
<span data-ttu-id="fa081-197">Planes de servicio de aplicaciones que están configurado tooautoscale hacerlo a una velocidad máxima por hora.</span><span class="sxs-lookup"><span data-stu-id="fa081-197">App Service plans that are configured tooautoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="fa081-198">Esta velocidad se calculen según en valores de hello proporcionados en la regla de escalado automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa081-198">This rate can be calculated based on hello values provided on hello autoscale rule.</span></span>

<span data-ttu-id="fa081-199">Descripción y calcular Hola *tasa de inflación del plan de servicio de aplicaciones* es importante para el escalado automático de entorno de servicio de aplicaciones porque el grupo de trabajo de tooa de cambios de escala no son instantáneos.</span><span class="sxs-lookup"><span data-stu-id="fa081-199">Understanding and calculating hello *App Service plan inflation rate* is important for App Service environment autoscale because scale changes tooa worker pool are not instantaneous.</span></span>

<span data-ttu-id="fa081-200">Hola tasa de inflación del plan de servicio de aplicaciones se calcula como sigue:</span><span class="sxs-lookup"><span data-stu-id="fa081-200">hello App Service plan inflation rate is calculated as follows:</span></span>

![Cálculo de la tasa de inflación del plan del Servicio de aplicaciones.][ASP-Inflation]

<span data-ttu-id="fa081-202">En función de hello escalado automático: regla escalar vertical para el perfil de día de la semana de Hola de producción de hello plan de servicio de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="fa081-202">Based on hello Autoscale – Scale Up rule for hello Weekday profile of hello production App Service plan:</span></span>

![Tasa de inflación del plan del Servicio de aplicaciones para los días laborables basándose en el escalado automático: regla escalar verticalmente.][Equation1]

<span data-ttu-id="fa081-204">En caso de hello de hello escalado automático: escalar vertical de la regla para el perfil de fin de semana de Hola de producción de hello plan de servicio de aplicaciones, la fórmula de Hola se resolverá en:</span><span class="sxs-lookup"><span data-stu-id="fa081-204">In hello case of hello Autoscale – Scale Up rule for hello Weekend profile of hello production App Service plan, hello formula would resolve to:</span></span>

![Tasa de inflación del plan del Servicio de aplicaciones para los fines de semana basado en el escalado automático: regla escalar verticalmente.][Equation2]

<span data-ttu-id="fa081-206">Este valor también se puede calcular para operaciones de reducción vertical.</span><span class="sxs-lookup"><span data-stu-id="fa081-206">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="fa081-207">En función de hello escalado automático: regla de escala hacia abajo para el perfil de día de la semana de Hola de producción de hello plan de servicio de aplicaciones, esto sería similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="fa081-207">Based on hello Autoscale – Scale Down rule for hello Weekday profile of hello production App Service plan, this would look as follows:</span></span>

![Tasa de inflación del plan del Servicio de aplicaciones para los días laborables basándose en el escalado automático: regla reducir verticalmente.][Equation3]

<span data-ttu-id="fa081-209">En caso de hello de hello escalado automático: regla de escala hacia abajo para el perfil de fin de semana de Hola de producción de hello plan de servicio de aplicaciones, la fórmula de Hola se resolverá en:</span><span class="sxs-lookup"><span data-stu-id="fa081-209">In hello case of hello Autoscale – Scale Down rule for hello Weekend profile of hello production App Service plan, hello formula would resolve to:</span></span>  

![Tasa de inflación del plan del Servicio de aplicaciones para los fines de semana basado en el escalado automático: regla reducir verticalmente.][Equation4]

<span data-ttu-id="fa081-211">producción de Hello plan de servicio de aplicaciones puede crecer en una velocidad máxima de ocho instancias por hora durante la semana de Hola y cuatro instancias por hora durante un fin de semana Hola.</span><span class="sxs-lookup"><span data-stu-id="fa081-211">hello production App Service plan can grow at a maximum rate of eight instances/hour during hello week and four instances/hour during hello weekend.</span></span> <span data-ttu-id="fa081-212">Puede liberar instancias a una velocidad máxima de cuatro instancias por hora durante la semana de Hola y seis instancias por hora durante los fines de semana.</span><span class="sxs-lookup"><span data-stu-id="fa081-212">It can release instances at a maximum rate of four instances/hour during hello week and six instances/hour during weekends.</span></span>

<span data-ttu-id="fa081-213">Si varios planes de servicio de aplicaciones se hospedan en un grupo de trabajo, tendrá que hello toocalculate *total tasa de inflación* como suma Hola de tasa de inflación de Hola para hello todos los planes de servicio de aplicaciones que se va a hospedar en ese grupo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="fa081-213">If multiple App Service plans are being hosted in a worker pool, you have toocalculate hello *total inflation rate* as hello sum of hello inflation rate for all hello App Service plans that are being hosting in that worker pool.</span></span>

![Cálculo de la tasa de inflación total para varios planes del Servicio de aplicaciones hospedados en un grupo de trabajo.][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a><span data-ttu-id="fa081-215">Hola servicio de aplicaciones de uso previsto reglas de escalado automático de grupo de trabajo de tasa de inflación toodefine</span><span class="sxs-lookup"><span data-stu-id="fa081-215">Use hello App Service plan inflation rate toodefine worker pool autoscale rules</span></span>
<span data-ttu-id="fa081-216">Los grupos de trabajo que hospedan los planes de servicio de aplicaciones que están configurado tooautoscale deben asignarse a un búfer de la capacidad.</span><span class="sxs-lookup"><span data-stu-id="fa081-216">Worker pools that host App Service plans that are configured tooautoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="fa081-217">búfer de Hello permite toogrow de operaciones de escalado automático de Hola y reducir el plan de servicio de aplicaciones, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fa081-217">hello buffer allows for hello autoscale operations toogrow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="fa081-218">mínimo de búfer de Hello sería Hola calcula la tasa de inflación Total de Plan de servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="fa081-218">hello minimum buffer would be hello calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="fa081-219">Dado que las operaciones de escalado del entorno de servicio de aplicaciones tienen algún tooapply tiempo, cualquier cambio tenga en cuenta más cambios en la demanda que pudieron ocurrir mientras está en curso una operación de escala.</span><span class="sxs-lookup"><span data-stu-id="fa081-219">Because App Service environment scale operations take some time tooapply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="fa081-220">tooaccommodate esta latencia, se recomienda que use Hola calcula la tasa de inflación Total de Plan de servicio de aplicación como el número mínimo de Hola de instancias que se agregan para cada operación de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="fa081-220">tooaccommodate this latency, we recommend that you use hello calculated Total App Service Plan Inflation Rate as hello minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="fa081-221">Con esta información, puede definir los Frank Hola siguiendo perfil de escalado automático y reglas:</span><span class="sxs-lookup"><span data-stu-id="fa081-221">With this information, Frank can define hello following autoscale profile and rules:</span></span>

![Ejemplo de reglas de perfil de escalado automático para línea de negocio.][Worker-Pool-Scale]

| <span data-ttu-id="fa081-223">**Perfil de escalado automático: Días laborables**</span><span class="sxs-lookup"><span data-stu-id="fa081-223">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="fa081-224">**Perfil de escalado automático: Fines de semana**</span><span class="sxs-lookup"><span data-stu-id="fa081-224">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="fa081-225">**Nombre:** perfil Día laborable</span><span class="sxs-lookup"><span data-stu-id="fa081-225">**Name:** Weekday profile</span></span> |<span data-ttu-id="fa081-226">**Nombre:** perfil Fin de semana</span><span class="sxs-lookup"><span data-stu-id="fa081-226">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="fa081-227">**Escalar por:** Reglas de rendimiento y programación</span><span class="sxs-lookup"><span data-stu-id="fa081-227">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="fa081-228">**Escalar por:** Reglas de rendimiento y programación</span><span class="sxs-lookup"><span data-stu-id="fa081-228">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="fa081-229">**Perfil:** Días laborables</span><span class="sxs-lookup"><span data-stu-id="fa081-229">**Profile:** Weekdays</span></span> |<span data-ttu-id="fa081-230">**Perfil:** Fin de semana</span><span class="sxs-lookup"><span data-stu-id="fa081-230">**Profile:** Weekend</span></span> |
| <span data-ttu-id="fa081-231">**Tipo:** periodicidad</span><span class="sxs-lookup"><span data-stu-id="fa081-231">**Type:** Recurrence</span></span> |<span data-ttu-id="fa081-232">**Tipo:** periodicidad</span><span class="sxs-lookup"><span data-stu-id="fa081-232">**Type:** Recurrence</span></span> |
| <span data-ttu-id="fa081-233">**Intervalo de destino:** 13 instancias too25</span><span class="sxs-lookup"><span data-stu-id="fa081-233">**Target range:** 13 too25 instances</span></span> |<span data-ttu-id="fa081-234">**Intervalo de destino:** 6 instancias too15</span><span class="sxs-lookup"><span data-stu-id="fa081-234">**Target range:** 6 too15 instances</span></span> |
| <span data-ttu-id="fa081-235">**Días:** lunes, martes, miércoles, jueves, viernes</span><span class="sxs-lookup"><span data-stu-id="fa081-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="fa081-236">**Días:** sábado, domingo</span><span class="sxs-lookup"><span data-stu-id="fa081-236">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="fa081-237">**Hora de inicio:** 7:00</span><span class="sxs-lookup"><span data-stu-id="fa081-237">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="fa081-238">**Hora de inicio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="fa081-238">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="fa081-239">**Zona horaria:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="fa081-239">**Time zone:** UTC-08</span></span> |<span data-ttu-id="fa081-240">**Zona horaria:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="fa081-240">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="fa081-241">**Regla de escalado automático (escalar verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="fa081-241">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="fa081-242">**Regla de escalado automático (escalar verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="fa081-242">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="fa081-243">**Recurso:** Grupo de trabajo 1</span><span class="sxs-lookup"><span data-stu-id="fa081-243">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="fa081-244">**Recurso:** Grupo de trabajo 1</span><span class="sxs-lookup"><span data-stu-id="fa081-244">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="fa081-245">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="fa081-245">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="fa081-246">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="fa081-246">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="fa081-247">**Operación:** Menor que 8</span><span class="sxs-lookup"><span data-stu-id="fa081-247">**Operation:** Less than 8</span></span> |<span data-ttu-id="fa081-248">**Operación:** Menor que 3</span><span class="sxs-lookup"><span data-stu-id="fa081-248">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="fa081-249">**Duración:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="fa081-249">**Duration:** 20 minutes</span></span> |<span data-ttu-id="fa081-250">**Duración:** 30 minutos</span><span class="sxs-lookup"><span data-stu-id="fa081-250">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="fa081-251">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="fa081-251">**Time aggregation:** Average</span></span> |<span data-ttu-id="fa081-252">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="fa081-252">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="fa081-253">**Acción:** Aumentar recuento en 8</span><span class="sxs-lookup"><span data-stu-id="fa081-253">**Action:** Increase count by 8</span></span> |<span data-ttu-id="fa081-254">**Acción:** Aumentar recuento en 3</span><span class="sxs-lookup"><span data-stu-id="fa081-254">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="fa081-255">**Tiempo de finalización (minutos):** 180</span><span class="sxs-lookup"><span data-stu-id="fa081-255">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="fa081-256">**Tiempo de finalización (minutos):** 180</span><span class="sxs-lookup"><span data-stu-id="fa081-256">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="fa081-257">**Regla de escalado automático (reducir verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="fa081-257">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="fa081-258">**Regla de escalado automático (reducir verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="fa081-258">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="fa081-259">**Recurso:** Grupo de trabajo 1</span><span class="sxs-lookup"><span data-stu-id="fa081-259">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="fa081-260">**Recurso:** Grupo de trabajo 1</span><span class="sxs-lookup"><span data-stu-id="fa081-260">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="fa081-261">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="fa081-261">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="fa081-262">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="fa081-262">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="fa081-263">**Operación:** Mayor que 8</span><span class="sxs-lookup"><span data-stu-id="fa081-263">**Operation:** Greater than 8</span></span> |<span data-ttu-id="fa081-264">**Operación:** Mayor que 3 %</span><span class="sxs-lookup"><span data-stu-id="fa081-264">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="fa081-265">**Duración:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="fa081-265">**Duration:** 20 minutes</span></span> |<span data-ttu-id="fa081-266">**Duración:** 15 minutos</span><span class="sxs-lookup"><span data-stu-id="fa081-266">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="fa081-267">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="fa081-267">**Time aggregation:** Average</span></span> |<span data-ttu-id="fa081-268">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="fa081-268">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="fa081-269">**Acción:** Reducir recuento en 2</span><span class="sxs-lookup"><span data-stu-id="fa081-269">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="fa081-270">**Acción:** Reducir recuento en 3</span><span class="sxs-lookup"><span data-stu-id="fa081-270">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="fa081-271">**Tiempo de finalización (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="fa081-271">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="fa081-272">**Tiempo de finalización (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="fa081-272">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="fa081-273">intervalo de destino definido en el perfil de Hola Hola se calcula instancias mínimo Hola definidas en el perfil para el plan de servicio de aplicación hello + búfer.</span><span class="sxs-lookup"><span data-stu-id="fa081-273">hello Target range defined in hello profile is calculated by hello minimum instances defined in the profile for hello App Service plan + buffer.</span></span>

<span data-ttu-id="fa081-274">intervalo máximo de Hello sería la suma de Hola de todos los intervalos máximo de Hola para todos los planes de servicio de aplicaciones que se hospeda en el grupo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa081-274">hello Maximum range would be hello sum of all hello maximum ranges for all App Service plans hosted in hello worker pool.</span></span>

<span data-ttu-id="fa081-275">Hola recuento de aumento para escalar Hola reglas debe ser tooat conjunto mínimo de 1 X la tasa de inflación de Plan de servicio de aplicación de escala de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fa081-275">hello Increase count for hello scale up rules should be set tooat least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="fa081-276">Recuento de disminución puede ser ajustado toosomething entre 1/2 X o 1 X Hola tasa de inflación de Plan de servicio de aplicación de escala hacia abajo.</span><span class="sxs-lookup"><span data-stu-id="fa081-276">Decrease count can be adjusted toosomething between 1/2X or 1X hello App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="fa081-277">Escalado automático para un grupo de servidores front-end</span><span class="sxs-lookup"><span data-stu-id="fa081-277">Autoscale for front-end pool</span></span>
<span data-ttu-id="fa081-278">Las reglas de escalado automático de front-end son más sencillas que las de los grupos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="fa081-278">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="fa081-279">En primer lugar, debe</span><span class="sxs-lookup"><span data-stu-id="fa081-279">Primarily, you should</span></span>  
<span data-ttu-id="fa081-280">Asegúrese de que la duración de medición de Hola y temporizadores de enfriamiento Hola, tenga en cuenta que las operaciones de escala en un plan de servicio de aplicaciones no son instantáneas.</span><span class="sxs-lookup"><span data-stu-id="fa081-280">make sure that duration of hello measurement and hello cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="fa081-281">En este escenario, Frank sabe esa tasa de errores de hello aumenta después de utilización de CPU del 80% de llegar a servidores front-end y establece escalado automático de hello en instancias de tooincrease de reglas como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="fa081-281">For this scenario, Frank knows that hello error rate increases after front ends reach 80% CPU utilization and sets hello autoscale rule tooincrease instances as follows:</span></span>

![Configuración del escalado automático para un grupo de servidores front-end.][Front-End-Scale]

| <span data-ttu-id="fa081-283">**Perfil de escalado automático: Servidores front-end**</span><span class="sxs-lookup"><span data-stu-id="fa081-283">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="fa081-284">**Nombre:** Escalado automático: Servidores front-end</span><span class="sxs-lookup"><span data-stu-id="fa081-284">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="fa081-285">**Escalar por:** Reglas de rendimiento y programación</span><span class="sxs-lookup"><span data-stu-id="fa081-285">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="fa081-286">**Perfil:** Todos los días</span><span class="sxs-lookup"><span data-stu-id="fa081-286">**Profile:** Everyday</span></span> |
| <span data-ttu-id="fa081-287">**Tipo:** periodicidad</span><span class="sxs-lookup"><span data-stu-id="fa081-287">**Type:** Recurrence</span></span> |
| <span data-ttu-id="fa081-288">**Intervalo de destino:** 3 instancias too10</span><span class="sxs-lookup"><span data-stu-id="fa081-288">**Target range:** 3 too10 instances</span></span> |
| <span data-ttu-id="fa081-289">**Días:** Todos los días</span><span class="sxs-lookup"><span data-stu-id="fa081-289">**Days:** Everyday</span></span> |
| <span data-ttu-id="fa081-290">**Hora de inicio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="fa081-290">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="fa081-291">**Zona horaria:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="fa081-291">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="fa081-292">**Regla de escalado automático (escalar verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="fa081-292">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="fa081-293">**Recurso:** Grupo de servidores front-end</span><span class="sxs-lookup"><span data-stu-id="fa081-293">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="fa081-294">**Métrica:** % de CPU</span><span class="sxs-lookup"><span data-stu-id="fa081-294">**Metric:** CPU %</span></span> |
| <span data-ttu-id="fa081-295">**Operación:** Mayor que 60%</span><span class="sxs-lookup"><span data-stu-id="fa081-295">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="fa081-296">**Duración:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="fa081-296">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="fa081-297">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="fa081-297">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="fa081-298">**Acción:** Aumentar recuento en 3</span><span class="sxs-lookup"><span data-stu-id="fa081-298">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="fa081-299">**Tiempo de finalización (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="fa081-299">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="fa081-300">**Regla de escalado automático (reducir verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="fa081-300">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="fa081-301">**Recurso:** Grupo de trabajo 1</span><span class="sxs-lookup"><span data-stu-id="fa081-301">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="fa081-302">**Métrica:** % de CPU</span><span class="sxs-lookup"><span data-stu-id="fa081-302">**Metric:** CPU %</span></span> |
| <span data-ttu-id="fa081-303">**Operación:** menor que el 30 %</span><span class="sxs-lookup"><span data-stu-id="fa081-303">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="fa081-304">**Duración:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="fa081-304">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="fa081-305">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="fa081-305">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="fa081-306">**Acción:** Reducir recuento en 3</span><span class="sxs-lookup"><span data-stu-id="fa081-306">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="fa081-307">**Tiempo de finalización (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="fa081-307">**Cool down (minutes):** 120</span></span> |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
