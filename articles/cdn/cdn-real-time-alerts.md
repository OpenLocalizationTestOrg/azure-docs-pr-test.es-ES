---
title: Alertas en tiempo real en la red CDN de Azure | Microsoft Docs
description: "Alertas en tiempo real en la red CDN de Microsoft Azure. Las alertas en tiempo real proporcionan notificaciones acerca del rendimiento de los puntos de conexión en un perfil de la red CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6e66eb076ac7220823a848b5047f147d4101cd55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="28023-104">Alertas en tiempo real en la red CDN de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="28023-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="28023-105">Información general</span><span class="sxs-lookup"><span data-stu-id="28023-105">Overview</span></span>
<span data-ttu-id="28023-106">En este documento se explican las alertas en tiempo real en la red CDN de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="28023-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="28023-107">Esta funcionalidad proporciona notificaciones en tiempo real acerca del rendimiento de los puntos de conexión en un perfil de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="28023-107">This functionality provides real-time notifications about the performance of the endpoints in your CDN profile.</span></span>  <span data-ttu-id="28023-108">Las alertas de correo o de HTTP se pueden configurar por:</span><span class="sxs-lookup"><span data-stu-id="28023-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="28023-109">Ancho de banda</span><span class="sxs-lookup"><span data-stu-id="28023-109">Bandwidth</span></span>
* <span data-ttu-id="28023-110">Códigos de estado</span><span class="sxs-lookup"><span data-stu-id="28023-110">Status Codes</span></span>
* <span data-ttu-id="28023-111">Estados de la memoria caché</span><span class="sxs-lookup"><span data-stu-id="28023-111">Cache Statuses</span></span>
* <span data-ttu-id="28023-112">Conexiones</span><span class="sxs-lookup"><span data-stu-id="28023-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="28023-113">Creación de una alerta en tiempo real</span><span class="sxs-lookup"><span data-stu-id="28023-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="28023-114">En el [Portal de Azure](https://portal.azure.com), vaya a su perfil de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="28023-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![Hoja del perfil de red CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="28023-116">En la hoja de perfil de CDN, haga clic en el botón **Administrar** .</span><span class="sxs-lookup"><span data-stu-id="28023-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="28023-118">Se abre el portal de administración de CDN.</span><span class="sxs-lookup"><span data-stu-id="28023-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="28023-119">Mantenga el mouse sobre la pestaña **Análisis** y, después, sobre el control flotante **Estadísticas en tiempo real**.</span><span class="sxs-lookup"><span data-stu-id="28023-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="28023-120">Haga clic en **Real-Time Alerts**(Alertas en tiempo real).</span><span class="sxs-lookup"><span data-stu-id="28023-120">Click on **Real-Time Alerts**.</span></span>
   
    ![Portal de administración de la red CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="28023-122">Se muestra la lista de las configuraciones de alerta existentes (si hay alguna).</span><span class="sxs-lookup"><span data-stu-id="28023-122">The list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="28023-123">Haga clic en el botón **Add Alert** (Agregar alerta).</span><span class="sxs-lookup"><span data-stu-id="28023-123">Click the **Add Alert** button.</span></span>
   
    ![Botón Add Alert (Agregar alerta)](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="28023-125">Se muestra un formulario para crear una alerta nueva.</span><span class="sxs-lookup"><span data-stu-id="28023-125">A form for creating a new alert is displayed.</span></span>
   
    ![Formulario de alerta nueva](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="28023-127">Si quiere que esta alerta se active al hacer clic en **Guardar**, active la casilla **Alerta habilitada**.</span><span class="sxs-lookup"><span data-stu-id="28023-127">If you want this alert to be active when you click **Save**, check the **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="28023-128">Escriba un nombre descriptivo para la alerta en el campo **Name** (Nombre).</span><span class="sxs-lookup"><span data-stu-id="28023-128">Enter a descriptive name for your alert in the **Name** field.</span></span>
7. <span data-ttu-id="28023-129">En la lista desplegable **Tipo de medio**, seleccione **Objeto grande HTTP**.</span><span class="sxs-lookup"><span data-stu-id="28023-129">In the **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![Tipo de medio con objetos HTTP grande seleccionado](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="28023-131">Necesita seleccionar **Objeto grande HTTP** en **Tipo de medio**.</span><span class="sxs-lookup"><span data-stu-id="28023-131">You must select **HTTP Large Object** as the **Media Type**.</span></span>  <span data-ttu-id="28023-132">**CDN de Azure de Verizon**no usa las restantes opciones.</span><span class="sxs-lookup"><span data-stu-id="28023-132">The other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="28023-133">Si no se selecciona **HTTP Large Object** (Objeto HTTP grande), la alerta nunca se desencadenará.</span><span class="sxs-lookup"><span data-stu-id="28023-133">Failure to select **HTTP Large Object** will cause your alert to never be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="28023-134">Cree la **expresión** que quiera supervisar (para hacerlo, seleccione una **métrica**, un **operador** y un **valor desencadenador**).</span><span class="sxs-lookup"><span data-stu-id="28023-134">Create an **Expression** to monitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="28023-135">En **Metric**(Métrica), seleccione el tipo de condición que desea supervisar.</span><span class="sxs-lookup"><span data-stu-id="28023-135">For **Metric**, select the type of condition you want monitored.</span></span>  <span data-ttu-id="28023-136">**Bandwidth Mbps** (Mbps de ancho de banda) es la cantidad de uso del ancho de banda, en megabits por segundo.</span><span class="sxs-lookup"><span data-stu-id="28023-136">**Bandwidth Mbps** is the amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="28023-137">**Total Connections** (Total de conexiones) es el número de conexiones HTTP simultáneas a nuestros servidores perimetrales.</span><span class="sxs-lookup"><span data-stu-id="28023-137">**Total Connections** is the number of concurrent HTTP connections to our edge servers.</span></span>  <span data-ttu-id="28023-138">Vea las definiciones de los diferentes estados de la memoria caché y códigos de estado en [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) (Códigos de estado de la memoria caché de la red CDN de Azure) y [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx) (Códigos de estado HTTP de la red CDN de Azure).</span><span class="sxs-lookup"><span data-stu-id="28023-138">For definitions of the various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="28023-139">**Operator** (Operador) es el operador matemático que establece la relación entre la métrica y el valor del desencadenador.</span><span class="sxs-lookup"><span data-stu-id="28023-139">**Operator** is the mathematical operator that establishes the relationship between the metric and the trigger value.</span></span>
   * <span data-ttu-id="28023-140">**Trigger Value** (Valor de desencadenador) es el valor de umbral que debe cumplirse para enviarse una notificación.</span><span class="sxs-lookup"><span data-stu-id="28023-140">**Trigger Value** is the threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="28023-141">En el ejemplo siguiente, la expresión creada indica el deseo de recibir notificación cuando el número de códigos de estado 404 es superior a 25.</span><span class="sxs-lookup"><span data-stu-id="28023-141">In the below example, the expression I have created indicates that I would like to be notified when the number of 404 status codes is greater than 25.</span></span>
     
     ![Expresión de ejemplo de alerta en tiempo real](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="28023-143">En **Interval**(Intervalo), especifique la frecuencia con que desea que se evalúe la expresión.</span><span class="sxs-lookup"><span data-stu-id="28023-143">For **Interval**, enter how frequently you would like the expression evaluated.</span></span>
10. <span data-ttu-id="28023-144">En la lista desplegable **Notify on** (Notificar el), seleccione si desea recibir una notificación cuando la expresión sea verdadera.</span><span class="sxs-lookup"><span data-stu-id="28023-144">In the **Notify on** dropdown, select when you would like to be notified when the expression is true.</span></span>
    
    * <span data-ttu-id="28023-145">**Condition Start** (Inicio de condición) indica que se enviará una notificación la primera vez que se detecte la condición especificada.</span><span class="sxs-lookup"><span data-stu-id="28023-145">**Condition Start** indicates that a notification will be sent when the specified condition is first detected.</span></span>
    * <span data-ttu-id="28023-146">**Condition End** (Fin de condición) indica que se enviará una notificación cuando la condición especificada deje de detectarse.</span><span class="sxs-lookup"><span data-stu-id="28023-146">**Condition End** indicates that a notification will be sent when the specified condition is no longer detected.</span></span> <span data-ttu-id="28023-147">Esta notificación solo se puede desencadenar después de que nuestro sistema de supervisión de red detecta que se ha producido el problema especificado.</span><span class="sxs-lookup"><span data-stu-id="28023-147">This notification can only be triggered after our network monitoring system detected that the specified condition occurred.</span></span>
    * <span data-ttu-id="28023-148">**Continuous** (Continuo) indica que se enviará una notificación cada vez que el sistema de supervisión de red detecte el problema especificado.</span><span class="sxs-lookup"><span data-stu-id="28023-148">**Continuous** indicates that a notification will be sent each time that the network monitoring system detects the specified condition.</span></span> <span data-ttu-id="28023-149">Tenga en cuenta que el sistema de supervisión de red solo comprobará una vez por intervalo si existe el problema especificado.</span><span class="sxs-lookup"><span data-stu-id="28023-149">Keep in mind that the network monitoring system will only check once per interval for the specified condition.</span></span>
    * <span data-ttu-id="28023-150">**Condition Start and End** (Inicio y fin de condición) indica que se enviará una notificación la primera vez que se detecte el problema especificado y se volverá a enviar cuando deje de detectarse.</span><span class="sxs-lookup"><span data-stu-id="28023-150">**Condition Start and End** indicates that a notification will be sent the first time that the specified condition is detected and once again when the condition is no longer detected.</span></span>
11. <span data-ttu-id="28023-151">Si desea recibir notificaciones por correo electrónico, active la casilla **Notify by Email** (Notificar por correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="28023-151">If you want to receive notifications by email, check the **Notify by Email** checkbox.</span></span>  
    
    ![Formulario de notificación por correo electrónico](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="28023-153">En el campo **To** (Para), escriba la dirección de correo electrónico a la que desea que se envíen las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="28023-153">In the **To** field, enter the email address you where you want notifications sent.</span></span> <span data-ttu-id="28023-154">En **Subject** (Asunto) y **Body** (Cuerpo) puede dejar los valores predeterminados o puede personalizar el mensaje con la lista **Available keywords** (Palabras clave disponibles) para insertar de forma dinámica los datos de las alertas al enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="28023-154">For **Subject** and **Body**, you may leave the default, or you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="28023-155">Para probar la notificación que se va a enviar por correo electrónico, haga clic en el botón **Test Notification** (Probar notificación), pero solo después de que la configuración de alertas se haya guardado.</span><span class="sxs-lookup"><span data-stu-id="28023-155">You can test the email notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="28023-156">Si desea que las notificaciones se publique en un servidor web, active la casilla **Notify by HTTP Post** (Notificar mediante HTTP Post).</span><span class="sxs-lookup"><span data-stu-id="28023-156">If you want notifications to be posted to a web server, check the **Notify by HTTP Post** checkbox.</span></span>
    
    ![Formulario de notificación de HTTP Post](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="28023-158">En el campo **Url** , escriba la dirección URL en que desea que se publique el mensaje HTTP.</span><span class="sxs-lookup"><span data-stu-id="28023-158">In the **Url** field, enter the URL you where you want the HTTP message posted.</span></span> <span data-ttu-id="28023-159">En el cuadro de texto **Headers** (Encabezados), escriba los encabezados HTTP que se enviarán en la solicitud.</span><span class="sxs-lookup"><span data-stu-id="28023-159">In the **Headers** textbox, enter the HTTP headers to be sent in the request.</span></span>  <span data-ttu-id="28023-160">En **Body** (Cuerpo) puede personalizar el mensaje con la lista **Available keywords** (Palabras clave disponibles) para insertar de forma dinámica los datos de las alertas al enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="28023-160">For **Body** you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>  <span data-ttu-id="28023-161">Los valores predeterminados de **Headers** (Encabezados) y **Body** (Cuerpo) son una carga XML similar a la del ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="28023-161">**Headers** and **Body** default to an XML payload similar to the below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="28023-162">Para probar la notificación mediante HTTP Post, haga clic en el botón **Test Notification** (Probar notificación), pero solo después de que la configuración de alertas se haya guardado.</span><span class="sxs-lookup"><span data-stu-id="28023-162">You can test the HTTP Post notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="28023-163">Haga clic en el botón **Save** (Guardar) la configuración de las alertas.</span><span class="sxs-lookup"><span data-stu-id="28023-163">Click the **Save** button to save your alert configuration.</span></span>  <span data-ttu-id="28023-164">Si activó **Alert Enabled** (Alerta habilitada) en el paso 5, la alerta ya está activa.</span><span class="sxs-lookup"><span data-stu-id="28023-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28023-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="28023-165">Next Steps</span></span>
* <span data-ttu-id="28023-166">Análisis de [estadísticas en tiempo real en la CDN de Microsoft Azure](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="28023-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="28023-167">Mayor profundización con [Informes de HTTP avanzados en la red CDN de Microsoft Azure](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="28023-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="28023-168">Analizar [patrones de uso](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="28023-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

