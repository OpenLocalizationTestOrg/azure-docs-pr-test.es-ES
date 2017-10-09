---
title: "aaaRetrain aprendizaje automático se modela mediante programación | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprogrammatically volver a entrenar un modelo y actualización hello web servicio toouse Hola recién entrenado en aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="002dc-103">Volver a entrenar modelos de aprendizaje automático mediante programación</span><span class="sxs-lookup"><span data-stu-id="002dc-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="002dc-104">En este tutorial, aprenderá cómo tooprogrammatically volver a entrenar a un servicio de Web de aprendizaje de máquina de Azure con C# y Hola servicio de ejecución de lotes de aprendizaje de máquina.</span><span class="sxs-lookup"><span data-stu-id="002dc-104">In this walkthrough, you will learn how tooprogrammatically retrain an Azure Machine Learning Web Service using C# and hello Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="002dc-105">Una vez que se vuelven a entrenar el modelo de hello, Hola siguientes tutoriales muestra cómo tooupdate Hola modelo en el servicio web de predicción:</span><span class="sxs-lookup"><span data-stu-id="002dc-105">Once you have retrained hello model, hello following walkthroughs show how tooupdate hello model in your predictive web service:</span></span>

* <span data-ttu-id="002dc-106">Si implementa un servicio web de clásico en el portal de servicios Web de aprendizaje de máquina de hello, consulte [entrenar el modelo de servicio web clásico](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="002dc-106">If you deployed a Classic web service in hello Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="002dc-107">Si ha implementado un nuevo servicio web, consulte [volver a entrenar un nuevo servicio web mediante los cmdlets de administración de aprendizaje de máquina de hello](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="002dc-107">If you deployed a New web service, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="002dc-108">Para obtener información general de hello reciclaje de proceso, consulte [volver a entrenar un modelo de aprendizaje automático](machine-learning-retrain-machine-learning-model.md).</span><span class="sxs-lookup"><span data-stu-id="002dc-108">For an overview of hello retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="002dc-109">Si desea que toostart con el contenido existente nuevo administrador de recursos de Azure basada en servicio web, consulte [entrenar el modelo de un servicio web de predicción existente](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="002dc-109">If you want toostart with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="002dc-110">Crear un experimento de entrenamiento</span><span class="sxs-lookup"><span data-stu-id="002dc-110">Create a training experiment</span></span>
<span data-ttu-id="002dc-111">En este ejemplo, usará "ejemplo 5: entrenar, prueba, evaluar para clasificación binaria: conjunto de datos Adult" de ejemplos de aprendizaje automático de Microsoft Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="002dc-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from hello Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="002dc-112">experimento de Hola toocreate:</span><span class="sxs-lookup"><span data-stu-id="002dc-112">toocreate hello experiment:</span></span>

1. <span data-ttu-id="002dc-113">Inicie sesión en tooMicrosoft estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="002dc-113">Sign into tooMicrosoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="002dc-114">En hello esquina inferior derecha del panel de hello, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="002dc-114">On hello bottom right corner of hello dashboard, click **New**.</span></span>
3. <span data-ttu-id="002dc-115">En Microsoft Samples hello, seleccione 5 de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="002dc-115">From hello Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="002dc-116">experimento de hello toorename, en parte superior de hello del lienzo del experimento de hello, seleccione el nombre de experimento de Hola "ejemplo 5: entrenar, prueba, evaluar para clasificación binaria: conjunto de datos Adult".</span><span class="sxs-lookup"><span data-stu-id="002dc-116">toorename hello experiment, at hello top of hello experiment canvas, select hello experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="002dc-117">Escriba Census Model (Modelo de censo).</span><span class="sxs-lookup"><span data-stu-id="002dc-117">Type Census Model.</span></span>
6. <span data-ttu-id="002dc-118">En la parte inferior de hello del lienzo del experimento de hello, haga clic en **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="002dc-118">At hello bottom of hello experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="002dc-119">Haga clic en **Set Up Web Service** (Configurar servicio web) y seleccione **Retraining Web Service** (Servicio web de reentrenamiento).</span><span class="sxs-lookup"><span data-stu-id="002dc-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="002dc-120">siguiente Hello muestra experimento inicial Hola.</span><span class="sxs-lookup"><span data-stu-id="002dc-120">hello following shows hello initial experiment.</span></span>
   
   ![Experimento inicial.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="002dc-122">Creación de un experimento predictivo y publicación como servicio web</span><span class="sxs-lookup"><span data-stu-id="002dc-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="002dc-123">A continuación creará un experimento predicativo.</span><span class="sxs-lookup"><span data-stu-id="002dc-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="002dc-124">En la parte inferior de hello del lienzo del experimento de hello, haga clic en **configurar el servicio de Web** y seleccione **predictivo servicio Web**.</span><span class="sxs-lookup"><span data-stu-id="002dc-124">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="002dc-125">Esto ahorra modelo Hola como un modelo entrenado y agrega módulos de entrada y salida del servicio web.</span><span class="sxs-lookup"><span data-stu-id="002dc-125">This saves hello model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="002dc-126">Haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="002dc-126">Click **Run**.</span></span> 
3. <span data-ttu-id="002dc-127">Después de experimento Hola ha terminado de ejecutarse, haga clic en **implementar servicio Web [estándar]** o **implementar [New] servicio Web**.</span><span class="sxs-lookup"><span data-stu-id="002dc-127">After hello experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="002dc-128">toodeploy un nuevo servicio web debe tener permisos suficientes en hello suscripción toowhich que implementar el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="002dc-128">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="002dc-129">Para obtener más información, vea [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="002dc-129">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a><span data-ttu-id="002dc-130">Implementar Hola experimento de entrenamiento como un servicio web de aprendizaje</span><span class="sxs-lookup"><span data-stu-id="002dc-130">Deploy hello training experiment as a Training web service</span></span>
<span data-ttu-id="002dc-131">modelo de aprendizaje de hello tooretrain, debe implementar experimento de entrenamiento de Hola que creó como un servicio web de Retraining.</span><span class="sxs-lookup"><span data-stu-id="002dc-131">tooretrain hello trained model, you must deploy hello training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="002dc-132">Este servicio web necesita un *resultado del servicio Web* módulo conectado toohello  *[entrenar modelo] [ train-model]*  toobe tooproduce capaz de nuevo, el módulo modelos entrenados.</span><span class="sxs-lookup"><span data-stu-id="002dc-132">This web service needs a *Web Service Output* module connected toohello *[Train Model][train-model]* module, toobe able tooproduce new trained models.</span></span>

1. <span data-ttu-id="002dc-133">experimento de entrenamiento de tooreturn toohello, haga clic en el icono de experimentos hello en el panel izquierdo de hello, haga clic en el experimento Hola denominado modelo del censo.</span><span class="sxs-lookup"><span data-stu-id="002dc-133">tooreturn toohello training experiment, click hello Experiments icon in hello left pane, then click hello experiment named Census Model.</span></span>  
2. <span data-ttu-id="002dc-134">En el cuadro de búsqueda de elementos de experimento de búsqueda de hello, tipo de servicio web.</span><span class="sxs-lookup"><span data-stu-id="002dc-134">In hello Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="002dc-135">Arrastre un *proporcionados por el servicio Web* módulo en hello experimentar lienzo y conectar su salida toohello *limpiar datos que faltan* módulo.</span><span class="sxs-lookup"><span data-stu-id="002dc-135">Drag a *Web Service Input* module onto hello experiment canvas and connect its output toohello *Clean Missing Data* module.</span></span>  <span data-ttu-id="002dc-136">Esto garantiza que se procesan los datos reconversión Hola de igual manera que los datos de entrenamiento original.</span><span class="sxs-lookup"><span data-stu-id="002dc-136">This ensures that your retraining data is processed hello same way as your original training data.</span></span>
4. <span data-ttu-id="002dc-137">Arrastre dos *salida del servicio web* módulos en hello experimentar lienzo.</span><span class="sxs-lookup"><span data-stu-id="002dc-137">Drag two *web service Output* modules onto hello experiment canvas.</span></span> <span data-ttu-id="002dc-138">Conecte la salida de hello de hello *entrenar modelo* salida de hello y tooone del módulo de hello *evaluar modelo* módulo toohello otros.</span><span class="sxs-lookup"><span data-stu-id="002dc-138">Connect hello output of hello *Train Model* module tooone and hello output of hello *Evaluate Model* module toohello other.</span></span> <span data-ttu-id="002dc-139">Hola resultado del servicio web para **entrenar modelo** nos da entrenado nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="002dc-139">hello web service output for **Train Model** gives us hello new trained model.</span></span> <span data-ttu-id="002dc-140">Hola salida adjunta demasiado**evaluar modelo** devuelve ese módulo de salida de la, que es resultados de rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="002dc-140">hello output attached too**Evaluate Model** returns that module’s output, which is hello performance results.</span></span>
5. <span data-ttu-id="002dc-141">Haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="002dc-141">Click **Run**.</span></span> 

<span data-ttu-id="002dc-142">A continuación debe implementar Hola experimento de entrenamiento como un servicio web que genera un modelo entrenado y resultados de la evaluación de modelo.</span><span class="sxs-lookup"><span data-stu-id="002dc-142">Next you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="002dc-143">tooaccomplish esto, el siguiente conjunto de acciones dependen de si está trabajando con un servicio de web estándar o un servicio web nuevo.</span><span class="sxs-lookup"><span data-stu-id="002dc-143">tooaccomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="002dc-144">**Servicio web clásico**</span><span class="sxs-lookup"><span data-stu-id="002dc-144">**Classic web service**</span></span>

<span data-ttu-id="002dc-145">En la parte inferior de hello del lienzo del experimento de hello, haga clic en **configurar el servicio de Web** y seleccione **implementar servicio Web [estándar]**.</span><span class="sxs-lookup"><span data-stu-id="002dc-145">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="002dc-146">Servicio Web de Hola **panel** se muestra con la página de Ayuda de hello API hello y clave de API para la ejecución por lotes.</span><span class="sxs-lookup"><span data-stu-id="002dc-146">hello Web Service **Dashboard** is displayed with hello API Key and hello API help page for Batch Execution.</span></span> <span data-ttu-id="002dc-147">Hola solo método de ejecución por lotes puede usarse para crear modelos entrenados.</span><span class="sxs-lookup"><span data-stu-id="002dc-147">Only hello Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="002dc-148">**Servicio web nuevo**</span><span class="sxs-lookup"><span data-stu-id="002dc-148">**New web service**</span></span>

<span data-ttu-id="002dc-149">En la parte inferior de hello del lienzo del experimento de hello, haga clic en **configurar el servicio de Web** y seleccione **implementar [New] servicio Web**.</span><span class="sxs-lookup"><span data-stu-id="002dc-149">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="002dc-150">portal de servicios Web de aprendizaje de máquina de Azure de Web Service Hola abre toohello implementar página al servicio web.</span><span class="sxs-lookup"><span data-stu-id="002dc-150">hello Web Service Azure Machine Learning Web Services portal opens toohello Deploy web service page.</span></span> <span data-ttu-id="002dc-151">Escriba un nombre para el servicio web y elija un plan de pago y después haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="002dc-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="002dc-152">Hola solo método de ejecución por lotes puede utilizarse para crear modelos entrenados</span><span class="sxs-lookup"><span data-stu-id="002dc-152">Only hello Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="002dc-153">En cualquier caso, después de experimento tiene en ejecución completada, flujo de trabajo resultante Hola debe ser como sigue:</span><span class="sxs-lookup"><span data-stu-id="002dc-153">In either case, after experiment has completed running, hello resulting workflow should look as follows:</span></span>

![Flujo de trabajo resultante después de la ejecución.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a><span data-ttu-id="002dc-155">Volver a entrenar el modelo de Hola con datos nuevos mediante BES</span><span class="sxs-lookup"><span data-stu-id="002dc-155">Retrain hello model with new data using BES</span></span>
<span data-ttu-id="002dc-156">En este ejemplo, está usando C# toocreate Hola reciclaje de aplicación.</span><span class="sxs-lookup"><span data-stu-id="002dc-156">For this example, you are using C# toocreate hello retraining application.</span></span> <span data-ttu-id="002dc-157">También sirve Hola Python o R ejemplo código tooaccomplish esta tarea.</span><span class="sxs-lookup"><span data-stu-id="002dc-157">You can also use hello Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="002dc-158">toocall Hola API de reciclaje:</span><span class="sxs-lookup"><span data-stu-id="002dc-158">toocall hello Retraining APIs:</span></span>

1. <span data-ttu-id="002dc-159">Cree una nueva aplicación de consola de C# en Visual Studio: **Nuevo** > **Proyecto** > **Visual C#** > **Escritorio clásico de Windows** > **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="002dc-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="002dc-160">Inicie sesión en toohello portal de servicio Web de aprendizaje de máquina.</span><span class="sxs-lookup"><span data-stu-id="002dc-160">Sign in toohello Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="002dc-161">Si está trabajando con un servicio web clásico, haga clic en **Classic Web Services**(Servicios web clásicos).</span><span class="sxs-lookup"><span data-stu-id="002dc-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="002dc-162">Haga clic en servicio web de Hola que está trabajando.</span><span class="sxs-lookup"><span data-stu-id="002dc-162">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="002dc-163">Haga clic en el punto de conexión de hello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="002dc-163">Click hello default endpoint.</span></span>
   3. <span data-ttu-id="002dc-164">Haga clic en **Consume**(Consumo).</span><span class="sxs-lookup"><span data-stu-id="002dc-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="002dc-165">En parte inferior de Hola de hello **Consume** página Hola **código de ejemplo** sección, haga clic en **por lotes**.</span><span class="sxs-lookup"><span data-stu-id="002dc-165">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="002dc-166">Continuar toostep 5 de este procedimiento.</span><span class="sxs-lookup"><span data-stu-id="002dc-166">Continue toostep 5 of this procedure.</span></span>
4. <span data-ttu-id="002dc-167">Si está trabajando con un servicio web nuevo, haga clic en **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="002dc-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="002dc-168">Haga clic en servicio web de Hola que está trabajando.</span><span class="sxs-lookup"><span data-stu-id="002dc-168">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="002dc-169">Haga clic en **Consume**(Consumo).</span><span class="sxs-lookup"><span data-stu-id="002dc-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="002dc-170">En parte inferior de Hola de hello Consume la página hello **código de ejemplo** sección, haga clic en **por lotes**.</span><span class="sxs-lookup"><span data-stu-id="002dc-170">At hello bottom of hello Consume page, in hello **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="002dc-171">Copiar código C# ejemplo de Hola para la ejecución por lotes y péguelo en el archivo Program.cs de hello, asegurándose de que el espacio de nombres de hello permanece intacto.</span><span class="sxs-lookup"><span data-stu-id="002dc-171">Copy hello sample C# code for batch execution and paste it into hello Program.cs file, making sure hello namespace remains intact.</span></span>

<span data-ttu-id="002dc-172">Agregar paquete de Nuget hello Microsoft.AspNet.WebApi.Client tal como se especifica en los comentarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="002dc-172">Add hello Nuget package Microsoft.AspNet.WebApi.Client as specified in hello comments.</span></span> <span data-ttu-id="002dc-173">tooadd Hola referencia tooMicrosoft.WindowsAzure.Storage.dll, primero tendrá que biblioteca de cliente hello tooinstall para servicios de almacenamiento de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="002dc-173">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="002dc-174">Para obtener más información, vea [Servicios de almacenamiento de Windows](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="002dc-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="002dc-175">Actualizar la declaración de hello apikey</span><span class="sxs-lookup"><span data-stu-id="002dc-175">Update hello apikey declaration</span></span>
<span data-ttu-id="002dc-176">Busque hello **apikey** declaración.</span><span class="sxs-lookup"><span data-stu-id="002dc-176">Locate hello **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="002dc-177">Hola **información básica de consumo** sección de hello **Consume** página, busque la clave principal de Hola y cópielo toohello **apikey** declaración.</span><span class="sxs-lookup"><span data-stu-id="002dc-177">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="002dc-178">Actualizar la información de almacenamiento de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="002dc-178">Update hello Azure Storage information</span></span>
<span data-ttu-id="002dc-179">código de ejemplo BES Hola carga un archivo desde un almacenamiento de tooAzure de unidad local (por ejemplo "C:\temp\CensusIpnput.csv"), lo procesa y escribe Hola resultados atrás tooAzure almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="002dc-179">hello BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="002dc-180">tooaccomplish esta tarea, debe recuperar la información de nombre, la clave y el contenedor de la cuenta del almacenamiento hello para la cuenta de almacenamiento del portal de Azure clásico de Hola y actualización de hello correspondientes valores en el código de hello.</span><span class="sxs-lookup"><span data-stu-id="002dc-180">tooaccomplish this task, you must retrieve hello Storage account name, key, and container information for your Storage account from hello classic Azure portal and hello update corresponding values in hello code.</span></span> 

1. <span data-ttu-id="002dc-181">Inicie sesión en el portal de Azure clásico toohello.</span><span class="sxs-lookup"><span data-stu-id="002dc-181">Sign in toohello classic Azure portal.</span></span>
2. <span data-ttu-id="002dc-182">En la columna de navegación izquierdo de hello, haga clic en **almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="002dc-182">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="002dc-183">En lista de Hola de cuentas de almacenamiento, seleccione uno toostore Hola volver a entrenar modelo.</span><span class="sxs-lookup"><span data-stu-id="002dc-183">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="002dc-184">En la parte inferior de Hola de página de hello, haga clic en **administrar claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="002dc-184">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="002dc-185">Copie y guarde hello **clave de acceso principal** y cuadro de diálogo Cerrar Hola.</span><span class="sxs-lookup"><span data-stu-id="002dc-185">Copy and save hello **Primary Access Key** and close hello dialog.</span></span> 
6. <span data-ttu-id="002dc-186">En la parte superior de Hola de página de hello, haga clic en **contenedores**.</span><span class="sxs-lookup"><span data-stu-id="002dc-186">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="002dc-187">Seleccione un contenedor existente o cree uno nuevo y guarde el nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="002dc-187">Select an existing container or create a new one and save hello name.</span></span>

<span data-ttu-id="002dc-188">Busque hello *StorageAccountName*, *StorageAccountKey*, y *StorageContainerName* Hola a declaraciones y actualizar valores de hello que guardó en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="002dc-188">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update hello values you saved from hello Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="002dc-189">También debe asegurarse de archivo de entrada de hello está disponible en la ubicación de Hola que especifique en el código de hello.</span><span class="sxs-lookup"><span data-stu-id="002dc-189">You also must ensure hello input file is available at hello location you specify in hello code.</span></span> 

### <a name="specify-hello-output-location"></a><span data-ttu-id="002dc-190">Especifique la ubicación de salida de hello</span><span class="sxs-lookup"><span data-stu-id="002dc-190">Specify hello output location</span></span>
<span data-ttu-id="002dc-191">Al especificar la ubicación de salida de hello en hello la carga de solicitudes, Hola extensión del archivo de hello especificado en *RelativeLocation* debe especificarse como ilearner.</span><span class="sxs-lookup"><span data-stu-id="002dc-191">When specifying hello output location in hello Request Payload, hello extension of hello file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="002dc-192">Vea el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="002dc-192">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="002dc-193">nombres de Hola de sus ubicaciones de salida pueden ser diferentes de hello los en este tutorial basados en el orden de hello en el que se ha agregado módulos de salida de hello web service.</span><span class="sxs-lookup"><span data-stu-id="002dc-193">hello names of your output locations may be different from hello ones in this walkthrough based on hello order in which you added hello web service output modules.</span></span> <span data-ttu-id="002dc-194">Puesto que se configura este experimento de entrenamiento con dos salidas, resultados de hello incluyen información de ubicación de almacenamiento para ambos.</span><span class="sxs-lookup"><span data-stu-id="002dc-194">Since you set up this training experiment with two outputs, hello results include storage location information for both of them.</span></span>  
> 
> 

![Salida de reentrenamiento][6]

<span data-ttu-id="002dc-196">Diagrama 4: Salida de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="002dc-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="002dc-197">Evaluar los resultados de reciclaje de Hola</span><span class="sxs-lookup"><span data-stu-id="002dc-197">Evaluate hello Retraining Results</span></span>
<span data-ttu-id="002dc-198">Cuando se ejecuta la aplicación hello, salida de hello incluye la dirección URL de Hola y tooaccess necesarios de token de SAS Hola resultados de la evaluación.</span><span class="sxs-lookup"><span data-stu-id="002dc-198">When you run hello application, hello output includes hello URL and SAS token necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="002dc-199">Puede ver los resultados de rendimiento de Hola de hello volver a entrenar modelo mediante la combinación de hello *BaseLocation*, *RelativeLocation*, y *SasBlobToken* de hello unos resultados para *output2* (como se muestra en hello anterior reciclaje imagen de salida) y pegar la dirección URL completa de hello en la barra de direcciones del explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="002dc-199">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL in hello browser address bar.</span></span>  

<span data-ttu-id="002dc-200">Examine Hola resultados toodetermine si Hola recién entrenado realiza lo suficientemente bien hello tooreplace uno existente.</span><span class="sxs-lookup"><span data-stu-id="002dc-200">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="002dc-201">Hola copia *BaseLocation*, *RelativeLocation*, y *SasBlobToken* de resultados de la salida de hello, utilizará durante Hola reciclaje de proceso.</span><span class="sxs-lookup"><span data-stu-id="002dc-201">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results, you will use them during hello retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="002dc-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="002dc-202">Next steps</span></span>
<span data-ttu-id="002dc-203">Si ha implementado el servicio web de predicción de hello haciendo clic en **implementar servicio Web [estándar]**, consulte [entrenar el modelo de servicio web clásico](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="002dc-203">If you deployed hello predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="002dc-204">Si ha implementado el servicio web de predicción de hello haciendo clic en **implementar [New] servicio Web**, consulte [volver a entrenar un nuevo servicio web mediante los cmdlets de administración de aprendizaje de máquina de hello](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="002dc-204">If you deployed hello predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
