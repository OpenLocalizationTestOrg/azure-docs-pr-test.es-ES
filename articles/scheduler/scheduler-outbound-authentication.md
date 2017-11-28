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
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="1c3c3-103">Autenticación saliente de Programador</span><span class="sxs-lookup"><span data-stu-id="1c3c3-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="1c3c3-104">Trabajos del programador que necesite toocall out tooservices que requieren autenticación.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-104">Scheduler jobs may need toocall out tooservices that require authentication.</span></span> <span data-ttu-id="1c3c3-105">De esta manera, un servicio llamado puede determinar si el trabajo del programador de hello puede tener acceso a sus recursos.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-105">This way, a called service can determine if hello Scheduler job can access its resources.</span></span> <span data-ttu-id="1c3c3-106">Algunos de estos servicios incluyen otros servicios de Azure, Salesforce.com, Facebook y sitios web personalizados que sean seguros.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="1c3c3-107">Incorporación y eliminación de autenticación</span><span class="sxs-lookup"><span data-stu-id="1c3c3-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="1c3c3-108">Agregar el trabajo del programador de autenticación tooa es sencillo: agregue un elemento secundario JSON `authentication` toohello `request` elemento al crear o actualizar un trabajo.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-108">Adding authentication tooa Scheduler job is simple – add a JSON child element `authentication` toohello `request` element when creating or updating a job.</span></span> <span data-ttu-id="1c3c3-109">Secretos pasan toohello servicio de programador en una solicitud PUT, PATCH o POST: como parte de hello `authentication` objeto: nunca se devuelven en respuestas.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-109">Secrets passed toohello Scheduler service in a PUT, PATCH, or POST request – as part of hello `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="1c3c3-110">En las respuestas, información secreta se establece toonull o puede tener un token público que representa la entidad de hello autenticado.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-110">In responses, secret information is set toonull or may have a public token that represents hello authenticated entity.</span></span>

<span data-ttu-id="1c3c3-111">tooremove autenticación, PUT o PATCH trabajo Hola explícitamente, establecer hello `authentication` toonull del objeto.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-111">tooremove authentication, PUT or PATCH hello job explicitly, setting hello `authentication` object toonull.</span></span> <span data-ttu-id="1c3c3-112">No verá ninguna propiedad de autenticación en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="1c3c3-113">Actualmente, Hola solo admitido tipos de autenticación están hello `ClientCertificate` modelo (para utilizar los certificados de cliente SSL/TLS hello), hello `Basic` de modelo (para la autenticación básica) y Hola `ActiveDirectoryOAuth` modelo (para OAuth de Active Directory autenticación).</span><span class="sxs-lookup"><span data-stu-id="1c3c3-113">Currently, hello only supported authentication types are hello `ClientCertificate` model (for using hello SSL/TLS client certificates), hello `Basic` model (for Basic authentication), and hello `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="1c3c3-114">Cuerpo de la solicitud en autenticación ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="1c3c3-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="1c3c3-115">Al agregar la autenticación mediante hello `ClientCertificate` del modelo, especificar Hola siguientes elementos adicionales en el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-115">When adding authentication using hello `ClientCertificate` model, specify hello following additional elements in hello request body.</span></span>  

| <span data-ttu-id="1c3c3-116">Elemento</span><span class="sxs-lookup"><span data-stu-id="1c3c3-116">Element</span></span> | <span data-ttu-id="1c3c3-117">Description</span><span class="sxs-lookup"><span data-stu-id="1c3c3-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1c3c3-118">*autenticación (elemento primario)*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-118">*authentication (parent element)*</span></span> |<span data-ttu-id="1c3c3-119">Objeto de autenticación para usar un certificado de cliente SSL.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="1c3c3-120">*type*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-120">*type*</span></span> |<span data-ttu-id="1c3c3-121">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-121">Required.</span></span> <span data-ttu-id="1c3c3-122">Tipo de autenticación. Para los certificados de cliente SSL, debe ser el valor de hello `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-122">Type of authentication.For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="1c3c3-123">*pfx*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-123">*pfx*</span></span> |<span data-ttu-id="1c3c3-124">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-124">Required.</span></span> <span data-ttu-id="1c3c3-125">Contenido con codificación base64 del archivo PFX de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-125">Base64-encoded contents of hello PFX file.</span></span> |
| <span data-ttu-id="1c3c3-126">*password*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-126">*password*</span></span> |<span data-ttu-id="1c3c3-127">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-127">Required.</span></span> <span data-ttu-id="1c3c3-128">Archivo de contraseña tooaccess hello PFX.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-128">Password tooaccess hello PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="1c3c3-129">Cuerpo de la respuesta en autenticación ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="1c3c3-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="1c3c3-130">Cuando se envía una solicitud con información de autenticación, respuesta de hello contiene Hola siguientes elementos relacionados con la autenticación.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-130">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="1c3c3-131">Elemento</span><span class="sxs-lookup"><span data-stu-id="1c3c3-131">Element</span></span> | <span data-ttu-id="1c3c3-132">Description</span><span class="sxs-lookup"><span data-stu-id="1c3c3-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1c3c3-133">*autenticación (elemento primario)*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-133">*authentication (parent element)*</span></span> |<span data-ttu-id="1c3c3-134">Objeto de autenticación para usar un certificado de cliente SSL.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="1c3c3-135">*type*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-135">*type*</span></span> |<span data-ttu-id="1c3c3-136">Tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-136">Type of authentication.</span></span> <span data-ttu-id="1c3c3-137">Para los certificados de cliente SSL, es el valor de hello `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-137">For SSL client certificates, hello value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="1c3c3-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-138">*certificateThumbprint*</span></span> |<span data-ttu-id="1c3c3-139">Hola huella digital del certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-139">hello thumbprint of hello certificate.</span></span> |
| <span data-ttu-id="1c3c3-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-140">*certificateSubjectName*</span></span> |<span data-ttu-id="1c3c3-141">Hola nombre distintivo del sujeto del certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-141">hello subject distinguished name of hello certificate.</span></span> |
| <span data-ttu-id="1c3c3-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-142">*certificateExpiration*</span></span> |<span data-ttu-id="1c3c3-143">fecha de expiración de Hello del certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-143">hello expiration date of hello certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="1c3c3-144">Ejemplo de solicitud de REST para la autenticación ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="1c3c3-144">Sample REST Request for ClientCertificate Authentication</span></span>
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

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="1c3c3-145">Ejemplo de respuesta de REST para la autenticación ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="1c3c3-145">Sample REST Response for ClientCertificate Authentication</span></span>
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

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="1c3c3-146">Cuerpo de la solicitud en autenticación básica</span><span class="sxs-lookup"><span data-stu-id="1c3c3-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="1c3c3-147">Al agregar la autenticación mediante hello `Basic` del modelo, especificar Hola siguientes elementos adicionales en el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-147">When adding authentication using hello `Basic` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="1c3c3-148">Elemento</span><span class="sxs-lookup"><span data-stu-id="1c3c3-148">Element</span></span> | <span data-ttu-id="1c3c3-149">Description</span><span class="sxs-lookup"><span data-stu-id="1c3c3-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1c3c3-150">*autenticación (elemento primario)*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-150">*authentication (parent element)*</span></span> |<span data-ttu-id="1c3c3-151">Objeto de autenticación para usar autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="1c3c3-152">*type*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-152">*type*</span></span> |<span data-ttu-id="1c3c3-153">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-153">Required.</span></span> <span data-ttu-id="1c3c3-154">Tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-154">Type of authentication.</span></span> <span data-ttu-id="1c3c3-155">Para la autenticación básica, debe ser el valor de hello `Basic`.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-155">For Basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="1c3c3-156">*username*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-156">*username*</span></span> |<span data-ttu-id="1c3c3-157">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-157">Required.</span></span> <span data-ttu-id="1c3c3-158">Tooauthenticate de nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-158">Username tooauthenticate.</span></span> |
| <span data-ttu-id="1c3c3-159">*password*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-159">*password*</span></span> |<span data-ttu-id="1c3c3-160">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-160">Required.</span></span> <span data-ttu-id="1c3c3-161">Tooauthenticate de contraseña.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-161">Password tooauthenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="1c3c3-162">Cuerpo de la respuesta en autenticación básica</span><span class="sxs-lookup"><span data-stu-id="1c3c3-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="1c3c3-163">Cuando se envía una solicitud con información de autenticación, respuesta de hello contiene Hola siguientes elementos relacionados con la autenticación.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-163">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="1c3c3-164">Elemento</span><span class="sxs-lookup"><span data-stu-id="1c3c3-164">Element</span></span> | <span data-ttu-id="1c3c3-165">Description</span><span class="sxs-lookup"><span data-stu-id="1c3c3-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1c3c3-166">*autenticación (elemento primario)*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-166">*authentication (parent element)*</span></span> |<span data-ttu-id="1c3c3-167">Objeto de autenticación para usar autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="1c3c3-168">*type*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-168">*type*</span></span> |<span data-ttu-id="1c3c3-169">Tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-169">Type of authentication.</span></span> <span data-ttu-id="1c3c3-170">Para la autenticación básica, es el valor de hello `Basic`.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-170">For Basic authentication, hello value is `Basic`.</span></span> |
| <span data-ttu-id="1c3c3-171">*username*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-171">*username*</span></span> |<span data-ttu-id="1c3c3-172">Hola autentica el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-172">hello authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="1c3c3-173">Ejemplo de solicitud de REST para la autenticación Basic</span><span class="sxs-lookup"><span data-stu-id="1c3c3-173">Sample REST Request for Basic Authentication</span></span>
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

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="1c3c3-174">Ejemplo de respuesta de REST para la autenticación Basic</span><span class="sxs-lookup"><span data-stu-id="1c3c3-174">Sample REST Response for Basic Authentication</span></span>
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

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="1c3c3-175">Cuerpo de la solicitud en autenticación ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="1c3c3-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="1c3c3-176">Al agregar la autenticación mediante hello `ActiveDirectoryOAuth` del modelo, especificar Hola siguientes elementos adicionales en el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-176">When adding authentication using hello `ActiveDirectoryOAuth` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="1c3c3-177">Elemento</span><span class="sxs-lookup"><span data-stu-id="1c3c3-177">Element</span></span> | <span data-ttu-id="1c3c3-178">Description</span><span class="sxs-lookup"><span data-stu-id="1c3c3-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1c3c3-179">*autenticación (elemento primario)*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-179">*authentication (parent element)*</span></span> |<span data-ttu-id="1c3c3-180">Objeto de autenticación para usar autenticación ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="1c3c3-181">*type*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-181">*type*</span></span> |<span data-ttu-id="1c3c3-182">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-182">Required.</span></span> <span data-ttu-id="1c3c3-183">Tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-183">Type of authentication.</span></span> <span data-ttu-id="1c3c3-184">Para la autenticación ActiveDirectoryOAuth, el valor de hello debe ser `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-184">For ActiveDirectoryOAuth authentication, hello value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="1c3c3-185">*tenant*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-185">*tenant*</span></span> |<span data-ttu-id="1c3c3-186">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-186">Required.</span></span> <span data-ttu-id="1c3c3-187">identificador del inquilino de Hello para el inquilino de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-187">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="1c3c3-188">*audience*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-188">*audience*</span></span> |<span data-ttu-id="1c3c3-189">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-189">Required.</span></span> <span data-ttu-id="1c3c3-190">Esto se establece toohttps://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-190">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="1c3c3-191">*clientId*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-191">*clientId*</span></span> |<span data-ttu-id="1c3c3-192">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-192">Required.</span></span> <span data-ttu-id="1c3c3-193">Proporcione el identificador de cliente de Hola para hello aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-193">Provide hello client identifier for hello Azure AD application.</span></span> |
| <span data-ttu-id="1c3c3-194">*secret*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-194">*secret*</span></span> |<span data-ttu-id="1c3c3-195">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-195">Required.</span></span> <span data-ttu-id="1c3c3-196">Secreto del cliente de Hola que solicita el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-196">Secret of hello client that is requesting hello token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="1c3c3-197">Determinación del identificador del inquilino</span><span class="sxs-lookup"><span data-stu-id="1c3c3-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="1c3c3-198">Puede encontrar el identificador del inquilino hello para el inquilino de hello Azure AD mediante la ejecución de `Get-AzureAccount` en PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-198">You can find hello tenant identifier for hello Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="1c3c3-199">Cuerpo de la respuesta en autenticación ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="1c3c3-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="1c3c3-200">Cuando se envía una solicitud con información de autenticación, respuesta de hello contiene Hola siguientes elementos relacionados con la autenticación.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-200">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="1c3c3-201">Elemento</span><span class="sxs-lookup"><span data-stu-id="1c3c3-201">Element</span></span> | <span data-ttu-id="1c3c3-202">Description</span><span class="sxs-lookup"><span data-stu-id="1c3c3-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1c3c3-203">*autenticación (elemento primario)*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-203">*authentication (parent element)*</span></span> |<span data-ttu-id="1c3c3-204">Objeto de autenticación para usar autenticación ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="1c3c3-205">*type*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-205">*type*</span></span> |<span data-ttu-id="1c3c3-206">Tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-206">Type of authentication.</span></span> <span data-ttu-id="1c3c3-207">Para la autenticación ActiveDirectoryOAuth, el valor de hello es `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-207">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="1c3c3-208">*tenant*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-208">*tenant*</span></span> |<span data-ttu-id="1c3c3-209">identificador del inquilino de Hello para el inquilino de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-209">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="1c3c3-210">*audience*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-210">*audience*</span></span> |<span data-ttu-id="1c3c3-211">Esto se establece toohttps://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-211">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="1c3c3-212">*clientId*</span><span class="sxs-lookup"><span data-stu-id="1c3c3-212">*clientId*</span></span> |<span data-ttu-id="1c3c3-213">Hola identificador de cliente de la aplicación hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-213">hello client identifier for hello Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="1c3c3-214">Ejemplo de solicitud de REST para la autenticación ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="1c3c3-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
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

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="1c3c3-215">Ejemplo de respuesta de REST para la autenticación ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="1c3c3-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
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

## <a name="see-also"></a><span data-ttu-id="1c3c3-216">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="1c3c3-216">See Also</span></span>
 [<span data-ttu-id="1c3c3-217">¿Qué es Programador?</span><span class="sxs-lookup"><span data-stu-id="1c3c3-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="1c3c3-218">Conceptos, terminología y jerarquía de entidades de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="1c3c3-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="1c3c3-219">Empezar a usar a Scheduler en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1c3c3-219">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="1c3c3-220">Planes y facturación en Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="1c3c3-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="1c3c3-221">Referencia de API de REST de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="1c3c3-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="1c3c3-222">Referencia de cmdlets de PowerShell de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="1c3c3-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="1c3c3-223">Alta disponibilidad y confiabilidad de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="1c3c3-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="1c3c3-224">Límites, valores predeterminados y códigos de error de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="1c3c3-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

