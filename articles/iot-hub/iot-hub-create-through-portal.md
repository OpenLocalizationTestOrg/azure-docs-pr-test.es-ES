---
title: aaaUse Hola toocreate portal Azure de un centro de IoT | Documentos de Microsoft
description: "Cómo toocreate, administrar y eliminar centros de IoT de Azure a través de hello portal de Azure. Incluye información sobre los niveles de precios, el escalado, la seguridad y la configuración de la mensajería."
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
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a><span data-ttu-id="124c7-104">Crear un centro de IoT con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="124c7-104">Create an IoT hub using hello Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="124c7-105">En este artículo se describe:</span><span class="sxs-lookup"><span data-stu-id="124c7-105">This article describes:</span></span>

* <span data-ttu-id="124c7-106">¿Cómo toofind Hola servicio del centro de IoT Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="124c7-106">How toofind hello IoT Hub service in hello Azure portal.</span></span>
* <span data-ttu-id="124c7-107">¿Cómo toocreate y administrar centros de IoT.</span><span class="sxs-lookup"><span data-stu-id="124c7-107">How toocreate and manage IoT hubs.</span></span>

## <a name="where-toofind-hello-iot-hub-service"></a><span data-ttu-id="124c7-108">Donde toofind Hola servicio del centro de IoT</span><span class="sxs-lookup"><span data-stu-id="124c7-108">Where toofind hello IoT Hub service</span></span>

<span data-ttu-id="124c7-109">Puede encontrar Hola servicio del centro de IoT Hola ubicaciones en el portal de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="124c7-109">You can find hello IoT Hub service in hello following locations in hello portal:</span></span>

* <span data-ttu-id="124c7-110">Elija **+ Nuevo** y después **Internet de las cosas**.</span><span class="sxs-lookup"><span data-stu-id="124c7-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="124c7-111">Hola Marketplace, elija **Internet de las cosas**.</span><span class="sxs-lookup"><span data-stu-id="124c7-111">In hello Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="124c7-112">Crear un centro de IoT</span><span class="sxs-lookup"><span data-stu-id="124c7-112">Create an IoT hub</span></span>

<span data-ttu-id="124c7-113">Puede crear un centro de IoT con hello siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="124c7-113">You can create an IoT hub using hello following methods:</span></span>

* <span data-ttu-id="124c7-114">Hola **+ nuevo** opción abre una hoja de Hola se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="124c7-114">hello **+ New** option opens hello blade shown in hello following screen shot.</span></span> <span data-ttu-id="124c7-115">Hola pasos para crear el centro de IoT de Hola a través de este método y a través de marketplace de hello son idénticos.</span><span class="sxs-lookup"><span data-stu-id="124c7-115">hello steps for creating hello IoT hub through this method and through hello marketplace are identical.</span></span>
* <span data-ttu-id="124c7-116">Hola Marketplace, elija **crear** hoja de hello tooopen se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="124c7-116">In hello Marketplace, choose **Create** tooopen hello blade shown in hello following screen shot.</span></span>

<span data-ttu-id="124c7-117">Hello las secciones siguientes describen Hola varios pasos toocreate un centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="124c7-117">hello following sections describe hello several steps toocreate an IoT hub:</span></span>

### <a name="choose-hello-name-of-hello-iot-hub"></a><span data-ttu-id="124c7-118">Elegir nombre de Hola de centro de IoT Hola</span><span class="sxs-lookup"><span data-stu-id="124c7-118">Choose hello name of hello IoT hub</span></span>

<span data-ttu-id="124c7-119">toocreate un centro de IoT, debe asignar un nombre centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="124c7-119">toocreate an IoT hub, you must name hello IoT hub.</span></span> <span data-ttu-id="124c7-120">Este nombre debe ser exclusivo para distinguirlo en todas las instancias de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="124c7-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a><span data-ttu-id="124c7-121">Elija el nivel de precios de Hola</span><span class="sxs-lookup"><span data-stu-id="124c7-121">Choose hello pricing tier</span></span>

<span data-ttu-id="124c7-122">Puede elegir entre cuatro niveles: **Gratis**, **Estándar 1**, **Estándar 2** y **Estándar S3**.</span><span class="sxs-lookup"><span data-stu-id="124c7-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="124c7-123">nivel gratis Hola permite sólo 500 toobe dispositivos conectados toohello centro de IoT y sube too8, 000 mensajes al día.</span><span class="sxs-lookup"><span data-stu-id="124c7-123">hello free tier allows only 500 devices toobe connected toohello IoT hub and up too8,000 messages per day.</span></span>

<span data-ttu-id="124c7-124">**Estándar S1**: edición de hello S1 de uso para las soluciones de IoT con un gran número de dispositivos que cada uno de ellos genera pequeñas cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="124c7-124">**Standard S1**: Use hello S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="124c7-125">Permite que cada unidad de edición de hello S1 un too400, 000 mensajes al día a través de todos los dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="124c7-125">Each unit of hello S1 edition allows up too400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="124c7-126">**Estándar S2**: edición de hello S2 de uso para las soluciones de IoT en el que los dispositivos generar grandes cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="124c7-126">**Standard S2**: Use hello S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="124c7-127">Permite que cada unidad de edición de hello S2 un too6 millones de mensajes al día entre todos los dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="124c7-127">Each unit of hello S2 edition allows up too6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="124c7-128">**Estándar S3**: edición de hello S3 de uso para las soluciones de IoT que generan un gran volumen de datos.</span><span class="sxs-lookup"><span data-stu-id="124c7-128">**Standard S3**: Use hello S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="124c7-129">Permite que cada unidad de edición de S3 Hola un too300 millones de mensajes al día entre todos los dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="124c7-129">Each unit of hello S3 edition allows up too300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="124c7-130">IoT Hub solo permite un único centro gratuito por suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="124c7-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="124c7-131">Unidades del Centro de IoT</span><span class="sxs-lookup"><span data-stu-id="124c7-131">IoT hub units</span></span>

<span data-ttu-id="124c7-132">número de Hello permitido por unidad al día de mensajes depende de nivel de precios de la base de datos central.</span><span class="sxs-lookup"><span data-stu-id="124c7-132">hello number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="124c7-133">Por ejemplo, si desea hello toosupport entrada de centro de IoT de 700 000 mensajes, elija dos unidades de nivel de S1.</span><span class="sxs-lookup"><span data-stu-id="124c7-133">For example, if you want hello IoT hub toosupport ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-toocloud-partitions-and-resource-group"></a><span data-ttu-id="124c7-134">Las particiones toocloud del dispositivo y el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="124c7-134">Device toocloud partitions and resource group</span></span>

<span data-ttu-id="124c7-135">Puede cambiar el número de Hola de particiones para un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="124c7-135">You can change hello number of partitions for an IoT hub.</span></span> <span data-ttu-id="124c7-136">número de particiones de Hello predeterminado es 4, puede elegir un número diferente de la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="124c7-136">hello default number of partitions is 4, you can choose a different number from hello drop-down list.</span></span>

<span data-ttu-id="124c7-137">No es necesario tooexplicitly crear un grupo de recursos vacío.</span><span class="sxs-lookup"><span data-stu-id="124c7-137">You do not need tooexplicitly create an empty resource group.</span></span> <span data-ttu-id="124c7-138">Cuando se crea un recurso, puede elegir cualquier toocreate un nuevo o usar un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="124c7-138">When you create a resource, you can choose either toocreate a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="124c7-139">Elección de la suscripción</span><span class="sxs-lookup"><span data-stu-id="124c7-139">Choose subscription</span></span>

<span data-ttu-id="124c7-140">Centro de IoT de Azure Hola de listas de cuenta de usuario de las suscripciones de Azure Hola se vincula automáticamente a.</span><span class="sxs-lookup"><span data-stu-id="124c7-140">Azure IoT Hub automatically lists hello Azure subscriptions hello user account is linked to.</span></span> <span data-ttu-id="124c7-141">Puede elegir el centro de IoT de hello suscripción de Azure tooassociate Hola a.</span><span class="sxs-lookup"><span data-stu-id="124c7-141">You can choose hello Azure subscription tooassociate hello IoT hub to.</span></span>

### <a name="choose-hello-location"></a><span data-ttu-id="124c7-142">Elegir ubicación de Hola</span><span class="sxs-lookup"><span data-stu-id="124c7-142">Choose hello location</span></span>

<span data-ttu-id="124c7-143">opción de ubicación de Hello proporciona una lista de regiones de Hola donde centro de IoT no está disponible.</span><span class="sxs-lookup"><span data-stu-id="124c7-143">hello location option provides a list of hello regions where IoT Hub is available.</span></span>

### <a name="create-hello-iot-hub"></a><span data-ttu-id="124c7-144">Crear centro de IoT Hola</span><span class="sxs-lookup"><span data-stu-id="124c7-144">Create hello IoT hub</span></span>

<span data-ttu-id="124c7-145">Una vez completados todos los pasos anteriores, puede crear centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="124c7-145">When all previous steps are complete, you can create hello IoT hub.</span></span> <span data-ttu-id="124c7-146">Haga clic en **crear** toostart Hola proceso back-end toocreate e implementar centro de IoT Hola con opciones de Hola que haya elegido.</span><span class="sxs-lookup"><span data-stu-id="124c7-146">Click **Create** toostart hello back-end process toocreate and deploy hello IoT hub with hello options you chose.</span></span>

<span data-ttu-id="124c7-147">Centro de IoT Hola de unos minutos toocreate puede tardar como tarda toorun de implementación de back-end de hello en los servidores de la ubicación apropiada de Hola.</span><span class="sxs-lookup"><span data-stu-id="124c7-147">It can take a few minutes toocreate hello IoT hub as it takes time for hello back-end deployment toorun on hello appropriate location servers.</span></span>

## <a name="change-hello-settings-of-hello-iot-hub"></a><span data-ttu-id="124c7-148">Cambiar la configuración de Hola de centro de IoT Hola</span><span class="sxs-lookup"><span data-stu-id="124c7-148">Change hello settings of hello IoT hub</span></span>

<span data-ttu-id="124c7-149">Puede cambiar configuración de Hola de un centro de IoT existente después de que se crea a partir de la hoja de centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="124c7-149">You can change hello settings of an existing IoT hub after it is created from hello IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="124c7-150">**Directivas de acceso compartido**: estas directivas definen los permisos de Hola para dispositivos y servicios tooIoT tooconnect concentrador.</span><span class="sxs-lookup"><span data-stu-id="124c7-150">**Shared access policies**: These policies define hello permissions for devices and services tooconnect tooIoT Hub.</span></span> <span data-ttu-id="124c7-151">Para acceder a estas directivas, haga clic en **Directivas de acceso compartido** en **General**.</span><span class="sxs-lookup"><span data-stu-id="124c7-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="124c7-152">En esta hoja puede modificar las directivas existentes o agregar una nueva.</span><span class="sxs-lookup"><span data-stu-id="124c7-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="124c7-153">Para crear una directiva</span><span class="sxs-lookup"><span data-stu-id="124c7-153">Create a policy</span></span>

* <span data-ttu-id="124c7-154">Haga clic en **agregar** tooopen una hoja.</span><span class="sxs-lookup"><span data-stu-id="124c7-154">Click **Add** tooopen a blade.</span></span> <span data-ttu-id="124c7-155">Aquí puede escribir el nuevo nombre de directiva de Hola y permisos Hola desea tooassociate con esta directiva, tal y como se muestra en hello siguiente figura:</span><span class="sxs-lookup"><span data-stu-id="124c7-155">Here you can enter hello new policy name and hello permissions that you want tooassociate with this policy, as shown in hello following figure:</span></span>

    <span data-ttu-id="124c7-156">Hay varios permisos que se pueden asociar a estas directivas compartidas.</span><span class="sxs-lookup"><span data-stu-id="124c7-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="124c7-157">Hola **lectura del registro** y **escritura del registro** directivas conceden lectura y el registro de identidad de toohello de derechos de acceso de escritura.</span><span class="sxs-lookup"><span data-stu-id="124c7-157">hello **Registry read** and **Registry write** policies grant read and write access rights toohello identity registry.</span></span> <span data-ttu-id="124c7-158">Elegir la opción de escritura de hello automáticamente elige Hola lee opción.</span><span class="sxs-lookup"><span data-stu-id="124c7-158">Choosing hello write option automatically chooses hello read option.</span></span>

    <span data-ttu-id="124c7-159">Hola **servicio conectar** directiva concede permiso tooaccess los extremos de servicio como **dispositivo a la nube de recepción**.</span><span class="sxs-lookup"><span data-stu-id="124c7-159">hello **Service connect** policy grants permission tooaccess service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="124c7-160">Hola **dispositivo conectar** directiva concede permisos para enviar y recibir mensajes mediante los puntos de conexión de hello centro de IoT del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="124c7-160">hello **Device connect** policy grants permissions for sending and receiving messages using hello IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="124c7-161">Haga clic en **crear** tooadd este recién creado lista existente de directiva toohello.</span><span class="sxs-lookup"><span data-stu-id="124c7-161">Click **Create** tooadd this newly created policy toohello existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="124c7-162">Puntos de conexión</span><span class="sxs-lookup"><span data-stu-id="124c7-162">Endpoints</span></span>

<span data-ttu-id="124c7-163">Haga clic en **extremos** toodisplay una lista de extremos de centro de IoT de Hola que va a modificar.</span><span class="sxs-lookup"><span data-stu-id="124c7-163">Click **Endpoints** toodisplay a list of endpoints for hello IoT hub that you are modifying.</span></span> <span data-ttu-id="124c7-164">Hay dos tipos de puntos de conexión: puntos de conexión que se integran en el centro de IoT de Hola y extremos que agregue centro de IoT toohello después de su creación.</span><span class="sxs-lookup"><span data-stu-id="124c7-164">There are two types of endpoints: endpoints that are built into hello IoT hub, and endpoints that you add toohello IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="124c7-165">Puntos de conexión integrados</span><span class="sxs-lookup"><span data-stu-id="124c7-165">Built-in endpoints</span></span>

<span data-ttu-id="124c7-166">Hay dos puntos de conexión integrados: **toodevice comentarios en la nube** y **eventos**.</span><span class="sxs-lookup"><span data-stu-id="124c7-166">There are two built-in endpoints: **Cloud toodevice feedback** and **Events**.</span></span>

* <span data-ttu-id="124c7-167">**Toodevice comentarios en la nube** configuración: esta opción no tiene dos subsettings: **tooDevice TTL en la nube** (período de vida) y **tiempo de retención** (en horas) para mensajes de saludo.</span><span class="sxs-lookup"><span data-stu-id="124c7-167">**Cloud toodevice feedback** settings: This setting has two subsettings: **Cloud tooDevice TTL** (time-to-live) and **Retention time** (in hours) for hello messages.</span></span> <span data-ttu-id="124c7-168">Cuando el primer crea un centro de IoT, ambas configuraciones tienen valor predeterminado de Hola de una hora.</span><span class="sxs-lookup"><span data-stu-id="124c7-168">When your first create an IoT hub, both these settings have hello default value of one hour.</span></span> <span data-ttu-id="124c7-169">tooadjust estas opciones, utilice los controles deslizantes de Hola o escriba los valores de hello.</span><span class="sxs-lookup"><span data-stu-id="124c7-169">tooadjust these settings, use hello sliders or type hello values.</span></span>
* <span data-ttu-id="124c7-170">Configuración de **Events** (Eventos): esta configuración tiene distintas opciones secundarias, algunas de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="124c7-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="124c7-171">Hola lista siguiente describe estas opciones:</span><span class="sxs-lookup"><span data-stu-id="124c7-171">hello following list describes these settings:</span></span>

  * <span data-ttu-id="124c7-172">**Las particiones**: se establece un valor predeterminado cuando se crea el centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="124c7-172">**Partitions**: A default value is set when hello IoT hub is created.</span></span> <span data-ttu-id="124c7-173">Puede cambiar Hola número de particiones a través de esta configuración.</span><span class="sxs-lookup"><span data-stu-id="124c7-173">You can change hello number of partitions through this setting.</span></span>

  * <span data-ttu-id="124c7-174">**Nombre de evento compatible con el centro y el extremo**: cuando se crea el centro de IoT hello, un concentrador de eventos lo creó internamente que puede necesita acceder a toounder determinadas circunstancias.</span><span class="sxs-lookup"><span data-stu-id="124c7-174">**Event Hub-compatible name and endpoint**: When hello IoT hub is created, an Event Hub is created internally that you may need access toounder certain circumstances.</span></span> <span data-ttu-id="124c7-175">No se pueden personalizar los valores de nombre y el extremo de hello compatible con el concentrador de eventos, pero se puede copiar, haga clic en **copia**.</span><span class="sxs-lookup"><span data-stu-id="124c7-175">You cannot customize hello Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="124c7-176">**Tiempo de retención**: establecer tooone día de forma predeterminada, pero puede cambiarlo mediante la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="124c7-176">**Retention Time**: Set tooone day by default but you can change it using hello drop-down list.</span></span> <span data-ttu-id="124c7-177">Este valor está en días para la configuración de dispositivo para la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="124c7-177">This value is in days for hello device-to-cloud setting.</span></span>

  * <span data-ttu-id="124c7-178">**Grupos de consumidores**: grupos de consumidores habilitar varios mensajes de tooread lectores independientemente de centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="124c7-178">**Consumer Groups**: Consumer groups enable multiple readers tooread messages independently from hello IoT hub.</span></span> <span data-ttu-id="124c7-179">Cada Centro de IoT se crea con un grupo de consumidores predeterminado.</span><span class="sxs-lookup"><span data-stu-id="124c7-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="124c7-180">Sin embargo, puede agregar o eliminar centros de IoT consumidor grupos tooyour con esta configuración.</span><span class="sxs-lookup"><span data-stu-id="124c7-180">However, you can add or delete consumer groups tooyour IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="124c7-181">grupo de consumidores de Hello predeterminado no se pueden modificar ni eliminar.</span><span class="sxs-lookup"><span data-stu-id="124c7-181">hello default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="124c7-182">Puntos de conexión personalizados</span><span class="sxs-lookup"><span data-stu-id="124c7-182">Custom endpoints</span></span>

<span data-ttu-id="124c7-183">Puede agregar extremos personalizados en el centro de IoT mediante el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="124c7-183">You can add custom endpoints on your IoT hub using hello portal.</span></span> <span data-ttu-id="124c7-184">De hello **extremos** hoja, haga clic en **agregar** en Hola tooopen superior Hola **Agregar extremo** hoja.</span><span class="sxs-lookup"><span data-stu-id="124c7-184">From hello **Endpoints** blade, click **Add** at hello top tooopen hello **Add endpoint** blade.</span></span> <span data-ttu-id="124c7-185">Escriba información de hello necesario, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="124c7-185">Enter hello required information, then click **OK**.</span></span> <span data-ttu-id="124c7-186">El punto de conexión personalizado aparece ahora en hello principal **extremos** hoja.</span><span class="sxs-lookup"><span data-stu-id="124c7-186">Your custom endpoint is now listed in hello main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="124c7-187">Puede leer más sobre los puntos de conexión personalizados en [Referencia: Puntos de conexión de IoT Hub][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="124c7-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="124c7-188">Rutas</span><span class="sxs-lookup"><span data-stu-id="124c7-188">Routes</span></span>

<span data-ttu-id="124c7-189">Haga clic en **rutas** toomanage cómo centro de IoT envía los mensajes del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="124c7-189">Click **Routes** toomanage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="124c7-190">Puede agregar el centro de IoT de rutas tooyour haciendo clic en **agregar** en parte superior de Hola de hello **rutas*** hoja, especificar información de hello necesario y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="124c7-190">You can add routes tooyour IoT hub by clicking **Add** at hello top of hello **Routes*** blade, entering hello required information, and clicking **OK**.</span></span> <span data-ttu-id="124c7-191">La ruta, a continuación, se muestra en hello principal **rutas** hoja.</span><span class="sxs-lookup"><span data-stu-id="124c7-191">Your route is then listed in hello main **Routes** blade.</span></span> <span data-ttu-id="124c7-192">Puede editar una ruta haciendo clic en él en la lista de Hola de rutas.</span><span class="sxs-lookup"><span data-stu-id="124c7-192">You can edit a route by clicking it in hello list of routes.</span></span> <span data-ttu-id="124c7-193">tooenable una ruta, haga clic en él en la lista de Hola de rutas y establezca hello **habilitado** alternar demasiado**desactivar**.</span><span class="sxs-lookup"><span data-stu-id="124c7-193">tooenable a route, click it in hello list of routes and set hello **Enabled** toggle too**Off**.</span></span> <span data-ttu-id="124c7-194">cambio de hello toosave, haga clic en **Aceptar** final Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="124c7-194">toosave hello change, click **OK** at hello bottom of hello blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="124c7-195">Precios y escala</span><span class="sxs-lookup"><span data-stu-id="124c7-195">Pricing and scale</span></span>

<span data-ttu-id="124c7-196">Hola de precios de un centro de IoT existente pueden cambiarse a través de hello **precios** configuración con hello siguientes excepciones:</span><span class="sxs-lookup"><span data-stu-id="124c7-196">hello pricing of an existing IoT hub can be changed through hello **Pricing** settings, with hello following exceptions:</span></span>

* <span data-ttu-id="124c7-197">En la implementación actual de hello, un centro de IoT a una SKU libre no puede cambiar tooone de niveles de hello SKU, de pago, o viceversa.</span><span class="sxs-lookup"><span data-stu-id="124c7-197">In hello current implementation, an IoT hub with a free SKU cannot change tiers tooone of hello paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="124c7-198">Solo puede haber un centro de IoT de nivel gratuito en hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="124c7-198">There can only be one free tier IoT hub in hello Azure subscription.</span></span>

![][12]

<span data-ttu-id="124c7-199">Puede mover de un nivel superior de toolower sólo cuando el número Hola de mensajes enviados a ese día superar la cuota de hello para el nivel inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="124c7-199">You can move from a higher toolower tier only when hello number of messages sent that day do exceed hello quota for hello lower tier.</span></span> <span data-ttu-id="124c7-200">Por ejemplo, si número Hola de mensajes al día supera 400.000, Hola nivel para hello IoT hub puede cambiarse.</span><span class="sxs-lookup"><span data-stu-id="124c7-200">For example, if hello number of messages per day exceeds 400,000, then hello tier for hello IoT hub can be changed.</span></span> <span data-ttu-id="124c7-201">Sin embargo, si cambia el nivel de S1 toohello centro de IoT Hola está limitado durante ese día.</span><span class="sxs-lookup"><span data-stu-id="124c7-201">However, if you change toohello S1 tier then hello IoT hub is throttled for that day.</span></span>

## <a name="delete-hello-iot-hub"></a><span data-ttu-id="124c7-202">Eliminar el centro de IoT Hola</span><span class="sxs-lookup"><span data-stu-id="124c7-202">Delete hello IoT hub</span></span>

<span data-ttu-id="124c7-203">Puede examinar desee toodelete haciendo clic en el centro de IoT de toohello **examinar**, y, a continuación, elegir Hola toodelete concentrador adecuado.</span><span class="sxs-lookup"><span data-stu-id="124c7-203">You can browse toohello IoT hub you want toodelete by clicking **Browse**, and then choosing hello appropriate hub toodelete.</span></span> <span data-ttu-id="124c7-204">toodelete Hola centro de IoT, haga clic en hello **eliminar** botón situado debajo del nombre del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="124c7-204">toodelete hello IoT hub, click hello **Delete** button below hello IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="124c7-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="124c7-205">Next steps</span></span>

<span data-ttu-id="124c7-206">Siga estos toolearn de vínculos más acerca de cómo administrar el centro de IoT de Azure:</span><span class="sxs-lookup"><span data-stu-id="124c7-206">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="124c7-207">[Administración masiva de dispositivos de IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="124c7-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="124c7-208">[Métricas de IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="124c7-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="124c7-209">[Supervisión de operaciones][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="124c7-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="124c7-210">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="124c7-210">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="124c7-211">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="124c7-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="124c7-212">[Simular un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="124c7-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="124c7-213">[Proteger la solución de IoT de hello masa][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="124c7-213">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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
