---
title: "Visualización de los datos de sensor desde el centro de IoT de Azure: aplicaciones Web aaaReal tiempo | Documentos de Microsoft"
description: "Usar la característica de las aplicaciones Web de Hola de servicio de aplicaciones de Microsoft Azure toovisualize temperatura y humedad datos que se recopila del sensor de Hola y envía el centro de Iot tooyour."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "visualización de datos en tiempo real, visualización de datos en directo, visualización de datos de sensor"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="e579e-104">Visualizar datos de sensor en tiempo real desde su centro de IoT de Azure mediante la característica de las aplicaciones Web de Hola de servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="e579e-104">Visualize real-time sensor data from your Azure IoT hub by using hello Web Apps feature of Azure App Service</span></span>

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="e579e-106">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="e579e-106">What you learn</span></span>

<span data-ttu-id="e579e-107">En este tutorial, aprenderá cómo toovisualize datos de sensor en tiempo real que recibe de su centro de IoT mediante la ejecución de una aplicación web que se hospedan en una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e579e-107">In this tutorial, you learn how toovisualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="e579e-108">Si desea datos de tootry toovisualize hello en el centro de IoT mediante el uso de Power BI, consulte [datos de sensor en tiempo real de toovisualize Use Power BI desde el centro de IoT de Azure](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="e579e-108">If you want tootry toovisualize hello data in your IoT hub by using Power BI, see [Use Power BI toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="e579e-109">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="e579e-109">What you do</span></span>

- <span data-ttu-id="e579e-110">Crear una aplicación web en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e579e-110">Create a web app in hello Azure portal.</span></span>
- <span data-ttu-id="e579e-111">Preparar el IoT Hub para el acceso a datos mediante la adición de un grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="e579e-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="e579e-112">Configurar datos de sensor de hello web app tooread desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e579e-112">Configure hello web app tooread sensor data from your IoT hub.</span></span>
- <span data-ttu-id="e579e-113">Cargar una toobe de aplicación web hospedada por la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="e579e-113">Upload a web application toobe hosted by hello web app.</span></span>
- <span data-ttu-id="e579e-114">Abrir hello web toosee en tiempo real temperatura y humedad datos de la aplicación desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e579e-114">Open hello web app toosee real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e579e-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="e579e-115">What you need</span></span>

- <span data-ttu-id="e579e-116">[Configurar el dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md), donde abordan las Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="e579e-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers hello following requirements:</span></span>
  - <span data-ttu-id="e579e-117">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="e579e-117">An active Azure subscription</span></span>
  - <span data-ttu-id="e579e-118">Un IoT Hub en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="e579e-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="e579e-119">Una aplicación cliente que envía el centro de Iot tooyour de mensajes</span><span class="sxs-lookup"><span data-stu-id="e579e-119">A client application that sends messages tooyour Iot hub</span></span>
- [<span data-ttu-id="e579e-120">Descargar Git</span><span class="sxs-lookup"><span data-stu-id="e579e-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="e579e-121">Creación de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="e579e-121">Create a web app</span></span>

1. <span data-ttu-id="e579e-122">Hola [portal de Azure](https://ms.portal.azure.com/), haga clic en **New** > **Web y móvil** > **aplicación Web**.</span><span class="sxs-lookup"><span data-stu-id="e579e-122">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="e579e-123">Escriba un nombre de trabajo único, compruebe la suscripción de hello, especifique un grupo de recursos y una ubicación, seleccione **Pin toodashboard**y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="e579e-123">Enter a unique job name, verify hello subscription, specify a resource group and a location, select **Pin toodashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="e579e-124">Le recomendamos que seleccione Hola misma ubicación que el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e579e-124">We recommend that you select hello same location as that of your resource group.</span></span> <span data-ttu-id="e579e-125">Si lo hace, ayuda con la velocidad de procesamiento y reduce el costo de Hola de transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="e579e-125">Doing so assists with processing speed and reduces hello cost of data transfer.</span></span>

   ![Creación de una aplicación web](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a><span data-ttu-id="e579e-127">Configurar datos de tooread la aplicación hello web desde el centro de IoT</span><span class="sxs-lookup"><span data-stu-id="e579e-127">Configure hello web app tooread data from your IoT hub</span></span>

1. <span data-ttu-id="e579e-128">Abra la aplicación web de hello que acaba de aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="e579e-128">Open hello web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="e579e-129">Haga clic en **configuración de la aplicación**y, a continuación, en **configuración de la aplicación**, agregar Hola después de pares clave/valor:</span><span class="sxs-lookup"><span data-stu-id="e579e-129">Click **Application settings**, and then, under **App settings**, add hello following key/value pairs:</span></span>

   | <span data-ttu-id="e579e-130">Clave</span><span class="sxs-lookup"><span data-stu-id="e579e-130">Key</span></span>                                   | <span data-ttu-id="e579e-131">Valor</span><span class="sxs-lookup"><span data-stu-id="e579e-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="e579e-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="e579e-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="e579e-133">Obtenido de iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="e579e-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="e579e-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="e579e-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="e579e-135">nombre de Hello del grupo de consumidores de Hola que agregue tooyour centro de IoT</span><span class="sxs-lookup"><span data-stu-id="e579e-135">hello name of hello consumer group that you add tooyour IoT hub</span></span>  |

   ![Agregar la aplicación web de configuración tooyour con pares clave/valor](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="e579e-137">Haga clic en **configuración de la aplicación**, en **configuración General**, Hola de alternancia **Web sockets** opción y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="e579e-137">Click **Application settings**, under **General settings**, toggle hello **Web sockets** option, and then click **Save**.</span></span>

   ![Alternar hello Web sockets, opción](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a><span data-ttu-id="e579e-139">Cargar una toobe de aplicación web hospedada por la aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="e579e-139">Upload a web application toobe hosted by hello web app</span></span>

<span data-ttu-id="e579e-140">Hemos facilitado el acceso a una aplicación web en GitHub que muestra datos del sensor en tiempo real desde su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e579e-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="e579e-141">Todo lo que necesita toodo es configurar hello web app toowork con un repositorio Git, descargar la aplicación web de hello desde GitHub y, a continuación, cargarlo tooAzure para toohost de aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="e579e-141">All you need toodo is configure hello web app toowork with a Git repository, download hello web application from GitHub, and then upload it tooAzure for hello web app toohost.</span></span>

1. <span data-ttu-id="e579e-142">En la aplicación web de hello, haga clic en **opciones de implementación** > **Elegir origen** > **repositorio de Git Local**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e579e-142">In hello web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![Configurar el repositorio de Git web app deployment toouse Hola local](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="e579e-144">Haga clic en **las credenciales de implementación**, cree un usuario nombre y la contraseña toouse tooconnect toohello repositorio de Git en Azure y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="e579e-144">Click **Deployment Credentials**, create a user name and password toouse tooconnect toohello Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="e579e-145">Haga clic en **Introducción**y anote el valor de Hola de **url de clonación de Git**.</span><span class="sxs-lookup"><span data-stu-id="e579e-145">Click **Overview**, and note hello value of **Git clone url**.</span></span>

   ![Obtener la dirección URL de clonación de Git de saludo de la aplicación web](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="e579e-147">Abra una ventana de comando o de terminal en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="e579e-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="e579e-148">Descargar la aplicación web de hello desde GitHub y cargarlo tooAzure para toohost de aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="e579e-148">Download hello web app from GitHub, and upload it tooAzure for hello web app toohost.</span></span> <span data-ttu-id="e579e-149">toodo es así, ejecute hello comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e579e-149">toodo so, run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="e579e-150">\<Dirección URL de clonación de GIT\> es Hola URL del repositorio de Git Hola se encuentra en hello **Introducción** página de aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="e579e-150">\<Git clone URL\> is hello URL of hello Git repository found on hello **Overview** page of hello web app.</span></span>

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="e579e-151">Abrir hello web toosee en tiempo real temperatura y humedad datos de la aplicación desde el centro de IoT</span><span class="sxs-lookup"><span data-stu-id="e579e-151">Open hello web app toosee real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="e579e-152">En hello **Introducción** página de la aplicación web, haga clic en aplicación web de hello URL tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="e579e-152">On hello **Overview** page of your web app, click hello URL tooopen hello web app.</span></span>

![Obtener dirección URL de saludo de la aplicación web](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="e579e-154">Debería ver datos de humedad y temperatura de hello en tiempo real desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e579e-154">You should see hello real-time temperature and humidity data from your IoT hub.</span></span>

![Página de aplicación web que muestra la temperatura y humedad en tiempo real](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="e579e-156">Asegúrese de que está ejecutando la aplicación de ejemplo de Hola en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e579e-156">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="e579e-157">Si no es así, obtendrá un gráfico en blanco, puede consultar toohello tutoriales en [configurar su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e579e-157">If not, you will get a blank chart, you can refer toohello tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e579e-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e579e-158">Next steps</span></span>
<span data-ttu-id="e579e-159">Ha usado correctamente los datos de sensor en tiempo real de toovisualize de aplicación web de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e579e-159">You've successfully used your web app toovisualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="e579e-160">Para un forma alternativa toovisualize los datos desde el centro de IoT de Azure, consulte [datos de sensor en tiempo real de toovisualize Use Power BI desde el centro de IoT](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="e579e-160">For an alternative way toovisualize data from Azure IoT Hub, see [Use Power BI toovisualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
