---
title: "Adición del conector de OneDrive a Logic Apps | Microsoft Docs"
description: "Información general del conector de OneDrive con parámetros de la API de REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 63bd33bf4e09b98aa53dcfec9fcc4a0109204952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-onedrive-connector"></a><span data-ttu-id="64e00-103">Introducción al conector de OneDrive</span><span class="sxs-lookup"><span data-stu-id="64e00-103">Get started with the OneDrive connector</span></span>
<span data-ttu-id="64e00-104">Conéctese a OneDrive para administrar los archivos, incluyendo las tareas de carga, obtención y eliminación de archivos, y muchas más.</span><span class="sxs-lookup"><span data-stu-id="64e00-104">Connect to OneDrive to manage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="64e00-105">Con OneDrive, puede:</span><span class="sxs-lookup"><span data-stu-id="64e00-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="64e00-106">Crear un flujo de trabajo almacenando archivos en OneDrive o actualizar las archivos que ya tenga en OneDrive.</span><span class="sxs-lookup"><span data-stu-id="64e00-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="64e00-107">Usar desencadenadores para iniciar el flujo de trabajo cuando se crea o se actualiza un archivo en OneDrive.</span><span class="sxs-lookup"><span data-stu-id="64e00-107">Use triggers to start your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="64e00-108">Usar acciones para crear o eliminar un archivo, entre otras muchas cosas.</span><span class="sxs-lookup"><span data-stu-id="64e00-108">Use actions to create a file, delete a file, and more.</span></span> <span data-ttu-id="64e00-109">Por ejemplo, cuando se reciba un nuevo correo electrónico de Office 365 con datos adjuntos (desencadenador), cree un nuevo archivo en OneDrive (acción).</span><span class="sxs-lookup"><span data-stu-id="64e00-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="64e00-110">En este tema se muestra cómo usar el conector de OneDrive en una aplicación lógica, y se enumeran los desencadenadores y las acciones.</span><span class="sxs-lookup"><span data-stu-id="64e00-110">This topic shows you how to use the OneDrive connector in a logic app, and also lists the triggers and actions.</span></span>

<span data-ttu-id="64e00-111">Para más información sobre Logic Apps, consulte [¿Qué son las aplicaciones lógicas?](../logic-apps/logic-apps-what-are-logic-apps.md) y [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="64e00-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-onedrive"></a><span data-ttu-id="64e00-112">Conexión a OneDrive</span><span class="sxs-lookup"><span data-stu-id="64e00-112">Connect to OneDrive</span></span>
<span data-ttu-id="64e00-113">Antes de que la aplicación lógica pueda acceder a cualquier servicio, cree primero una *conexión* a este.</span><span class="sxs-lookup"><span data-stu-id="64e00-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="64e00-114">Una conexión proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="64e00-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="64e00-115">Por ejemplo, para conectarse a OneDrive, primero necesita una *conexión* de OneDrive.</span><span class="sxs-lookup"><span data-stu-id="64e00-115">For example, to connect to OneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="64e00-116">Para crear una conexión, escriba las credenciales que utiliza normalmente para acceder al servicio al que desea conectarse.</span><span class="sxs-lookup"><span data-stu-id="64e00-116">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="64e00-117">Por lo tanto, con OneDrive, escriba las credenciales de la cuenta de OneDrive para crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="64e00-117">So, with OneDrive, enter the credentials to your OneDrive account  to create the connection.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="64e00-118">Creación de la conexión</span><span class="sxs-lookup"><span data-stu-id="64e00-118">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to OneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="64e00-119">Uso de un desencadenador</span><span class="sxs-lookup"><span data-stu-id="64e00-119">Use a trigger</span></span>
<span data-ttu-id="64e00-120">Un desencadenador es un evento que se puede utilizar para iniciar el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="64e00-120">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="64e00-121">Los desencadenadores "sondean" el servicio en el intervalo y la frecuencia que desee.</span><span class="sxs-lookup"><span data-stu-id="64e00-121">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="64e00-122">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="64e00-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="64e00-123">En la aplicación lógica, escriba "onedrive" para obtener una lista de los desencadenadores:</span><span class="sxs-lookup"><span data-stu-id="64e00-123">In the logic app, type "onedrive" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="64e00-124">Seleccione **Cuando se modifica un archivo**.</span><span class="sxs-lookup"><span data-stu-id="64e00-124">Select **When a file is modified**.</span></span> <span data-ttu-id="64e00-125">Si ya existe una conexión, seleccione el botón Mostrar Selector para seleccionar una carpeta.</span><span class="sxs-lookup"><span data-stu-id="64e00-125">If a connection already exists, then select the Show Picker button to select a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="64e00-126">Si se le solicita que inicie sesión, escriba los datos de inicio de sesión para crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="64e00-126">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="64e00-127">En la sección [Creación de la conexión](connectors-create-api-onedrive.md#create-the-connection) de este tema se enumeran los pasos.</span><span class="sxs-lookup"><span data-stu-id="64e00-127">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="64e00-128">En este ejemplo, la aplicación lógica se ejecuta cuando un archivo de la carpeta que elija se actualiza.</span><span class="sxs-lookup"><span data-stu-id="64e00-128">In this example, the logic app runs when a file in the folder you choose is updated.</span></span> <span data-ttu-id="64e00-129">Para ver los resultados de este desencadenador, agregue otra acción que envíe un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="64e00-129">To see the results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="64e00-130">Por ejemplo, agregue la acción *Enviar un correo electrónico* de Office 365 Outlook que le envía un correo electrónico cuando se actualiza un archivo.</span><span class="sxs-lookup"><span data-stu-id="64e00-130">For example, add the Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="64e00-131">Seleccione el botón **Editar** y defina los valores de **Frecuencia** e **Intervalo**.</span><span class="sxs-lookup"><span data-stu-id="64e00-131">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="64e00-132">Por ejemplo, si desea que el desencadenador sondee cada 15 minutos, establezca el valor de **Frecuencia** en **Minuto** y el de **Intervalo** en **15**.</span><span class="sxs-lookup"><span data-stu-id="64e00-132">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="64e00-133">**Guarde** los cambios (esquina superior izquierda de la barra de herramientas).</span><span class="sxs-lookup"><span data-stu-id="64e00-133">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="64e00-134">La aplicación lógica se guarda y se puede habilitar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="64e00-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="64e00-135">Uso de una acción</span><span class="sxs-lookup"><span data-stu-id="64e00-135">Use an action</span></span>
<span data-ttu-id="64e00-136">Una acción es una operación que se lleva a cabo mediante el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="64e00-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="64e00-137">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="64e00-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="64e00-138">Seleccione el signo más.</span><span class="sxs-lookup"><span data-stu-id="64e00-138">Select the plus sign.</span></span> <span data-ttu-id="64e00-139">Aparecen varias opciones: **Agregar una acción**, **Agregar una condición** o una de las opciones de **Más**.</span><span class="sxs-lookup"><span data-stu-id="64e00-139">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="64e00-140">Elija **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="64e00-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="64e00-141">En el cuadro de texto, escriba "onedrive" para obtener una lista de todas las acciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="64e00-141">In the text box, type “onedrive” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="64e00-142">En nuestro ejemplo, elija **OneDrive - Crear archivo**.</span><span class="sxs-lookup"><span data-stu-id="64e00-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="64e00-143">Si ya existe una conexión, seleccione la **Ruta de la carpeta** en la que se incluirá el archivo, escriba el **Nombre de archivo** y elija el **Contenido de archivo** que desee:</span><span class="sxs-lookup"><span data-stu-id="64e00-143">If a connection already exists, then select the **Folder Path** to put the file, enter the **File Name**, and choose the **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="64e00-144">Si se le solicita la información de conexión, escriba los detalles para crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="64e00-144">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="64e00-145">Estas propiedades se describen en la sección [Creación de la conexión](connectors-create-api-onedrive.md#create-the-connection) de este tema.</span><span class="sxs-lookup"><span data-stu-id="64e00-145">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="64e00-146">En este ejemplo, creamos un nuevo archivo en una carpeta de OneDrive.</span><span class="sxs-lookup"><span data-stu-id="64e00-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="64e00-147">Puede utilizar la salida de otro desencadenador para crear el archivo de OneDrive.</span><span class="sxs-lookup"><span data-stu-id="64e00-147">You can use output from another trigger to create the OneDrive file.</span></span> <span data-ttu-id="64e00-148">Por ejemplo, agregue el desencadenador *Cuando llega un nuevo correo electrónico* de Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="64e00-148">For example, add the Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="64e00-149">A continuación, agregue la acción *Crear archivo* de OneDrive, que usa los campos Attachments y Content-Type de una instrucción ForEach para crear el nuevo archivo en OneDrive.</span><span class="sxs-lookup"><span data-stu-id="64e00-149">Then add the OneDrive *Create file* action that uses the Attachments and Content-Type fields within a ForEach to create the new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="64e00-150">**Guarde** los cambios (esquina superior izquierda de la barra de herramientas).</span><span class="sxs-lookup"><span data-stu-id="64e00-150">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="64e00-151">La aplicación lógica se guarda y se puede habilitar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="64e00-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="64e00-152">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="64e00-152">Connector-specific details</span></span>

<span data-ttu-id="64e00-153">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="64e00-153">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="64e00-154">Más conectores</span><span class="sxs-lookup"><span data-stu-id="64e00-154">More connectors</span></span>
<span data-ttu-id="64e00-155">Volver a la [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="64e00-155">Go back to the [APIs list](apis-list.md).</span></span>