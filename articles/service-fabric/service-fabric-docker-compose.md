---
title: aaaAzure Crear vista previa en el tejido de Docker servicio
description: "Azure Service Fabric acepta Docker Compose toomake de formato sea más fácil tooorchestrate los contenedores existentes mediante Service Fabric. Esta compatibilidad se encuentra actualmente en versión preliminar."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a>Compatibilidad con la aplicación Docker Compose en Azure Service Fabric (versión preliminar)

Docker usa hello [docker compose.yml](https://docs.docker.com/compose) archivo para definir el contenedor de varias aplicaciones. toomake lo fácil para clientes familiarizados con aplicaciones contenedor Docker tooorchestrate existentes en el tejido de servicio de Azure, hemos incluido soporte de vista previa para Docker Compose forma nativa en la plataforma de Hola. Service Fabric puede aceptar la versión 3 y posterior de los archivos `docker-compose.yml`. 

Dado que esta compatibilidad está en versión preliminar, solo se admite un subconjunto de directivas de Compose. Por ejemplo, no se admiten las actualizaciones de aplicaciones. Sin embargo, siempre puede quitar e implementar aplicaciones en lugar de actualizarlas.

toouse esta vista previa, crear el clúster con la versión 5.7 o posterior del tiempo de ejecución de hello Service Fabric a través de hello portal de Azure junto con hello correspondiente SDK. 

> [!NOTE]
> Esta característica se encuentra en versión preliminar y no se admite en producción.

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a>Implementación de un archivo de Docker Compose en Service Fabric

Hello siguientes comandos crean una aplicación de Service Fabric (denominado `fabric:/TestContainerApp` en el anterior ejemplo de Hola), que puede supervisar y administrar como cualquier otra aplicación de Service Fabric. Puede usar el nombre de la aplicación especificada de Hola para consultas de estado.

### <a name="use-powershell"></a>Uso de PowerShell

Crear una aplicación de redacción de tejido de servicio desde un archivo de docker compose.yml ejecutando el siguiente comando de PowerShell de hello:

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

`RegistryUserName`y `RegistryPassword` consulte toohello contenedor del registro username y password. Después de haber completado la aplicación hello, puede comprobar su estado mediante Hola siguiente comando:

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

toodelete Hola redactar aplicación a través de PowerShell, use Hola siguiente comando:

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a>Uso de la CLI de Azure Service Fabric (sfctl)

Como alternativa, puede usar Hola siguiente comando de CLI de tejido de servicio:

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

Después de haber creado la aplicación hello, puede comprobar su estado mediante Hola siguiente comando:

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

Hola toodelete aplicación de redacción, utilice Hola siguiente comando:

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a>Directivas de Compose admitidas

Esta vista previa admite un subconjunto de opciones de configuración de Hola desde el formato de versión 3 de redactar hello, incluidos Hola después a primitivas:

* Services > Deploy > Replicas
* Services > Deploy > Placement > Constraints
* Services > Deploy > Resources > Limits
    * -cpu-shares
    * -memory
    * -memory-swap
* Services > Commands
* Services > Environment
* Services > Ports
* Services > Image
* Services > Isolation (solo para Windows)
* Services > Logging > Driver
* Services > Logging > Driver > Options
* Volumen e implementación > Volumen

Configurar clúster Hola para aplicar límites de recursos, como se describe en [regulador de recursos de Service Fabric](service-fabric-resource-governance.md). El resto de directivas de Docker Compose no se admiten en esta versión preliminar.

## <a name="servicednsname-computation"></a>Cálculo de ServiceDnsName

Si el nombre de servicio de Hola que especifique en un archivo de composición es un nombre de dominio completo (es decir, contiene un punto [.]), nombre DNS de hello registrado por Service Fabric es `<ServiceName>` (incluido el punto de hello). De lo contrario, cada segmento de ruta de acceso en nombre de la aplicación hello se convierte en una etiqueta de dominio en nombre DNS del servicio de hello, con el primer segmento de ruta de acceso Hola se convierta en etiqueta de dominio de nivel superior de Hola.

Por ejemplo, si Hola especifica el nombre de la aplicación es `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` sería Hola nombre DNS registrado.

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a>Diferencias entre Compose (definición de instancia) y el modelo de aplicación de Service Fabric (definición de tipo)

Un archivo docker-compose.yml describe un conjunto implementable de contenedores que incluye sus propiedades y configuraciones.
Por ejemplo, archivo hello puede contener variables de entorno y puertos. También puede especificar parámetros de implementación, como las restricciones de posición, los límites de recursos y los nombres DNS, en archivo de hello compose.yml de docker.

Hola [modelo de aplicaciones de Service Fabric](service-fabric-application-model.md) usa tipos de servicio y los tipos de aplicación, donde puede tener muchas instancias de aplicación de Hola mismo tipo. Por ejemplo, puede tener una instancia de aplicación por cliente. Este modelo basado en el tipo es compatible con varias versiones del programa Hola a mismo tipo de aplicación que está registrado con hello en tiempo de ejecución.

Por ejemplo, un cliente puede tener una aplicación crea una instancia con tipo 1.0 de AppTypeA y cliente B puede tener otra aplicación que crea una instancia con hello mismo tipo y la versión. Definir tipos de aplicación hello en los manifiestos de aplicación hello y especificar parámetros de nombre y la implementación de la aplicación hello cuando se crea la aplicación hello.

Aunque este modelo ofrece flexibilidad, planeamos toosupport un modelo de implementación sea más sencillo y basados en instancias donde tipos son implícitos del archivo de manifiesto de Hola. En este modelo, cada aplicación obtiene su propio manifiesto independiente. Esta iniciativa se va a trasladar a la versión preliminar agregando compatibilidad con el archivo docker-compose.yml, que es un formato de implementación basado en instancias.

## <a name="next-steps"></a>Pasos siguientes

* Obtener información detallada acerca de hello [modelo de aplicaciones de Service Fabric](service-fabric-application-model.md)
* [Introducción a la CLI de Service Fabric](service-fabric-cli.md)
