---
title: Conector de Dropbox en Azure Logic Apps | Microsoft Docs
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. Conéctese a Dropbox para administrar los archivos. En Dropbox, puede realizar diversas acciones, como cargar, actualizar, obtener y eliminar archivos."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 0d09580c60fd620811b539147439d0922839fe7e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-dropbox-connector"></a><span data-ttu-id="d37e9-105">Introducción al conector de Dropbox</span><span class="sxs-lookup"><span data-stu-id="d37e9-105">Get started with the Dropbox connector</span></span>
<span data-ttu-id="d37e9-106">Conéctese a Dropbox para administrar los archivos.</span><span class="sxs-lookup"><span data-stu-id="d37e9-106">Connect to Dropbox to manage your files.</span></span> <span data-ttu-id="d37e9-107">En Dropbox, puede realizar diversas acciones, como cargar, actualizar, obtener y eliminar archivos.</span><span class="sxs-lookup"><span data-stu-id="d37e9-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="d37e9-108">Para poder usar [un conector](apis-list.md), primero debe crear una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="d37e9-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="d37e9-109">Puede empezar [creando una aplicación lógica ahora](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d37e9-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-dropbox"></a><span data-ttu-id="d37e9-110">Conexión con Dropbox</span><span class="sxs-lookup"><span data-stu-id="d37e9-110">Connect to Dropbox</span></span>
<span data-ttu-id="d37e9-111">Para que la aplicación lógica pueda acceder a un servicio, primero debe crear una *conexión* con dicho servicio.</span><span class="sxs-lookup"><span data-stu-id="d37e9-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="d37e9-112">Una conexión proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="d37e9-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="d37e9-113">Por ejemplo, para poder conectarse a Dropbox, primero necesita crear una *conexión* a Dropbox.</span><span class="sxs-lookup"><span data-stu-id="d37e9-113">For example, in order to connect to Dropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="d37e9-114">Para ello, tendrá que especificar las credenciales que usa habitualmente para acceder al servicio al que desea conectarse.</span><span class="sxs-lookup"><span data-stu-id="d37e9-114">To create a connection, you would need to provide the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="d37e9-115">Por tanto, en el ejemplo de Dropbox, deberá escribir las credenciales de la cuenta de Dropbox para crear la conexión con este servicio.</span><span class="sxs-lookup"><span data-stu-id="d37e9-115">So, in the Dropbox example, you would need the credentials to your Dropbox account in order to create the connection to Dropbox.</span></span> [<span data-ttu-id="d37e9-116">Más información sobre las conexiones</span><span class="sxs-lookup"><span data-stu-id="d37e9-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-to-dropbox"></a><span data-ttu-id="d37e9-117">Creación de una conexión con Dropbox</span><span class="sxs-lookup"><span data-stu-id="d37e9-117">Create a connection to Dropbox</span></span>
> [!INCLUDE [Steps to create a connection to Dropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="d37e9-118">Uso de un desencadenador de Dropbox</span><span class="sxs-lookup"><span data-stu-id="d37e9-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="d37e9-119">Un desencadenador es un evento que se puede utilizar para iniciar el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="d37e9-119">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="d37e9-120">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d37e9-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="d37e9-121">En este ejemplo, vamos a usar el desencadenador **When a file is created (Cuando se crea un archivo)**.</span><span class="sxs-lookup"><span data-stu-id="d37e9-121">In this example, we will use the **When a file is created** trigger.</span></span> <span data-ttu-id="d37e9-122">Cuando se active este desencadenador, se invocará la acción de Dropbox **Get file content using path (Obtener contenido del archivo mediante la ruta de acceso)**.</span><span class="sxs-lookup"><span data-stu-id="d37e9-122">When this trigger occurs, we will call the **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="d37e9-123">Escriba *dropbox* en el cuadro de búsqueda del diseñador de Logic Apps y seleccione el desencadenador **Dropbox - When a file is created (Dropbox - Cuando se cree un archivo)**.</span><span class="sxs-lookup"><span data-stu-id="d37e9-123">Enter *dropbox* in the search box on the Logic Apps designer, then select the **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="d37e9-124">Seleccione la carpeta en la que se va a supervisar la creación de archivos.</span><span class="sxs-lookup"><span data-stu-id="d37e9-124">Select the folder in which you want to track file creation.</span></span> <span data-ttu-id="d37e9-125">Seleccione la opción … (marcada con un cuadro rojo) y busque la carpeta que quiere seleccionar para la entrada del desencadenador.</span><span class="sxs-lookup"><span data-stu-id="d37e9-125">Select ... (identified in the red box) and browse to the folder you wish to select for the trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="d37e9-126">Uso de una acción de Dropbox</span><span class="sxs-lookup"><span data-stu-id="d37e9-126">Use a Dropbox action</span></span>
<span data-ttu-id="d37e9-127">Una acción es una operación que se lleva a cabo mediante el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="d37e9-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="d37e9-128">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d37e9-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="d37e9-129">Ahora que se ha agregado el desencadenador, siga estos pasos para incorporar una acción que obtenga el contenido del nuevo archivo.</span><span class="sxs-lookup"><span data-stu-id="d37e9-129">Now that the trigger has been added, follow these steps to add an action that will get the new file's content.</span></span>

1. <span data-ttu-id="d37e9-130">Seleccione **+ Nuevo paso** para agregar la acción que quiere que se ejecute cuando se cree un archivo.</span><span class="sxs-lookup"><span data-stu-id="d37e9-130">Select **+ New Step** to add the action you would like to take when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="d37e9-131">Seleccione **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="d37e9-131">Select **Add an action**.</span></span> <span data-ttu-id="d37e9-132">Se abrirá el cuadro de búsqueda en el que podrá buscar cualquier acción que quiera realizar.</span><span class="sxs-lookup"><span data-stu-id="d37e9-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="d37e9-133">Escriba *dropbox* para buscar las acciones relacionadas con Dropbox.</span><span class="sxs-lookup"><span data-stu-id="d37e9-133">Enter *dropbox* to search for actions related to Dropbox.</span></span>  
4. <span data-ttu-id="d37e9-134">Seleccione **Dropbox - Get file content using path (Dropbox: obtener el contenido del archivo mediante la ruta de acceso)**. Esta será la acción que se ejecutará cuando se cree un archivo en la carpeta de Dropbox seleccionada.</span><span class="sxs-lookup"><span data-stu-id="d37e9-134">Select **Dropbox - Get file content using path** as the action to take when a new file is created in the selected Dropbox folder.</span></span> <span data-ttu-id="d37e9-135">Se abre el bloque de control de acción.</span><span class="sxs-lookup"><span data-stu-id="d37e9-135">The action control block opens.</span></span> <span data-ttu-id="d37e9-136">Si no lo ha hecho previamente, se le pedirá que autorice a la aplicación lógica para que pueda acceder a la cuenta de Dropbox.</span><span class="sxs-lookup"><span data-stu-id="d37e9-136">You will be prompted to authorize your logic app to access your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="d37e9-137">Seleccione la opción … (la encontrará a la derecha del control **Ruta de archivo**) y busque la ruta de archivo que quiere usar.</span><span class="sxs-lookup"><span data-stu-id="d37e9-137">Select ... (located at the right side of the **File Path** control) and browse to the file path you would like to use.</span></span> <span data-ttu-id="d37e9-138">También puede usar el token de la **ruta de archivo** para crear más rápido la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="d37e9-138">Or, use the **file path** token to speed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="d37e9-139">Guarde el trabajo y cree un nuevo archivo en Dropbox para activar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d37e9-139">Save your work and create a new file in Dropbox to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="d37e9-140">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="d37e9-140">Connector-specific details</span></span>

<span data-ttu-id="d37e9-141">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/dropbox/).</span><span class="sxs-lookup"><span data-stu-id="d37e9-141">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="d37e9-142">Más conectores</span><span class="sxs-lookup"><span data-stu-id="d37e9-142">More connectors</span></span>
<span data-ttu-id="d37e9-143">Volver a la [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="d37e9-143">Go back to the [APIs list](apis-list.md).</span></span>