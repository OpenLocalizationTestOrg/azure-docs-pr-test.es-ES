---
title: ': los gemelos de aaaUnderstand centro de IoT de Azure dispositivo | Documentos de Microsoft'
description: "Guía del desarrollador - utilizar dispositivo gemelos toosynchronize los datos de estado y la configuración entre los dispositivos y el centro de IoT"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a>Dispositivos gemelos en IoT Hub
## <a name="overview"></a>Información general
Los *dispositivos gemelos* son documentos JSON que almacenan información sobre el estado de los dispositivos (metadatos, configuraciones y condiciones). Centro de IoT conserva a un gemelas de dispositivo para cada dispositivo que conecte tooIoT concentrador. En este artículo se describe:

* Hola estructura de gemelas de dispositivo de hello: *etiquetas*, *deseado* y *notificado propiedades*, y
* operaciones de Hola que aplicaciones para dispositivos y back-ends pueden realizar en: los gemelos de dispositivo.

> [!NOTE]
> Actualmente, están accesibles sólo desde los dispositivos que se conectan tooIoT concentrador: los gemelos de dispositivo mediante el protocolo MQTT Hola. Consulte toohello [compatibilidad MQTT] [ lnk-devguide-mqtt] artículo para obtener instrucciones sobre cómo toouse de aplicación de dispositivo existente de tooconvert MQTT.
> 
> 

### <a name="when-toouse"></a>Cuando toouse
Use los dispositivos gemelos para:

* Almacenar metadatos específicos del dispositivo en la nube de Hola. Por ejemplo, hello ubicación de implementación de una máquina expendedora.
* Notificar la información sobre el estado actual, como las funcionalidades y las condiciones disponibles de la aplicación del dispositivo. Por ejemplo, un dispositivo está conectado tooyour centro de IoT over móvil o Wi-Fi.
* Sincronizar el estado de Hola de flujos de trabajo de larga duración entre la aplicación para dispositivos y aplicaciones back-end. Por ejemplo, cuando una copia de solución de hello final especifica Hola nueva tooinstall de versión de firmware e informes de aplicaciones de dispositivos de Hola Hola distintas fases del proceso de actualización de Hola.
* Consultar los metadatos, la configuración o el estado del dispositivo.

Consulte demasiado[Guía de comunicación de dispositivos a la nube] [ lnk-d2c-guidance] para obtener instrucciones sobre el uso de propiedades notificados, mensajes del dispositivo a la nube o cargar el archivo.
Consulte demasiado[orientación para la comunicación en la nube para dispositivos] [ lnk-c2d-guidance] para obtener instrucciones sobre el uso de propiedades que desee, métodos directos o mensajes de la nube al dispositivo.

## <a name="device-twins"></a>Dispositivos gemelos
Los dispositivos gemelos almacenan información relacionada con el dispositivo que:

* Extremos de dispositivo y de vuelta pueden utilizar configuración y las condiciones de dispositivo de toosynchronize.
* Hola solución back-end puede usar tooquery y operaciones de ejecución prolongada de destino.

ciclo de vida de Hola de un doble de dispositivo está vinculado correspondiente toohello [identidad del dispositivo][lnk-identity]. Los dispositivos gemelos se crean y se eliminan implícitamente cuando se crea o se elimina una nueva identidad de dispositivo en IoT Hub.

Un dispositivo gemelo es un documento JSON que incluye:

* **Etiquetas**. Puede leer de y escribir en una sección del documento JSON de Hola Hola back-end de la solución. Las etiquetas no son aplicaciones de toodevice visible.
* **Propiedades deseadas**. Se utiliza junto con la configuración del dispositivo notificado propiedades toosynchronize o condiciones. Propiedades deseadas solo pueden establecerse por solución de hello volver final y pueden ser leídos por la aplicación de dispositivo de hello. aplicación de dispositivo de Hello también puede recibir una notificación en tiempo real de los cambios en las propiedades de hello deseado.
* **Propiedades notificadas**. Se utiliza junto con la configuración de dispositivo de toosynchronize de propiedades que desee o condiciones. Propiedades incluidos solo puede establecerse mediante la aplicación de dispositivo de hello y se pueden leer y consultar Hola solución back-end.

Además, raíz de Hola de documento JSON de hello dispositivo gemelas contiene las propiedades de solo lectura de Hola de identidad hello de dispositivo correspondiente almacenado en hello [del registro de identidad][lnk-identity].

![][img-twin]

Hola de ejemplo siguiente muestra a un documento JSON gemelas de dispositivo:

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

En el objeto raíz de hello, es propiedades del sistema de Hola y contenedor de objetos para `tags` y `reported` y `desired` propiedades. Hola `properties` contenedor contiene algunos elementos de solo lectura (`$metadata`, `$etag`, y `$version`) descrito en hello [dispositivo gemelas metadatos] [ lnk-twin-metadata] y [ Simultaneidad optimista] [ lnk-concurrency] secciones.

### <a name="reported-property-example"></a>Ejemplo de propiedad notificada
En el ejemplo anterior de hello, gemelos de dispositivo de hello contiene un `batteryLevel` propiedad notificado por la aplicación de dispositivo de hello. Esta propiedad resulta posible tooquery y operar con dispositivos basados en el último nivel de batería notificado Hola. Otros ejemplos incluyen funciones de dispositivo informes de aplicación de dispositivo de Hola u opciones de conectividad.

> [!NOTE]
> Propiedades notificados simplifican los escenarios donde hello solución back-end está interesado en hello última conocida el valor de una propiedad. Use [mensajes del dispositivo a la nube] [ lnk-d2c] si Hola solución back-end debe tooprocess telemetría de dispositivo en forma de Hola de secuencias de eventos con marca de tiempo, como la serie temporal.

### <a name="desired-property-example"></a>Ejemplo de propiedad deseada
En el ejemplo anterior de hello, Hola `telemetryConfig` gemelas dispositivo deseado y back-end de soluciones de Hola y configuración de telemetría de Hola de hello dispositivos aplicación toosynchronize utiliza propiedades notificados para este dispositivo. Por ejemplo:

1. Hola solución back-end establece la propiedad Hola deseado con el valor de configuración de hello deseado. Aquí es parte de hello del documento de hello con conjunto de propiedades de hello deseado:
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. Hola del dispositivo es una notificación de cambio de hello inmediatamente si conectado o en hello en primer lugar la reconexión. Hello del dispositivo, a continuación, notifica Hola actualizar configuración (o una condición de error mediante hello `status` propiedad). Aquí es parte de Hola de hello notificado propiedades:
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. Hola solución back-end puede realizar un seguimiento Hola resultados de la operación de configuración de hello en varios dispositivos, por [consultar] [ lnk-query] : los gemelos de dispositivo.

> [!NOTE]
> Hello fragmentos de código anteriores se muestran son ejemplos optimizado para mejorar la legibilidad, de una manera tooencode una configuración de dispositivo y su estado. Centro de IoT no impone un esquema específico para gemelas de hello dispositivo desean y notifican propiedades en: los gemelos de hello dispositivo.
> 
> 

Puede usar operaciones de larga duración: los gemelos toosynchronize como actualizaciones de firmware. Para obtener más información sobre cómo toouse propiedades toosynchronize y realizar un seguimiento de una operación larga en todos los dispositivos, consulte [uso deseado propiedades de dispositivos con tooconfigure][lnk-twin-properties].

## <a name="back-end-operations"></a>Operaciones de back-end
back-end de Hello solución funciona en gemelas de dispositivo de hello mediante hello las siguientes operaciones atómicas, expuestas a través de HTTP:

1. **Recuperación del dispositivo gemelo por el id**. Esta operación devuelve Hola dispositivo gemelas, incluidas las etiquetas y documentos deseado, notifican y propiedades del sistema.
2. **Actualización parcial de los dispositivos gemelos**. Esta operación permite Hola solución back-end toopartially actualización hello las etiquetas o propiedades que desee en un doble de dispositivo. actualización parcial de Hola se expresa como un documento JSON que agrega o actualiza cualquier propiedad. Se establecen demasiado`null` se quitan. Hello en el ejemplo siguiente se crea una nueva propiedad deseada con valor `{"newProperty": "newValue"}`, sobrescribe el valor existente de Hola de `existingProperty` con `"otherNewValue"`y quita `otherOldProperty`. Se realiza ningún otro cambio tooexisting deseado propiedades o etiquetas:
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. **Reemplazar propiedades deseadas**. Esta toocompletely de back-end de soluciones de Hola de operación permite sobrescribir todas las propiedades deseadas existentes y sustituir un nuevo documento JSON para `properties/desired`.
4. **Reemplazar etiquetas**. Esta toocompletely de back-end de soluciones de Hola de operación permite sobrescribir todas las etiquetas existentes y sustituir un nuevo documento JSON para `tags`.
5. **Recibir notificaciones gemelas**. Esta operación permite toobe de back-end de soluciones de Hola una notificación cuando se modifican gemelas Hola. toodo por lo tanto, la solución de IoT necesita toocreate una ruta e igual de origen de datos de hello tooset demasiado*twinChangeEvents*. De forma predeterminada, no se envían notificaciones gemelas, es decir, no existen previamente tales rutas. Si es demasiado alta tasa de Hola de cambio o por otras razones, como los errores internos, Hola centro de IoT puede enviar solo una notificación que contiene todos los cambios. Por lo tanto, si la aplicación necesita registro y auditoría confiables de todos los estados intermedios, la recomendación sigue siendo usar mensajes D2C. mensaje de notificación de Hello gemelas incluye propiedades y cuerpo.

    - Propiedades

    | Nombre | Valor |
    | --- | --- |
    $content-type | application/json |
    $iothub-enqueuedtime |  Hora de envían de notificaciones de Hola |
    $iothub-message-source | twinChangeEvents |
    $content-encoding | utf-8 |
    deviceId | Id. de dispositivo de Hola |
    hubName | Nombre de IoT Hub |
    operationTimestamp | Marca de tiempo [ISO8601] de operación |
    iothub-message-schema | deviceLifecycleNotification |
    opType | "replaceTwin" o "updateTwin" |

    Propiedades de sistema de mensajes tienen el prefijo hello `'$'` símbolos.

    - Cuerpo
        
    Esta sección incluye todos los cambios de hello gemelas en un formato JSON. Utiliza Hola mismo formato como una revisión, con la diferencia de Hola que TI puede contener todas las secciones de gemelas: etiquetas, properties.reported, properties.desired y que contiene elementos de Hola "$metadata". Por ejemplo,
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

Todos los Hola compatibilidad anterior de operations [simultaneidad optimista] [ lnk-concurrency] y requieren hello **ServiceConnect** permiso, tal como se define en hello [seguridad ] [ lnk-security] artículo.

Además operaciones toothese, solución de hello realice copia final puede:

* : Los gemelos de dispositivo de hello mediante Hola de consulta similar a SQL [lenguaje de consultas del centro de IoT][lnk-query].
* Realizar operaciones en conjuntos grandes de dispositivos gemelos usando [trabajos][lnk-jobs].

## <a name="device-operations"></a>Operaciones de dispositivo
aplicación de dispositivo de Hello opera en gemelas de dispositivo de hello mediante las siguientes operaciones atómicas de hello:

1. **Recuperación del dispositivo gemelo**. Esta operación devuelve el documento de hello dispositivo gemelas (incluidas las etiquetas y deseado, notifican y propiedades del sistema) de hello dispositivo está conectado actualmente.
2. **Actualizar parcialmente propiedades notificadas**. Esta actualización parcial de operación habilita Hola de hello informó de propiedades de dispositivo de hello conectado actualmente. Este Hola de usos de operación actualizar JSON mismo formato que Hola solución back-end usa para una actualización parcial de propiedades que desee.
3. **Observar las propiedades deseadas**. dispositivo conectado actualmente Hola puede toobe una notificación de propiedades de toohello deseado de las actualizaciones que se produzcan. dispositivo de Hello recibe Hola mismo formulario de actualización (reemplazo completo o parcial) ejecuta Hola solución back-end.

Todas las operaciones anteriores de Hola requieren hello **DeviceConnect** permiso, tal como se define en hello [seguridad] [ lnk-security] artículo.

Hola [dispositivos de IoT de Azure SDK] [ lnk-sdks] facilitan hello toouse fácil anterior a las operaciones de muchos lenguajes y plataformas. Puede encontrar más información sobre los detalles de Hola de primitivas del centro de IoT para sincronización de propiedades que desee en [flujo de reconexión de dispositivo][lnk-reconnection].

> [!NOTE]
> Actualmente, están accesibles sólo desde los dispositivos que se conectan tooIoT concentrador: los gemelos de dispositivo mediante el protocolo MQTT Hola.
> 
> 

## <a name="reference-topics"></a>Temas de referencia:
Hello temas de referencia siguientes proporcionan más información sobre el centro de IoT de controlar acceso tooyour.

## <a name="tags-and-properties-format"></a>Formato de etiquetas y propiedades
Etiquetas, propiedades deseadas y se notificará son objetos JSON con hello siguientes restricciones:

* Todas las claves en objetos JSON son cadenas UNICODE UTF-8 de 64 caracteres que distinguen entre mayúsculas y minúsculas. Entre los caracteres permitidos no se incluyen los caracteres de control UNICODE (segmentos C0 y C1), ni `'.'`, `' '` y `'$'`.
* Todos los valores en objetos JSON pueden ser de los siguientes tipos JSON de hello: un valor booleano, número, cadena, objeto. No se permiten matrices.
* Todos los objetos JSON en etiquetas y propiedades deseadas y notificadas pueden tener una profundidad máxima de 5. Por ejemplo, hello después el objeto es válido:

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* Todos los valores de cadena pueden tener como máximo una longitud de 512 bytes.

## <a name="device-twin-size"></a>Tamaño del dispositivo gemelo
Centro de IoT exige una limitación de tamaño de 8KB en valores de hello de `tags`, `properties/desired`, y `properties/reported`, excluir elementos de solo lectura.
Hello tamaño se calcula el recuento de todos los caracteres excepto UNICODE controlan caracteres (segmentos C0 y C1) y los espacios `' '` cuando aparece fuera de una constante de cadena.
Centro de IoT rechaza con un error todas las operaciones que podrían aumentar el tamaño de Hola de esos documentos por encima del límite de Hola.

## <a name="device-twin-metadata"></a>Metadatos de dispositivo gemelo
Centro de IoT mantiene Hola marca de tiempo de la última actualización de Hola para cada objeto JSON de gemelas dispositivo deseado y notifica propiedades. las marcas de tiempo de Hello en formato UTC y codifica en hello [ISO8601] formato `YYYY-MM-DDTHH:MM:SS.mmmZ`.
Por ejemplo:

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

Esta información se mantiene en cada nivel actualizaciones de toopreserve (hojas de hello no solo de hello estructura JSON) que quitar claves de objeto.

## <a name="optimistic-concurrency"></a>Simultaneidad optimista
Tanto las etiquetas como las propiedades deseadas y notificadas admiten la simultaneidad optimista.
Las etiquetas tienen un valor de ETag, como por [RFC7232], que representa la representación JSON de la etiqueta de Hola. Puede usar ETags en operaciones de actualización condicional de coherencia de tooensure de back-end de soluciones de Hola.

Gemelas dispositivo deseado y notifica propiedades no tienen valores de ETag, pero tienen un `$version` valor confirmado toobe incremental. De igual forma tooan ETag, versión de Hola puede utilizarse por hello coherencia tooenforce de entidad de las actualizaciones de la actualización. Por ejemplo, una aplicación de dispositivo para un notificado propiedad o hello solución back-end para una propiedad deseada.

Versiones también son útiles cuando un agente de observación (por ejemplo, la aplicación de dispositivo de hello observar propiedades Hola deseado) deberá conciliar los carreras entre una notificación de actualización y el resultado de hello de una operación de recuperación. Hola sección [flujo de reconexión de dispositivo] [ lnk-reconnection] proporciona más información.

## <a name="device-reconnection-flow"></a>Flujo de reconexión de dispositivos
IoT Hub no conserva las notificaciones de actualización de las propiedades deseadas para los dispositivos desconectados. Después de que un dispositivo que se está conectando debe recuperar el documento de todas las propiedades deseadas de hello, en toosubscribing de suma para notificaciones de actualización. Dada la posibilidad de Hola de carreras entre notificaciones de actualización y la recuperación completa, debe garantizarse Hola siga flujo:

1. Aplicación de dispositivo conecta tooan centro de IoT.
2. La aplicación de dispositivo se suscribe a las notificaciones de actualización de las propiedades deseadas.
3. Aplicación de dispositivo recupera el documento "hello" completo de propiedades que desee.

aplicación de dispositivo de Hello puede pasar por alto todas las notificaciones con `$version` inferior o igual a la versión de Hola de documento recuperado "hello" completo. Este enfoque es posible porque IoT Hub garantiza que las versiones siempre se incrementan.

> [!NOTE]
> Esta lógica se ha implementado en hello [dispositivos de IoT de Azure SDK][lnk-sdks]. Esta descripción es útil sólo si Hola del dispositivo no puede usar cualquiera de los dispositivos de IoT de Azure SDK y debe programar la interfaz de hello MQTT directamente.
> 
> 

## <a name="additional-reference-material"></a>Material de referencia adicional
Otros temas de referencia en la Guía del desarrollador de centro de IoT Hola incluyen:

* Hola [los extremos del centro de IoT] [ lnk-endpoints] artículo describe Hola varios extremos que cada centro de IoT expone las operaciones de tiempo de ejecución y administración.
* Hola [limitación y las cuotas] [ lnk-quotas] artículo describen las cuotas de Hola que se aplican toohello servicio del centro de IoT y Hola limitación tooexpect de comportamiento cuando se usa el servicio de Hola.
* Hola [SDK de dispositivos y servicios de Azure IoT] [ lnk-sdks] listas de artículo Hola SDK idioma puede usar cuando se desarrollan aplicaciones de dispositivos y servicios que interactúan con el centro de IoT.
* Hola [lenguaje de consulta de centro de IoT para: los gemelos de dispositivo, los trabajos y el enrutamiento de mensajes] [ lnk-query] artículo describe Hola lenguaje de consultas del centro de IoT puede usar información de tooretrieve centro de IoT de: los gemelos de dispositivo y trabajos .
* Hola [compatibilidad IoT Hub MQTT] [ lnk-devguide-mqtt] artículo proporciona más información acerca del soporte técnico de centro de IoT para el protocolo MQTT Hola.

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido: los gemelos de dispositivo, es posible que interesa Hola temas de guía para desarrolladores de centro de IoT siguientes:

* [Invocación de un método directo en un dispositivo][lnk-methods]
* [Programación de trabajos en varios dispositivos][lnk-jobs]

Si desea que tootry algunos de los conceptos de hello descritos en este artículo, es posible que interesa Hola centro de IoT tutoriales:

* [¿Cómo toouse Hola gemelas de dispositivo][lnk-twin-tutorial]
* [¿Cómo toouse dispositivo dos propiedades][lnk-twin-properties]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
