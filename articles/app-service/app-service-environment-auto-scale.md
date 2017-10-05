---
title: "Escalado automático y App Service Environment v1"
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
ms.openlocfilehash: f32affd285f3918feb0e893543f2a28f678b7b10
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a><span data-ttu-id="01cc3-103">Escalado automático y App Service Environment v1</span><span class="sxs-lookup"><span data-stu-id="01cc3-103">Autoscaling and App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="01cc3-104">Este artículo trata sobre App Service Environment v1.</span><span class="sxs-lookup"><span data-stu-id="01cc3-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="01cc3-105">Hay una versión más reciente de App Service Environment que resulta más fácil de usar y se ejecuta en una infraestructura más eficaz.</span><span class="sxs-lookup"><span data-stu-id="01cc3-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="01cc3-106">Para aprender más sobre la nueva versión, consulte [Introducción a App Service Environment](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="01cc3-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

<span data-ttu-id="01cc3-107">Los entornos del Servicio de aplicaciones de Azure admiten el *escalado automático*.</span><span class="sxs-lookup"><span data-stu-id="01cc3-107">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="01cc3-108">Puede usar el escalado automático basado en métricas o programación grupos de trabajo individuales.</span><span class="sxs-lookup"><span data-stu-id="01cc3-108">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![Opciones de escalado automático para un grupo de trabajo.][intro]

<span data-ttu-id="01cc3-110">El escalado automático optimiza el uso de recursos gracias al crecimiento y reducción automáticos de un entorno del Servicio de aplicaciones para ajustarse a su presupuesto o a su perfil de carga.</span><span class="sxs-lookup"><span data-stu-id="01cc3-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment to fit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="01cc3-111">Configuración del escalado automático de grupo de trabajo</span><span class="sxs-lookup"><span data-stu-id="01cc3-111">Configure worker pool autoscale</span></span>
<span data-ttu-id="01cc3-112">Puede acceder a la funcionalidad de escalado automático desde la pestaña **Configuración** del grupo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="01cc3-112">You can access the autoscale functionality from the **Settings** tab of the worker pool.</span></span>

![Pestaña Configuración del grupo de trabajo.][settings-scale]

<span data-ttu-id="01cc3-114">A partir de ahí, la interfaz debe resultar bastante familiar ya que se trata de la misma experiencia que ve al escala un plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="01cc3-114">From there, the interface should be fairly familiar since it is the same experience that you see when you scale an App Service plan.</span></span> 

![Configuración de la escala manual.][scale-manual]

<span data-ttu-id="01cc3-116">También puede configurar un perfil de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="01cc3-116">You can also configure an autoscale profile.</span></span>

![Configuración del escalado automático.][scale-profile]

<span data-ttu-id="01cc3-118">Los perfiles de escalado automático resultan útiles para establecer límites en la escala.</span><span class="sxs-lookup"><span data-stu-id="01cc3-118">Autoscale profiles are useful to set limits on your scale.</span></span> <span data-ttu-id="01cc3-119">De este modo tener una experiencia de rendimiento coherente, mediante el establecimiento de un valor de escala de límite inferior (1) y un techo de gasto predecible, mediante el establecimiento de un límite superior (2).</span><span class="sxs-lookup"><span data-stu-id="01cc3-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![Configuración de la escala en el perfil.][scale-profile2]

<span data-ttu-id="01cc3-121">Después de definir un perfil, puede agregar reglas de escalado automático para escalar o reducir verticalmente el número de instancias en el grupo de trabajo dentro de los límites definidos por el perfil.</span><span class="sxs-lookup"><span data-stu-id="01cc3-121">After you define a profile, you can add autoscale rules to scale up or down the number of instances in the worker pool within the bounds defined by the profile.</span></span> <span data-ttu-id="01cc3-122">Las reglas de escalado automático se basan en las métricas.</span><span class="sxs-lookup"><span data-stu-id="01cc3-122">Autoscale rules are based on metrics.</span></span>

![Regla de escala.][scale-rule]

 <span data-ttu-id="01cc3-124">Se puede usar cualquier grupo de trabajo o métrica de front-end para definir las reglas de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="01cc3-124">Any worker pool or front-end metrics can be used to define autoscale rules.</span></span> <span data-ttu-id="01cc3-125">Son las mismas métricas que puede supervisar en los gráficos de la hoja de recursos o para las que puede configurar alertas.</span><span class="sxs-lookup"><span data-stu-id="01cc3-125">These metrics are the same metrics you can monitor in the resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="01cc3-126">Ejemplo de escalado automático</span><span class="sxs-lookup"><span data-stu-id="01cc3-126">Autoscale example</span></span>
<span data-ttu-id="01cc3-127">La mejor manera de ilustrar el escalado automático de un entorno del Servicio de aplicaciones es mediante un escenario.</span><span class="sxs-lookup"><span data-stu-id="01cc3-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="01cc3-128">Este artículo explica todas las consideraciones necesarias para configurar el escalado automático.</span><span class="sxs-lookup"><span data-stu-id="01cc3-128">This article explains all the necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="01cc3-129">En este artículo veremos todas las interacciones que entran en juego cuando se aplica el escalado automático en los App Service Environment que se hospedan en un App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="01cc3-129">The article walks you through the interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="01cc3-130">Introducción al escenario</span><span class="sxs-lookup"><span data-stu-id="01cc3-130">Scenario introduction</span></span>
<span data-ttu-id="01cc3-131">Frank es administrador de sistemas de una empresa y ha migrado parte de las cargas de trabajo que administra a un entorno del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="01cc3-131">Frank is a sysadmin for an enterprise who has migrated a portion of the workloads that he manages to an App Service environment.</span></span>

<span data-ttu-id="01cc3-132">El entorno del Servicio de aplicaciones está configurado a escala manual de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="01cc3-132">The App Service environment is configured to manual scale as follows:</span></span>

* <span data-ttu-id="01cc3-133">**Servidores front-end** : 3</span><span class="sxs-lookup"><span data-stu-id="01cc3-133">**Front ends:** 3</span></span>
* <span data-ttu-id="01cc3-134">**Grupo de trabajo 1**: 10</span><span class="sxs-lookup"><span data-stu-id="01cc3-134">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="01cc3-135">**Grupo de trabajo 2**: 5</span><span class="sxs-lookup"><span data-stu-id="01cc3-135">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="01cc3-136">**Grupo de trabajo 3**: 5</span><span class="sxs-lookup"><span data-stu-id="01cc3-136">**Worker pool 3**: 5</span></span>

<span data-ttu-id="01cc3-137">El grupo de trabajo 1 se usa para las cargas de trabajo de producción, en tanto que los grupos de trabajo 2 y 3 se usan para las cargas de trabajo de control de calidad y desarrollo.</span><span class="sxs-lookup"><span data-stu-id="01cc3-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="01cc3-138">Los planes de App Service de QA y desarrollo están configurados para la escala manual.</span><span class="sxs-lookup"><span data-stu-id="01cc3-138">The App Service plans for QA and dev are configured to manual scale.</span></span> <span data-ttu-id="01cc3-139">El plan de App Service de producción se establece en escalado automático para tratar con las variaciones de carga y el tráfico.</span><span class="sxs-lookup"><span data-stu-id="01cc3-139">The production App Service plan is set to autoscale to deal with variations in load and traffic.</span></span>

<span data-ttu-id="01cc3-140">Frank está muy familiarizado con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="01cc3-140">Frank is very familiar with the application.</span></span> <span data-ttu-id="01cc3-141">Sabe que las horas pico de carga están entre las 9:00 y 6:00 porque se trata de una aplicación de línea de negocio (LOB) que los empleados usan mientras están en la oficina.</span><span class="sxs-lookup"><span data-stu-id="01cc3-141">He knows that the peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in the office.</span></span> <span data-ttu-id="01cc3-142">El uso cae después, una vez que los usuarios han terminado la jornada.</span><span class="sxs-lookup"><span data-stu-id="01cc3-142">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="01cc3-143">Fuera de las horas punta, sigue habiendo cierta carga porque los usuarios pueden acceder de forma remota a la aplicación mediante sus dispositivos móviles o equipos domésticos.</span><span class="sxs-lookup"><span data-stu-id="01cc3-143">Outside peak hours, there is still some load because users can access the app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="01cc3-144">El plan del servicio de Aplicaciones de producción ya está configurado para el escalado automático en función del uso de CPU con las reglas siguientes:</span><span class="sxs-lookup"><span data-stu-id="01cc3-144">The production App Service plan is already configured to autoscale based on CPU usage with the following rules:</span></span>

![Configuración específica para las aplicaciones LOB.][asp-scale]

| <span data-ttu-id="01cc3-146">**Perfil de escalado automático: Días laborables: plan del Servicio de aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="01cc3-146">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="01cc3-147">**Perfil de escalado automático: Fines de semana: plan del Servicio de aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="01cc3-147">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="01cc3-148">**Nombre:** perfil Día laborable</span><span class="sxs-lookup"><span data-stu-id="01cc3-148">**Name:** Weekday profile</span></span> |<span data-ttu-id="01cc3-149">**Nombre:** perfil Fin de semana</span><span class="sxs-lookup"><span data-stu-id="01cc3-149">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="01cc3-150">**Escalar por:** Reglas de rendimiento y programación</span><span class="sxs-lookup"><span data-stu-id="01cc3-150">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="01cc3-151">**Escalar por:** Reglas de rendimiento y programación</span><span class="sxs-lookup"><span data-stu-id="01cc3-151">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="01cc3-152">**Perfil:** Días laborables</span><span class="sxs-lookup"><span data-stu-id="01cc3-152">**Profile:** Weekdays</span></span> |<span data-ttu-id="01cc3-153">**Perfil:** Fin de semana</span><span class="sxs-lookup"><span data-stu-id="01cc3-153">**Profile:** Weekend</span></span> |
| <span data-ttu-id="01cc3-154">**Tipo:** periodicidad</span><span class="sxs-lookup"><span data-stu-id="01cc3-154">**Type:** Recurrence</span></span> |<span data-ttu-id="01cc3-155">**Tipo:** periodicidad</span><span class="sxs-lookup"><span data-stu-id="01cc3-155">**Type:** Recurrence</span></span> |
| <span data-ttu-id="01cc3-156">**Rango objetivo:** de 5 a 20 instancias</span><span class="sxs-lookup"><span data-stu-id="01cc3-156">**Target range:** 5 to 20 instances</span></span> |<span data-ttu-id="01cc3-157">**Rango objetivo:** de 3 a 10 instancias</span><span class="sxs-lookup"><span data-stu-id="01cc3-157">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="01cc3-158">**Días:** lunes, martes, miércoles, jueves, viernes</span><span class="sxs-lookup"><span data-stu-id="01cc3-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="01cc3-159">**Días:** sábado, domingo</span><span class="sxs-lookup"><span data-stu-id="01cc3-159">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="01cc3-160">**Hora de inicio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="01cc3-160">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="01cc3-161">**Hora de inicio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="01cc3-161">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="01cc3-162">**Zona horaria:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="01cc3-162">**Time zone:** UTC-08</span></span> |<span data-ttu-id="01cc3-163">**Zona horaria:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="01cc3-163">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="01cc3-164">**Regla de escalado automático (escalar verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="01cc3-164">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="01cc3-165">**Regla de escalado automático (escalar verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="01cc3-165">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="01cc3-166">**Recurso:** Producción (entorno del Servicio de aplicaciones)</span><span class="sxs-lookup"><span data-stu-id="01cc3-166">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="01cc3-167">**Recurso:** Producción (entorno del Servicio de aplicaciones)</span><span class="sxs-lookup"><span data-stu-id="01cc3-167">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="01cc3-168">**Métrica:** % de CPU</span><span class="sxs-lookup"><span data-stu-id="01cc3-168">**Metric:** CPU %</span></span> |<span data-ttu-id="01cc3-169">**Métrica:** % de CPU</span><span class="sxs-lookup"><span data-stu-id="01cc3-169">**Metric:** CPU %</span></span> |
| <span data-ttu-id="01cc3-170">**Operación:** Mayor que 60%</span><span class="sxs-lookup"><span data-stu-id="01cc3-170">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="01cc3-171">**Operación:** Mayor que 80%</span><span class="sxs-lookup"><span data-stu-id="01cc3-171">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="01cc3-172">**Duración:** 5 minutos</span><span class="sxs-lookup"><span data-stu-id="01cc3-172">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="01cc3-173">**Duración:** 10 minutos</span><span class="sxs-lookup"><span data-stu-id="01cc3-173">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="01cc3-174">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="01cc3-174">**Time aggregation:** Average</span></span> |<span data-ttu-id="01cc3-175">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="01cc3-175">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="01cc3-176">**Acción:** Aumentar recuento en 2</span><span class="sxs-lookup"><span data-stu-id="01cc3-176">**Action:** Increase count by 2</span></span> |<span data-ttu-id="01cc3-177">**Acción:** Aumentar recuento en 1</span><span class="sxs-lookup"><span data-stu-id="01cc3-177">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="01cc3-178">**Tiempo de finalización (minutos):** 15</span><span class="sxs-lookup"><span data-stu-id="01cc3-178">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="01cc3-179">**Tiempo de finalización (minutos):** 20</span><span class="sxs-lookup"><span data-stu-id="01cc3-179">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="01cc3-180">**Regla de escalado automático (reducir verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="01cc3-180">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="01cc3-181">**Regla de escalado automático (reducir verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="01cc3-181">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="01cc3-182">**Recurso:** Producción (entorno del Servicio de aplicaciones)</span><span class="sxs-lookup"><span data-stu-id="01cc3-182">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="01cc3-183">**Recurso:** Producción (entorno del Servicio de aplicaciones)</span><span class="sxs-lookup"><span data-stu-id="01cc3-183">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="01cc3-184">**Métrica:** % de CPU</span><span class="sxs-lookup"><span data-stu-id="01cc3-184">**Metric:** CPU %</span></span> |<span data-ttu-id="01cc3-185">**Métrica:** % de CPU</span><span class="sxs-lookup"><span data-stu-id="01cc3-185">**Metric:** CPU %</span></span> |
| <span data-ttu-id="01cc3-186">**Operación:** menor que el 30 %</span><span class="sxs-lookup"><span data-stu-id="01cc3-186">**Operation:** Less than 30%</span></span> |<span data-ttu-id="01cc3-187">**Operación:** menor que el 20 %</span><span class="sxs-lookup"><span data-stu-id="01cc3-187">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="01cc3-188">**Duración:** 10 minutos</span><span class="sxs-lookup"><span data-stu-id="01cc3-188">**Duration:** 10 minutes</span></span> |<span data-ttu-id="01cc3-189">**Duración:** 15 minutos</span><span class="sxs-lookup"><span data-stu-id="01cc3-189">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="01cc3-190">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="01cc3-190">**Time aggregation:** Average</span></span> |<span data-ttu-id="01cc3-191">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="01cc3-191">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="01cc3-192">**Acción:** Reducir recuento en 1</span><span class="sxs-lookup"><span data-stu-id="01cc3-192">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="01cc3-193">**Acción:** Reducir recuento en 1</span><span class="sxs-lookup"><span data-stu-id="01cc3-193">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="01cc3-194">**Tiempo de finalización (minutos):** 20</span><span class="sxs-lookup"><span data-stu-id="01cc3-194">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="01cc3-195">**Tiempo de finalización (minutos):** 10</span><span class="sxs-lookup"><span data-stu-id="01cc3-195">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="01cc3-196">Tasa de inflación del plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="01cc3-196">App Service plan inflation rate</span></span>
<span data-ttu-id="01cc3-197">Los planes de App Service configurados para el escalado automático se realizan a una tasa máxima por hora.</span><span class="sxs-lookup"><span data-stu-id="01cc3-197">App Service plans that are configured to autoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="01cc3-198">Esta tasa se puede calcular en función de los valores indicados en la regla de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="01cc3-198">This rate can be calculated based on the values provided on the autoscale rule.</span></span>

<span data-ttu-id="01cc3-199">Comprender y calcular la *tasa de inflación del plan del Servicio de aplicaciones* es importante para el escalado automático del entorno del Servicio de aplicaciones, ya que los cambios en el escalado de un grupo de trabajo no son instantáneos.</span><span class="sxs-lookup"><span data-stu-id="01cc3-199">Understanding and calculating the *App Service plan inflation rate* is important for App Service environment autoscale because scale changes to a worker pool are not instantaneous.</span></span>

<span data-ttu-id="01cc3-200">La tasa de inflación del plan del Servicio de aplicaciones se calcula del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="01cc3-200">The App Service plan inflation rate is calculated as follows:</span></span>

![Cálculo de la tasa de inflación del plan del Servicio de aplicaciones.][ASP-Inflation]

<span data-ttu-id="01cc3-202">De acuerdo con la regla Escalado automático: escalar verticalmente del perfil Días laborables del plan de App Service de producción:</span><span class="sxs-lookup"><span data-stu-id="01cc3-202">Based on the Autoscale – Scale Up rule for the Weekday profile of the production App Service plan:</span></span>

![Tasa de inflación del plan del Servicio de aplicaciones para los días laborables basándose en el escalado automático: regla escalar verticalmente.][Equation1]

<span data-ttu-id="01cc3-204">En el caso de la regla Escalado automático: escalar verticalmente del perfil Fines de semana del plan del Servicio de aplicaciones de producción, la fórmula daría como resultado:</span><span class="sxs-lookup"><span data-stu-id="01cc3-204">In the case of the Autoscale – Scale Up rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>

![Tasa de inflación del plan del Servicio de aplicaciones para los fines de semana basado en el escalado automático: regla escalar verticalmente.][Equation2]

<span data-ttu-id="01cc3-206">Este valor también se puede calcular para operaciones de reducción vertical.</span><span class="sxs-lookup"><span data-stu-id="01cc3-206">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="01cc3-207">De acuerdo con la regla Escalado automático: reducir verticalmente del perfil Días laborables del plan del Servicio de aplicaciones de producción, sería:</span><span class="sxs-lookup"><span data-stu-id="01cc3-207">Based on the Autoscale – Scale Down rule for the Weekday profile of the production App Service plan, this would look as follows:</span></span>

![Tasa de inflación del plan del Servicio de aplicaciones para los días laborables basándose en el escalado automático: regla reducir verticalmente.][Equation3]

<span data-ttu-id="01cc3-209">En el caso de la regla Escalado automático: reducir verticalmente del perfil Fines de semana del plan del Servicio de aplicaciones de producción, la fórmula daría como resultado:</span><span class="sxs-lookup"><span data-stu-id="01cc3-209">In the case of the Autoscale – Scale Down rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>  

![Tasa de inflación del plan del Servicio de aplicaciones para los fines de semana basado en el escalado automático: regla reducir verticalmente.][Equation4]

<span data-ttu-id="01cc3-211">El plan de App Service de producción puede crecer a una tasa máxima de ocho instancias por hora durante la semana y de cuatro instancias por hora durante los fines de semana.</span><span class="sxs-lookup"><span data-stu-id="01cc3-211">The production App Service plan can grow at a maximum rate of eight instances/hour during the week and four instances/hour during the weekend.</span></span> <span data-ttu-id="01cc3-212">Puede liberar las instancias a una tasa máxima de cuatro instancias por hora durante la semana y seis instancias por hora durante los fines de semana.</span><span class="sxs-lookup"><span data-stu-id="01cc3-212">It can release instances at a maximum rate of four instances/hour during the week and six instances/hour during weekends.</span></span>

<span data-ttu-id="01cc3-213">Si se hospedan varios planes del Servicio de aplicaciones en un grupo de trabajo, debe calcular la *tasa de inflación total* como la suma de la tasa de inflación de todos los planes del Servicio de aplicaciones que se hospedan en dicho grupo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="01cc3-213">If multiple App Service plans are being hosted in a worker pool, you have to calculate the *total inflation rate* as the sum of the inflation rate for all the App Service plans that are being hosting in that worker pool.</span></span>

![Cálculo de la tasa de inflación total para varios planes del Servicio de aplicaciones hospedados en un grupo de trabajo.][ASP-Total-Inflation]

### <a name="use-the-app-service-plan-inflation-rate-to-define-worker-pool-autoscale-rules"></a><span data-ttu-id="01cc3-215">Uso de la tasa de inflación del plan del Servicio de aplicaciones para definir reglas de escalado automático del grupo de trabajo</span><span class="sxs-lookup"><span data-stu-id="01cc3-215">Use the App Service plan inflation rate to define worker pool autoscale rules</span></span>
<span data-ttu-id="01cc3-216">Los grupos de trabajo que hospedan planes del App Service que están configurados para el escalado automático tendrán que asignar un búfer de capacidad.</span><span class="sxs-lookup"><span data-stu-id="01cc3-216">Worker pools that host App Service plans that are configured to autoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="01cc3-217">El búfer permite que las operaciones de escalado automático aumenten y reduzcan el plan del Servicio de aplicaciones según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="01cc3-217">The buffer allows for the autoscale operations to grow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="01cc3-218">El búfer mínimo será la tasa de inflación total del plan del Servicio de aplicaciones calculada.</span><span class="sxs-lookup"><span data-stu-id="01cc3-218">The minimum buffer would be the calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="01cc3-219">Puesto que las operaciones de escalado del entorno del Servicio de aplicaciones tardan algún tiempo en aplicarse, deben tenerse en cuenta los cambios de demanda adicionales que se pueden producir mientras están en curso una operación de escalado.</span><span class="sxs-lookup"><span data-stu-id="01cc3-219">Because App Service environment scale operations take some time to apply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="01cc3-220">Para dar cabida a esta latencia, se recomienda usar la tasa de inflación total del plan del Servicio de aplicaciones calculada como el número mínimo de instancias que se agregan para cada operación de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="01cc3-220">To accommodate this latency, we recommend that you use the calculated Total App Service Plan Inflation Rate as the minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="01cc3-221">Con esta información, Frank puede definir el siguiente perfil y las siguientes reglas de escalado automático:</span><span class="sxs-lookup"><span data-stu-id="01cc3-221">With this information, Frank can define the following autoscale profile and rules:</span></span>

![Ejemplo de reglas de perfil de escalado automático para línea de negocio.][Worker-Pool-Scale]

| <span data-ttu-id="01cc3-223">**Perfil de escalado automático: Días laborables**</span><span class="sxs-lookup"><span data-stu-id="01cc3-223">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="01cc3-224">**Perfil de escalado automático: Fines de semana**</span><span class="sxs-lookup"><span data-stu-id="01cc3-224">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="01cc3-225">**Nombre:** perfil Día laborable</span><span class="sxs-lookup"><span data-stu-id="01cc3-225">**Name:** Weekday profile</span></span> |<span data-ttu-id="01cc3-226">**Nombre:** perfil Fin de semana</span><span class="sxs-lookup"><span data-stu-id="01cc3-226">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="01cc3-227">**Escalar por:** Reglas de rendimiento y programación</span><span class="sxs-lookup"><span data-stu-id="01cc3-227">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="01cc3-228">**Escalar por:** Reglas de rendimiento y programación</span><span class="sxs-lookup"><span data-stu-id="01cc3-228">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="01cc3-229">**Perfil:** Días laborables</span><span class="sxs-lookup"><span data-stu-id="01cc3-229">**Profile:** Weekdays</span></span> |<span data-ttu-id="01cc3-230">**Perfil:** Fin de semana</span><span class="sxs-lookup"><span data-stu-id="01cc3-230">**Profile:** Weekend</span></span> |
| <span data-ttu-id="01cc3-231">**Tipo:** periodicidad</span><span class="sxs-lookup"><span data-stu-id="01cc3-231">**Type:** Recurrence</span></span> |<span data-ttu-id="01cc3-232">**Tipo:** periodicidad</span><span class="sxs-lookup"><span data-stu-id="01cc3-232">**Type:** Recurrence</span></span> |
| <span data-ttu-id="01cc3-233">**Rango objetivo:** de 13 a 25 instancias</span><span class="sxs-lookup"><span data-stu-id="01cc3-233">**Target range:** 13 to 25 instances</span></span> |<span data-ttu-id="01cc3-234">**Rango objetivo:** de 6 a 15 instancias</span><span class="sxs-lookup"><span data-stu-id="01cc3-234">**Target range:** 6 to 15 instances</span></span> |
| <span data-ttu-id="01cc3-235">**Días:** lunes, martes, miércoles, jueves, viernes</span><span class="sxs-lookup"><span data-stu-id="01cc3-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="01cc3-236">**Días:** sábado, domingo</span><span class="sxs-lookup"><span data-stu-id="01cc3-236">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="01cc3-237">**Hora de inicio:** 7:00</span><span class="sxs-lookup"><span data-stu-id="01cc3-237">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="01cc3-238">**Hora de inicio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="01cc3-238">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="01cc3-239">**Zona horaria:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="01cc3-239">**Time zone:** UTC-08</span></span> |<span data-ttu-id="01cc3-240">**Zona horaria:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="01cc3-240">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="01cc3-241">**Regla de escalado automático (escalar verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="01cc3-241">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="01cc3-242">**Regla de escalado automático (escalar verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="01cc3-242">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="01cc3-243">**Recurso:** Grupo de trabajo 1</span><span class="sxs-lookup"><span data-stu-id="01cc3-243">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="01cc3-244">**Recurso:** Grupo de trabajo 1</span><span class="sxs-lookup"><span data-stu-id="01cc3-244">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="01cc3-245">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="01cc3-245">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="01cc3-246">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="01cc3-246">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="01cc3-247">**Operación:** Menor que 8</span><span class="sxs-lookup"><span data-stu-id="01cc3-247">**Operation:** Less than 8</span></span> |<span data-ttu-id="01cc3-248">**Operación:** Menor que 3</span><span class="sxs-lookup"><span data-stu-id="01cc3-248">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="01cc3-249">**Duración:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="01cc3-249">**Duration:** 20 minutes</span></span> |<span data-ttu-id="01cc3-250">**Duración:** 30 minutos</span><span class="sxs-lookup"><span data-stu-id="01cc3-250">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="01cc3-251">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="01cc3-251">**Time aggregation:** Average</span></span> |<span data-ttu-id="01cc3-252">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="01cc3-252">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="01cc3-253">**Acción:** Aumentar recuento en 8</span><span class="sxs-lookup"><span data-stu-id="01cc3-253">**Action:** Increase count by 8</span></span> |<span data-ttu-id="01cc3-254">**Acción:** Aumentar recuento en 3</span><span class="sxs-lookup"><span data-stu-id="01cc3-254">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="01cc3-255">**Tiempo de finalización (minutos):** 180</span><span class="sxs-lookup"><span data-stu-id="01cc3-255">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="01cc3-256">**Tiempo de finalización (minutos):** 180</span><span class="sxs-lookup"><span data-stu-id="01cc3-256">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="01cc3-257">**Regla de escalado automático (reducir verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="01cc3-257">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="01cc3-258">**Regla de escalado automático (reducir verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="01cc3-258">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="01cc3-259">**Recurso:** Grupo de trabajo 1</span><span class="sxs-lookup"><span data-stu-id="01cc3-259">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="01cc3-260">**Recurso:** Grupo de trabajo 1</span><span class="sxs-lookup"><span data-stu-id="01cc3-260">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="01cc3-261">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="01cc3-261">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="01cc3-262">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="01cc3-262">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="01cc3-263">**Operación:** Mayor que 8</span><span class="sxs-lookup"><span data-stu-id="01cc3-263">**Operation:** Greater than 8</span></span> |<span data-ttu-id="01cc3-264">**Operación:** Mayor que 3 %</span><span class="sxs-lookup"><span data-stu-id="01cc3-264">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="01cc3-265">**Duración:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="01cc3-265">**Duration:** 20 minutes</span></span> |<span data-ttu-id="01cc3-266">**Duración:** 15 minutos</span><span class="sxs-lookup"><span data-stu-id="01cc3-266">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="01cc3-267">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="01cc3-267">**Time aggregation:** Average</span></span> |<span data-ttu-id="01cc3-268">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="01cc3-268">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="01cc3-269">**Acción:** Reducir recuento en 2</span><span class="sxs-lookup"><span data-stu-id="01cc3-269">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="01cc3-270">**Acción:** Reducir recuento en 3</span><span class="sxs-lookup"><span data-stu-id="01cc3-270">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="01cc3-271">**Tiempo de finalización (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="01cc3-271">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="01cc3-272">**Tiempo de finalización (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="01cc3-272">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="01cc3-273">El rango objetivo definido en el perfil se calcula sumando el número mínimo de instancias definido en el perfil para el plan del Servicio de aplicaciones al búfer.</span><span class="sxs-lookup"><span data-stu-id="01cc3-273">The Target range defined in the profile is calculated by the minimum instances defined in the profile for the App Service plan + buffer.</span></span>

<span data-ttu-id="01cc3-274">El rango máximo debe ser la suma de todos los rangos máximos de todos los planes del Servicio de aplicaciones alojados en el grupo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="01cc3-274">The Maximum range would be the sum of all the maximum ranges for all App Service plans hosted in the worker pool.</span></span>

<span data-ttu-id="01cc3-275">El recuento de aumento de las reglas de escalado vertical se debe configurar al menos en 1X de la tasa de inflación del Plan del Servicio de aplicaciones para el escalado vertical.</span><span class="sxs-lookup"><span data-stu-id="01cc3-275">The Increase count for the scale up rules should be set to at least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="01cc3-276">El recuento de reducción se puede ajustar en un valor situado entre 1/2X y 1X de la tasa de inflación del plan del Servicio de aplicaciones para la reducción vertical.</span><span class="sxs-lookup"><span data-stu-id="01cc3-276">Decrease count can be adjusted to something between 1/2X or 1X the App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="01cc3-277">Escalado automático para un grupo de servidores front-end</span><span class="sxs-lookup"><span data-stu-id="01cc3-277">Autoscale for front-end pool</span></span>
<span data-ttu-id="01cc3-278">Las reglas de escalado automático de front-end son más sencillas que las de los grupos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="01cc3-278">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="01cc3-279">En primer lugar, debe</span><span class="sxs-lookup"><span data-stu-id="01cc3-279">Primarily, you should</span></span>  
<span data-ttu-id="01cc3-280">asegurarse de que dicha duración de la medida y los temporizadores de enfriamiento tienen en cuenta que las operaciones de escala no son instantáneas en un plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="01cc3-280">make sure that duration of the measurement and the cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="01cc3-281">En este escenario, Frank sabe que la tasa de errores aumenta una vez que los servidores front-end alcanzan el 80 % de uso de CPU y configura la regla de escalado automático para que aumente las instancias como sigue:</span><span class="sxs-lookup"><span data-stu-id="01cc3-281">For this scenario, Frank knows that the error rate increases after front ends reach 80% CPU utilization and sets the autoscale rule to increase instances as follows:</span></span>

![Configuración del escalado automático para un grupo de servidores front-end.][Front-End-Scale]

| <span data-ttu-id="01cc3-283">**Perfil de escalado automático: Servidores front-end**</span><span class="sxs-lookup"><span data-stu-id="01cc3-283">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="01cc3-284">**Nombre:** Escalado automático: Servidores front-end</span><span class="sxs-lookup"><span data-stu-id="01cc3-284">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="01cc3-285">**Escalar por:** Reglas de rendimiento y programación</span><span class="sxs-lookup"><span data-stu-id="01cc3-285">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="01cc3-286">**Perfil:** Todos los días</span><span class="sxs-lookup"><span data-stu-id="01cc3-286">**Profile:** Everyday</span></span> |
| <span data-ttu-id="01cc3-287">**Tipo:** periodicidad</span><span class="sxs-lookup"><span data-stu-id="01cc3-287">**Type:** Recurrence</span></span> |
| <span data-ttu-id="01cc3-288">**Rango objetivo:** de 3 a 10 instancias</span><span class="sxs-lookup"><span data-stu-id="01cc3-288">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="01cc3-289">**Días:** Todos los días</span><span class="sxs-lookup"><span data-stu-id="01cc3-289">**Days:** Everyday</span></span> |
| <span data-ttu-id="01cc3-290">**Hora de inicio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="01cc3-290">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="01cc3-291">**Zona horaria:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="01cc3-291">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="01cc3-292">**Regla de escalado automático (escalar verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="01cc3-292">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="01cc3-293">**Recurso:** Grupo de servidores front-end</span><span class="sxs-lookup"><span data-stu-id="01cc3-293">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="01cc3-294">**Métrica:** % de CPU</span><span class="sxs-lookup"><span data-stu-id="01cc3-294">**Metric:** CPU %</span></span> |
| <span data-ttu-id="01cc3-295">**Operación:** Mayor que 60%</span><span class="sxs-lookup"><span data-stu-id="01cc3-295">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="01cc3-296">**Duración:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="01cc3-296">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="01cc3-297">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="01cc3-297">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="01cc3-298">**Acción:** Aumentar recuento en 3</span><span class="sxs-lookup"><span data-stu-id="01cc3-298">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="01cc3-299">**Tiempo de finalización (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="01cc3-299">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="01cc3-300">**Regla de escalado automático (reducir verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="01cc3-300">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="01cc3-301">**Recurso:** Grupo de trabajo 1</span><span class="sxs-lookup"><span data-stu-id="01cc3-301">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="01cc3-302">**Métrica:** % de CPU</span><span class="sxs-lookup"><span data-stu-id="01cc3-302">**Metric:** CPU %</span></span> |
| <span data-ttu-id="01cc3-303">**Operación:** menor que el 30 %</span><span class="sxs-lookup"><span data-stu-id="01cc3-303">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="01cc3-304">**Duración:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="01cc3-304">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="01cc3-305">**Agregación de tiempo:** media</span><span class="sxs-lookup"><span data-stu-id="01cc3-305">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="01cc3-306">**Acción:** Reducir recuento en 3</span><span class="sxs-lookup"><span data-stu-id="01cc3-306">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="01cc3-307">**Tiempo de finalización (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="01cc3-307">**Cool down (minutes):** 120</span></span> |

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
