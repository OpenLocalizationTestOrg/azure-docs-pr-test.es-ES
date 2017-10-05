---
title: Aprenda a usar el conector de FTP en Logic Apps | Microsoft Docs
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. Conéctese a un servidor FTP para administrar sus archivos. En FTP, puede realizar diversas acciones, como cargar, actualizar, obtener y eliminar archivos."
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
ms.openlocfilehash: 61bfbedfd4f1e84b6976099323a32f3a720634c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-ftp-connector"></a><span data-ttu-id="39f78-105">Introducción al conector de FTP</span><span class="sxs-lookup"><span data-stu-id="39f78-105">Get started with the FTP connector</span></span>
<span data-ttu-id="39f78-106">Use el conector de FTP para supervisar, administrar y crear archivos en un servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="39f78-106">Use the FTP connector to monitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="39f78-107">Para poder usar [un conector](apis-list.md), primero debe crear una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="39f78-107">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="39f78-108">Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="39f78-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-ftp"></a><span data-ttu-id="39f78-109">Conexión a un FTP</span><span class="sxs-lookup"><span data-stu-id="39f78-109">Connect to FTP</span></span>
<span data-ttu-id="39f78-110">Para que la aplicación lógica pueda acceder a un servicio, primero debe crear una *conexión* con dicho servicio.</span><span class="sxs-lookup"><span data-stu-id="39f78-110">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="39f78-111">Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="39f78-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-ftp"></a><span data-ttu-id="39f78-112">Creación de una conexión a FTP</span><span class="sxs-lookup"><span data-stu-id="39f78-112">Create a connection to FTP</span></span>
> [!INCLUDE [Steps to create a connection to FTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="39f78-113">Uso de un desencadenador de FTP</span><span class="sxs-lookup"><span data-stu-id="39f78-113">Use a FTP trigger</span></span>
<span data-ttu-id="39f78-114">Un desencadenador es un evento que se puede utilizar para iniciar el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="39f78-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="39f78-115">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="39f78-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="39f78-116">El conector de FTP necesita un servidor FTP que sea accesible desde Internet y que esté configurado para poder funcionar en modo PASIVO.</span><span class="sxs-lookup"><span data-stu-id="39f78-116">The FTP connector requires an FTP server that  is accessible from the Internet and is configured to operate with PASSIVE mode.</span></span> <span data-ttu-id="39f78-117">Además, el conector de FTP **no es compatible con FTPS implícito (FTP por SSL)**.</span><span class="sxs-lookup"><span data-stu-id="39f78-117">Also, the FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="39f78-118">El conector de FTP solo admite FTPS explícito (FTP por SSL).</span><span class="sxs-lookup"><span data-stu-id="39f78-118">The FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="39f78-119">En este ejemplo, le enseñaremos a usar el desencadenador **FTP - When a file is added or modified (FTP: cuando se agrega o modifica un archivo)** para que, cuando se agregue o se modifique un archivo en un servidor FTP, se inicie el flujo de trabajo de una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="39f78-119">In this example, I will show you how to use the **FTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="39f78-120">En un entorno empresarial, podría utilizar este desencadenador para supervisar los nuevos archivos que se agregan a una carpeta FTP y que representan los pedidos de los clientes.</span><span class="sxs-lookup"><span data-stu-id="39f78-120">In an enterprise example, you could use this trigger to monitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="39f78-121">Podría usar una acción del conector de FTP, como **Get file content (Obtener contenido del archivo)**, para obtener el contenido del archivo a fin de procesarlo y almacenarlo después en la base de datos de pedidos.</span><span class="sxs-lookup"><span data-stu-id="39f78-121">You could then use an FTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="39f78-122">Escriba *ftp* en el cuadro de búsqueda del diseñador de Logic Apps y seleccione el desencadenador **FTP - When a file is added or modified (FTP: cuando se agrega o modifica un archivo)**.</span><span class="sxs-lookup"><span data-stu-id="39f78-122">Enter *ftp* in the search box on the logic apps designer then select the **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="39f78-123">![Imagen de desencadenador de FTP 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="39f78-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="39f78-124">Se abre el control **When a file is added or modified** (Cuando se agrega o modifica un archivo).</span><span class="sxs-lookup"><span data-stu-id="39f78-124">The **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="39f78-125">![Imagen de desencadenador de FTP 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="39f78-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="39f78-126">Seleccione la opción **...** situada a la derecha del control.</span><span class="sxs-lookup"><span data-stu-id="39f78-126">Select the **...** located on the right side of the control.</span></span> <span data-ttu-id="39f78-127">Se abrirá el control de selector de carpeta.</span><span class="sxs-lookup"><span data-stu-id="39f78-127">This opens the folder picker control</span></span>  
   <span data-ttu-id="39f78-128">![Imagen de desencadenador de FTP 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="39f78-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="39f78-129">Seleccione la opción **>** (flecha derecha) y busque la carpeta donde quiere supervisar los archivos nuevos o modificados.</span><span class="sxs-lookup"><span data-stu-id="39f78-129">Select the **>** (right arrow) and browse to find the folder that you want to monitor for new or modified files.</span></span> <span data-ttu-id="39f78-130">Al seleccionar la carpeta, observará que esta aparece en el control **Carpeta**.</span><span class="sxs-lookup"><span data-stu-id="39f78-130">Select the folder and notice the folder is now displayed in the **Folder** control.</span></span>  
   <span data-ttu-id="39f78-131">![Imagen de desencadenador de FTP 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="39f78-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="39f78-132">En este punto, la aplicación lógica está configurada con un desencadenador que activará otros desencadenadores y acciones del flujo de trabajo cuando se cree o modifique un archivo en la carpeta FTP especificada.</span><span class="sxs-lookup"><span data-stu-id="39f78-132">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow when a file is either modified or created in the specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="39f78-133">Para que una aplicación lógica sea funcional, debe contener al menos un desencadenador y una acción.</span><span class="sxs-lookup"><span data-stu-id="39f78-133">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="39f78-134">Siga los pasos que se describen en la sección siguiente para agregar una acción.</span><span class="sxs-lookup"><span data-stu-id="39f78-134">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="39f78-135">Uso de una acción de FTP</span><span class="sxs-lookup"><span data-stu-id="39f78-135">Use a FTP action</span></span>
<span data-ttu-id="39f78-136">Una acción es una operación que se lleva a cabo mediante el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="39f78-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="39f78-137">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="39f78-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="39f78-138">Ahora que ha agregado un desencadenador, siga estos pasos para incorporar una acción que obtendrá el contenido del archivo nuevo o modificado detectado por el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="39f78-138">Now that you have added a trigger, follow these steps to add an action that will get the contents of the new or modified file found by the trigger.</span></span>    

1. <span data-ttu-id="39f78-139">Seleccione **+ Nuevo paso** para agregar la acción que obtendrá el contenido del archivo del servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="39f78-139">Select **+ New step** to add the the action to get the contents of the file on the FTP server</span></span>  
2. <span data-ttu-id="39f78-140">Seleccione el vínculo **Add an action** (Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="39f78-140">Select the **Add an action** link.</span></span>  
   <span data-ttu-id="39f78-141">![Imagen de acción de FTP 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="39f78-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="39f78-142">Escriba *FTP* para buscar todas las acciones relacionadas con FTP.</span><span class="sxs-lookup"><span data-stu-id="39f78-142">Enter *FTP* to search for all actions related to FTP.</span></span>
4. <span data-ttu-id="39f78-143">Seleccione **FTP - Get file content (FTP: obtener contenido del archivo)**. Esta será la acción que se ejecutará cuando se encuentre un archivo nuevo o modificado en la carpeta FTP.</span><span class="sxs-lookup"><span data-stu-id="39f78-143">Select **FTP - Get file content**  as the action to take when a new or modified file is found in the FTP folder.</span></span>      
   <span data-ttu-id="39f78-144">![Imagen de acción de FTP 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="39f78-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="39f78-145">Se abrirá el control **Get file content (Obtener contenido del archivo)**.</span><span class="sxs-lookup"><span data-stu-id="39f78-145">The **Get file content** control opens.</span></span> <span data-ttu-id="39f78-146">**Nota**: Si no lo ha hecho previamente, se le pedirá que autorice a la aplicación lógica para que pueda acceder a la cuenta del servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="39f78-146">**Note**: you will be prompted to authorize your logic app to access your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="39f78-147">![Imagen de acción de FTP 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="39f78-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="39f78-148">Seleccione el control **Archivo** (el espacio en blanco situado bajo **ARCHIVO***).</span><span class="sxs-lookup"><span data-stu-id="39f78-148">Select the **File** control (the white space located below **FILE***).</span></span> <span data-ttu-id="39f78-149">Aquí, podrá utilizar cualquiera de las propiedades del archivo nuevo o modificado detectado en el servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="39f78-149">Here, you can use any of the various properties from the new or modified file found on the FTP server.</span></span>  
6. <span data-ttu-id="39f78-150">Seleccione la opción **Contenido del archivo**.</span><span class="sxs-lookup"><span data-stu-id="39f78-150">Select the **File content** option.</span></span>  
   <span data-ttu-id="39f78-151">![Imagen de acción de FTP 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="39f78-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="39f78-152">El control se actualiza, lo que indica que la acción **FTP - Get file content (FTP: obtener contenido del archivo)** obtendrá el *contenido del archivo* nuevo o modificado del servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="39f78-152">The control is updated, indicating that the **FTP - Get file content** action will get the *file content* of the new or modified file on the FTP server.</span></span>      
   <span data-ttu-id="39f78-153">![Imagen de acción de FTP 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="39f78-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="39f78-154">Guarde el trabajo y agregue un archivo a la carpeta FTP para comprobar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="39f78-154">Save your work then add a file to the FTP folder to test your workflow.</span></span>    

<span data-ttu-id="39f78-155">En este punto, la aplicación lógica está configurada con un desencadenador que supervisa una carpeta de un servidor FTP e inicia el flujo de trabajo cuando se detecta un archivo nuevo o modificado en dicho servidor.</span><span class="sxs-lookup"><span data-stu-id="39f78-155">At this point, the logic app has been configured with a trigger to monitor a folder on an FTP server and initiate the workflow when it finds either a new file or a modified file on the FTP server.</span></span> 

<span data-ttu-id="39f78-156">La aplicación lógica también está configurada con una acción que obtiene el contenido del archivo nuevo o modificado.</span><span class="sxs-lookup"><span data-stu-id="39f78-156">The logic app also has been configured with an action to get the contents of the new or modified file.</span></span>

<span data-ttu-id="39f78-157">Puede agregar otra acción; por ejemplo, [SQL Server - insert row (SQL Server: insertar fila)](connectors-create-api-sqlazure.md), para insertar el contenido del archivo nuevo o modificado en una tabla de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="39f78-157">You can now add another action such as the [SQL Server - insert row](connectors-create-api-sqlazure.md) action to insert the contents of the new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="39f78-158">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="39f78-158">Connector-specific details</span></span>

<span data-ttu-id="39f78-159">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="39f78-159">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="39f78-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="39f78-160">Next Steps</span></span>
[<span data-ttu-id="39f78-161">Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="39f78-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

