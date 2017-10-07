---
title: "Connect Raspberry PI (C) tooAzure IoT - lección 3: ejecutar el ejemplo | Documentos de Microsoft"
description: "Implemente y ejecute un tooRaspberry de aplicación de ejemplo 3 de Pi que envía el centro de IoT tooyour de mensajes y parpadea Hola LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: pi en la nube con parpadeo del led, parpadeo del led desde la nube
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c484beb2e2d3a3cf19f071f2ba87b9a4fe41c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Ejecutar un toosend de la aplicación de ejemplo mensajes del dispositivo a la nube
## <a name="what-you-will-do"></a>Lo que hará
En este artículo le mostrará cómo toodeploy y ejecute una aplicación de ejemplo en frambuesa Pi 3 que envía mensajes tooyour centro de IoT. Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá
Obtendrá información sobre cómo hello toouse gulp toodeploy de herramienta y ejecutar la aplicación de Node.js de ejemplo de Hola en Pi.

## <a name="what-you-need"></a>Lo que necesita
* Antes de iniciar esta tarea, debe haber completado correctamente [crear una aplicación de Azure de función y un centro de IoT de almacenamiento cuenta tooprocess y el almacén de mensajes](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obtención de las cadenas de conexión de IoT Hub y del dispositivo
cadena de conexión de dispositivo de Hello participa en el centro de IoT de Pi tooconnect tooyour. Hola cadena de conexión de base de datos central de IoT es registro, identidad toohello tooconnect usado en los dispositivos de Hola de IoT hub toomanage que se permiten tooconnect tooyour IoT hub. 

* Lista de todos los centros de IoT. en el grupo de recursos si ejecuta Hola siguiente comando de CLI de Azure:

```bash
az iot hub list -g iot-sample --query [].name
```

Use `iot-sample` como valor de Hola de `{resource group name}` si no cambia el valor de Hola.

* Obtener la cadena de conexión de base de datos central de hello IoT ejecutando el siguiente comando de CLI de Azure de hello:

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

`{my hub name}`es el nombre de Hola que especificó cuando creó el centro de IoT y había registrado Pi.

* Obtener la cadena de conexión de dispositivo de hello ejecutando Hola siguiente comando:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

Use `myraspberrypi` como valor de Hola de `{device id}` si no cambia el valor de Hola.

## <a name="configure-hello-device-connection"></a>Configurar conexión de dispositivo de Hola
1. Inicializar el archivo de configuración de hello ejecutando Hola siguientes comandos:
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> Ejecute también **gulp install-tools** si no lo hizo en la lección 1.

2. Archivo de configuración de dispositivos de hello abierto `config-raspberrypi.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. Realizar Hola después reemplazos en hello `config-raspberrypi.json` archivo:
   
   * Reemplace **[nombre de host de dispositivo o dirección IP]** con el nombre de host o dirección de la IP del dispositivo Hola que se obtuvo al `device-discovery-cli` o con el valor de hello heredado al configurar el dispositivo.
   * Reemplace **[cadena de conexión de dispositivos de IoT]** con hello `device connection string` obtenidas.
   * Reemplace **[cadena de conexión de base de datos central de IoT]** con hello `iot hub connection string` obtenidas.

> [!NOTE]
> `azure_storage_connection_string` no es necesario en este artículo. Déjelo como está.

Hola de actualización `config-raspberrypi.json` de archivos para que pueda implementar la aplicación de ejemplo de Hola desde su equipo.

## <a name="deploy-and-run-hello-sample-application"></a>Implementar y ejecutar la aplicación de ejemplo de Hola
Implementar y ejecutar la aplicación de ejemplo de Hola en Pi ejecutando Hola siguiente comando:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Compruebe que la aplicación de ejemplo de Hola funciona
Debería ver Hola LED que está conectado tooPi parpadea cada dos segundos. Cada vez que Hola LED parpadea, aplicación de ejemplo de Hola envía un centro de IoT tooyour de mensaje y comprueba que ese mensaje Hola se ha enviado correctamente tooyour centro de IoT. Además, cada mensaje recibido por el centro de IoT Hola se imprime en la ventana de la consola de Hola. aplicación de ejemplo de Hola finaliza automáticamente después de enviar 20 mensajes.

![Aplicación de ejemplo con mensajes enviados y recibidos](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a>Resumen
Ha implementado y ejecute nueva aplicación de ejemplo de intermitencia Hola en Centro de IoT tooyour de Pi toosend mensajes del dispositivo a la nube. Ahora, supervisar los mensajes tal y como se escriben toohello cuenta de almacenamiento.

## <a name="next-steps"></a>Pasos siguientes
[Read messages persisted in Azure Storage](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md) (Lectura de los mensajes guardados en Azure Storage)

