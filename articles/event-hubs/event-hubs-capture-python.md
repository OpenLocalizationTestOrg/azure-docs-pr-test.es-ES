---
title: Tutorial de Azure Event Hubs Capture | Microsoft Docs
description: "Ejemplo que usa el SDK de Azure para Python a fin de demostrar el uso de la característica Event Hubs Capture."
services: event-hubs
documentationcenter: 
author: djrosanova
manager: timlt
editor: 
ms.assetid: bdff820c-5b38-4054-a06a-d1de207f01f6
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: darosa;sethm
ms.openlocfilehash: a764a116755c20f60e92e553bd7c896425272b85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a><span data-ttu-id="a43da-103">Tutorial de Event Hubs Capture: Python</span><span class="sxs-lookup"><span data-stu-id="a43da-103">Event Hubs Capture walkthrough: Python</span></span>

<span data-ttu-id="a43da-104">Event Hubs Capture es una característica de Event Hubs que le permite ofrecer automáticamente los datos de streaming que hay en un centro de eventos a la cuenta de Azure Blob Storage que prefiera.</span><span class="sxs-lookup"><span data-stu-id="a43da-104">Event Hubs Capture is a feature of Event Hubs that enables you to automatically deliver the streaming data in your event hub to an Azure Blob storage account of your choice.</span></span> <span data-ttu-id="a43da-105">Esto facilita el procesamiento por lotes en datos de streaming en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="a43da-105">This capability makes it easy to perform batch processing on real-time streaming data.</span></span> <span data-ttu-id="a43da-106">En este artículo se describe cómo utilizar Event Hubs Capture con Python.</span><span class="sxs-lookup"><span data-stu-id="a43da-106">This article describes how to use Event Hubs Capture with Python.</span></span> <span data-ttu-id="a43da-107">Para más información acerca de Event Hubs Capture, consulte este [artículo con información general al respecto](event-hubs-archive-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a43da-107">For more information about Event Hubs Capture, see the [overview article](event-hubs-archive-overview.md).</span></span>

<span data-ttu-id="a43da-108">En este ejemplo se usa el [SDK de Azure para Python](https://azure.microsoft.com/develop/python/) a fin de demostrar la característica Capture.</span><span class="sxs-lookup"><span data-stu-id="a43da-108">This sample uses the [Azure Python SDK](https://azure.microsoft.com/develop/python/) to demonstrate the Capture feature.</span></span> <span data-ttu-id="a43da-109">El programa sender.py envía datos telemétricos del entorno simulados a Event Hubs en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a43da-109">The sender.py program sends simulated environmental telemetry to Event Hubs in JSON format.</span></span> <span data-ttu-id="a43da-110">El centro de eventos está configurado para usar la característica Capture para escribir estos datos en Blob Storage en lotes.</span><span class="sxs-lookup"><span data-stu-id="a43da-110">The event hub is configured to use the Capture feature to write this data to blob storage in batches.</span></span> <span data-ttu-id="a43da-111">Luego, la aplicación capturereader.py lee estos blobs y crea un archivo de anexos por dispositivo, y escribe los datos en archivos .csv.</span><span class="sxs-lookup"><span data-stu-id="a43da-111">The capturereader.py app then reads these blobs and creates an append file per device, then writes the data into .csv files.</span></span>

## <a name="what-will-be-accomplished"></a><span data-ttu-id="a43da-112">Lo que se logrará</span><span class="sxs-lookup"><span data-stu-id="a43da-112">What will be accomplished</span></span>

1. <span data-ttu-id="a43da-113">Crear una cuenta de Azure Blob Storage y un contenedor de blobs en ella, para lo que se debe usar Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a43da-113">Create an Azure Blob Storage account and a blob container within it, using the Azure portal.</span></span>
2. <span data-ttu-id="a43da-114">Crear un espacio de nombres del Centro de eventos desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a43da-114">Create an Event Hub namespace, using the Azure portal.</span></span>
3. <span data-ttu-id="a43da-115">Crear un centro de eventos con la característica Capture habilitada desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a43da-115">Create an event hub with the Capture feature enabled, using the Azure portal.</span></span>
4. <span data-ttu-id="a43da-116">Enviar datos al centro de eventos con un script de Python.</span><span class="sxs-lookup"><span data-stu-id="a43da-116">Send data to the event hub with a Python script.</span></span>
5. <span data-ttu-id="a43da-117">Leer los archivos de la captura y procesarlos con otro script de Python.</span><span class="sxs-lookup"><span data-stu-id="a43da-117">Read the files from the capture and process them with another Python script.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a43da-118">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a43da-118">Prerequisites</span></span>

- <span data-ttu-id="a43da-119">Python 2.7.x</span><span class="sxs-lookup"><span data-stu-id="a43da-119">Python 2.7.x</span></span>
- <span data-ttu-id="a43da-120">Una suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="a43da-120">An Azure subscription</span></span>
- <span data-ttu-id="a43da-121">Un [espacio de nombres de Event Hubs y un centro de eventos](event-hubs-create.md) activos.</span><span class="sxs-lookup"><span data-stu-id="a43da-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="a43da-122">Creación de una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="a43da-122">Create an Azure Storage account</span></span>
1. <span data-ttu-id="a43da-123">Inicie sesión en [Azure Portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="a43da-123">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="a43da-124">En el panel de navegación izquierdo del portal, haga clic en **Nuevo**, luego en **Storage** y, a continuación, en **Cuenta de Storage**.</span><span class="sxs-lookup"><span data-stu-id="a43da-124">In the left navigation pane of the portal, click **New**, then click **Storage**, and then click **Storage Account**.</span></span>
3. <span data-ttu-id="a43da-125">Complete los campos de la hoja de la cuenta de almacenamiento y, luego, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a43da-125">Complete the fields in the storage account blade and then click **Create**.</span></span>
   
   ![][1]
4. <span data-ttu-id="a43da-126">Una vez que aparezca el mensaje **Implementaciones correctas**, haga clic en el nombre de la nueva cuenta de almacenamiento y, en la hoja **Essentials**, haga clic en **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="a43da-126">After you see the **Deployments Succeeded** message, click the name of the new storage account and in the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="a43da-127">Cuando se abra la hoja **Blob service**, haga clic en **+ Container** (Contenedor +) en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="a43da-127">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="a43da-128">Asigne al contenedor el nombre **capture** (captura) y cierre la hoja **Blob service** (Servicio Blob).</span><span class="sxs-lookup"><span data-stu-id="a43da-128">Name the container **capture**, then close the **Blob service** blade.</span></span>
5. <span data-ttu-id="a43da-129">Haga clic en **Claves de acceso** en la hoja izquierda y copie el nombre de la cuenta de almacenamiento y el valor de **key1**.</span><span class="sxs-lookup"><span data-stu-id="a43da-129">Click **Access keys** in the left blade and copy the name of the storage account and the value of **key1**.</span></span> <span data-ttu-id="a43da-130">Guarde estos valores en el Bloc de notas, o en cualquier otra ubicación temporal.</span><span class="sxs-lookup"><span data-stu-id="a43da-130">Save these values to Notepad or some other temporary location.</span></span>

## <a name="create-a-python-script-to-send-events-to-your-event-hub"></a><span data-ttu-id="a43da-131">Creación de un script de Python para enviar eventos a un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="a43da-131">Create a Python script to send events to your event hub</span></span>
1. <span data-ttu-id="a43da-132">Abra el editor de Python que prefiera, como [Visual Studio Code][Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="a43da-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="a43da-133">Crear un script denominado **sender.py**.</span><span class="sxs-lookup"><span data-stu-id="a43da-133">Create a script called **sender.py**.</span></span> <span data-ttu-id="a43da-134">Este script le envía 200 eventos a un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="a43da-134">This script sends 200 events to your event hub.</span></span> <span data-ttu-id="a43da-135">Son lecturas simples del entorno enviadas en JSON.</span><span class="sxs-lookup"><span data-stu-id="a43da-135">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="a43da-136">Pegue el código siguiente en sender.py:</span><span class="sxs-lookup"><span data-stu-id="a43da-136">Paste the following code into sender.py:</span></span>
   
  ```python
  import uuid
  import datetime
  import random
  import json
  from azure.servicebus import ServiceBusService
   
  sbs = ServiceBusService(service_namespace='INSERT YOUR NAMESPACE NAME', shared_access_key_name='RootManageSharedAccessKey', shared_access_key_value='INSERT YOUR KEY')
  devices = []
  for x in range(0, 10):
      devices.append(str(uuid.uuid4()))
   
  for y in range(0,20):
      for dev in devices:
          reading = {'id': dev, 'timestamp': str(datetime.datetime.utcnow()), 'uv': random.random(), 'temperature': random.randint(70, 100), 'humidity': random.randint(70, 100)}
          s = json.dumps(reading)
          sbs.send_event('INSERT YOUR EVENT HUB NAME', s)
      print y
  ```
4. <span data-ttu-id="a43da-137">Actualice el código anterior para que use el nombre del espacio de nombres, el valor de clave y el nombre del centro de eventos que obtuviera cuando se creó el espacio de nombres de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="a43da-137">Update the preceding code to use your namespace name, key value, and event hub name that you obtained when you created the Event Hubs namespace.</span></span>

## <a name="create-a-python-script-to-read-your-capture-files"></a><span data-ttu-id="a43da-138">Creación de un script de Python que lea archivos de Capture</span><span class="sxs-lookup"><span data-stu-id="a43da-138">Create a Python script to read your Capture files</span></span>

1. <span data-ttu-id="a43da-139">Rellene la hoja y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a43da-139">Fill out the blade and click **Create**.</span></span>
2. <span data-ttu-id="a43da-140">Cree un script denominado **capturereader.py**.</span><span class="sxs-lookup"><span data-stu-id="a43da-140">Create a script called **capturereader.py**.</span></span> <span data-ttu-id="a43da-141">Este script lee los archivos capturados y crea un archivo por dispositivo para escribir los datos solo para dicho dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a43da-141">This script reads the captured files and creates a file per device to write the data only for that device.</span></span>
3. <span data-ttu-id="a43da-142">Pegue el código siguiente en capturereader.py:</span><span class="sxs-lookup"><span data-stu-id="a43da-142">Paste the following code into capturereader.py:</span></span>
   
  ```python
  import os
  import string
  import json
  import avro.schema
  from avro.datafile import DataFileReader, DataFileWriter
  from avro.io import DatumReader, DatumWriter
  from azure.storage.blob import BlockBlobService
   
  def processBlob(filename):
      reader = DataFileReader(open(filename, 'rb'), DatumReader())
      dict = {}
      for reading in reader:
          parsed_json = json.loads(reading["Body"])
          if not 'id' in parsed_json:
              return
          if not dict.has_key(parsed_json['id']):
              list = []
              dict[parsed_json['id']] = list
          else:
              list = dict[parsed_json['id']]
              list.append(parsed_json)
      reader.close()
      for device in dict.keys():
          deviceFile = open(device + '.csv', "a")
          for r in dict[device]:
              deviceFile.write(", ".join([str(r[x]) for x in r.keys()])+'\n')
   
  def startProcessing(accountName, key, container):
      print 'Processor started using path: ' + os.getcwd()
      block_blob_service = BlockBlobService(account_name=accountName, account_key=key)
      generator = block_blob_service.list_blobs(container)
      for blob in generator:
          if blob.properties.content_length != 0:
              print('Downloaded a non empty blob: ' + blob.name)
              cleanName = string.replace(blob.name, '/', '_')
              block_blob_service.get_blob_to_path(container, blob.name, cleanName)
              processBlob(cleanName)
              os.remove(cleanName)
          block_blob_service.delete_blob(container, blob.name)
  startProcessing('YOUR STORAGE ACCOUNT NAME', 'YOUR KEY', 'capture')
  ```
4. <span data-ttu-id="a43da-143">Asegúrese de pegar los valores adecuados del nombre y la clave de su cuenta de almacenamiento en la llamada a `startProcessing`.</span><span class="sxs-lookup"><span data-stu-id="a43da-143">Be sure to paste the appropriate values for your storage account name and key in the call to `startProcessing`.</span></span>

## <a name="run-the-scripts"></a><span data-ttu-id="a43da-144">Ejecución de los scripts</span><span class="sxs-lookup"><span data-stu-id="a43da-144">Run the scripts</span></span>
1. <span data-ttu-id="a43da-145">Abra un símbolo del sistema que tiene Python en su ruta de acceso y, después, ejecute dichos comandos para instalar los paquetes de requisitos previos de Python:</span><span class="sxs-lookup"><span data-stu-id="a43da-145">Open a command prompt that has Python in its path, and then run these commands to install Python prerequisite packages:</span></span>
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  <span data-ttu-id="a43da-146">Si tiene una versión anterior de azure-storage o azure, puede que necesite utilizar la opción **--upgrade**</span><span class="sxs-lookup"><span data-stu-id="a43da-146">If you have an earlier version of either azure-storage or azure, you may need to use the **--upgrade** option</span></span>
   
  <span data-ttu-id="a43da-147">Es posible que también deba ejecutar el siguiente comando (no es necesario en la mayoría de los sistemas):</span><span class="sxs-lookup"><span data-stu-id="a43da-147">You might also need to run the following (not necessary on most systems):</span></span>
   
  ```
  pip install cryptography
  ```
2. <span data-ttu-id="a43da-148">Cambie el directorio a la ubicación en que guardó sender.py y capturereader.py, y ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="a43da-148">Change your directory to wherever you saved sender.py and capturereader.py, and run this command:</span></span>
   
  ```
  start python sender.py
  ```
   
  <span data-ttu-id="a43da-149">Este comando inicia un nuevo proceso de Python para ejecutar el remitente.</span><span class="sxs-lookup"><span data-stu-id="a43da-149">This command starts a new Python process to run the sender.</span></span>
3. <span data-ttu-id="a43da-150">Espere unos minutos para que se ejecute la captura.</span><span class="sxs-lookup"><span data-stu-id="a43da-150">Now wait a few minutes for the capture to run.</span></span> <span data-ttu-id="a43da-151">Después, escriba el siguiente comando en la ventana de comandos original:</span><span class="sxs-lookup"><span data-stu-id="a43da-151">Then type the following command into your original command window:</span></span>
   
   ```
   python capturereader.py
   ```

   <span data-ttu-id="a43da-152">Este procesador de captura usa el directorio local para descargar todos los blobs del contenedor o de la cuenta de captura.</span><span class="sxs-lookup"><span data-stu-id="a43da-152">This capture processor uses the local directory to download all the blobs from the storage account/container.</span></span> <span data-ttu-id="a43da-153">Procesa los que no estén vacíos y escribe los resultados en forma de archivos .csv en el directorio local.</span><span class="sxs-lookup"><span data-stu-id="a43da-153">It processes any that are not empty, and writes the results as .csv files into the local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a43da-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a43da-154">Next steps</span></span>

<span data-ttu-id="a43da-155">Para más información acerca de Event Hubs, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a43da-155">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="a43da-156">[Información general de Event Hubs Capture][Overview of Event Hubs Capture]</span><span class="sxs-lookup"><span data-stu-id="a43da-156">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span></span>
* <span data-ttu-id="a43da-157">Una [aplicación de ejemplo completa que usa Event Hubs][sample application that uses Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="a43da-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span></span>
* <span data-ttu-id="a43da-158">El ejemplo [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] (Escalado horizontal del procesamiento de eventos con Event Hubs).</span><span class="sxs-lookup"><span data-stu-id="a43da-158">The [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span></span>
* <span data-ttu-id="a43da-159">[Información general de Event Hubs][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="a43da-159">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
