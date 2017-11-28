---
title: aaaCreate una regla personalizada en el conjunto de IoT de Azure | Documentos de Microsoft
description: "¿Cómo toocreate una regla personalizada en un conjunto de IoT había preconfigurado solución."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 6c5bb2ca54f3f17b99ad482e727c8e9fa28d7fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="f63ee-103">Crear una regla personalizada en hello solución preconfigurada de supervisión remota</span><span class="sxs-lookup"><span data-stu-id="f63ee-103">Create a custom rule in hello remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="f63ee-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="f63ee-104">Introduction</span></span>

<span data-ttu-id="f63ee-105">En las soluciones de hello preconfigurado, puede configurar [las reglas que activan cuando una telemetría valor para un dispositivo alcanza un umbral específico][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="f63ee-105">In hello preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="f63ee-106">[Use la telemetría dinámica con hello solución preconfigurada de supervisión remota] [ lnk-dynamic-telemetry] describe cómo puede agregar valores de telemetría personalizada, como *ExternalTemperature* tooyour solución.</span><span class="sxs-lookup"><span data-stu-id="f63ee-106">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* tooyour solution.</span></span> <span data-ttu-id="f63ee-107">Este artículo muestra cómo toocreate regla personalizada para telemetría dinámica de los tipos de la solución.</span><span class="sxs-lookup"><span data-stu-id="f63ee-107">This article shows you how toocreate custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="f63ee-108">Este tutorial usa un simple Node.js dispositivo simulado toogenerate telemetría dinámica toosend toohello solución preconfigurada back-end.</span><span class="sxs-lookup"><span data-stu-id="f63ee-108">This tutorial uses a simple Node.js simulated device toogenerate dynamic telemetry toosend toohello preconfigured solution back end.</span></span> <span data-ttu-id="f63ee-109">A continuación, agregará reglas personalizadas en hello **RemoteMonitoring** solución de Visual Studio e implementar este tooyour de back-end personalizada suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f63ee-109">You then add custom rules in hello **RemoteMonitoring** Visual Studio solution and deploy this customized back end tooyour Azure subscription.</span></span>

<span data-ttu-id="f63ee-110">toocomplete este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="f63ee-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="f63ee-111">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="f63ee-111">An active Azure subscription.</span></span> <span data-ttu-id="f63ee-112">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="f63ee-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f63ee-113">Para más información, consulte la [evaluación gratuita de Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="f63ee-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="f63ee-114">[Node.js] [ lnk-node] versión 0.12.x o posterior toocreate un dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="f63ee-114">[Node.js][lnk-node] version 0.12.x or later toocreate a simulated device.</span></span>
* <span data-ttu-id="f63ee-115">Visual Studio 2015 o Visual Studio de 2017 toomodify Hola preconfigurado solución volver terminar con las nuevas reglas.</span><span class="sxs-lookup"><span data-stu-id="f63ee-115">Visual Studio 2015 or Visual Studio 2017 toomodify hello preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="f63ee-116">Tome nota del nombre de la solución de Hola que eligió para su implementación.</span><span class="sxs-lookup"><span data-stu-id="f63ee-116">Make a note of hello solution name you chose for your deployment.</span></span> <span data-ttu-id="f63ee-117">Necesitará el nombre de esta solución más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="f63ee-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="f63ee-118">Puede detener la aplicación de consola de hello Node.js cuando haya comprobado que está enviando **ExternalTemperature** toohello de telemetría preconfigurado solución.</span><span class="sxs-lookup"><span data-stu-id="f63ee-118">You can stop hello Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry toohello preconfigured solution.</span></span> <span data-ttu-id="f63ee-119">Mantenga la ventana de la consola de hello abierta porque esta aplicación de consola Node.js vuelva a ejecutar después de Agregar solución toohello de hello regla personalizada.</span><span class="sxs-lookup"><span data-stu-id="f63ee-119">Keep hello console window open because you run this Node.js console app again after you add hello custom rule toohello solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="f63ee-120">Ubicaciones de almacenamiento de las reglas</span><span class="sxs-lookup"><span data-stu-id="f63ee-120">Rule storage locations</span></span>

<span data-ttu-id="f63ee-121">La información sobre las reglas se mantiene en dos ubicaciones:</span><span class="sxs-lookup"><span data-stu-id="f63ee-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="f63ee-122">**DeviceRulesNormalizedTable** : esta tabla almacena un normalizado hacen referencia a las reglas de toohello definidas por el portal de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="f63ee-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference toohello rules defined by hello solution portal.</span></span> <span data-ttu-id="f63ee-123">Cuando el portal de solución de hello muestra reglas de dispositivos, consulta esta tabla para las definiciones de reglas de Hola.</span><span class="sxs-lookup"><span data-stu-id="f63ee-123">When hello solution portal displays device rules, it queries this table for hello rule definitions.</span></span>
* <span data-ttu-id="f63ee-124">**DeviceRules** blob – este blob almacena todas las reglas de hello definidas para todos los dispositivos registrados y se define como un trabajos de análisis de transmisiones de Azure toohello entrada de referencia.</span><span class="sxs-lookup"><span data-stu-id="f63ee-124">**DeviceRules** blob – This blob stores all hello rules defined for all registered devices and is defined as a reference input toohello Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="f63ee-125">Al actualizar una regla existente o definir una nueva regla en el portal de solución de hello, tabla hello y blob son cambios de hello tooreflect actualizada.</span><span class="sxs-lookup"><span data-stu-id="f63ee-125">When you update an existing rule or define a new rule in hello solution portal, both hello table and blob are updated tooreflect hello changes.</span></span> <span data-ttu-id="f63ee-126">regla Hola definición se muestra en el portal de hello procede del almacén de tablas de Hola y regla Hola definición hace referencia a trabajos de análisis de transmisiones de hello procede de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="f63ee-126">hello rule definition displayed in hello portal comes from hello table store, and hello rule definition referenced by hello Stream Analytics jobs comes from hello blob.</span></span> 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="f63ee-127">Actualizar soluciones de Visual Studio de RemoteMonitoring Hola</span><span class="sxs-lookup"><span data-stu-id="f63ee-127">Update hello RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="f63ee-128">Hello pasos siguientes muestran cómo toomodify Hola tooinclude de solución de Visual Studio de RemoteMonitoring una nueva regla que utilice hello **ExternalTemperature** telemetría enviado desde dispositivo simulado de hello:</span><span class="sxs-lookup"><span data-stu-id="f63ee-128">hello following steps show you how toomodify hello RemoteMonitoring Visual Studio solution tooinclude a new rule that uses hello **ExternalTemperature** telemetry sent from hello simulated device:</span></span>

1. <span data-ttu-id="f63ee-129">Si se ha no lo ha hecho, Hola clon **-iot-remoto-supervisión de azure** ubicación adecuada del repositorio tooa en el equipo local mediante el siguiente comando de Git de hello:</span><span class="sxs-lookup"><span data-stu-id="f63ee-129">If you have not already done so, clone hello **azure-iot-remote-monitoring** repository tooa suitable location on your local machine using hello following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="f63ee-130">En Visual Studio, abra el archivo de RemoteMonitoring.sln de Hola desde su copia local de hello **-iot-remoto-supervisión de azure** repositorio.</span><span class="sxs-lookup"><span data-stu-id="f63ee-130">In Visual Studio, open hello RemoteMonitoring.sln file from your local copy of hello **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="f63ee-131">Abra el archivo hello Infrastructure\Models\DeviceRuleBlobEntity.cs y agregue un **ExternalTemperature** propiedad tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="f63ee-131">Open hello file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="f63ee-132">En el mismo archivo de Hola, agregar un **ExternalTemperatureRuleOutput** propiedad tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="f63ee-132">In hello same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="f63ee-133">Abra el archivo hello Infrastructure\Models\DeviceRuleDataFields.cs y agregue Hola siguiente **ExternalTemperature** propiedad después de hello existente **humedad** propiedad:</span><span class="sxs-lookup"><span data-stu-id="f63ee-133">Open hello file Infrastructure\Models\DeviceRuleDataFields.cs and add hello following **ExternalTemperature** property after hello existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="f63ee-134">Hola mismo archivo en la consulta, actualizar hello **_availableDataFields** método tooinclude **ExternalTemperature** como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="f63ee-134">In hello same file, update hello **_availableDataFields** method tooinclude **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="f63ee-135">Abra el archivo hello Infrastructure\Repository\DeviceRulesRepository.cs y modificar hello **BuildBlobEntityListFromTableRows** método tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="f63ee-135">Open hello file Infrastructure\Repository\DeviceRulesRepository.cs and modify hello **BuildBlobEntityListFromTableRows** method as follows:</span></span>

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-hello-solution"></a><span data-ttu-id="f63ee-136">Volver a generar e implementar soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="f63ee-136">Rebuild and redeploy hello solution.</span></span>

<span data-ttu-id="f63ee-137">Ahora puede implementar Hola Actualizar solución tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f63ee-137">You can now deploy hello updated solution tooyour Azure subscription.</span></span>

1. <span data-ttu-id="f63ee-138">Abra un símbolo del sistema con privilegios elevados y vaya toohello raíz de una copia local del repositorio de hello-iot-remoto-supervisión de azure.</span><span class="sxs-lookup"><span data-stu-id="f63ee-138">Open an elevated command prompt and navigate toohello root of your local copy of hello azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="f63ee-139">toodeploy la solución actualizada, ejecute hello después de sustituir el comando **{nombre de la implementación}** con nombre de saludo de la implementación de soluciones preconfiguradas que se ha indicado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="f63ee-139">toodeploy your updated solution, run hello following command substituting **{deployment name}** with hello name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a><span data-ttu-id="f63ee-140">Actualizar el trabajo de análisis de transmisiones de Hola</span><span class="sxs-lookup"><span data-stu-id="f63ee-140">Update hello Stream Analytics job</span></span>

<span data-ttu-id="f63ee-141">Una vez completada la implementación de hello, puede actualizar Hola análisis de transmisiones toouse Hola nueva regla definiciones de trabajos.</span><span class="sxs-lookup"><span data-stu-id="f63ee-141">When hello deployment is complete, you can update hello Stream Analytics job toouse hello new rule definitions.</span></span>

1. <span data-ttu-id="f63ee-142">Hola portal de Azure, navegue toohello grupo de recursos que contiene los recursos de la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="f63ee-142">In hello Azure portal, navigate toohello resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="f63ee-143">Este grupo de recursos tiene Hola mismo nombre que especificó para Hola solución durante la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f63ee-143">This resource group has hello same name you specified for hello solution during hello deployment.</span></span>

2. <span data-ttu-id="f63ee-144">Navegue toohello {nombre de la implementación}-trabajo de análisis de transmisiones de reglas.</span><span class="sxs-lookup"><span data-stu-id="f63ee-144">Navigate toohello {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="f63ee-145">Haga clic en **detener** trabajo de análisis de transmisiones de hello toostop de ejecución.</span><span class="sxs-lookup"><span data-stu-id="f63ee-145">Click **Stop** toostop hello Stream Analytics job from running.</span></span> <span data-ttu-id="f63ee-146">(Se debe esperar a hello toostop de trabajo de streaming antes de poder editar consulta hello).</span><span class="sxs-lookup"><span data-stu-id="f63ee-146">(You must wait for hello streaming job toostop before you can edit hello query).</span></span>

4. <span data-ttu-id="f63ee-147">Haga clic en **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="f63ee-147">Click **Query**.</span></span> <span data-ttu-id="f63ee-148">Editar Hola de hello consulta tooinclude **seleccione** instrucción para **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="f63ee-148">Edit hello query tooinclude hello **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="f63ee-149">Hello en el ejemplo siguiente se muestra completo de la consulta Hola con hello nueva **seleccione** instrucción:</span><span class="sxs-lookup"><span data-stu-id="f63ee-149">hello following sample shows hello complete query with hello new **SELECT** statement:</span></span>

    ```
    WITH AlarmsData AS 
    (
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Temperature' as ReadingType,
         Stream.Temperature as Reading,
         Ref.Temperature as Threshold,
         Ref.TemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Humidity' as ReadingType,
         Stream.Humidity as Reading,
         Ref.Humidity as Threshold,
         Ref.HumidityRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. <span data-ttu-id="f63ee-150">Haga clic en **guardar** toochange Hola actualiza la consulta de la regla.</span><span class="sxs-lookup"><span data-stu-id="f63ee-150">Click **Save** toochange hello updated rule query.</span></span>

6. <span data-ttu-id="f63ee-151">Haga clic en **iniciar** trabajo de análisis de transmisiones de hello toostart ejecutar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="f63ee-151">Click **Start** toostart hello Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-hello-dashboard"></a><span data-ttu-id="f63ee-152">Agregar la nueva regla en el panel de Hola</span><span class="sxs-lookup"><span data-stu-id="f63ee-152">Add your new rule in hello dashboard</span></span>

<span data-ttu-id="f63ee-153">Ahora puede agregar hello **ExternalTemperature** dispositivo de tooa de regla en el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="f63ee-153">You can now add hello **ExternalTemperature** rule tooa device in hello solution dashboard.</span></span>

1. <span data-ttu-id="f63ee-154">Navegue toohello portal de solución.</span><span class="sxs-lookup"><span data-stu-id="f63ee-154">Navigate toohello solution portal.</span></span>

2. <span data-ttu-id="f63ee-155">Navegue toohello **dispositivos** panel.</span><span class="sxs-lookup"><span data-stu-id="f63ee-155">Navigate toohello **Devices** panel.</span></span>

3. <span data-ttu-id="f63ee-156">Busque Hola dispositivo personalizado que crea que envía **ExternalTemperature** telemetría y en hello **detalles del dispositivo** del panel, haga clic en **Agregar regla**.</span><span class="sxs-lookup"><span data-stu-id="f63ee-156">Locate hello custom device you created that sends **ExternalTemperature** telemetry and on hello **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="f63ee-157">Seleccione **ExternalTemperature** en **Campo de datos**.</span><span class="sxs-lookup"><span data-stu-id="f63ee-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="f63ee-158">Establecer **umbral** too56.</span><span class="sxs-lookup"><span data-stu-id="f63ee-158">Set **Threshold** too56.</span></span> <span data-ttu-id="f63ee-159">Luego, haga clic en **Guardar y ver reglas**.</span><span class="sxs-lookup"><span data-stu-id="f63ee-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="f63ee-160">Devuelve el historial de alarma de toohello panel tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="f63ee-160">Return toohello dashboard tooview hello alarm history.</span></span>

7. <span data-ttu-id="f63ee-161">En ventana de consola de Hola dejan abiertos, empezar a enviar de toobegin de aplicación de hello Node.js consola **ExternalTemperature** los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="f63ee-161">In hello console window you left open, start hello Node.js console app toobegin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="f63ee-162">Tenga en cuenta que hello **historial de alarma** tabla muestran alarmas nueva cuando se desencadene Hola nueva regla.</span><span class="sxs-lookup"><span data-stu-id="f63ee-162">Notice that hello **Alarm History** table shows new alarms when hello new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="f63ee-163">Información adicional</span><span class="sxs-lookup"><span data-stu-id="f63ee-163">Additional information</span></span>

<span data-ttu-id="f63ee-164">Cambiar operador hello  **>**  es más compleja y va más allá de los pasos de hello descritos en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f63ee-164">Changing hello operator **>** is more complex and goes beyond hello steps outlined in this tutorial.</span></span> <span data-ttu-id="f63ee-165">Aunque es posible cambiar toouse de trabajo de análisis de transmisiones de hello cualquier operador le gusta, reflejar ese operador en el portal de solución de hello es una tarea más compleja.</span><span class="sxs-lookup"><span data-stu-id="f63ee-165">While you can change hello Stream Analytics job toouse whatever operator you like, reflecting that operator in hello solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f63ee-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f63ee-166">Next steps</span></span>
<span data-ttu-id="f63ee-167">Ahora que ha visto cómo toocreate reglas personalizadas, puede obtener más información acerca de las soluciones de hello preconfigurado:</span><span class="sxs-lookup"><span data-stu-id="f63ee-167">Now that you've seen how toocreate custom rules, you can learn more about hello preconfigured solutions:</span></span>

- <span data-ttu-id="f63ee-168">[Solución de Azure de supervisión remota de conjunto de IoT preconfigurado tooyour de aplicación lógica de conexión][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="f63ee-168">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="f63ee-169">[Metadatos de información de dispositivo de supervisión remota de hello preconfigurado solución][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="f63ee-169">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md