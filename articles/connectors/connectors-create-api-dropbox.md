---
title: "Conector de aaaDropbox en las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. Conectar tooDropbox toomanage los archivos. En Dropbox, puede realizar diversas acciones, como cargar, actualizar, obtener y eliminar archivos."
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
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a><span data-ttu-id="a93d9-105">Empezar a trabajar con el conector de Dropbox Hola</span><span class="sxs-lookup"><span data-stu-id="a93d9-105">Get started with hello Dropbox connector</span></span>
<span data-ttu-id="a93d9-106">Conectar tooDropbox toomanage los archivos.</span><span class="sxs-lookup"><span data-stu-id="a93d9-106">Connect tooDropbox toomanage your files.</span></span> <span data-ttu-id="a93d9-107">En Dropbox, puede realizar diversas acciones, como cargar, actualizar, obtener y eliminar archivos.</span><span class="sxs-lookup"><span data-stu-id="a93d9-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="a93d9-108">toouse [cualquier conector](apis-list.md), primero debe toocreate una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="a93d9-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="a93d9-109">Puede empezar [creando una aplicación lógica ahora](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a93d9-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toodropbox"></a><span data-ttu-id="a93d9-110">Conectar tooDropbox</span><span class="sxs-lookup"><span data-stu-id="a93d9-110">Connect tooDropbox</span></span>
<span data-ttu-id="a93d9-111">Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero debe toocreate una *conexión* toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="a93d9-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="a93d9-112">Una conexión proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="a93d9-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="a93d9-113">Por ejemplo, en orden tooconnect tooDropbox, primero necesita una lista desplegable *conexión*.</span><span class="sxs-lookup"><span data-stu-id="a93d9-113">For example, in order tooconnect tooDropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="a93d9-114">toocreate una conexión, tendría las credenciales de hello tooprovide que suele usar el servicio de hello tooaccess a que desea tooconnect.</span><span class="sxs-lookup"><span data-stu-id="a93d9-114">toocreate a connection, you would need tooprovide hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="a93d9-115">Por lo tanto, en el ejemplo de Hola a Dropbox, necesitaría Hola credenciales tooyour cuenta de Dropbox en orden toocreate Hola conexión tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="a93d9-115">So, in hello Dropbox example, you would need hello credentials tooyour Dropbox account in order toocreate hello connection tooDropbox.</span></span> [<span data-ttu-id="a93d9-116">Más información sobre las conexiones</span><span class="sxs-lookup"><span data-stu-id="a93d9-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-toodropbox"></a><span data-ttu-id="a93d9-117">Crear una conexión tooDropbox</span><span class="sxs-lookup"><span data-stu-id="a93d9-117">Create a connection tooDropbox</span></span>
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="a93d9-118">Uso de un desencadenador de Dropbox</span><span class="sxs-lookup"><span data-stu-id="a93d9-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="a93d9-119">Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica.</span><span class="sxs-lookup"><span data-stu-id="a93d9-119">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="a93d9-120">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="a93d9-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="a93d9-121">En este ejemplo, usaremos hello **cuando se crea un archivo** desencadenador.</span><span class="sxs-lookup"><span data-stu-id="a93d9-121">In this example, we will use hello **When a file is created** trigger.</span></span> <span data-ttu-id="a93d9-122">Cuando se produce este desencadenador, llamaremos a hello **obtener el contenido del archivo con la ruta de acceso** acción Dropbox.</span><span class="sxs-lookup"><span data-stu-id="a93d9-122">When this trigger occurs, we will call hello **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="a93d9-123">Escriba *dropbox* en el cuadro de búsqueda de hello en el Diseñador de aplicaciones de la lógica de hello, a continuación, seleccione hello **Dropbox - cuando se crea un archivo** desencadenador.</span><span class="sxs-lookup"><span data-stu-id="a93d9-123">Enter *dropbox* in hello search box on hello Logic Apps designer, then select hello **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="a93d9-124">Seleccione la carpeta de hello en el que desea tootrack creación del archivo.</span><span class="sxs-lookup"><span data-stu-id="a93d9-124">Select hello folder in which you want tootrack file creation.</span></span> <span data-ttu-id="a93d9-125">Seleccione... (identificado en el cuadro de hello rojo) y examinar las carpetas toohello desea tooselect de desencadenador de hello de la entrada.</span><span class="sxs-lookup"><span data-stu-id="a93d9-125">Select ... (identified in hello red box) and browse toohello folder you wish tooselect for hello trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="a93d9-126">Uso de una acción de Dropbox</span><span class="sxs-lookup"><span data-stu-id="a93d9-126">Use a Dropbox action</span></span>
<span data-ttu-id="a93d9-127">Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a93d9-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="a93d9-128">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="a93d9-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="a93d9-129">Ahora que hello desencadenador se ha agregado, siga estas tooadd pasos una acción que se obtendrá el contenido del archivo nuevo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a93d9-129">Now that hello trigger has been added, follow these steps tooadd an action that will get hello new file's content.</span></span>

1. <span data-ttu-id="a93d9-130">Seleccione **+ nuevo paso** acción de hello tooadd le gustaría tootake cuando se crea un nuevo archivo.</span><span class="sxs-lookup"><span data-stu-id="a93d9-130">Select **+ New Step** tooadd hello action you would like tootake when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="a93d9-131">Seleccione **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="a93d9-131">Select **Add an action**.</span></span> <span data-ttu-id="a93d9-132">Este cuadro de búsqueda de hello abre donde puede buscar cualquier acción desea que tootake.</span><span class="sxs-lookup"><span data-stu-id="a93d9-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="a93d9-133">Escriba *dropbox* toosearch para acciones relacionadas tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="a93d9-133">Enter *dropbox* toosearch for actions related tooDropbox.</span></span>  
4. <span data-ttu-id="a93d9-134">Seleccione **Dropbox - obtener contenido del archivo con la ruta de acceso** como Hola tootake acción cuando se crea un nuevo archivo en hello seleccionado la carpeta de Dropbox.</span><span class="sxs-lookup"><span data-stu-id="a93d9-134">Select **Dropbox - Get file content using path** as hello action tootake when a new file is created in hello selected Dropbox folder.</span></span> <span data-ttu-id="a93d9-135">se abre el bloque de control de acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="a93d9-135">hello action control block opens.</span></span> <span data-ttu-id="a93d9-136">También será solicitada tooauthorize su tooaccess de aplicación lógica su Dropbox cuenta si aún no lo hecho previamente.</span><span class="sxs-lookup"><span data-stu-id="a93d9-136">You will be prompted tooauthorize your logic app tooaccess your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="a93d9-137">Seleccione... (situado en el lado derecho de Hola de hello **ruta de acceso del archivo** control) y busque la ruta de acceso del archivo toohello le gustaría toouse.</span><span class="sxs-lookup"><span data-stu-id="a93d9-137">Select ... (located at hello right side of hello **File Path** control) and browse toohello file path you would like toouse.</span></span> <span data-ttu-id="a93d9-138">O bien, use hello **ruta de acceso de archivo** toospeed símbolo (token) de la creación de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="a93d9-138">Or, use hello **file path** token toospeed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="a93d9-139">Guarde su trabajo y crear un nuevo archivo en Dropbox tooactivate el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a93d9-139">Save your work and create a new file in Dropbox tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="a93d9-140">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="a93d9-140">Connector-specific details</span></span>

<span data-ttu-id="a93d9-141">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/dropbox/).</span><span class="sxs-lookup"><span data-stu-id="a93d9-141">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="a93d9-142">Más conectores</span><span class="sxs-lookup"><span data-stu-id="a93d9-142">More connectors</span></span>
<span data-ttu-id="a93d9-143">Volver atrás toohello [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="a93d9-143">Go back toohello [APIs list](apis-list.md).</span></span>
