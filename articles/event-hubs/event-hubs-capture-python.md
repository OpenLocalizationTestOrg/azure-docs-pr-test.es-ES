---
title: Tutorial de captura de los centros de eventos aaaAzure | Documentos de Microsoft
description: "Ejemplo que usa hello Azure SDK de Python toodemonstrate mediante la característica de captura de los centros de eventos de Hola."
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
ms.openlocfilehash: 1737dcca283711d863aa970db0e80ae71814e666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a><span data-ttu-id="b8847-103">Tutorial de Event Hubs Capture: Python</span><span class="sxs-lookup"><span data-stu-id="b8847-103">Event Hubs Capture walkthrough: Python</span></span>

<span data-ttu-id="b8847-104">Captura de los centros de eventos es una característica de los centros de eventos que permite tooautomatically entregar Hola transmisión de datos en su tooan de concentrador de eventos cuenta de almacenamiento de blobs de Azure de su elección.</span><span class="sxs-lookup"><span data-stu-id="b8847-104">Event Hubs Capture is a feature of Event Hubs that enables you tooautomatically deliver hello streaming data in your event hub tooan Azure Blob storage account of your choice.</span></span> <span data-ttu-id="b8847-105">Esta capacidad resulta fácil tooperform procesamiento por lotes en los datos de transmisión por secuencias en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="b8847-105">This capability makes it easy tooperform batch processing on real-time streaming data.</span></span> <span data-ttu-id="b8847-106">Este artículo se describe cómo toouse la captura de los centros de eventos con Python.</span><span class="sxs-lookup"><span data-stu-id="b8847-106">This article describes how toouse Event Hubs Capture with Python.</span></span> <span data-ttu-id="b8847-107">Para obtener más información sobre la captura de los centros de eventos, vea hello [artículo general](event-hubs-archive-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b8847-107">For more information about Event Hubs Capture, see hello [overview article](event-hubs-archive-overview.md).</span></span>

<span data-ttu-id="b8847-108">Este ejemplo utiliza hello [SDK de Azure Python](https://azure.microsoft.com/develop/python/) característica de captura de toodemonstrate Hola.</span><span class="sxs-lookup"><span data-stu-id="b8847-108">This sample uses hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) toodemonstrate hello Capture feature.</span></span> <span data-ttu-id="b8847-109">programa de Hello sender.py envía telemetría entorno simulado tooEvent concentradores en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="b8847-109">hello sender.py program sends simulated environmental telemetry tooEvent Hubs in JSON format.</span></span> <span data-ttu-id="b8847-110">Hello concentrador de eventos está configurado toouse Hola captura característica toowrite este almacenamiento de datos tooblob en lotes.</span><span class="sxs-lookup"><span data-stu-id="b8847-110">hello event hub is configured toouse hello Capture feature toowrite this data tooblob storage in batches.</span></span> <span data-ttu-id="b8847-111">aplicación de Hello capturereader.py, a continuación, lee estos blobs y crea un archivo de datos anexados por dispositivo y después escribe datos de hello en los archivos .csv.</span><span class="sxs-lookup"><span data-stu-id="b8847-111">hello capturereader.py app then reads these blobs and creates an append file per device, then writes hello data into .csv files.</span></span>

## <a name="what-will-be-accomplished"></a><span data-ttu-id="b8847-112">Lo que se logrará</span><span class="sxs-lookup"><span data-stu-id="b8847-112">What will be accomplished</span></span>

1. <span data-ttu-id="b8847-113">Crear una cuenta de almacenamiento de blobs de Azure y un contenedor de blobs dentro de ella, mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8847-113">Create an Azure Blob Storage account and a blob container within it, using hello Azure portal.</span></span>
2. <span data-ttu-id="b8847-114">Crear un espacio de nombres de concentrador de eventos, mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8847-114">Create an Event Hub namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="b8847-115">Cree un concentrador de eventos con característica de captura de hello está habilitado, mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8847-115">Create an event hub with hello Capture feature enabled, using hello Azure portal.</span></span>
4. <span data-ttu-id="b8847-116">Enviar el concentrador de eventos de toohello de datos con un script de Python.</span><span class="sxs-lookup"><span data-stu-id="b8847-116">Send data toohello event hub with a Python script.</span></span>
5. <span data-ttu-id="b8847-117">Leer archivos de Hola de captura de Hola y procesarlos con otro script de Python.</span><span class="sxs-lookup"><span data-stu-id="b8847-117">Read hello files from hello capture and process them with another Python script.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8847-118">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b8847-118">Prerequisites</span></span>

- <span data-ttu-id="b8847-119">Python 2.7.x</span><span class="sxs-lookup"><span data-stu-id="b8847-119">Python 2.7.x</span></span>
- <span data-ttu-id="b8847-120">Una suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="b8847-120">An Azure subscription</span></span>
- <span data-ttu-id="b8847-121">Un [espacio de nombres de Event Hubs y un centro de eventos](event-hubs-create.md) activos.</span><span class="sxs-lookup"><span data-stu-id="b8847-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="b8847-122">Creación de una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="b8847-122">Create an Azure Storage account</span></span>
1. <span data-ttu-id="b8847-123">Inicie sesión en toohello [portal de Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="b8847-123">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="b8847-124">En el panel de navegación izquierdo de hello del portal de hello, haga clic en **New**, a continuación, haga clic en **almacenamiento**y, a continuación, haga clic en **cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="b8847-124">In hello left navigation pane of hello portal, click **New**, then click **Storage**, and then click **Storage Account**.</span></span>
3. <span data-ttu-id="b8847-125">Complete los campos de hello en la hoja de cuenta de almacenamiento de hello y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="b8847-125">Complete hello fields in hello storage account blade and then click **Create**.</span></span>
   
   ![][1]
4. <span data-ttu-id="b8847-126">Después de ver hello **se ha realizado correctamente en implementaciones** de mensajes, haga clic en nombre de Hola de nueva cuenta de almacenamiento de Hola y Hola **Essentials** hoja, haga clic en **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="b8847-126">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account and in hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="b8847-127">Cuando Hola **servicio Blob** hoja se abre, haga clic en **+ contenedor** en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8847-127">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="b8847-128">Contenedor con nombre hello **capturar**, a continuación, cierre hello **servicio Blob** hoja.</span><span class="sxs-lookup"><span data-stu-id="b8847-128">Name hello container **capture**, then close hello **Blob service** blade.</span></span>
5. <span data-ttu-id="b8847-129">Haga clic en **las claves de acceso** en hello izquierdo hoja y copia Hola el nombre de cuenta de almacenamiento de Hola y el valor de Hola de **key1**.</span><span class="sxs-lookup"><span data-stu-id="b8847-129">Click **Access keys** in hello left blade and copy hello name of hello storage account and hello value of **key1**.</span></span> <span data-ttu-id="b8847-130">Guardar estos valores tooNotepad o alguna otra ubicación temporal.</span><span class="sxs-lookup"><span data-stu-id="b8847-130">Save these values tooNotepad or some other temporary location.</span></span>

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a><span data-ttu-id="b8847-131">Cree un concentrador de eventos de Python script toosend eventos tooyour</span><span class="sxs-lookup"><span data-stu-id="b8847-131">Create a Python script toosend events tooyour event hub</span></span>
1. <span data-ttu-id="b8847-132">Abra el editor de Python que prefiera, como [Visual Studio Code][Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="b8847-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="b8847-133">Crear un script denominado **sender.py**.</span><span class="sxs-lookup"><span data-stu-id="b8847-133">Create a script called **sender.py**.</span></span> <span data-ttu-id="b8847-134">Esta secuencia de comandos envía concentrador de eventos de tooyour de 200 eventos.</span><span class="sxs-lookup"><span data-stu-id="b8847-134">This script sends 200 events tooyour event hub.</span></span> <span data-ttu-id="b8847-135">Son lecturas simples del entorno enviadas en JSON.</span><span class="sxs-lookup"><span data-stu-id="b8847-135">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="b8847-136">Pegue Hola siguiente código en sender.py:</span><span class="sxs-lookup"><span data-stu-id="b8847-136">Paste hello following code into sender.py:</span></span>
   
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
4. <span data-ttu-id="b8847-137">Actualizar Hola anterior código toouse su espacio de nombres, el valor de clave y el nombre del centro de eventos que obtuvo al crear el espacio de nombres de hello centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="b8847-137">Update hello preceding code toouse your namespace name, key value, and event hub name that you obtained when you created hello Event Hubs namespace.</span></span>

## <a name="create-a-python-script-tooread-your-capture-files"></a><span data-ttu-id="b8847-138">Crear un tooread de script de Python en los archivos de captura</span><span class="sxs-lookup"><span data-stu-id="b8847-138">Create a Python script tooread your Capture files</span></span>

1. <span data-ttu-id="b8847-139">Rellene la hoja de Hola y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="b8847-139">Fill out hello blade and click **Create**.</span></span>
2. <span data-ttu-id="b8847-140">Cree un script denominado **capturereader.py**.</span><span class="sxs-lookup"><span data-stu-id="b8847-140">Create a script called **capturereader.py**.</span></span> <span data-ttu-id="b8847-141">Este script lee Hola captura archivos y crea un archivo por los datos del dispositivo toowrite Hola solo para ese dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b8847-141">This script reads hello captured files and creates a file per device toowrite hello data only for that device.</span></span>
3. <span data-ttu-id="b8847-142">Pegue Hola siguiente código en capturereader.py:</span><span class="sxs-lookup"><span data-stu-id="b8847-142">Paste hello following code into capturereader.py:</span></span>
   
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
4. <span data-ttu-id="b8847-143">Ser toopaste seguro de los valores adecuados de hello para el nombre de la cuenta de almacenamiento y la clave en Hola llamada demasiado`startProcessing`.</span><span class="sxs-lookup"><span data-stu-id="b8847-143">Be sure toopaste hello appropriate values for your storage account name and key in hello call too`startProcessing`.</span></span>

## <a name="run-hello-scripts"></a><span data-ttu-id="b8847-144">Ejecutar scripts de Hola</span><span class="sxs-lookup"><span data-stu-id="b8847-144">Run hello scripts</span></span>
1. <span data-ttu-id="b8847-145">Abra un símbolo del sistema con Python en su ruta de acceso y, a continuación, ejecute estos comandos paquetes de requisitos previos de Python tooinstall:</span><span class="sxs-lookup"><span data-stu-id="b8847-145">Open a command prompt that has Python in its path, and then run these commands tooinstall Python prerequisite packages:</span></span>
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  <span data-ttu-id="b8847-146">Si tiene una versión anterior de almacenamiento de azure o azure, puede que necesite hello toouse **--actualizar** opción</span><span class="sxs-lookup"><span data-stu-id="b8847-146">If you have an earlier version of either azure-storage or azure, you may need toouse hello **--upgrade** option</span></span>
   
  <span data-ttu-id="b8847-147">Puede que también tenga toorun Hola siguientes (no es necesario en la mayoría de los sistemas):</span><span class="sxs-lookup"><span data-stu-id="b8847-147">You might also need toorun hello following (not necessary on most systems):</span></span>
   
  ```
  pip install cryptography
  ```
2. <span data-ttu-id="b8847-148">Cambiar el toowherever directory guardan sender.py y capturereader.py y ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="b8847-148">Change your directory toowherever you saved sender.py and capturereader.py, and run this command:</span></span>
   
  ```
  start python sender.py
  ```
   
  <span data-ttu-id="b8847-149">Este comando inicia un nuevo remitente Hola de Python proceso toorun.</span><span class="sxs-lookup"><span data-stu-id="b8847-149">This command starts a new Python process toorun hello sender.</span></span>
3. <span data-ttu-id="b8847-150">Ahora, espere unos minutos para hello captura toorun.</span><span class="sxs-lookup"><span data-stu-id="b8847-150">Now wait a few minutes for hello capture toorun.</span></span> <span data-ttu-id="b8847-151">A continuación, escriba el siguiente comando en la ventana de comandos original de hello:</span><span class="sxs-lookup"><span data-stu-id="b8847-151">Then type hello following command into your original command window:</span></span>
   
   ```
   python capturereader.py
   ```

   <span data-ttu-id="b8847-152">Este procesador captura usa toodownload de directorio local de hello todos los blobs de Hola de Hola la cuenta o el contenedor de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b8847-152">This capture processor uses hello local directory toodownload all hello blobs from hello storage account/container.</span></span> <span data-ttu-id="b8847-153">Procesa cualquiera que no están vacías y escribe los resultados de hello como archivos .csv en el directorio local de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8847-153">It processes any that are not empty, and writes hello results as .csv files into hello local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8847-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b8847-154">Next steps</span></span>

<span data-ttu-id="b8847-155">Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="b8847-155">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="b8847-156">[Información general de Event Hubs Capture][Overview of Event Hubs Capture]</span><span class="sxs-lookup"><span data-stu-id="b8847-156">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span></span>
* <span data-ttu-id="b8847-157">Una [aplicación de ejemplo completa que usa Event Hubs][sample application that uses Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="b8847-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span></span>
* <span data-ttu-id="b8847-158">Hola [escalada de procesamiento de eventos con los concentradores de eventos] [ Scale out Event Processing with Event Hubs] ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b8847-158">hello [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span></span>
* <span data-ttu-id="b8847-159">[Información general de Event Hubs][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="b8847-159">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
