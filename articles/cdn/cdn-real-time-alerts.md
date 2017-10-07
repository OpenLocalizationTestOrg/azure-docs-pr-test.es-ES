---
title: alertas en tiempo real de aaaAzure CDN | Documentos de Microsoft
description: Alertas en tiempo real en la red CDN de Microsoft Azure. Alertas en tiempo real proporcionan notificaciones sobre el rendimiento de Hola de extremos de hello en el perfil de CDN.
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
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="f9a11-104">Alertas en tiempo real en la red CDN de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f9a11-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="f9a11-105">Información general</span><span class="sxs-lookup"><span data-stu-id="f9a11-105">Overview</span></span>
<span data-ttu-id="f9a11-106">En este documento se explican las alertas en tiempo real en la red CDN de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f9a11-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="f9a11-107">Esta funcionalidad proporciona notificaciones en tiempo real sobre el rendimiento de Hola de extremos de hello en el perfil de CDN.</span><span class="sxs-lookup"><span data-stu-id="f9a11-107">This functionality provides real-time notifications about hello performance of hello endpoints in your CDN profile.</span></span>  <span data-ttu-id="f9a11-108">Las alertas de correo o de HTTP se pueden configurar por:</span><span class="sxs-lookup"><span data-stu-id="f9a11-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="f9a11-109">Ancho de banda</span><span class="sxs-lookup"><span data-stu-id="f9a11-109">Bandwidth</span></span>
* <span data-ttu-id="f9a11-110">Códigos de estado</span><span class="sxs-lookup"><span data-stu-id="f9a11-110">Status Codes</span></span>
* <span data-ttu-id="f9a11-111">Estados de la memoria caché</span><span class="sxs-lookup"><span data-stu-id="f9a11-111">Cache Statuses</span></span>
* <span data-ttu-id="f9a11-112">Conexiones</span><span class="sxs-lookup"><span data-stu-id="f9a11-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="f9a11-113">Creación de una alerta en tiempo real</span><span class="sxs-lookup"><span data-stu-id="f9a11-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="f9a11-114">Hola [Portal de Azure](https://portal.azure.com), examinar el perfil de CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="f9a11-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![Hoja del perfil de red CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="f9a11-116">En la hoja de perfil CDN Hola, haga clic en hello **administrar** botón.</span><span class="sxs-lookup"><span data-stu-id="f9a11-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="f9a11-118">se abre el portal de administración de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="f9a11-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="f9a11-119">Mantenga el mouse sobre hello **análisis** ficha y, a continuación, mantenga el mouse sobre hello **estadísticas en tiempo real** ventana flotante.</span><span class="sxs-lookup"><span data-stu-id="f9a11-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="f9a11-120">Haga clic en **Real-Time Alerts**(Alertas en tiempo real).</span><span class="sxs-lookup"><span data-stu-id="f9a11-120">Click on **Real-Time Alerts**.</span></span>
   
    ![Portal de administración de la red CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="f9a11-122">se muestra la lista de Hola de las configuraciones de alerta existentes (si existe).</span><span class="sxs-lookup"><span data-stu-id="f9a11-122">hello list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="f9a11-123">Haga clic en hello **Agregar alerta** botón.</span><span class="sxs-lookup"><span data-stu-id="f9a11-123">Click hello **Add Alert** button.</span></span>
   
    ![Botón Add Alert (Agregar alerta)](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="f9a11-125">Se muestra un formulario para crear una alerta nueva.</span><span class="sxs-lookup"><span data-stu-id="f9a11-125">A form for creating a new alert is displayed.</span></span>
   
    ![Formulario de alerta nueva](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="f9a11-127">Si desea que esta alerta toobe activa al hacer clic en **guardar**, comprobar hello **alerta habilitada** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="f9a11-127">If you want this alert toobe active when you click **Save**, check hello **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="f9a11-128">Escriba un nombre descriptivo para la alerta en hello **nombre** campo.</span><span class="sxs-lookup"><span data-stu-id="f9a11-128">Enter a descriptive name for your alert in hello **Name** field.</span></span>
7. <span data-ttu-id="f9a11-129">Hola **tipo de medio** lista desplegable, seleccione **objetos grandes de HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f9a11-129">In hello **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![Tipo de medio con objetos HTTP grande seleccionado](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="f9a11-131">Debe seleccionar **objetos grandes de HTTP** como hello **tipo de medio**.</span><span class="sxs-lookup"><span data-stu-id="f9a11-131">You must select **HTTP Large Object** as hello **Media Type**.</span></span>  <span data-ttu-id="f9a11-132">Hello otras opciones no se usan por **CDN de Azure de Verizon**.</span><span class="sxs-lookup"><span data-stu-id="f9a11-132">hello other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="f9a11-133">Error tooselect **objetos grandes de HTTP** hará que la alerta se desencadena toonever.</span><span class="sxs-lookup"><span data-stu-id="f9a11-133">Failure tooselect **HTTP Large Object** will cause your alert toonever be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="f9a11-134">Crear un **expresión** toomonitor seleccionando un **métrica**, **operador**, y **desencadenar valor**.</span><span class="sxs-lookup"><span data-stu-id="f9a11-134">Create an **Expression** toomonitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="f9a11-135">Para **métrica**, seleccione tipo hello de condición que desee supervisar.</span><span class="sxs-lookup"><span data-stu-id="f9a11-135">For **Metric**, select hello type of condition you want monitored.</span></span>  <span data-ttu-id="f9a11-136">**Mbps de ancho de banda** es la cantidad de Hola de uso de ancho de banda en megabits por segundo.</span><span class="sxs-lookup"><span data-stu-id="f9a11-136">**Bandwidth Mbps** is hello amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="f9a11-137">**Total de conexiones** es número de Hola de tooour de conexiones HTTP simultánea servidores perimetrales.</span><span class="sxs-lookup"><span data-stu-id="f9a11-137">**Total Connections** is hello number of concurrent HTTP connections tooour edge servers.</span></span>  <span data-ttu-id="f9a11-138">Para obtener definiciones de saludo diversos estados de memoria caché y códigos de estado, consulte [códigos de estado de memoria caché de CDN de Azure](https://msdn.microsoft.com/library/mt759237.aspx) y [códigos de estado de HTTP de CDN de Azure](https://msdn.microsoft.com/library/mt759238.aspx)</span><span class="sxs-lookup"><span data-stu-id="f9a11-138">For definitions of hello various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="f9a11-139">**Operador** es Hola operador matemático que establece Hola relación entre la métrica de Hola y el valor de desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9a11-139">**Operator** is hello mathematical operator that establishes hello relationship between hello metric and hello trigger value.</span></span>
   * <span data-ttu-id="f9a11-140">**Desencadenar valor** es el valor de umbral de Hola que debe cumplirse antes de que se enviará una notificación de.</span><span class="sxs-lookup"><span data-stu-id="f9a11-140">**Trigger Value** is hello threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="f9a11-141">Hola ejemplo siguiente, expresión Hola que se crearon indica que me gustaría toobe una notificación cuando el número de hello 404 códigos de estado es mayor que 25.</span><span class="sxs-lookup"><span data-stu-id="f9a11-141">In hello below example, hello expression I have created indicates that I would like toobe notified when hello number of 404 status codes is greater than 25.</span></span>
     
     ![Expresión de ejemplo de alerta en tiempo real](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="f9a11-143">Para **intervalo**, escriba la frecuencia con que desea que la expresión Hola evaluada.</span><span class="sxs-lookup"><span data-stu-id="f9a11-143">For **Interval**, enter how frequently you would like hello expression evaluated.</span></span>
10. <span data-ttu-id="f9a11-144">Hola **que se notifique** lista desplegable, seleccione cuándo desea toobe una notificación cuando hello expresión es verdadera.</span><span class="sxs-lookup"><span data-stu-id="f9a11-144">In hello **Notify on** dropdown, select when you would like toobe notified when hello expression is true.</span></span>
    
    * <span data-ttu-id="f9a11-145">**Condición de inicio** indica que se enviará una notificación cuando Hola especifica primero se detecta la condición.</span><span class="sxs-lookup"><span data-stu-id="f9a11-145">**Condition Start** indicates that a notification will be sent when hello specified condition is first detected.</span></span>
    * <span data-ttu-id="f9a11-146">**Condición final** indica que se enviará una notificación cuando Hola especificado ya no se detecta la condición.</span><span class="sxs-lookup"><span data-stu-id="f9a11-146">**Condition End** indicates that a notification will be sent when hello specified condition is no longer detected.</span></span> <span data-ttu-id="f9a11-147">Solo se puede desencadenar esta notificación después de nuestro sistema de supervisión de red ha detectado que Hola especificado insuficiente.</span><span class="sxs-lookup"><span data-stu-id="f9a11-147">This notification can only be triggered after our network monitoring system detected that hello specified condition occurred.</span></span>
    * <span data-ttu-id="f9a11-148">**Continuo** indica que se enviará una notificación cada vez que Hola sistema de supervisión de red detecta Hola especificada condición.</span><span class="sxs-lookup"><span data-stu-id="f9a11-148">**Continuous** indicates that a notification will be sent each time that hello network monitoring system detects hello specified condition.</span></span> <span data-ttu-id="f9a11-149">Tenga en cuenta esa red Hola supervisión sistema sólo comprobación de una vez por intervalo de hello condición especificada.</span><span class="sxs-lookup"><span data-stu-id="f9a11-149">Keep in mind that hello network monitoring system will only check once per interval for hello specified condition.</span></span>
    * <span data-ttu-id="f9a11-150">**Condición inicial y final** indica que se enviará una notificación Hola se detecta la primera vez que Hola condición especificada y una vez más cuando se detecta ya no es la condición de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9a11-150">**Condition Start and End** indicates that a notification will be sent hello first time that hello specified condition is detected and once again when hello condition is no longer detected.</span></span>
11. <span data-ttu-id="f9a11-151">Si desea tooreceive notificaciones por correo electrónico, active hello **notificar por correo electrónico** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="f9a11-151">If you want tooreceive notifications by email, check hello **Notify by Email** checkbox.</span></span>  
    
    ![Formulario de notificación por correo electrónico](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="f9a11-153">Hola **a** , escriba la dirección de correo electrónico de Hola donde desea que las notificaciones envió.</span><span class="sxs-lookup"><span data-stu-id="f9a11-153">In hello **To** field, enter hello email address you where you want notifications sent.</span></span> <span data-ttu-id="f9a11-154">Para **asunto** y **cuerpo**, puede dejar predeterminado de Hola o sólo puede personalizar el mensaje de Hola mediante hello **palabras clave disponibles** lista toodynamically insertar datos de alertas cuando se envía el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="f9a11-154">For **Subject** and **Body**, you may leave hello default, or you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="f9a11-155">Puede probar la notificación por correo electrónico de hello haciendo clic en hello **notificación de prueba** button, pero solo después de que se ha guardado la configuración de alertas de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9a11-155">You can test hello email notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="f9a11-156">Si desea que registra el servidor web de tooa de toobe de notificaciones, compruebe hello **notificar mediante HTTP Post** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="f9a11-156">If you want notifications toobe posted tooa web server, check hello **Notify by HTTP Post** checkbox.</span></span>
    
    ![Formulario de notificación de HTTP Post](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="f9a11-158">Hola **dirección Url** , escriba la dirección URL de hello, donde desea que el mensaje de bienvenida HTTP publica.</span><span class="sxs-lookup"><span data-stu-id="f9a11-158">In hello **Url** field, enter hello URL you where you want hello HTTP message posted.</span></span> <span data-ttu-id="f9a11-159">Hola **encabezados** cuadro de texto, escriba Hola HTTP encabezados toobe enviado en la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="f9a11-159">In hello **Headers** textbox, enter hello HTTP headers toobe sent in hello request.</span></span>  <span data-ttu-id="f9a11-160">Para **cuerpo** sólo puede personalizar el mensaje de Hola mediante hello **palabras clave disponibles** lista toodynamically insertar datos de alertas cuando se envía el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="f9a11-160">For **Body** you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>  <span data-ttu-id="f9a11-161">**Encabezados de** y **cuerpo** predeterminado tooan XML carga similar toohello ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="f9a11-161">**Headers** and **Body** default tooan XML payload similar toohello below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="f9a11-162">Puede probar Hola notificación HTTP Post haciendo clic en hello **notificación de prueba** button, pero solo después de que se ha guardado la configuración de alertas de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9a11-162">You can test hello HTTP Post notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="f9a11-163">Haga clic en hello **guardar** botón toosave la configuración de alertas.</span><span class="sxs-lookup"><span data-stu-id="f9a11-163">Click hello **Save** button toosave your alert configuration.</span></span>  <span data-ttu-id="f9a11-164">Si activó **Alert Enabled** (Alerta habilitada) en el paso 5, la alerta ya está activa.</span><span class="sxs-lookup"><span data-stu-id="f9a11-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9a11-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f9a11-165">Next Steps</span></span>
* <span data-ttu-id="f9a11-166">Análisis de [estadísticas en tiempo real en la CDN de Microsoft Azure](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="f9a11-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="f9a11-167">Mayor profundización con [Informes de HTTP avanzados en la red CDN de Microsoft Azure](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="f9a11-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="f9a11-168">Analizar [patrones de uso](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="f9a11-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

