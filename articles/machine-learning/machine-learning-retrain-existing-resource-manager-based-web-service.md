---
title: aaaRetrain predictivo existente servicio web | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooretrain un modelo y actualización hello web servicio toouse Hola recién entrenado en aprendizaje automático de Azure."
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
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="70ec6-103">Reciclaje de un servicio web predictivo existente</span><span class="sxs-lookup"><span data-stu-id="70ec6-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="70ec6-104">Este documento describe Hola reciclaje de proceso para hello siguiendo el escenario:</span><span class="sxs-lookup"><span data-stu-id="70ec6-104">This document describes hello retraining process for hello following scenario:</span></span>

* <span data-ttu-id="70ec6-105">Dispone de un experimento de entrenamiento y un experimento predictivo que se ha implementado como un servicio web de operaciones.</span><span class="sxs-lookup"><span data-stu-id="70ec6-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="70ec6-106">Tiene nuevos datos que desea que su tooperform de toouse de servicio web de predicción su puntuación.</span><span class="sxs-lookup"><span data-stu-id="70ec6-106">You have new data that you want your predictive web service toouse tooperform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="70ec6-107">toodeploy un nuevo servicio web debe tener permisos suficientes en hello suscripción toowhich que implementar el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="70ec6-107">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="70ec6-108">Para obtener más información, vea [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="70ec6-108">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="70ec6-109">A partir de su servicio web existente y los experimentos, necesita toofollow estos pasos:</span><span class="sxs-lookup"><span data-stu-id="70ec6-109">Starting with your existing web service and experiments, you need toofollow these steps:</span></span>

1. <span data-ttu-id="70ec6-110">Actualizar modelo Hola.</span><span class="sxs-lookup"><span data-stu-id="70ec6-110">Update hello model.</span></span>
   1. <span data-ttu-id="70ec6-111">Modifique la tooallow de experimento de entrenamiento para web servicio entradas y salidas.</span><span class="sxs-lookup"><span data-stu-id="70ec6-111">Modify your training experiment tooallow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="70ec6-112">Implementar Hola experimento de entrenamiento como un servicio web reconversión.</span><span class="sxs-lookup"><span data-stu-id="70ec6-112">Deploy hello training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="70ec6-113">Utilizar modelo de Hola de tooretrain de servicio de ejecución de lotes (BES) del experimento de entrenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="70ec6-113">Use hello training experiment's Batch Execution Service (BES) tooretrain hello model.</span></span>
2. <span data-ttu-id="70ec6-114">Utilice el experimento de predicción de hello Azure Machine Learning PowerShell cmdlets tooupdate Hola.</span><span class="sxs-lookup"><span data-stu-id="70ec6-114">Use hello Azure Machine Learning PowerShell cmdlets tooupdate hello predictive experiment.</span></span>
   1. <span data-ttu-id="70ec6-115">Inicie sesión en tooyour cuenta de administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="70ec6-115">Sign in tooyour Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="70ec6-116">Obtener la definición de servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="70ec6-116">Get hello web service definition.</span></span>
   3. <span data-ttu-id="70ec6-117">Exportar la definición del servicio web hello como JSON.</span><span class="sxs-lookup"><span data-stu-id="70ec6-117">Export hello web service definition as JSON.</span></span>
   4. <span data-ttu-id="70ec6-118">Actualizar el blob de hello referencia toohello ilearner Hola JSON.</span><span class="sxs-lookup"><span data-stu-id="70ec6-118">Update hello reference toohello ilearner blob in hello JSON.</span></span>
   5. <span data-ttu-id="70ec6-119">Importar Hola JSON en una definición de servicio web.</span><span class="sxs-lookup"><span data-stu-id="70ec6-119">Import hello JSON into a web service definition.</span></span>
   6. <span data-ttu-id="70ec6-120">Actualizar el servicio web de hello con una nueva definición de servicio web.</span><span class="sxs-lookup"><span data-stu-id="70ec6-120">Update hello web service with a new web service definition.</span></span>

## <a name="deploy-hello-training-experiment"></a><span data-ttu-id="70ec6-121">Implementar el experimento de entrenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="70ec6-121">Deploy hello training experiment</span></span>
<span data-ttu-id="70ec6-122">toodeploy Hola experimento de entrenamiento como un servicio web reconversión, debe agregar el modelo de toohello de entradas y salidas del servicio web.</span><span class="sxs-lookup"><span data-stu-id="70ec6-122">toodeploy hello training experiment as a retraining web service, you must add web service inputs and outputs toohello model.</span></span> <span data-ttu-id="70ec6-123">Conectando un *resultado del servicio Web* del experimento de módulo toohello  *[entrenar modelo] [ train-model]*  módulo, se habilita Hola experimento de entrenamiento tooproduce un nuevo modelo entrenado que puede usar en el experimento de predicción.</span><span class="sxs-lookup"><span data-stu-id="70ec6-123">By connecting a *Web Service Output* module toohello experiment's *[Train Model][train-model]* module, you enable hello training experiment tooproduce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="70ec6-124">Si tiene una *evaluar modelo* módulo, también puede adjuntar los resultados de evaluación de Hola de tooget en la salida del servicio web como salida.</span><span class="sxs-lookup"><span data-stu-id="70ec6-124">If you have an *Evaluate Model* module, you can also attach web service output tooget hello evaluation results as output.</span></span>

<span data-ttu-id="70ec6-125">tooupdate el experimento de entrenamiento:</span><span class="sxs-lookup"><span data-stu-id="70ec6-125">tooupdate your training experiment:</span></span>

1. <span data-ttu-id="70ec6-126">Conectar un *entrada de servicio Web* datos tooyour del módulo de entrada (por ejemplo, un *limpiar datos que faltan* módulo).</span><span class="sxs-lookup"><span data-stu-id="70ec6-126">Connect a *Web Service Input* module tooyour data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="70ec6-127">Normalmente, deseará tooensure que los datos de entrada se procesa en Hola de igual manera que los datos de entrenamiento original.</span><span class="sxs-lookup"><span data-stu-id="70ec6-127">Typically, you want tooensure that your input data is processed in hello same way as your original training data.</span></span>
2. <span data-ttu-id="70ec6-128">Conectar un *resultado del servicio Web* toohello salida del módulo de su *entrenar modelo* módulo.</span><span class="sxs-lookup"><span data-stu-id="70ec6-128">Connect a *Web Service Output* module toohello output of your *Train Model* module.</span></span>
3. <span data-ttu-id="70ec6-129">Si tiene una *evaluar modelo* módulo y desea toooutput resultados de la evaluación de hello, conecte un *resultado del servicio Web* toohello salida del módulo de su *evaluar modelo* módulo.</span><span class="sxs-lookup"><span data-stu-id="70ec6-129">If you have an *Evaluate Model* module and you want toooutput hello evaluation results, connect a *Web Service Output* module toohello output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="70ec6-130">Ejecute el experimento.</span><span class="sxs-lookup"><span data-stu-id="70ec6-130">Run your experiment.</span></span>

<span data-ttu-id="70ec6-131">A continuación, debe implementar Hola experimento de entrenamiento como un servicio web que genera un modelo entrenado y resultados de la evaluación de modelo.</span><span class="sxs-lookup"><span data-stu-id="70ec6-131">Next, you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="70ec6-132">En la parte inferior de hello del lienzo del experimento de hello, haga clic en **configurar el servicio de Web**y, a continuación, seleccione **implementar [New] servicio Web**.</span><span class="sxs-lookup"><span data-stu-id="70ec6-132">At hello bottom of hello experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="70ec6-133">Abre el portal de servicios Web de Azure Machine Learning Hello toohello **implementar el servicio de Web** página.</span><span class="sxs-lookup"><span data-stu-id="70ec6-133">hello Azure Machine Learning Web Services portal opens toohello **Deploy Web Service** page.</span></span> <span data-ttu-id="70ec6-134">Escriba un nombre para el servicio web y elija un plan de pago y después haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="70ec6-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="70ec6-135">Solo puede usar el método de ejecución por lotes de hello para la creación de modelos entrenados.</span><span class="sxs-lookup"><span data-stu-id="70ec6-135">You can only use hello Batch Execution method for creating trained models.</span></span>

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a><span data-ttu-id="70ec6-136">Volver a entrenar modelo de hello con nuevos datos utilizando BES</span><span class="sxs-lookup"><span data-stu-id="70ec6-136">Retrain hello model with new data by using BES</span></span>
<span data-ttu-id="70ec6-137">En este ejemplo, estamos usando C# toocreate Hola reciclaje de aplicación.</span><span class="sxs-lookup"><span data-stu-id="70ec6-137">For this example, we're using C# toocreate hello retraining application.</span></span> <span data-ttu-id="70ec6-138">También puede utilizar Python o R tooaccomplish de código de ejemplo de esta tarea.</span><span class="sxs-lookup"><span data-stu-id="70ec6-138">You can also use Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="70ec6-139">toocall Hola reciclaje API:</span><span class="sxs-lookup"><span data-stu-id="70ec6-139">toocall hello retraining APIs:</span></span>

1. <span data-ttu-id="70ec6-140">Cree una nueva aplicación de consola de C# en Visual Studio: **Nuevo** > **Proyecto** > **Visual C#** > **Escritorio clásico de Windows** > **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="70ec6-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="70ec6-141">Inicie sesión en toohello portal de servicios Web de aprendizaje de máquina.</span><span class="sxs-lookup"><span data-stu-id="70ec6-141">Sign in toohello Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="70ec6-142">Haga clic en el servicio web de Hola que está trabajando con.</span><span class="sxs-lookup"><span data-stu-id="70ec6-142">Click hello web service that you're working with.</span></span>
4. <span data-ttu-id="70ec6-143">Haga clic en **Consume**(Consumo).</span><span class="sxs-lookup"><span data-stu-id="70ec6-143">Click **Consume**.</span></span>
5. <span data-ttu-id="70ec6-144">En parte inferior de Hola de hello **Consume** página Hola **código de ejemplo** sección, haga clic en **por lotes**.</span><span class="sxs-lookup"><span data-stu-id="70ec6-144">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="70ec6-145">Copiar código C# ejemplo de Hola para la ejecución por lotes y péguelo en el archivo Program.cs de Hola.</span><span class="sxs-lookup"><span data-stu-id="70ec6-145">Copy hello sample C# code for batch execution and paste it into hello Program.cs file.</span></span> <span data-ttu-id="70ec6-146">Asegúrese de que ese espacio de nombres Hola permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="70ec6-146">Make sure that hello namespace remains intact.</span></span>

<span data-ttu-id="70ec6-147">Agregar paquete de NuGet hello Microsoft.AspNet.WebApi.Client, tal como se especifica en los comentarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="70ec6-147">Add hello NuGet package Microsoft.AspNet.WebApi.Client, as specified in hello comments.</span></span> <span data-ttu-id="70ec6-148">tooadd Hola referencia tooMicrosoft.WindowsAzure.Storage.dll, primero deberá hello tooinstall [biblioteca de cliente para servicios de almacenamiento de Azure](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="70ec6-148">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="70ec6-149">captura de pantalla siguiente Hello muestra hello **Consume** página del portal de servicios Web de Azure Machine Learning Hola.</span><span class="sxs-lookup"><span data-stu-id="70ec6-149">hello following screenshot shows hello **Consume** page in hello Azure Machine Learning Web Services portal.</span></span>

![Página Consumo][1]

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="70ec6-151">Actualizar la declaración de hello apikey</span><span class="sxs-lookup"><span data-stu-id="70ec6-151">Update hello apikey declaration</span></span>
<span data-ttu-id="70ec6-152">Busque hello **apikey** declaración:</span><span class="sxs-lookup"><span data-stu-id="70ec6-152">Locate hello **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="70ec6-153">Hola **información básica de consumo** sección de hello **Consume** página, busque la clave principal de Hola y cópielo toohello **apikey** declaración.</span><span class="sxs-lookup"><span data-stu-id="70ec6-153">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="70ec6-154">Actualizar la información de almacenamiento de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="70ec6-154">Update hello Azure Storage information</span></span>
<span data-ttu-id="70ec6-155">código de ejemplo BES Hola carga un archivo desde un almacenamiento de tooAzure de unidad local (por ejemplo, "C:\temp\CensusIpnput.csv"), lo procesa y escribe Hola resultados atrás tooAzure almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="70ec6-155">hello BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="70ec6-156">información de almacenamiento de Azure de tooupdate hello, debe recuperar la cuenta de almacenamiento de hello información de nombre, la clave y el contenedor de su cuenta de almacenamiento de hello portal de Azure clásico y, a continuación, actualización hello correspondi después de ejecutar el experimento, Hola resultante flujo de trabajo debería ser similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="70ec6-156">tooupdate hello Azure Storage information, you must retrieve hello storage account name, key, and container information for your storage account from hello Azure classic portal, and then update hello correspondi After running your experiment, hello resulting workflow should be similar toohello following:</span></span>

![Flujo de trabajo resultante después de la ejecución][4]<span data-ttu-id="70ec6-158">valores de NG en el código de hello.</span><span class="sxs-lookup"><span data-stu-id="70ec6-158">ng values in hello code.</span></span>

1. <span data-ttu-id="70ec6-159">Inicie sesión en toohello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="70ec6-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="70ec6-160">En la columna de navegación izquierdo de hello, haga clic en **almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="70ec6-160">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="70ec6-161">En lista de Hola de cuentas de almacenamiento, seleccione uno toostore Hola volver a entrenar modelo.</span><span class="sxs-lookup"><span data-stu-id="70ec6-161">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="70ec6-162">En la parte inferior de Hola de página de hello, haga clic en **administrar claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="70ec6-162">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="70ec6-163">Copie y guarde hello **clave de acceso principal** y cuadro de diálogo Cerrar Hola.</span><span class="sxs-lookup"><span data-stu-id="70ec6-163">Copy and save hello **Primary Access Key** and close hello dialog.</span></span>
6. <span data-ttu-id="70ec6-164">En la parte superior de Hola de página de hello, haga clic en **contenedores**.</span><span class="sxs-lookup"><span data-stu-id="70ec6-164">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="70ec6-165">Seleccione un contenedor existente, o crear uno nuevo y guarde el nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="70ec6-165">Select an existing container, or create a new one and save hello name.</span></span>

<span data-ttu-id="70ec6-166">Busque hello *StorageAccountName*, *StorageAccountKey*, y *StorageContainerName* declaraciones y actualizar los valores de hello que guardó en el portal clásico de Hola .</span><span class="sxs-lookup"><span data-stu-id="70ec6-166">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update hello values that you saved from hello classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="70ec6-167">También debe asegurarse de que ese archivo de entrada de hello está disponible en la ubicación de Hola que especifique en el código de hello.</span><span class="sxs-lookup"><span data-stu-id="70ec6-167">You also must ensure that hello input file is available at hello location that you specify in hello code.</span></span>

### <a name="specify-hello-output-location"></a><span data-ttu-id="70ec6-168">Especifique la ubicación de salida de hello</span><span class="sxs-lookup"><span data-stu-id="70ec6-168">Specify hello output location</span></span>
<span data-ttu-id="70ec6-169">Cuando se especifica la ubicación de salida de hello en hello la carga de solicitudes, Hola extensión del archivo de Hola que se especifica en *RelativeLocation* debe especificarse como `ilearner`.</span><span class="sxs-lookup"><span data-stu-id="70ec6-169">When you specify hello output location in hello Request Payload, hello extension of hello file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="70ec6-170">Vea el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="70ec6-170">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="70ec6-171">Hello aquí te mostramos un ejemplo de reciclaje de salida: ![reciclaje salida][6]</span><span class="sxs-lookup"><span data-stu-id="70ec6-171">hello following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="70ec6-172">Evaluar Hola reciclaje resultados</span><span class="sxs-lookup"><span data-stu-id="70ec6-172">Evaluate hello retraining results</span></span>
<span data-ttu-id="70ec6-173">Cuando se ejecuta la aplicación hello, resultado de hello incluye dirección URL de Hola y token de firmas de acceso compartido que se muestran resultados de evaluación de hello tooaccess necesarios.</span><span class="sxs-lookup"><span data-stu-id="70ec6-173">When you run hello application, hello output includes hello URL and shared access signatures token that are necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="70ec6-174">Puede ver los resultados de rendimiento de Hola de hello volver a entrenar modelo mediante la combinación de hello *BaseLocation*, *RelativeLocation*, y *SasBlobToken* de hello unos resultados para *output2* (como se muestra en hello anterior reciclaje imagen de salida) y pegue la dirección URL completa de hello en barra de direcciones del explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="70ec6-174">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL into hello browser address bar.</span></span>  

<span data-ttu-id="70ec6-175">Examine Hola resultados toodetermine si Hola recién entrenado realiza lo suficientemente bien hello tooreplace uno existente.</span><span class="sxs-lookup"><span data-stu-id="70ec6-175">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="70ec6-176">Hola copia *BaseLocation*, *RelativeLocation*, y *SasBlobToken* de hello mostrar los resultados.</span><span class="sxs-lookup"><span data-stu-id="70ec6-176">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results.</span></span>

## <a name="retrain-hello-web-service"></a><span data-ttu-id="70ec6-177">Entrenar el modelo de servicio web de Hola</span><span class="sxs-lookup"><span data-stu-id="70ec6-177">Retrain hello web service</span></span>
<span data-ttu-id="70ec6-178">Al entrenar el modelo de un servicio web nuevo, se actualiza hello web predictivo servicio definición tooreference Hola nuevo modelo entrenado.</span><span class="sxs-lookup"><span data-stu-id="70ec6-178">When you retrain a new web service, you update hello predictive web service definition tooreference hello new trained model.</span></span> <span data-ttu-id="70ec6-179">definición del servicio web Hello es una representación interna de entrenado Hola del servicio web de hello y no es modificable directamente.</span><span class="sxs-lookup"><span data-stu-id="70ec6-179">hello web service definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="70ec6-180">Asegúrese de que está recuperando definición del servicio web hello para el experimento de predicción y no el experimento de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="70ec6-180">Make sure that you are retrieving hello web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-tooazure-resource-manager"></a><span data-ttu-id="70ec6-181">Inicie sesión en el Administrador de recursos tooAzure</span><span class="sxs-lookup"><span data-stu-id="70ec6-181">Sign in tooAzure Resource Manager</span></span>
<span data-ttu-id="70ec6-182">Debe iniciar sesión en la cuenta de Azure desde dentro del entorno de PowerShell de hello tooyour mediante el uso de hello [AzureRmAccount agregar](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="70ec6-182">You must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition-object"></a><span data-ttu-id="70ec6-183">Obtener el objeto de definición de servicio Web de Hola</span><span class="sxs-lookup"><span data-stu-id="70ec6-183">Get hello Web Service Definition object</span></span>
<span data-ttu-id="70ec6-184">A continuación, obtener objeto de definición de servicio Web de Hola Hola llamada [AzureRmMlWebService Get](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="70ec6-184">Next, get hello Web Service Definition object by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="70ec6-185">toodetermine el nombre de grupo de recursos de Hola de un servicio web existente, ejecute el cmdlet de Get-AzureRmMlWebService de hello sin ningún servicio web de parámetros toodisplay hello en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="70ec6-185">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="70ec6-186">Busque el servicio web de hello y, a continuación, examine su identificador de servicio web.</span><span class="sxs-lookup"><span data-stu-id="70ec6-186">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="70ec6-187">nombre de Hola Hola del grupo de recursos es el cuarto elemento de hello en el identificador hello, justo después de hello *resourceGroups* elemento.</span><span class="sxs-lookup"><span data-stu-id="70ec6-187">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="70ec6-188">En el siguiente ejemplo de Hola, nombre del grupo de recursos de hello es SouthCentralUS de MachineLearning de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="70ec6-188">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="70ec6-189">O bien, toodetermine Hola nombre grupo de recursos de un miembro de servicio web, inicie sesión en el portal de servicios Web de Azure Machine Learning toohello.</span><span class="sxs-lookup"><span data-stu-id="70ec6-189">Alternatively, toodetermine hello resource group name of an existing web service, sign in toohello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="70ec6-190">Seleccione el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="70ec6-190">Select hello web service.</span></span> <span data-ttu-id="70ec6-191">nombre del grupo de recursos de Hello es quinto elemento de Hola de hello URL del servicio web de hello, justo después de hello *resourceGroups* elemento.</span><span class="sxs-lookup"><span data-stu-id="70ec6-191">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="70ec6-192">En el siguiente ejemplo de Hola, nombre del grupo de recursos de hello es SouthCentralUS de MachineLearning de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="70ec6-192">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a><span data-ttu-id="70ec6-193">Exportar el objeto de definición de servicio Web de hello como JSON</span><span class="sxs-lookup"><span data-stu-id="70ec6-193">Export hello Web Service Definition object as JSON</span></span>
<span data-ttu-id="70ec6-194">definición de hello toomodify de hello de hello entrenado toouse recién entrena el modelo, primero debe usar hello [AzureRmMlWebService de exportación](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport de cmdlet, archivo tooa formato JSON.</span><span class="sxs-lookup"><span data-stu-id="70ec6-194">toomodify hello definition of hello trained model toouse hello newly trained model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a><span data-ttu-id="70ec6-195">Actualizar Hola referencia toohello ilearner blob</span><span class="sxs-lookup"><span data-stu-id="70ec6-195">Update hello reference toohello ilearner blob</span></span>
<span data-ttu-id="70ec6-196">En los activos de hello, busque Hola [entrenado], actualización hello *uri* valor Hola *locationInfo* nodo con hello URI de blob de hello ilearner.</span><span class="sxs-lookup"><span data-stu-id="70ec6-196">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="70ec6-197">Hello URI generado por la combinación de hello *BaseLocation* hello y *RelativeLocation* de salida de hello de hello llamada reconversión BES.</span><span class="sxs-lookup"><span data-stu-id="70ec6-197">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span>

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

## <a name="import-hello-json-into-a-web-service-definition-object"></a><span data-ttu-id="70ec6-198">Importar Hola JSON en un objeto de definición de servicio Web</span><span class="sxs-lookup"><span data-stu-id="70ec6-198">Import hello JSON into a Web Service Definition object</span></span>
<span data-ttu-id="70ec6-199">Debe usar hello [AzureRmMlWebService de importación](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert Hola modifica archivo JSON en un objeto de definición de servicio Web que se puede usar el experimento de predicative tooupdate Hola.</span><span class="sxs-lookup"><span data-stu-id="70ec6-199">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition object that you can use tooupdate hello predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a><span data-ttu-id="70ec6-200">Actualizar el servicio web de Hola</span><span class="sxs-lookup"><span data-stu-id="70ec6-200">Update hello web service</span></span>
<span data-ttu-id="70ec6-201">Por último, utilice hello [AzureRmMlWebService actualización](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate Hola experimento de predicción.</span><span class="sxs-lookup"><span data-stu-id="70ec6-201">Finally, use hello [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
