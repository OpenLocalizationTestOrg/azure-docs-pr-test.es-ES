---
title: "aaaLearn cómo toouse Hola conector FTP en las aplicaciones lógicas | Documentos de Microsoft"
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. Conectar tooFTP server toomanage los archivos. En FTP, puede realizar diversas acciones, como cargar, actualizar, obtener y eliminar archivos."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a><span data-ttu-id="93035-105">Empezar a trabajar con el conector FTP de Hola</span><span class="sxs-lookup"><span data-stu-id="93035-105">Get started with hello FTP connector</span></span>
<span data-ttu-id="93035-106">Usar Hola FTP conector toomonitor, administrar y crear archivos en un servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="93035-106">Use hello FTP connector toomonitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="93035-107">toouse [cualquier conector](apis-list.md), primero debe toocreate una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="93035-107">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="93035-108">Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="93035-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooftp"></a><span data-ttu-id="93035-109">Conectar tooFTP</span><span class="sxs-lookup"><span data-stu-id="93035-109">Connect tooFTP</span></span>
<span data-ttu-id="93035-110">Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero debe toocreate una *conexión* toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="93035-110">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="93035-111">Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="93035-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tooftp"></a><span data-ttu-id="93035-112">Crear una conexión tooFTP</span><span class="sxs-lookup"><span data-stu-id="93035-112">Create a connection tooFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="93035-113">Uso de un desencadenador de FTP</span><span class="sxs-lookup"><span data-stu-id="93035-113">Use a FTP trigger</span></span>
<span data-ttu-id="93035-114">Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica.</span><span class="sxs-lookup"><span data-stu-id="93035-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="93035-115">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="93035-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="93035-116">conector FTP de Hello requiere un servidor FTP que es accesible desde Internet hello y está configurada toooperate con el modo pasivo.</span><span class="sxs-lookup"><span data-stu-id="93035-116">hello FTP connector requires an FTP server that  is accessible from hello Internet and is configured toooperate with PASSIVE mode.</span></span> <span data-ttu-id="93035-117">Además, el conector de hello FTP es **no es compatible con implícita FTPS (FTP sobre SSL)**.</span><span class="sxs-lookup"><span data-stu-id="93035-117">Also, hello FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="93035-118">conector FTP de Hello solo admite explícita FTPS (FTP sobre SSL).</span><span class="sxs-lookup"><span data-stu-id="93035-118">hello FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="93035-119">En este ejemplo, le mostrará cómo hello toouse **FTP: cuando se agrega o modifica un archivo** desencadenar tooinitiate un flujo de trabajo de aplicación lógica cuando se agregan a un archivo, o modifica en un servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="93035-119">In this example, I will show you how toouse hello **FTP - When a file is added or modified** trigger tooinitiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="93035-120">En un ejemplo de la empresa, podría utilizar este toomonitor desencadenador una carpeta FTP para los archivos nuevos que representan los pedidos de los clientes.</span><span class="sxs-lookup"><span data-stu-id="93035-120">In an enterprise example, you could use this trigger toomonitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="93035-121">A continuación, podría utilizar una acción de conector FTP como **obtener el contenido del archivo** tooget contenido de Hola Hola del orden de para su posterior procesamiento y almacenamiento en la base de datos de pedidos.</span><span class="sxs-lookup"><span data-stu-id="93035-121">You could then use an FTP connector action such as **Get file content** tooget hello contents of hello order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="93035-122">Escriba *ftp* en el cuadro de búsqueda de hello en el Diseñador de aplicaciones de lógica de hello, a continuación, seleccione hello **FTP: cuando se agrega o modifica un archivo** desencadenador</span><span class="sxs-lookup"><span data-stu-id="93035-122">Enter *ftp* in hello search box on hello logic apps designer then select hello **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="93035-123">![Imagen de desencadenador de FTP 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="93035-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="93035-124">Hola **cuando se agrega o modifica un archivo** abrirá control</span><span class="sxs-lookup"><span data-stu-id="93035-124">hello **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="93035-125">![Imagen de desencadenador de FTP 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="93035-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="93035-126">Seleccione hello **...**  ubicado en hello derecha del control de Hola.</span><span class="sxs-lookup"><span data-stu-id="93035-126">Select hello **...** located on hello right side of hello control.</span></span> <span data-ttu-id="93035-127">Esto abre el control de selector de carpeta Hola</span><span class="sxs-lookup"><span data-stu-id="93035-127">This opens hello folder picker control</span></span>  
   <span data-ttu-id="93035-128">![Imagen de desencadenador de FTP 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="93035-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="93035-129">Seleccione hello  **>**  (flecha derecha) y busque la carpeta de hello toofind que desea toomonitor para archivos nuevos o modificados.</span><span class="sxs-lookup"><span data-stu-id="93035-129">Select hello **>** (right arrow) and browse toofind hello folder that you want toomonitor for new or modified files.</span></span> <span data-ttu-id="93035-130">Seleccione la carpeta de hello y observe carpeta Hola aparece ahora en hello **carpeta** control.</span><span class="sxs-lookup"><span data-stu-id="93035-130">Select hello folder and notice hello folder is now displayed in hello **Folder** control.</span></span>  
   <span data-ttu-id="93035-131">![Imagen de desencadenador de FTP 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="93035-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="93035-132">En este punto, la aplicación lógica se ha configurado con un desencadenador que comience una ejecución del programa Hola a otros desencadenadores y acciones de flujo de trabajo de hello cuando un archivo se modifica o se crea en carpeta FTP específico de Hola.</span><span class="sxs-lookup"><span data-stu-id="93035-132">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow when a file is either modified or created in hello specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="93035-133">Para que una toobe de aplicación lógica funcional, debe contener al menos un desencadenador y una acción.</span><span class="sxs-lookup"><span data-stu-id="93035-133">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="93035-134">Siga los pasos de Hola Hola siguiente sección tooadd una acción.</span><span class="sxs-lookup"><span data-stu-id="93035-134">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="93035-135">Uso de una acción de FTP</span><span class="sxs-lookup"><span data-stu-id="93035-135">Use a FTP action</span></span>
<span data-ttu-id="93035-136">Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="93035-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="93035-137">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="93035-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="93035-138">Ahora que ha agregado un desencadenador, siga estas tooadd pasos una acción que van a obtener contenido de Hola de hello nuevos o modificados se encuentra el archivo desencadenador Hola.</span><span class="sxs-lookup"><span data-stu-id="93035-138">Now that you have added a trigger, follow these steps tooadd an action that will get hello contents of hello new or modified file found by hello trigger.</span></span>    

1. <span data-ttu-id="93035-139">Seleccione **+ nuevo paso** tooadd Hola Hola acción tooget Hola contenido de archivo hello en servidor hello FTP</span><span class="sxs-lookup"><span data-stu-id="93035-139">Select **+ New step** tooadd hello hello action tooget hello contents of hello file on hello FTP server</span></span>  
2. <span data-ttu-id="93035-140">Seleccione hello **agregar una acción** vínculo.</span><span class="sxs-lookup"><span data-stu-id="93035-140">Select hello **Add an action** link.</span></span>  
   <span data-ttu-id="93035-141">![Imagen de acción de FTP 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="93035-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="93035-142">Escriba *FTP* toosearch para todas las acciones relacionadas con tooFTP.</span><span class="sxs-lookup"><span data-stu-id="93035-142">Enter *FTP* toosearch for all actions related tooFTP.</span></span>
4. <span data-ttu-id="93035-143">Seleccione **FTP: obtener el contenido del archivo** como Hola tootake acción cuando un archivo nuevo o modificado se encuentra en la carpeta de hello FTP.</span><span class="sxs-lookup"><span data-stu-id="93035-143">Select **FTP - Get file content**  as hello action tootake when a new or modified file is found in hello FTP folder.</span></span>      
   <span data-ttu-id="93035-144">![Imagen de acción de FTP 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="93035-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="93035-145">Hola **obtener el contenido del archivo** controlar se abre.</span><span class="sxs-lookup"><span data-stu-id="93035-145">hello **Get file content** control opens.</span></span> <span data-ttu-id="93035-146">**Tenga en cuenta**: será solicitada tooauthorize su tooaccess de aplicación lógica, el servidor FTP de la cuenta si aún no lo hecho previamente.</span><span class="sxs-lookup"><span data-stu-id="93035-146">**Note**: you will be prompted tooauthorize your logic app tooaccess your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="93035-147">![Imagen de acción de FTP 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="93035-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="93035-148">Seleccione hello **archivo** control (Hola espacios en blanco que se encuentra debajo de **archivo***).</span><span class="sxs-lookup"><span data-stu-id="93035-148">Select hello **File** control (hello white space located below **FILE***).</span></span> <span data-ttu-id="93035-149">En este caso, puede utilizar cualquiera de hello varias propiedades de hello nuevos o modificados se encuentra el archivo en el servidor FTP de Hola.</span><span class="sxs-lookup"><span data-stu-id="93035-149">Here, you can use any of hello various properties from hello new or modified file found on hello FTP server.</span></span>  
6. <span data-ttu-id="93035-150">Seleccione hello **el contenido del archivo** opción.</span><span class="sxs-lookup"><span data-stu-id="93035-150">Select hello **File content** option.</span></span>  
   <span data-ttu-id="93035-151">![Imagen de acción de FTP 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="93035-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="93035-152">se actualiza el control Hello, que indica que hello **FTP: obtener el contenido del archivo** acción obtendrá hello *el contenido del archivo* del archivo de Hola nuevos o modificados en el servidor de hello FTP.</span><span class="sxs-lookup"><span data-stu-id="93035-152">hello control is updated, indicating that hello **FTP - Get file content** action will get hello *file content* of hello new or modified file on hello FTP server.</span></span>      
   <span data-ttu-id="93035-153">![Imagen de acción de FTP 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="93035-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="93035-154">Guarde su trabajo, a continuación, agregue un tootest de carpeta de archivo toohello FTP en el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="93035-154">Save your work then add a file toohello FTP folder tootest your workflow.</span></span>    

<span data-ttu-id="93035-155">En este momento, ha sido la aplicación de la lógica de hello configurado con un desencadenador toomonitor una carpeta en un servidor FTP y el flujo de trabajo de hello iniciar cuando encuentra un nuevo archivo o abrir un archivo modificado en el servidor de hello FTP.</span><span class="sxs-lookup"><span data-stu-id="93035-155">At this point, hello logic app has been configured with a trigger toomonitor a folder on an FTP server and initiate hello workflow when it finds either a new file or a modified file on hello FTP server.</span></span> 

<span data-ttu-id="93035-156">aplicación de la lógica de Hello también se ha configurado con un contenido de Hola de acción tooget del archivo Hola de nuevo o modificado.</span><span class="sxs-lookup"><span data-stu-id="93035-156">hello logic app also has been configured with an action tooget hello contents of hello new or modified file.</span></span>

<span data-ttu-id="93035-157">Ahora puede agregar otra acción, como hello [SQL Server - Insertar fila](connectors-create-api-sqlazure.md) contenido de hello tooinsert de acción del archivo de hello nuevos o modificados en una tabla de base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="93035-157">You can now add another action such as hello [SQL Server - insert row](connectors-create-api-sqlazure.md) action tooinsert hello contents of hello new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="93035-158">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="93035-158">Connector-specific details</span></span>

<span data-ttu-id="93035-159">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="93035-159">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="93035-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="93035-160">Next Steps</span></span>
[<span data-ttu-id="93035-161">Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="93035-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

