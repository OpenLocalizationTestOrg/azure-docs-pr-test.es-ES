---
title: "aaaAzure IoT Suite conectado generador preguntas más frecuentes | Documentos de Microsoft"
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
ms.openlocfilehash: 4ae9beb0daf1b0578850cd652eaca7635b0d039d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite-connected-factory-preconfigured-solution"></a>Preguntas más frecuentes sobre la solución preconfigurada de fábrica conectada a Conjunto de aplicaciones de IoT

Vea también, Hola general [preguntas más frecuentes sobre](iot-suite-faq.md) para IoT Suite.

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solution"></a>¿Dónde puedo encontrar el código fuente de hello para la solución de hello preconfigurado?

código fuente de Hola se almacena en hello después de repositorio de GitHub:

* [Solución preconfigurada de fábrica conectada](https://github.com/Azure/azure-iot-connected-factory)

### <a name="what-is-opc-ua"></a>¿Qué es OPC UA?

OPC Unified Architecture (UA), publicado en 2008, es un estándar de interoperabilidad independiente de plataforma y orientado a servicios. OPC UA se usa en diversos sistemas industriales y dispositivos como equipos, PLC y sensores del sector. OPC UA integra la funcionalidad de Hola de especificaciones de OPC clásico de hello en un solo marco extensible con seguridad integrada. Es un estándar que se controla mediante Hola Foundation de OPC. Hola [Foundation OPC](http://opcfoundation.org/) es una organización sin ánimo de lucro con más de 440 miembros. objetivo de Hola de organización de hello es toouse OPC especificaciones toofacilitate varios proveedor, multiplataforma, segura y confiable interoperabilidad a través de:

* Infraestructura
* Especificaciones
* Technology
* Procesos

### <a name="why-did-microsoft-choose-opc-ua-for-hello-connected-factory-preconfigured-solution"></a>¿Por qué escogió Microsoft que opc UA para hello conectado solución preconfigurada de fábrica?

Microsoft ha elegido OPC UA porque es un estándar abierto, independiente de la plataforma, no es de propiedad, es reconocido por el sector y está probado. Es un requisito para las soluciones de arquitectura de referencia de Industrie 4.0 (RAMI4.0), que garantiza la interoperabilidad entre un amplio conjunto de procesos y equipos de fabricación. Microsoft detecta la petición de nuestras soluciones de toobuild Industrie 4.0 de los clientes. Compatibilidad con OPC UA ayuda barrera de hello inferior para los clientes tooachieve sus objetivos y proporciona toothem del valor de negocio inmediato.

### <a name="how-do-i-add-a-public-ip-address-toohello-simulation-vm"></a>¿Cómo se agrega una simulación de toohello de dirección IP pública VM?

Tiene dos direcciones IP de opciones tooadd hello:

* Usar script de PowerShell de hello `Simulation/Factory/Add-SimulationPublicIp.ps1` en hello [repositorio](https://github.com/Azure/azure-iot-connected-factory). Pase el nombre de la implementación como un parámetro. Para una implementación local, use `<your username>ConnFactoryLocal`. script de Hola imprime de dirección IP de Hola de hello máquina virtual.

* Hola portal de Azure, busque el grupo de recursos de hello de la implementación. Excepto para una implementación local, el grupo de recursos de hello tiene nombre hello especificado como solución o nombre de la implementación. Para una implementación local mediante el script de compilación de hello, Hola Hola del grupo de recursos se denomina `<your username>ConnFactoryLocal`. Ahora agregue un nuevo **dirección IP pública** el grupo de recursos de toohello.

> [!NOTE]
> En cualquier caso, asegúrese de instalar las últimas revisiones de hello siguiendo las instrucciones de Hola de hello [sitio Web de Ubuntu](https://wiki.ubuntu.com/Security/Upgrades). Mantener instalación Hola seguridad toodate para siempre que la máquina virtual sea accesible a través de una dirección IP pública.

### <a name="how-do-i-remove-hello-public-ip-address-toohello-simulation-vm"></a>¿Cómo se puede quitar Hola pública IP dirección toohello simulación VM?

Tiene dos direcciones IP de opciones tooremove hello:

* Usar script de PowerShell de hello Simulation/Factory/Remove-SimulationPublicIp.ps1 de hello [repositorio](https://github.com/Azure/azure-iot-connected-factory). Pase el nombre de la implementación como un parámetro. Para una implementación local, use `<your username>ConnFactoryLocal`. script de Hola imprime de dirección IP de Hola de hello máquina virtual.

* Hola portal de Azure, busque el grupo de recursos de hello de la implementación. Excepto para una implementación local, el grupo de recursos de hello tiene nombre hello especificado como solución o nombre de la implementación. Para una implementación local mediante el script de compilación de hello, Hola Hola del grupo de recursos se denomina `<your username>ConnFactoryLocal`. Quitar ahora hello **dirección IP pública** recursos del grupo de recursos de Hola.

### <a name="how-do-i-sign-in-toohello-simulation-vm"></a>¿Cómo iniciar sesión toohello simulación VM?

Iniciar sesión en la simulación de toohello VM solo se admite si ha implementado la solución con script de PowerShell de hello `build.ps1` en hello [repositorio](https://github.com/Azure/azure-iot-connected-factory).

Si ha implementado la solución de Hola desde www.azureiotsuite.com, no puede iniciar sesión en toohello máquina virtual. No se puede iniciar sesión, porque la contraseña de Hola se genera aleatoriamente y no puede restablecer.

1. Agregar una toohello de dirección IP virtual pública. ¿Vea [cómo se agrega una simulación de toohello de dirección IP pública VM?](#how-do-i-remove-the-public-ip-address-to-the-simulation-vm)
1. Crear un tooyour de sesión SSH VM utilizando la dirección IP de Hola de hello máquina virtual.
1. Hola toouse de nombre de usuario es: `docker`.
1. Hola contraseña toouse depende de la versión de Hola que usa toodeploy:
    * Para las soluciones implementadas mediante la secuencia de comandos de hello build.ps1 antes de 1 de junio de 2017, contraseña de hello es: `Passw0rd`.
    * Para las soluciones implementadas mediante la secuencia de comandos de hello build.ps1 después del 1 de junio de 2017, encontrará contraseña Hola Hola `<name of your deployment>.config.user` archivo. Hola se guarda en hello **VmAdminPassword** configuración. Hello contraseña se genera aleatoriamente durante la implementación a menos que especifique mediante hello `build.ps1` parámetro de script`-VmAdminPassword`

### <a name="how-do-i-stop-and-start-all-docker-processes-in-hello-simulation-vm"></a>¿Cómo se puede detener e iniciar todos los procesos de docker de simulación de hello VM?

1. Inicie sesión en la simulación de toohello máquina virtual. Vea [¿cómo iniciar sesión toohello simulación VM?](#how-do-i-sign-in-to-the-simulation-vm)
1. toocheck qué contenedores están activas, ejecute: `docker ps`.
1. ejecución de todos los contenedores de simulación, toostop: `./stopsimulation`.
1. toostart todos los contenedores de simulación:
    * Exportar una variable del shell con nombre hello **IOTHUB_CONNECTIONSTRING**. Usar valor Hola de hello **IotHubOwnerConnectionString** en hello `<name of your deployment>.config.user` archivo. Por ejemplo:

        ```
        export IOTHUB_CONNECTIONSTRING="HostName={yourdeployment}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={your key}"
        ```

    * Ejecute `./startsimulation`.

### <a name="how-do-i-update-hello-simulation-in-hello-vm"></a>¿Cómo puedo actualizar simulación de Hola Hola VM?

Si ha realizado algún cambio toohello simulación, puede usar script de PowerShell de hello `build.ps1` en hello [repositorio](https://github.com/Azure/azure-iot-connected-factory) con hello `updatedimulation` comando. Este script genera todos los componentes de simulación de hello, detiene la simulación de Hola Hola VM, carga, instala e inicia.

### <a name="how-do-i-find-out-hello-connection-string-of-hello-iot-hub-used-by-my-solution"></a>¿Cómo puede averiguar la cadena de conexión de Hola de centro de IoT Hola utilizado por mi solución?

Si ha implementado la solución con hello `build.ps1` secuencia de comandos de hello [repositorio](https://github.com/Azure/azure-iot-connected-factory), cadena de conexión de hello es el valor de Hola de **IotHubOwnerConnectionString** en hello `<name of your deployment>.config.user` archivo.

También puede encontrar la cadena de conexión de hello con hello portal de Azure. Hola recursos del centro de IoT Hola grupo de recursos de la implementación, busque configuración hello de la cadena de conexión.

### <a name="which-iot-hub-devices-does-hello-connected-factory-simulation-use"></a>¿Los dispositivos del centro de IoT Hola uso de simulación de fábrica conectado?

Hola simulación en sí mismo registra Hola siguientes dispositivos:

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

Con hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) o [el centro de IOT explorador](https://github.com/azure/iothub-explorer) herramienta, puede comprobar qué dispositivos están registrados en el centro de IoT Hola está usando la solución. toouse estas herramientas, debe cadena de conexión de hello para el centro de IoT de hello en su implementación.

### <a name="how-can-i-get-log-data-from-hello-simulation-components"></a>¿Cómo se puede obtener datos de registro de componentes de simulación de hello?

Todos los componentes de la información de registro de simulación de hello en archivos de toolog. Estos archivos pueden encontrarse en hello VM en la carpeta de hello `home/docker/Logs`. registros de hello tooretrieve, puede usar script de PowerShell de hello `Simulation/Factory/Get-SimulationLogs.ps1` en hello [repositorio](https://github.com/Azure/azure-iot-connected-factory).

Esta secuencia de comandos debe toosign en toohello máquina virtual. Deberá tooprovide credenciales para el inicio de sesión Hola. Vea [¿cómo iniciar sesión toohello simulación VM?](#how-do-i-sign-in-to-the-simulation-vm) las credenciales de hello toofind.

script de Hola agrega o quita un toohello de dirección IP pública de máquina virtual, si todavía no tiene uno y lo quita. script de Hola coloca todos los archivos de registro en un archivo y las descargas de estación de trabajo de desarrollo de hello archivo tooyour.

O bien, inicie sesión en toohello máquina virtual a través de SSH e inspeccionar los archivos de registro de hello en tiempo de ejecución.

### <a name="how-can-i-check-if-hello-simulation-is-sending-data-toohello-cloud"></a>¿Cómo puedo comprobar si simulación de hello está enviando datos toohello en la nube?

Con hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) o hello [el centro de IOT explorador](https://github.com/azure/iothub-explorer) herramienta, puede inspeccionar los datos de hello enviados tooIoT concentrador de determinados dispositivos. toouse estas herramientas, debe tooknow cadena de conexión de hello para el centro de IoT de Hola en su implementación. Vea [¿cómo saber cadena de conexión de Hola de centro de IoT Hola utilizado por mi solución?](#how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution)

Inspeccionar los datos de hello enviados por uno de los dispositivos de hello publicador:

* publisher.beijing.corp.contoso
* publisher.capetown.corp.contoso
* publisher.mumbai.corp.contoso
* publisher.munich0.corp.contoso
* publisher.rio.corp.contoso
* publisher.seattle.corp.contoso

Si no ve ningún dato enviar tooIoT concentrador, a continuación, hay un problema con la simulación de Hola. Como primer paso de análisis debe analizar los archivos de registro de hello de componentes de simulación de Hola. Vea [¿cómo puedo obtener datos de registro de hello componentes de simulación?](#how-can-i-get-log-data-from-the-simulation-components) A continuación, intente toostop, iniciar la simulación de Hola y si todavía no hay ningún dato que se envían, actualice simulación de hello completamente. ¿Vea [cómo actualizar simulación de Hola Hola VM?](#how-do-i-update-the-simulation-in-the-vm)

### <a name="next-steps"></a>Pasos siguientes

También puede explorar algunas de hello otras características y capacidades de hello IoT preconfigurado soluciones:

* [Información general de la solución preconfigurada de mantenimiento predictivo](iot-suite-predictive-overview.md)
* [Introducción a la solución preconfigurada de fábrica conectada](iot-suite-connected-factory-overview.md)
* [Seguridad de IoT de hello masa](securing-iot-ground-up.md)
