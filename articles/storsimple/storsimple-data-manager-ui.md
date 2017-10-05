---
title: Interfaz de usuario de Microsoft Azure StorSimple Data Manager | Microsoft Docs
description: "Describe cómo se usa la interfaz de usuario del servicio StorSimple Data Manager (versión preliminar privada)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 53a8599df2c647613122cd791b680e2e658586b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-using-the-storsimple-data-manager-service-ui-private-preview"></a><span data-ttu-id="6b6ce-103">Administración del uso de la interfaz de usuario del servicio StorSimple Data Manager (versión preliminar privada)</span><span class="sxs-lookup"><span data-stu-id="6b6ce-103">Manage using the StorSimple Data Manager service UI (Private Preview)</span></span>

<span data-ttu-id="6b6ce-104">En este artículo se explica cómo se puede usar la interfaz de usuario de StorSimple Data Manager para realizar la transformación de datos que residen en los dispositivos de la serie StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-104">This article explains how you can use the StorSimple Data Manager UI to perform data transformation on data residing on the StorSimple 8000 series devices.</span></span> <span data-ttu-id="6b6ce-105">Posteriormente, los datos transformados pueden consumirlos otros servicios de Azure, como Azure Media Services, Azure HDInsight, Azure Machine Learning y Azure Search.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-105">The transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span></span> 


## <a name="use-storsimple-data-transformation"></a><span data-ttu-id="6b6ce-106">Uso de transformación de datos de StorSimple</span><span class="sxs-lookup"><span data-stu-id="6b6ce-106">Use StorSimple Data Transformation</span></span>

<span data-ttu-id="6b6ce-107">StorSimple Data Manager es el recurso en el que se pueden crear instancias de transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-107">The StorSimple Data Manager is the resource within which Data Transformation can be instantiated.</span></span> <span data-ttu-id="6b6ce-108">El servicio de transformación de datos permite mover los datos de un dispositivo StorSimple local a blobs de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-108">The Data Transformation service lets you move data from your StorSimple on-premises device to blobs in Azure storage.</span></span> <span data-ttu-id="6b6ce-109">De ahí que en el flujo de trabajo sea preciso especificar los detalles del dispositivo StorSimple y los datos de interés que se desean mover a la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-109">Hence, in workflow you need to specify the details about your StorSimple device and the data of interest that you want to move to the storage account.</span></span>

### <a name="create-a-storsimple-data-manager-service"></a><span data-ttu-id="6b6ce-110">Creación de un servicio StorSimple Data Manager</span><span class="sxs-lookup"><span data-stu-id="6b6ce-110">Create a StorSimple Data Manager service</span></span>

<span data-ttu-id="6b6ce-111">Siga estos pasos para crear un servicio StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-111">Perform the following steps to create a StorSimple Data Manager service.</span></span>

1. <span data-ttu-id="6b6ce-112">Para crear un servicio StorSimple Data Manager, vaya a [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span><span class="sxs-lookup"><span data-stu-id="6b6ce-112">To create a StorSimple Data Manager service, go to [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span></span>

2. <span data-ttu-id="6b6ce-113">Haga clic en el icono **+** y busque StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-113">Click the **+** icon and search for StorSimple Data Manager.</span></span> <span data-ttu-id="6b6ce-114">Haga clic en el servicio StorSimple Data Manager y, después, en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="6b6ce-114">Click your StorSimple Data Manager service and then click **Create**.</span></span>

3. <span data-ttu-id="6b6ce-115">Si la suscripción está habilitada para la creación de este servicio, verá la siguiente hoja.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-115">If your subscription is enabled for creating this service, you see the following blade.</span></span>

    ![Creación de un recurso de StorSimple Data Manager](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. <span data-ttu-id="6b6ce-117">Escriba la información que debe introducir y haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="6b6ce-117">Enter the inputs and click **Create**.</span></span> <span data-ttu-id="6b6ce-118">La ubicación especificada debe ser la que aloje las cuentas de almacenamiento y el servicio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-118">The specified location should be the one that houses your storage accounts and your StorSimple Manager service.</span></span> <span data-ttu-id="6b6ce-119">Actualmente, solo se admiten las regiones oeste de EE. UU. y Europa occidental.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-119">Currently, only West US and West Europe regions are supported.</span></span> <span data-ttu-id="6b6ce-120">Por lo tanto, el servicio StorSimple Manager, el servicio Data Manager y la cuenta de almacenamiento asociada deben estar en las regiones admitidas anteriores.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-120">Hence, your StorSimple Manager service, Data Manager service, and the associated storage account should all be in the preceding supported regions.</span></span> <span data-ttu-id="6b6ce-121">El servicio tarda aproximadamente un minuto en crearse.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-121">It takes about a minute to create the service.</span></span>

### <a name="create-a-data-transformation-job-definition"></a><span data-ttu-id="6b6ce-122">Creación de una definición del trabajo de transformación de datos</span><span class="sxs-lookup"><span data-stu-id="6b6ce-122">Create a data transformation job definition</span></span>

<span data-ttu-id="6b6ce-123">En un servicio StorSimple Data Manager, es preciso crear una definición del trabajo de transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-123">Within a StorSimple Data Manager service, you need to create a data transformation job definition.</span></span> <span data-ttu-id="6b6ce-124">Una definición del trabajo especifica los detalles de los datos que esté interesado en mover a una cuenta de almacenamiento en el formato nativo.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-124">A job definition specifies details of the data that you are interested in moving into a storage account in the native format.</span></span> 

<span data-ttu-id="6b6ce-125">Realice los pasos siguientes para crear una nueva definición del trabajo de transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-125">Perform the following steps to create a new data transformation job definition.</span></span>

1.  <span data-ttu-id="6b6ce-126">Navegue hasta el servicio que ha creado.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-126">Navigate to the service that you created.</span></span> <span data-ttu-id="6b6ce-127">Haga clic en **+ Job Definition** (+ Definición de trabajo).</span><span class="sxs-lookup"><span data-stu-id="6b6ce-127">Click **+ Job Definition**.</span></span>

    ![Haga clic en + Job Definition (+ Definición de trabajo)](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. <span data-ttu-id="6b6ce-129">Se abre la hoja de definición de trabajo nueva.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-129">The new job definition blade opens up.</span></span> <span data-ttu-id="6b6ce-130">Asigne un nombre a la definición de trabajo y haga clic en **Origen**.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-130">Give your job definition a name and click **Source**.</span></span> <span data-ttu-id="6b6ce-131">En la hoja **Configurar origen de datos**, especifique los detalles del dispositivo StorSimple y los datos de interés.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-131">In the **Configure data source** blade, specify the details of your StorSimple device and the data of interest.</span></span>

    ![Creación de una definición de trabajo](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. <span data-ttu-id="6b6ce-133">Al ser un servicio Data Manager nuevo, no se configuran repositorios de datos.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-133">Since this is a new Data Manager service, no data repositories are configured.</span></span> <span data-ttu-id="6b6ce-134">Para agregar StorSimple Manager como un repositorio de datos, haga clic en **Add new** (Agregar nuevo) en la lista desplegable de repositorios de datos y, después, en **Add Data Repository** (Agregar repositorio de datos).</span><span class="sxs-lookup"><span data-stu-id="6b6ce-134">To add your StorSimple Manager as a data repository, click **Add new** in the data repository dropdown and then click **Add Data Repository**.</span></span>

4. <span data-ttu-id="6b6ce-135">Elija **StorSimple 8000 series Manager** como tipo de repositorio y especifique las propiedades de **StorSimple Manager**.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-135">Choose **StorSimple 8000 series Manager** as the repository type and enter the properties of your **StorSimple Manager**.</span></span> <span data-ttu-id="6b6ce-136">En el campo **Resource Id** (Id. de recurso), es preciso escribir el número delante del signo **:** en la clave de registro de StorSimple manager.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-136">For the **Resource Id** field, you need to enter the number before the **:** in the registration key of your StorSimple manager.</span></span>

    ![Creación de un origen de datos](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  <span data-ttu-id="6b6ce-138">Pulse **OK** (Aceptar) cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-138">Click **OK** when done.</span></span> <span data-ttu-id="6b6ce-139">Esto guarda el repositorio de datos y StorSimple Manager se pueden reutilizar en otras definiciones de trabajo sin tener que volver a escribir estos parámetros.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-139">This saves your data repository and this StorSimple Manager can be reused in other job definitions without entering these parameters again.</span></span> <span data-ttu-id="6b6ce-140">Unos segundos después de hacer clic en **OK** (Aceptar) StorSimple Manager aparece en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-140">It takes a few seconds after you click **OK** for the StorSimple Manager to show up in the dropdown.</span></span>

6.  <span data-ttu-id="6b6ce-141">En la hoja **Configurar origen de datos**, escriba el nombre del dispositivo y el nombre del volumen que tiene los datos que le interesan.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-141">In the **Configure data source** blade, enter the device name and the volume name that has your data of interest.</span></span>

7.  <span data-ttu-id="6b6ce-142">En la subsección **Filtro**, escriba el directorio raíz que contiene los datos de interés (el campo debe empezar por una barra inclinada `\`).</span><span class="sxs-lookup"><span data-stu-id="6b6ce-142">In the **Filter** subsection, enter the root directory that contains your data of interest (this field should start with a `\`).</span></span> <span data-ttu-id="6b6ce-143">Aquí también se pueden agregar los filtros de archivo.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-143">You can also add any file filters here.</span></span>

8.  <span data-ttu-id="6b6ce-144">El servicio de transformación de datos funciona en los datos que se insertan en Azure a través de instantáneas.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-144">The data transformation service works on the data that is pushed up to the Azure via snapshots.</span></span> <span data-ttu-id="6b6ce-145">Al ejecutar este trabajo, puede elegir realizar una copia de seguridad cada vez que se ejecuta este trabajo (para trabajar con los datos más recientes) o utilizar la última copia de seguridad existente en la nube (si trabaja con datos archivados).</span><span class="sxs-lookup"><span data-stu-id="6b6ce-145">When running this job, you can choose to take a backup every time this job is run (to work on latest data) or to use the last existing backup in the cloud (if you are working on some archived data).</span></span>

    ![Detalles del origen de datos nuevo](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. <span data-ttu-id="6b6ce-147">A continuación, es preciso configurar los valores del destino.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-147">Next, the Target settings need to be configured.</span></span> <span data-ttu-id="6b6ce-148">Se admiten dos 2 tipos de destinos: cuentas de Azure Storage y cuentas de Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-148">There are 2 types of supported targets – Azure Storage accounts and Azure Media Services accounts.</span></span> <span data-ttu-id="6b6ce-149">Elija el primero si desea colocar los archivos en blobs de esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-149">Choose storage accounts to put files into blobs in that account.</span></span> <span data-ttu-id="6b6ce-150">Elija el segundo si desea colocar los archivos en recursos de esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-150">Choose media services account to put files into assets in that account.</span></span> <span data-ttu-id="6b6ce-151">Una vez más, es preciso agregar un repositorio.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-151">Again, we need to add a repository.</span></span> <span data-ttu-id="6b6ce-152">En la lista desplegable, seleccione **Agregar nuevo** y, después, **Parámetros de configuración**.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-152">In the dropdown, select **Add new** and then **Configure settings**.</span></span>

    ![Crear el receptor de datos](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. <span data-ttu-id="6b6ce-154">Aquí puede seleccionar el tipo de repositorio que desea agregar y los restantes parámetros asociados con el repositorio.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-154">Here, you can select the type of repository you want to add and the other parameters associated with the repository.</span></span> <span data-ttu-id="6b6ce-155">En ambos casos, cuando se ejecuta el trabajo se crea una cola de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-155">In both cases, a storage queue is created when the job runs.</span></span> <span data-ttu-id="6b6ce-156">Esta cola se rellena con mensajes de los blobs transformados a medida que están listos.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-156">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="6b6ce-157">El nombre de esta cola es el mismo que el de la definición del trabajo.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-157">The name of this queue is the same as the name of the job definition.</span></span> <span data-ttu-id="6b6ce-158">Si selecciona **Media Services** como tipo de repositorio, también puede especificar las credenciales de la cuenta de almacenamiento en que se crea la cola.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-158">If you select **Media Services** as the repo type, then you can also enter storage account credentials where the queue is created.</span></span>

    ![Detalles del receptor de datos nuevo](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. <span data-ttu-id="6b6ce-160">Después de agregar el repositorio de datos (se tarda unos segundos), encontrará el repositorio en la lista desplegable de **Target account name** (Nombre de cuenta de destino).</span><span class="sxs-lookup"><span data-stu-id="6b6ce-160">After adding the data repository (which takes a few seconds), you will find the repo in the dropdown in the **Target account name**.</span></span>  <span data-ttu-id="6b6ce-161">Elija el destino que necesita.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-161">Choose the target that you need.</span></span>

12. <span data-ttu-id="6b6ce-162">Haga clic en **OK** (Aceptar) para crear la definición del trabajo.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-162">Click **OK** to create the job definition.</span></span> <span data-ttu-id="6b6ce-163">La definición de trabajo ya está configurada.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-163">Your job definition is now set up.</span></span> <span data-ttu-id="6b6ce-164">Esta definición de trabajo se puede usar varias veces a través de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-164">You can use this job definition multiple times via the UI.</span></span>

    ![Agregar una definición de trabajo nueva](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-the-job-definition"></a><span data-ttu-id="6b6ce-166">Ejecución de la definición de trabajo</span><span class="sxs-lookup"><span data-stu-id="6b6ce-166">Run the job definition</span></span>

<span data-ttu-id="6b6ce-167">Siempre que tenga que mover los datos de StorSimple a la cuenta de almacenamiento que ha especificado en la definición del trabajo, será preciso que la invoque.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-167">Whenever you need to move data from StorSimple to the storage account that you have specified in the job definition, you will need to invoke it.</span></span> <span data-ttu-id="6b6ce-168">Hay cierta flexibilidad a la hora de cambiar los parámetros cada vez que se invoca el trabajo.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-168">There is some flexibility in changing the parameters every time you invoke the job.</span></span> <span data-ttu-id="6b6ce-169">Los pasos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="6b6ce-169">The steps are as follows:</span></span>

1. <span data-ttu-id="6b6ce-170">Seleccione el servicio StorSimple Data Manager y vaya a **Monitoring** (Supervisión).</span><span class="sxs-lookup"><span data-stu-id="6b6ce-170">Select your StorSimple Data Manager service and go to **Monitoring**.</span></span> <span data-ttu-id="6b6ce-171">Haga clic en **Run now** (Ejecutar ahora).</span><span class="sxs-lookup"><span data-stu-id="6b6ce-171">Click **Run Now**.</span></span>

    ![Desencadenar la definición de trabajo](./media/storsimple-data-manager-ui/run-now.png)

2. <span data-ttu-id="6b6ce-173">Elija la definición de trabajo que desea ejecutar.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-173">Choose the job definition that you want to run.</span></span> <span data-ttu-id="6b6ce-174">Haga clic en **Ejecutar Configuración** para modificar los parámetros que desea cambiar para la ejecución de este trabajo.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-174">Click **Run settings** to modify any settings that you might want to change for this job run.</span></span>

    ![Ejecutar configuración de trabajo](./media/storsimple-data-manager-ui/run-settings.png)

3. <span data-ttu-id="6b6ce-176">Haga clic en **Aceptar** y, luego, haga clic en **Ejecutar** para iniciar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-176">Click **OK** and then click **Run** to launch your job.</span></span> <span data-ttu-id="6b6ce-177">Para supervisar este trabajo, vaya a la página **Jobs** (Trabajos) de StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-177">To monitor this job, go to the **Jobs** page in your StorSimple Data Manager.</span></span>

    ![Lista y estado de los trabajos](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. <span data-ttu-id="6b6ce-179">Además de la supervisión de la hoja **Trabajos**, también puede escuchar la cola de almacenamiento a la que se agrega un mensaje cada vez que se mueve un archivo desde StorSimple a la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="6b6ce-179">In addition to monitoring in the **Jobs** blade, you can also listen on the storage queue where a message is added every time a file is moved from StorSimple to the storage account.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6b6ce-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6b6ce-180">Next steps</span></span>

<span data-ttu-id="6b6ce-181">[Use the .Net SDK to initiate data transformation](storsimple-data-manager-dotnet-jobs.md) (Uso del SDK de .NET para iniciar la transformación de datos).</span><span class="sxs-lookup"><span data-stu-id="6b6ce-181">[Use .NET SDK to launch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span></span>