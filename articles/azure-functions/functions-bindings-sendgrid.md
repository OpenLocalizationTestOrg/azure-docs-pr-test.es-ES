---
title: enlaces de funciones SendGrid aaaAzure | Documentos de Microsoft
description: Referencia de enlaces de SendGrid de Azure Functions
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/16/2017
ms.author: rachelap
ms.openlocfilehash: 10a3837875eb6ae18e6c789bcf64cc401cf5f26a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="c342d-103">Enlaces de SendGrid de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="c342d-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="c342d-104">Este artículo se explica cómo tooconfigure y trabajar con enlaces de SendGrid en las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c342d-104">This article explains how tooconfigure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="c342d-105">Con SendGrid, puede utilizar correo electrónico de las funciones de Azure toosend personalizado mediante programación.</span><span class="sxs-lookup"><span data-stu-id="c342d-105">With SendGrid, you can use Azure Functions toosend customized email programmatically.</span></span>

<span data-ttu-id="c342d-106">Este artículo sirve como información de referencia para los desarrolladores de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c342d-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="c342d-107">Si está nuevas funciones de tooAzure, empiece con hello recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c342d-107">If you're new tooAzure Functions, start with hello following resources:</span></span>

<span data-ttu-id="c342d-108">[Cree la primera Azure Function](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="c342d-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="c342d-109">Referencias para desarrolladores de [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) o [nodo](functions-reference-node.md).</span><span class="sxs-lookup"><span data-stu-id="c342d-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="c342d-110">function.json para enlaces de SendGrid</span><span class="sxs-lookup"><span data-stu-id="c342d-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="c342d-111">Azure Functions proporciona un enlace de salida para SendGrid.</span><span class="sxs-lookup"><span data-stu-id="c342d-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="c342d-112">Hola SendGrid salida enlace permite toocreate y enviar correo electrónico mediante programación.</span><span class="sxs-lookup"><span data-stu-id="c342d-112">hello SendGrid output binding enables you toocreate and send email programmatically.</span></span> 

<span data-ttu-id="c342d-113">enlace de SendGrid Hola admite Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="c342d-113">hello SendGrid binding supports hello following properties:</span></span>

- <span data-ttu-id="c342d-114">`name`: Es obligatorio - Nombre de variable de saludo utilizado en código de la función para la solicitud de Hola o cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c342d-114">`name` : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="c342d-115">Este valor es ```$return``` cuando hay solo un valor de devuelto.</span><span class="sxs-lookup"><span data-stu-id="c342d-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="c342d-116">`type`: Es obligatorio - debe estar configurado demasiado "sendGrid".</span><span class="sxs-lookup"><span data-stu-id="c342d-116">`type` : Required - must be set too"sendGrid."</span></span>
- <span data-ttu-id="c342d-117">`direction`: Requerida: debe ser establecido demasiado "out".</span><span class="sxs-lookup"><span data-stu-id="c342d-117">`direction` : Required - must be set too"out."</span></span>
- <span data-ttu-id="c342d-118">`apiKey`: Requerida: debe ser el nombre de la clave de API que se almacena en la configuración de la aplicación de la aplicación de la función de hello toohello del conjunto de.</span><span class="sxs-lookup"><span data-stu-id="c342d-118">`apiKey` : Required - must be set toohello name of your API key stored in hello Function App's app settings.</span></span>
- <span data-ttu-id="c342d-119">`to`: Hola dirección de correo electrónico del destinatario.</span><span class="sxs-lookup"><span data-stu-id="c342d-119">`to` : hello recipient's email address.</span></span>
- <span data-ttu-id="c342d-120">`from`: Hola dirección de correo electrónico del remitente.</span><span class="sxs-lookup"><span data-stu-id="c342d-120">`from` : hello sender's email address.</span></span>
- <span data-ttu-id="c342d-121">`subject`: asunto Hola de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="c342d-121">`subject` : hello subject of hello email.</span></span>
- <span data-ttu-id="c342d-122">`text`: Hola contenido de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="c342d-122">`text` : hello email content.</span></span>

<span data-ttu-id="c342d-123">Ejemplo de **function.json**:</span><span class="sxs-lookup"><span data-stu-id="c342d-123">Example of **function.json**:</span></span>

```json 
{
    "bindings": [
        {
            "name": "$return",
            "type": "sendGrid",
            "direction": "out",
            "apiKey" : "MySendGridKey",
            "to": "{ToEmail}",
            "from": "{FromEmail}",
            "subject": "SendGrid output bindings"
        }
    ]
}
```

> [!NOTE]
> <span data-ttu-id="c342d-124">Azure Functions almacena la información de conexión y las claves de API como configuración de la aplicación de forma que no se protegen en el repositorio de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="c342d-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="c342d-125">Esta acción protege la información confidencial.</span><span class="sxs-lookup"><span data-stu-id="c342d-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="c342d-126">Enlace de salida de ejemplo de C# de hello SendGrid</span><span class="sxs-lookup"><span data-stu-id="c342d-126">C# example of hello SendGrid output binding</span></span>

```csharp
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static Mail Run(TraceWriter log, string input, out Mail message)
{
     message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    personalization.AddTo(new Email("recipient@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

## <a name="node-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="c342d-127">Nodo de hello SendGrid salida de ejemplo para enlazar</span><span class="sxs-lookup"><span data-stu-id="c342d-127">Node example of hello SendGrid output binding</span></span>

```javascript
module.exports = function (context, input) {    
    var message = {
         "personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
        from: "sender@contoso.com",        
        subject: "Azure news",
        content: [{
            type: 'text/plain',
            value: input
        }]
    };

    context.done(null, message);
};

```

## <a name="next-steps"></a><span data-ttu-id="c342d-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c342d-128">Next steps</span></span>
<span data-ttu-id="c342d-129">Para información sobre otros enlaces y desencadenadores de Azure Functions, consulte:</span><span class="sxs-lookup"><span data-stu-id="c342d-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="c342d-130">Referencia para desarrolladores de desencadenadores y enlaces de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="c342d-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="c342d-131">[Procedimientos recomendados para las funciones de Azure](functions-best-practices.md) enumera algunos toouse de prácticas recomendada al crear funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c342d-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="c342d-132">[Guía para desarrolladores de Azure Functions](functions-reference.md): contiene las referencias del programador para codificar las funciones y definir los desencadenadores y los enlaces.</span><span class="sxs-lookup"><span data-stu-id="c342d-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
