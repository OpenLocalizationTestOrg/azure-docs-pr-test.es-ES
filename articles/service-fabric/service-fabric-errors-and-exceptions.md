---
title: excepciones del FabricClient aaaCommon | Documentos de Microsoft
description: "Describe las excepciones de common de Hola y errores que se pueden producir por hello FabricClient APIs mientras se realizan operaciones de administración de aplicación y clúster."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: bb821313-b221-479f-b08e-36cf07e60a07
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 55bb556b25150524ebc28756eb1bd3e91dc37853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="common-exceptions-and-errors-when-working-with-hello-fabricclient-apis"></a>Excepciones y errores cuando se trabaja con hello FabricClient APIs comunes
Hola [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) API permiten clúster y aplicación de los administradores tooperform tareas administrativas en un clúster, servicio o aplicación de Service Fabric. Por ejemplo, implementación de aplicaciones, actualización y eliminación, comprobando el estado de hello un clúster o probar un servicio. Los desarrolladores de aplicaciones y los administradores de clústeres hello FabricClient API toodevelop herramientas sirven para administrar aplicaciones y clúster de Service Fabric Hola.

Hay muchos tipos diferentes de operaciones que pueden realizarse mediante FabricClient.  Cada método puede producir excepciones para errores debidos tooincorrect entrada, errores en tiempo de ejecución o problemas de infraestructura transitorio.  Consulte toofind de documentación de referencia de hello API qué excepciones se producen por un método específico. Sin embargo, existen algunas excepciones que muchas API [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) diferentes pueden producir. Hello tabla siguiente enumeran las excepciones de Hola que son comunes a hello FabricClient APIs.

| Excepción | Se produce cuando |
| --- |:--- |
| [System.Fabric.FabricObjectClosedException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricobjectclosedexception#System_Fabric_FabricObjectClosedException) |Hola [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) objeto se encuentra en un estado cerrado. Deseche hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) objeto usa y crear instancias de un nuevo [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) objeto. |
| [System.TimeoutException](https://docs.microsoft.com/dotnet/core/api/system.timeoutexception#System_TimeoutException) |operación de Hello agotó el tiempo de espera. [OperationTimedOut](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) se devuelve cuando la operación de hello tarda más de toocomplete MaxOperationTimeout. |
| [System.UnauthorizedAccessException](https://docs.microsoft.com/dotnet/core/api/system.unauthorizedaccessexception#System_UnauthorizedAccessException) |Error de comprobación de acceso de Hello para la operación de Hola. Se devuelve E_ACCESSDENIED. |
| [System.Fabric.FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException) |Se ha producido un error en tiempo de ejecución al realizar la operación de Hola. Cualquiera de los métodos de hello FabricClient puede producir potencialmente [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException), hello [ErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException_ErrorCode) propiedad indica la causa exacta Hola de excepción de Hola. Códigos de error se definen en hello [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) enumeración. |
| [System.Fabric.FabricTransientException](https://docs.microsoft.com/dotnet/api/system.fabric.fabrictransientexception#System_Fabric_FabricTransientException) |Error en la operación de Hello debido tooa condición de error transitorio de algún tipo. Por ejemplo, se puede producir un error en la operación porque no se puede obtener acceso temporalmente a un cuórum de réplicas. Las excepciones transitorias corresponden a las operaciones de toofailed que se pueden recuperar. |

Algunos errores [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) frecuentes que pueden devolverse en [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException):

| Error | Condición |
| --- |:--- |
| CommunicationError |Un error de comunicación causa Hola operación toofail, operación de reintento de Hola. |
| InvalidCredentialType |tipo de credencial de Hello no es válido. |
| InvalidX509FindType |Hola X509FindType no es válido. |
| InvalidX509StoreLocation |ubicación del almacén de Hello X509 no es válido. |
| InvalidX509StoreName |nombre de la tienda de Hello X509 no es válido. |
| InvalidX509Thumbprint |cadena de huella digital de certificado de Hello X509 no es válido. |
| InvalidProtectionLevel |nivel de protección de Hello no es válido. |
| InvalidX509Store |no se puede abrir el almacén de certificados de Hello X509. |
| InvalidSubjectName |nombre de sujeto de Hello no es válido. |
| InvalidAllowedCommonNameList |Hola formato de cadena de lista de nombre común no es válido. Debe ser una lista separada por comas. |

