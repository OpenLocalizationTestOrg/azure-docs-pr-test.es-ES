---
title: "Temas de actualización de aplicación aaaAdvanced | Documentos de Microsoft"
description: "En este artículo se trata algunos temas avanzados pertenecen tooupgrading una aplicación de Service Fabric."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a>Actualización de la aplicación de Service Fabric: temas avanzados
## <a name="adding-or-removing-services-during-an-application-upgrade"></a>Adición o eliminación de servicios durante la actualización de una aplicación
Si un nuevo servicio se agrega tooan aplicación que ya está implementado y publicado como una actualización, nuevo servicio de hello es aplicación de agregado toohello implementado.  Esta actualización no afecta a ninguno de los servicios de Hola que ya formaban parte de la aplicación hello. Sin embargo, se debe iniciar una instancia de servicio de Hola que se agregó para toobe de servicio nuevo de hello active (con hello `New-ServiceFabricService` cmdlet).

También se pueden quitar servicios de una aplicación como parte de una actualización. Sin embargo, se deben detener todas las instancias actuales del servicio de Hola se van a eliminar antes de continuar con la actualización de hello (con hello `Remove-ServiceFabricService` cmdlet).

## <a name="manual-upgrade-mode"></a>Modo de actualización manual
> [!NOTE]
> modo manual no supervisada de Hello debe considerarse solo para una actualización de errores o suspendida. modo supervisado de Hello es Hola recomienda el modo de actualización para las aplicaciones de Service Fabric.
>
>

Azure Service Fabric proporciona varios modos de actualización de clústeres de desarrollo y producción de toosupport. Las opciones de implementación elegidas pueden ser diferentes para distintos entornos.

Hola supervisado de actualización gradual de la aplicación es toouse de actualización más habitual de hello en el entorno de producción de hello. Cuando actualiza Hola se especifica la directiva, Service Fabric garantiza que la aplicación hello es correcto para poder continuar con la actualización Hola.

 Administrador de la aplicación Hello sirve manual Hola gradual a modo de actualización de aplicación toohave control total sobre el progreso de la actualización Hola a través de hello distintos dominios de actualización. Este modo es útil cuando se requiere una directiva de evaluación de estado personalizado o compleja, o qué está ocurriendo una actualización no convencional (por ejemplo, aplicación hello ya está en pérdida de datos).

Por último, hello automatizadas actualización gradual de la aplicación es útil para el desarrollo o pruebas de entornos tooprovide ciclo de una iteración rápida durante el desarrollo del servicio.

## <a name="change-toomanual-upgrade-mode"></a>Cambiar el modo de actualización toomanual
**Manual**--Detener actualización de la aplicación hello en Hola Hola UD y cambio actual Actualizar tooUnmonitored de modo Manual. Hello administrador necesita llamada toomanually **MoveNextApplicationUpgradeDomainAsync** tooproceed con hello, actualizar o activar una reversión si se inicia una nueva actualización. Una vez que la actualización de hello entra en el modo Manual hello, permanece en modo Manual de hello hasta que se inicia una nueva actualización. Hola **GetApplicationUpgradeProgressAsync** comando devuelve tejido\_aplicación\_actualizar\_estado\_GRADUALES\_al día\_pendiente.

## <a name="upgrade-with-a-diff-package"></a>Actualización con un paquete de diferencias
Puede actualizarse una aplicación de Service Fabric mediante el aprovisionamiento de un paquete de aplicación completo y autocontenido. Una aplicación también puede actualizarse mediante un paquete de diferencias que contiene solo de los archivos de aplicación de hello actualizado, Hola actualiza el manifiesto de aplicación y los archivos de manifiesto de servicio de Hola.

Un paquete completo de la aplicación contiene todos los Hola archivos necesarios toostart y ejecuta una aplicación de Service Fabric. Un paquete de diferencias contiene sólo los archivos de hello cambiado entre aprovisionar última Hola y de actualización actual de hello, además de manifiesto de aplicación completa de Hola y el servicio de hello los archivos de manifiesto. Cualquier referencia en el manifiesto de aplicación de Hola o manifiesto de servicio que no se encuentra en el diseño de la compilación de Hola se busca en el almacén de imágenes de Hola.

Paquetes de aplicación completo son necesarios para la primera instalación de un clúster de toohello de aplicación de Hola. Las actualizaciones posteriores pueden ser un paquete de aplicación completo o un paquete de diferencias.

Casos en los que usar un paquete de diferencias sería una buena opción:

* Se prefiere un paquete de diferencias cuando tiene un paquete de aplicación grande que hace referencia a varios archivos del manifiesto de servicio o varios paquetes de código, configuración o datos.
* Un paquete de diferencias es preferible cuando tenga un sistema de implementación que se genera el diseño de la compilación de hello directamente desde el proceso de compilación de la aplicación. En este caso, incluso si no ha cambiado el código de hello, ensamblados recién creados obtienen una suma de comprobación diferentes. Uso de un paquete completo de la aplicación requeriría tooupdate Hola versión en todos los paquetes de código. Con un paquete de diferencias, sólo proporcionar archivos Hola que ha cambiado y archivos de manifiesto de Hola que ha cambiado la versión de Hola.

Cuando se actualiza una aplicación mediante Visual Studio, el paquete de diferencias de Hola se publica automáticamente. toocreate un paquete de diferencias Hola manualmente, el manifiesto de aplicación y deben actualizarse los manifiestos de servicio de hello, pero solamente los paquetes de saludo cambiado deben incluirse en el paquete de aplicación final de Hola.

Por ejemplo, puede empezar con hello tras la aplicación (números de versión proporcionados para facilitar la comprensión):

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

Ahora, supongamos que desea tooupdate solo Hola paquete de código de service1 mediante un paquete de diferencias mediante PowerShell. Ahora, la aplicación actualizada tiene Hola siguiendo la estructura de carpetas:

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

En este caso, actualiza too2.0.0 de manifiesto de aplicación de Hola y el manifiesto de servicio de hello actualización del paquete de código de service1 tooreflect Hola. carpeta de Hello para el paquete de aplicación tendría Hola siguiente estructura:

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a>Pasos siguientes
[actualización de aplicaciones usando Visual Studio](service-fabric-application-upgrade-tutorial.md) ofrece información para actualizar una aplicación mediante Visual Studio.

[actualización de aplicaciones mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) se explica en detalle lo que tiene que hacer para actualizar una aplicación mediante PowerShell.

Puede controlar cómo se actualiza una aplicación usando [parámetros de actualización](service-fabric-application-upgrade-parameters.md).

Hacer que las actualizaciones de la aplicación sea compatible por el aprendizaje cómo toouse [serialización de datos](service-fabric-application-upgrade-data-serialization.md).

Solucione problemas habituales en las actualizaciones de aplicaciones, se hace referencia a pasos toohello en [solución de problemas de las actualizaciones de aplicaciones](service-fabric-application-upgrade-troubleshooting.md).
