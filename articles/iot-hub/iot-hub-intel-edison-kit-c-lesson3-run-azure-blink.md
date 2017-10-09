---
title: "Connect Intel Edison (C) tooAzure IoT - lección 3: enviar mensajes | Documentos de Microsoft"
description: "Implemente y ejecute un tooIntel de aplicación de ejemplo Edison que envía el centro de IoT tooyour de mensajes y parpadea Hola LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servicio de nube de IOT, arduino enviar datos toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 12672b64-795a-4dfc-86fd-df53ed3eeef7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 83615335027cc792b89d3894578fc3f7a55e5c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Ejecutar un toosend de la aplicación de ejemplo mensajes del dispositivo a la nube
## <a name="what-you-will-do"></a>Lo que hará
En este artículo le mostrará cómo toodeploy y ejecute una aplicación de ejemplo en Edison de Intel que envía mensajes tooyour centro de IoT. Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].

## <a name="what-you-will-learn"></a>Lo qué aprenderá
Aprenderá cómo hello toouse gulp toodeploy de herramienta y ejecutar la aplicación de C de ejemplo de Hola en Edison.

## <a name="what-you-need"></a>Lo que necesita
* Antes de iniciar esta tarea, debe haber completado correctamente [crear una aplicación de Azure de función y un centro de IoT de almacenamiento cuenta tooprocess y el almacén de mensajes][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obtención de las cadenas de conexión de IoT Hub y del dispositivo
cadena de conexión de dispositivo de Hello es usado tooconnect centro de IoT Edison tooyour. Hola la cadena de conexión de base de datos central de IoT es tooconnect usado su identidad de dispositivos de IoT hub toohello que representa Edison en el centro de IoT Hola.

* Lista de todos los centros de IoT. en el grupo de recursos si ejecuta Hola siguiente comando de CLI de Azure:

```bash
az iot hub list -g iot-sample --query [].name
```

Use `iot-sample` como valor de Hola de `{resource group name}` si no cambia el valor de Hola.

* Obtener la cadena de conexión de base de datos central de hello IoT ejecutando el siguiente comando de CLI de Azure de hello:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`es el nombre de Hola que especificó cuando creó el centro de IoT y había registrado a Edison.

* Obtener la cadena de conexión de dispositivo de hello ejecutando Hola siguiente comando:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

Use `myinteledison` como valor de Hola de `{device id}` si no cambia el valor de Hola.

## <a name="configure-hello-device-connection"></a>Configurar conexión de dispositivo de Hola
1. Inicializar el archivo de configuración de hello ejecutando Hola siguientes comandos:

   ```bash
   npm install
   gulp init
   ```
   > [!NOTE]
   > Ejecute también **gulp install-tools** si no lo hizo en la lección 1.

2. Archivo de configuración de dispositivos de hello abierto `config-edison.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)

3. Realizar Hola después reemplazos en hello `config-edison.json` archivo:

   * Reemplace **[nombre de host de dispositivo o dirección IP]** con la dirección IP del dispositivo Hola marcados como inactivos cuando se configura el dispositivo.
   * Reemplace **[cadena de conexión de dispositivos de IoT]** con hello `device connection string` obtenidas.
   * Reemplace **[cadena de conexión de base de datos central de IoT]** con hello `iot hub connection string` obtenidas.

   > [!NOTE]
   > `azure_storage_connection_string` no es necesario en este artículo. Déjelo como está.

## <a name="deploy-and-run-hello-sample-application"></a>Implementar y ejecutar la aplicación de ejemplo de Hola
Implementar y ejecutar la aplicación de ejemplo de Hola en Edison ejecutando Hola siguiente comando:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Compruebe que la aplicación de ejemplo de Hola funciona
Debería ver Hola LED que está conectado tooEdison parpadea cada dos segundos. Cada vez que Hola LED parpadea, aplicación de ejemplo de Hola envía un centro de IoT tooyour de mensaje y comprueba que ese mensaje Hola se ha enviado correctamente tooyour centro de IoT. Además, cada mensaje recibido por el centro de IoT Hola se imprime en la ventana de la consola de Hola. aplicación de ejemplo de Hola finaliza automáticamente después de enviar 20 mensajes.

![Aplicación de ejemplo con mensajes enviados y recibidos][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Resumen
Se ha implementado y ejecutar nueva aplicación de ejemplo de intermitencia hello en Edison centro de IoT de tooyour toosend mensajes del dispositivo a la nube. Ahora, supervisar los mensajes tal y como se escriben toohello cuenta de almacenamiento.

## <a name="next-steps"></a>Pasos siguientes
[Lectura de los mensajes que se conservan en Azure Storage][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run_c.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-c-lesson3-read-table-storage.md