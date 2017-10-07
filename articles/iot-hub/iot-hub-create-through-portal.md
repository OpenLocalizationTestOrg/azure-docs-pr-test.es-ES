---
title: aaaUse Hola toocreate portal Azure de un centro de IoT | Documentos de Microsoft
description: "Cómo toocreate, administrar y eliminar centros de IoT de Azure a través de hello portal de Azure. Incluye información sobre los niveles de precios, el escalado, la seguridad y la configuración de la mensajería."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a>Crear un centro de IoT con hello portal de Azure

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

En este artículo se describe:

* ¿Cómo toofind Hola servicio del centro de IoT Hola portal de Azure.
* ¿Cómo toocreate y administrar centros de IoT.

## <a name="where-toofind-hello-iot-hub-service"></a>Donde toofind Hola servicio del centro de IoT

Puede encontrar Hola servicio del centro de IoT Hola ubicaciones en el portal de hello siguientes:

* Elija **+ Nuevo** y después **Internet de las cosas**.
* Hola Marketplace, elija **Internet de las cosas**.

## <a name="create-an-iot-hub"></a>Crear un centro de IoT

Puede crear un centro de IoT con hello siguientes métodos:

* Hola **+ nuevo** opción abre una hoja de Hola se muestra en la siguiente captura de pantalla de Hola. Hola pasos para crear el centro de IoT de Hola a través de este método y a través de marketplace de hello son idénticos.
* Hola Marketplace, elija **crear** hoja de hello tooopen se muestra en la siguiente captura de pantalla de Hola.

Hello las secciones siguientes describen Hola varios pasos toocreate un centro de IoT:

### <a name="choose-hello-name-of-hello-iot-hub"></a>Elegir nombre de Hola de centro de IoT Hola

toocreate un centro de IoT, debe asignar un nombre centro de IoT Hola. Este nombre debe ser exclusivo para distinguirlo en todas las instancias de IoT Hub.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a>Elija el nivel de precios de Hola

Puede elegir entre cuatro niveles: **Gratis**, **Estándar 1**, **Estándar 2** y **Estándar S3**. nivel gratis Hola permite sólo 500 toobe dispositivos conectados toohello centro de IoT y sube too8, 000 mensajes al día.

**Estándar S1**: edición de hello S1 de uso para las soluciones de IoT con un gran número de dispositivos que cada uno de ellos genera pequeñas cantidades de datos. Permite que cada unidad de edición de hello S1 un too400, 000 mensajes al día a través de todos los dispositivos conectados.

**Estándar S2**: edición de hello S2 de uso para las soluciones de IoT en el que los dispositivos generar grandes cantidades de datos. Permite que cada unidad de edición de hello S2 un too6 millones de mensajes al día entre todos los dispositivos conectados.

**Estándar S3**: edición de hello S3 de uso para las soluciones de IoT que generan un gran volumen de datos. Permite que cada unidad de edición de S3 Hola un too300 millones de mensajes al día entre todos los dispositivos conectados.

![][4]

> [!NOTE]
> IoT Hub solo permite un único centro gratuito por suscripción de Azure.

### <a name="iot-hub-units"></a>Unidades del Centro de IoT

número de Hello permitido por unidad al día de mensajes depende de nivel de precios de la base de datos central. Por ejemplo, si desea hello toosupport entrada de centro de IoT de 700 000 mensajes, elija dos unidades de nivel de S1.

### <a name="device-toocloud-partitions-and-resource-group"></a>Las particiones toocloud del dispositivo y el grupo de recursos

Puede cambiar el número de Hola de particiones para un centro de IoT. número de particiones de Hello predeterminado es 4, puede elegir un número diferente de la lista desplegable de Hola.

No es necesario tooexplicitly crear un grupo de recursos vacío. Cuando se crea un recurso, puede elegir cualquier toocreate un nuevo o usar un grupo de recursos existente.

![][5]

### <a name="choose-subscription"></a>Elección de la suscripción

Centro de IoT de Azure Hola de listas de cuenta de usuario de las suscripciones de Azure Hola se vincula automáticamente a. Puede elegir el centro de IoT de hello suscripción de Azure tooassociate Hola a.

### <a name="choose-hello-location"></a>Elegir ubicación de Hola

opción de ubicación de Hello proporciona una lista de regiones de Hola donde centro de IoT no está disponible.

### <a name="create-hello-iot-hub"></a>Crear centro de IoT Hola

Una vez completados todos los pasos anteriores, puede crear centro de IoT Hola. Haga clic en **crear** toostart Hola proceso back-end toocreate e implementar centro de IoT Hola con opciones de Hola que haya elegido.

Centro de IoT Hola de unos minutos toocreate puede tardar como tarda toorun de implementación de back-end de hello en los servidores de la ubicación apropiada de Hola.

## <a name="change-hello-settings-of-hello-iot-hub"></a>Cambiar la configuración de Hola de centro de IoT Hola

Puede cambiar configuración de Hola de un centro de IoT existente después de que se crea a partir de la hoja de centro de IoT Hola.

![][8]

**Directivas de acceso compartido**: estas directivas definen los permisos de Hola para dispositivos y servicios tooIoT tooconnect concentrador. Para acceder a estas directivas, haga clic en **Directivas de acceso compartido** en **General**. En esta hoja puede modificar las directivas existentes o agregar una nueva.

### <a name="create-a-policy"></a>Para crear una directiva

* Haga clic en **agregar** tooopen una hoja. Aquí puede escribir el nuevo nombre de directiva de Hola y permisos Hola desea tooassociate con esta directiva, tal y como se muestra en hello siguiente figura:

    Hay varios permisos que se pueden asociar a estas directivas compartidas. Hola **lectura del registro** y **escritura del registro** directivas conceden lectura y el registro de identidad de toohello de derechos de acceso de escritura. Elegir la opción de escritura de hello automáticamente elige Hola lee opción.

    Hola **servicio conectar** directiva concede permiso tooaccess los extremos de servicio como **dispositivo a la nube de recepción**. Hola **dispositivo conectar** directiva concede permisos para enviar y recibir mensajes mediante los puntos de conexión de hello centro de IoT del dispositivo.

* Haga clic en **crear** tooadd este recién creado lista existente de directiva toohello.

![][10]

## <a name="endpoints"></a>Puntos de conexión

Haga clic en **extremos** toodisplay una lista de extremos de centro de IoT de Hola que va a modificar. Hay dos tipos de puntos de conexión: puntos de conexión que se integran en el centro de IoT de Hola y extremos que agregue centro de IoT toohello después de su creación.

![][11]

### <a name="built-in-endpoints"></a>Puntos de conexión integrados

Hay dos puntos de conexión integrados: **toodevice comentarios en la nube** y **eventos**.

* **Toodevice comentarios en la nube** configuración: esta opción no tiene dos subsettings: **tooDevice TTL en la nube** (período de vida) y **tiempo de retención** (en horas) para mensajes de saludo. Cuando el primer crea un centro de IoT, ambas configuraciones tienen valor predeterminado de Hola de una hora. tooadjust estas opciones, utilice los controles deslizantes de Hola o escriba los valores de hello.
* Configuración de **Events** (Eventos): esta configuración tiene distintas opciones secundarias, algunas de solo lectura. Hola lista siguiente describe estas opciones:

  * **Las particiones**: se establece un valor predeterminado cuando se crea el centro de IoT Hola. Puede cambiar Hola número de particiones a través de esta configuración.

  * **Nombre de evento compatible con el centro y el extremo**: cuando se crea el centro de IoT hello, un concentrador de eventos lo creó internamente que puede necesita acceder a toounder determinadas circunstancias. No se pueden personalizar los valores de nombre y el extremo de hello compatible con el concentrador de eventos, pero se puede copiar, haga clic en **copia**.

  * **Tiempo de retención**: establecer tooone día de forma predeterminada, pero puede cambiarlo mediante la lista desplegable de Hola. Este valor está en días para la configuración de dispositivo para la nube de Hola.

  * **Grupos de consumidores**: grupos de consumidores habilitar varios mensajes de tooread lectores independientemente de centro de IoT Hola. Cada Centro de IoT se crea con un grupo de consumidores predeterminado. Sin embargo, puede agregar o eliminar centros de IoT consumidor grupos tooyour con esta configuración.

  > [!NOTE]
  > grupo de consumidores de Hello predeterminado no se pueden modificar ni eliminar.

### <a name="custom-endpoints"></a>Puntos de conexión personalizados

Puede agregar extremos personalizados en el centro de IoT mediante el portal de Hola. De hello **extremos** hoja, haga clic en **agregar** en Hola tooopen superior Hola **Agregar extremo** hoja. Escriba información de hello necesario, a continuación, haga clic en **Aceptar**. El punto de conexión personalizado aparece ahora en hello principal **extremos** hoja.

![][13]

Puede leer más sobre los puntos de conexión personalizados en [Referencia: Puntos de conexión de IoT Hub][lnk-devguide-endpoints].

## <a name="routes"></a>Rutas

Haga clic en **rutas** toomanage cómo centro de IoT envía los mensajes del dispositivo a la nube.

![][14]

Puede agregar el centro de IoT de rutas tooyour haciendo clic en **agregar** en parte superior de Hola de hello **rutas*** hoja, especificar información de hello necesario y haga clic en **Aceptar**. La ruta, a continuación, se muestra en hello principal **rutas** hoja. Puede editar una ruta haciendo clic en él en la lista de Hola de rutas. tooenable una ruta, haga clic en él en la lista de Hola de rutas y establezca hello **habilitado** alternar demasiado**desactivar**. cambio de hello toosave, haga clic en **Aceptar** final Hola de hoja de Hola.

![][15]

## <a name="pricing-and-scale"></a>Precios y escala

Hola de precios de un centro de IoT existente pueden cambiarse a través de hello **precios** configuración con hello siguientes excepciones:

* En la implementación actual de hello, un centro de IoT a una SKU libre no puede cambiar tooone de niveles de hello SKU, de pago, o viceversa.
* Solo puede haber un centro de IoT de nivel gratuito en hello suscripción de Azure.

![][12]

Puede mover de un nivel superior de toolower sólo cuando el número Hola de mensajes enviados a ese día superar la cuota de hello para el nivel inferior de Hola. Por ejemplo, si número Hola de mensajes al día supera 400.000, Hola nivel para hello IoT hub puede cambiarse. Sin embargo, si cambia el nivel de S1 toohello centro de IoT Hola está limitado durante ese día.

## <a name="delete-hello-iot-hub"></a>Eliminar el centro de IoT Hola

Puede examinar desee toodelete haciendo clic en el centro de IoT de toohello **examinar**, y, a continuación, elegir Hola toodelete concentrador adecuado. toodelete Hola centro de IoT, haga clic en hello **eliminar** botón situado debajo del nombre del centro de IoT Hola.

## <a name="next-steps"></a>Pasos siguientes

Siga estos toolearn de vínculos más acerca de cómo administrar el centro de IoT de Azure:

* [Administración masiva de dispositivos de IoT][lnk-bulk]
* [Métricas de IoT Hub][lnk-metrics]
* [Supervisión de operaciones][lnk-monitor]

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Guía para desarrolladores de IoT Hub][lnk-devguide]
* [Simular un dispositivo con IoT Edge][lnk-iotedge]
* [Proteger la solución de IoT de hello masa][lnk-securing]

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
