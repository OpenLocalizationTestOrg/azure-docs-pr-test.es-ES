---
title: "aaaDebug la aplicación de tejido de servicio de Azure en Eclipse | Documentos de Microsoft"
description: "Mejorar Hola confiabilidad y rendimiento de los servicios mediante el desarrollo y depuración en Eclipse en un clúster de desarrollo local."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a>Depuración de la aplicación de Service Fabric para Java con Eclipse
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
> 

1. Iniciar un clúster de desarrollo local siguiendo los pasos de hello en [configuración del entorno de desarrollo de Service Fabric](service-fabric-get-started-linux.md).

2. Actualizar entryPoint.sh del servicio de hello desea toodebug, para que se inicie el proceso de java de hello con parámetros de depuración remota. Este archivo puede encontrarse en hello ubicación siguiente: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``. En este ejemplo, el puerto 8001 está establecido para depuración.

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. Actualizar Hola el manifiesto de aplicación mediante el establecimiento de recuento de instancias de Hola o hello número de réplica para el servicio de Hola que se está depurando too1. Esta configuración evita conflictos de puerto de Hola que se utiliza para la depuración. Por ejemplo, para los servicios sin estado, establezca ``InstanceCount="1"`` y servicios con estado de réplica de destino y min Hola conjunto establezca too1 tamaños de la manera siguiente: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.

4. Implementar la aplicación hello.

5. Hola Eclipse IDE, seleccione **ejecución -> Debug Configurations -> aplicación Java remota y las propiedades de conexión de entrada** y establecer las propiedades de hello como sigue:

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  Establecer puntos de interrupción en puntos deseados y depurar la aplicación hello.

Si se bloquea la aplicación hello, también puede tooenable coredumps. Ejecute ``ulimit -c`` en un shell y, si devuelve el valor 0, los volcados de memoria no están habilitados. tooenable coredumps ilimitados, ejecutar el siguiente comando de Hola: ``ulimit -c unlimited``. También puede comprobar el estado de hello mediante comandos de hello ``ulimit -a``.  Si desea que la ruta de acceso de generación de tooupdate hello coredump, ejecute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``. 

### <a name="next-steps"></a>Pasos siguientes

* [Recopilación de registros con Diagnósticos de Azure de Linux](service-fabric-diagnostics-how-to-setup-lad.md).
* [Supervisión y diagnóstico de servicios localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).
