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
# <a name="event-hubs-capture-walkthrough-python"></a>Tutorial de Event Hubs Capture: Python

Captura de los centros de eventos es una característica de los centros de eventos que permite tooautomatically entregar Hola transmisión de datos en su tooan de concentrador de eventos cuenta de almacenamiento de blobs de Azure de su elección. Esta capacidad resulta fácil tooperform procesamiento por lotes en los datos de transmisión por secuencias en tiempo real. Este artículo se describe cómo toouse la captura de los centros de eventos con Python. Para obtener más información sobre la captura de los centros de eventos, vea hello [artículo general](event-hubs-archive-overview.md).

Este ejemplo utiliza hello [SDK de Azure Python](https://azure.microsoft.com/develop/python/) característica de captura de toodemonstrate Hola. programa de Hello sender.py envía telemetría entorno simulado tooEvent concentradores en formato JSON. Hello concentrador de eventos está configurado toouse Hola captura característica toowrite este almacenamiento de datos tooblob en lotes. aplicación de Hello capturereader.py, a continuación, lee estos blobs y crea un archivo de datos anexados por dispositivo y después escribe datos de hello en los archivos .csv.

## <a name="what-will-be-accomplished"></a>Lo que se logrará

1. Crear una cuenta de almacenamiento de blobs de Azure y un contenedor de blobs dentro de ella, mediante Hola portal de Azure.
2. Crear un espacio de nombres de concentrador de eventos, mediante Hola portal de Azure.
3. Cree un concentrador de eventos con característica de captura de hello está habilitado, mediante Hola portal de Azure.
4. Enviar el concentrador de eventos de toohello de datos con un script de Python.
5. Leer archivos de Hola de captura de Hola y procesarlos con otro script de Python.

## <a name="prerequisites"></a>Requisitos previos

- Python 2.7.x
- Una suscripción de Azure
- Un [espacio de nombres de Event Hubs y un centro de eventos](event-hubs-create.md) activos.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a>Creación de una cuenta de almacenamiento de Azure
1. Inicie sesión en toohello [portal de Azure][Azure portal].
2. En el panel de navegación izquierdo de hello del portal de hello, haga clic en **New**, a continuación, haga clic en **almacenamiento**y, a continuación, haga clic en **cuenta de almacenamiento**.
3. Complete los campos de hello en la hoja de cuenta de almacenamiento de hello y, a continuación, haga clic en **crear**.
   
   ![][1]
4. Después de ver hello **se ha realizado correctamente en implementaciones** de mensajes, haga clic en nombre de Hola de nueva cuenta de almacenamiento de Hola y Hola **Essentials** hoja, haga clic en **Blobs**. Cuando Hola **servicio Blob** hoja se abre, haga clic en **+ contenedor** en la parte superior de Hola. Contenedor con nombre hello **capturar**, a continuación, cierre hello **servicio Blob** hoja.
5. Haga clic en **las claves de acceso** en hello izquierdo hoja y copia Hola el nombre de cuenta de almacenamiento de Hola y el valor de Hola de **key1**. Guardar estos valores tooNotepad o alguna otra ubicación temporal.

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a>Cree un concentrador de eventos de Python script toosend eventos tooyour
1. Abra el editor de Python que prefiera, como [Visual Studio Code][Visual Studio Code].
2. Crear un script denominado **sender.py**. Esta secuencia de comandos envía concentrador de eventos de tooyour de 200 eventos. Son lecturas simples del entorno enviadas en JSON.
3. Pegue Hola siguiente código en sender.py:
   
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
4. Actualizar Hola anterior código toouse su espacio de nombres, el valor de clave y el nombre del centro de eventos que obtuvo al crear el espacio de nombres de hello centros de eventos.

## <a name="create-a-python-script-tooread-your-capture-files"></a>Crear un tooread de script de Python en los archivos de captura

1. Rellene la hoja de Hola y haga clic en **crear**.
2. Cree un script denominado **capturereader.py**. Este script lee Hola captura archivos y crea un archivo por los datos del dispositivo toowrite Hola solo para ese dispositivo.
3. Pegue Hola siguiente código en capturereader.py:
   
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
4. Ser toopaste seguro de los valores adecuados de hello para el nombre de la cuenta de almacenamiento y la clave en Hola llamada demasiado`startProcessing`.

## <a name="run-hello-scripts"></a>Ejecutar scripts de Hola
1. Abra un símbolo del sistema con Python en su ruta de acceso y, a continuación, ejecute estos comandos paquetes de requisitos previos de Python tooinstall:
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  Si tiene una versión anterior de almacenamiento de azure o azure, puede que necesite hello toouse **--actualizar** opción
   
  Puede que también tenga toorun Hola siguientes (no es necesario en la mayoría de los sistemas):
   
  ```
  pip install cryptography
  ```
2. Cambiar el toowherever directory guardan sender.py y capturereader.py y ejecute este comando:
   
  ```
  start python sender.py
  ```
   
  Este comando inicia un nuevo remitente Hola de Python proceso toorun.
3. Ahora, espere unos minutos para hello captura toorun. A continuación, escriba el siguiente comando en la ventana de comandos original de hello:
   
   ```
   python capturereader.py
   ```

   Este procesador captura usa toodownload de directorio local de hello todos los blobs de Hola de Hola la cuenta o el contenedor de almacenamiento. Procesa cualquiera que no están vacías y escribe los resultados de hello como archivos .csv en el directorio local de Hola.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:

* [Información general de Event Hubs Capture][Overview of Event Hubs Capture]
* Una [aplicación de ejemplo completa que usa Event Hubs][sample application that uses Event Hubs].
* Hola [escalada de procesamiento de eventos con los concentradores de eventos] [ Scale out Event Processing with Event Hubs] ejemplo.
* [Información general de Event Hubs][Event Hubs overview]

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
