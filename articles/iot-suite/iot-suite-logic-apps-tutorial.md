---
title: aaaAzure IoT Suite y Logic Apps | Documentos de Microsoft
description: "Ver un tutorial sobre cómo toohook seguridad Logic Apps tooAzure IoT conjunto para el proceso empresarial."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="d81b0-103">Tutorial: Conectar la solución de aplicación lógica tooyour Azure de supervisión remota de conjunto de IoT preconfigurado</span><span class="sxs-lookup"><span data-stu-id="d81b0-103">Tutorial: Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="d81b0-104">Hola [Microsoft Azure IoT Suite] [ lnk-internetofthings] solución preconfigurada de supervisión remota es una excelente manera tooget a trabajar rápidamente con un conjunto de características de-to-end que ejemplifica una solución de IoT.</span><span class="sxs-lookup"><span data-stu-id="d81b0-104">hello [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way tooget started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="d81b0-105">Este tutorial le guía a través de la supervisión remota de tooadd aplicación lógica tooyour Microsoft Azure IoT Suite había preconfigurado solución.</span><span class="sxs-lookup"><span data-stu-id="d81b0-105">This tutorial walks you through how tooadd Logic App tooyour Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="d81b0-106">Estos pasos muestran cómo puede aprovechar aún más la solución de IoT conectándola tooa proceso de negocio.</span><span class="sxs-lookup"><span data-stu-id="d81b0-106">These steps demonstrate how you can take your IoT solution even further by connecting it tooa business process.</span></span>

<span data-ttu-id="d81b0-107">*Si está pensando para ver un tutorial sobre cómo tooprovision una supervisión remota preconfigurado solución, consulte [Tutorial: Introducción a soluciones de IoT preconfigurado hello][lnk-getstarted].*</span><span class="sxs-lookup"><span data-stu-id="d81b0-107">*If you’re looking for a walkthrough on how tooprovision a remote monitoring preconfigured solution, see [Tutorial: Get started with hello IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="d81b0-108">Antes de comenzar este tutorial, debe:</span><span class="sxs-lookup"><span data-stu-id="d81b0-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="d81b0-109">Hola de aprovisionar solución preconfigurada en su suscripción de Azure de supervisión remoto.</span><span class="sxs-lookup"><span data-stu-id="d81b0-109">Provision hello remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="d81b0-110">Crear un tooenable de cuenta de SendGrid toosend un correo electrónico que desencadena el proceso empresarial.</span><span class="sxs-lookup"><span data-stu-id="d81b0-110">Create a SendGrid account tooenable you toosend an email that triggers your business process.</span></span> <span data-ttu-id="d81b0-111">Puede registrarse para obtener una cuenta de evaluación gratuita en [SendGrid](https://sendgrid.com/) haciendo clic en **Try for Free**(Probar gratis).</span><span class="sxs-lookup"><span data-stu-id="d81b0-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="d81b0-112">Después de haber registrado para su cuenta de evaluación gratuita, debe toocreate una [clave de API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) en SendGrid que concede permisos toosend correo.</span><span class="sxs-lookup"><span data-stu-id="d81b0-112">After you have registered for your free trial account, you need toocreate an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions toosend mail.</span></span> <span data-ttu-id="d81b0-113">Se necesita esta clave API más adelante en el tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="d81b0-113">You need this API key later in hello tutorial.</span></span>

<span data-ttu-id="d81b0-114">toocomplete este tutorial, necesita Visual Studio 2015 o Visual Studio de 2017 acciones de hello toomodify en hello solución preconfigurada back-end.</span><span class="sxs-lookup"><span data-stu-id="d81b0-114">toocomplete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 toomodify hello actions in hello preconfigured solution back end.</span></span>

<span data-ttu-id="d81b0-115">Suponiendo que ya se ha aprovisionado la supervisión remota preconfigurado solución, vaya toohello el grupo de recursos para esa solución Hola [portal de Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="d81b0-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate toohello resource group for that solution in hello [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="d81b0-116">grupo de recursos de Hello tiene Hola mismo nombre como hello solución el nombre eligió al aprovisionar la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="d81b0-116">hello resource group has hello same name as hello solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="d81b0-117">En el grupo de recursos de hello, puede ver aprovisionado de hello todos los recursos de Azure para su solución excepto Hola aplicación de Azure Active Directory que se puede encontrar en hello Portal clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="d81b0-117">In hello resource group, you can see all hello provisioned Azure resources for your solution except for hello Azure Active Directory application that you can find in hello Azure Classic Portal.</span></span> <span data-ttu-id="d81b0-118">Hello captura de pantalla siguiente muestra un ejemplo **grupo de recursos** hoja para una supervisión remota preconfigurado soluciones:</span><span class="sxs-lookup"><span data-stu-id="d81b0-118">hello following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="d81b0-119">toobegin, configurar toouse de aplicación lógica de hello con hello preconfigurado solución.</span><span class="sxs-lookup"><span data-stu-id="d81b0-119">toobegin, set up hello logic app toouse with hello preconfigured solution.</span></span>

## <a name="set-up-hello-logic-app"></a><span data-ttu-id="d81b0-120">Configurar la aplicación lógica de Hola</span><span class="sxs-lookup"><span data-stu-id="d81b0-120">Set up hello Logic App</span></span>
1. <span data-ttu-id="d81b0-121">Haga clic en **agregar** en parte superior de saludo de la hoja de grupo de recursos en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d81b0-121">Click **Add** at hello top of your resource group blade in hello Azure portal.</span></span>
2. <span data-ttu-id="d81b0-122">Busque la **aplicación lógica**, selecciónela y, después, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d81b0-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="d81b0-123">Rellene hello **nombre** y use Hola mismo **suscripción** y **grupo de recursos** que usó al aprovisionar la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="d81b0-123">Fill out hello **Name** and use hello same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="d81b0-124">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d81b0-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="d81b0-125">Cuando se completa la implementación, puede ver Hola que lógica de aplicación se muestra como un recurso en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d81b0-125">When your deployment completes, you can see hello Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="d81b0-126">Haga clic en la hoja de aplicación lógica de toohello de toonavigate de aplicación lógica de hello, seleccione hello **en blanco de lógica de aplicación** Hola de plantilla tooopen **el Diseñador de aplicaciones de la lógica de**.</span><span class="sxs-lookup"><span data-stu-id="d81b0-126">Click hello Logic App toonavigate toohello Logic App blade, select hello **Blank Logic App** template tooopen hello **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="d81b0-127">Seleccione **Solicitud**.</span><span class="sxs-lookup"><span data-stu-id="d81b0-127">Select **Request**.</span></span> <span data-ttu-id="d81b0-128">Esta acción especifica que una solicitud HTTP entrante con una carga específica con formato de JSON actúa como desencadenador.</span><span class="sxs-lookup"><span data-stu-id="d81b0-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="d81b0-129">Pegue Hola siguiente código en hello esquema de JSON de cuerpo de solicitud:</span><span class="sxs-lookup"><span data-stu-id="d81b0-129">Paste hello following code into hello Request Body JSON Schema:</span></span>
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > <span data-ttu-id="d81b0-130">Puede copiar dirección URL de Hola de publicación de hello HTTP después de guardar aplicación lógica de hello, pero primero debe agregar una acción.</span><span class="sxs-lookup"><span data-stu-id="d81b0-130">You can copy hello URL for hello HTTP post after you save hello logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="d81b0-131">Haga clic en **+ Nuevo paso** en el desencadenador manual.</span><span class="sxs-lookup"><span data-stu-id="d81b0-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="d81b0-132">A continuación, haga clic en **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="d81b0-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="d81b0-133">Busque la opción **SendGrid - Send email** (SendGrid: enviar correo electrónico) y haga clic en ella.</span><span class="sxs-lookup"><span data-stu-id="d81b0-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="d81b0-134">Escriba un nombre para la conexión de hello, como **SendGridConnection**, escriba Hola **clave de API de SendGrid** que creó al configurar la cuenta de SendGrid y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="d81b0-134">Enter a name for hello connection, such as **SendGridConnection**, enter hello **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="d81b0-135">Agregar direcciones de correo electrónico tooboth propio hello **de** y **a** campos.</span><span class="sxs-lookup"><span data-stu-id="d81b0-135">Add email addresses you own tooboth hello **From** and **To** fields.</span></span> <span data-ttu-id="d81b0-136">Agregar **alerta de supervisión remota [DeviceId]** toohello **asunto** campo.</span><span class="sxs-lookup"><span data-stu-id="d81b0-136">Add **Remote monitoring alert [DeviceId]** toohello **Subject** field.</span></span> <span data-ttu-id="d81b0-137">Hola **cuerpo del correo electrónico** , a continuación, agregar **ha informado de dispositivo [DeviceId] [measurementName] con el valor [measuredValue].**</span><span class="sxs-lookup"><span data-stu-id="d81b0-137">In hello **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="d81b0-138">Puede agregar **[DeviceId]**, **[measurementName]**, y **[measuredValue]** haciendo clic en hello **puede insertar datos de los pasos anteriores**sección.</span><span class="sxs-lookup"><span data-stu-id="d81b0-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in hello **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="d81b0-139">Haga clic en **guardar** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="d81b0-139">Click **Save** in hello top menu.</span></span>
13. <span data-ttu-id="d81b0-140">Haga clic en hello **solicitar** desencadenador y copia hello **dirección URL de Http Post toothis** valor.</span><span class="sxs-lookup"><span data-stu-id="d81b0-140">Click hello **Request** trigger and copy hello **Http Post toothis URL** value.</span></span> <span data-ttu-id="d81b0-141">Necesitará esta URL más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="d81b0-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="d81b0-142">Las aplicaciones lógicas le permiten toorun [muchos tipos diferentes de acción] [ lnk-logic-apps-actions] incluidas acciones en Office 365.</span><span class="sxs-lookup"><span data-stu-id="d81b0-142">Logic Apps enable you toorun [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a><span data-ttu-id="d81b0-143">Configurar hello EventProcessor Web trabajo</span><span class="sxs-lookup"><span data-stu-id="d81b0-143">Set up hello EventProcessor Web Job</span></span>
<span data-ttu-id="d81b0-144">En esta sección, se conecta la aplicación lógica que creó toohello de solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="d81b0-144">In this section, you connect your preconfigured solution toohello Logic App you created.</span></span> <span data-ttu-id="d81b0-145">toocomplete esta tarea, agregará hello tootrigger Hola aplicación lógica toohello acción de dirección URL que se desencadena cuando un valor del sensor de dispositivo supera un umbral.</span><span class="sxs-lookup"><span data-stu-id="d81b0-145">toocomplete this task, you add hello URL tootrigger hello Logic App toohello action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="d81b0-146">Use la git tooclone Hola última versión del cliente de hello [azure iot-remoto-supervisión de repositorio de github][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="d81b0-146">Use your git client tooclone hello latest version of hello [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="d81b0-147">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d81b0-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="d81b0-148">En Visual Studio, abra hello **RemoteMonitoring.sln** desde la copia local de hello del repositorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d81b0-148">In Visual Studio, open hello **RemoteMonitoring.sln** from hello local copy of hello repository.</span></span>
3. <span data-ttu-id="d81b0-149">Abra hello **ActionRepository.cs** archivo Hola **infraestructura\\repositorio** carpeta.</span><span class="sxs-lookup"><span data-stu-id="d81b0-149">Open hello **ActionRepository.cs** file in hello **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="d81b0-150">Hola de actualización **actionIds** diccionario con hello **dirección URL de Http Post toothis** que anotó desde la aplicación lógica como sigue:</span><span class="sxs-lookup"><span data-stu-id="d81b0-150">Update hello **actionIds** dictionary with hello **Http Post toothis URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. <span data-ttu-id="d81b0-151">Guardar los cambios de hello en la solución y salga de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d81b0-151">Save hello changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-hello-command-line"></a><span data-ttu-id="d81b0-152">Implementar desde la línea de comandos de Hola</span><span class="sxs-lookup"><span data-stu-id="d81b0-152">Deploy from hello command line</span></span>
<span data-ttu-id="d81b0-153">En esta sección, se implementa la versión actualizada de hello supervisión solución tooreplace Hola versión remota está ejecutando actualmente en Azure.</span><span class="sxs-lookup"><span data-stu-id="d81b0-153">In this section, you deploy your updated version of hello remote monitoring solution tooreplace hello version currently running in Azure.</span></span>

1. <span data-ttu-id="d81b0-154">Después de hello [dev instalación] [ lnk-devsetup] tooset de instrucciones del entorno para la implementación.</span><span class="sxs-lookup"><span data-stu-id="d81b0-154">Following hello [dev set-up][lnk-devsetup] instructions tooset up your environment for deployment.</span></span>
2. <span data-ttu-id="d81b0-155">toodeploy localmente, siga hello [implementación local] [ lnk-localdeploy] instrucciones.</span><span class="sxs-lookup"><span data-stu-id="d81b0-155">toodeploy locally, follow hello [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="d81b0-156">toodeploy toohello en la nube y actualizar la implementación de nube existente, siga hello [implementación de nube] [ lnk-clouddeploy] instrucciones.</span><span class="sxs-lookup"><span data-stu-id="d81b0-156">toodeploy toohello cloud and update your existing cloud deployment, follow hello [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="d81b0-157">Usar el nombre de saludo de la implementación original como nombre de la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d81b0-157">Use hello name of your original deployment as hello deployment name.</span></span> <span data-ttu-id="d81b0-158">Por ejemplo, si se llamara a implementación original de hello **demologicapp**, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="d81b0-158">For example if hello original deployment was called **demologicapp**, use hello following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="d81b0-159">Cuando Hola compila el script se ejecuta, asegúrese de toouse Hola misma cuenta de Azure, suscripción, región e instancia de Active Directory que usó al aprovisionar solución Hola.</span><span class="sxs-lookup"><span data-stu-id="d81b0-159">When hello build script runs, be sure toouse hello same Azure account, subscription, region, and Active Directory instance you used when you provisioned hello solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="d81b0-160">La aplicación lógica en acción</span><span class="sxs-lookup"><span data-stu-id="d81b0-160">See your Logic App in action</span></span>
<span data-ttu-id="d81b0-161">Hola remoto solución preconfigurada de supervisión tiene dos reglas configuradas de forma predeterminada al aprovisionar una solución.</span><span class="sxs-lookup"><span data-stu-id="d81b0-161">hello remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="d81b0-162">Ambas reglas se encuentran en hello **SampleDevice001** dispositivo:</span><span class="sxs-lookup"><span data-stu-id="d81b0-162">Both rules are on hello **SampleDevice001** device:</span></span>

* <span data-ttu-id="d81b0-163">Temperature > 38.00 (Temperatura > 38,00)</span><span class="sxs-lookup"><span data-stu-id="d81b0-163">Temperature > 38.00</span></span>
* <span data-ttu-id="d81b0-164">Humidity > 48.00 (Humedad > 48,00)</span><span class="sxs-lookup"><span data-stu-id="d81b0-164">Humidity > 48.00</span></span>

<span data-ttu-id="d81b0-165">regla de temperatura de Hello desencadena hello **generar alarma** hello y acción de regla de humedad desencadena hello **SendMessage** acción.</span><span class="sxs-lookup"><span data-stu-id="d81b0-165">hello temperature rule triggers hello **Raise Alarm** action and hello Humidity rule triggers hello **SendMessage** action.</span></span> <span data-ttu-id="d81b0-166">Suponiendo que utilizaran Hola misma dirección URL para ambos hello acciones **ActionRepository** de la clase, los desencadenadores de aplicación lógica para cualquiera de ellas.</span><span class="sxs-lookup"><span data-stu-id="d81b0-166">Assuming you used hello same URL for both actions hello **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="d81b0-167">Ambas reglas usan SendGrid toosend un correo electrónico toohello **a** dirección con detalles de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="d81b0-167">Both rules use SendGrid toosend an email toohello **To** address with details of hello alert.</span></span>

> [!NOTE]
> <span data-ttu-id="d81b0-168">Hola aplicación lógica continúa tootrigger cada vez que se alcanza el umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="d81b0-168">hello Logic App continues tootrigger every time hello threshold is met.</span></span> <span data-ttu-id="d81b0-169">tooavoid de los correos electrónicos innecesarios, o bien puede deshabilitar las reglas de hello en su solución portal o deshabilitar Hola aplicación lógica en hello [portal de Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="d81b0-169">tooavoid unnecessary emails, you can either disable hello rules in your solution portal or disable hello Logic App in hello [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="d81b0-170">Además tooreceiving de mensajes de correo electrónico, también puede ver cuando Hola lógica de aplicación se ejecuta en el portal de hello:</span><span class="sxs-lookup"><span data-stu-id="d81b0-170">In addition tooreceiving emails, you can also see when hello Logic App runs in hello portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="d81b0-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d81b0-171">Next steps</span></span>
<span data-ttu-id="d81b0-172">Ahora que ha usado un proceso de negocio de tooa de solución de aplicación lógica tooconnect Hola preconfigurado, puede aprender más acerca de las opciones de Hola para personalizar soluciones de hello preconfigurado:</span><span class="sxs-lookup"><span data-stu-id="d81b0-172">Now that you've used a Logic App tooconnect hello preconfigured solution tooa business process, you can learn more about hello options for customizing hello preconfigured solutions:</span></span>

* <span data-ttu-id="d81b0-173">[Use la telemetría dinámica con hello solución preconfigurada de supervisión remota][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="d81b0-173">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="d81b0-174">[Metadatos de información de dispositivo en hello solución preconfigurada de supervisión remota][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="d81b0-174">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
