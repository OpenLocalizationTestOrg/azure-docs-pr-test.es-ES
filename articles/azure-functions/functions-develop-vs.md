---
title: Desarrollo de Azure Functions con Visual Studio | Microsoft Docs
description: "Obtenga información sobre cómo desarrollar y probar Azure Functions mediante Herramientas de Azure Functions para Visual Studio 2017."
services: functions
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: glenga
ms.openlocfilehash: 1e0568bc58e8879cabe409cf8e9b5866f922e7c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a><span data-ttu-id="b33bf-103">Herramientas de Azure Functions para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b33bf-103">Azure Functions Tools for Visual Studio</span></span>  

<span data-ttu-id="b33bf-104">Herramientas de Azure Functions para Visual Studio 2017 es una extensión para Visual Studio que le permite desarrollar, probar e implementar funciones de C# en Azure.</span><span class="sxs-lookup"><span data-stu-id="b33bf-104">Azure Functions Tools for Visual Studio 2017 is an extension for Visual Studio that lets you develop, test, and deploy C# functions to Azure.</span></span> <span data-ttu-id="b33bf-105">Si esta es su primera experiencia con Azure Functions, puede obtener más información en [Introducción a Azure Functions](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b33bf-105">If this is your first experience with Azure Functions, you can learn more at [An introduction to Azure Functions](functions-overview.md).</span></span>

<span data-ttu-id="b33bf-106">Herramientas de Azure Functions proporciona los siguientes beneficios:</span><span class="sxs-lookup"><span data-stu-id="b33bf-106">The Azure Functions Tools provides the following benefits:</span></span> 

* <span data-ttu-id="b33bf-107">Editar, compilar y ejecutar funciones en el equipo de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="b33bf-107">Edit, build, and run functions on your local development computer.</span></span> 
* <span data-ttu-id="b33bf-108">Publicar su proyecto de Azure Functions directamente en Azure.</span><span class="sxs-lookup"><span data-stu-id="b33bf-108">Publish your Azure Functions project directly to Azure.</span></span> 
* <span data-ttu-id="b33bf-109">Usar atributos de WebJobs para declarar los enlaces de función directamente en el código C# en lugar de mantener un function.json separado para enlazar definiciones.</span><span class="sxs-lookup"><span data-stu-id="b33bf-109">Use WebJobs attributes to declare function bindings directly in the C# code instead of maintaining a separate function.json for binding definitions.</span></span>
* <span data-ttu-id="b33bf-110">Desarrollar e implementar funciones de C# compiladas previamente.</span><span class="sxs-lookup"><span data-stu-id="b33bf-110">Develop and deploy pre-compiled C# functions.</span></span> <span data-ttu-id="b33bf-111">Las funciones compiladas previamente proporcionan un mejor rendimiento de arranque en frío que las funciones basadas en scripts de C#.</span><span class="sxs-lookup"><span data-stu-id="b33bf-111">Pre-complied functions provide a better cold-start performance than C# script-based functions.</span></span> 
* <span data-ttu-id="b33bf-112">Programar las funciones en C# a la vez que se tienen todos los beneficios del desarrollo de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b33bf-112">Code your functions in C# while having all of the benefits of Visual Studio development.</span></span> 

<span data-ttu-id="b33bf-113">En este tema se muestra cómo usar Herramientas de Azure Functions para Visual Studio 2017 a fin de desarrollar las funciones en C#.</span><span class="sxs-lookup"><span data-stu-id="b33bf-113">This topic shows you how to use the Azure Functions Tools for Visual Studio 2017 to develop your functions in C#.</span></span> <span data-ttu-id="b33bf-114">También puede obtener información sobre cómo publicar el proyecto en Azure como un ensamblado .NET.</span><span class="sxs-lookup"><span data-stu-id="b33bf-114">You also learn how to publish your project to Azure as a .NET assembly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b33bf-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b33bf-115">Prerequisites</span></span>

<span data-ttu-id="b33bf-116">Las herramientas de Azure Functions forman parte de la carga de trabajo de desarrollo de Azure de la [versión 15.3 de Visual Studio 2017](https://www.visualstudio.com/vs/) y las posteriores.</span><span class="sxs-lookup"><span data-stu-id="b33bf-116">Azure Functions Tools is included in the Azure development workload of [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/), or a later version.</span></span> <span data-ttu-id="b33bf-117">Asegúrese de incluir la carga de trabajo de **desarrollo Azure** en la instalación de la versión 15.3 de Visual Studio 2017:</span><span class="sxs-lookup"><span data-stu-id="b33bf-117">Make sure you include the **Azure development** workload in your Visual Studio 2017 version 15.3 installation:</span></span>

![Instalar Visual Studio 2017 con la cargas de trabajo Desarrollo de Azure](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

<span data-ttu-id="b33bf-119">Para crear e implementar funciones, también necesita:</span><span class="sxs-lookup"><span data-stu-id="b33bf-119">To create and deploy functions, you also need:</span></span>

* <span data-ttu-id="b33bf-120">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="b33bf-120">An active Azure subscription.</span></span> <span data-ttu-id="b33bf-121">Si no tiene una suscripción de Azure, hay disponibles [cuentas gratis](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="b33bf-121">If you don't have an Azure subscription, [free accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) are available.</span></span>

* <span data-ttu-id="b33bf-122">Una cuenta de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b33bf-122">An Azure Storage account.</span></span> <span data-ttu-id="b33bf-123">Para crear una cuenta de almacenamiento, consulte [Creación de una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="b33bf-123">To create a storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
## <a name="create-an-azure-functions-project"></a><span data-ttu-id="b33bf-124">Creación de un proyecto de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b33bf-124">Create an Azure Functions project</span></span> 

[!INCLUDE [Create a project using the Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-the-project-for-local-development"></a><span data-ttu-id="b33bf-125">Configuración del proyecto para el desarrollo local</span><span class="sxs-lookup"><span data-stu-id="b33bf-125">Configure the project for local development</span></span>

<span data-ttu-id="b33bf-126">Cuando crea un proyecto nuevo con la plantilla de Azure Functions, obtiene un proyecto C# vacío que contiene los archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b33bf-126">When you create a new project using the Azure Functions template, you get an empty C# project that contains the following files:</span></span>

* <span data-ttu-id="b33bf-127">**host.json**: permite configurar el host de Functions.</span><span class="sxs-lookup"><span data-stu-id="b33bf-127">**host.json**: Lets you configure the Functions host.</span></span> <span data-ttu-id="b33bf-128">Esta configuración se aplica tanto cuando se ejecuta localmente como en Azure.</span><span class="sxs-lookup"><span data-stu-id="b33bf-128">These settings apply both when running locally and in Azure.</span></span> <span data-ttu-id="b33bf-129">Para más información, consulte el artículo de referencia sobre [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="b33bf-129">For more information, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) reference article.</span></span>
    
* <span data-ttu-id="b33bf-130">**local.settings.json**: mantiene la configuración que se usa cuando se ejecutan localmente las funciones.</span><span class="sxs-lookup"><span data-stu-id="b33bf-130">**local.settings.json**: Maintains settings used when running functions locally.</span></span> <span data-ttu-id="b33bf-131">Azure no usa estas configuraciones, sino que las usa [Azure Functions Core Tools](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="b33bf-131">These settings are not used by Azure, they are used by the [Azure Functions Core Tools](functions-run-local.md).</span></span> <span data-ttu-id="b33bf-132">Use este archivo para especificar la configuración, tal como las cadenas de conexión a otros servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="b33bf-132">Use this file to specify settings, such as connection strings to other Azure services.</span></span> <span data-ttu-id="b33bf-133">Agregue una clave nueva a la matriz de **valores** para cada conexión que requieren las funciones de su proyecto.</span><span class="sxs-lookup"><span data-stu-id="b33bf-133">Add a new key to the **Values** array for each connection required by functions in your project.</span></span> <span data-ttu-id="b33bf-134">Para más información, consulte [Archivo de configuración local](functions-run-local.md#local-settings-file) en el tema Azure Functions Core Tools.</span><span class="sxs-lookup"><span data-stu-id="b33bf-134">For more information, see [Local settings file](functions-run-local.md#local-settings-file) in the Azure Functions Core Tools topic.</span></span>

<span data-ttu-id="b33bf-135">El entorno de tiempo de ejecución de Functions usa internamente una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b33bf-135">The Functions runtime uses an Azure Storage account internally.</span></span> <span data-ttu-id="b33bf-136">Para todos los tipos de desencadenadores distintos de HTTP y webhooks, debe establecer la clave **Values.AzureWebJobsStorage** en una cadena de conexión de cuenta de Azure Storage válida.</span><span class="sxs-lookup"><span data-stu-id="b33bf-136">For all trigger types other than HTTP and webhooks, you must set the **Values.AzureWebJobsStorage** key to a valid Azure Storage account connection string.</span></span>

[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

 <span data-ttu-id="b33bf-137">Para establecer la cadena de conexión de cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="b33bf-137">To set the storage account connection string:</span></span>

1. <span data-ttu-id="b33bf-138">En Visual Studio, abra **Cloud Explorer**, expanda **Cuenta de almacenamiento** > **Su cuenta de almacenamiento** y seleccione **Propiedades** y copie el valor **Cadena de conexión principal**.</span><span class="sxs-lookup"><span data-stu-id="b33bf-138">In Visual Studio, open **Cloud Explorer**, expand **Storage Account** > **Your Storage Account**, then select **Properties** and copy the **Primary Connection String** value.</span></span>   

2. <span data-ttu-id="b33bf-139">En el proyecto, abra el archivo del proyecto local.settings.json y establezca el valor de la clave **AzureWebJobsStorage** en la cadena de conexión que copió.</span><span class="sxs-lookup"><span data-stu-id="b33bf-139">In your project, open the local.settings.json project file and set the value of the **AzureWebJobsStorage** key to the connection string you copied.</span></span>

3. <span data-ttu-id="b33bf-140">Repita el paso anterior para agregar claves únicas a la matriz de **valores** para cualquier otra conexión que requieran sus funciones.</span><span class="sxs-lookup"><span data-stu-id="b33bf-140">Repeat the previous step to add unique keys to the **Values** array for any other connections required by your functions.</span></span>  

## <a name="create-a-function"></a><span data-ttu-id="b33bf-141">Creación de una función</span><span class="sxs-lookup"><span data-stu-id="b33bf-141">Create a function</span></span>

<span data-ttu-id="b33bf-142">En las funciones compiladas previamente, los enlaces que la función usa se definen mediante la aplicación de atributos en el código.</span><span class="sxs-lookup"><span data-stu-id="b33bf-142">In pre-compiled functions, the bindings used by the function are defined by applying attributes in the code.</span></span> <span data-ttu-id="b33bf-143">Cuando usa Herramientas de Azure Functions para crear las funciones a partir de las plantillas proporcionadas, estos atributos se aplican automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b33bf-143">When you use the Azure Functions Tools to create your functions from the provided templates, these attributes are applied for you.</span></span> 

1. <span data-ttu-id="b33bf-144">En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo del proyecto y seleccione **Agregar** > **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="b33bf-144">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="b33bf-145">Seleccione **Función de Azure**, escriba un **nombre** para la clase y, luego, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b33bf-145">Select **Azure Function**, type a **Name** for the class, and click **Add**.</span></span>

2. <span data-ttu-id="b33bf-146">Elija el desencadenador, establezca las propiedades de enlace y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b33bf-146">Choose your trigger, set the binding properties, and click **Create**.</span></span> <span data-ttu-id="b33bf-147">En el ejemplo siguiente se muestra la configuración cuando se crea una función desencadenada de Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="b33bf-147">The following example shows the settings when creating a Queue storage triggered function.</span></span> 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    <span data-ttu-id="b33bf-148">Se suministra una clave de cadena de conexión de nominada **QueueStorage**, que se define en el archivo local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="b33bf-148">A connection string key named **QueueStorage** is supplied, which is defined in the local.settings.json file.</span></span> 
 
3. <span data-ttu-id="b33bf-149">Examine la clase recién agregada.</span><span class="sxs-lookup"><span data-stu-id="b33bf-149">Examine the newly added class.</span></span> <span data-ttu-id="b33bf-150">Verá un método **Run** estático, que cuenta con el atributo **FunctionName**.</span><span class="sxs-lookup"><span data-stu-id="b33bf-150">You see a static **Run** method, that is attributed with the **FunctionName** attribute.</span></span> <span data-ttu-id="b33bf-151">Este atributo indica que el método es el punto de entrada de la función.</span><span class="sxs-lookup"><span data-stu-id="b33bf-151">This attribute indicates that the method is the entry point for the function.</span></span> 

    <span data-ttu-id="b33bf-152">Por ejemplo, la clase C# siguiente representa una función desencadenada de Queue Storage:</span><span class="sxs-lookup"><span data-stu-id="b33bf-152">For example, the following C# class represents a basic Queue storage triggered function:</span></span>

    ````csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;
    
    namespace FunctionApp1
    {
        public static class Function1
        {
            [FunctionName("QueueTriggerCSharp")]        
            public static void Run([QueueTrigger("myqueue-items", Connection = "QueueStorage")]string myQueueItem, TraceWriter log)
            {
                log.Info($"C# Queue trigger function processed: {myQueueItem}");
            }
        }
    } 
    ````
 
    <span data-ttu-id="b33bf-153">Se aplica un atributo específico de enlace a cada parámetro de enlace que se suministra al método de punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="b33bf-153">A binding-specific attribute is applied to each binding parameter supplied to the entry point method.</span></span> <span data-ttu-id="b33bf-154">El atributo toma la información de enlace como parámetros.</span><span class="sxs-lookup"><span data-stu-id="b33bf-154">The attribute takes the binding information as parameters.</span></span> <span data-ttu-id="b33bf-155">En el ejemplo anterior, el primer parámetro tiene aplicado un atributo **QueueTrigger**, que indica la función desencadenada de cola.</span><span class="sxs-lookup"><span data-stu-id="b33bf-155">In the previous example, The first parameter has a **QueueTrigger** attribute applied, indicating queue triggered function.</span></span> <span data-ttu-id="b33bf-156">El nombre de la configuración de cadena de conexión y el nombre de cola se pasan como parámetros.</span><span class="sxs-lookup"><span data-stu-id="b33bf-156">The queue name and connection string setting name are passed as parameters.</span></span>  

## <a name="testing-functions"></a><span data-ttu-id="b33bf-157">Funciones de prueba</span><span class="sxs-lookup"><span data-stu-id="b33bf-157">Testing functions</span></span>

<span data-ttu-id="b33bf-158">Azure Functions Core Tools le permite ejecutar un proyecto de Azure Functions en el equipo de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="b33bf-158">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="b33bf-159">Se le solicita que instale estas herramientas la primera vez que inicie una función de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b33bf-159">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>  

<span data-ttu-id="b33bf-160">Para probar la función, presione F5.</span><span class="sxs-lookup"><span data-stu-id="b33bf-160">To test your function, press F5.</span></span> <span data-ttu-id="b33bf-161">Si se le solicita, acepte la solicitud de Visual Studio para descargar e instalar las herramientas de Azure Functions Core (CLI).</span><span class="sxs-lookup"><span data-stu-id="b33bf-161">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="b33bf-162">También es preciso que habilite una excepción de firewall para que las herramientas para controlen las solicitudes de HTTP.</span><span class="sxs-lookup"><span data-stu-id="b33bf-162">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

<span data-ttu-id="b33bf-163">Con el proyecto en ejecución, puede probar el código tal como probaría la función implementada.</span><span class="sxs-lookup"><span data-stu-id="b33bf-163">With the project running, you can test your code as you would test deployed function.</span></span> <span data-ttu-id="b33bf-164">Para más información, consulte [Estrategias para probar el código en Azure Functions](functions-test-a-function.md).</span><span class="sxs-lookup"><span data-stu-id="b33bf-164">For more information, see [Strategies for testing your code in Azure Functions](functions-test-a-function.md).</span></span> <span data-ttu-id="b33bf-165">Cuando se ejecuta en modo de depuración, los puntos de interrupción se alcanzan en Visual Studio tal como se esperaba.</span><span class="sxs-lookup"><span data-stu-id="b33bf-165">When running in debug mode, breakpoints are hit in Visual Studio as expected.</span></span> 

<span data-ttu-id="b33bf-166">Para un ejemplo de cómo probar una función desencadenada de cola, consulte el [tutorial de inicio rápido de la función desencadenada de cola](functions-create-storage-queue-triggered-function.md#test-the-function).</span><span class="sxs-lookup"><span data-stu-id="b33bf-166">For an example of how to test a queue triggered function, see the [queue triggered function quickstart tutorial](functions-create-storage-queue-triggered-function.md#test-the-function).</span></span>  

<span data-ttu-id="b33bf-167">Para más información sobre cómo usar Azure Functions Core Tools, consulte [Codificación y comprobación de las funciones de Azure en un entorno local](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="b33bf-167">To learn more about using the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>

## <a name="publish-to-azure"></a><span data-ttu-id="b33bf-168">Publicación en Azure</span><span class="sxs-lookup"><span data-stu-id="b33bf-168">Publish to Azure</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
><span data-ttu-id="b33bf-169">Cualquier configuración que agregue en local.settings.json debe agregarse a la aplicación de función en Azure.</span><span class="sxs-lookup"><span data-stu-id="b33bf-169">Any settings you added in the local.settings.json must be also added to the function app in Azure.</span></span> <span data-ttu-id="b33bf-170">Esta configuración no se agrega automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b33bf-170">These settings are not added automatically.</span></span> <span data-ttu-id="b33bf-171">Puede agregar la configuración necesaria a la aplicación de función de alguna de estas maneras:</span><span class="sxs-lookup"><span data-stu-id="b33bf-171">You can add required settings to your function app in one of these ways:</span></span>
>
>* <span data-ttu-id="b33bf-172">[Uso de Azure Portal](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="b33bf-172">[Using the Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>
>* <span data-ttu-id="b33bf-173">[Uso de la opción de publicación de `--publish-local-settings` en Herramientas principales de Azure Functions](functions-run-local.md#publish).</span><span class="sxs-lookup"><span data-stu-id="b33bf-173">[Using the `--publish-local-settings` publish option in the Azure Functions Core Tools](functions-run-local.md#publish).</span></span>
>* <span data-ttu-id="b33bf-174">[Uso de la CLI de Azure](/cli/azure/functionapp/config/appsettings#set).</span><span class="sxs-lookup"><span data-stu-id="b33bf-174">[Using the Azure CLI](/cli/azure/functionapp/config/appsettings#set).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b33bf-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b33bf-175">Next steps</span></span>

<span data-ttu-id="b33bf-176">Para más información sobre Herramientas de Azure Functions, consulte la sección Preguntas comunes de la entrada de blog [Herramientas de Visual Studio 2017 para Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="b33bf-176">For more information about Azure Functions Tools, see the Common Questions section of the [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog post.</span></span>

<span data-ttu-id="b33bf-177">Para más información sobre Azure Functions Core Tools, consulte [Codificación y comprobación de las funciones de Azure en un entorno local](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="b33bf-177">To learn more about the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>  
<span data-ttu-id="b33bf-178">Para más información sobre el desarrollo de funciones como bibliotecas de clases .NET, consulte [Utilizar bibliotecas de clases de .NET con Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="b33bf-178">To learn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> <span data-ttu-id="b33bf-179">En este tema también se ofrecen ejemplos sobre cómo usar atributos para declarar varios tipos de vínculos admitidos por Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="b33bf-179">This topic also provides examples of how to use attributes to declare the various types of bindings supported by Azure Functions.</span></span>    
