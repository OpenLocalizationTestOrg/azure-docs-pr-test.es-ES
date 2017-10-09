---
title: Interfaz de usuario de Mobile Engagement - aaaAzure de segmentos
description: "Obtenga información acerca de cómo toocreate y administran segmentos de patrones de uso de los usuarios tooidentify con Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a><span data-ttu-id="e9290-103">¿Cómo toocreate y administran segmentos de patrones de uso de los usuarios tooidentify</span><span class="sxs-lookup"><span data-stu-id="e9290-103">How toocreate and manage segments of users tooidentify usage patterns</span></span>
<span data-ttu-id="e9290-104">Este artículo describe hello **segmentos** ficha de hello **Mobile Engagement** portal.</span><span class="sxs-lookup"><span data-stu-id="e9290-104">This article describes hello **SEGMENTS** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="e9290-105">Usar hello **Mobile Engagement** toomonitor portal y administrar aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="e9290-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span>

<span data-ttu-id="e9290-106">sección de segmentos de Hola de hello interfaz de usuario le permite toowork en la segmentación de los usuarios según un comportamiento diferente Hola y de análisis que puede obtener de la aplicación hello y también puede tener acceso a través de la API de segmentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9290-106">hello Segments section of hello UI allows you toowork on segmenting your users based on hello different behavior and analytics that you can get from hello application and can also access through hello Segments API.</span></span> <span data-ttu-id="e9290-107">Segmentos se calculan primero 24 horas después de que se crearon y se vuelven a calcular cada 24 horas en función de la información de análisis más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9290-107">Segments are first computed 24 hours after they are created, and they are recomputed every 24 hours based on hello latest analytics information.</span></span> <span data-ttu-id="e9290-108">Una vez que se calcula un segmento, muestra un gráfico de "Historial de tooday día" cada día.</span><span class="sxs-lookup"><span data-stu-id="e9290-108">Once a segment is calculated, it displays a "Day tooday history" chart each day.</span></span>

> [!NOTE]
> <span data-ttu-id="e9290-109">Muchas de las secciones de hello **Mobile Engagement** portal de interfaz de usuario contienen hello **ayuda para mostrar** botón.</span><span class="sxs-lookup"><span data-stu-id="e9290-109">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="e9290-110">Presione este botón tooget más información contextual sobre una sección.</span><span class="sxs-lookup"><span data-stu-id="e9290-110">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="create-segments"></a><span data-ttu-id="e9290-111">Crear segmentos</span><span class="sxs-lookup"><span data-stu-id="e9290-111">Create Segments</span></span>
<span data-ttu-id="e9290-112">Puede crear un segmento basándose en los criterios de too10 en un período específico días laborables too60 Hola pasado desde la sección de análisis de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9290-112">You can create a segment based on up too10 criteria on a specific period up too60 days in hello past from hello analytics section.</span></span> <span data-ttu-id="e9290-113">Por ejemplo, puede crear un segmento basándose en hello quienes han consultado ciertas páginas o buscar contenido específico dentro de la aplicación dentro de hello últimos 10 días.</span><span class="sxs-lookup"><span data-stu-id="e9290-113">For example, you can create a segment based on hello people who have viewed certain pages or searched for specific content within your app within hello last 10 days.</span></span> <span data-ttu-id="e9290-114">Esta información está disponible en la sección de análisis de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9290-114">This information is available in hello analytics section.</span></span> <span data-ttu-id="e9290-115">Por lo tanto, puede usar las expresiones toocreate un segmento y, a continuación, configurar una tootarget de notificación de inserción este subconjunto de usuarios tooget les toocome toohello atrás aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9290-115">So, you can use it toocreate a segment, and then set up a push notification tootarget this subset of users tooget them toocome back toohello application.</span></span> 

> [!NOTE]
> <span data-ttu-id="e9290-116">Una vez que se ha calculado un segmento, no se puede editar; solo se puede clonar (copiar) o destruir (eliminar).</span><span class="sxs-lookup"><span data-stu-id="e9290-116">Once a segment has been calculated, it cannot be edited; it can only be cloned (copied) or destroyed (deleted).</span></span> <span data-ttu-id="e9290-117">Se puede clonar un segmento dentro de hello misma aplicación (con Hola AppID mismo), y también se puede clonar en otras aplicaciones (con un AppID diferentes).</span><span class="sxs-lookup"><span data-stu-id="e9290-117">A segment can be cloned within hello same application (with hello same AppID), and it can also be cloned into other applications (with a different AppID).</span></span> 

 ![segments1][35] 

## <a name="examples-segments"></a><span data-ttu-id="e9290-119">Segmentos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e9290-119">Examples Segments</span></span>
 ![segments2][36]

<span data-ttu-id="e9290-121">Segmentos de permitir que los usuarios finales de toosegment hello de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9290-121">Segments allow you toosegment hello end-users of your application.</span></span>
<span data-ttu-id="e9290-122">La segmentación de los usuarios es una estrategia de marketing importante.</span><span class="sxs-lookup"><span data-stu-id="e9290-122">Segmenting your users is an important marketing strategy.</span></span> <span data-ttu-id="e9290-123">Azure Mobile Engagement le permite tooget los datos históricos y crear segmentos personalizados.</span><span class="sxs-lookup"><span data-stu-id="e9290-123">Azure Mobile Engagement allows you tooget historic data and create custom segments.</span></span> <span data-ttu-id="e9290-124">Esta eficaz herramienta le permite toolearn sobre la experiencia de los clientes en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9290-124">This powerful tool enables you toolearn about your customers’ experience in your application.</span></span> <span data-ttu-id="e9290-125">Puede analizar fácilmente los segmentos y utilizarlos como destinos de inserción.</span><span class="sxs-lookup"><span data-stu-id="e9290-125">You can easily analyze your segments and use your segments as push targets.</span></span>
<span data-ttu-id="e9290-126">Un caso de uso común es que desea toosend una inserción de una notificación tooencourage su toorate de los usuarios finales la aplicación en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9290-126">A common use-case is that you want toosend a push a notification tooencourage your end-users toorate your application in hello store.</span></span> <span data-ttu-id="e9290-127">En lugar de enviar una notificación tooall los usuarios finales, puede crear un segmento que especificaría solo los usuarios que han usado la aplicación cada día para hello último mes y que han tenido un usuario gran experiencia.</span><span class="sxs-lookup"><span data-stu-id="e9290-127">Rather than sending a notification tooall your end-users, you can create a segment that would specify only users that have used your application every day for hello last month and have had a great user experience.</span></span> <span data-ttu-id="e9290-128">Cuando se envían menos notificaciones de inserción de mayor grado de orientación, se obtiene una mayor rentabilidad.</span><span class="sxs-lookup"><span data-stu-id="e9290-128">When you send fewer, highly targeted push notifications, you get a better ROI.</span></span>

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a><span data-ttu-id="e9290-130">Segmentos que se pueden crear en función de los elementos principales de Azure Mobile Engagement de hello:</span><span class="sxs-lookup"><span data-stu-id="e9290-130">Segments you can create based on hello major Azure Mobile Engagement elements:</span></span>
* <span data-ttu-id="e9290-131">Evento: crear un segmento de ese evento específico uno de destinos de la aplicación hello que se produjeron más de dos veces por semana.</span><span class="sxs-lookup"><span data-stu-id="e9290-131">Event: create a segment that targets one specific event of hello application that happened more than twice a week.</span></span> 
* <span data-ttu-id="e9290-132">Sesión: crear un segmento de usuarios que han usado la aplicación hello más de 5 veces la semana pasada.</span><span class="sxs-lookup"><span data-stu-id="e9290-132">Session: create a segment of users that have used hello application more than 5 times last week.</span></span>
* <span data-ttu-id="e9290-133">Actividad: cree un segmento de los usuarios que hayan utilizado una página o contenido más o menos de 10 horas el último mes.</span><span class="sxs-lookup"><span data-stu-id="e9290-133">Activity: create a segment of users that have used one page or content more or less than 10 time last month.</span></span>
* <span data-ttu-id="e9290-134">Trabajo: cree un segmento de usuarios que ha completado un trabajo más de dos veces al día.</span><span class="sxs-lookup"><span data-stu-id="e9290-134">Job: create a segment of users that have completed a job more than twice a day.</span></span>
* <span data-ttu-id="e9290-135">Bloqueo: crear un segmento de todos los usuarios de Hola que han tenido un bloqueo más de 10 veces la semana pasada.</span><span class="sxs-lookup"><span data-stu-id="e9290-135">Crash: create a segment of all hello users that have had a crash more than 10 times last week.</span></span> <span data-ttu-id="e9290-136">(Puede insertar este segmento con una disculpa o incluso un cupón).</span><span class="sxs-lookup"><span data-stu-id="e9290-136">(You could push this segment with an apology or even a coupon!)</span></span>
* <span data-ttu-id="e9290-137">Error: crear un segmento de todos los usuarios de Hola que han tenido un error más de 100 veces últimos 3 días.</span><span class="sxs-lookup"><span data-stu-id="e9290-137">Error: create a segment of all hello users that have had an error more than 100 times last 3 days.</span></span>
* <span data-ttu-id="e9290-138">Información de la aplicación: crear un segmento que tenga como destino una información de aplicación personalizada que se produjo durante el saludo últimos 25 días.</span><span class="sxs-lookup"><span data-stu-id="e9290-138">App Info: create a segment that targets a custom App Info that happened during hello last 25 days.</span></span>
  
  ![segments4][38]

<span data-ttu-id="e9290-140">toouse segmento de una forma óptima, debe haber hecho una integración personalizada de hello SDK en la aplicación con un plan de etiquetado de etiquetas "Información de la aplicación".</span><span class="sxs-lookup"><span data-stu-id="e9290-140">toouse Segment in an optimal way, you must have done a customized integration of hello SDK in your application with a tagging plan of "App Info" tags.</span></span>
<span data-ttu-id="e9290-141">A continuación, ir a página de inicio de toohello de interfaz de hello, seleccione aplicación de Hola que desee y haga clic en la sección de "Segmentos" Hola.</span><span class="sxs-lookup"><span data-stu-id="e9290-141">Then, go toohello home page of hello interface, select hello application you want and click on hello "Segments" section.</span></span>

1. <span data-ttu-id="e9290-142">Seleccione la sección de "Segmentos" Hola.</span><span class="sxs-lookup"><span data-stu-id="e9290-142">Select hello "Segments" section.</span></span>
2. <span data-ttu-id="e9290-143">Haga clic en "Nuevo segmento" hello botón toocreate un segmento nuevo.</span><span class="sxs-lookup"><span data-stu-id="e9290-143">Click on hello "New segment" button toocreate a new segment.</span></span>

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a><span data-ttu-id="e9290-144">Ejemplo en la vida real: cree un segmento simple basado en la información de "Sesión"</span><span class="sxs-lookup"><span data-stu-id="e9290-144">Real Life Example: Create a simple segment based on "Session" information</span></span>
<span data-ttu-id="e9290-145">Crear un segmento de todos los usuarios finales de Hola que ha usado la aplicación al menos 50 veces de hello última semana.</span><span class="sxs-lookup"><span data-stu-id="e9290-145">Create a segment of all hello end-users that have used your app at least 50 times in hello last week.</span></span> <span data-ttu-id="e9290-146">Desde allí, buscar solo usuarios finales de Hola que han invertido al menos 30 segundos en la aplicación por sesión.</span><span class="sxs-lookup"><span data-stu-id="e9290-146">From there, find only hello end-users that have spent at least 30 seconds in your app per session.</span></span> <span data-ttu-id="e9290-147">Esto mostrará todos los usuarios finales de Hola que tengan una experiencia positiva en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9290-147">This will show all hello end-users who have a positive experience in your app.</span></span> <span data-ttu-id="e9290-148">A continuación, segmento Hola creado podría ser utilizado toopush un tooask de los usuarios finales de notificación toothese les toorate la aplicación Hola almacenar.</span><span class="sxs-lookup"><span data-stu-id="e9290-148">Then, hello segment created could be used toopush a notification toothese end-users tooask them toorate your app in hello store.</span></span>

 ![segments5][39]

1. <span data-ttu-id="e9290-150">Asigne un nombre de segmento en orden toofind rápidamente en la lista de "Segmento" Hola.</span><span class="sxs-lookup"><span data-stu-id="e9290-150">Give your segment a name in order toofind it quickly in hello "Segment" list.</span></span>
2. <span data-ttu-id="e9290-151">Haga clic en hello botón "Crear".</span><span class="sxs-lookup"><span data-stu-id="e9290-151">Click on hello "Create" button.</span></span>
   
   ![segments6][40]

<span data-ttu-id="e9290-153">Seleccione la sesión.</span><span class="sxs-lookup"><span data-stu-id="e9290-153">Select Session.</span></span>

 ![segments7][41]

1. <span data-ttu-id="e9290-155">Seleccione el período de Hola de "Última semana".</span><span class="sxs-lookup"><span data-stu-id="e9290-155">Select hello period of "Last week".</span></span>
2. <span data-ttu-id="e9290-156">Haga clic en Siguiente.</span><span class="sxs-lookup"><span data-stu-id="e9290-156">Click next.</span></span>
   
   ![segments8][42]
3. <span data-ttu-id="e9290-158">Seleccione Hola operador que es relevante en lista de hello: =; ≥, ≤.</span><span class="sxs-lookup"><span data-stu-id="e9290-158">Select hello Operator that is relevant among hello list: =; ≥, ≤.</span></span>
4. <span data-ttu-id="e9290-159">Escriba Hola número que desea.</span><span class="sxs-lookup"><span data-stu-id="e9290-159">Enter hello Count you want.</span></span>
5. <span data-ttu-id="e9290-160">Seleccione Hola aparición que desee.</span><span class="sxs-lookup"><span data-stu-id="e9290-160">Select hello Occurrence you want.</span></span> 
6. <span data-ttu-id="e9290-161">Haga clic en Siguiente.</span><span class="sxs-lookup"><span data-stu-id="e9290-161">Click next.</span></span>
   <span data-ttu-id="e9290-162">En este ejemplo se establece para esa over Hola última semana, los usuarios de coincidencia que han realizado al menos 50 sesiones.</span><span class="sxs-lookup"><span data-stu-id="e9290-162">This example is set so that over hello last week, match users that have made at least 50 sessions.</span></span>
   
   ![segments9][43]

<span data-ttu-id="e9290-164">Para hello segmentación de sesión, puede elegir longitud Hola por sesión como criterio.</span><span class="sxs-lookup"><span data-stu-id="e9290-164">For hello Session segmentation, you can choose hello length per session as a criteria.</span></span>

1. <span data-ttu-id="e9290-165">Seleccione Hola operador de hello lista.</span><span class="sxs-lookup"><span data-stu-id="e9290-165">Select hello Operator from hello list.</span></span>
2. <span data-ttu-id="e9290-166">Proporcionar Hola longitud por sesión.</span><span class="sxs-lookup"><span data-stu-id="e9290-166">Provide hello Length per session.</span></span>
3. <span data-ttu-id="e9290-167">Haga clic en Siguiente.</span><span class="sxs-lookup"><span data-stu-id="e9290-167">Click Next.</span></span>
   <span data-ttu-id="e9290-168">En este ejemplo, dice que omite todo hello las sesiones que se ha segmentado en la sección de la aparición de hello, seleccione sólo Hola los usuarios que han invertido más de 30 segundos por sesión.</span><span class="sxs-lookup"><span data-stu-id="e9290-168">In this example, it says that over all hello sessions that have been segmented on hello occurrence section, select only hello users that have spent more than 30 seconds per session.</span></span>
   
   ![segments10][44]

<span data-ttu-id="e9290-170">El criterio en tooretrieve pedido en hello completar el nombre de embudo y haga clic en Finalizar.</span><span class="sxs-lookup"><span data-stu-id="e9290-170">Name your criterion in order tooretrieve it in hello complete funnel, and click Finish.</span></span>

 ![segments11][45]

<span data-ttu-id="e9290-172">Cuando haya terminado de configurar el criterio, aparecerá en el embudo de segmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9290-172">When you have finished setting up your criterion, it will appear in hello segment funnel.</span></span>
<span data-ttu-id="e9290-173">Dado que los segmentos se basan en un segmento de datos de análisis, los segmentos se calculan una vez al día.</span><span class="sxs-lookup"><span data-stu-id="e9290-173">Because a segment is based on analytics data, segments are computed once per day.</span></span>
<span data-ttu-id="e9290-174">En este ejemplo, 47,7% de los usuarios finales de hello total coincide con el criterio de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9290-174">In this example, 47,7% of hello total end-users matched hello criterion.</span></span> <span data-ttu-id="e9290-175">Deben ser usuarios de Hola que han tenido una buena experiencia y se pueden tooprovide probablemente una clasificación mayor si se inserta una notificación pedirles toorate aplicación de hello en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9290-175">They should be hello users who have had a good experience and will be likely tooprovide a higher rating if you push them a notification asking them toorate hello app in hello store.</span></span>

## <a name="see-also"></a><span data-ttu-id="e9290-176">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="e9290-176">See also</span></span>
* <span data-ttu-id="e9290-177">[Conceptos][Link 6]</span><span class="sxs-lookup"><span data-stu-id="e9290-177">[Concepts][Link 6]</span></span>
* <span data-ttu-id="e9290-178">[Guía de solución de problemas de servicios][Link 24]</span><span class="sxs-lookup"><span data-stu-id="e9290-178">[Troubleshooting Guide Service][Link 24]</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

