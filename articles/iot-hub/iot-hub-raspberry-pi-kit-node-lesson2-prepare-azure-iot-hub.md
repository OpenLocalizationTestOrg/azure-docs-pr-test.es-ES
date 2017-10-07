---
featureFlags: usabilla
title: "Conectar frambuesa Pi (nodo) tooAzure IoT - lección 2: registrar el dispositivo | Documentos de Microsoft"
description: Crear un grupo de recursos, crear un centro de IoT de Azure y registrar Pi en hello del registro de identidad de centro de IoT mediante la CLI de Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "nube de raspberry pi, conexión a la nube de pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97533298d52d1187c49a4c35ddda922d6e45c87d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a>Creación de un centro de IoT y registro de Raspberry Pi 3
## <a name="what-you-will-do"></a>Lo que hará
* Cree un grupo de recursos.
* Crear el centro de IoT de Azure en el grupo de recursos de Hola.
* Agregar el centro de IoT de Azure de toohello de frambuesa Pi 3 mediante hello Azure interfaz de línea de comandos (CLI de Azure).

Cuando se usa el centro de IoT de Azure CLI tooadd Pi tooyour, servicio de hello genera una clave para tooauthenticate Pi con el servicio de Hola. Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:
* ¿Cómo toouse CLI de Azure toocreate un centro de IoT
* ¿Cómo toocreate una identidad de dispositivo de Pi en el centro de IoT

## <a name="what-you-need"></a>Lo que necesita
* Una cuenta de Azure
* Un equipo Mac o en un equipo Windows con hello CLI de Azure instalado

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
> nombre de Hola de su centro de IoT debe ser único globalmente. Solamente puede crear una edición F1 de Azure IoT Hub en la suscripción de Azure.

## <a name="register-pi-in-your-iot-hub"></a>Registro de Pi en el centro de IoT hub
Cada dispositivo que envía el centro de IoT tooyour de mensajes y recibe mensajes desde el centro de IoT debe estar registrado con un identificador único. Utilizará CLI de Azure tooregister su Pi y crear un certificado autofirmado de X.509 para la autenticación de dispositivo.

Ejecute el siguiente comando de hello:

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a>Resumen
Ha creado un centro de IoT Hub y ha registrado Pi con una identidad de dispositivo en este centro. Ya está listo toolearn cómo toosend mensajes Pi tooyour centro de IoT.

## <a name="next-steps"></a>Pasos siguientes
[Crear una aplicación de Azure de función y una tooprocess de cuenta de almacenamiento de Azure y almacenar mensajes de centro de IoT](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

