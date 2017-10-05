---
title: "Repetición del entrenamiento de los modelos de Machine Learning mediante programación | Microsoft Docs"
description: "Obtenga información acerca de cómo volver a entrenar un modelo y actualizar el servicio web mediante programación para utilizar el modelo recién entrenado en el Aprendizaje automático de Azure."
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
ms.openlocfilehash: cf7a39e14a935d0d0e0df07e66a8f37480ec9687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="e70c8-103">Volver a entrenar modelos de aprendizaje automático mediante programación</span><span class="sxs-lookup"><span data-stu-id="e70c8-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="e70c8-104">En este tutorial, aprenderá a entrenar mediante programación un servicio web Azure Machine Learning mediante C# y el servicio de ejecución por lotes de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e70c8-104">In this walkthrough, you will learn how to programmatically retrain an Azure Machine Learning Web Service using C# and the Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="e70c8-105">Cuando haya reentrenado el modelo, los tutoriales siguientes le mostrarán cómo actualizarlo en el servicio web predictivo:</span><span class="sxs-lookup"><span data-stu-id="e70c8-105">Once you have retrained the model, the following walkthroughs show how to update the model in your predictive web service:</span></span>

* <span data-ttu-id="e70c8-106">Si implementó un servicio web clásico en el portal Servicios web Machine Learning, consulte [Reentrenamiento de un servicio web clásico](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e70c8-106">If you deployed a Classic web service in the Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="e70c8-107">Si implementó un servicio web nuevo, consulte [Reentrenamiento de un servicio web nuevo mediante los cmdlets de administración de Machine Learning](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e70c8-107">If you deployed a New web service, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="e70c8-108">Para obtener información general sobre el proceso de reentrenamiento, consulte [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md) (Reentrenamiento de un modelo de Machine Learning).</span><span class="sxs-lookup"><span data-stu-id="e70c8-108">For an overview of the retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="e70c8-109">Si desea comenzar por el servicio web existente basado en el nuevo Azure Resource Manager, consulte [Retrain an existing Predictive Web service](machine-learning-retrain-existing-resource-manager-based-web-service.md) (Reentrenamiento de un servicio web predictivo existente).</span><span class="sxs-lookup"><span data-stu-id="e70c8-109">If you want to start with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="e70c8-110">Crear un experimento de entrenamiento</span><span class="sxs-lookup"><span data-stu-id="e70c8-110">Create a training experiment</span></span>
<span data-ttu-id="e70c8-111">En este ejemplo, usará "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" (Ejemplo 5: Entrenar, probar, evaluar para clasificación binaria: Conjunto de datos para adultos) de entre los ejemplos de Aprendizaje automático de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e70c8-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from the Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="e70c8-112">Para crear el experimento:</span><span class="sxs-lookup"><span data-stu-id="e70c8-112">To create the experiment:</span></span>

1. <span data-ttu-id="e70c8-113">Inicie sesión en Estudio de aprendizaje automático de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e70c8-113">Sign into to Microsoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="e70c8-114">En la esquina inferior derecha del panel, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="e70c8-114">On the bottom right corner of the dashboard, click **New**.</span></span>
3. <span data-ttu-id="e70c8-115">En los ejemplos de Microsoft, seleccione el ejemplo 5.</span><span class="sxs-lookup"><span data-stu-id="e70c8-115">From the Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="e70c8-116">Para cambiar el nombre del experimento, en la parte superior del lienzo del experimento, seleccione el nombre del experimento, en este caso "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span><span class="sxs-lookup"><span data-stu-id="e70c8-116">To rename the experiment, at the top of the experiment canvas, select the experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="e70c8-117">Escriba Census Model (Modelo de censo).</span><span class="sxs-lookup"><span data-stu-id="e70c8-117">Type Census Model.</span></span>
6. <span data-ttu-id="e70c8-118">En la parte inferior del lienzo del experimento, haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="e70c8-118">At the bottom of the experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="e70c8-119">Haga clic en **Set Up Web Service** (Configurar servicio web) y seleccione **Retraining Web Service** (Servicio web de reentrenamiento).</span><span class="sxs-lookup"><span data-stu-id="e70c8-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="e70c8-120">A continuación, se muestra el experimento inicial.</span><span class="sxs-lookup"><span data-stu-id="e70c8-120">The following shows the initial experiment.</span></span>
   
   ![Experimento inicial.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="e70c8-122">Creación de un experimento predictivo y publicación como servicio web</span><span class="sxs-lookup"><span data-stu-id="e70c8-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="e70c8-123">A continuación creará un experimento predicativo.</span><span class="sxs-lookup"><span data-stu-id="e70c8-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="e70c8-124">En la parte inferior del lienzo del experimento, haga clic en **Set Up Web Service** (Configurar servicio web) y seleccione **Predictive web Service** (Servicio web predictivo).</span><span class="sxs-lookup"><span data-stu-id="e70c8-124">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="e70c8-125">Esto permite guardar el modelo como un modelo entrenado y agrega los módulos de entrada y salida de servicio web.</span><span class="sxs-lookup"><span data-stu-id="e70c8-125">This saves the model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="e70c8-126">Haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="e70c8-126">Click **Run**.</span></span> 
3. <span data-ttu-id="e70c8-127">Cuando el experimento haya terminado de ejecutarse, haga clic en **Deploy Web Service [Classic]** (Implementar servicio web [clásico]) o en **Deploy Web Service [New]** (Implementar servicio web [nuevo]).</span><span class="sxs-lookup"><span data-stu-id="e70c8-127">After the experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="e70c8-128">Para implementar un nuevo servicio web, debe tener permisos suficientes en la suscripción en la que lo implementa.</span><span class="sxs-lookup"><span data-stu-id="e70c8-128">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="e70c8-129">Para obtener más información, consulte [Administración de un servicio web mediante el portal Servicios web Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="e70c8-129">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-the-training-experiment-as-a-training-web-service"></a><span data-ttu-id="e70c8-130">Implementación del experimento de entrenamiento como un servicio web de entrenamiento</span><span class="sxs-lookup"><span data-stu-id="e70c8-130">Deploy the training experiment as a Training web service</span></span>
<span data-ttu-id="e70c8-131">Para reciclar el modelo entrenado, debe implementar el experimento de entrenamiento que creó como un servicio web de reciclaje.</span><span class="sxs-lookup"><span data-stu-id="e70c8-131">To retrain the trained model, you must deploy the training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="e70c8-132">Este servicio necesita un módulo de *salida del servicio web* conectado al módulo *[Entrenar modelo][train-model]* para poder generar nuevos modelos entrenados.</span><span class="sxs-lookup"><span data-stu-id="e70c8-132">This web service needs a *Web Service Output* module connected to the *[Train Model][train-model]* module, to be able to produce new trained models.</span></span>

1. <span data-ttu-id="e70c8-133">Para volver al experimento de entrenamiento, haga clic en el icono Experimentos en el panel izquierdo, y luego haga clic en el experimento denominado Census Model (Modelo de censo).</span><span class="sxs-lookup"><span data-stu-id="e70c8-133">To return to the training experiment, click the Experiments icon in the left pane, then click the experiment named Census Model.</span></span>  
2. <span data-ttu-id="e70c8-134">En el cuadro de búsqueda Search Experiment Items (Buscar elementos de experimentos), escriba servicio web.</span><span class="sxs-lookup"><span data-stu-id="e70c8-134">In the Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="e70c8-135">Arrastre un módulo de *entrada de servicio web* al lienzo de experimentos y conecte la salida al módulo *Clean Missing Data* (Limpiar datos que faltan).</span><span class="sxs-lookup"><span data-stu-id="e70c8-135">Drag a *Web Service Input* module onto the experiment canvas and connect its output to the *Clean Missing Data* module.</span></span>  <span data-ttu-id="e70c8-136">Esto garantiza que los datos de reentrenamiento se procesen del mismo modo que los datos de entrenamiento originales.</span><span class="sxs-lookup"><span data-stu-id="e70c8-136">This ensures that your retraining data is processed the same way as your original training data.</span></span>
4. <span data-ttu-id="e70c8-137">Arrastre dos módulos de *salida de servicio web* al lienzo de experimentos.</span><span class="sxs-lookup"><span data-stu-id="e70c8-137">Drag two *web service Output* modules onto the experiment canvas.</span></span> <span data-ttu-id="e70c8-138">Conecte la salida del módulo *Entrenar modelo* a uno y la salida del módulo *Evaluate Model* (Evaluar modelo), al otro.</span><span class="sxs-lookup"><span data-stu-id="e70c8-138">Connect the output of the *Train Model* module to one and the output of the *Evaluate Model* module to the other.</span></span> <span data-ttu-id="e70c8-139">La salida del servicio web para **Entrenar modelo** nos ofrecerá el nuevo modelo entrenado.</span><span class="sxs-lookup"><span data-stu-id="e70c8-139">The web service output for **Train Model** gives us the new trained model.</span></span> <span data-ttu-id="e70c8-140">La salida conectada a **Evaluate Model** (Evaluar modelo) devuelve los resultados de ese módulo, que son los resultados de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="e70c8-140">The output attached to **Evaluate Model** returns that module’s output, which is the performance results.</span></span>
5. <span data-ttu-id="e70c8-141">Haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="e70c8-141">Click **Run**.</span></span> 

<span data-ttu-id="e70c8-142">Después, debe implementar el experimento de entrenamiento como un servicio web que genera un modelo entrenado y resultados de evaluación del modelo.</span><span class="sxs-lookup"><span data-stu-id="e70c8-142">Next you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="e70c8-143">Para lograr esto, el siguiente conjunto de acciones depende de si está trabajando con un servicio web clásico o un servicio web nuevo.</span><span class="sxs-lookup"><span data-stu-id="e70c8-143">To accomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="e70c8-144">**Servicio web clásico**</span><span class="sxs-lookup"><span data-stu-id="e70c8-144">**Classic web service**</span></span>

<span data-ttu-id="e70c8-145">En la parte inferior del lienzo del experimento, haga clic en **Set Up Web Service** (Configurar servicio web) y seleccione **Deploy Web Service [Classic]** (Implementar servicio web [clásico]).</span><span class="sxs-lookup"><span data-stu-id="e70c8-145">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="e70c8-146">Aparecerá el **panel** del servicio web con la clave de API y la página de Ayuda de API para la ejecución por lotes.</span><span class="sxs-lookup"><span data-stu-id="e70c8-146">The Web Service **Dashboard** is displayed with the API Key and the API help page for Batch Execution.</span></span> <span data-ttu-id="e70c8-147">Solo se puede usar el método de ejecución por lotes para crear modelos entrenados.</span><span class="sxs-lookup"><span data-stu-id="e70c8-147">Only the Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="e70c8-148">**Servicio web nuevo**</span><span class="sxs-lookup"><span data-stu-id="e70c8-148">**New web service**</span></span>

<span data-ttu-id="e70c8-149">En la parte inferior del lienzo del experimento, haga clic en **Set Up Web Service** (Configurar servicio web) y seleccione **Deploy Web Service [New]** (Implementar servicio web [nuevo]).</span><span class="sxs-lookup"><span data-stu-id="e70c8-149">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="e70c8-150">El portal de servicios web de Azure Machine Learning se abre en la página Deploy Web service (Implementar servicio web).</span><span class="sxs-lookup"><span data-stu-id="e70c8-150">The Web Service Azure Machine Learning Web Services portal opens to the Deploy web service page.</span></span> <span data-ttu-id="e70c8-151">Escriba un nombre para el servicio web y elija un plan de pago y después haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="e70c8-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="e70c8-152">Solo se puede usar el método de ejecución de lotes para crear modelos entrenados.</span><span class="sxs-lookup"><span data-stu-id="e70c8-152">Only the Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="e70c8-153">En cualquier caso, una vez que el experimento ha finalizado su ejecución, el flujo de trabajo resultante debe ser el siguiente:</span><span class="sxs-lookup"><span data-stu-id="e70c8-153">In either case, after experiment has completed running, the resulting workflow should look as follows:</span></span>

![Flujo de trabajo resultante después de la ejecución.][4]



## <a name="retrain-the-model-with-new-data-using-bes"></a><span data-ttu-id="e70c8-155">Reentrenamiento del modelo con nuevos datos mediante BES</span><span class="sxs-lookup"><span data-stu-id="e70c8-155">Retrain the model with new data using BES</span></span>
<span data-ttu-id="e70c8-156">En este ejemplo, se utiliza C# para crear la aplicación de reentrenamiento.</span><span class="sxs-lookup"><span data-stu-id="e70c8-156">For this example, you are using C# to create the retraining application.</span></span> <span data-ttu-id="e70c8-157">También puede utilizar el código de ejemplo de Python o R para realizar esta tarea.</span><span class="sxs-lookup"><span data-stu-id="e70c8-157">You can also use the Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="e70c8-158">Para llamar a las API de reentrenamiento:</span><span class="sxs-lookup"><span data-stu-id="e70c8-158">To call the Retraining APIs:</span></span>

1. <span data-ttu-id="e70c8-159">Cree una nueva aplicación de consola de C# en Visual Studio: **Nuevo** > **Proyecto** > **Visual C#** > **Escritorio clásico de Windows** > **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="e70c8-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="e70c8-160">Inicie sesión en el portal de servicio web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e70c8-160">Sign in to the Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="e70c8-161">Si está trabajando con un servicio web clásico, haga clic en **Classic Web Services**(Servicios web clásicos).</span><span class="sxs-lookup"><span data-stu-id="e70c8-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="e70c8-162">Haga clic en el servicio web con el que está trabajando.</span><span class="sxs-lookup"><span data-stu-id="e70c8-162">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="e70c8-163">Haga clic en el punto de conexión predeterminado.</span><span class="sxs-lookup"><span data-stu-id="e70c8-163">Click the default endpoint.</span></span>
   3. <span data-ttu-id="e70c8-164">Haga clic en **Consume**(Consumo).</span><span class="sxs-lookup"><span data-stu-id="e70c8-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="e70c8-165">En la parte inferior de la página **Consume** (Consumo), en la sección **Código de ejemplo**, haga clic en **Batch**.</span><span class="sxs-lookup"><span data-stu-id="e70c8-165">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="e70c8-166">Vaya al paso 5 de este procedimiento.</span><span class="sxs-lookup"><span data-stu-id="e70c8-166">Continue to step 5 of this procedure.</span></span>
4. <span data-ttu-id="e70c8-167">Si está trabajando con un servicio web nuevo, haga clic en **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="e70c8-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="e70c8-168">Haga clic en el servicio web con el que está trabajando.</span><span class="sxs-lookup"><span data-stu-id="e70c8-168">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="e70c8-169">Haga clic en **Consume**(Consumo).</span><span class="sxs-lookup"><span data-stu-id="e70c8-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="e70c8-170">En la parte inferior de la página Consume (Consumo), en la sección **Código de ejemplo**, haga clic en **Batch**.</span><span class="sxs-lookup"><span data-stu-id="e70c8-170">At the bottom of the Consume page, in the **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="e70c8-171">Copie el código C# de ejemplo para la ejecución por lotes y péguelo en el archivo Program.cs, asegurándose de que el espacio de nombres permanece intacto.</span><span class="sxs-lookup"><span data-stu-id="e70c8-171">Copy the sample C# code for batch execution and paste it into the Program.cs file, making sure the namespace remains intact.</span></span>

<span data-ttu-id="e70c8-172">Agregue el paquete NuGet Microsoft.AspNet.WebApi.Client tal como se especifica en los comentarios.</span><span class="sxs-lookup"><span data-stu-id="e70c8-172">Add the Nuget package Microsoft.AspNet.WebApi.Client as specified in the comments.</span></span> <span data-ttu-id="e70c8-173">Para agregar la referencia a Microsoft.WindowsAzure.Storage.dll, primero debe instalar la biblioteca de cliente para servicios de Microsoft Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e70c8-173">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="e70c8-174">Para obtener más información, vea [Servicios de almacenamiento de Windows](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="e70c8-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="e70c8-175">Actualización de la declaración de apikey</span><span class="sxs-lookup"><span data-stu-id="e70c8-175">Update the apikey declaration</span></span>
<span data-ttu-id="e70c8-176">Localice la declaración de **apikey** .</span><span class="sxs-lookup"><span data-stu-id="e70c8-176">Locate the **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="e70c8-177">En la sección **Basic consumption info** (Información básica sobre consumo) de la página **Consume** (Consumo), localice la clave principal y cópiela en la declaración de **apikey**.</span><span class="sxs-lookup"><span data-stu-id="e70c8-177">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="e70c8-178">Actualización de la información de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="e70c8-178">Update the Azure Storage information</span></span>
<span data-ttu-id="e70c8-179">El código de ejemplo de BES carga un archivo desde una unidad local (por ejemplo "C:\temp\CensusIpnput.csv") en el Almacenamiento de Azure, lo procesa y escribe los resultados de nuevo en el Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e70c8-179">The BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="e70c8-180">Para ello, debe recuperar el nombre, la clave y la información de contenedor de la cuenta de almacenamiento desde el Portal de Azure clásico y actualizar los valores correspondientes del código.</span><span class="sxs-lookup"><span data-stu-id="e70c8-180">To accomplish this task, you must retrieve the Storage account name, key, and container information for your Storage account from the classic Azure portal and the update corresponding values in the code.</span></span> 

1. <span data-ttu-id="e70c8-181">Inicie sesión en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="e70c8-181">Sign in to the classic Azure portal.</span></span>
2. <span data-ttu-id="e70c8-182">En la columna de navegación izquierda, haga clic en **Almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="e70c8-182">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="e70c8-183">En la lista de cuentas de almacenamiento, seleccione una para almacenar el modelo reciclado.</span><span class="sxs-lookup"><span data-stu-id="e70c8-183">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="e70c8-184">En la parte inferior de la página, haga clic en **Administrar claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="e70c8-184">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="e70c8-185">Copie y guarde la **clave de acceso principal** y cierre el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e70c8-185">Copy and save the **Primary Access Key** and close the dialog.</span></span> 
6. <span data-ttu-id="e70c8-186">En la parte superior de la página, haga clic en **Contenedores**.</span><span class="sxs-lookup"><span data-stu-id="e70c8-186">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="e70c8-187">Seleccione un contenedor existente o cree uno nuevo y guarde el nombre.</span><span class="sxs-lookup"><span data-stu-id="e70c8-187">Select an existing container or create a new one and save the name.</span></span>

<span data-ttu-id="e70c8-188">Busque las declaraciones *StorageAccountName*, *StorageAccountKey* y *StorageContainerName* y actualice los valores guardados en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e70c8-188">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update the values you saved from the Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="e70c8-189">También deberá asegurarse de que el archivo de entrada está disponible en la ubicación que especifique en el código.</span><span class="sxs-lookup"><span data-stu-id="e70c8-189">You also must ensure the input file is available at the location you specify in the code.</span></span> 

### <a name="specify-the-output-location"></a><span data-ttu-id="e70c8-190">Especifique la ubicación de salida.</span><span class="sxs-lookup"><span data-stu-id="e70c8-190">Specify the output location</span></span>
<span data-ttu-id="e70c8-191">Al especificar la ubicación de salida en la carga útil de solicitud, la extensión del archivo especificado en *RelativeLocation* debe especificarse como ilearner.</span><span class="sxs-lookup"><span data-stu-id="e70c8-191">When specifying the output location in the Request Payload, the extension of the file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="e70c8-192">Consulte el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e70c8-192">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you would like to use for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="e70c8-193">Los nombres de las ubicaciones de salida pueden ser diferentes de aquellos que aparecen en este tutorial que se basa en el orden en que se agregaron los módulos de salida del servicio web.</span><span class="sxs-lookup"><span data-stu-id="e70c8-193">The names of your output locations may be different from the ones in this walkthrough based on the order in which you added the web service output modules.</span></span> <span data-ttu-id="e70c8-194">Puesto que ha configurado este experimento de entrenamiento con dos salidas, los resultados incluyen información de ubicación de almacenamiento para ambas.</span><span class="sxs-lookup"><span data-stu-id="e70c8-194">Since you set up this training experiment with two outputs, the results include storage location information for both of them.</span></span>  
> 
> 

![Salida de reentrenamiento][6]

<span data-ttu-id="e70c8-196">Diagrama 4: Salida de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="e70c8-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="e70c8-197">Evaluación de los resultados de reentrenamiento</span><span class="sxs-lookup"><span data-stu-id="e70c8-197">Evaluate the Retraining Results</span></span>
<span data-ttu-id="e70c8-198">Al ejecutar la aplicación, la salida incluye la dirección URL y el token SAS necesarios para tener acceso a los resultados de evaluación.</span><span class="sxs-lookup"><span data-stu-id="e70c8-198">When you run the application, the output includes the URL and SAS token necessary to access the evaluation results.</span></span>

<span data-ttu-id="e70c8-199">Podrá ver los resultados de rendimiento del modelo reentrenado combinando *BaseLocation*, *RelativeLocation* y *SasBlobToken* de los resultados de salida de *output2* (como se muestra en la imagen de la salida de reentrenamiento anterior) y copiando y pegando la dirección URL completa en la barra de direcciones del explorador.</span><span class="sxs-lookup"><span data-stu-id="e70c8-199">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL in the browser address bar.</span></span>  

<span data-ttu-id="e70c8-200">Revise los resultados para determinar si el modelo recientemente entrenado funciona lo suficientemente bien como para reemplazar el existente.</span><span class="sxs-lookup"><span data-stu-id="e70c8-200">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="e70c8-201">Copie *BaseLocation*, *RelativeLocation* y *SasBlobToken* de los resultados de salida, ya que se usarán durante el proceso de reentrenamiento.</span><span class="sxs-lookup"><span data-stu-id="e70c8-201">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results, you will use them during the retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e70c8-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e70c8-202">Next steps</span></span>
<span data-ttu-id="e70c8-203">Si implementa el servicio web predictivo haciendo clic en **Deploy Web Service [Classic]** (Implementar servicio web [clásico]), consulte [Reentrenamiento de un servicio web clásico](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e70c8-203">If you deployed the predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="e70c8-204">Si implementó el servicio web predictivo haciendo clic en **Deploy Web Service [Classic]** (Implementar servicio web [clásico]), consulte [Reentrenamiento de un servicio web nuevo mediante los cmdlets de administración de Machine Learning](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e70c8-204">If you deployed the predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using the Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
