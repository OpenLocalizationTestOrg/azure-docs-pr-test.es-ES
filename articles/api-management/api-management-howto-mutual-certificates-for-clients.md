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
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a>Cómo toosecure API con cliente de certificado autenticación de administración de API

Administración de API proporciona Hola capacidad toosecure acceso tooAPIs (es decir, cliente tooAPI administración) mediante certificados de cliente. Actualmente, puede comprobar la huella digital de Hola de un certificado de cliente con un valor deseado. También puede comprobar la huella digital de hello en los certificados existentes cargado tooAPI administración.  

Para obtener información acerca de cómo proteger el servicio de back-end de toohello de acceso de una API que usan certificados de cliente (es decir, administración de API tooback-end), vea [cómo toosecure servicios de back-end con cliente de certificado autenticación](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)

## <a name="checking-hello-expiration-date"></a>Comprobación de la fecha de expiración de Hola

Por debajo de directivas puede ser toocheck configurado si ha caducado el certificado de hello:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a>Comprobación de asunto y emisor Hola

Por debajo de directivas puede ser configurado toocheck Hola emisor y el asunto de un certificado de cliente:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a>Comprobación de huella digital de Hola

Por debajo de las directivas puede ser la huella digital de Hola de toocheck configurado de un certificado de cliente:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a>Comprobar una huella digital contra certificados cargado tooAPI administración

Hello en el ejemplo siguiente se muestra cómo la huella digital de hello toocheck de un certificado de cliente con certificados había cargado tooAPI administración: 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a>Paso siguiente

*  [¿Cómo toosecure servicios de back-end con cliente de certificado autenticación](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [Cómo certificados tooupload](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

