---
title: "Conector de OneDrive aaaAdd hello en las aplicaciones lógicas | Documentos de Microsoft"
description: "Información general del conector de hello OneDrive con parámetros de la API de REST"
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
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a><span data-ttu-id="0f922-103">Empezar a trabajar con el conector de hello OneDrive</span><span class="sxs-lookup"><span data-stu-id="0f922-103">Get started with hello OneDrive connector</span></span>
<span data-ttu-id="0f922-104">Conectar tooOneDrive toomanage sus archivos, incluidas la carga, get, elimine los archivos y mucho más.</span><span class="sxs-lookup"><span data-stu-id="0f922-104">Connect tooOneDrive toomanage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="0f922-105">Con OneDrive, puede:</span><span class="sxs-lookup"><span data-stu-id="0f922-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="0f922-106">Crear un flujo de trabajo almacenando archivos en OneDrive o actualizar las archivos que ya tenga en OneDrive.</span><span class="sxs-lookup"><span data-stu-id="0f922-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="0f922-107">Usar desencadenadores toostart el flujo de trabajo cuando se crea un archivo o se actualiza dentro de su OneDrive.</span><span class="sxs-lookup"><span data-stu-id="0f922-107">Use triggers toostart your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="0f922-108">Usar acciones toocreate un archivo, eliminar un archivo y mucho más.</span><span class="sxs-lookup"><span data-stu-id="0f922-108">Use actions toocreate a file, delete a file, and more.</span></span> <span data-ttu-id="0f922-109">Por ejemplo, cuando se reciba un nuevo correo electrónico de Office 365 con datos adjuntos (desencadenador), cree un nuevo archivo en OneDrive (acción).</span><span class="sxs-lookup"><span data-stu-id="0f922-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="0f922-110">Este tema muestra cómo toouse Hola OneDrive conector en una aplicación de lógica, y también listas Hola acciones y desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="0f922-110">This topic shows you how toouse hello OneDrive connector in a logic app, and also lists hello triggers and actions.</span></span>

<span data-ttu-id="0f922-111">toolearn más información acerca de las aplicaciones lógicas, consulte [¿cuáles son las aplicaciones lógicas](../logic-apps/logic-apps-what-are-logic-apps.md) y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0f922-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooonedrive"></a><span data-ttu-id="0f922-112">Conectar tooOneDrive</span><span class="sxs-lookup"><span data-stu-id="0f922-112">Connect tooOneDrive</span></span>
<span data-ttu-id="0f922-113">Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero cree un *conexión* toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="0f922-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="0f922-114">Una conexión proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="0f922-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="0f922-115">Por ejemplo, tooconnect tooOneDrive, primero necesita una OneDrive *conexión*.</span><span class="sxs-lookup"><span data-stu-id="0f922-115">For example, tooconnect tooOneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="0f922-116">toocreate una conexión, escriba las credenciales de Hola que suele usar el servicio de hello tooaccess desea tooconnect a.</span><span class="sxs-lookup"><span data-stu-id="0f922-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="0f922-117">Por lo tanto, con OneDrive, escriba conexión con una Hola Hola credenciales tooyour OneDrive cuenta toocreate.</span><span class="sxs-lookup"><span data-stu-id="0f922-117">So, with OneDrive, enter hello credentials tooyour OneDrive account  toocreate hello connection.</span></span>

### <a name="create-hello-connection"></a><span data-ttu-id="0f922-118">Crear conexiones de Hola</span><span class="sxs-lookup"><span data-stu-id="0f922-118">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="0f922-119">Uso de un desencadenador</span><span class="sxs-lookup"><span data-stu-id="0f922-119">Use a trigger</span></span>
<span data-ttu-id="0f922-120">Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica.</span><span class="sxs-lookup"><span data-stu-id="0f922-120">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="0f922-121">Desencadenadores "sondean" hello servicio en un intervalo y la frecuencia que desee.</span><span class="sxs-lookup"><span data-stu-id="0f922-121">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="0f922-122">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="0f922-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="0f922-123">En la aplicación de la lógica de hello, escriba "onedrive" tooget una lista de los desencadenadores de hello:</span><span class="sxs-lookup"><span data-stu-id="0f922-123">In hello logic app, type "onedrive" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="0f922-124">Seleccione **Cuando se modifica un archivo**.</span><span class="sxs-lookup"><span data-stu-id="0f922-124">Select **When a file is modified**.</span></span> <span data-ttu-id="0f922-125">Si ya existe una conexión, a continuación, seleccione Hola selector Mostrar botón tooselect una carpeta.</span><span class="sxs-lookup"><span data-stu-id="0f922-125">If a connection already exists, then select hello Show Picker button tooselect a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="0f922-126">Si son toosign solicitada en, escriba el inicio de sesión de hello en conexión de hello toocreate de detalles.</span><span class="sxs-lookup"><span data-stu-id="0f922-126">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="0f922-127">[Crear conexiones de hello](connectors-create-api-onedrive.md#create-the-connection) en este tema se enumeran los pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f922-127">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0f922-128">En este ejemplo, aplicación de lógica de Hola se ejecuta cuando un archivo en la carpeta de Hola que elija se actualiza.</span><span class="sxs-lookup"><span data-stu-id="0f922-128">In this example, hello logic app runs when a file in hello folder you choose is updated.</span></span> <span data-ttu-id="0f922-129">resultados de hello toosee de este desencadenador, agregar otra acción que envía un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="0f922-129">toosee hello results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="0f922-130">Por ejemplo, agregar Hola Office 365 Outlook *enviar un correo electrónico* acción que envía por correo electrónico cuando se actualiza un archivo.</span><span class="sxs-lookup"><span data-stu-id="0f922-130">For example, add hello Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="0f922-131">Seleccione hello **editar** botón y establezca hello **frecuencia** y **intervalo** valores.</span><span class="sxs-lookup"><span data-stu-id="0f922-131">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="0f922-132">Por ejemplo, si desea Hola desencadenador toopoll cada 15 minutos, a continuación, establezca hello **frecuencia** demasiado**minuto**, conjunto hello y **intervalo** demasiado**15**.</span><span class="sxs-lookup"><span data-stu-id="0f922-132">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="0f922-133">**Guardar** los cambios (esquina superior izquierda de la barra de herramientas de hello).</span><span class="sxs-lookup"><span data-stu-id="0f922-133">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="0f922-134">La aplicación lógica se guarda y se puede habilitar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="0f922-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="0f922-135">Uso de una acción</span><span class="sxs-lookup"><span data-stu-id="0f922-135">Use an action</span></span>
<span data-ttu-id="0f922-136">Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f922-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="0f922-137">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="0f922-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="0f922-138">Seleccione el signo más Hola.</span><span class="sxs-lookup"><span data-stu-id="0f922-138">Select hello plus sign.</span></span> <span data-ttu-id="0f922-139">Vea elegir entre varias opciones: **agregar una acción**, **agregar una condición**, o uno de hello **más** opciones.</span><span class="sxs-lookup"><span data-stu-id="0f922-139">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="0f922-140">Elija **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="0f922-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="0f922-141">En el cuadro de texto hello, escriba "onedrive" tooget una lista de todas las acciones disponibles Hola.</span><span class="sxs-lookup"><span data-stu-id="0f922-141">In hello text box, type “onedrive” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="0f922-142">En nuestro ejemplo, elija **OneDrive - Crear archivo**.</span><span class="sxs-lookup"><span data-stu-id="0f922-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="0f922-143">Si ya existe una conexión, a continuación, seleccione hello **ruta de acceso de carpeta** tooput Hola de archivo, escriba Hola **nombre de archivo**y elija hello **contenido del archivo** que desee:</span><span class="sxs-lookup"><span data-stu-id="0f922-143">If a connection already exists, then select hello **Folder Path** tooput hello file, enter hello **File Name**, and choose hello **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="0f922-144">Si se le solicitará información de conexión de hello, a continuación, escriba la conexión de hello detalles toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="0f922-144">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="0f922-145">[Crear conexiones de hello](connectors-create-api-onedrive.md#create-the-connection) en este tema se describen estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="0f922-145">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0f922-146">En este ejemplo, creamos un nuevo archivo en una carpeta de OneDrive.</span><span class="sxs-lookup"><span data-stu-id="0f922-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="0f922-147">Puede utilizar la salida de archivo de otro desencadenador toocreate hello OneDrive.</span><span class="sxs-lookup"><span data-stu-id="0f922-147">You can use output from another trigger toocreate hello OneDrive file.</span></span> <span data-ttu-id="0f922-148">Por ejemplo, agregar Hola Office 365 Outlook *cuando llega un nuevo correo electrónico* desencadenador.</span><span class="sxs-lookup"><span data-stu-id="0f922-148">For example, add hello Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="0f922-149">A continuación, agregue hello OneDrive *crear archivo* acción que usa Hola datos adjuntos y los campos de tipo de contenido dentro de un archivo nuevo de ForEach toocreate hello en OneDrive.</span><span class="sxs-lookup"><span data-stu-id="0f922-149">Then add hello OneDrive *Create file* action that uses hello Attachments and Content-Type fields within a ForEach toocreate hello new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="0f922-150">**Guardar** los cambios (esquina superior izquierda de la barra de herramientas de hello).</span><span class="sxs-lookup"><span data-stu-id="0f922-150">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="0f922-151">La aplicación lógica se guarda y se puede habilitar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="0f922-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="0f922-152">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="0f922-152">Connector-specific details</span></span>

<span data-ttu-id="0f922-153">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="0f922-153">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="0f922-154">Más conectores</span><span class="sxs-lookup"><span data-stu-id="0f922-154">More connectors</span></span>
<span data-ttu-id="0f922-155">Volver atrás toohello [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="0f922-155">Go back toohello [APIs list](apis-list.md).</span></span>
