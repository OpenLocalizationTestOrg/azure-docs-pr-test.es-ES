---
title: "Protección de API mediante la autenticación de certificados de cliente en API Management - Azure API Management | Microsoft Docs"
description: "Obtenga información acerca de cómo proteger el acceso a las API mediante certificados de cliente."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: apimpm
ms.openlocfilehash: d3d51d0575a6d2dacced931601d48eb1e51a4051
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="695ba-103">Protección de API mediante la autenticación de certificados de cliente en API Management</span><span class="sxs-lookup"><span data-stu-id="695ba-103">How to secure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="695ba-104">API Management proporciona la capacidad de proteger el acceso a las API (es decir, de cliente a API Management) mediante certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="695ba-104">API Management provides the capability to secure access to APIs (i.e., client to API Management) using client certificates.</span></span> <span data-ttu-id="695ba-105">Actualmente, puede comprobar la huella digital de un certificado de cliente en relación con un valor deseado.</span><span class="sxs-lookup"><span data-stu-id="695ba-105">Currently, you can check the thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="695ba-106">También puede comprobar la huella digital en relación con certificados existentes que se hayan cargado en API Management.</span><span class="sxs-lookup"><span data-stu-id="695ba-106">You can also check the thumbprint against existing certificates uploaded to API Management.</span></span>  

<span data-ttu-id="695ba-107">Para obtener información acerca de cómo proteger el acceso al servicio de back-end de una API mediante certificados de cliente (por ejemplo, de API Management a back-end), consulte [Cómo asegurar servicios back-end con la autenticación de certificados de cliente en Administración de API de Azure](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="695ba-107">For information about securing access to the back-end service of an API using client certificates (i.e., API Management to back-end), see [How to secure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-the-expiration-date"></a><span data-ttu-id="695ba-108">Comprobación de la fecha de expiración</span><span class="sxs-lookup"><span data-stu-id="695ba-108">Checking the expiration date</span></span>

<span data-ttu-id="695ba-109">Las directivas siguientes pueden configurarse para comprobar si el certificado ha caducado:</span><span class="sxs-lookup"><span data-stu-id="695ba-109">Below policies can be configured to check if the certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-issuer-and-subject"></a><span data-ttu-id="695ba-110">Comprobación del emisor y el asunto</span><span class="sxs-lookup"><span data-stu-id="695ba-110">Checking the issuer and subject</span></span>

<span data-ttu-id="695ba-111">Es posible configurar las directivas siguientes para comprobar el emisor y el firmante de un certificado de cliente:</span><span class="sxs-lookup"><span data-stu-id="695ba-111">Below policies can be configured to check the issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-thumbprint"></a><span data-ttu-id="695ba-112">Comprobación de la huella digital</span><span class="sxs-lookup"><span data-stu-id="695ba-112">Checking the thumbprint</span></span>

<span data-ttu-id="695ba-113">Es posible configurar las directivas siguientes para comprobar la huella digital de un certificado de cliente:</span><span class="sxs-lookup"><span data-stu-id="695ba-113">Below policies can be configured to check the thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-to-api-management"></a><span data-ttu-id="695ba-114">Comprobación de una huella digital en relación con certificados cargados en API Management</span><span class="sxs-lookup"><span data-stu-id="695ba-114">Checking a thumbprint against certificates uploaded to API Management</span></span>

<span data-ttu-id="695ba-115">En el ejemplo siguiente se muestra cómo comprobar la huella digital de un certificado de cliente en relación con los certificados cargados en API Management:</span><span class="sxs-lookup"><span data-stu-id="695ba-115">The following example shows how to check the thumbprint of a client certificate against certificates uploaded to API Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="695ba-116">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="695ba-116">Next step</span></span>

*  [<span data-ttu-id="695ba-117">Cómo asegurar servicios back-end con la autenticación de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="695ba-117">How to secure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="695ba-118">¿Cómo se cargan certificados?</span><span class="sxs-lookup"><span data-stu-id="695ba-118">How to upload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

