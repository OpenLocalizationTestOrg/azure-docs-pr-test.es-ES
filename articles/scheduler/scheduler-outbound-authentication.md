---
title: "Autenticación saliente de Programador"
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
ms.openlocfilehash: e345b2e22daae5b24c23645f7d2636f66df630ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="7eef6-103">Autenticación saliente de Programador</span><span class="sxs-lookup"><span data-stu-id="7eef6-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="7eef6-104">Puede que los trabajos de Programador tengan que llamar a servicios que requieren autenticación.</span><span class="sxs-lookup"><span data-stu-id="7eef6-104">Scheduler jobs may need to call out to services that require authentication.</span></span> <span data-ttu-id="7eef6-105">De este modo, un servicio llamado puede determinar si el trabajo de Programador puede tener acceso a sus recursos.</span><span class="sxs-lookup"><span data-stu-id="7eef6-105">This way, a called service can determine if the Scheduler job can access its resources.</span></span> <span data-ttu-id="7eef6-106">Algunos de estos servicios incluyen otros servicios de Azure, Salesforce.com, Facebook y sitios web personalizados que sean seguros.</span><span class="sxs-lookup"><span data-stu-id="7eef6-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="7eef6-107">Incorporación y eliminación de autenticación</span><span class="sxs-lookup"><span data-stu-id="7eef6-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="7eef6-108">La incorporación de autenticación a un trabajo de Programador es sencilla: agregue un elemento secundario JSON `authentication` al elemento `request` al crear o actualizar un trabajo.</span><span class="sxs-lookup"><span data-stu-id="7eef6-108">Adding authentication to a Scheduler job is simple – add a JSON child element `authentication` to the `request` element when creating or updating a job.</span></span> <span data-ttu-id="7eef6-109">Los secretos que se pasan al servicio Programador en una solicitud PUT, PATCH o POST, como parte del objeto `authentication` , nunca se devuelven en respuestas.</span><span class="sxs-lookup"><span data-stu-id="7eef6-109">Secrets passed to the Scheduler service in a PUT, PATCH, or POST request – as part of the `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="7eef6-110">En las respuestas, la información secreta se establece en null o puede que tenga un token público que represente la entidad autenticada.</span><span class="sxs-lookup"><span data-stu-id="7eef6-110">In responses, secret information is set to null or may have a public token that represents the authenticated entity.</span></span>

<span data-ttu-id="7eef6-111">Para quitar la autenticación, incluya explícitamente una solicitud PUT o PATCH en el trabajo, lo que establece el objeto `authentication` en null.</span><span class="sxs-lookup"><span data-stu-id="7eef6-111">To remove authentication, PUT or PATCH the job explicitly, setting the `authentication` object to null.</span></span> <span data-ttu-id="7eef6-112">No verá ninguna propiedad de autenticación en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="7eef6-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="7eef6-113">Actualmente, los únicos tipos de autenticación compatibles son el modelo `ClientCertificate` (para usar los certificados de cliente SSL/TLS), el modelo `Basic` (para la autenticación básica) y el modelo `ActiveDirectoryOAuth` (para autenticación ActiveDirectoryOAuth).</span><span class="sxs-lookup"><span data-stu-id="7eef6-113">Currently, the only supported authentication types are the `ClientCertificate` model (for using the SSL/TLS client certificates), the `Basic` model (for Basic authentication), and the `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="7eef6-114">Cuerpo de la solicitud en autenticación ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="7eef6-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="7eef6-115">Al agregar autenticación mediante el modelo `ClientCertificate` , especifique los siguientes elementos adicionales en el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="7eef6-115">When adding authentication using the `ClientCertificate` model, specify the following additional elements in the request body.</span></span>  

| <span data-ttu-id="7eef6-116">Elemento</span><span class="sxs-lookup"><span data-stu-id="7eef6-116">Element</span></span> | <span data-ttu-id="7eef6-117">Description</span><span class="sxs-lookup"><span data-stu-id="7eef6-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7eef6-118">*autenticación (elemento primario)*</span><span class="sxs-lookup"><span data-stu-id="7eef6-118">*authentication (parent element)*</span></span> |<span data-ttu-id="7eef6-119">Objeto de autenticación para usar un certificado de cliente SSL.</span><span class="sxs-lookup"><span data-stu-id="7eef6-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="7eef6-120">*type*</span><span class="sxs-lookup"><span data-stu-id="7eef6-120">*type*</span></span> |<span data-ttu-id="7eef6-121">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7eef6-121">Required.</span></span> <span data-ttu-id="7eef6-122">Tipo de autenticación. En certificados de cliente SSL, el valor debe ser `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="7eef6-122">Type of authentication.For SSL client certificates, the value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="7eef6-123">*pfx*</span><span class="sxs-lookup"><span data-stu-id="7eef6-123">*pfx*</span></span> |<span data-ttu-id="7eef6-124">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7eef6-124">Required.</span></span> <span data-ttu-id="7eef6-125">Contenido codificado en base 64 del archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="7eef6-125">Base64-encoded contents of the PFX file.</span></span> |
| <span data-ttu-id="7eef6-126">*password*</span><span class="sxs-lookup"><span data-stu-id="7eef6-126">*password*</span></span> |<span data-ttu-id="7eef6-127">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7eef6-127">Required.</span></span> <span data-ttu-id="7eef6-128">Contraseña de acceso al archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="7eef6-128">Password to access the PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="7eef6-129">Cuerpo de la respuesta en autenticación ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="7eef6-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="7eef6-130">Cuando se envía una solicitud con información de autenticación, la respuesta contiene los siguientes elementos relacionados con la autenticación.</span><span class="sxs-lookup"><span data-stu-id="7eef6-130">When a request is sent with authentication info, the response contains the following authentication-related elements.</span></span>

| <span data-ttu-id="7eef6-131">Elemento</span><span class="sxs-lookup"><span data-stu-id="7eef6-131">Element</span></span> | <span data-ttu-id="7eef6-132">Description</span><span class="sxs-lookup"><span data-stu-id="7eef6-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7eef6-133">*autenticación (elemento primario)*</span><span class="sxs-lookup"><span data-stu-id="7eef6-133">*authentication (parent element)*</span></span> |<span data-ttu-id="7eef6-134">Objeto de autenticación para usar un certificado de cliente SSL.</span><span class="sxs-lookup"><span data-stu-id="7eef6-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="7eef6-135">*type*</span><span class="sxs-lookup"><span data-stu-id="7eef6-135">*type*</span></span> |<span data-ttu-id="7eef6-136">Tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="7eef6-136">Type of authentication.</span></span> <span data-ttu-id="7eef6-137">Para los certificados de cliente SSL, el valor es `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="7eef6-137">For SSL client certificates, the value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="7eef6-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="7eef6-138">*certificateThumbprint*</span></span> |<span data-ttu-id="7eef6-139">Huella digital del certificado.</span><span class="sxs-lookup"><span data-stu-id="7eef6-139">The thumbprint of the certificate.</span></span> |
| <span data-ttu-id="7eef6-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="7eef6-140">*certificateSubjectName*</span></span> |<span data-ttu-id="7eef6-141">Nombre distintivo del sujeto del certificado.</span><span class="sxs-lookup"><span data-stu-id="7eef6-141">The subject distinguished name of the certificate.</span></span> |
| <span data-ttu-id="7eef6-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="7eef6-142">*certificateExpiration*</span></span> |<span data-ttu-id="7eef6-143">Fecha de expiración del certificado</span><span class="sxs-lookup"><span data-stu-id="7eef6-143">The expiration date of the certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="7eef6-144">Ejemplo de solicitud de REST para la autenticación ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="7eef6-144">Sample REST Request for ClientCertificate Authentication</span></span>
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

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="7eef6-145">Ejemplo de respuesta de REST para la autenticación ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="7eef6-145">Sample REST Response for ClientCertificate Authentication</span></span>
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

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="7eef6-146">Cuerpo de la solicitud en autenticación básica</span><span class="sxs-lookup"><span data-stu-id="7eef6-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="7eef6-147">Al agregar autenticación mediante el modelo `Basic` , especifique los siguientes elementos adicionales en el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="7eef6-147">When adding authentication using the `Basic` model, specify the following additional elements in the request body.</span></span>

| <span data-ttu-id="7eef6-148">Elemento</span><span class="sxs-lookup"><span data-stu-id="7eef6-148">Element</span></span> | <span data-ttu-id="7eef6-149">Description</span><span class="sxs-lookup"><span data-stu-id="7eef6-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7eef6-150">*autenticación (elemento primario)*</span><span class="sxs-lookup"><span data-stu-id="7eef6-150">*authentication (parent element)*</span></span> |<span data-ttu-id="7eef6-151">Objeto de autenticación para usar autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="7eef6-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="7eef6-152">*type*</span><span class="sxs-lookup"><span data-stu-id="7eef6-152">*type*</span></span> |<span data-ttu-id="7eef6-153">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7eef6-153">Required.</span></span> <span data-ttu-id="7eef6-154">Tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="7eef6-154">Type of authentication.</span></span> <span data-ttu-id="7eef6-155">En autenticación básica, el valor debe ser `Basic`.</span><span class="sxs-lookup"><span data-stu-id="7eef6-155">For Basic authentication, the value must be `Basic`.</span></span> |
| <span data-ttu-id="7eef6-156">*username*</span><span class="sxs-lookup"><span data-stu-id="7eef6-156">*username*</span></span> |<span data-ttu-id="7eef6-157">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7eef6-157">Required.</span></span> <span data-ttu-id="7eef6-158">Nombre de usuario para autenticar.</span><span class="sxs-lookup"><span data-stu-id="7eef6-158">Username to authenticate.</span></span> |
| <span data-ttu-id="7eef6-159">*password*</span><span class="sxs-lookup"><span data-stu-id="7eef6-159">*password*</span></span> |<span data-ttu-id="7eef6-160">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7eef6-160">Required.</span></span> <span data-ttu-id="7eef6-161">Contraseña para autenticar.</span><span class="sxs-lookup"><span data-stu-id="7eef6-161">Password to authenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="7eef6-162">Cuerpo de la respuesta en autenticación básica</span><span class="sxs-lookup"><span data-stu-id="7eef6-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="7eef6-163">Cuando se envía una solicitud con información de autenticación, la respuesta contiene los siguientes elementos relacionados con la autenticación.</span><span class="sxs-lookup"><span data-stu-id="7eef6-163">When a request is sent with authentication info, the response contains the following authentication-related elements.</span></span>

| <span data-ttu-id="7eef6-164">Elemento</span><span class="sxs-lookup"><span data-stu-id="7eef6-164">Element</span></span> | <span data-ttu-id="7eef6-165">Description</span><span class="sxs-lookup"><span data-stu-id="7eef6-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7eef6-166">*autenticación (elemento primario)*</span><span class="sxs-lookup"><span data-stu-id="7eef6-166">*authentication (parent element)*</span></span> |<span data-ttu-id="7eef6-167">Objeto de autenticación para usar autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="7eef6-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="7eef6-168">*type*</span><span class="sxs-lookup"><span data-stu-id="7eef6-168">*type*</span></span> |<span data-ttu-id="7eef6-169">Tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="7eef6-169">Type of authentication.</span></span> <span data-ttu-id="7eef6-170">En autenticación básica, el valor es `Basic`.</span><span class="sxs-lookup"><span data-stu-id="7eef6-170">For Basic authentication, the value is `Basic`.</span></span> |
| <span data-ttu-id="7eef6-171">*username*</span><span class="sxs-lookup"><span data-stu-id="7eef6-171">*username*</span></span> |<span data-ttu-id="7eef6-172">Nombre del usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="7eef6-172">The authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="7eef6-173">Ejemplo de solicitud de REST para la autenticación Basic</span><span class="sxs-lookup"><span data-stu-id="7eef6-173">Sample REST Request for Basic Authentication</span></span>
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

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="7eef6-174">Ejemplo de respuesta de REST para la autenticación Basic</span><span class="sxs-lookup"><span data-stu-id="7eef6-174">Sample REST Response for Basic Authentication</span></span>
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

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="7eef6-175">Cuerpo de la solicitud en autenticación ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="7eef6-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="7eef6-176">Al agregar autenticación mediante el modelo `ActiveDirectoryOAuth` , especifique los siguientes elementos adicionales en el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="7eef6-176">When adding authentication using the `ActiveDirectoryOAuth` model, specify the following additional elements in the request body.</span></span>

| <span data-ttu-id="7eef6-177">Elemento</span><span class="sxs-lookup"><span data-stu-id="7eef6-177">Element</span></span> | <span data-ttu-id="7eef6-178">Description</span><span class="sxs-lookup"><span data-stu-id="7eef6-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7eef6-179">*autenticación (elemento primario)*</span><span class="sxs-lookup"><span data-stu-id="7eef6-179">*authentication (parent element)*</span></span> |<span data-ttu-id="7eef6-180">Objeto de autenticación para usar autenticación ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="7eef6-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="7eef6-181">*type*</span><span class="sxs-lookup"><span data-stu-id="7eef6-181">*type*</span></span> |<span data-ttu-id="7eef6-182">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7eef6-182">Required.</span></span> <span data-ttu-id="7eef6-183">Tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="7eef6-183">Type of authentication.</span></span> <span data-ttu-id="7eef6-184">En autenticación ActiveDirectoryOAuth, el valor debe ser `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="7eef6-184">For ActiveDirectoryOAuth authentication, the value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="7eef6-185">*tenant*</span><span class="sxs-lookup"><span data-stu-id="7eef6-185">*tenant*</span></span> |<span data-ttu-id="7eef6-186">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7eef6-186">Required.</span></span> <span data-ttu-id="7eef6-187">Identificador del inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7eef6-187">The tenant identifier for the Azure AD tenant.</span></span> |
| <span data-ttu-id="7eef6-188">*audience*</span><span class="sxs-lookup"><span data-stu-id="7eef6-188">*audience*</span></span> |<span data-ttu-id="7eef6-189">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7eef6-189">Required.</span></span> <span data-ttu-id="7eef6-190">Esto se establece en https://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="7eef6-190">This is set to https://management.core.windows.net/.</span></span> |
| <span data-ttu-id="7eef6-191">*clientId*</span><span class="sxs-lookup"><span data-stu-id="7eef6-191">*clientId*</span></span> |<span data-ttu-id="7eef6-192">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7eef6-192">Required.</span></span> <span data-ttu-id="7eef6-193">Proporcione el identificador de cliente para la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7eef6-193">Provide the client identifier for the Azure AD application.</span></span> |
| <span data-ttu-id="7eef6-194">*secret*</span><span class="sxs-lookup"><span data-stu-id="7eef6-194">*secret*</span></span> |<span data-ttu-id="7eef6-195">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7eef6-195">Required.</span></span> <span data-ttu-id="7eef6-196">Secreto del cliente que solicita el token.</span><span class="sxs-lookup"><span data-stu-id="7eef6-196">Secret of the client that is requesting the token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="7eef6-197">Determinación del identificador del inquilino</span><span class="sxs-lookup"><span data-stu-id="7eef6-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="7eef6-198">Encontrará el identificador del inquilino de Azure AD ejecutando `Get-AzureAccount` en Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7eef6-198">You can find the tenant identifier for the Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="7eef6-199">Cuerpo de la respuesta en autenticación ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="7eef6-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="7eef6-200">Cuando se envía una solicitud con información de autenticación, la respuesta contiene los siguientes elementos relacionados con la autenticación.</span><span class="sxs-lookup"><span data-stu-id="7eef6-200">When a request is sent with authentication info, the response contains the following authentication-related elements.</span></span>

| <span data-ttu-id="7eef6-201">Elemento</span><span class="sxs-lookup"><span data-stu-id="7eef6-201">Element</span></span> | <span data-ttu-id="7eef6-202">Description</span><span class="sxs-lookup"><span data-stu-id="7eef6-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7eef6-203">*autenticación (elemento primario)*</span><span class="sxs-lookup"><span data-stu-id="7eef6-203">*authentication (parent element)*</span></span> |<span data-ttu-id="7eef6-204">Objeto de autenticación para usar autenticación ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="7eef6-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="7eef6-205">*type*</span><span class="sxs-lookup"><span data-stu-id="7eef6-205">*type*</span></span> |<span data-ttu-id="7eef6-206">Tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="7eef6-206">Type of authentication.</span></span> <span data-ttu-id="7eef6-207">En autenticación ActiveDirectoryOAuth, el valor es `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="7eef6-207">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="7eef6-208">*tenant*</span><span class="sxs-lookup"><span data-stu-id="7eef6-208">*tenant*</span></span> |<span data-ttu-id="7eef6-209">Identificador del inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7eef6-209">The tenant identifier for the Azure AD tenant.</span></span> |
| <span data-ttu-id="7eef6-210">*audience*</span><span class="sxs-lookup"><span data-stu-id="7eef6-210">*audience*</span></span> |<span data-ttu-id="7eef6-211">Esto se establece en https://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="7eef6-211">This is set to https://management.core.windows.net/.</span></span> |
| <span data-ttu-id="7eef6-212">*clientId*</span><span class="sxs-lookup"><span data-stu-id="7eef6-212">*clientId*</span></span> |<span data-ttu-id="7eef6-213">Identificador de cliente para la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7eef6-213">The client identifier for the Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="7eef6-214">Ejemplo de solicitud de REST para la autenticación ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="7eef6-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
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

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="7eef6-215">Ejemplo de respuesta de REST para la autenticación ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="7eef6-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
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

## <a name="see-also"></a><span data-ttu-id="7eef6-216">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="7eef6-216">See Also</span></span>
 [<span data-ttu-id="7eef6-217">¿Qué es Programador?</span><span class="sxs-lookup"><span data-stu-id="7eef6-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="7eef6-218">Conceptos, terminología y jerarquía de entidades de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="7eef6-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="7eef6-219">Introducción al Programador de Azure en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7eef6-219">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="7eef6-220">Planes y facturación en Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="7eef6-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="7eef6-221">Referencia de API de REST de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="7eef6-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="7eef6-222">Referencia de cmdlets de PowerShell de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="7eef6-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="7eef6-223">Alta disponibilidad y confiabilidad de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="7eef6-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="7eef6-224">Límites, valores predeterminados y códigos de error de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="7eef6-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

