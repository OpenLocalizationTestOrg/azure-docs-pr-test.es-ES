---
title: "Conector de base de datos de SQL Azure de hello aaaAdd en las aplicaciones lógicas | Documentos de Microsoft"
description: "Información general sobre el conector de Base de datos SQL de Azure con los parámetros de la API de REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a><span data-ttu-id="de347-103">Empezar a trabajar con el conector de base de datos de SQL Azure Hola</span><span class="sxs-lookup"><span data-stu-id="de347-103">Get started with hello Azure SQL Database connector</span></span>
<span data-ttu-id="de347-104">Mediante el conector de base de datos de SQL Azure de hello, crear flujos de trabajo para su organización que administran datos de las tablas.</span><span class="sxs-lookup"><span data-stu-id="de347-104">Using hello Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="de347-105">Con Base de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="de347-105">With SQL Database, you:</span></span>

* <span data-ttu-id="de347-106">Compilar el flujo de trabajo mediante la adición de una base de datos de los clientes de tooa cliente nuevo o actualizar un pedido en una base de datos de pedidos.</span><span class="sxs-lookup"><span data-stu-id="de347-106">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="de347-107">Usar acciones tooget una fila de datos, insertar una fila nueva e incluso eliminar.</span><span class="sxs-lookup"><span data-stu-id="de347-107">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="de347-108">Por ejemplo, al crear un registro en Dynamics CRM Online (desencadenador), inserte una fila en una base de datos SQL de Azure (acción).</span><span class="sxs-lookup"><span data-stu-id="de347-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="de347-109">Este tema muestra cómo toouse Hola conector de base de datos SQL en una aplicación de lógica, y también listas Hola acciones.</span><span class="sxs-lookup"><span data-stu-id="de347-109">This topic shows you how toouse hello SQL Database connector in a logic app, and also lists hello actions.</span></span>

<span data-ttu-id="de347-110">toolearn más información acerca de las aplicaciones lógicas, consulte [¿cuáles son las aplicaciones lógicas](../logic-apps/logic-apps-what-are-logic-apps.md) y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="de347-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-sql-database"></a><span data-ttu-id="de347-111">Conectar tooAzure base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="de347-111">Connect tooAzure SQL Database</span></span>
<span data-ttu-id="de347-112">Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero cree un *conexión* toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="de347-112">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="de347-113">Una conexión proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="de347-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="de347-114">Por ejemplo, tooconnect tooSQL base de datos, en primer lugar crear una base de datos de SQL *conexión*.</span><span class="sxs-lookup"><span data-stu-id="de347-114">For example, tooconnect tooSQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="de347-115">toocreate una conexión, escriba las credenciales de Hola que suele usar el servicio de hello tooaccess a que se conecta.</span><span class="sxs-lookup"><span data-stu-id="de347-115">toocreate a connection, you enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="de347-116">Por lo tanto, en la base de datos de SQL, escriba la conexión de base de datos SQL credenciales toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="de347-116">So, in SQL Database, enter your SQL Database credentials toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="de347-117">Crear conexiones de Hola</span><span class="sxs-lookup"><span data-stu-id="de347-117">Create hello connection</span></span>
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="de347-118">Uso de un desencadenador</span><span class="sxs-lookup"><span data-stu-id="de347-118">Use a trigger</span></span>
<span data-ttu-id="de347-119">Este conector no tiene ningún desencadenador.</span><span class="sxs-lookup"><span data-stu-id="de347-119">This connector does not have any triggers.</span></span> <span data-ttu-id="de347-120">Utilice otra aplicación de lógica de desencadenadores toostart hello, como un desencadenador de periodicidad, un desencadenador de HTTP Webhook, desencadenadores disponibles con otros conectores y mucho más.</span><span class="sxs-lookup"><span data-stu-id="de347-120">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="de347-121">En [Creación de una nueva aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md) se puede ver un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="de347-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="de347-122">Uso de una acción</span><span class="sxs-lookup"><span data-stu-id="de347-122">Use an action</span></span>
<span data-ttu-id="de347-123">Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="de347-123">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="de347-124">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="de347-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="de347-125">Seleccione el signo más Hola.</span><span class="sxs-lookup"><span data-stu-id="de347-125">Select hello plus sign.</span></span> <span data-ttu-id="de347-126">Vea elegir entre varias opciones: **agregar una acción**, **agregar una condición**, o uno de hello **más** opciones.</span><span class="sxs-lookup"><span data-stu-id="de347-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="de347-127">Elija **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="de347-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="de347-128">En el cuadro de texto hello, escriba "sql" tooget una lista de todas las acciones disponibles Hola.</span><span class="sxs-lookup"><span data-stu-id="de347-128">In hello text box, type “sql” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="de347-129">En nuestro ejemplo, elija **SQL Server - Obtener fila**.</span><span class="sxs-lookup"><span data-stu-id="de347-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="de347-130">Si ya existe una conexión, a continuación, seleccione hello **nombre de la tabla** en Hola de lista desplegable lista y escriba hello **identificador de fila** desea tooreturn.</span><span class="sxs-lookup"><span data-stu-id="de347-130">If a connection already exists, then select hello **Table name** from hello drop-down list, and enter hello **Row ID** you want tooreturn.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="de347-131">Si se le solicitará información de conexión de hello, a continuación, escriba la conexión de hello detalles toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="de347-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="de347-132">[Crear conexiones de hello](connectors-create-api-sqlazure.md#create-the-connection) en este tema se describen estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="de347-132">[Create hello connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="de347-133">En este ejemplo, devolvemos una fila de una tabla.</span><span class="sxs-lookup"><span data-stu-id="de347-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="de347-134">datos de hello toosee en esta fila, agregue otra acción que crea un archivo mediante los campos de Hola de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="de347-134">toosee hello data in this row, add another action that creates a file using hello fields from hello table.</span></span> <span data-ttu-id="de347-135">Por ejemplo, agregar una acción de OneDrive que usa hello, FirstName y LastName campos toocreate un archivo nuevo en la cuenta de almacenamiento de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="de347-135">For example, add a OneDrive action that uses hello FirstName and LastName fields toocreate a new file in hello cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="de347-136">**Guardar** los cambios (esquina superior izquierda de la barra de herramientas de hello).</span><span class="sxs-lookup"><span data-stu-id="de347-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="de347-137">La aplicación lógica se guarda y se puede habilitar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="de347-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="de347-138">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="de347-138">Connector-specific details</span></span>

<span data-ttu-id="de347-139">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/sql/).</span><span class="sxs-lookup"><span data-stu-id="de347-139">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="de347-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="de347-140">Next steps</span></span>
<span data-ttu-id="de347-141">[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="de347-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="de347-142">Explorar Hola otros conectores disponibles en las aplicaciones lógicas en nuestro [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="de347-142">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

