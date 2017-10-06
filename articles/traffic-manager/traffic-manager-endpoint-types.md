---
title: "Tipos de punto de conexión de administrador aaaTraffic | Documentos de Microsoft"
description: "En este artículo, se explican los diferentes tipos de puntos de conexión que pueden utilizarse con el Administrador de tráfico de Azure."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 4e506986-f78d-41d1-becf-56c8516e4d21
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: kumud
ms.openlocfilehash: 787412ac6207f76791bf3ff753d1df2767b1a964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoints"></a>Puntos de conexión del Administrador de tráfico
Las implementaciones de tooapplication que se ejecutan en distintos centros de datos de distribuidas de Microsoft Azure Traffic Manager permite toocontrol forma de tráfico de red. Se configura cada implementación de aplicaciones como un "punto de conexión" en Traffic Manager. Cuando el Administrador de tráfico recibe una solicitud DNS, elige un tooreturn de punto de conexión disponible en hello respuesta DNS. Administrador de tráfico envergadura elección de hello en el estado de punto de conexión actual de Hola y el método de enrutamiento del tráfico de hello. Para obtener más información, consulte [Cómo funciona el Administrador de tráfico](traffic-manager-how-traffic-manager-works.md).

El Administrador de tráfico admite tres tipos de puntos de conexión:
* **puntos de conexión de Azure** se utilizan para los servicios hospedados en Azure.
* **puntos de conexión externos** se emplean para los servicios hospedados fuera de Azure; es decir, de forma local o con otro proveedor de hospedaje.
* **Anidar extremos** es toocreate de perfiles de Traffic Manager toocombine usado más flexible enrutamiento del tráfico esquemas toosupport Hola necesidades de las implementaciones más grandes y complejas.

No hay restricciones en cuanto a cómo se combinan los diferentes tipos de puntos de conexión en un único perfil del Administrador de tráfico. Cada perfil puede contener cualquier combinación de tipos de punto de conexión.

Hola las secciones siguientes describe cada tipo de punto de conexión en mayor profundidad.

## <a name="azure-endpoints"></a>puntos de conexión de Azure

Los puntos de conexión de Azure se utilizan para servicios basados en Azure en Traffic Manager. se admite Hola siguientes tipos de recursos de Azure:

* Máquinas virtuales IaaS "clásicas" y servicios en la nube PaaS.
* Web Apps
* Recursos de PublicIPAddress (que pueden ser tooVMs conectado directamente o a través de un equilibrador de carga de Azure). Hola publicIpAddress debe tener un nombre DNS asignado toobe usada en un perfil de Traffic Manager.

Los recursos de PublicIPAddress son recursos de Azure Resource Manager. No existen en el modelo de implementación clásica de Hola. Por lo tanto, solo son compatibles con Azure Resource Manager de Traffic Manager. Hola se admiten otros tipos de punto de conexión a través de hello y Administrador de recursos del modelo de implementación clásica.

Cuando se usan puntos de conexión de Azure, Traffic Manager detecta cuándo se detiene e inicia una máquina virtual IaaS "clásica", un servicio en la nube o una aplicación web. Este estado se refleja en el estado de punto de conexión de Hola. Consulte [Supervisión de puntos de conexión de Traffic Manager](traffic-manager-monitoring.md#endpoint-and-profile-status) para más información. Cuando se detiene el servicio subyacente de Hola, Administrador de tráfico no lleva a cabo comprobaciones de mantenimiento del punto de conexión o el punto de conexión de dirigir el tráfico toohello. No se producen eventos de facturación para hello de Traffic Manager detuvo la instancia. Cuando se reinicia el servicio hello, facturación se reanuda y punto de conexión de hello es apto tooreceive tráfico. Esta detección no aplica a los puntos de conexión tooPublicIpAddress.

## <a name="external-endpoints"></a>puntos de conexión externos

Los puntos de conexión externos se usan para servicios fuera de Azure. Por ejemplo, un servicio hospedado localmente o con un proveedor diferente. Extremos externos pueden utilizar individualmente o combinar con extremos de Azure en hello mismo perfil de Traffic Manager. La combinación de puntos de conexión de Azure con otros externos posibilita distintos escenarios:

* En un modelo de conmutación por error activo / activo o activo / pasivo, utilice Azure tooprovide mayor redundancia para una aplicación local existente.
* latencia de aplicación tooreduce para los usuarios alrededor de Hola a todos, ampliar una existente local aplicación tooadditional las ubicaciones geográficas de Azure. Para más información, consulte [Método de enrutamiento del tráfico de rendimiento de Traffic Manager](traffic-manager-routing-methods.md#performance).
* Utilice Azure tooprovide capacidad adicional para una aplicación local existente, continuamente o como un toomeet de solución de 'ráfaga en la nube' aumento de la demanda.

En algunos casos, resulta útil toouse extremos externos tooreference Azure servicios (para obtener ejemplos, vea hello [preguntas más frecuentes sobre](traffic-manager-faqs.md#traffic-manager-endpoints)). En este caso, las comprobaciones de mantenimiento se cobran a Hola extremos de Azure velocidad, no Hola extremos externos. Sin embargo, a diferencia de los extremos de Azure, si detiene o eliminar Hola subyacente service, comprobación de mantenimiento facturación continúa hasta que deshabilitar o eliminar el extremo de hello en el Administrador de tráfico.

## <a name="nested-endpoints"></a>puntos de conexión anidados

Extremos anidados combinan varios Traffic Manager perfiles toocreate enrutamiento del tráfico esquemas flexibles y satisfacer las necesidades de Hola de implementaciones grandes y complejas. Con los puntos de conexión, se agrega un perfil de 'child' como un perfil de punto de conexión tooa 'parent'. Ambos perfiles de hello primarios y secundarios pueden contener otros puntos de conexión de cualquier tipo, incluidos otros perfiles anidados. Para más información, consulte [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md)(Perfiles anidados de Administrador de tráfico).

## <a name="web-apps-as-endpoints"></a>Aplicaciones web como puntos de conexión

A la hora de configurar aplicaciones web como puntos de conexión en el Administrador de tráfico, hay que tener en cuenta otras consideraciones:

1. Solo las aplicaciones Web en hello SKU 'Estándar' o una versión posterior son aptas para su uso con el Administrador de tráfico. Intentos de tooadd una aplicación Web de un error SKU inferior. Degradar Hola provoca SKU de una aplicación Web existente en el Administrador de tráfico ya no enviar tráfico toothat aplicación Web.
2. Cuando un punto de conexión recibe una solicitud HTTP, utiliza hello 'host' encabezado en hello solicitud toodetermine qué aplicación Web debe solicitar Hola de servicio. encabezado de host de Hello contiene Hola DNS nombre utilizado tooinitiate Hola solicitud, por ejemplo 'contosoapp.azurewebsites.net'. un nombre DNS diferente con la aplicación Web, el nombre DNS de hello toouse debe registrarse como un nombre de dominio personalizado para la aplicación Hola. Al agregar un punto de conexión de la aplicación Web como un extremo de Azure, nombre DNS del perfil de Traffic Manager de Hola se registra automáticamente para la aplicación hello. Este registro se quita automáticamente cuando se elimina el punto de conexión de Hola.
3. Cada perfil del Administrador de tráfico puede tener, como máximo, un punto de conexión de aplicación web en cada región de Azure. toowork alrededor de esta restricción, puede configurar una aplicación Web como un extremo externo. Para obtener más información, vea hello [preguntas más frecuentes sobre](traffic-manager-faqs.md#traffic-manager-endpoints).

## <a name="enabling-and-disabling-endpoints"></a>Habilitación y deshabilitación de puntos de conexión

Deshabilitar un punto de conexión en el Administrador de tráfico puede ser útil tootemporarily remove tráfico desde un punto de conexión que se encuentra en modo de mantenimiento o que se va a volver a implementar. Una vez que el punto de conexión de hello funcione de nuevo, puede volver a habilitar.

Los puntos de conexión se pueden habilitar y deshabilitar mediante el portal de administrador de tráfico de hello, PowerShell, CLI o API de REST, todos ellos se admiten en el Administrador de recursos y el modelo de implementación clásica de Hola.

> [!NOTE]
> Deshabilitar un extremo de Azure no tiene nada toodo con su estado de implementación en Azure. Un Azure servicio (por ejemplo, tal y como una máquina virtual o una aplicación Web permanece tráfico de tooreceive ejecutando y puede incluso cuando está deshabilitado en el Administrador de tráfico. El tráfico se puede resolver directamente toohello instancia de servicio en lugar de a través de hello Traffic Manager nombre DNS del perfil. Para obtener más información, consulte [Cómo funciona el Administrador de tráfico](traffic-manager-how-traffic-manager-works.md).

Elegibilidad actual de Hola de cada tráfico tooreceive de punto de conexión depende de hello siguientes factores:

* estado del perfil Hello (habilitado/deshabilitado)
* estado de punto de conexión de Hello (habilitado/deshabilitado)
* resultados de Hola Hola de comprobaciones de estado para ese punto de conexión

Consulte [Acerca de la supervisión del Administrador de tráfico](traffic-manager-monitoring.md#endpoint-and-profile-status)para obtener más información.

> [!NOTE]
> Dado que Traffic Manager funciona en el nivel de DNS de hello, es punto de conexión de tooany de conexiones existente de tooinfluence no se puede. Cuando un punto de conexión no está disponible, el Administrador de tráfico dirige nuevas conexiones tooanother punto de conexión disponible. Sin embargo, host Hola detrás de Hola deshabilitado o punto de conexión incorrecto puede continuar tooreceive tráfico a través de las conexiones existentes hasta que terminen las sesiones. Las aplicaciones deben limitar toodrain Hola sesión duración tooallow tráfico desde las conexiones existentes.

Si se deshabilitan todos los extremos de un perfil, o si está deshabilitado el propio perfil Hola, Traffic Manager envía una 'NXDOMAIN' respuesta tooa nueva consulta DNS.


## <a name="next-steps"></a>Pasos siguientes

* Consulte [Cómo funciona el Administrador de tráfico](traffic-manager-how-traffic-manager-works.md).
* Obtenga información sobre la [supervisión del punto de conexión y la conmutación por error automática](traffic-manager-monitoring.md)del Administrador de tráfico.
* Conozca los [métodos de enrutamiento de tráfico](traffic-manager-routing-methods.md)del Administrador de tráfico.
