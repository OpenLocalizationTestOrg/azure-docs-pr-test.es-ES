---
title: "aaaSecure API mediante la autenticación de certificado de cliente en administración de API - Administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toosecure tener acceso a tooAPIs mediante certificados de cliente"
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
ms.openlocfilehash: 6ff78bda3d429829da79d0dc4d652f19669cc919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="cf593-103">Cómo toosecure API con cliente de certificado autenticación de administración de API</span><span class="sxs-lookup"><span data-stu-id="cf593-103">How toosecure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="cf593-104">Administración de API proporciona Hola capacidad toosecure acceso tooAPIs (es decir, cliente tooAPI administración) mediante certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="cf593-104">API Management provides hello capability toosecure access tooAPIs (i.e., client tooAPI Management) using client certificates.</span></span> <span data-ttu-id="cf593-105">Actualmente, puede comprobar la huella digital de Hola de un certificado de cliente con un valor deseado.</span><span class="sxs-lookup"><span data-stu-id="cf593-105">Currently, you can check hello thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="cf593-106">También puede comprobar la huella digital de hello en los certificados existentes cargado tooAPI administración.</span><span class="sxs-lookup"><span data-stu-id="cf593-106">You can also check hello thumbprint against existing certificates uploaded tooAPI Management.</span></span>  

<span data-ttu-id="cf593-107">Para obtener información acerca de cómo proteger el servicio de back-end de toohello de acceso de una API que usan certificados de cliente (es decir, administración de API tooback-end), vea [cómo toosecure servicios de back-end con cliente de certificado autenticación](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="cf593-107">For information about securing access toohello back-end service of an API using client certificates (i.e., API Management tooback-end), see [How toosecure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-hello-expiration-date"></a><span data-ttu-id="cf593-108">Comprobación de la fecha de expiración de Hola</span><span class="sxs-lookup"><span data-stu-id="cf593-108">Checking hello expiration date</span></span>

<span data-ttu-id="cf593-109">Por debajo de directivas puede ser toocheck configurado si ha caducado el certificado de hello:</span><span class="sxs-lookup"><span data-stu-id="cf593-109">Below policies can be configured toocheck if hello certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a><span data-ttu-id="cf593-110">Comprobación de asunto y emisor Hola</span><span class="sxs-lookup"><span data-stu-id="cf593-110">Checking hello issuer and subject</span></span>

<span data-ttu-id="cf593-111">Por debajo de directivas puede ser configurado toocheck Hola emisor y el asunto de un certificado de cliente:</span><span class="sxs-lookup"><span data-stu-id="cf593-111">Below policies can be configured toocheck hello issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a><span data-ttu-id="cf593-112">Comprobación de huella digital de Hola</span><span class="sxs-lookup"><span data-stu-id="cf593-112">Checking hello thumbprint</span></span>

<span data-ttu-id="cf593-113">Por debajo de las directivas puede ser la huella digital de Hola de toocheck configurado de un certificado de cliente:</span><span class="sxs-lookup"><span data-stu-id="cf593-113">Below policies can be configured toocheck hello thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a><span data-ttu-id="cf593-114">Comprobar una huella digital contra certificados cargado tooAPI administración</span><span class="sxs-lookup"><span data-stu-id="cf593-114">Checking a thumbprint against certificates uploaded tooAPI Management</span></span>

<span data-ttu-id="cf593-115">Hello en el ejemplo siguiente se muestra cómo la huella digital de hello toocheck de un certificado de cliente con certificados había cargado tooAPI administración:</span><span class="sxs-lookup"><span data-stu-id="cf593-115">hello following example shows how toocheck hello thumbprint of a client certificate against certificates uploaded tooAPI Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="cf593-116">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="cf593-116">Next step</span></span>

*  [<span data-ttu-id="cf593-117">¿Cómo toosecure servicios de back-end con cliente de certificado autenticación</span><span class="sxs-lookup"><span data-stu-id="cf593-117">How toosecure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="cf593-118">Cómo certificados tooupload</span><span class="sxs-lookup"><span data-stu-id="cf593-118">How tooupload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

