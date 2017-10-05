---
title: Uso de Azure Portal para crear un centro de IoT | Microsoft Docs
description: "Describe sobre cómo crear, administrar y eliminar los centros de IoT Hub de Azure a través de Azure Portal. Incluye información sobre los niveles de precios, el escalado, la seguridad y la configuración de la mensajería."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: bca7eea5f44bbed3b784b56edaac235161b43e5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-portal"></a><span data-ttu-id="c16be-104">Creación de una instancia de IoT Hub mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c16be-104">Create an IoT hub using the Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="c16be-105">En este artículo se describe:</span><span class="sxs-lookup"><span data-stu-id="c16be-105">This article describes:</span></span>

* <span data-ttu-id="c16be-106">Cómo buscar el servicio IoT Hub en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c16be-106">How to find the IoT Hub service in the Azure portal.</span></span>
* <span data-ttu-id="c16be-107">Cómo crear y administrar instancias de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c16be-107">How to create and manage IoT hubs.</span></span>

## <a name="where-to-find-the-iot-hub-service"></a><span data-ttu-id="c16be-108">Dónde buscar el servicio IoT Hub</span><span class="sxs-lookup"><span data-stu-id="c16be-108">Where to find the IoT Hub service</span></span>

<span data-ttu-id="c16be-109">Puede buscar el servicio IoT Hub en las siguientes ubicaciones del portal:</span><span class="sxs-lookup"><span data-stu-id="c16be-109">You can find the IoT Hub service in the following locations in the portal:</span></span>

* <span data-ttu-id="c16be-110">Elija **+ Nuevo** y después **Internet de las cosas**.</span><span class="sxs-lookup"><span data-stu-id="c16be-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="c16be-111">En Marketplace, elija **Internet de las cosas**.</span><span class="sxs-lookup"><span data-stu-id="c16be-111">In the Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="c16be-112">Crear un centro de IoT</span><span class="sxs-lookup"><span data-stu-id="c16be-112">Create an IoT hub</span></span>

<span data-ttu-id="c16be-113">Puede crear un IoT Hub con los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c16be-113">You can create an IoT hub using the following methods:</span></span>

* <span data-ttu-id="c16be-114">La opción **+ Nuevo** abre la hoja que se muestra en la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="c16be-114">The **+ New** option opens the blade shown in the following screen shot.</span></span> <span data-ttu-id="c16be-115">Los pasos para crear el Centro de IoT con este método y con Marketplace son idénticos.</span><span class="sxs-lookup"><span data-stu-id="c16be-115">The steps for creating the IoT hub through this method and through the marketplace are identical.</span></span>
* <span data-ttu-id="c16be-116">En Marketplace, elija **Crear** para abrir la hoja que se muestra en la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="c16be-116">In the Marketplace, choose **Create** to open the blade shown in the following screen shot.</span></span>

<span data-ttu-id="c16be-117">En las secciones siguientes se describen los distintos pasos para crear una instancia de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="c16be-117">The following sections describe the several steps to create an IoT hub:</span></span>

### <a name="choose-the-name-of-the-iot-hub"></a><span data-ttu-id="c16be-118">Elección del nombre del Centro de IoT</span><span class="sxs-lookup"><span data-stu-id="c16be-118">Choose the name of the IoT hub</span></span>

<span data-ttu-id="c16be-119">Para crear un centro de IoT, debe asignar un nombre al centro.</span><span class="sxs-lookup"><span data-stu-id="c16be-119">To create an IoT hub, you must name the IoT hub.</span></span> <span data-ttu-id="c16be-120">Este nombre debe ser exclusivo para distinguirlo en todas las instancias de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c16be-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-the-pricing-tier"></a><span data-ttu-id="c16be-121">Elección del plan de tarifa</span><span class="sxs-lookup"><span data-stu-id="c16be-121">Choose the pricing tier</span></span>

<span data-ttu-id="c16be-122">Puede elegir entre cuatro niveles: **Gratis**, **Estándar 1**, **Estándar 2** y **Estándar S3**.</span><span class="sxs-lookup"><span data-stu-id="c16be-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="c16be-123">El nivel Gratis permite solo la conexión de 500 dispositivos con el Centro de IoT y hasta 8000 mensajes al día.</span><span class="sxs-lookup"><span data-stu-id="c16be-123">The free tier allows only 500 devices to be connected to the IoT hub and up to 8,000 messages per day.</span></span>

<span data-ttu-id="c16be-124">**Estándar S1**: use la edición S1 de las soluciones de IoT con un gran número de dispositivos, y cada uno de ellos genera pequeñas cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="c16be-124">**Standard S1**: Use the S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="c16be-125">Cada unidad de la edición S1 permite transmitir hasta 400.000 mensajes por día a través de todos los dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="c16be-125">Each unit of the S1 edition allows up to 400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="c16be-126">**Estándar S2**: use la edición S2 de las soluciones de IoT en las que los dispositivos generan grandes cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="c16be-126">**Standard S2**: Use the S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="c16be-127">Cada unidad de la edición S2 permite transmitir hasta 6 millones de mensajes al día entre todos los dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="c16be-127">Each unit of the S2 edition allows up to 6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="c16be-128">**Estándar S3**: use la edición S3 de las soluciones de IoT que generan grandes cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="c16be-128">**Standard S3**: Use the S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="c16be-129">Cada unidad de la edición S3 permite transmitir hasta 300 millones de mensajes al día entre todos los dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="c16be-129">Each unit of the S3 edition allows up to 300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="c16be-130">IoT Hub solo permite un único centro gratuito por suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c16be-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="c16be-131">Unidades del Centro de IoT</span><span class="sxs-lookup"><span data-stu-id="c16be-131">IoT hub units</span></span>

<span data-ttu-id="c16be-132">El número de mensajes que se permiten por unidad al día depende del plan de tarifa del centro.</span><span class="sxs-lookup"><span data-stu-id="c16be-132">The number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="c16be-133">Por ejemplo, si desea que el Centro de IoT admita la entrada de 700 000 mensajes, elija dos unidades del nivel de S1.</span><span class="sxs-lookup"><span data-stu-id="c16be-133">For example, if you want the IoT hub to support ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-to-cloud-partitions-and-resource-group"></a><span data-ttu-id="c16be-134">Dispositivo para particiones en la nube y grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c16be-134">Device to cloud partitions and resource group</span></span>

<span data-ttu-id="c16be-135">Puede cambiar el número de particiones para un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c16be-135">You can change the number of partitions for an IoT hub.</span></span> <span data-ttu-id="c16be-136">El número predeterminado de particiones es cuatro, pero puede elegir un número diferente de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="c16be-136">The default number of partitions is 4, you can choose a different number from the drop-down list.</span></span>

<span data-ttu-id="c16be-137">No es necesario crear explícitamente un grupo de recursos vacío.</span><span class="sxs-lookup"><span data-stu-id="c16be-137">You do not need to explicitly create an empty resource group.</span></span> <span data-ttu-id="c16be-138">Al crear un recurso, puede elegir entre crear un grupo de recursos o usar uno existente.</span><span class="sxs-lookup"><span data-stu-id="c16be-138">When you create a resource, you can choose either to create a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="c16be-139">Elección de la suscripción</span><span class="sxs-lookup"><span data-stu-id="c16be-139">Choose subscription</span></span>

<span data-ttu-id="c16be-140">Azure IoT Hub muestra automáticamente la lista de suscripciones de Azure a la que está vinculada la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="c16be-140">Azure IoT Hub automatically lists the Azure subscriptions the user account is linked to.</span></span> <span data-ttu-id="c16be-141">Puede elegir la suscripción de Azure a la que desea asociar la instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c16be-141">You can choose the Azure subscription to associate the IoT hub to.</span></span>

### <a name="choose-the-location"></a><span data-ttu-id="c16be-142">Selección de la ubicación</span><span class="sxs-lookup"><span data-stu-id="c16be-142">Choose the location</span></span>

<span data-ttu-id="c16be-143">La opción de ubicación proporciona una lista de las regiones en las que se ofrece IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c16be-143">The location option provides a list of the regions where IoT Hub is available.</span></span>

### <a name="create-the-iot-hub"></a><span data-ttu-id="c16be-144">Creación del Centro de IoT</span><span class="sxs-lookup"><span data-stu-id="c16be-144">Create the IoT hub</span></span>

<span data-ttu-id="c16be-145">Cuando se completen todos los pasos anteriores, ya se puede crear la instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c16be-145">When all previous steps are complete, you can create the IoT hub.</span></span> <span data-ttu-id="c16be-146">Haga clic en **Crear** para iniciar el proceso de back-end para crear e implementar la instancia de IoT Hub con las opciones elegidas.</span><span class="sxs-lookup"><span data-stu-id="c16be-146">Click **Create** to start the back-end process to create and deploy the IoT hub with the options you chose.</span></span>

<span data-ttu-id="c16be-147">La creación de IoT Hub puede tardar unos minutos, ya que la implementación back-end necesita tiempo para ejecutarse en los servidores de ubicación adecuados.</span><span class="sxs-lookup"><span data-stu-id="c16be-147">It can take a few minutes to create the IoT hub as it takes time for the back-end deployment to run on the appropriate location servers.</span></span>

## <a name="change-the-settings-of-the-iot-hub"></a><span data-ttu-id="c16be-148">Cambio de la configuración del Centro de IoT</span><span class="sxs-lookup"><span data-stu-id="c16be-148">Change the settings of the IoT hub</span></span>

<span data-ttu-id="c16be-149">Puede cambiar la configuración de un Centro de IoT después de crearlo desde la hoja Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c16be-149">You can change the settings of an existing IoT hub after it is created from the IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="c16be-150">**Directivas de acceso compartido**: estas directivas definen los permisos para que los dispositivos y servicios se conecten a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c16be-150">**Shared access policies**: These policies define the permissions for devices and services to connect to IoT Hub.</span></span> <span data-ttu-id="c16be-151">Para acceder a estas directivas, haga clic en **Directivas de acceso compartido** en **General**.</span><span class="sxs-lookup"><span data-stu-id="c16be-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="c16be-152">En esta hoja puede modificar las directivas existentes o agregar una nueva.</span><span class="sxs-lookup"><span data-stu-id="c16be-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="c16be-153">Para crear una directiva</span><span class="sxs-lookup"><span data-stu-id="c16be-153">Create a policy</span></span>

* <span data-ttu-id="c16be-154">Haga clic en **Agregar** para abrir una hoja.</span><span class="sxs-lookup"><span data-stu-id="c16be-154">Click **Add** to open a blade.</span></span> <span data-ttu-id="c16be-155">Aquí puede escribir el nombre de la nueva directiva y los permisos que quiere asociar a esta directiva, tal como se muestra en la siguiente ilustración:</span><span class="sxs-lookup"><span data-stu-id="c16be-155">Here you can enter the new policy name and the permissions that you want to associate with this policy, as shown in the following figure:</span></span>

    <span data-ttu-id="c16be-156">Hay varios permisos que se pueden asociar a estas directivas compartidas.</span><span class="sxs-lookup"><span data-stu-id="c16be-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="c16be-157">Las directivas **Lectura del Registro** y **Escritura del Registro** conceden derechos de acceso de lectura y escritura para el registro de identidades.</span><span class="sxs-lookup"><span data-stu-id="c16be-157">The **Registry read** and **Registry write** policies grant read and write access rights to the identity registry.</span></span> <span data-ttu-id="c16be-158">Si selecciona la opción de escritura, se elegirá automáticamente la opción de lectura.</span><span class="sxs-lookup"><span data-stu-id="c16be-158">Choosing the write option automatically chooses the read option.</span></span>

    <span data-ttu-id="c16be-159">La directiva **Conexión del servicio** concede permiso de acceso a los puntos de conexión de servicio como **Recepción del dispositivo a la nube**.</span><span class="sxs-lookup"><span data-stu-id="c16be-159">The **Service connect** policy grants permission to access service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="c16be-160">La directiva **Conexión del dispositivo** concede permisos para enviar y recibir mensajes con los puntos de conexión del dispositivo de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c16be-160">The **Device connect** policy grants permissions for sending and receiving messages using the IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="c16be-161">Haga clic en **Crear** para agregar la directiva recién creada a la lista existente.</span><span class="sxs-lookup"><span data-stu-id="c16be-161">Click **Create** to add this newly created policy to the existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="c16be-162">Puntos de conexión</span><span class="sxs-lookup"><span data-stu-id="c16be-162">Endpoints</span></span>

<span data-ttu-id="c16be-163">Haga clic en **Endpoints** (Puntos de conexión) para mostrar una lista de puntos de conexión para el centro de IoT que está modificando.</span><span class="sxs-lookup"><span data-stu-id="c16be-163">Click **Endpoints** to display a list of endpoints for the IoT hub that you are modifying.</span></span> <span data-ttu-id="c16be-164">Hay dos tipos de puntos de conexión: los integrados en el centro de IoT y los que agrega al centro de IoT después de crearlo.</span><span class="sxs-lookup"><span data-stu-id="c16be-164">There are two types of endpoints: endpoints that are built into the IoT hub, and endpoints that you add to the IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="c16be-165">Puntos de conexión integrados</span><span class="sxs-lookup"><span data-stu-id="c16be-165">Built-in endpoints</span></span>

<span data-ttu-id="c16be-166">Hay dos puntos de conexión integrados: **Cloud to device feedback** (Comentarios de la nube al dispositivo) y **Events** (Eventos).</span><span class="sxs-lookup"><span data-stu-id="c16be-166">There are two built-in endpoints: **Cloud to device feedback** and **Events**.</span></span>

* <span data-ttu-id="c16be-167">Configuración de **Cloud to device feedback** (Comentarios de la nube al dispositivo): esta configuración tiene dos opciones secundarias: **Cloud to Device TTL** (TTL de nube a dispositivo) (período de vida) y **Retention time** (Tiempo de retención) (en horas) para los mensajes.</span><span class="sxs-lookup"><span data-stu-id="c16be-167">**Cloud to device feedback** settings: This setting has two subsettings: **Cloud to Device TTL** (time-to-live) and **Retention time** (in hours) for the messages.</span></span> <span data-ttu-id="c16be-168">Al crear por primera vez un centro de IoT, ambas configuraciones tienen el valor predeterminado de una hora.</span><span class="sxs-lookup"><span data-stu-id="c16be-168">When your first create an IoT hub, both these settings have the default value of one hour.</span></span> <span data-ttu-id="c16be-169">Para ajustar la configuración, use los controles deslizantes o escriba los valores.</span><span class="sxs-lookup"><span data-stu-id="c16be-169">To adjust these settings, use the sliders or type the values.</span></span>
* <span data-ttu-id="c16be-170">Configuración de **Events** (Eventos): esta configuración tiene distintas opciones secundarias, algunas de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="c16be-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="c16be-171">Estas opciones secundarias se describen en la lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="c16be-171">The following list describes these settings:</span></span>

  * <span data-ttu-id="c16be-172">**Partitions** (Particiones): se establece un valor predeterminado cuando se crea el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c16be-172">**Partitions**: A default value is set when the IoT hub is created.</span></span> <span data-ttu-id="c16be-173">Esta opción permite cambiar el número de particiones.</span><span class="sxs-lookup"><span data-stu-id="c16be-173">You can change the number of partitions through this setting.</span></span>

  * <span data-ttu-id="c16be-174">**Punto de conexión y nombre compatible del Centro de eventos**: Cuando se crea IoT Hub, se crea internamente un Event Hub al que el usuario podría necesitar acceder en determinadas circunstancias.</span><span class="sxs-lookup"><span data-stu-id="c16be-174">**Event Hub-compatible name and endpoint**: When the IoT hub is created, an Event Hub is created internally that you may need access to under certain circumstances.</span></span> <span data-ttu-id="c16be-175">No se pueden personalizar los valores de nombre y punto de conexión compatibles con el centro de eventos, pero los puede copiar al hacer clic en **Copy** (Copiar).</span><span class="sxs-lookup"><span data-stu-id="c16be-175">You cannot customize the Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="c16be-176">**Retention Time** (Tiempo de retención): se establece en un día de forma predeterminada, pero se puede cambiar gracias a la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="c16be-176">**Retention Time**: Set to one day by default but you can change it using the drop-down list.</span></span> <span data-ttu-id="c16be-177">Este valor está en días para la configuración del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="c16be-177">This value is in days for the device-to-cloud setting.</span></span>

  * <span data-ttu-id="c16be-178">**Grupos de consumidores**: los grupos de consumidores permiten que varios lectores lean mensajes con independencia de la instancia de IoT Hub desde la que lo hagan.</span><span class="sxs-lookup"><span data-stu-id="c16be-178">**Consumer Groups**: Consumer groups enable multiple readers to read messages independently from the IoT hub.</span></span> <span data-ttu-id="c16be-179">Cada Centro de IoT se crea con un grupo de consumidores predeterminado.</span><span class="sxs-lookup"><span data-stu-id="c16be-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="c16be-180">Sin embargo, con esta configuración puede agregar o eliminar grupos de consumidores en los centros de IoT.</span><span class="sxs-lookup"><span data-stu-id="c16be-180">However, you can add or delete consumer groups to your IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c16be-181">El grupo de consumidores predeterminado no se puede modificar ni eliminar.</span><span class="sxs-lookup"><span data-stu-id="c16be-181">The default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="c16be-182">Puntos de conexión personalizados</span><span class="sxs-lookup"><span data-stu-id="c16be-182">Custom endpoints</span></span>

<span data-ttu-id="c16be-183">Puede agregar puntos de conexión personalizados al centro de IoT a través del portal.</span><span class="sxs-lookup"><span data-stu-id="c16be-183">You can add custom endpoints on your IoT hub using the portal.</span></span> <span data-ttu-id="c16be-184">En la hoja **Endpoints** (Puntos de conexión), haga clic en **Add** (Agregar) de la parte superior para abrir la hoja **Add endpoint** (Agregar punto de conexión).</span><span class="sxs-lookup"><span data-stu-id="c16be-184">From the **Endpoints** blade, click **Add** at the top to open the **Add endpoint** blade.</span></span> <span data-ttu-id="c16be-185">Escriba la información necesaria y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="c16be-185">Enter the required information, then click **OK**.</span></span> <span data-ttu-id="c16be-186">El punto de conexión personalizado aparecerá ahora en la hoja principal de **Endpoints** (Puntos de conexión).</span><span class="sxs-lookup"><span data-stu-id="c16be-186">Your custom endpoint is now listed in the main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="c16be-187">Puede leer más sobre los puntos de conexión personalizados en [Referencia: Puntos de conexión de IoT Hub][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="c16be-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="c16be-188">Rutas</span><span class="sxs-lookup"><span data-stu-id="c16be-188">Routes</span></span>

<span data-ttu-id="c16be-189">Haga clic en **Routes** (Rutas) para administrar el envío de mensajes del dispositivo a la nube de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c16be-189">Click **Routes** to manage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="c16be-190">Puede agregar rutas adicionales a su IoT Hub; para ello, haga clic en **Agregar** en la parte superior de la hoja **Rutas**, escriba la información necesaria y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c16be-190">You can add routes to your IoT hub by clicking **Add** at the top of the **Routes*** blade, entering the required information, and clicking **OK**.</span></span> <span data-ttu-id="c16be-191">La ruta aparecerá en la lista de la hoja principal de **Rutas**.</span><span class="sxs-lookup"><span data-stu-id="c16be-191">Your route is then listed in the main **Routes** blade.</span></span> <span data-ttu-id="c16be-192">Puede editar una ruta al hacer clic en ella en la lista de rutas.</span><span class="sxs-lookup"><span data-stu-id="c16be-192">You can edit a route by clicking it in the list of routes.</span></span> <span data-ttu-id="c16be-193">Para habilitar una ruta, haga clic en ella en la lista de rutas y establezca el control de alternancia de **Habilitar** en **Desactivado**.</span><span class="sxs-lookup"><span data-stu-id="c16be-193">To enable a route, click it in the list of routes and set the **Enabled** toggle to **Off**.</span></span> <span data-ttu-id="c16be-194">Para guardar los cambios, haga clic en **Aceptar** en la parte inferior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="c16be-194">To save the change, click **OK** at the bottom of the blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="c16be-195">Precios y escala</span><span class="sxs-lookup"><span data-stu-id="c16be-195">Pricing and scale</span></span>

<span data-ttu-id="c16be-196">El precio de un Centro de IoT existente se puede cambiar mediante la configuración **Precios** , con las siguientes excepciones:</span><span class="sxs-lookup"><span data-stu-id="c16be-196">The pricing of an existing IoT hub can be changed through the **Pricing** settings, with the following exceptions:</span></span>

* <span data-ttu-id="c16be-197">En la implementación actual, un Centro de IoT con una SKU gratuita no puede cambiar de nivel a una de las SKU de pago o viceversa.</span><span class="sxs-lookup"><span data-stu-id="c16be-197">In the current implementation, an IoT hub with a free SKU cannot change tiers to one of the paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="c16be-198">Solo puede haber un único IoT Hub de nivel Gratis en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c16be-198">There can only be one free tier IoT hub in the Azure subscription.</span></span>

![][12]

<span data-ttu-id="c16be-199">Puede cambiar de un nivel superior a uno inferior solo cuando el número de mensajes enviados ese día exceda la cuota del nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="c16be-199">You can move from a higher to lower tier only when the number of messages sent that day do exceed the quota for the lower tier.</span></span> <span data-ttu-id="c16be-200">Por ejemplo, si el número de mensajes por día supera los 400 000, se puede cambiar el nivel para IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c16be-200">For example, if the number of messages per day exceeds 400,000, then the tier for the IoT hub can be changed.</span></span> <span data-ttu-id="c16be-201">Sin embargo, si cambia al nivel S1, el centro de IoT está limitado durante ese día.</span><span class="sxs-lookup"><span data-stu-id="c16be-201">However, if you change to the S1 tier then the IoT hub is throttled for that day.</span></span>

## <a name="delete-the-iot-hub"></a><span data-ttu-id="c16be-202">Eliminación del Centro de IoT</span><span class="sxs-lookup"><span data-stu-id="c16be-202">Delete the IoT hub</span></span>

<span data-ttu-id="c16be-203">Puede examinar el Centro de IoT que desea eliminar haciendo clic en **Examinar**y, a continuación, seleccionar el centro adecuado que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="c16be-203">You can browse to the IoT hub you want to delete by clicking **Browse**, and then choosing the appropriate hub to delete.</span></span> <span data-ttu-id="c16be-204">Para eliminar la instancia de IoT Hub, haga clic en el botón **Eliminar** debajo del nombre de dicha instancia.</span><span class="sxs-lookup"><span data-stu-id="c16be-204">To delete the IoT hub, click the **Delete** button below the IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c16be-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c16be-205">Next steps</span></span>

<span data-ttu-id="c16be-206">Siga estos vínculos para más información sobre la administración del Centro de IoT de Azure:</span><span class="sxs-lookup"><span data-stu-id="c16be-206">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="c16be-207">[Administración masiva de dispositivos de IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="c16be-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="c16be-208">[Métricas de IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="c16be-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="c16be-209">[Supervisión de operaciones][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="c16be-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="c16be-210">Para explorar aún más las funcionalidades de IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="c16be-210">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="c16be-211">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="c16be-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="c16be-212">[Simular un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="c16be-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="c16be-213">[Protección total de la solución de IoT][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="c16be-213">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
