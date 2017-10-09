---
title: aaaUse un tooconnect de puerta de enlace de IoT un centro de IoT de dispositivo tooAzure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Intel NUC como un tooconnect de puerta de enlace de IoT un SensorTag de TI y envío sensor datos tooAzure centro de IoT en hello en la nube."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: puerta de enlace de IOT conectar dispositivo toocloud
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a>Usar IoT puerta de enlace tooconnect cosas toohello cloud - SensorTag tooAzure centro de IoT

> [!NOTE]
> Antes de empezar este tutorial, asegúrese de haber completado [Set up Intel NUC as an IoT gateway (Configurar Intel NUC como una puerta de enlace de IoT)](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md). En [configurar Intel NUC como una puerta de enlace de IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), configura Hola Intel NUC dispositivo como una puerta de enlace de IoT.

## <a name="what-you-will-learn"></a>Lo qué aprenderá

Aprenderá cómo toouse una tooconnect de puerta de enlace de IoT un centro de IoT de tooAzure Texas instrumentos SensorTag (CC2650STK). puerta de enlace de IoT Hola envía temperatura y recopilan los datos de humedad de hello SensorTag tooAzure centro de IoT.

## <a name="what-you-will-do"></a>Lo que hará

- Cree un Centro de IoT.
- Registrar un dispositivo en el centro de IoT de Hola para hello SensorTag.
- Habilitar conexión Hola entre la puerta de enlace de IoT de Hola y Hola SensorTag.
- Ejecute un centro de IoT Bilitar ejemplo aplicación toosend SensorTag datos tooyour.

## <a name="what-you-need"></a>Lo que necesita

- Tutorial [Set up Intel NUC as an IoT gateway (Configurar Intel NUC como una puerta de enlace de IoT)](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completado en el que haya configurado Intel NUC como una puerta de enlace de IoT.
- * Una suscripción de Azure activa. Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.
- Un cliente de SSH que se ejecute en el equipo host. En Windows se recomienda PuTTY. Linux y macOS ya vienen con un cliente de SSH.
- dirección IP de Hola y Hola username y password tooaccess Hola puerta de enlace de cliente de SSH Hola.
- Una conexión a Internet.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> Aquí se registra este nuevo dispositivo para el SensorTag

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a>Habilitar conexión Hola entre la puerta de enlace de IoT de Hola y Hola SensorTag

En esta sección, realizar Hola siguientes tareas:

- Obtener dirección MAC de Hola de hello SensorTag conexión Bluetooth.
- Iniciar una conexión de Bluetooth de toohello de puerta de enlace de IoT de hello SensorTag.

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a>Obtener dirección MAC de Hola de hello SensorTag para conexión de Bluetooth

1. En el equipo de host de hello, ejecutar el cliente de SSH de Hola y conectar la puerta de enlace de IoT toohello.
1. Desbloquear Bluetooth ejecutando Hola siguiente comando:

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. Iniciar el servicio de Bluetooth de hello en la puerta de enlace de IoT de Hola y escriba un tooconfigure de shell de Bluetooth Bluetooth ejecutando Hola siguientes comandos:

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. Encendido de controlador de Bluetooth Hola ejecutando Hola siguiente comando en hello Bluetooth shell:

   ```bash
   power on
   ```

   ![encendido de controlador de Bluetooth hello en puerta de enlace de IoT de hello con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. Iniciar buscar dispositivos Bluetooth cercanos ejecutando Hola siguiente comando:

   ```bash
   scan on
   ```

   ![Buscar dispositivos Bluetooth cercanos con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. Presione el botón en hello SensorTag de emparejamiento de Hola. Hola verde LED en hello SensorTag parpadea.
1. En el shell de Bluetooth hello, debería ver Hola que sensortag se encuentra. Tome nota de hello dirección MAC de hello SensorTag. En este ejemplo, hello dirección MAC de hello SensorTag es `24:71:89:C0:7F:82`.
1. Desactivar el examen de hello ejecutando el siguiente comando de hello:

   ```bash
   scan off
   ```

   ![Detener la detección de dispositivos Bluetooth cercanos con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a>Iniciar una conexión de Bluetooth de toohello de puerta de enlace de IoT de hello SensorTag

1. Conectarse toohello SensorTag, ejecute el siguiente comando de hello:

   ```bash
   connect <MAC address>
   ```

   ![Conectar toohello SensorTag con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. Desconectarse de hello SensorTag y ejecutar salir del shell de Bluetooth Hola Hola siguientes comandos:

   ```bash
   disconnect
   exit
   ```

   ![Desconectarse de hello SensorTag con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

Conexión Hola entre la puerta de enlace de IoT de Hola y Hola SensorTag haya habilitado correctamente.

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a>Ejecutar un centro de IoT Bilitar ejemplo aplicación toosend SensorTag datos tooyour

Borde de IoT de Azure proporciona Hola aplicación de ejemplo de Bluetooth baja energía (n). aplicación de ejemplo de Hola recopila datos de conexión Bilitar y centro de IoT de hello datos tooyou de envío. aplicación de ejemplo de Hola toorun, debe:

1. Configurar la aplicación de ejemplo de Hola.
1. Ejecutar la aplicación de ejemplo de Hola en puerta de enlace de IoT Hola.

### <a name="configure-hello-sample-application"></a>Configurar la aplicación de ejemplo de Hola

1. Vaya toohello carpeta de aplicación de ejemplo de Hola ejecutando Hola siguiente comando:

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. Abra el archivo de configuración de hello ejecutando Hola siguiente comando:

   ```bash
   vi ble_gateway.json
   ```

1. En el archivo de configuración de hello, rellene Hola siguientes valores:

   **IoTHubName**: nombre de Hola de su centro de IoT.

   **IoTHubSuffix**: IoTHubSuffix obtener de la clave principal Hola de cadena de conexión de dispositivo de Hola que anotó hacia abajo. Asegurarse de que obtener la clave principal de Hola de cadena de conexión de dispositivo de hello, no Hola clave principal de la cadena de conexión de base de datos central de IoT. clave principal de Hola de cadena de conexión de dispositivo de hello está en formato de Hola de `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.

   **Transporte**: valor predeterminado de hello es `amqp`. Este valor muestra el protocolo de Hola durante transpotation. Podría ser `http`, `amqp` o `mqtt`.

   **macAddress**: Hola dirección MAC de hello SensorTag que anotó hacia abajo.

   **Id. de dispositivo**: Id. de dispositivo de Hola que creó en el centro de IoT.

   **deviceKey**: clave principal de Hola de cadena de conexión de dispositivo de Hola.

   ![Archivo de configuración de hello completa del programa Hola a aplicación de ejemplo BLE](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. Presione `ESC` y el tipo de `:wq` archivo de hello toosave.

### <a name="run-hello-sample-application"></a>Ejecutar la aplicación de ejemplo de Hola

1. Asegúrese de hello seguro que sensortag está encendida.
1. Ejecute el siguiente comando de hello:

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Pasos siguientes

[Usar la puerta de enlace de IoT para la transformación de datos de sensor con Azure IoT Edge](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
