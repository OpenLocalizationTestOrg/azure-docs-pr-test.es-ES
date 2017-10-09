---
title: "aaaCreate la primera función en Azure con Visual Studio | Documentos de Microsoft"
description: "Crear y publicar un tooAzure de función HTTP desencadenada simple mediante el uso de funciones de Azure Tools para Visual Studio."
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: azure functions, funciones, procesamiento de eventos, proceso, arquitectura sin servidor
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="ca347-104">Creación de la primera función mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ca347-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="ca347-105">Las funciones de Azure permite ejecutar el código en un entorno sin servidor sin necesidad de toofirst crear una máquina virtual o publicar una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ca347-105">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span>

<span data-ttu-id="ca347-106">En este tema, aprenderá cómo toouse Hola 2017 de Visual Studio tools para toocreate de las funciones de Azure y probar una función de "Hola a todos" localmente.</span><span class="sxs-lookup"><span data-stu-id="ca347-106">In this topic, you learn how toouse hello Visual Studio 2017 tools for Azure Functions toocreate and test a "hello world" function locally.</span></span> <span data-ttu-id="ca347-107">A continuación, publicará tooAzure de código de función de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca347-107">You will then publish hello function code tooAzure.</span></span> <span data-ttu-id="ca347-108">Estas herramientas están disponibles como parte de la carga de trabajo de desarrollo de Azure de hello en Visual Studio 2017 versión 15.3, o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="ca347-108">These tools are available as part of hello Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Código Azure Functions en un proyecto de Visual Studio](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="ca347-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ca347-110">Prerequisites</span></span>

<span data-ttu-id="ca347-111">toocomplete este tutorial, programa de instalación:</span><span class="sxs-lookup"><span data-stu-id="ca347-111">toocomplete this tutorial, install:</span></span>

* <span data-ttu-id="ca347-112">[Visual Studio 2017 versión 15.3](https://www.visualstudio.com/vs/preview/), incluidos hello **desarrollo Azure** carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ca347-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including hello **Azure development** workload.</span></span>

    ![Instalar Visual Studio de 2017 con cargas de trabajo de desarrollo de Azure Hola](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="ca347-114">Después de instalar o actualizar tooVisual Studio 2017 versión 15.3, también tendrá que herramientas de toomanually actualización Hola 2017 de Visual Studio para las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="ca347-114">After you install or upgrade tooVisual Studio 2017 version 15.3, you might also need toomanually update hello Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="ca347-115">Puede actualizar herramientas Hola de hello **herramientas** menú situado bajo **extensiones y actualizaciones...**   >  **Actualizaciones** > **Visual Studio Marketplace** > **herramientas de trabajos de las funciones de Azure y Web**  >  **Actualización**.</span><span class="sxs-lookup"><span data-stu-id="ca347-115">You can update hello tools from hello **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="ca347-116">Creación de un proyecto de Azure Functions en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ca347-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="ca347-117">Ahora que ha creado el proyecto de hello, puede crear la primera función.</span><span class="sxs-lookup"><span data-stu-id="ca347-117">Now that you have created hello project, you can create your first function.</span></span>

## <a name="create-hello-function"></a><span data-ttu-id="ca347-118">Crear función hello</span><span class="sxs-lookup"><span data-stu-id="ca347-118">Create hello function</span></span>

1. <span data-ttu-id="ca347-119">En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo del proyecto y seleccione **Agregar** > **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="ca347-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="ca347-120">Seleccione **Función de Azure** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ca347-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="ca347-121">Seleccione **HttpTrigger**, escriba un **nombre de función**, seleccione **Anónimo** en **Derechos de acceso**y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ca347-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="ca347-122">función Hello creada se tiene acceso con una solicitud HTTP desde cualquier cliente.</span><span class="sxs-lookup"><span data-stu-id="ca347-122">hello function created is accessed by an HTTP request from any client.</span></span> 

    ![Crear una nueva función de Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="ca347-124">Un archivo de código se agrega el proyecto tooyour que contiene una clase que implementa el código de función.</span><span class="sxs-lookup"><span data-stu-id="ca347-124">A code file is added tooyour project that contains a class that implements your function code.</span></span> <span data-ttu-id="ca347-125">Este código se basa en una plantilla, que recibe un valor de nombre y lo transmite de nuevo.</span><span class="sxs-lookup"><span data-stu-id="ca347-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="ca347-126">Hola **FunctionName** atributo establece el nombre de hello de la función.</span><span class="sxs-lookup"><span data-stu-id="ca347-126">hello **FunctionName** attribute sets hello name of your function.</span></span> <span data-ttu-id="ca347-127">Hola **HttpTrigger** atributo indica el mensaje de Hola que desencadena la función hello.</span><span class="sxs-lookup"><span data-stu-id="ca347-127">hello **HttpTrigger** attribute indicates hello message that triggers hello function.</span></span> 

    ![Archivo de código de función](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="ca347-129">Ahora que ha creado una función desencadenada por HTTP, puede probarla en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="ca347-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-hello-function-locally"></a><span data-ttu-id="ca347-130">Probar función hello localmente</span><span class="sxs-lookup"><span data-stu-id="ca347-130">Test hello function locally</span></span>

<span data-ttu-id="ca347-131">Azure Functions Core Tools le permite ejecutar un proyecto de Azure Functions en el equipo de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="ca347-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="ca347-132">Son solicitada tooinstall estas herramientas Hola la primera vez que inicie una función de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca347-132">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="ca347-133">tootest su función, presione F5.</span><span class="sxs-lookup"><span data-stu-id="ca347-133">tootest your function, press F5.</span></span> <span data-ttu-id="ca347-134">Si se le solicita, Aceptar solicitud Hola de toodownload de Visual Studio e instalar herramientas de núcleo de las funciones de Azure (CLI).</span><span class="sxs-lookup"><span data-stu-id="ca347-134">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="ca347-135">También deberá tooenable una excepción de firewall para que las herramientas de hello pueden administrar las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="ca347-135">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="ca347-136">Copiar dirección URL de saludo de la función de tiempo de ejecución de funciones de Azure Hola de salida.</span><span class="sxs-lookup"><span data-stu-id="ca347-136">Copy hello URL of your function from hello Azure Functions runtime output.</span></span>  

    ![Runtime local de Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="ca347-138">Pegue la URL de Hola de solicitud HTTP de hello en barra de direcciones de su explorador.</span><span class="sxs-lookup"><span data-stu-id="ca347-138">Paste hello URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="ca347-139">Anexar la cadena de consulta de hello `&name=<yourname>` toothis URL y ejecutar la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="ca347-139">Append hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span> <span data-ttu-id="ca347-140">siguiente Hello muestra respuesta hello en hello explorador toohello local GET solicitud devuelto por la función hello:</span><span class="sxs-lookup"><span data-stu-id="ca347-140">hello following shows hello response in hello browser toohello local GET request returned by hello function:</span></span> 

    ![Respuesta de host local de la función en el Explorador de Hola](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="ca347-142">toostop depuración, haga clic en hello **detener** botón de barra de herramientas de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="ca347-142">toostop debugging, click hello **Stop** button on hello Visual Studio toolbar.</span></span>

<span data-ttu-id="ca347-143">Una vez que haya comprobado que función hello se ejecuta correctamente en el equipo local, es hora toopublish Hola proyecto tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ca347-143">After you have verified that hello function runs correctly on your local computer, it's time toopublish hello project tooAzure.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="ca347-144">Publicar Hola proyecto tooAzure</span><span class="sxs-lookup"><span data-stu-id="ca347-144">Publish hello project tooAzure</span></span>

<span data-ttu-id="ca347-145">Debe tener una aplicación de función en la suscripción de Azure para poder publicar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ca347-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="ca347-146">Las aplicaciones de función se pueden crear directamente desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca347-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="ca347-147">Prueba de una función en Azure</span><span class="sxs-lookup"><span data-stu-id="ca347-147">Test your function in Azure</span></span>

1. <span data-ttu-id="ca347-148">Copiar dirección URL base de Hola de aplicación de la función de hello desde la página de perfil de publicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca347-148">Copy hello base URL of hello function app from hello Publish profile page.</span></span> <span data-ttu-id="ca347-149">Reemplace hello `localhost:port` parte de la dirección URL de Hola que utilizó al probar la función hello localmente con la dirección URL base nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="ca347-149">Replace hello `localhost:port` portion of hello URL you used when testing hello function locally with hello new base URL.</span></span> <span data-ttu-id="ca347-150">Al igual que antes, asegúrese de cadena de consulta de hello tooappend seguro `&name=<yourname>` toothis URL y ejecutar la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="ca347-150">As before, make sure tooappend hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span>

    <span data-ttu-id="ca347-151">dirección URL de Hola que llama el HTTP desencadena función es similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="ca347-151">hello URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="ca347-152">Pegue esta nueva dirección URL de solicitud de hello HTTP en la barra de direcciones del explorador.</span><span class="sxs-lookup"><span data-stu-id="ca347-152">Paste this new URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="ca347-153">siguiente Hello muestra respuesta hello en hello explorador toohello remoto GET solicitud devuelto por la función hello:</span><span class="sxs-lookup"><span data-stu-id="ca347-153">hello following shows hello response in hello browser toohello remote GET request returned by hello function:</span></span> 

    ![Respuesta de la función en el Explorador de Hola](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="ca347-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ca347-155">Next steps</span></span>

<span data-ttu-id="ca347-156">Ha usado la aplicación de función de Visual Studio toocreate C# con una función simple de HTTP que se desencadena.</span><span class="sxs-lookup"><span data-stu-id="ca347-156">You have used Visual Studio toocreate a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="ca347-157">toolearn cómo tooconfigure su toosupport proyecto otros tipos de desencadenadores y enlaces, vea hello [configurar proyectos de hello para el desarrollo local](functions-develop-vs.md#configure-the-project-for-local-development) sección [funciones de Azure Tools para Visual Studio](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="ca347-157">toolearn how tooconfigure your project toosupport other types of triggers and bindings, see hello [Configure hello project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="ca347-158">toolearn más información acerca de probarlo y depuración con herramientas de hello Azure funciones principales, vea [código y probar las funciones de Azure localmente](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="ca347-158">toolearn more about local testing and debugging using hello Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="ca347-159">toolearn más sobre el desarrollo de las funciones como bibliotecas de clases. NET, vea [bibliotecas de clases de .NET usando con funciones de Azure](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="ca347-159">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

