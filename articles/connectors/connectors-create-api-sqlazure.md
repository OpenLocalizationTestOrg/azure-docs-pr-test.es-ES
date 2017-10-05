---
title: "Adición del conector de Azure SQL Database en Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: a3d5cb909dbfcb00f3fbfa0165bb6cd58eb18688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-sql-database-connector"></a><span data-ttu-id="cf652-103">Introducción al conector de Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="cf652-103">Get started with the Azure SQL Database connector</span></span>
<span data-ttu-id="cf652-104">Mediante el conector de Base de datos SQL Azure, cree flujos de trabajo para su organización que administren datos de las tablas.</span><span class="sxs-lookup"><span data-stu-id="cf652-104">Using the Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="cf652-105">Con Base de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="cf652-105">With SQL Database, you:</span></span>

* <span data-ttu-id="cf652-106">Agregue un nuevo cliente a una base de datos de clientes o actualice un pedido en una base de datos de pedidos para crear el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="cf652-106">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="cf652-107">Use acciones para obtener una fila de datos, insertar una fila nueva e incluso eliminarla.</span><span class="sxs-lookup"><span data-stu-id="cf652-107">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="cf652-108">Por ejemplo, al crear un registro en Dynamics CRM Online (desencadenador), inserte una fila en una base de datos SQL de Azure (acción).</span><span class="sxs-lookup"><span data-stu-id="cf652-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="cf652-109">En este tema se muestra cómo usar el conector de SQL Database en una aplicación lógica, y se enumeran las acciones.</span><span class="sxs-lookup"><span data-stu-id="cf652-109">This topic shows you how to use the SQL Database connector in a logic app, and also lists the actions.</span></span>

<span data-ttu-id="cf652-110">Para más información sobre Logic Apps, consulte [¿Qué son las aplicaciones lógicas?](../logic-apps/logic-apps-what-are-logic-apps.md) y [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="cf652-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-sql-database"></a><span data-ttu-id="cf652-111">Conexión a una Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="cf652-111">Connect to Azure SQL Database</span></span>
<span data-ttu-id="cf652-112">Antes de que la aplicación lógica pueda acceder a cualquier servicio, cree primero una *conexión* a este.</span><span class="sxs-lookup"><span data-stu-id="cf652-112">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="cf652-113">Una conexión proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="cf652-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="cf652-114">Por ejemplo, para conectarse a SQL Database, primero cree una *conexión* de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="cf652-114">For example, to connect to SQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="cf652-115">Para crear una conexión, escriba las credenciales que utiliza normalmente para acceder al servicio al que se está conectando.</span><span class="sxs-lookup"><span data-stu-id="cf652-115">To create a connection, you enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="cf652-116">Por lo tanto, en la base de datos de SQL, escriba sus credenciales de la base de datos SQL para crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="cf652-116">So, in SQL Database, enter your SQL Database credentials to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="cf652-117">Creación de la conexión</span><span class="sxs-lookup"><span data-stu-id="cf652-117">Create the connection</span></span>
> [!INCLUDE [Create the connection to SQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="cf652-118">Uso de un desencadenador</span><span class="sxs-lookup"><span data-stu-id="cf652-118">Use a trigger</span></span>
<span data-ttu-id="cf652-119">Este conector no tiene ningún desencadenador.</span><span class="sxs-lookup"><span data-stu-id="cf652-119">This connector does not have any triggers.</span></span> <span data-ttu-id="cf652-120">Utilice otros desencadenadores para iniciar la aplicación lógica; por ejemplo, un desencadenador de periodicidad, un desencadenador HTTP webhook, los desencadenadores disponibles con otros conectores, etc.</span><span class="sxs-lookup"><span data-stu-id="cf652-120">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="cf652-121">En [Creación de una nueva aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md) se puede ver un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="cf652-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="cf652-122">Uso de una acción</span><span class="sxs-lookup"><span data-stu-id="cf652-122">Use an action</span></span>
<span data-ttu-id="cf652-123">Una acción es una operación que se lleva a cabo mediante el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="cf652-123">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="cf652-124">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="cf652-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="cf652-125">Seleccione el signo más.</span><span class="sxs-lookup"><span data-stu-id="cf652-125">Select the plus sign.</span></span> <span data-ttu-id="cf652-126">Aparecen varias opciones: **Agregar una acción**, **Agregar una condición** o una de las opciones de **Más**.</span><span class="sxs-lookup"><span data-stu-id="cf652-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="cf652-127">Elija **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="cf652-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="cf652-128">En el cuadro de texto, escriba "sql" para obtener una lista de todas las acciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="cf652-128">In the text box, type “sql” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="cf652-129">En nuestro ejemplo, elija **SQL Server - Obtener fila**.</span><span class="sxs-lookup"><span data-stu-id="cf652-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="cf652-130">Si ya existe una conexión, seleccione el **Nombre de la tabla** en la lista desplegable y escriba el **Identificador de fila** que desee devolver.</span><span class="sxs-lookup"><span data-stu-id="cf652-130">If a connection already exists, then select the **Table name** from the drop-down list, and enter the **Row ID** you want to return.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="cf652-131">Si se le solicita la información de conexión, escriba los detalles para crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="cf652-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="cf652-132">Estas propiedades se describen en la sección [Creación de la conexión](connectors-create-api-sqlazure.md#create-the-connection) de este tema.</span><span class="sxs-lookup"><span data-stu-id="cf652-132">[Create the connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="cf652-133">En este ejemplo, devolvemos una fila de una tabla.</span><span class="sxs-lookup"><span data-stu-id="cf652-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="cf652-134">Para ver los datos de esta fila, agregue otra acción que cree un archivo con los campos de la tabla.</span><span class="sxs-lookup"><span data-stu-id="cf652-134">To see the data in this row, add another action that creates a file using the fields from the table.</span></span> <span data-ttu-id="cf652-135">Por ejemplo, agregue una acción de OneDrive que use los campos FirstName y LastName para crear un nuevo archivo en la cuenta de almacenamiento de la nube.</span><span class="sxs-lookup"><span data-stu-id="cf652-135">For example, add a OneDrive action that uses the FirstName and LastName fields to create a new file in the cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="cf652-136">**Guarde** los cambios (esquina superior izquierda de la barra de herramientas).</span><span class="sxs-lookup"><span data-stu-id="cf652-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="cf652-137">La aplicación lógica se guarda y se puede habilitar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="cf652-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="cf652-138">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="cf652-138">Connector-specific details</span></span>

<span data-ttu-id="cf652-139">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/sql/).</span><span class="sxs-lookup"><span data-stu-id="cf652-139">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cf652-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf652-140">Next steps</span></span>
<span data-ttu-id="cf652-141">[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="cf652-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="cf652-142">Explore los demás conectores disponibles en Logic Apps en nuestra [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="cf652-142">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

