---
title: "Preguntas más frecuentes sobre la fábrica conectada a Conjunto de aplicaciones de IoT de Azure | Microsoft Docs"
description: "Preguntas más frecuentes sobre la fábrica conectada a Conjunto de aplicaciones de IoT"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 35cf824210a14410d7ea2aedddde0040309901f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions-for-iot-suite-connected-factory-preconfigured-solution"></a>Preguntas más frecuentes sobre la solución preconfigurada de fábrica conectada a Conjunto de aplicaciones de IoT

Consulte, además, las [preguntas más frecuentes](iot-suite-faq.md) sobre Conjunto de aplicaciones de IoT.

### <a name="where-can-i-find-the-source-code-for-the-preconfigured-solution"></a>¿Dónde se puede encontrar el código fuente de la solución preconfigurada?

El código fuente se almacena en el siguiente repositorios de GitHub:

* [Solución preconfigurada de fábrica conectada](https://github.com/Azure/azure-iot-connected-factory)

### <a name="what-is-opc-ua"></a>¿Qué es OPC UA?

OPC Unified Architecture (UA), publicado en 2008, es un estándar de interoperabilidad independiente de plataforma y orientado a servicios. OPC UA se usa en diversos sistemas industriales y dispositivos como equipos, PLC y sensores del sector. OPC UA integra la funcionalidad de las especificaciones de OPC Classic en un solo marco extensible con seguridad integrada. Es un estándar controlado por OPC Foundation. [OPC Foundation](http://opcfoundation.org/) es una organización sin ánimo de lucro con más de 440 miembros. El objetivo de la organización es usar la especificación OPC para facilitar la interoperabilidad multiproveedor, multiplataforma, segura y confiable gracias a lo siguiente:

* Infraestructura
* Especificaciones
* Technology
* Procesos

### <a name="why-did-microsoft-choose-opc-ua-for-the-connected-factory-preconfigured-solution"></a>¿Por qué Microsoft ha elegido a OPC UA para la solución preconfigurada de fábrica conectada?

Microsoft ha elegido OPC UA porque es un estándar abierto, independiente de la plataforma, no es de propiedad, es reconocido por el sector y está probado. Es un requisito para las soluciones de arquitectura de referencia de Industrie 4.0 (RAMI4.0), que garantiza la interoperabilidad entre un amplio conjunto de procesos y equipos de fabricación. Microsoft ha detectado una demanda por parte de sus clientes para crear soluciones de Industrie 4.0. La compatibilidad con OPC UA ayuda a reducir las barreras para que los clientes puedan lograr sus objetivos y les proporciona un valor de negocio inmediato.

### <a name="how-do-i-add-a-public-ip-address-to-the-simulation-vm"></a>¿Cómo se agrega una dirección IP pública a la máquina virtual de simulación?

Tiene dos opciones para agregar la dirección IP:

* Usar el script de PowerShell `Simulation/Factory/Add-SimulationPublicIp.ps1` en el [repositorio](https://github.com/Azure/azure-iot-connected-factory). Pase el nombre de la implementación como un parámetro. Para una implementación local, use `<your username>ConnFactoryLocal`. El script imprime la dirección IP de la máquina virtual.

* En Azure Portal, busque el grupo de recursos de la implementación. Excepto para una implementación local, el grupo de recursos tiene el nombre especificado como nombre de solución o de implementación. Para una implementación local mediante el script de compilación, el nombre del grupo de recursos es `<your username>ConnFactoryLocal`. Ahora agregue un nuevo recurso de la **dirección IP pública** al grupo de recursos.

> [!NOTE]
> En cualquier caso, asegúrese de instalar las revisiones más recientes; para ello, siga las instrucciones que aparecen el [sitio web de Ubuntu](https://wiki.ubuntu.com/Security/Upgrades). Mantenga la instalación actualizada siempre que la máquina virtual sea accesible a través de una dirección IP pública.

### <a name="how-do-i-remove-the-public-ip-address-to-the-simulation-vm"></a>¿Cómo se quita una dirección IP pública de la máquina virtual de simulación?

Tiene dos opciones para quitar la dirección IP:

* Use el script de PowerShell Simulation/Factory/Remove-SimulationPublicIp.ps1 del [repositorio](https://github.com/Azure/azure-iot-connected-factory). Pase el nombre de la implementación como un parámetro. Para una implementación local, use `<your username>ConnFactoryLocal`. El script imprime la dirección IP de la máquina virtual.

* En Azure Portal, busque el grupo de recursos de la implementación. Excepto para una implementación local, el grupo de recursos tiene el nombre especificado como nombre de solución o de implementación. Para una implementación local mediante el script de compilación, el nombre del grupo de recursos es `<your username>ConnFactoryLocal`. Quite ahora el recurso de la **dirección IP pública** del grupo de recursos.

### <a name="how-do-i-sign-in-to-the-simulation-vm"></a>¿Cómo se inicia sesión en la máquina virtual de simulación?

Solo se admite el inicio de sesión en la máquina virtual de simulación si ha implementado la solución con el script de PowerShell `build.ps1` en el [repositorio](https://github.com/Azure/azure-iot-connected-factory).

Si ha implementado la solución de www.azureiotsuite.com, no puede iniciar sesión en la máquina virtual. No se puede iniciar sesión porque la contraseña se genera aleatoriamente y no se puede restablecer.

1. Agregue una dirección IP pública a la máquina virtual. Consulte [¿Cómo se agrega una dirección IP pública a la máquina virtual de simulación](#how-do-i-remove-the-public-ip-address-to-the-simulation-vm)
1. Cree una sesión de SSH para la máquina virtual con la dirección IP de la máquina virtual.
1. Es el nombre de usuario que se va a utilizar es: `docker`.
1. La contraseña que se utilice depende de la versión que se usó en la implementación:
    * Para las soluciones implementadas con el script build.ps1 antes del 1 de junio de 2017, la contraseña es: `Passw0rd`.
    * Para las soluciones implementadas con el script build.ps1 después del 1 de junio de 2017, la contraseña es: `<name of your deployment>.config.user`. La contraseña se almacena en el valor **VmAdminPassword**. La contraseña se genera aleatoriamente durante la implementación a menos que la especifique con el parámetro `-VmAdminPassword` del script `build.ps1`.

### <a name="how-do-i-stop-and-start-all-docker-processes-in-the-simulation-vm"></a>¿Cómo se puede detener e iniciar todos los procesos de docker en la máquina virtual de simulación?

1. Inicie sesión en la máquina virtual de simulación. Consulte [¿Cómo se inicia sesión en la máquina virtual de simulación?](#how-do-i-sign-in-to-the-simulation-vm)
1. Para comprobar qué contenedores están activos, ejecute: `docker ps`.
1. Para detener todos los contenedores de simulación, ejecute: `./stopsimulation`.
1. Para iniciar todos los contenedores de simulación:
    * Exporte una variable de shell con el nombre **IOTHUB_CONNECTIONSTRING**. Utilice el valor de la configuración **IotHubOwnerConnectionString** en el archivo `<name of your deployment>.config.user`. Por ejemplo:

        ```
        export IOTHUB_CONNECTIONSTRING="HostName={yourdeployment}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={your key}"
        ```

    * Ejecute `./startsimulation`.

### <a name="how-do-i-update-the-simulation-in-the-vm"></a>¿Cómo se actualiza la simulación en la máquina virtual?

Si ha realizado algún cambio en la simulación, puede usar el script de PowerShell `build.ps1` en el [repositorio](https://github.com/Azure/azure-iot-connected-factory) mediante el comando `updatedimulation`. Este script crea todos los componentes de simulación, detiene la simulación en la máquina virtual, realiza la carga, la instalación y los inicia.

### <a name="how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution"></a>¿Cómo se puede averiguar la cadena de conexión de IoT Hub utilizada por la solución?

Si ha implementado la solución con el script `build.ps1` en el [repositorio](https://github.com/Azure/azure-iot-connected-factory), la cadena de conexión es el valor de **IotHubOwnerConnectionString** en el archivo `<name of your deployment>.config.user`.

También puede encontrar la cadena de conexión mediante Azure Portal: En el recurso de IoT Hub del grupo de recursos de la implementación, busque el valor de la cadena de conexión.

### <a name="which-iot-hub-devices-does-the-connected-factory-simulation-use"></a>¿Qué dispositivos de IoT Hub usa la simulación de fábrica conectada?

La misma simulación registra los siguientes dispositivos:

* proxy.beijing.corp.contoso
* proxy.capetown.corp.contoso
* proxy.mumbai.corp.contoso
* proxy.munich0.corp.contoso
* proxy.rio.corp.contoso
* proxy.seattle.corp.contoso
* publisher.beijing.corp.contoso
* publisher.capetown.corp.contoso
* publisher.mumbai.corp.contoso
* publisher.munich0.corp.contoso
* publisher.rio.corp.contoso
* publisher.seattle.corp.contoso

Mediante la herramienta [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) o [iothub-explorer](https://github.com/azure/iothub-explorer), puede comprobar qué dispositivos están registrados en la instancia IoT Hub que usa la solución. Para usar estas herramientas, necesita la cadena de conexión para la instancia de IoT Hub de la implementación.

### <a name="how-can-i-get-log-data-from-the-simulation-components"></a>¿Cómo se pueden obtener datos de registro de los componentes de simulación?

Todos los componentes de la simulación registran información en los archivos de registro. Estos archivos pueden encontrarse en la máquina virtual, en la carpeta `home/docker/Logs`. Para recuperar los registros, puede usar el script de PowerShell `Simulation/Factory/Get-SimulationLogs.ps1` en el [repositorio](https://github.com/Azure/azure-iot-connected-factory).

Este script debe iniciar sesión en la máquina virtual. Debe proporcionar credenciales para el inicio de sesión. Consulte [¿Cómo se inicia sesión en la máquina virtual de simulación?](#how-do-i-sign-in-to-the-simulation-vm) para buscar las credenciales.

El script agrega o quita una dirección IP pública en la máquina virtual, si todavía no tiene una y la quita. El script coloca todos los archivos de registro en un archivo y lo descarga en la estación de trabajo de desarrollo.

También puede iniciar sesión en la máquina virtual a través de SSH e inspeccionar los archivos de registro en tiempo de ejecución.

### <a name="how-can-i-check-if-the-simulation-is-sending-data-to-the-cloud"></a>¿Cómo puedo comprobar si la simulación envía datos a la nube?

Con la herramienta [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) o [iothub-explorer](https://github.com/azure/iothub-explorer), puede inspeccionar los datos enviados a IoT Hub desde determinados dispositivos. Para usar estas herramientas, tiene que saber la cadena de conexión para la instancia de IoT Hub de la implementación. Consulte [¿Cómo se puede averiguar la cadena de conexión de IoT Hub utilizada por la solución?](#how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution)

Inspeccione los datos enviados por uno de los dispositivos del editor:

* publisher.beijing.corp.contoso
* publisher.capetown.corp.contoso
* publisher.mumbai.corp.contoso
* publisher.munich0.corp.contoso
* publisher.rio.corp.contoso
* publisher.seattle.corp.contoso

Si ve que ningún dato se envía a IoT Hub, hay un problema con la simulación. Como primer paso de análisis debe analizar los archivos de registro de los componentes de la simulación. Consulte [¿Cómo se pueden obtener datos de registro de los componentes de simulación?](#how-can-i-get-log-data-from-the-simulation-components) Ahora, pruebe a detener e iniciar la simulación, y, si todavía no hay datos enviados, actualice completamente la simulación. Consulte [¿Cómo se actualiza la simulación en la máquina virtual?](#how-do-i-update-the-simulation-in-the-vm)

### <a name="next-steps"></a>Pasos siguientes

También puede explorar algunas de las demás características y funcionalidades de las soluciones preconfiguradas del conjunto de aplicaciones de IoT:

* [Información general de la solución preconfigurada de mantenimiento predictivo](iot-suite-predictive-overview.md)
* [Introducción a la solución preconfigurada de fábrica conectada](iot-suite-connected-factory-overview.md)
* [Seguridad de Internet de las cosas desde el principio](securing-iot-ground-up.md)