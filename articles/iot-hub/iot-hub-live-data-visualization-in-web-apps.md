---
title: "Visualización de datos del sensor en tiempo real desde Azure IoT Hub (Web Apps) | Microsoft Docs"
description: "Use la característica Web Apps de Microsoft Azure App Service para visualizar datos de temperatura y humedad que se recopilan desde el sensor y se envían a su IoT Hub."
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
ms.openlocfilehash: e037f5c29cabf8e5d0d3e7ded187280a0652d5c3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-the-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="44df3-104">Visualizar datos del sensor en tiempo real desde Azure IoT Hub mediante la característica Web Apps de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="44df3-104">Visualize real-time sensor data from your Azure IoT hub by using the Web Apps feature of Azure App Service</span></span>

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="44df3-106">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="44df3-106">What you learn</span></span>

<span data-ttu-id="44df3-107">En este tutorial, obtendrá más información sobre cómo visualizar los datos del sensor en tiempo real que recibe su IoT Hub mediante la ejecución de una aplicación web hospedada en una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="44df3-107">In this tutorial, you learn how to visualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="44df3-108">Si quiere intentar visualizar los datos en su IoT Hub con Power BI, vea [Visualización de datos del sensor en tiempo real desde Azure IoT Hub mediante Power BI](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="44df3-108">If you want to try to visualize the data in your IoT hub by using Power BI, see [Use Power BI to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="44df3-109">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="44df3-109">What you do</span></span>

- <span data-ttu-id="44df3-110">Crear una aplicación web en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="44df3-110">Create a web app in the Azure portal.</span></span>
- <span data-ttu-id="44df3-111">Preparar el IoT Hub para el acceso a datos mediante la adición de un grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="44df3-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="44df3-112">Configurar la aplicación web para leer datos del sensor desde su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="44df3-112">Configure the web app to read sensor data from your IoT hub.</span></span>
- <span data-ttu-id="44df3-113">Cargar una aplicación web para que se hospede en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="44df3-113">Upload a web application to be hosted by the web app.</span></span>
- <span data-ttu-id="44df3-114">Abrir la aplicación web para ver datos de temperatura y humedad en tiempo real desde su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="44df3-114">Open the web app to see real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="44df3-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="44df3-115">What you need</span></span>

- <span data-ttu-id="44df3-116">[Instalar el dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md), que incluye los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="44df3-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers the following requirements:</span></span>
  - <span data-ttu-id="44df3-117">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="44df3-117">An active Azure subscription</span></span>
  - <span data-ttu-id="44df3-118">Un IoT Hub en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="44df3-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="44df3-119">Una aplicación cliente que envíe mensajes a su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="44df3-119">A client application that sends messages to your Iot hub</span></span>
- [<span data-ttu-id="44df3-120">Descargar Git</span><span class="sxs-lookup"><span data-stu-id="44df3-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="44df3-121">Creación de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="44df3-121">Create a web app</span></span>

1. <span data-ttu-id="44df3-122">En [Azure Portal](https://ms.portal.azure.com/), haga clic en **Nuevo** > **Web y móvil** > **Aplicación web**.</span><span class="sxs-lookup"><span data-stu-id="44df3-122">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="44df3-123">Escriba un nombre de trabajo único, compruebe la suscripción, especifique un grupo de recursos y una ubicación, seleccione **Anclar al panel** y luego haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="44df3-123">Enter a unique job name, verify the subscription, specify a resource group and a location, select **Pin to dashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="44df3-124">Se recomienda seleccionar la misma ubicación donde se encuentra el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="44df3-124">We recommend that you select the same location as that of your resource group.</span></span> <span data-ttu-id="44df3-125">Esto ayuda a acelerar el procesamiento y a reduce el coste de la transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="44df3-125">Doing so assists with processing speed and reduces the cost of data transfer.</span></span>

   ![Creación de una aplicación web](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-the-web-app-to-read-data-from-your-iot-hub"></a><span data-ttu-id="44df3-127">Configuración de la aplicación web para leer datos del IoT Hub</span><span class="sxs-lookup"><span data-stu-id="44df3-127">Configure the web app to read data from your IoT hub</span></span>

1. <span data-ttu-id="44df3-128">Abra la aplicación web que acaba de aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="44df3-128">Open the web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="44df3-129">Haga clic en **Configuración de la aplicación** y luego, en **Configuración de la aplicación**, agregue los siguientes pares clave-valor:</span><span class="sxs-lookup"><span data-stu-id="44df3-129">Click **Application settings**, and then, under **App settings**, add the following key/value pairs:</span></span>

   | <span data-ttu-id="44df3-130">Clave</span><span class="sxs-lookup"><span data-stu-id="44df3-130">Key</span></span>                                   | <span data-ttu-id="44df3-131">Valor</span><span class="sxs-lookup"><span data-stu-id="44df3-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="44df3-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="44df3-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="44df3-133">Obtenido de iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="44df3-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="44df3-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="44df3-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="44df3-135">El nombre del grupo de consumidores que agrega a su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="44df3-135">The name of the consumer group that you add to your IoT hub</span></span>  |

   ![Agregar la configuración a una aplicación web con pares clave-valor](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="44df3-137">Haga clic en **Configuración de la aplicación**, en **Configuración General**, active o desactive la opción **Web sockets** y, después, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="44df3-137">Click **Application settings**, under **General settings**, toggle the **Web sockets** option, and then click **Save**.</span></span>

   ![Activar o desactivar la opción Web sockets](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-to-be-hosted-by-the-web-app"></a><span data-ttu-id="44df3-139">Carga de una aplicación web para que se hospede en la aplicación web</span><span class="sxs-lookup"><span data-stu-id="44df3-139">Upload a web application to be hosted by the web app</span></span>

<span data-ttu-id="44df3-140">Hemos facilitado el acceso a una aplicación web en GitHub que muestra datos del sensor en tiempo real desde su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="44df3-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="44df3-141">Todo lo que tiene que hacer es configurar la aplicación web para que funcione con un repositorio de Git, descargarla de GitHub y cargarla en Azure para que la hospede la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="44df3-141">All you need to do is configure the web app to work with a Git repository, download the web application from GitHub, and then upload it to Azure for the web app to host.</span></span>

1. <span data-ttu-id="44df3-142">En la aplicación web, haga clic en **Opciones de implementación** > **Elegir origen** > **Repositorio de Git local** y después pulse **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="44df3-142">In the web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![Configuración de la implementación de la aplicación web para usar el repositorio de Git local](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="44df3-144">Haga clic en **Credenciales de implementación**, cree un nombre de usuario y una contraseña que se usarán para conectarse al repositorio de Git de Azure y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="44df3-144">Click **Deployment Credentials**, create a user name and password to use to connect to the Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="44df3-145">Haga clic en **Información general** y anote el valor de la **URL de clonación de Git**.</span><span class="sxs-lookup"><span data-stu-id="44df3-145">Click **Overview**, and note the value of **Git clone url**.</span></span>

   ![Obtener la dirección URL de clonación de Git de la aplicación web](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="44df3-147">Abra una ventana de comando o de terminal en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="44df3-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="44df3-148">Descargue la aplicación web de GitHub y cárguela en Azure para que se hospede en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="44df3-148">Download the web app from GitHub, and upload it to Azure for the web app to host.</span></span> <span data-ttu-id="44df3-149">Para ello, ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="44df3-149">To do so, run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="44df3-150">La \<dirección URL de clonación de GIT\> es la dirección URL del repositorio de Git que se encuentra en la página **Overview** (Información general) de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="44df3-150">\<Git clone URL\> is the URL of the Git repository found on the **Overview** page of the web app.</span></span>

## <a name="open-the-web-app-to-see-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="44df3-151">Abra la aplicación web para ver los datos de temperatura y humedad en tiempo real desde su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="44df3-151">Open the web app to see real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="44df3-152">En la página **Overview** (Información general) de la aplicación web, haga clic en la dirección URL para abrir la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="44df3-152">On the **Overview** page of your web app, click the URL to open the web app.</span></span>

![Obtención de la dirección URL de la aplicación web](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="44df3-154">Verá los datos de temperatura y humedad en tiempo real desde su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="44df3-154">You should see the real-time temperature and humidity data from your IoT hub.</span></span>

![Página de aplicación web que muestra la temperatura y humedad en tiempo real](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="44df3-156">Asegúrese de que la aplicación de ejemplo se ejecuta en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="44df3-156">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="44df3-157">Si no es así, obtendrá un gráfico en blanco; puede consultar los tutoriales de [configuración del dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="44df3-157">If not, you will get a blank chart, you can refer to the tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="44df3-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="44df3-158">Next steps</span></span>
<span data-ttu-id="44df3-159">Ha usado correctamente una aplicación web para visualizar datos del sensor en tiempo real desde su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="44df3-159">You've successfully used your web app to visualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="44df3-160">Para obtener una forma alternativa de visualizar los datos desde Azure IoT Hub, vea [Visualización de datos del sensor en tiempo real desde Azure IoT Hub mediante Power BI](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="44df3-160">For an alternative way to visualize data from Azure IoT Hub, see [Use Power BI to visualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
