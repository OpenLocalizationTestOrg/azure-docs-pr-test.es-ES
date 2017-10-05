---
title: Reciclaje de un servicio web predictivo existente | Microsoft Docs
description: "Obtenga información sobre cómo reciclar un modelo y actualizar el servicio web para utilizar el modelo recién entrenado en Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: bdc994daf441d397157f8e6cbcf84d72584927f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="30a93-103">Reciclaje de un servicio web predictivo existente</span><span class="sxs-lookup"><span data-stu-id="30a93-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="30a93-104">En este documento se describe el proceso de reciclaje para el escenario siguiente:</span><span class="sxs-lookup"><span data-stu-id="30a93-104">This document describes the retraining process for the following scenario:</span></span>

* <span data-ttu-id="30a93-105">Dispone de un experimento de entrenamiento y un experimento predictivo que se ha implementado como un servicio web de operaciones.</span><span class="sxs-lookup"><span data-stu-id="30a93-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="30a93-106">Tiene nuevos datos que desea que el servicio web predictivo utilice para realizar su puntuación.</span><span class="sxs-lookup"><span data-stu-id="30a93-106">You have new data that you want your predictive web service to use to perform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="30a93-107">Para implementar un nuevo servicio web, debe tener permisos suficientes en la suscripción en la que lo implementa.</span><span class="sxs-lookup"><span data-stu-id="30a93-107">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="30a93-108">Para obtener más información, consulte [Administración de un servicio web mediante el portal Servicios web Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="30a93-108">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="30a93-109">A partir de su servicio web existente y los experimentos, debe seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="30a93-109">Starting with your existing web service and experiments, you need to follow these steps:</span></span>

1. <span data-ttu-id="30a93-110">Actualizar el modelo.</span><span class="sxs-lookup"><span data-stu-id="30a93-110">Update the model.</span></span>
   1. <span data-ttu-id="30a93-111">Modificar el experimento de entrenamiento para permitir salidas y entradas del servicio web.</span><span class="sxs-lookup"><span data-stu-id="30a93-111">Modify your training experiment to allow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="30a93-112">Implementar el experimento de entrenamiento como un servicio web de reciclaje.</span><span class="sxs-lookup"><span data-stu-id="30a93-112">Deploy the training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="30a93-113">Utilizar el servicio de ejecución por lotes (BES) del experimento de entrenamiento para reciclar el modelo.</span><span class="sxs-lookup"><span data-stu-id="30a93-113">Use the training experiment's Batch Execution Service (BES) to retrain the model.</span></span>
2. <span data-ttu-id="30a93-114">Usar los cmdlets de PowerShell de Azure Machine Learning para actualizar el experimento predictivo.</span><span class="sxs-lookup"><span data-stu-id="30a93-114">Use the Azure Machine Learning PowerShell cmdlets to update the predictive experiment.</span></span>
   1. <span data-ttu-id="30a93-115">Inicie sesión en la cuenta de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="30a93-115">Sign in to your Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="30a93-116">Obtenga la definición de servicio web.</span><span class="sxs-lookup"><span data-stu-id="30a93-116">Get the web service definition.</span></span>
   3. <span data-ttu-id="30a93-117">Exporte la definición de servicio web como JSON.</span><span class="sxs-lookup"><span data-stu-id="30a93-117">Export the web service definition as JSON.</span></span>
   4. <span data-ttu-id="30a93-118">Actualice la referencia al blob ilearner en JSON</span><span class="sxs-lookup"><span data-stu-id="30a93-118">Update the reference to the ilearner blob in the JSON.</span></span>
   5. <span data-ttu-id="30a93-119">Importe JSON en una definición de servicio web.</span><span class="sxs-lookup"><span data-stu-id="30a93-119">Import the JSON into a web service definition.</span></span>
   6. <span data-ttu-id="30a93-120">Actualice el servicio web con la nueva definición de servicio web.</span><span class="sxs-lookup"><span data-stu-id="30a93-120">Update the web service with a new web service definition.</span></span>

## <a name="deploy-the-training-experiment"></a><span data-ttu-id="30a93-121">Implementación del experimento de entrenamiento</span><span class="sxs-lookup"><span data-stu-id="30a93-121">Deploy the training experiment</span></span>
<span data-ttu-id="30a93-122">Para implementar el experimento de entrenamiento como servicio web de reciclaje, debe agregar entradas y salidas de servicio web al modelo.</span><span class="sxs-lookup"><span data-stu-id="30a93-122">To deploy the training experiment as a retraining web service, you must add web service inputs and outputs to the model.</span></span> <span data-ttu-id="30a93-123">Si conecta un módulo de *Salida de servicio web* en el módulo del *[modelo de entrenamiento][train-model]*, puede activar el experimento de entrenamiento para producir un nuevo modelo de entrenamiento o que puede usar en el experimento predictivo.</span><span class="sxs-lookup"><span data-stu-id="30a93-123">By connecting a *Web Service Output* module to the experiment's *[Train Model][train-model]* module, you enable the training experiment to produce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="30a93-124">Si tiene un módulo *Evaluar modelo*, puede adjuntar un resultado del servicio web para obtener los resultados de evaluación como salida.</span><span class="sxs-lookup"><span data-stu-id="30a93-124">If you have an *Evaluate Model* module, you can also attach web service output to get the evaluation results as output.</span></span>

<span data-ttu-id="30a93-125">Para actualizar el experimento de entrenamiento:</span><span class="sxs-lookup"><span data-stu-id="30a93-125">To update your training experiment:</span></span>

1. <span data-ttu-id="30a93-126">Conecte un módulo *Entrada de servicio web* en la entrada de datos (por ejemplo, un módulo *Limpiar datos que faltan*).</span><span class="sxs-lookup"><span data-stu-id="30a93-126">Connect a *Web Service Input* module to your data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="30a93-127">Normalmente, quiere asegurarse de que los datos de entrada se procesen de la misma forma que los datos de entrenamiento original.</span><span class="sxs-lookup"><span data-stu-id="30a93-127">Typically, you want to ensure that your input data is processed in the same way as your original training data.</span></span>
2. <span data-ttu-id="30a93-128">Conecte un módulo *Salida de servicio web* a la salida del módulo *Modelo de entrenamiento*.</span><span class="sxs-lookup"><span data-stu-id="30a93-128">Connect a *Web Service Output* module to the output of your *Train Model* module.</span></span>
3. <span data-ttu-id="30a93-129">Si tiene un módulo *Evaluar modelo* y desea los resultados de la evaluación, conecte n módulo *Salida del servicio web* a la salida de su módulo *Evaluar modelo*.</span><span class="sxs-lookup"><span data-stu-id="30a93-129">If you have an *Evaluate Model* module and you want to output the evaluation results, connect a *Web Service Output* module to the output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="30a93-130">Ejecute el experimento.</span><span class="sxs-lookup"><span data-stu-id="30a93-130">Run your experiment.</span></span>

<span data-ttu-id="30a93-131">Después, debe implementar el experimento de entrenamiento como un servicio web que genera un modelo entrenado y resultados de evaluación del modelo.</span><span class="sxs-lookup"><span data-stu-id="30a93-131">Next, you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="30a93-132">En la parte inferior del lienzo del experimento, haga clic en **Set Up Web Service** (Configurar servicio web) y después seleccione **Deploy Web Service [New]** (Implementar servicio web [nuevo]).</span><span class="sxs-lookup"><span data-stu-id="30a93-132">At the bottom of the experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="30a93-133">El portal de servicios web de Azure Machine Learning se abre en la página **Deploy Web service** (Implementar servicio web).</span><span class="sxs-lookup"><span data-stu-id="30a93-133">The Azure Machine Learning Web Services portal opens to the **Deploy Web Service** page.</span></span> <span data-ttu-id="30a93-134">Escriba un nombre para el servicio web y elija un plan de pago y después haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="30a93-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="30a93-135">Solo puede usar el método Ejecución de lotes para crear modelos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="30a93-135">You can only use the Batch Execution method for creating trained models.</span></span>

## <a name="retrain-the-model-with-new-data-by-using-bes"></a><span data-ttu-id="30a93-136">Reciclaje del modelo con nuevos datos mediante BES</span><span class="sxs-lookup"><span data-stu-id="30a93-136">Retrain the model with new data by using BES</span></span>
<span data-ttu-id="30a93-137">En este ejemplo, se utiliza C# para crear la aplicación de reciclado.</span><span class="sxs-lookup"><span data-stu-id="30a93-137">For this example, we're using C# to create the retraining application.</span></span> <span data-ttu-id="30a93-138">También puede utilizar el código de ejemplo de Python o R para realizar esta tarea.</span><span class="sxs-lookup"><span data-stu-id="30a93-138">You can also use Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="30a93-139">Para llamar a las API de reciclado:</span><span class="sxs-lookup"><span data-stu-id="30a93-139">To call the retraining APIs:</span></span>

1. <span data-ttu-id="30a93-140">Cree una nueva aplicación de consola de C# en Visual Studio: **Nuevo** > **Proyecto** > **Visual C#** > **Escritorio clásico de Windows** > **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="30a93-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="30a93-141">Inicie sesión en el portal de servicio web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="30a93-141">Sign in to the Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="30a93-142">Haga clic en el servicio web con el que está trabajando.</span><span class="sxs-lookup"><span data-stu-id="30a93-142">Click the web service that you're working with.</span></span>
4. <span data-ttu-id="30a93-143">Haga clic en **Consume**(Consumo).</span><span class="sxs-lookup"><span data-stu-id="30a93-143">Click **Consume**.</span></span>
5. <span data-ttu-id="30a93-144">En la parte inferior de la página **Consume** (Consumo), en la sección **Código de ejemplo**, haga clic en **Batch**.</span><span class="sxs-lookup"><span data-stu-id="30a93-144">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="30a93-145">Copie el código C# de ejemplo para la ejecución por lotes y péguelo en el archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="30a93-145">Copy the sample C# code for batch execution and paste it into the Program.cs file.</span></span> <span data-ttu-id="30a93-146">Asegúrese de que el espacio de nombres permanece intacto.</span><span class="sxs-lookup"><span data-stu-id="30a93-146">Make sure that the namespace remains intact.</span></span>

<span data-ttu-id="30a93-147">Agregue el paquete NuGet Microsoft.AspNet.WebApi.Client tal como se especifica en los comentarios.</span><span class="sxs-lookup"><span data-stu-id="30a93-147">Add the NuGet package Microsoft.AspNet.WebApi.Client, as specified in the comments.</span></span> <span data-ttu-id="30a93-148">Para agregar la referencia a Microsoft.WindowsAzure.Storage.dll, primero debe instalar la [biblioteca de cliente para servicios de Azure Storage](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="30a93-148">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="30a93-149">La siguiente captura de pantalla muestra la página **Consumo** en el portal de servicios de web de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="30a93-149">The following screenshot shows the **Consume** page in the Azure Machine Learning Web Services portal.</span></span>

![Página Consumo][1]

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="30a93-151">Actualización de la declaración de apikey</span><span class="sxs-lookup"><span data-stu-id="30a93-151">Update the apikey declaration</span></span>
<span data-ttu-id="30a93-152">Localice la declaración de **apikey**:</span><span class="sxs-lookup"><span data-stu-id="30a93-152">Locate the **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="30a93-153">En la sección **Basic consumption info** (Información básica sobre consumo) de la página **Consume** (Consumo), localice la clave principal y cópiela en la declaración de **apikey**.</span><span class="sxs-lookup"><span data-stu-id="30a93-153">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="30a93-154">Actualización de la información de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="30a93-154">Update the Azure Storage information</span></span>
<span data-ttu-id="30a93-155">El código de ejemplo de BES carga un archivo desde una unidad local (por ejemplo, "C:\temp\CensusIpnput.csv") en Azure Storage, lo procesa y escribe los resultados de nuevo en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="30a93-155">The BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="30a93-156">Para actualizar la información de Azure Storage, debe recuperar el nombre de la cuenta de almacenamiento, la clave y la información del contenedor para la cuenta de almacenamiento desde el Portal de Azure clásico y, a continuación, actualice el correspondiente después de ejecutar el experimento. El flujo de trabajo resultante debe ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="30a93-156">To update the Azure Storage information, you must retrieve the storage account name, key, and container information for your storage account from the Azure classic portal, and then update the correspondi After running your experiment, the resulting workflow should be similar to the following:</span></span>

![Flujo de trabajo resultante después de la ejecución][4]<span data-ttu-id="30a93-158">de valores ng en el código.</span><span class="sxs-lookup"><span data-stu-id="30a93-158">ng values in the code.</span></span>

1. <span data-ttu-id="30a93-159">Inicie sesión en el portal clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="30a93-159">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="30a93-160">En la columna de navegación izquierda, haga clic en **Almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="30a93-160">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="30a93-161">En la lista de cuentas de almacenamiento, seleccione una para almacenar el modelo reciclado.</span><span class="sxs-lookup"><span data-stu-id="30a93-161">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="30a93-162">En la parte inferior de la página, haga clic en **Administrar claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="30a93-162">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="30a93-163">Copie y guarde la **clave de acceso principal** y cierre el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="30a93-163">Copy and save the **Primary Access Key** and close the dialog.</span></span>
6. <span data-ttu-id="30a93-164">En la parte superior de la página, haga clic en **Contenedores**.</span><span class="sxs-lookup"><span data-stu-id="30a93-164">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="30a93-165">Seleccione un contenedor existente o cree uno nuevo y guarde el nombre.</span><span class="sxs-lookup"><span data-stu-id="30a93-165">Select an existing container, or create a new one and save the name.</span></span>

<span data-ttu-id="30a93-166">Busque las declaraciones *StorageAccountName*, *StorageAccountKey* y *StorageContainerName* y actualice los valores guardados en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="30a93-166">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update the values that you saved from the classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="30a93-167">También deberá asegurarse de que el archivo de entrada está disponible en la ubicación que especifique en el código.</span><span class="sxs-lookup"><span data-stu-id="30a93-167">You also must ensure that the input file is available at the location that you specify in the code.</span></span>

### <a name="specify-the-output-location"></a><span data-ttu-id="30a93-168">Especifique la ubicación de salida.</span><span class="sxs-lookup"><span data-stu-id="30a93-168">Specify the output location</span></span>
<span data-ttu-id="30a93-169">Al especificar la ubicación de salida en la carga útil de solicitud, la extensión del archivo especificado en *RelativeLocation* debe especificarse como `ilearner`.</span><span class="sxs-lookup"><span data-stu-id="30a93-169">When you specify the output location in the Request Payload, the extension of the file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="30a93-170">Consulte el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="30a93-170">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you want to use for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="30a93-171">El siguiente es un ejemplo de resultado de reciclaje: ![Reciclaje de salida][6]</span><span class="sxs-lookup"><span data-stu-id="30a93-171">The following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="30a93-172">Evaluación de los resultados de reciclaje</span><span class="sxs-lookup"><span data-stu-id="30a93-172">Evaluate the retraining results</span></span>
<span data-ttu-id="30a93-173">Al ejecutar la aplicación, la salida incluye la dirección URL y el token de firmas de acceso compartido que son necesarios para tener acceso a los resultados de evaluación.</span><span class="sxs-lookup"><span data-stu-id="30a93-173">When you run the application, the output includes the URL and shared access signatures token that are necessary to access the evaluation results.</span></span>

<span data-ttu-id="30a93-174">Podrá ver los resultados de rendimiento del modelo reciclado combinando *BaseLocation*, *RelativeLocation* y *SasBlobToken* de los resultados de salida de *output2* (como se muestra en la imagen de la salida de reciclado anterior) y copiando y pegando la dirección URL completa en la barra de direcciones del explorador.</span><span class="sxs-lookup"><span data-stu-id="30a93-174">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL into the browser address bar.</span></span>  

<span data-ttu-id="30a93-175">Revise los resultados para determinar si el modelo recientemente entrenado funciona lo suficientemente bien como para reemplazar el existente.</span><span class="sxs-lookup"><span data-stu-id="30a93-175">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="30a93-176">Copie *BaseLocation*, *RelativeLocation* y *SasBlobToken* de los resultados de salida.</span><span class="sxs-lookup"><span data-stu-id="30a93-176">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results.</span></span>

## <a name="retrain-the-web-service"></a><span data-ttu-id="30a93-177">Reciclar el servicio web</span><span class="sxs-lookup"><span data-stu-id="30a93-177">Retrain the web service</span></span>
<span data-ttu-id="30a93-178">Al reciclar un servicio web nuevo, actualice la definición del servicio web predictiva para hacer referencia al nuevo modelo entrenado.</span><span class="sxs-lookup"><span data-stu-id="30a93-178">When you retrain a new web service, you update the predictive web service definition to reference the new trained model.</span></span> <span data-ttu-id="30a93-179">La definición de servicio web es una representación interna del modelo entrenado del servicio web y no es modificable directamente.</span><span class="sxs-lookup"><span data-stu-id="30a93-179">The web service definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="30a93-180">Asegúrese de que va a recuperar la definición de servicio web para el experimento predictivo y no para el experimento de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="30a93-180">Make sure that you are retrieving the web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-to-azure-resource-manager"></a><span data-ttu-id="30a93-181">Iniciar sesión en Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="30a93-181">Sign in to Azure Resource Manager</span></span>
<span data-ttu-id="30a93-182">Primero debe iniciar sesión en la cuenta de Azure en el entorno de PowerShell mediante el cmdlet [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) .</span><span class="sxs-lookup"><span data-stu-id="30a93-182">You must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-the-web-service-definition-object"></a><span data-ttu-id="30a93-183">Obtener el objeto de definición del servicio web</span><span class="sxs-lookup"><span data-stu-id="30a93-183">Get the Web Service Definition object</span></span>
<span data-ttu-id="30a93-184">A continuación, obtenga el objeto de definición de servicio web, llamando al cmdlet [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx).</span><span class="sxs-lookup"><span data-stu-id="30a93-184">Next, get the Web Service Definition object by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="30a93-185">Para determinar el nombre del grupo de recursos de un servicio web existente, ejecute el cmdlet Get-AzureRmMlWebService sin ningún parámetro para mostrar los servicios web en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="30a93-185">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="30a93-186">Busque el servicio web y luego examine su identificador de servicio web.</span><span class="sxs-lookup"><span data-stu-id="30a93-186">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="30a93-187">El nombre del grupo de recursos es el cuarto elemento del identificador, justo después del elemento *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="30a93-187">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="30a93-188">En el ejemplo siguiente, el nombre del grupo de recursos es Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="30a93-188">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="30a93-189">Como alternativa, para determinar el nombre del grupo de recursos de un servicio web existente, inicie sesión en el portal de servicios web de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="30a93-189">Alternatively, to determine the resource group name of an existing web service, sign in to the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="30a93-190">Seleccione el servicio web.</span><span class="sxs-lookup"><span data-stu-id="30a93-190">Select the web service.</span></span> <span data-ttu-id="30a93-191">El nombre del grupo de recursos es el quinto elemento de la dirección URL del servicio web, justo después del elemento *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="30a93-191">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="30a93-192">En el ejemplo siguiente, el nombre del grupo de recursos es Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="30a93-192">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-object-as-json"></a><span data-ttu-id="30a93-193">Exportar el objeto de definición de servicio web como JSON</span><span class="sxs-lookup"><span data-stu-id="30a93-193">Export the Web Service Definition object as JSON</span></span>
<span data-ttu-id="30a93-194">Para modificar la definición para el modelo entrenado para usar el modelo recién entrenado, primero debe usar el cmdlet [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) para exportar a un archivo con formato JSON.</span><span class="sxs-lookup"><span data-stu-id="30a93-194">To modify the definition of the trained model to use the newly trained model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob"></a><span data-ttu-id="30a93-195">Actualizar la referencia al blob ilearner</span><span class="sxs-lookup"><span data-stu-id="30a93-195">Update the reference to the ilearner blob</span></span>
<span data-ttu-id="30a93-196">En los recursos, busque [modelo entrenado], actualice el valor de *uri* en el nodo *locationInfo* con el identificador URI del blob ilearner.</span><span class="sxs-lookup"><span data-stu-id="30a93-196">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="30a93-197">El identificador URI se genera mediante la combinación de *BaseLocation* y *RelativeLocation* a partir del resultado de la llamada de reentrenamiento de BES.</span><span class="sxs-lookup"><span data-stu-id="30a93-197">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span>

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-the-json-into-a-web-service-definition-object"></a><span data-ttu-id="30a93-198">Importar JSON en un objeto de definición de servicio web</span><span class="sxs-lookup"><span data-stu-id="30a93-198">Import the JSON into a Web Service Definition object</span></span>
<span data-ttu-id="30a93-199">Debe utilizar el cmdlet [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) para convertir el archivo JSON modificado en un objeto de definición de servicio web que puede usar para actualizar el experimento predictivo.</span><span class="sxs-lookup"><span data-stu-id="30a93-199">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition object that you can use to update the predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service"></a><span data-ttu-id="30a93-200">Actualizar el servicio web</span><span class="sxs-lookup"><span data-stu-id="30a93-200">Update the web service</span></span>
<span data-ttu-id="30a93-201">Por último, utilice el cmdlet [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) para actualizar el experimento predictivo.</span><span class="sxs-lookup"><span data-stu-id="30a93-201">Finally, use the [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/