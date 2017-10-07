---
title: "aaaScheduler autenticación de salida"
description: "Autenticación saliente de Programador"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 6707f82b-7e32-401b-a960-02aae7bb59cc
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2016
ms.author: deli
ms.openlocfilehash: ef713f4770b48d0a9176415e87c1042a823582e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-outbound-authentication"></a>Autenticación saliente de Programador
Trabajos del programador que necesite toocall out tooservices que requieren autenticación. De esta manera, un servicio llamado puede determinar si el trabajo del programador de hello puede tener acceso a sus recursos. Algunos de estos servicios incluyen otros servicios de Azure, Salesforce.com, Facebook y sitios web personalizados que sean seguros.

## <a name="adding-and-removing-authentication"></a>Incorporación y eliminación de autenticación
Agregar el trabajo del programador de autenticación tooa es sencillo: agregue un elemento secundario JSON `authentication` toohello `request` elemento al crear o actualizar un trabajo. Secretos pasan toohello servicio de programador en una solicitud PUT, PATCH o POST: como parte de hello `authentication` objeto: nunca se devuelven en respuestas. En las respuestas, información secreta se establece toonull o puede tener un token público que representa la entidad de hello autenticado.

tooremove autenticación, PUT o PATCH trabajo Hola explícitamente, establecer hello `authentication` toonull del objeto. No verá ninguna propiedad de autenticación en la respuesta.

Actualmente, Hola solo admitido tipos de autenticación están hello `ClientCertificate` modelo (para utilizar los certificados de cliente SSL/TLS hello), hello `Basic` de modelo (para la autenticación básica) y Hola `ActiveDirectoryOAuth` modelo (para OAuth de Active Directory autenticación).

## <a name="request-body-for-clientcertificate-authentication"></a>Cuerpo de la solicitud en autenticación ClientCertificate
Al agregar la autenticación mediante hello `ClientCertificate` del modelo, especificar Hola siguientes elementos adicionales en el cuerpo de la solicitud de saludo.  

| Elemento | Description |
|:--- |:--- |
| *autenticación (elemento primario)* |Objeto de autenticación para usar un certificado de cliente SSL. |
| *type* |Necesario. Tipo de autenticación. Para los certificados de cliente SSL, debe ser el valor de hello `ClientCertificate`. |
| *pfx* |Necesario. Contenido con codificación base64 del archivo PFX de Hola. |
| *password* |Necesario. Archivo de contraseña tooaccess hello PFX. |

## <a name="response-body-for-clientcertificate-authentication"></a>Cuerpo de la respuesta en autenticación ClientCertificate
Cuando se envía una solicitud con información de autenticación, respuesta de hello contiene Hola siguientes elementos relacionados con la autenticación.

| Elemento | Description |
|:--- |:--- |
| *autenticación (elemento primario)* |Objeto de autenticación para usar un certificado de cliente SSL. |
| *type* |Tipo de autenticación. Para los certificados de cliente SSL, es el valor de hello `ClientCertificate`. |
| *certificateThumbprint* |Hola huella digital del certificado de Hola. |
| *certificateSubjectName* |Hola nombre distintivo del sujeto del certificado de Hola. |
| *certificateExpiration* |fecha de expiración de Hello del certificado de Hola. |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a>Ejemplo de solicitud de REST para la autenticación ClientCertificate
```
PUT https://management.azure.com/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "clientcertificate",
          "password": "password",
          "pfx": "pfx key"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-clientcertificate-authentication"></a>Ejemplo de respuesta de REST para la autenticación ClientCertificate
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 858
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 56c7b40e-721a-437e-88e6-f68562a73aa8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 1075219e-e879-4030-bc81-094e54fbabce
x-ms-routing-request-id: WESTUS:20160316T190424Z:1075219e-e879-4030-bc81-094e54fbabce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:04:23 GMT

{
  "id": "/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
  "type": "Microsoft.Scheduler/jobCollections/jobs",
  "name": "southeastasiajc/httpjob",
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "certificateThumbprint": "88105CG9DF9ADE75B835711D899296CB217D7055",
          "certificateExpiration": "2021-01-01T07:00:00Z",
          "certificateSubjectName": "CN=Scheduler Mgmt",
          "type": "ClientCertificate"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
    "status": {
      "nextExecutionTime": "2016-03-16T19:05:00Z",
      "executionCount": 0,
      "failureCount": 0,
      "faultedCount": 0
    }
  }
}
```

## <a name="request-body-for-basic-authentication"></a>Cuerpo de la solicitud en autenticación básica
Al agregar la autenticación mediante hello `Basic` del modelo, especificar Hola siguientes elementos adicionales en el cuerpo de la solicitud de saludo.

| Elemento | Description |
|:--- |:--- |
| *autenticación (elemento primario)* |Objeto de autenticación para usar autenticación básica. |
| *type* |Obligatorio. Tipo de autenticación. Para la autenticación básica, debe ser el valor de hello `Basic`. |
| *username* |Necesario. Tooauthenticate de nombre de usuario. |
| *password* |Necesario. Tooauthenticate de contraseña. |

## <a name="response-body-for-basic-authentication"></a>Cuerpo de la respuesta en autenticación básica
Cuando se envía una solicitud con información de autenticación, respuesta de hello contiene Hola siguientes elementos relacionados con la autenticación.

| Elemento | Description |
|:--- |:--- |
| *autenticación (elemento primario)* |Objeto de autenticación para usar autenticación básica. |
| *type* |Tipo de autenticación. Para la autenticación básica, es el valor de hello `Basic`. |
| *username* |Hola autentica el nombre de usuario. |

## <a name="sample-rest-request-for-basic-authentication"></a>Ejemplo de solicitud de REST para la autenticación Basic
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 562
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "basic",
          "username": "user",
          "password": "password"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-basic-authentication"></a>Ejemplo de respuesta de REST para la autenticación Basic
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 701
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: a2dcb9cd-1aea-4887-8893-d81273a8cf04
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 7816f222-6ea7-468d-b919-e6ddebbd7e95
x-ms-routing-request-id: WESTUS:20160316T190506Z:7816f222-6ea7-468d-b919-e6ddebbd7e95
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:05:06 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "username":"user1",
               "type":"Basic"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "nextExecutionTime":"2016-03-16T19:06:00Z",
         "executionCount":0,
         "failureCount":0,
         "faultedCount":0
      }
   }
}
```

## <a name="request-body-for-activedirectoryoauth-authentication"></a>Cuerpo de la solicitud en autenticación ActiveDirectoryOAuth
Al agregar la autenticación mediante hello `ActiveDirectoryOAuth` del modelo, especificar Hola siguientes elementos adicionales en el cuerpo de la solicitud de saludo.

| Elemento | Description |
|:--- |:--- |
| *autenticación (elemento primario)* |Objeto de autenticación para usar autenticación ActiveDirectoryOAuth. |
| *type* |Obligatorio. Tipo de autenticación. Para la autenticación ActiveDirectoryOAuth, el valor de hello debe ser `ActiveDirectoryOAuth`. |
| *tenant* |Necesario. identificador del inquilino de Hello para el inquilino de hello Azure AD. |
| *audience* |Necesario. Esto se establece toohttps://management.core.windows.net/. |
| *clientId* |Necesario. Proporcione el identificador de cliente de Hola para hello aplicación de Azure AD. |
| *secret* |Necesario. Secreto del cliente de Hola que solicita el token de Hola. |

### <a name="determining-your-tenant-identifier"></a>Determinación del identificador del inquilino
Puede encontrar el identificador del inquilino hello para el inquilino de hello Azure AD mediante la ejecución de `Get-AzureAccount` en PowerShell de Azure.

## <a name="response-body-for-activedirectoryoauth-authentication"></a>Cuerpo de la respuesta en autenticación ActiveDirectoryOAuth
Cuando se envía una solicitud con información de autenticación, respuesta de hello contiene Hola siguientes elementos relacionados con la autenticación.

| Elemento | Description |
|:--- |:--- |
| *autenticación (elemento primario)* |Objeto de autenticación para usar autenticación ActiveDirectoryOAuth. |
| *type* |Tipo de autenticación. Para la autenticación ActiveDirectoryOAuth, el valor de hello es `ActiveDirectoryOAuth`. |
| *tenant* |identificador del inquilino de Hello para el inquilino de hello Azure AD. |
| *audience* |Esto se establece toohttps://management.core.windows.net/. |
| *clientId* |Hola identificador de cliente de la aplicación hello Azure AD. |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a>Ejemplo de solicitud de REST para la autenticación ActiveDirectoryOAuth
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 757
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "tenant":"microsoft.onmicrosoft.com",
          "audience":"https://management.core.windows.net/",
          "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
          "secret": "G6u071r8Gjw4V4KSibnb+VK4+tX399hkHaj7LOyHuj5=",
          "type":"ActiveDirectoryOAuth"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a>Ejemplo de respuesta de REST para la autenticación ActiveDirectoryOAuth
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 885
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 86d8e9fd-ac0d-4bed-9420-9baba1af3251
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
x-ms-routing-request-id: WESTUS:20160316T191003Z:5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:10:02 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "tenant":"microsoft.onmicrosoft.com",
               "audience":"https://management.core.windows.net/",
               "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
               "type":"ActiveDirectoryOAuth"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "lastExecutionTime":"2016-03-16T19:10:00.3762123Z",
         "nextExecutionTime":"2016-03-16T19:11:00Z",
         "executionCount":5,
         "failureCount":5,
         "faultedCount":1
      }
   }
}
```

## <a name="see-also"></a>Otras referencias
 [¿Qué es Programador?](scheduler-intro.md)

 [Conceptos, terminología y jerarquía de entidades de Programador de Azure](scheduler-concepts-terms.md)

 [Empezar a usar a Scheduler en hello portal de Azure](scheduler-get-started-portal.md)

 [Planes y facturación en Programador de Azure](scheduler-plans-billing.md)

 [Referencia de API de REST de Programador de Azure](https://msdn.microsoft.com/library/mt629143)

 [Referencia de cmdlets de PowerShell de Programador de Azure](scheduler-powershell-reference.md)

 [Alta disponibilidad y confiabilidad de Programador de Azure](scheduler-high-availability-reliability.md)

 [Límites, valores predeterminados y códigos de error de Programador de Azure](scheduler-limits-defaults-errors.md)

