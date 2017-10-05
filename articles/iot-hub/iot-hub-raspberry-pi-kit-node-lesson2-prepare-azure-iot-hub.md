---
featureFlags: usabilla
title: "Conexión de Raspberry Pi (Node) a Azure IoT: Lección 2: Registro del dispositivo | Microsoft Docs"
description: Cree un grupo de recursos, cree un centro de IoT Hub de Azure y registre Pi en este centro mediante la CLI de Azure.
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
ms.openlocfilehash: 774f9356d7a11b2c61905ada75bed92d44e5fc0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a>Creación de un centro de IoT y registro de Raspberry Pi 3
## <a name="what-you-will-do"></a>Lo que hará
* Cree un grupo de recursos.
* Cree una instancia de IoT Hub de Azure en el grupo de recursos.
* Agregue Raspberry Pi 3 al centro de Azure IoT Hub mediante la interfaz de la línea de comandos de Azure (CLI de Azure).

Si utiliza la CLI de Azure para agregar Pi al centro de IoT Hub, el servicio generará una clave para autenticar Pi en el servicio. Si tiene problemas, puede encontrar soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:
* Uso de la CLI de Azure para crear un centro de IoT Hub
* Creación de una identidad de dispositivos para Pi en IoT Hub

## <a name="what-you-need"></a>Lo que necesita
* Una cuenta de Azure
* Un equipo Mac o un equipo Windows con la CLI de Azure instalada

## <a name="create-your-iot-hub"></a>Creación de un centro de IoT Hub
IoT Hub de Azure ayuda a conectar, supervisar y administrar millones de activos de IoT. Para crear el centro de IoT Hub, siga estos pasos:

1. Inicie sesión en la cuenta de Azure mediante el siguiente comando:

   ```bash
   az login
   ```

   Una vez que la sesión se ha iniciado correctamente, aparecen todas las suscripciones disponibles.

2. Establezca la suscripción predeterminada que desea usar mediante el siguiente comando:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   El valor de `subscription ID or name` puede verse en la salida del comando `az login` o del comando `az account list`.

3. Registre el proveedor con el siguiente comando. Los proveedores de recursos son servicios que proporcionan recursos para la aplicación. Debe registrar el proveedor para poder implementar el recurso de Azure que este le ofrece.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. Cree un grupo de recursos denominado "iot-sample" en la región oeste de EE. UU. ejecutando el comando siguiente:

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus` es la ubicación en la que se crea el grupo de recursos. Si desea utilizar otra ubicación, puede ejecutar `az account list-locations -o table` para ver todas las ubicaciones admitidas por Azure.
 
5. Cree una instancia de IoT Hub en el grupo de recursos iot-sample ejecutando el comando siguiente:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   De forma predeterminada, la herramienta crea la instancia de IoT Hub con el plan de tarifa Gratis. Para más información, consulte los [precios de Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE] 
> El nombre de su instancia de IoT Hub debe única globalmente. Solamente puede crear una edición F1 de Azure IoT Hub en la suscripción de Azure.

## <a name="register-pi-in-your-iot-hub"></a>Registro de Pi en el centro de IoT hub
Todos los dispositivos que envían mensajes al centro de IoT Hub y los reciben de este deben estar registrados con un identificador único. Debe usar la CLI de Azure para registrar Pi y crear un certificado X.509 autofirmado para autenticar el dispositivo.

Ejecute el siguiente comando:

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a>Resumen
Ha creado un centro de IoT Hub y ha registrado Pi con una identidad de dispositivo en este centro. Ya está preparado para aprender a enviar mensajes desde Pi a IoT Hub.

## <a name="next-steps"></a>Pasos siguientes
[Creación de una instancia de Azure Function App y una cuenta de Azure Storage para procesar y almacenar mensajes de IoT Hub](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

