---
title: Conjunto de aplicaciones de IoT de Azure y Logic Apps | Microsoft Docs
description: "Un tutorial sobre cómo enlazar aplicaciones lógicas con el conjunto de aplicaciones de IoT de Azure para el proceso empresarial."
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
ms.openlocfilehash: 2e7997e2a8bdeeec6083d40acb55e653f87e140b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-connect-logic-app-to-your-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="3f0da-103">Tutorial: Conexión de una aplicación lógica a la solución preconfigurada de supervisión remota del conjunto de aplicaciones de IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="3f0da-103">Tutorial: Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="3f0da-104">La solución preconfigurada de supervisión remota del [conjunto de aplicaciones de IoT de Microsoft Azure][lnk-internetofthings] constituye una excelente forma de empezar a trabajar rápidamente con una serie de características de extremo a extremo que ejemplifica una solución de IoT.</span><span class="sxs-lookup"><span data-stu-id="3f0da-104">The [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way to get started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="3f0da-105">Este tutorial le mostrará cómo agregar una aplicación lógica a su solución preconfigurada de supervisión remota de dicho conjunto de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3f0da-105">This tutorial walks you through how to add Logic App to your Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="3f0da-106">Estos pasos muestran cómo puede aprovechar aún más la solución de IoT conectándola a un proceso empresarial.</span><span class="sxs-lookup"><span data-stu-id="3f0da-106">These steps demonstrate how you can take your IoT solution even further by connecting it to a business process.</span></span>

<span data-ttu-id="3f0da-107">*Si está buscando un tutorial sobre cómo aprovisionar una solución preconfigurada de supervisión remota, consulte [Tutorial: Introducción a las soluciones preconfiguradas][lnk-getstarted].*</span><span class="sxs-lookup"><span data-stu-id="3f0da-107">*If you’re looking for a walkthrough on how to provision a remote monitoring preconfigured solution, see [Tutorial: Get started with the IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="3f0da-108">Antes de comenzar este tutorial, debe:</span><span class="sxs-lookup"><span data-stu-id="3f0da-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="3f0da-109">Aprovisionar la solución preconfigurada de supervisión remota en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3f0da-109">Provision the remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="3f0da-110">Crear una cuenta de SendGrid para poder enviar un correo electrónico que desencadene el proceso de negocio.</span><span class="sxs-lookup"><span data-stu-id="3f0da-110">Create a SendGrid account to enable you to send an email that triggers your business process.</span></span> <span data-ttu-id="3f0da-111">Puede registrarse para obtener una cuenta de evaluación gratuita en [SendGrid](https://sendgrid.com/) haciendo clic en **Try for Free**(Probar gratis).</span><span class="sxs-lookup"><span data-stu-id="3f0da-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="3f0da-112">Después de haberse registrado para crear una cuenta de evaluación gratuita, deberá generar una [clave de API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) en SendGrid que conceda permisos para enviar correo.</span><span class="sxs-lookup"><span data-stu-id="3f0da-112">After you have registered for your free trial account, you need to create an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions to send mail.</span></span> <span data-ttu-id="3f0da-113">La necesitará más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="3f0da-113">You need this API key later in the tutorial.</span></span>

<span data-ttu-id="3f0da-114">Para completar este tutorial, necesita Visual Studio 2015 o Visual Studio 2017 para modificar las acciones en el back-end de soluciones preconfiguradas.</span><span class="sxs-lookup"><span data-stu-id="3f0da-114">To complete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 to modify the actions in the preconfigured solution back end.</span></span>

<span data-ttu-id="3f0da-115">Suponiendo que ya se haya aprovisionado la solución preconfigurada de supervisión remota, vaya al grupo de recursos correspondiente a esa solución en[ Azure Portal][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="3f0da-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate to the resource group for that solution in the [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="3f0da-116">El grupo de recursos tiene el mismo nombre que la solución de supervisión remota aprovisionada.</span><span class="sxs-lookup"><span data-stu-id="3f0da-116">The resource group has the same name as the solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="3f0da-117">En el grupo de recursos, puede ver todos los recursos de Azure aprovisionados previamente para su solución (a excepción de la aplicación Azure Active Directory, que se puede encontrar en el Portal de Azure clásico).</span><span class="sxs-lookup"><span data-stu-id="3f0da-117">In the resource group, you can see all the provisioned Azure resources for your solution except for the Azure Active Directory application that you can find in the Azure Classic Portal.</span></span> <span data-ttu-id="3f0da-118">La captura de pantalla siguiente muestra una hoja de **grupo de recursos** de ejemplo para una solución preconfigurada de supervisión remota:</span><span class="sxs-lookup"><span data-stu-id="3f0da-118">The following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="3f0da-119">Para comenzar, configure la aplicación lógica que se usará con la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="3f0da-119">To begin, set up the logic app to use with the preconfigured solution.</span></span>

## <a name="set-up-the-logic-app"></a><span data-ttu-id="3f0da-120">Configuración de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="3f0da-120">Set up the Logic App</span></span>
1. <span data-ttu-id="3f0da-121">Haga clic en la opción **Agregar** que verá en la parte superior de la hoja del grupo de recursos en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3f0da-121">Click **Add** at the top of your resource group blade in the Azure portal.</span></span>
2. <span data-ttu-id="3f0da-122">Busque la **aplicación lógica**, selecciónela y, después, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3f0da-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="3f0da-123">Especifique un valor en **Nombre** y utilice los mismos valores de **Suscripción** y **Grupo de recursos** que usó al aprovisionar la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="3f0da-123">Fill out the **Name** and use the same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="3f0da-124">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3f0da-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="3f0da-125">Cuando se complete la implementación, verá que la aplicación lógica aparece incluida en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3f0da-125">When your deployment completes, you can see the Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="3f0da-126">Haga clic en la aplicación lógica para desplazarse a la hoja de aplicación lógica y seleccione la plantilla **Aplicación lógica en blanco** para abrir el **Diseñador de aplicaciones lógicas**.</span><span class="sxs-lookup"><span data-stu-id="3f0da-126">Click the Logic App to navigate to the Logic App blade, select the **Blank Logic App** template to open the **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="3f0da-127">Seleccione **Solicitud**.</span><span class="sxs-lookup"><span data-stu-id="3f0da-127">Select **Request**.</span></span> <span data-ttu-id="3f0da-128">Esta acción especifica que una solicitud HTTP entrante con una carga específica con formato de JSON actúa como desencadenador.</span><span class="sxs-lookup"><span data-stu-id="3f0da-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="3f0da-129">Pegue el siguiente código en el esquema de JSON del cuerpo de la solicitud:</span><span class="sxs-lookup"><span data-stu-id="3f0da-129">Paste the following code into the Request Body JSON Schema:</span></span>
   
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
   > <span data-ttu-id="3f0da-130">Puede copiar la dirección URL de HTTP POST tras guardar la aplicación lógica, pero, primero, debe agregar una acción.</span><span class="sxs-lookup"><span data-stu-id="3f0da-130">You can copy the URL for the HTTP post after you save the logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="3f0da-131">Haga clic en **+ Nuevo paso** en el desencadenador manual.</span><span class="sxs-lookup"><span data-stu-id="3f0da-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="3f0da-132">A continuación, haga clic en **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="3f0da-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="3f0da-133">Busque la opción **SendGrid - Send email** (SendGrid: enviar correo electrónico) y haga clic en ella.</span><span class="sxs-lookup"><span data-stu-id="3f0da-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="3f0da-134">Escriba un nombre para la conexión, como **SendGridConnection**, escriba la **clave de API de SendGrid** que creó al configurar la cuenta de SendGrid y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3f0da-134">Enter a name for the connection, such as **SendGridConnection**, enter the **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="3f0da-135">Agregue direcciones de correo electrónico que posea tanto al campo **De** como a **Para**.</span><span class="sxs-lookup"><span data-stu-id="3f0da-135">Add email addresses you own to both the **From** and **To** fields.</span></span> <span data-ttu-id="3f0da-136">Agregue **Alerta de supervisión remota [DeviceId]** al campo **Asunto**.</span><span class="sxs-lookup"><span data-stu-id="3f0da-136">Add **Remote monitoring alert [DeviceId]** to the **Subject** field.</span></span> <span data-ttu-id="3f0da-137">En el campo **Cuerpo del correo electrónico**, agregue **. El dispositivo [DeviceId] ha informado de [measurementName] con el valor [measuredValue].**</span><span class="sxs-lookup"><span data-stu-id="3f0da-137">In the **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="3f0da-138">Puede agregar **[DeviceId]**, **[measurementName]** y **[measuredValue]** haciendo clic en la sección **Puede insertar datos de pasos anteriores**.</span><span class="sxs-lookup"><span data-stu-id="3f0da-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in the **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="3f0da-139">Haga clic en **Guardar** en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="3f0da-139">Click **Save** in the top menu.</span></span>
13. <span data-ttu-id="3f0da-140">Haga clic en el desencadenador **Solicitud** y copie el valor **HTTP POST a esta dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="3f0da-140">Click the **Request** trigger and copy the **Http Post to this URL** value.</span></span> <span data-ttu-id="3f0da-141">Necesitará esta URL más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="3f0da-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="3f0da-142">Logic Apps permite ejecutar [muchos tipos diferentes de acciones][lnk-logic-apps-actions], incluidas las de Office 365.</span><span class="sxs-lookup"><span data-stu-id="3f0da-142">Logic Apps enable you to run [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-the-eventprocessor-web-job"></a><span data-ttu-id="3f0da-143">Configuración del trabajo web EventProcessor</span><span class="sxs-lookup"><span data-stu-id="3f0da-143">Set up the EventProcessor Web Job</span></span>
<span data-ttu-id="3f0da-144">En esta sección, se conectará la solución preconfigurada a la aplicación lógica creada.</span><span class="sxs-lookup"><span data-stu-id="3f0da-144">In this section, you connect your preconfigured solution to the Logic App you created.</span></span> <span data-ttu-id="3f0da-145">Para completar esta tarea, agregue la dirección URL para desencadenar la aplicación lógica con la acción que se activa cuando el valor del sensor de un dispositivo supera un umbral.</span><span class="sxs-lookup"><span data-stu-id="3f0da-145">To complete this task, you add the URL to trigger the Logic App to the action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="3f0da-146">Use el cliente de Git para clonar la versión más reciente del [repositorio de GitHub azure-iot-remote-monitoring][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="3f0da-146">Use your git client to clone the latest version of the [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="3f0da-147">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3f0da-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="3f0da-148">En Visual Studio, abra **RemoteMonitoring.sln** de la copia local del repositorio.</span><span class="sxs-lookup"><span data-stu-id="3f0da-148">In Visual Studio, open the **RemoteMonitoring.sln** from the local copy of the repository.</span></span>
3. <span data-ttu-id="3f0da-149">Abra el archivo **ActionRepository.cs** de la carpeta **Infrastructure\\Repository**.</span><span class="sxs-lookup"><span data-stu-id="3f0da-149">Open the **ActionRepository.cs** file in the **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="3f0da-150">Actualice el diccionario **actionIds** con el valor de **HTTP POST a esta dirección URL** que anotó de la aplicación lógica, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="3f0da-150">Update the **actionIds** dictionary with the **Http Post to this URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post to this URL>" },
        { "Raise Alarm", "<Http Post to this URL>" }
    };
    ```
5. <span data-ttu-id="3f0da-151">Guarde los cambios de la solución y salga de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3f0da-151">Save the changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-the-command-line"></a><span data-ttu-id="3f0da-152">Implementación desde la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="3f0da-152">Deploy from the command line</span></span>
<span data-ttu-id="3f0da-153">En esta sección, implementará la versión actualizada de la solución de supervisión remota para reemplazar la que se encuentre actualmente en ejecución en Azure.</span><span class="sxs-lookup"><span data-stu-id="3f0da-153">In this section, you deploy your updated version of the remote monitoring solution to replace the version currently running in Azure.</span></span>

1. <span data-ttu-id="3f0da-154">Siga las instrucciones de [configuración del entorno de desarrollo][lnk-devsetup] con el fin de prepararlo para la implementación.</span><span class="sxs-lookup"><span data-stu-id="3f0da-154">Following the [dev set-up][lnk-devsetup] instructions to set up your environment for deployment.</span></span>
2. <span data-ttu-id="3f0da-155">Para efectuar la implementación localmente, siga las instrucciones de [implementación local][lnk-localdeploy].</span><span class="sxs-lookup"><span data-stu-id="3f0da-155">To deploy locally, follow the [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="3f0da-156">Para efectuar la implementación en la nube y actualizar la existente, siga las instrucciones de [implementación de nube][lnk-clouddeploy].</span><span class="sxs-lookup"><span data-stu-id="3f0da-156">To deploy to the cloud and update your existing cloud deployment, follow the [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="3f0da-157">Utilice el nombre de la implementación original como el nombre de la implementación.</span><span class="sxs-lookup"><span data-stu-id="3f0da-157">Use the name of your original deployment as the deployment name.</span></span> <span data-ttu-id="3f0da-158">Por ejemplo, si la original se denomina **demologicapp**, utilice el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="3f0da-158">For example if the original deployment was called **demologicapp**, use the following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="3f0da-159">Cuando se ejecute el script de compilación, asegúrese de usar la misma cuenta, suscripción, región e instancia de Active Directory de Azure que utilizó al aprovisionar la solución.</span><span class="sxs-lookup"><span data-stu-id="3f0da-159">When the build script runs, be sure to use the same Azure account, subscription, region, and Active Directory instance you used when you provisioned the solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="3f0da-160">La aplicación lógica en acción</span><span class="sxs-lookup"><span data-stu-id="3f0da-160">See your Logic App in action</span></span>
<span data-ttu-id="3f0da-161">La solución preconfigurada de supervisión remota tiene dos reglas configuradas de forma predeterminada al aprovisionar una solución.</span><span class="sxs-lookup"><span data-stu-id="3f0da-161">The remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="3f0da-162">Ambas se encuentran en el dispositivo **SampleDevice001** :</span><span class="sxs-lookup"><span data-stu-id="3f0da-162">Both rules are on the **SampleDevice001** device:</span></span>

* <span data-ttu-id="3f0da-163">Temperature > 38.00 (Temperatura > 38,00)</span><span class="sxs-lookup"><span data-stu-id="3f0da-163">Temperature > 38.00</span></span>
* <span data-ttu-id="3f0da-164">Humidity > 48.00 (Humedad > 48,00)</span><span class="sxs-lookup"><span data-stu-id="3f0da-164">Humidity > 48.00</span></span>

<span data-ttu-id="3f0da-165">La regla de temperatura desencadena la acción **Activar alarma**, mientras que la de humedad desencadena la acción **Enviar mensaje**.</span><span class="sxs-lookup"><span data-stu-id="3f0da-165">The temperature rule triggers the **Raise Alarm** action and the Humidity rule triggers the **SendMessage** action.</span></span> <span data-ttu-id="3f0da-166">Suponiendo que utiliza la misma dirección URL para ambas acciones de la clase **ActionRepository** , la aplicación lógica se desencadenará con cualquiera de las dos reglas.</span><span class="sxs-lookup"><span data-stu-id="3f0da-166">Assuming you used the same URL for both actions the **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="3f0da-167">Ambas reglas usan SendGrid para enviar un correo electrónico a la dirección **Para** con detalles de la alerta.</span><span class="sxs-lookup"><span data-stu-id="3f0da-167">Both rules use SendGrid to send an email to the **To** address with details of the alert.</span></span>

> [!NOTE]
> <span data-ttu-id="3f0da-168">La aplicación lógica se sigue desencadenando cada vez que se alcance el umbral.</span><span class="sxs-lookup"><span data-stu-id="3f0da-168">The Logic App continues to trigger every time the threshold is met.</span></span> <span data-ttu-id="3f0da-169">Para evitar mensajes innecesarios, puede deshabilitar las reglas en el portal de la solución o deshabilitar la aplicación lógica en [Azure Portal][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="3f0da-169">To avoid unnecessary emails, you can either disable the rules in your solution portal or disable the Logic App in the [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="3f0da-170">Además de recibir mensajes de correo electrónico, también puede ver cuándo se ejecuta la aplicación lógica en el portal:</span><span class="sxs-lookup"><span data-stu-id="3f0da-170">In addition to receiving emails, you can also see when the Logic App runs in the portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="3f0da-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3f0da-171">Next steps</span></span>
<span data-ttu-id="3f0da-172">Ahora que ha utilizado una aplicación lógica para conectar la solución preconfigurada a un proceso empresarial, puede obtener más información sobre las opciones para personalizar las soluciones preconfiguradas:</span><span class="sxs-lookup"><span data-stu-id="3f0da-172">Now that you've used a Logic App to connect the preconfigured solution to a business process, you can learn more about the options for customizing the preconfigured solutions:</span></span>

* <span data-ttu-id="3f0da-173">[Uso de telemetría dinámica con la solución de supervisión remota preconfigurada][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="3f0da-173">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="3f0da-174">[Metadatos de información de dispositivo en la solución preconfigurada de supervisión remota][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="3f0da-174">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>

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
