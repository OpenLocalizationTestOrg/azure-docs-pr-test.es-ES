---
title: "aaaLearn cómo toouse Hola conector SFTP en las aplicaciones lógicas | Documentos de Microsoft"
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. Conecte toosend tooSFTP API y recibir archivos. Puede realizar varias operaciones, como crear, actualizar, obtener o eliminar archivos."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a><span data-ttu-id="e1c95-105">Empezar a trabajar con el conector de hello SFTP</span><span class="sxs-lookup"><span data-stu-id="e1c95-105">Get started with hello SFTP connector</span></span>
<span data-ttu-id="e1c95-106">Utilice Hola SFTP conector tooaccess un toosend de cuenta SFTP y recibir archivos.</span><span class="sxs-lookup"><span data-stu-id="e1c95-106">Use hello SFTP connector tooaccess an SFTP account toosend and receive files.</span></span> <span data-ttu-id="e1c95-107">Puede realizar varias operaciones, como crear, actualizar, obtener o eliminar archivos.</span><span class="sxs-lookup"><span data-stu-id="e1c95-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="e1c95-108">toouse [cualquier conector](apis-list.md), primero debe toocreate una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="e1c95-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="e1c95-109">Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e1c95-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosftp"></a><span data-ttu-id="e1c95-110">Conectar tooSFTP</span><span class="sxs-lookup"><span data-stu-id="e1c95-110">Connect tooSFTP</span></span>
<span data-ttu-id="e1c95-111">Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero debe toocreate una *conexión* toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="e1c95-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="e1c95-112">Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="e1c95-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosftp"></a><span data-ttu-id="e1c95-113">Crear una conexión tooSFTP</span><span class="sxs-lookup"><span data-stu-id="e1c95-113">Create a connection tooSFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="e1c95-114">Uso de un desencadenador de SFTP</span><span class="sxs-lookup"><span data-stu-id="e1c95-114">Use an SFTP trigger</span></span>
<span data-ttu-id="e1c95-115">Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica.</span><span class="sxs-lookup"><span data-stu-id="e1c95-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="e1c95-116">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="e1c95-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="e1c95-117">En este ejemplo, Hola **SFTP - cuando se agrega o modifica un archivo** desencadenador es tooinitiate usa un flujo de trabajo de aplicación lógica cuando se agregan a un archivo, o modifica en un servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="e1c95-117">In this example, hello **SFTP - When a file is added or modified** trigger is used tooinitiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="e1c95-118">Agregar una condición que comprueba el contenido de Hola de archivo nuevo o modificado de Hola y hace que un archivo de decisión tooextract Hola si su contenido indica que se debe extraer antes de utilizar el contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1c95-118">You also add a condition that checks hello contents of hello new or modified file, and makes a decision tooextract hello file if its contents indicate that it should be extracted before using hello contents.</span></span> <span data-ttu-id="e1c95-119">Por último, agregue un contenido de hello tooextract de acción de un archivo y colocar el contenido de hello extraído en una carpeta de servidor SFTP de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1c95-119">Finally, add an action tooextract hello contents of a file, and place hello extracted contents in a folder on hello SFTP server.</span></span> 

<span data-ttu-id="e1c95-120">En un ejemplo de la empresa, podría utilizar este toomonitor desencadenador una carpeta SFTP para archivos nuevos que representan los pedidos de los clientes.</span><span class="sxs-lookup"><span data-stu-id="e1c95-120">In an enterprise example, you could use this trigger toomonitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="e1c95-121">A continuación, podría utilizar una acción de conector SFTP, como **obtener el contenido del archivo**, contenido de hello tooget de pedido de Hola para su posterior procesamiento y almacenamiento en una base de datos de pedidos.</span><span class="sxs-lookup"><span data-stu-id="e1c95-121">You could then use an SFTP connector action, such as **Get file content**, tooget hello contents of hello order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="e1c95-122">Agregar una condición</span><span class="sxs-lookup"><span data-stu-id="e1c95-122">Add a condition</span></span>
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="e1c95-123">Uso de una acción de SFTP</span><span class="sxs-lookup"><span data-stu-id="e1c95-123">Use an SFTP action</span></span>
<span data-ttu-id="e1c95-124">Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1c95-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="e1c95-125">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="e1c95-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="e1c95-126">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="e1c95-126">Connector-specific details</span></span>

<span data-ttu-id="e1c95-127">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="e1c95-127">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="e1c95-128">Más conectores</span><span class="sxs-lookup"><span data-stu-id="e1c95-128">More connectors</span></span>
<span data-ttu-id="e1c95-129">Volver atrás toohello [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e1c95-129">Go back toohello [APIs list](apis-list.md).</span></span>
