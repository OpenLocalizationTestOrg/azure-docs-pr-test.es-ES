---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 2: Registro del dispositivo | Microsoft Docs"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot hub, nube de internet de las cosas, dispositivo de creación de azure iot hub, sensortag de ti, ble de ti"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5d2322268aa18f52f60c2833778323773ac4eec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a>Creación de una instancia de Azure IoT Hub y registro del dispositivo

## <a name="what-you-will-do"></a>Lo que hará

- Crear un grupo de recursos
- Crear su primera instancia de IoT Hub
- Registre el dispositivo en el centro de IoT mediante Hola CLI de Azure. 

Al registrar el dispositivo en el centro de IoT, Hola servicio del centro de IoT de Azure genera una clave para su tooauthenticate toouse de dispositivo con el servicio de Hola. 

Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá

En esta lección, aprenderá lo siguiente:

- ¿Cómo toouse Hola toocreate de CLI de Azure de un centro de IoT.
- ¿Cómo tooregister un dispositivo en un centro de IoT.

## <a name="what-you-need"></a>Lo que necesita

- Una suscripción de Azure activa. Si no tiene ninguna cuenta de Azure, puede crear una [cuenta de evaluación gratuita de Azure](http://azure.microsoft.com/pricing/free-trial/) en solo unos minutos.
- Debe tener Hola que CLI de Azure instalado.

## <a name="create-an-iot-hub"></a>Crear un centro de IoT

toocreate un centro de IoT, siga estos pasos:

1. Inicie sesión en tooyour cuenta de Azure ejecutando el siguiente comando de hello:

   ```bash
   az login
   ```

   Una vez que se haya iniciado sesión correctamente, se mostrarán todas las suscripciones disponibles.

2. Establezca el valor predeterminado de hello suscripción de Azure que quiere toouse, ejecute hello siguiente comando:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`puede encontrarse en la salida de hello de hello `az login` o hello `az account list` comando.

3. Registrar un proveedor Hola ejecutando el siguiente comando de Hola. Los proveedores de recursos son servicios que proporcionan recursos para la aplicación. Debe registrar proveedor de Hola para poder implementar Hola recursos de Azure que Hola ofertas de proveedor.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. Cree un grupo de recursos denominado `iot-gateway` en región del oeste de Estados Unidos de Hola ejecutando el siguiente comando de hello:

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   `westus`es la ubicación de hello crear el grupo de recursos. Si desea toouse en otra ubicación, puede ejecutar `az account list-locations -o table` toosee todos Hola ubicaciones de Azure admite.

5. Crear un centro de IoT en hello `iot-gateway` grupo de recursos mediante la ejecución de hello siguiente comando:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

De forma predeterminada, herramienta de hello crea un centro de IoT en el nivel de precios de Hola. Para más información, consulte los [precios de Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> nombre de Hola de su centro de IoT debe ser único globalmente. Solo puede crear una edición F1 de Azure IoT Hub en su suscripción de Azure.

## <a name="register-your-device-in-your-iot-hub"></a>Registro del dispositivo en IoT Hub

Cada dispositivo que envía el centro de IoT tooyour de mensajes y recibe mensajes desde el centro de IoT debe estar registrado con un identificador único.
Registre el dispositivo en IoT Hub ejecutando el comando siguiente:

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a>Resumen

Ha creado una instancia de IoT Hub y ha registrado en ella el dispositivo local con una identidad de dispositivo. Ya está listo toolearn cómo tooconfigure y ejecutar una puerta de enlace ejemplo aplicación toosend de datos desde el centro de IoT de dispositivo físico tooyour Hola en la nube.

## <a name="next-steps"></a>Pasos siguientes
[Configuración y ejecución de la aplicación de ejemplo BLE](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)