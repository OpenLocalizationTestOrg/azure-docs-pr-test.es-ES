---
title: "Conectar Arduino tooAzure IoT - lección 2: registrar el dispositivo | Documentos de Microsoft"
description: Crear un grupo de recursos, crear un centro de IoT de Azure y registrar Adafruit compacto M0 Wi-Fi en el centro de IoT de Azure de hello mediante Hola CLI de Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "conexión arduino toocloud, centro de iot de azure, internet de nube de cosas, centro de iot de azure crear un dispositivo, arduino en la nube"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 5edc690b-7a1d-4ebc-b011-ff27bfffe6e8
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ca362f9c143dd3a98bf47a66b63a9725a0ffc2d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a>Creación de una instancia de IoT Hub de Azure y registro de Adafruit Feather M0 WiFi

## <a name="what-you-will-do"></a>Lo que hará
* Cree un grupo de recursos.
* Crear el centro de IoT de Azure en el grupo de recursos de Hola.
* Agregar el centro de IoT de Azure de Arduino panel toohello mediante hello Azure interfaz de línea de comandos (CLI de Azure).

Cuando usas hello Azure CLI tooadd su centro de IoT Arduino panel tooyour, servicio de hello genera una clave para su tooauthenticate de panel Arduino con el servicio de Hola. Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshoot].

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:
* ¿Cómo toouse Hola toocreate de CLI de Azure de un centro de IoT.
* ¿Cómo toocreate una identidad de dispositivo para su Arduino del panel en el centro de IoT.

## <a name="what-you-need"></a>Lo que necesita
* Una cuenta de Azure
* Un equipo con hello CLI de Azure instalado

## <a name="create-your-iot-hub"></a>Creación de un centro de IoT Hub
IoT Hub de Azure ayuda a conectar, supervisar y administrar millones de activos de IoT. toocreate su centro de IoT, siga estos pasos:

1. Inicie sesión en tooyour cuenta de Azure ejecutando el siguiente comando de hello:

   ```bash
   az login
   ```

   Una vez que la sesión se ha iniciado correctamente, aparecen todas las suscripciones disponibles.

2. Establecer suscripción predeterminada de Hola que desea toouse ejecutando el siguiente comando de hello:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`puede encontrarse en la salida de hello de hello `az login` o hello `az account list` comando.

3. Registrar un proveedor Hola ejecutando el siguiente comando de Hola. Los proveedores de recursos son servicios que proporcionan recursos para la aplicación. Debe registrar proveedor de Hola para poder implementar Hola recursos de Azure que Hola ofertas de proveedor.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. Crear un grupo de recursos denominado ejemplo iot en región del oeste de Estados Unidos de hello ejecutando Hola siguiente comando:

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus`es la ubicación de hello crear el grupo de recursos. Si desea toouse en otra ubicación, puede ejecutar `az account list-locations -o table` toosee todos Hola ubicaciones de Azure admite.

5. Crear un centro de IoT en grupo de recursos de ejemplo de iot de hello ejecutando Hola siguiente comando:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

De forma predeterminada, herramienta de hello crea un centro de IoT en el nivel de precios de Hola. Para más información, consulte los [precios de Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> nombre de Hola de su centro de IoT debe ser único globalmente.
> Solamente puede crear una edición F1 de Azure IoT Hub en la suscripción de Azure.

## <a name="register-your-arduino-board-in-your-iot-hub"></a>Registro de la placa de Arduino en el centro de IoT Hub
Cada dispositivo que envía el centro de IoT tooyour de mensajes y recibe mensajes desde el centro de IoT debe estar registrado con un identificador único.

Registre la placa de Arduino en su instancia de IoT Hub ejecutando el comando siguiente:

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a>Resumen
Ha creado un centro de IoT Hub y ha registrado la placa de Arduino con una identidad de dispositivo en este centro de IoT Hub. Ya está listo toolearn cómo toosend mensajes desde el centro de IoT Arduino tooyour de panel.

## <a name="next-steps"></a>Pasos siguientes
[Crear una aplicación de Azure de función y un centro de IoT de almacenamiento de Azure cuenta tooprocess y el almacén de mensajes][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md