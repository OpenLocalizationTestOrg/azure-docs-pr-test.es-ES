---
title: Enlaces de SendGrid de Azure Functions | Microsoft Docs
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
ms.openlocfilehash: 445a40a884e648cdb2a57f8ef43bed4f8a3efcf2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="715e0-103">Enlaces de SendGrid de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="715e0-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="715e0-104">En este artículo se explica cómo configurar y trabajar con enlaces de SendGrid en Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="715e0-104">This article explains how to configure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="715e0-105">Con SendGrid, puede usar Azure Functions para enviar correo electrónico personalizado mediante programación.</span><span class="sxs-lookup"><span data-stu-id="715e0-105">With SendGrid, you can use Azure Functions to send customized email programmatically.</span></span>

<span data-ttu-id="715e0-106">Este artículo sirve como información de referencia para los desarrolladores de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="715e0-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="715e0-107">Si está familiarizado con Funciones de Azure, comience con los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="715e0-107">If you're new to Azure Functions, start with the following resources:</span></span>

<span data-ttu-id="715e0-108">[Cree la primera Azure Function](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="715e0-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="715e0-109">Referencias para desarrolladores de [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) o [nodo](functions-reference-node.md).</span><span class="sxs-lookup"><span data-stu-id="715e0-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="715e0-110">function.json para enlaces de SendGrid</span><span class="sxs-lookup"><span data-stu-id="715e0-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="715e0-111">Azure Functions proporciona un enlace de salida para SendGrid.</span><span class="sxs-lookup"><span data-stu-id="715e0-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="715e0-112">El enlace de salida de SendGrid le permite crear y enviar correo electrónico mediante programación.</span><span class="sxs-lookup"><span data-stu-id="715e0-112">The SendGrid output binding enables you to create and send email programmatically.</span></span> 

<span data-ttu-id="715e0-113">El enlace de SendGrid admite las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="715e0-113">The SendGrid binding supports the following properties:</span></span>

- <span data-ttu-id="715e0-114">`name` (requerido): el nombre de variable que se usa en el código de función para la solicitud o el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="715e0-114">`name` : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="715e0-115">Este valor es ```$return``` cuando hay solo un valor de devuelto.</span><span class="sxs-lookup"><span data-stu-id="715e0-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="715e0-116">`type` (requerido): se debe establecer en "sendGrid".</span><span class="sxs-lookup"><span data-stu-id="715e0-116">`type` : Required - must be set to "sendGrid."</span></span>
- <span data-ttu-id="715e0-117">`direction` (requerido): se debe establecer en "out".</span><span class="sxs-lookup"><span data-stu-id="715e0-117">`direction` : Required - must be set to "out."</span></span>
- <span data-ttu-id="715e0-118">`apiKey` (requerido): se debe establecer en el nombre de la clave de API almacenada en la configuración de aplicación de Function App.</span><span class="sxs-lookup"><span data-stu-id="715e0-118">`apiKey` : Required - must be set to the name of your API key stored in the Function App's app settings.</span></span>
- <span data-ttu-id="715e0-119">`to`: dirección de correo electrónico del destinatario.</span><span class="sxs-lookup"><span data-stu-id="715e0-119">`to` : the recipient's email address.</span></span>
- <span data-ttu-id="715e0-120">`from`: dirección de correo electrónico del remitente.</span><span class="sxs-lookup"><span data-stu-id="715e0-120">`from` : the sender's email address.</span></span>
- <span data-ttu-id="715e0-121">`subject` : el asunto del correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="715e0-121">`subject` : the subject of the email.</span></span>
- <span data-ttu-id="715e0-122">`text` : el contenido del correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="715e0-122">`text` : the email content.</span></span>

<span data-ttu-id="715e0-123">Ejemplo de **function.json**:</span><span class="sxs-lookup"><span data-stu-id="715e0-123">Example of **function.json**:</span></span>

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
> <span data-ttu-id="715e0-124">Azure Functions almacena la información de conexión y las claves de API como configuración de la aplicación de forma que no se protegen en el repositorio de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="715e0-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="715e0-125">Esta acción protege la información confidencial.</span><span class="sxs-lookup"><span data-stu-id="715e0-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="715e0-126">Ejemplo de C# del enlace de salida de SendGrid</span><span class="sxs-lookup"><span data-stu-id="715e0-126">C# example of the SendGrid output binding</span></span>

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

## <a name="node-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="715e0-127">Ejemplo de nodo del enlace de salida de SendGrid</span><span class="sxs-lookup"><span data-stu-id="715e0-127">Node example of the SendGrid output binding</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="715e0-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="715e0-128">Next steps</span></span>
<span data-ttu-id="715e0-129">Para información sobre otros enlaces y desencadenadores de Azure Functions, consulte:</span><span class="sxs-lookup"><span data-stu-id="715e0-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="715e0-130">Referencia para desarrolladores de desencadenadores y enlaces de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="715e0-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="715e0-131">[Procedimientos recomendados de Azure Functions](functions-best-practices.md): se enumeran algunos procedimientos recomendados para crear Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="715e0-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="715e0-132">[Guía para desarrolladores de Azure Functions](functions-reference.md): contiene las referencias del programador para codificar las funciones y definir los desencadenadores y los enlaces.</span><span class="sxs-lookup"><span data-stu-id="715e0-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
