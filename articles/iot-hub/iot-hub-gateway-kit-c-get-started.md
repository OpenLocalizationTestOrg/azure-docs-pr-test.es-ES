---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Introducción | Microsoft Docs"
description: "Introducción a la puerta de enlace de IoT Starter Kit, crea el centro de IoT de Azure y conectar el centro de IoT toohello SensorTag y puerta de enlace"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Centro de iot de Azure, puerta de enlace de iot, introducción a Hola internet de las cosas, el Kit de herramientas de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a>Introducción con el kit de inicio de puerta de enlace de IoT mediante un dispositivo SensorTag

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Dispositivo simulado](iot-hub-gateway-kit-c-sim-get-started.md)

En este tutorial, empiece por obtener información sobre fundamentos de hello sobre cómo trabajar con [Starter Kit de puerta de enlace de IoT](https://aka.ms/gateway-kit). Se va a trabajar con NUC de Intel que ejecuta Linux demarcación de viento y hello [SensorTag de TI](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main). Obtendrá información sobre cómo tooseamleesly conectar la nube de toohello de dispositivos mediante el uso de centro de IoT de Azure.

***
**¿Aún no tiene el kit?:** haga clic [aquí](https://aka.ms/gateway-kit). **¿No tiene un dispositivo SensorTag?:**[Empiece con un dispositivo simulado](iot-hub-gateway-kit-c-sim-get-started.md) o [compre un dispositivo SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)
***

## <a name="lesson-1-configure-your-nuc"></a>Lección 1: Configuración de NUC
![Diagrama integral de la lección 1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

En esta lección, configurar NUC de Intel (siguiente unidad de "informática") en hello Kit como una puerta de enlace de IoT de Azure, instalar paquetes de hello borde de IoT de Azure en NUC y ejecutar una funcionalidad de la puerta de enlace de la aplicación tooverify ejemplo Hola.

*Estimado toocomplete de tiempo: 15 minutos*

Vaya demasiado[configurar Intel NUC como una puerta de enlace de IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Lección 2: Creación de la instancia de IoT Hub
![Diagrama integral de la lección 2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

En esta lección, instale herramientas de Hola y el software en el equipo host. A continuación, crear su cuenta de Azure gratuita, aprovisionar el centro de IoT de Azure y crear su primer dispositivo en el centro de IoT Hola.

Complete la lección 1 antes de iniciar esta.

### <a name="get-hello-tools"></a>Obtener herramientas de Hola
Instalar software y herramientas de hello en el equipo host.

*Estimado toocomplete de tiempo: 20 minutos*

Vaya demasiado[obtener herramientas Hola](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>Cree una instancia de IoT Hub y registre el dispositivo
Crear el grupo de recursos, aprovisionar el primer centro de IoT de Azure y agregar el primer centro de IoT de toohello de dispositivo mediante Hola CLI de Azure.

*Estimado toocomplete de tiempo: 10 minutos*

Vaya demasiado[crear un centro de IoT y registrar el dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a>Lección 3: Recibir mensajes de SensorTag y leerlos en IoT Hub
En esta lección, usará configuración de las secuencias de comandos tooautomate hello y ejecución de una aplicación de ejemplo Bilitar en la puerta de enlace. Dichas aplicaciones utiliza una colección de módulos tooaggregate y transformación de datos, procesan los comandos o realizan una serie de tareas relacionadas. Los módulos se comunican entre sí a través de un agente de mensajes. aplicación de ejemplo de Hola tiene un módulo de Bilitar y un módulo de centro de IoT. módulo de Hello Bilitar recibe datos de Bilitar SensorTag. Hola paquetes de módulo de centro de IoT datos Hola reciben y envía el centro de IoT tooyour a través del marco de puerta de enlace de hello proporcionado en el borde de IoT de Azure.

![Diagrama integral de la lección 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a>Configurar y ejecutar la aplicación de ejemplo de Hola BLE
Configurar la conectividad de hello entre SensorTag y la puerta de enlace. A continuación, finalice la configuración de Hola y ejecutar la aplicación de ejemplo de Hola Bilitar.

*Estimado toocomplete de tiempo: 15 minutos*

Vaya demasiado[ejecución hello habilitar y configurar aplicación de ejemplo](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

### <a name="read-messages-from-your-iot-hub"></a>Lectura de mensajes en IoT Hub
Ejecutar código de ejemplo en el host de equipo tooread mensajes desde el centro de IoT.

*Estimado toocomplete de tiempo: 15 minutos*

Vaya demasiado[leer los mensajes de su centro de IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>Lección 4: Guardar mensajes tooAzure el almacenamiento de tabla
Crear una aplicación de Azure de función que obtiene los mensajes entrantes desde el centro de IoT y los escribe tooAzure el almacenamiento de tabla.

![Diagrama integral de la lección 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Creación de una cuenta de Azure Storage y una aplicación de Azure Function
Utilice un toocreate de plantilla de Azure Resource Manager, una aplicación de Azure de función y una cuenta de almacenamiento de Azure.

*Estimado toocomplete de tiempo: 10 minutos*

Vaya demasiado[crear una cuenta de almacenamiento de Azure y la aplicación de Azure (función)](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Lectura de los mensajes que se conservan en Azure Table Storage
Supervisar mensajes de puerta de enlace a la nube de hello tal y como se escriben tooAzure el almacenamiento de tabla.

*Estimado toocomplete de tiempo: 5 minutos*

Vaya demasiado[leer los mensajes de guardado en el almacenamiento de Azure Table](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Solución de problemas
Si tiene problemas durante las lecciones de hello, buscar soluciones en hello [solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md) artículo.

## <a name="explore-more"></a>Explorar más
Visite hello [zona de desarrollador de Kit de puerta de enlace de IoT de Intel](http://software.intel.com/iot/microsoft-azure) toolearn más.
